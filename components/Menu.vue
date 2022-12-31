<template>
  <div
    class="w-full md:w-1/6 bg-gray-900 md:bg-gray-900 px-2 text-center fixed bottom-0 md:pt-8 md:top-0 md:left-0 h-16 md:h-screen md:border-r-4 md:border-gray-600"
  >
    <div class="md:relative mx-auto lg:float-right lg:px-6">
      <p
        class="text-white text-center p-2 text-lg uppercase font-bold hidden md:block"
      >
        Dream Book
      </p>
      <ul class="list-reset flex flex-row md:flex-col text-center md:text-left">
        <li class="mr-3 flex-1">
          <NuxtLink
            to="/"
            class="flex py-1 md:py-3 pl-1 align-middle text-gray-800 no-underline hover:text-pink-500 border-b-2 border-gray-800 md:border-gray-900 hover:border-pink-500"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-7 h-7 pr-2 text-white"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M8.25 6.75h12M8.25 12h12m-12 5.25h12M3.75 6.75h.007v.008H3.75V6.75zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zM3.75 12h.007v.008H3.75V12zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zm-.375 5.25h.007v.008H3.75v-.008zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z"
              />
            </svg>

            <span
              class="pb-1 md:pb-0 text-lg uppercase md:text-base text-white font-bold md:text-gray-400 block md:inline-block"
            >Dreams</span>
          </NuxtLink>
        </li>
        <li class="mr-3 flex-1">
          <NuxtLink
            v-if="!$auth.user"
            to="/auth/login"
            class="flex py-1 md:py-3 pl-1 align-middle text-gray-800 no-underline hover:text-pink-500 border-b-2 border-gray-800 md:border-gray-900 hover:border-pink-500"
          >
            <span
              class="pb-1 md:pb-0 text-lg uppercase md:text-base text-white font-bold md:text-gray-400 block md:inline-block"
            >Login</span>
          </NuxtLink>
          <NuxtLink
            v-if="$auth.user"
            to="/auth/logout"
            class="flex py-1 md:py-3 pl-1 align-middle text-gray-800 no-underline hover:text-pink-500 border-b-2 border-gray-800 md:border-gray-900 hover:border-pink-500"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-7 h-7 pr-2 text-white"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M15.75 9V5.25A2.25 2.25 0 0013.5 3h-6a2.25 2.25 0 00-2.25 2.25v13.5A2.25 2.25 0 007.5 21h6a2.25 2.25 0 002.25-2.25V15M12 9l-3 3m0 0l3 3m-3-3h12.75"
              />
            </svg>

            <span
              class="pb-1 md:pb-0 text-lg uppercase md:text-base text-white font-bold md:text-gray-400 block md:inline-block"
            >Logout</span>
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: 'AppMenu'
}
</script>
