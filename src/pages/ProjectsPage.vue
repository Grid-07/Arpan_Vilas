<template>
  <div class="page">
    <Navigation />
    <Projects />
    <Footer />
  </div>
</template>

<script>
import Navigation from '../components/Navigation.vue'
import Projects from '../components/Projects.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'ProjectsPage',
  components: {
    Navigation,
    Projects,
    Footer
  }
}
</script>

<style scoped>
.page {
  min-height: 100vh;
}
</style>
