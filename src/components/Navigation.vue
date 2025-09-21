<!-- <template>
  <nav class="navbar" :class="{ 'navbar--scrolled': isScrolled }">
    <div class="nav-container">
      <div class="nav-logo">
        <h2>ARPAN VILASH</h2>
      </div>
      <div class="nav-links">
        <a href="#hero" class="nav-link" @click="scrollToSection('hero')">Home</a>
        <a href="#overview" class="nav-link" @click="scrollToSection('overview')">About</a>
        <a href="#floor-plans" class="nav-link" @click="scrollToSection('floor-plans')">Projects</a>
        <a href="#contact" class="nav-link" @click="scrollToSection('contact')">Contact Us</a>
      </div>
      <button class="btn btn--primary btn--3d nav-cta" @click="scrollToSection('contact')">
        Book Visits
      </button>
    </div>
  </nav>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'Navigation',
  setup() {
    const isScrolled = ref(false)

    const handleScroll = () => {
      isScrolled.value = window.scrollY > 100
    }

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

    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
    })

    return {
      isScrolled,
      scrollToSection
    }
  }
}
</script>

<style scoped>
.navbar--scrolled {
  background: rgba(255, 255, 255, 0.98) !important;
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(51, 51, 51, 0.15);
}
</style> -->
<template>
  <nav class="navbar" :class="{ 'navbar--scrolled': isScrolled }">
    <div class="nav-container">
      <div class="nav-logo">
        <h2>ARPAN VILASH</h2>
      </div>
      
      <!-- Mobile menu button -->
      <button 
        class="mobile-menu-btn" 
        @click="toggleMobileMenu"
        :class="{ 'active': isMobileMenuOpen }"
        aria-label="Toggle navigation menu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
      
      <!-- Navigation links -->
      <div class="nav-links" :class="{ 'nav-links--open': isMobileMenuOpen }">
        <a href="#hero" class="nav-link" @click="handleNavClick('hero')">Home</a>
        <a href="#overview" class="nav-link" @click="handleNavClick('overview')">About</a>
        <a href="#floor-plans" class="nav-link" @click="handleNavClick('floor-plans')">Projects</a>
        <a href="#contact" class="nav-link" @click="handleNavClick('contact')">Contact Us</a>
      </div>
      
      <button class="btn btn--primary btn--3d nav-cta" @click="handleNavClick('contact')">
        Book Visits
      </button>
    </div>
  </nav>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'Navigation',
  setup() {
    const isScrolled = ref(false)
    const isMobileMenuOpen = ref(false)

    const handleScroll = () => {
      isScrolled.value = window.scrollY > 100
    }

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

    const toggleMobileMenu = () => {
      isMobileMenuOpen.value = !isMobileMenuOpen.value
      // Prevent body scroll when menu is open
      document.body.style.overflow = isMobileMenuOpen.value ? 'hidden' : ''
    }

    const handleNavClick = (sectionId) => {
      scrollToSection(sectionId)
      // Close mobile menu after click
      isMobileMenuOpen.value = false
      document.body.style.overflow = ''
    }

    // Close mobile menu when clicking outside
    const handleClickOutside = (event) => {
      if (isMobileMenuOpen.value && !event.target.closest('.nav-container')) {
        isMobileMenuOpen.value = false
        document.body.style.overflow = ''
      }
    }

    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      document.addEventListener('click', handleClickOutside)
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
      document.removeEventListener('click', handleClickOutside)
      document.body.style.overflow = ''
    })

    return {
      isScrolled,
      isMobileMenuOpen,
      toggleMobileMenu,
      handleNavClick,
      scrollToSection
    }
  }
}
</script>
