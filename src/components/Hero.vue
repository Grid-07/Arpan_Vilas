<template>
  <section id="hero" class="hero">
    <div class="hero-bg-animation"></div>
    <div class="hero-particles"></div>
    
    <!-- Hero Image Gallery -->
    <div class="hero-image-gallery">
      <div class="hero-main-image">
        <img 
          src="/images/building-frontal-view.jpg" 
          alt="BIMLA MANGAL GARDENS - Premium 3BHK apartments frontal view showcasing modern architecture and luxury living in Bihar Sharif"
          class="hero-image"
        />
        <div class="image-overlay"></div>
      </div>
      <div class="hero-secondary-images">
        <img 
          src="/images/building-overview.jpg" 
          alt="BIMLA MANGAL GARDENS building overview showing twin towers with premium amenities and open spaces"
          class="secondary-image"
        />
        <img 
          src="/images/courtyard-pool-view.jpg" 
          alt="Luxury swimming pool area in BIMLA MANGAL GARDENS courtyard with modern amenities"
          class="secondary-image"
        />
      </div>
    </div>
    
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-title">
          <span class="title-main">BIMLA MANGAL GARDENS</span>
          <span class="title-sub">A HOME THAT YOU DESERVE</span>
        </h1>
        <p class="hero-description">
          Experience luxury living in 108 exquisitely designed 3BHK homes with 62% open space and premium amenities and comercial space.
        </p>
        <div class="hero-buttons">
          <button class="btn btn--primary btn--3d btn--hero" @click="scrollToSection('floor-plans')">
            <span>Explore Floor Plans</span>
            <div class="btn-ripple"></div>
          </button>
          <button class="btn btn--secondary btn--3d btn--hero" @click="scrollToSection('contact')">
            <span>Book Site Visit</span>
            <div class="btn-ripple"></div>
          </button>
        </div>
      </div>
      <div class="hero-stats">
        <div class="stat-item">
          <span class="stat-number" ref="stat1">{{ animatedStats.flats }}</span>
          <span class="stat-label">Premium Flats</span>
        </div>
        <div class="stat-item">
          <span class="stat-number" ref="stat2">{{ animatedStats.towers }}</span>
          <span class="stat-label">Towers</span>
        </div>
        <div class="stat-item">
          <span class="stat-number" ref="stat3">{{ animatedStats.openSpace }}</span>
          <span class="stat-label">% Open Space</span>
        </div>
      </div>
    </div>
    <div class="scroll-indicator">
      <div class="scroll-arrow"></div>
    </div>
  </section>
</template>

<script>
import { ref, reactive, onMounted } from 'vue'

export default {
  name: 'Hero',
  setup() {
    const animatedStats = reactive({
      flats: 0,
      towers: 0,
      openSpace: 0
    })

    const scrollToSection = (sectionId) => {
      const element = document.getElementById(sectionId)
      if (element) {
        const offsetTop = element.offsetTop - 80
        window.scrollTo({
          top: offsetTop,
          behavior: 'smooth'
        })
      }
    }

    const animateCounter = (target, property, duration = 2000) => {
      const increment = target / (duration / 16)
      let current = 0
      
      const updateCounter = () => {
        current += increment
        if (current < target) {
          animatedStats[property] = Math.floor(current)
          requestAnimationFrame(updateCounter)
        } else {
          animatedStats[property] = target
        }
      }
      
      updateCounter()
    }

    onMounted(() => {
      setTimeout(() => {
        animateCounter(28, 'flats')
        animateCounter(2, 'towers')
        animateCounter(62, 'openSpace')
      }, 1000)
    })

    return {
      animatedStats,
      scrollToSection
    }
  }
}
</script>
