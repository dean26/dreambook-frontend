<template>
  <div>
    <h1 class="text-3xl font-bold underline mb-2">
      Hello {{ $auth.user.user.name }}
    </h1>
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
      <div class="p-4">
        <label for="table-search" class="sr-only">Search</label>
        <div class="relative mt-1">
          <div
            class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none"
          >
            <svg
              class="w-5 h-5 text-gray-500 dark:text-gray-400"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                clip-rule="evenodd"
              />
            </svg>
          </div>
          <input
            id="table-search"
            v-model="queryString"
            v-debounce:300ms="queryStringWatch"
            type="text"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-80 pl-10 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Search for items"
          >
        </div>
      </div>
      <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead
          class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
        >
          <tr>
            <th scope="col" class="p-4">
              <div class="flex items-center">
                <input
                  id="checkbox-all-search"
                  type="checkbox"
                  class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
                >
                <label
                  for="checkbox-all-search"
                  class="sr-only"
                >checkbox</label>
              </div>
            </th>
            <th scope="col" class="px-6 py-3">
              Data
            </th>
            <th scope="col" class="px-6 py-3">
              Description
            </th>
            <th scope="col" class="px-6 py-3">
              Actions
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="dream in dreams.data"
            :key="dream.id"
            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600"
          >
            <td class="w-4 p-4">
              <div class="flex items-center">
                <input
                  id="checkbox-table-search-1"
                  type="checkbox"
                  class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
                >
                <label
                  for="checkbox-table-search-1"
                  class="sr-only"
                >checkbox</label>
              </div>
            </td>
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap"
            >
              {{ dream.day }}
            </th>
            <td class="px-6 py-4">
              {{ dream.description }}
              <div v-if="dream.tags" class="mt-1 flex">
                <nuxt-link
                  v-for="tag in dream.tags"
                  :key="tag.id"
                  aria-current="tag"
                  :to="`/?tag=${tag.name}`"
                >
                  <div
                    class="mr-2 text-xs inline-flex items-center font-bold leading-sm uppercase px-2 py-1 bg-orange-200 text-orange-700 rounded-full"
                  >
                    {{ tag.name }}
                  </div>
                </nuxt-link>
              </div>
            </td>
            <td class="px-6 py-4 text-right">
              <a
                href="#"
                class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
              >Edit</a>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <Pagination v-if="dreams.meta" :meta="dreams.meta" />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: 'default',
  async asyncData (context) {
    const page = context.query.page ?? 1
    const tag = context.query.tag ?? null

    let searchParams = `?page=${page}`
    if (tag) {
      searchParams += `&tag=${tag}`
    }

    const dreams = await context.$axios.$get(`/api/dreams${searchParams}`)
    return { dreams }
  },
  data () {
    return {
      queryString: ''
    }
  },
  watch: {
    async queryString (value) {}
  },
  watchQuery: ['page', 'tag'],
  methods: {
    async queryStringWatch (value, e) {
      if (value.length > 1) {
        this.dreams = await this.$axios.$get(`/api/dreams?query=${value}`)
      } else {
        this.dreams = await this.$axios.$get('/api/dreams')
      }
    }
  }
}
</script>
