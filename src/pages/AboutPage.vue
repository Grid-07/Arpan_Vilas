<template>
  <div class="page">
    <Navigation />
    <Overview />
    <Footer />
  </div>
</template>

<script>
import Navigation from '../components/Navigation.vue'
import Overview from '../components/Overview.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'AboutPage',
  components: {
    Navigation,
    Overview,
    Footer
  }
}
</script>

<style scoped>
.page {
  min-height: 100vh;
}
</style>
