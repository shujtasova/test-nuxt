<template>
  <footer class="bg-[rgba(248,213,195,1)] flex flex-col pt-35 pl-28 ">
    <div>
      <p class="text-base">Is there a project?</p>
    </div>
    <div class="flex justify-between gap-60 pb-36">
      <a href="/#" class="block text-black underline decoration-[1px] underline-offset-[20px] text-[112px] transition-colors duration-100 hover:text-[#5A2D0C]">
        Let’s work together
      </a>

      <div class="flex flex-col gap-9 pr-80">
        <div class="text-base">
          <p>For all questions</p>
          <a href="tel:+79202780068" class="block hover:underline">+7 (920) 278-00-68</a>
          <a href="mailto:qtim@agency.com" class="block hover:underline">qtim@agency.com</a>
        </div>

        <div class="text-base">
          <p>Office in Russia</p>
          <p>139 Ruben Station Lake Drew, NM 52678</p>
          <button class="rounded-full p-[10px] bg-black" @click="openMap">
            <img src="~assets/icons/location.webp" alt="location-pointer" class="h-[12px] w-[12px]">
          </button>
        </div>

        <div class="text-base">
          <p>Office in Dubai</p>
          <p>139 Ruben Station Lake Drew, NM 52678</p>
          <button class="rounded-full p-[10px] bg-black" @click="openMap">
            <img src="~assets/icons/location.webp" alt="location-pointer" class="h-[12px] w-[12px]">
          </button>
        </div>
      </div>
    </div>

    <div class="flex justify-between items-end pr-28">
      <div class="flex gap-8 pb-[30px]">
        <a href="/#" class="hover:underline">Facebook</a>
        <a href="/#" class="hover:underline">Instagram</a>
        <a href="/#" class="hover:underline">Telegram</a>
      </div>

      <div>
        <a href="/#">
          <img src="~assets/icons/button.webp" alt="location-pointer" class=" w-[358px]">
        </a>
      </div>


      <div class="flex gap-8 pb-[30px]">
        <a href="/#" class="hover:underline">Behance</a>
        <a href="/#" class="hover:underline">Linkedin</a>
        <a href="/#" class="hover:underline">Privacy Policy</a>
      </div>

    </div>
    
  </footer>
</template>

<script setup lang="ts">
const openMap = () => {
  const address = encodeURIComponent("139 Ruben Station Lake Drew, NM 52678");
  window.open(`https://www.google.com/maps/search/?api=1&query=${address}`, "_blank");
};

</script>

  