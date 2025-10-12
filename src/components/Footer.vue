<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>BIMLA MANGAL GARDENSH</h3>
          <p>A HOME THAT YOU DESERVE</p>
          <br>
          <p>Experience luxury living in the heart of Ranchi with world-class amenities and premium construction quality.</p>
        </div>
        <div class="footer-section">
          <h4>Architect</h4>
          <p>GRIDS CONSULTANTS<br>2ND FLOOR, ROSHPA TOWER, MAIN ROAD, RANCHI</p>
        </div>
        <div class="footer-section">
          <h4>Quick Links</h4>
          <a href="#floor-plans" @click="scrollToSection('floor-plans')">Floor Plans</a>
          <a href="#amenities" @click="scrollToSection('amenities')">Amenities</a>
          <a href="#where-we-work" @click="scrollToSection('where-we-work')">Where We Work</a>
          <a href="#contact" @click="scrollToSection('contact')">Contact</a>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2025 ARPAN MEGA STRUCTURE. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  setup() {
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

    return {
      scrollToSection
    }
  }
}
</script>
