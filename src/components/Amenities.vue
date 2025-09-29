<template>
  <section id="amenities" class="amenities">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">World-Class Amenities</h2>
        <p class="section-subtitle">Experience luxury living with premium amenities designed for your comfort and convenience</p>
      </div>

      <div class="amenities-grid">
        <div class="amenity-card" v-for="amenity in amenities" :key="amenity.id">
          <div class="amenity-icon">{{ amenity.icon }}</div>
          <h4>{{ amenity.name }}</h4>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Amenities',
  setup() {
    const amenities = ref([
      { id: 1, icon: '🏘️', name: 'Club House' },
      { id: 2, icon: '🏃‍♂️', name: 'Jogging Track' },
      { id: 3, icon: '🎠', name: 'Children Park' },
      { id: 4, icon: '💪', name: 'Gym & Yoga Center' },
      { id: 5, icon: '🛡️', name: '24 Hour Security' },
      { id: 6, icon: '📹', name: 'CCTV Surveillance' },
      { id: 7, icon: '🚗', name: 'Visitor Parking' },
      { id: 8, icon: '⚡', name: 'Power Backup' },
      { id: 9, icon: '🔥', name: 'Fire Safety' },
      { id: 10, icon: '🛗', name: 'Lift Facility' },
      { id: 11, icon: '🏊‍♂️', name: 'Swimming Pool' },
      { id: 12, icon: '🌳', name: 'Beautiful Landscaping' }
    ])

    return {
      amenities
    }
  }
}
</script>
