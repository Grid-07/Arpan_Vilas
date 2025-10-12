<template>
  <div class="page">
    <Navigation />
    <FloorPlans />
    <Footer />
  </div>
</template>

<script>
import Navigation from '../components/Navigation.vue'
import FloorPlans from '../components/FloorPlans.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'FloorPlansPage',
  components: {
    Navigation,
    FloorPlans,
    Footer
  }
}
</script>

<style scoped>
.page {
  min-height: 100vh;
}
</style>
