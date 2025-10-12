<template>
  <div class="page">
    <Navigation />
    <Contact />
    <Footer />
  </div>
</template>

<script>
import Navigation from '../components/Navigation.vue'
import Contact from '../components/Contact.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'ContactPage',
  components: {
    Navigation,
    Contact,
    Footer
  }
}
</script>

<style scoped>
.page {
  min-height: 100vh;
}
</style>
