<template>
  <div id="app">
    <Navigation />
    <Hero />
    <Overview />
    <FloorPlans />
    <Amenities />
    <WhereWeWork />
    <Contact />
    <Footer />
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue'
import Hero from './components/Hero.vue'
import Overview from './components/Overview.vue'
import FloorPlans from './components/FloorPlans.vue'
import Amenities from './components/Amenities.vue'
import WhereWeWork from './components/WhereWeWork.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Hero,
    Overview,
    FloorPlans,
    Amenities,
    WhereWeWork,
    Contact,
    Footer
  }
}
</script>

<style>
#app {
  font-family: 'Inter', Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
