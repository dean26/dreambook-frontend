<template>
  <div class="mt-4 mb-4">
    <nav aria-label="Page navigation example">
      <span class="text-sm text-gray-700 dark:text-gray-400 block">
        Showing
        <span class="font-semibold text-gray-900 dark:text-white">
          {{ meta.from }}
        </span>
        to
        <span class="font-semibold text-gray-900 dark:text-white">
          {{ meta.to }}
        </span>
        of
        <span class="font-semibold text-gray-900 dark:text-white">
          {{ meta.total }}</span>
        Entries
      </span>
      <ul class="inline-flex items-center -space-x-px">
        <li v-for="link in meta.links" :key="link.label">
          <nuxt-link
            aria-current="page"
            class="block px-3 py-2 ml-0 leading-tight text-gray-500 border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
            :to="`/${getParamsFromUrl(link.url)}`"
            :class="{
              'bg-gray-200':
                $route.query.page &&
                $route.query.page == getPageNoFromUrl(link.url)
            }"
          >
            <span v-html="link.label" />
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'PaginationLinks',
  props: ['meta'],
  methods: {
    getParamsFromUrl (url) {
      if (url && url !== 'null') {
        return '?' + url.split('?').pop()
      }
      return ''
    },
    getPageNoFromUrl (url) {
      if (url && url !== 'null') {
        const urlParams = new URL(url)
        return urlParams.searchParams.get('page') ?? 1
      }
      return null
    }
  }
}
</script>
