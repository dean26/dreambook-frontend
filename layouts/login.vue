<template>
  <div class="bg-white font-family-karla h-screen">
    <vue-up />
    <div class="w-full flex flex-wrap">
      <!-- Login Section -->
      <Nuxt />

      <!-- Image Section -->
      <div class="w-1/2 shadow-2xl">
        <img
          class="object-cover w-full h-screen hidden md:block"
          src="~/assets/images/universe.webp"
        >
      </div>
    </div>
  </div>
</template>
