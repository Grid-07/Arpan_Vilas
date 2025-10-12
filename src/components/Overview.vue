<template>
  <section id="overview" class="overview">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Project Overview</h2>
        <p class="section-subtitle">
          BIMLA MANGAL GARDENSH is a mantra of exclusivity, serenity and calm. These exquisite homes are open, perfectly planned fluid spaces designed to enhance the lives of those who inhabit them.
        </p>
      </div>
      
      <!-- Project Images Gallery -->
      <div class="project-gallery">
        <div class="gallery-main">
          <img 
            src="/images/building-facade-detail.jpg" 
            alt="Detailed facade view of BIMLA MANGAL GARDENS showing premium architectural design and modern building materials"
            class="gallery-main-image"
          />
        </div>
        <div class="gallery-secondary">
          <img 
            src="/images/courtyard-passage.jpg" 
            alt="Interior courtyard passage at BIMLA MANGAL GARDENS showcasing beautiful landscaping and walkways"
            class="gallery-secondary-image"
          />
          <img 
            src="/images/street-view.jpg" 
            alt="Street view of BIMLA MANGAL GARDENS building showing prime location and accessibility in Bihar Sharif"
            class="gallery-secondary-image"
          />
        </div>
      </div>
      
      <div class="overview-grid">
        <div class="overview-card" v-for="feature in features" :key="feature.id">
          <div class="card-icon">{{ feature.icon }}</div>
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.description }}</p>
        </div>
      </div>

      <div class="location-info">
        <h3>Prime Location</h3>
        <p class="location-address">Maghra, Bihar Sharif</p>
        <button class="btn btn--outline btn--3d" @click="showMapNotification">
          View on Map
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Overview',
  setup() {
    const features = ref([
      {
        id: 1,
        icon: '🏢',
        title: '28 Premium Flats',
        description: 'Spacious 3BHK apartments designed for modern living'
      },
      {
        id: 2,
        icon: '🏗️',
        title: '2 Towers',
        description: 'Twin tower architecture with optimal space utilization'
      },
      {
        id: 3,
        icon: '✅',
        title: '10+ Premium Amenities',
        description: 'Serene Walking Track, Swimming Pool, Clubhouse and more'
      },
      {
        id: 4,
        icon: '🌳',
        title: 'Luxury Living',
        description: 'Ample Open Space'
      }
    ])

    const showMapNotification = () => {
      alert('Map functionality will be available soon. Please contact us for directions.')
    }

    return {
      features,
      showMapNotification
    }
  }
}
</script>
