<template>
  <div class="page">
    <Navigation />
    <Hero />
    <Overview />
    <Projects />
    <FloorPlans />
    <Amenities />
    <WhereWeWork />
    <Contact />
    <Footer />
  </div>
</template>

<script>
import Navigation from '../components/Navigation.vue'
import Hero from '../components/Hero.vue'
import Overview from '../components/Overview.vue'
import Projects from '../components/Projects.vue'
import FloorPlans from '../components/FloorPlans.vue'
import Amenities from '../components/Amenities.vue'
import WhereWeWork from '../components/WhereWeWork.vue'
import Contact from '../components/Contact.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'HomePage',
  components: {
    Navigation,
    Hero,
    Overview,
    Projects,
    FloorPlans,
    Amenities,
    WhereWeWork,
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
