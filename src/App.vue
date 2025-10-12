<template>
  <div id="app">
    <router-view />
    <WhatsAppPopup />
  </div>
</template>

<script>
import WhatsAppPopup from './components/WhatsAppPopup.vue'

export default {
  name: 'App',
  components: {
    WhatsAppPopup
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
