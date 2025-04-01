<template>
    <div class="flex mt-12 space-x-2">
        <button
            v-if="currentPage > 1"
            @click="$emit('changePage', 'Previous')"
            class="w-11 h-11 flex items-center justify-center rounded-lg border border-[rgba(232,232,232,1)] transition-colors duration-200 bg-[rgba(255, 255, 255, 1)] hover:bg-[rgba(232,232,232,1)]"
        >
            <img src="~assets/icons/arrow.webp" class="h-6 w-6 rotate-180">
        </button>
  
        <button
            v-for="button in paginationButtons"
            :key="button"
            @click="$emit('changePage', button)"
            :disabled="button === '...' || button === currentPage"
            class="w-11 h-11 rounded-lg transition-colors duration-200"
            :class="{
              'bg-[rgba(16,16,16,1)] text-white': button === currentPage,
              'bg-[rgba(243,243,243,1)] hover:bg-[rgba(232,232,232,1)]': button !== currentPage && button !== '...',
              'cursor-default': button === '...',
            }"
        >
            {{ button }}
        </button>
  
        <button
            v-if="currentPage < totalPages"
            @click="$emit('changePage', 'Next')"
            class="w-11 h-11 flex items-center justify-center rounded-lg border border-[rgba(232,232,232,1)] transition-colors duration-200 bg-[rgba(255, 255, 255, 1)] hover:bg-[rgba(232,232,232,1)]"
        >
            <img src="~assets/icons/arrow.webp" class="h-6 w-6">
        </button>
    </div>
</template>
  
<script setup lang="ts">
import { computed, defineProps } from 'vue';
  
const props = defineProps<{ currentPage: number; totalPages: number }>();
  
const paginationButtons = computed(() => {
    const buttons: (number | string)[] = [];
  
    if (props.totalPages <= 6) {
        for (let i = 1; i <= props.totalPages; i++) {
          buttons.push(i);
        }
    } else {
      if (props.currentPage <= 3) {
          buttons.push(1, 2, 3, '...', props.totalPages);
      } else if (props.currentPage >= props.totalPages - 2) {
          buttons.push(1, '...', props.totalPages - 2, props.totalPages - 1, props.totalPages);
      } else {
          buttons.push(1, '...', props.currentPage - 1, props.currentPage, props.currentPage + 1, '...', props.totalPages);
      }
    }
  
    return buttons;
});
</script>