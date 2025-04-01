<template>
    <div class="w-[280px]">
        <router-link
            :to="{ name: 'articles-id', params: { id }, state: { image } }"
            @click="saveImageToLocalStorage"
        >
            <img
                :src="image"
                alt="Article image"
                class="w-[280px] h-[280px] object-cover pb-6 transform transition-transform duration-300 hover:scale-105"
            />
            <p
                ref="textElement"
                class="text-[rgba(16,16,16,1)] text-[20px] leading-[28px] overflow-hidden"
                :style="{ maxHeight: isTruncated ? '84px' : 'none' }"
            >
                {{ preview }}
            </p>
        </router-link>

        <button
            v-if="shouldShowButton"
            @click="toggleDescription"
            :style="{ color: 'rgba(248, 213, 195, 1)' }"
            class="hover:underline text-[20px]"
        >
            {{ isTruncated ? "Read more" : "Read less" }}
        </button>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick, defineProps } from 'vue';

interface Props {
    preview: string;
    image: string;
    id?: string;
}

const props = defineProps<Props>();
const isTruncated = ref(true);
const shouldShowButton = ref(false);
const textElement = ref<HTMLElement | null>(null);

const checkTextOverflow = () => {
    if (textElement.value) {
        const lineHeight = 28;
        const maxLines = 3;
        const maxHeight = lineHeight * maxLines;
        
        shouldShowButton.value = textElement.value.scrollHeight > maxHeight;
    }
};

const toggleDescription = () => {
    isTruncated.value = !isTruncated.value;
};

const saveImageToLocalStorage = () => {
    localStorage.setItem(`article_image_${props.id}`, props.image);
};

onMounted(async () => {
    await nextTick();
    checkTextOverflow();
});
</script>