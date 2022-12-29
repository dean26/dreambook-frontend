<template>
  <div>
    <h1 class="text-3xl font-bold underline">
      Logout...
    </h1>
  </div>
</template>

<script>
export default {
  name: 'AboutPage',
  middleware: 'auth',

  async created () {
    try {
      await this.$auth.logout()
      this.$router.push('/auth/login')
    } catch (err) {
      this.$popup({
        message: err.response?.data?.message,
        delay: 3,
        backgroundColor: 'rgb(255,0,0,0.5)',
        color: '#fff'
      })
    }
  }
}
</script>
