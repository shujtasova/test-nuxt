<template>
    <div class="mx-auto pt-[120px] pl-[112px] pr-[112px] pb-[140px] m-0">
        <h2 class="text-[84px] pb-9">Articles</h2>
        <div v-if="isLoading" class="text-center text-gray-500">Loading...</div>
        <div v-else-if="error" class="text-red-500">{{ error }}</div>
        <div v-else class="grid grid-cols-4 gap-8">
            <ArticleCard
                v-for="post in paginatedPosts"
                :key="post.id"
                :id="post.id"
                :preview="post.preview"
                :image="imageMap[post.id] || plugImage"
            />
        </div>

        <Pagination
            :currentPage="currentPage"
            :totalPages="totalPages"
            @changePage="changePage"
        />
    </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import ArticleCard from './ArticleCard.vue';
import Pagination from './Pagination.vue';
import plugImage from '@/assets/img/plug.webp';

const posts = ref<Post[]>([]);
const makeupImages = ref<string[]>([]);
const imageMap = ref<Record<string, string>>({});
const isLoading = ref(true);
const error = ref<string | null>(null);
const currentPage = ref(1);
const postsPerPage = 8;
const apiKey = 'OQ1HwFjBTu4aDP3Fv3yqvVbcSNtTSYVMFbUV-UebRI8';

const fetchPosts = async () => {
    try {
        const response = await fetch('https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/');
        if (!response.ok) throw new Error('Ошибка загрузки данных');
        const data = await response.json();
        posts.value = data;
        await fetchMakeupImages();
    } catch (err) {
        error.value = (err as Error).message;
    } finally {
        isLoading.value = false;
    }
};

const fetchMakeupImages = async () => {
    try {
        let allImages: string[] = [];
        for (let page = 1; page <= 3; page++) {
            const response = await fetch(`https://api.unsplash.com/search/photos?query=makeup&client_id=${apiKey}&per_page=30&page=${page}`);
            const data = await response.json();
            allImages = allImages.concat(data.results.map((photo: { urls: { regular: string } }) => photo.urls.regular));
        }

        posts.value.forEach((post, index) => {
            imageMap.value[post.id] = allImages[index] || plugImage;
        });
    } catch (error) {
        console.error(error);
    }
};

onMounted(() => {
    fetchPosts();
});

const paginatedPosts = computed(() => {
    const start = (currentPage.value - 1) * postsPerPage;
    return posts.value.slice(start, start + postsPerPage).map((post, index) => ({
        ...post,
        image: makeupImages.value[start + index] || plugImage,
    }));
});

const totalPages = computed(() => Math.ceil(posts.value.length / postsPerPage));
const changePage = (page: number | string) => {
    if (page === 'Next' && currentPage.value < totalPages.value) {
        currentPage.value++;
    } else if (page === 'Previous' && currentPage.value > 1) {
        currentPage.value--;
    } else if (typeof page === 'number') {
        currentPage.value = page;
    }
};
</script>  