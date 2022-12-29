<template>
  <div>
    <h1 class="text-3xl font-bold underline">
      About {{ $auth.user.user.email }}
    </h1>
    <p>
      <a href="#" @click.prevent="logout">Logout</a>
    </p>
  </div>
</template>

<script>
export default {
  name: 'AboutPage',
  middleware: 'auth',
  data () {
    return {
      user: this.$auth.user.user
    }
  },
  methods: {
    async logout () {
      await this.$auth.logout()

      this.$router.push('/auth/login')
    }
  }
}
</script>
