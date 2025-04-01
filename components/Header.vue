<template>
    <header class="p-10">
        <nav class="flex justify-between items-center">
            <NuxtLink to="/">
                <img src="~assets/icons/logo-payot.webp" alt="PAYOT logo" class="h-8 w-auto">
            </NuxtLink>
            <div>
                <div class="flex gap-24 items-center">
                    <div class="space-x-4 text-[20px]">
                        <NuxtLink to="/works" class="hover:text-[#F8D5C3]">Works</NuxtLink>
                        <NuxtLink to="/about" class="hover:text-[#F8D5C3]">About</NuxtLink>
                    </div>
                    <div class="flex gap-4">
                        <button class="border-2 border-[rgba(0,0,0,0.1)] rounded-full p-[10px] transform transition-transform duration-300 hover:scale-105">
                            <img src="~assets/icons/en.webp" alt="language-switcher" class="h-8 w-auto">
                        </button>
                        <button class="bg-[rgba(16,16,16,1)] text-white rounded-full px-8 py-2 text-[20px] transform transition-transform duration-300 hover:scale-105">
                            Let's work
                        </button>
                    </div>
                </div>
            </div>
        </nav>
    </header>
</template>