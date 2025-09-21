<template>
  <section id="overview" class="overview">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Project Overview</h2>
        <p class="section-subtitle">
          ARPAN VILASH is a mantra of exclusivity, serenity and calm. These exquisite homes are open, perfectly planned fluid spaces designed to enhance the lives of those who inhabit them.
        </p>
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
        <p class="location-address">Arpan Colony, Tetartoli Talab, Near RIMS, Ranchi</p>
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
        title: '108 Premium Flats',
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
        title: 'CNT Free',
        description: 'Hassle-free ownership with clear title'
      },
      {
        id: 4,
        icon: '🌳',
        title: '62% Open Space',
        description: 'Abundant green spaces for a peaceful environment'
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
