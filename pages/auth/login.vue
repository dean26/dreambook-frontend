<template>
  <div class="w-full md:w-1/2 flex flex-col">
    <div class="flex justify-center md:justify-start pt-12 md:pl-12 md:-mb-24">
      <span
        href="#"
        class="bg-black text-white font-bold text-xl p-4"
      >Lucas DreamBook</span>
    </div>

    <div
      class="flex flex-col justify-center md:justify-start my-auto pt-8 md:pt-0 px-8 md:px-24 lg:px-32"
    >
      <div
        v-if="error"
        class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
        role="alert"
      >
        <strong class="font-bold">Wystąpił błąd</strong>
        <span class="block sm:inline">{{ error }}</span>
      </div>

      <form
        class="flex flex-col pt-3 md:pt-8"
        method="post"
        @submit.prevent="login"
      >
        <div class="flex flex-col pt-4">
          <label for="email" class="text-lg">Email</label>
          <input
            id="email"
            v-model="email"
            type="email"
            placeholder="your@email.com"
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mt-1 leading-tight focus:outline-none focus:shadow-outline"
          >
        </div>

        <div class="flex flex-col pt-4">
          <label for="password" class="text-lg">Password</label>
          <input
            id="password"
            v-model="password"
            type="password"
            placeholder="Password"
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mt-1 leading-tight focus:outline-none focus:shadow-outline"
          >
        </div>

        <button
          class="bg-black text-white font-bold text-lg hover:bg-gray-700 p-2 mt-8"
          native-type="submit"
        >
          Login
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginPage',
  layout: 'login',
  middleware: false,

  data () {
    return {
      email: '',
      password: '',
      error: ''
    }
  },

  mounted () {
    this.$axios.$get('/sanctum/csrf-cookie')
  },

  methods: {
    async login () {
      this.error = ''
      try {
        await this.$auth.loginWith('laravelSanctum', {
          data: {
            email: this.email,
            password: this.password
          }
        })
        this.$router.push('/')
      } catch (err) {
        this.error = err.response?.data?.message
      }
    }
  }
}
</script>
