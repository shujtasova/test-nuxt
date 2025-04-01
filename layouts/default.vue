<template>
    <div class="flex flex-col min-h-screen justify-between">
        <Header />
  
        <main>
            <slot />
        </main>

        <Footer />
    </div>
</template>

<script setup>
import Footer from '@/components/Footer.vue';
import Header from '~/components/Header.vue';
</script>