<template>
    <div class="article">
        <div class="flex pl-28 pr-45 pt-[119px] justify-between gap-8">
            <h2 class="text-[84px] w-1/2">{{ article.title }}</h2>
            <p class="text-4xl w-1/2">{{ article.preview }}</p>
        </div>

        <div class="pt-10 pl-28 pr-28 flex justify-center">
            <img :src="article.image" alt="Article image" class="h-[700px] mt-6 mb-8" />
        </div>

        <div class="flex pl-80 pr-80 pt-[80px] pb-[125px] align-center flex-col gap-8">
            <h3 class="text-base">About</h3>
            <p class="text-4xl">{{ article.description }}</p>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch, nextTick } from 'vue';
import { useRoute } from 'vue-router';
import plugImage from '@/assets/img/plug.webp';

const route = useRoute();
const article = ref({
    title: '',
    preview: '',
    description: '',
    image: '',
});

const loadImageFromLocalStorage = () => {
    const savedImage = localStorage.getItem(`article_image_${route.params.id}`);
    if (savedImage) {
        article.value.image = savedImage;
    } else {
        article.value.image = plugImage;
    }
};

const loadArticleData = async (id: string) => {
    try {
        const response = await fetch(`https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/${id}`);
        const data = await response.json();
        article.value = {
            ...data,
            image: article.value.image || plugImage,
        };
    } catch (error) {
        console.error(error);
    }
};

onMounted(async () => {
    loadImageFromLocalStorage(); // загружаем изображение сразу после монтирования компонента
    await nextTick(); // ждем, пока компонент отрендерится, затем грузим статью
    loadArticleData(route.params.id); // загружаем остальные данные статьи
});

watch(() => route.params.id, (newId) => {
    loadImageFromLocalStorage();
    loadArticleData(newId);
});
</script>

