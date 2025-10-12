<template>
  <nav class="navbar" :class="{ 'navbar--scrolled': isScrolled }">
    <div class="nav-container">
      <div class="nav-logo">
        <!-- Logo Image -->
        <img src="../assests/abha engicon.png" alt="Abha Engicon Logo" class="logo-image" />
      </div>

      <!-- Mobile menu button -->
      <button
        class="mobile-menu-btn"
        @click="toggleMobileMenu"
        :class="{ active: isMobileMenuOpen }"
        aria-label="Toggle navigation menu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>

      <!-- Navigation links -->
      <div class="nav-links" :class="{ 'nav-links--open': isMobileMenuOpen }">
        <router-link to="/" class="nav-link" @click="handleNavClick">Home</router-link>
        <router-link to="/about" class="nav-link" @click="handleNavClick">About</router-link>
        <router-link to="/projects" class="nav-link" @click="handleNavClick">Projects</router-link>
        <router-link to="/floor-plans" class="nav-link" @click="handleNavClick">Floor Plans</router-link>
        <router-link to="/contact" class="nav-link" @click="handleNavClick">Contact Us</router-link>
      </div>

      <router-link to="/contact" class="btn btn--primary btn--3d nav-cta" @click="handleNavClick">
        Book Visits
      </router-link>
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
      document.body.style.overflow = isMobileMenuOpen.value ? 'hidden' : ''
    }

    const handleNavClick = () => {
      isMobileMenuOpen.value = false
      document.body.style.overflow = ''
    }

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
      handleNavClick
    }
  }
}
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 1rem 2rem;
  display: flex;
  justify-content: center;
  z-index: 1000;
  transition: background 0.3s ease;
  background: transparent;
}

.navbar--scrolled {
  background: rgba(255, 255, 255, 0.98) !important;
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(51, 51, 51, 0.15);
}

.nav-container {
  max-width: 1200px;
  width: 100%;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  position: relative;
}

.nav-logo {
  flex-shrink: 0;
   position: relative;
  
} 

.logo-image {
  height: 60px;
  width: auto;
}

/* Desktop nav links */
.nav-links {
  display: flex;
  flex: 1;
  gap: 24px;
  justify-content: flex-start;
}

.nav-link {
  color: #111;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  transition: color 0.2s;
}

.nav-link:hover {
  color: #ff4444;
}

.nav-link.router-link-active {
  color: #ff4444;
}

/* Call to action button */
.nav-cta {
  white-space: nowrap;
}

/* Mobile Menu Button - Hamburger */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 24px;
  height: 18px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1100;
}

.mobile-menu-btn span {
  display: block;
  height: 3px;
  background: #111;
  border-radius: 2px;
  transition: all 0.3s ease;
}

.mobile-menu-btn.active span:nth-child(1) {
  transform: translateY(7.5px) rotate(45deg);
}

.mobile-menu-btn.active span:nth-child(2) {
  opacity: 0;
}

.mobile-menu-btn.active span:nth-child(3) {
  transform: translateY(-7.5px) rotate(-45deg);
}

/* Hide mobile menu links by default */
.nav-links {
  transition: max-height 0.3s ease;
}

@media (max-width: 768px) {
  .nav-links {
  background: transparent;
    backdrop-filter: blur(20px);
    position: absolute;
    top: 100%;
     /* align left edge of dropdown with left edge of logo */
    left: 0;
    background: #fff;
    flex-direction: column;
    width: 220px; /* enough to fit content */
    max-height: 0;
    overflow: hidden;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border-radius: 8px;
    z-index: 1000;
  }

  .nav-links.nav-links--open {
       background: #FAF0E6;

    max-height: 500px; /* high enough to show all links */
  }

  .nav-link {
   padding: 1rem 1.5rem;
    font-size: 1rem;
    border-bottom: 1px solid #eee;
  }

  .nav-cta {
    display: none; /* Hide button on small screens or put inside menu if desired */
  }

  .mobile-menu-btn {
    display: flex;
  }
}
</style>
