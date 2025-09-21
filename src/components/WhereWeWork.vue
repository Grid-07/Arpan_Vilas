<template>
  <section id="where-we-work" class="where-we-work">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Where We Work</h2>
        <p class="section-subtitle">We work for our clients and develop ideals for lasting success. So that your wish is met with a new building and also for the construction of your future</p>
      </div>

      <div class="main-content">
        <!-- Left Side - Map Section -->
        <div class="map-section">
          <div class="map-container" ref="mapContainer">
            <img 
              ref="mapImage"
              src="/indiaHigh.svg" 
              alt="India Map" 
              class="map-svg"
              @load="onMapLoad"
              @error="onMapError"
            />
            
            <!-- Debug Info (Remove in production) -->
            <div class="debug-info" v-if="showDebug">
              <p>Map Size: {{ mapSize.width }}x{{ mapSize.height }}</p>
              <p>Container Size: {{ containerSize.width }}x{{ containerSize.height }}</p>
              <p>Hovered Location: {{ hoveredLocation }}</p>
            </div>
            
            <!-- Responsive Interactive Location Pins -->
            <div 
              v-for="location in mapLocations" 
              :key="location.id" 
              class="pin-container"
              :style="getPinPosition(location)"
              @mouseenter="handlePinHover(location.id, true)"
              @mouseleave="handlePinHover(location.id, false)"
            >
              <!-- Enhanced Pin with Better Visibility -->
              <div 
                class="pin"
                :class="{ active: location.active }"
              >
                <div class="pin-shadow"></div>
                <div class="pin-circle">
                  <div class="pin-inner"></div>
                </div>
                <div class="pin-pulse" v-if="location.active"></div>
              </div>
              
              <!-- Enhanced Pin Label -->
              <div 
                class="pin-label"
                :class="{ active: location.active }"
              >
                {{ location.city }}
              </div>

              <!-- Location Popup - Hover Only -->
              <div 
                v-show="hoveredLocation === location.id"
                class="location-popup"
                :class="{ 'popup-visible': hoveredLocation === location.id }"
              >
                <!-- Popup Arrow -->
                <div class="popup-arrow"></div>
                
                <!-- Popup Content -->
                <div class="popup-content">
                  <div class="popup-header">
                    <div class="location-icon">{{ location.icon }}</div>
                    <div class="location-info">
                      <h4 class="location-title">{{ location.city }}</h4>
                      <p class="location-state">{{ location.state }}</p>
                    </div>
                  </div>
                  
                  <div class="popup-body">
                    <p class="location-description">{{ location.description }}</p>
                    
                    <div class="location-highlights">
                      <div class="highlight-item">
                        <span class="highlight-icon">🏗️</span>
                        <div class="highlight-content">
                          <strong>{{ location.projects }}</strong>
                          <span>Active Projects</span>
                        </div>
                      </div>
                      <div class="highlight-item">
                        <span class="highlight-icon">📍</span>
                        <div class="highlight-content">
                          <strong>{{ location.status }}</strong>
                          <span>Development Status</span>
                        </div>
                      </div>
                      <div class="highlight-item">
                        <span class="highlight-icon">🏡</span>
                        <div class="highlight-content">
                          <strong>{{ location.totalUnits }}</strong>
                          <span>Total Units</span>
                        </div>
                      </div>
                    </div>

                    <div class="location-projects" v-if="location.featuredProjects">
                      <h5>Featured Projects</h5>
                      <div class="project-list">
                        <div 
                          v-for="project in location.featuredProjects" 
                          :key="project.name"
                          class="project-item"
                        >
                          <div class="project-info">
                            <strong>{{ project.name }}</strong>
                            <span>{{ project.type }}</span>
                          </div>
                          <div class="project-status">{{ project.status }}</div>
                        </div>
                      </div>
                    </div>                
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Side - What We Do Section -->
        <div class="what-we-do-section">
          <div class="what-we-do-header">
            <h2 class="what-we-do-title">What we do</h2>
            <p class="what-we-do-subtitle">Multi-Disciplined Engineering Solutions</p>
          </div>

          <div class="services-grid">
            <div class="service-card" v-for="service in services" :key="service.id">
              <div class="service-number">{{ service.number }}</div>
              <h3 class="service-title">{{ service.title }}</h3>
              <p class="service-description">{{ service.description }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="stats-section">
        <div class="stat-item">
          <span class="stat-number">{{ animatedStats.happyCustomers }}</span>
          <span class="stat-label">Happy Customers</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">{{ animatedStats.greenEnvironment }}</span>
          <span class="stat-label">% Green Environment</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">{{ totalLocations }}</span>
          <span class="stat-label">Active Locations</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">{{ totalProjects }}</span>
          <span class="stat-label">Total Projects</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, reactive, computed, onMounted, onUnmounted, nextTick } from 'vue'

export default {
  name: 'WhereWeWork',
  setup() {
    const mapContainer = ref(null)
    const mapImage = ref(null)
    const showDebug = ref(false) // Set to true for debugging hover issues
    
    const mapSize = reactive({ width: 0, height: 0 })
    const containerSize = reactive({ width: 0, height: 0 })
    
    // Simplified to hover-only state management
    const hoveredLocation = ref(null)
    
    // Enhanced location data
    const mapLocations = ref([
      {
        id: 1,
        icon: '🏙️',
        city: 'Ranchi',
        state: 'Jharkhand',
        xPercent: 60.0,
        yPercent: 52.0,
        active: false,
        description: 'Our primary development hub in Jharkhand with multiple luxury residential projects creating modern living spaces.',
        projects: '5+',
        status: 'Active',
        totalUnits: '500+',
        featuredProjects: [
          { name: 'Arpan Vilash', type: '3BHK Luxury Flats', status: 'Ongoing' },
          { name: 'Palash Arpan', type: 'Premium Apartments', status: 'Completed' },
          { name: 'Nishesh Arpan', type: 'Modern Homes', status: 'Planning' }
        ]
      },
      {
        id: 2,
        icon: '🏘️',
        city: 'Bihar Sharif',
        state: 'Bihar',
        xPercent: 63.5,
        yPercent: 47.0,
        active: false,
        description: 'Affordable luxury living solutions in the historic city of Bihar Sharif with modern amenities.',
        projects: '1',
        status: 'Active',
        totalUnits: '108',
        featuredProjects: [
          { name: 'Sri Ganesh Arpan', type: 'Residential Complex', status: 'Ongoing' }
        ]
      },
      {
        id: 3,
        icon: '🏛️',
        city: 'Patna',
        state: 'Bihar',
        xPercent: 62.0,
        yPercent: 45.0,
        active: false,
        description: 'Expanding our presence in Bihar\'s capital with world-class residential and commercial developments.',
        projects: '3+',
        status: 'Planning',
        totalUnits: '300+',
        featuredProjects: [
          { name: 'Patna Heights', type: 'Commercial Complex', status: 'Planning' },
          { name: 'Bihar Capital Homes', type: 'Luxury Residences', status: 'Upcoming' }
        ]
      },
      {
        id: 4,
        icon: '🏜️',
        city: 'Jaipur',
        state: 'Rajasthan',
        xPercent: 25.0,
        yPercent: 42.0,
        active: false,
        description: 'Future expansion bringing our signature luxury living experience to the Pink City with premium developments.',
        projects: '2+',
        status: 'Future',
        totalUnits: '200+',
        featuredProjects: [
          { name: 'Pink City Paradise', type: 'Luxury Villas', status: 'Future' },
          { name: 'Royal Residences', type: 'Premium Apartments', status: 'Conceptual' }
        ]
      }
    ])

    // What We Do services data
    const services = ref([
      {
        id: 1,
        number: '01.',
        title: 'World Class Amenities',
        description: 'We provide exclusive access to top-of-the-line conveniences, including high-class amenities.'
      },
      {
        id: 2,
        number: '02.',
        title: 'Affordable Prices',
        description: 'We provide lots of flats, buildings which are affordable for all'
      },
      {
        id: 3,
        number: '03.',
        title: 'Commitment Towards Environment and Safety',
        description: 'We are committed to create a world class environment that is safe and eco-friendly for you and nature'
      },
      {
        id: 4,
        number: '04.',
        title: 'Construction Management',
        description: 'We always engineers plan, design, monitor and inspect systems to make buildings comfortable, functional, efficient and safe.'
      }
    ])

    const animatedStats = reactive({
      happyCustomers: 0,
      greenEnvironment: 0
    })

    const totalProjects = computed(() => {
      return mapLocations.value.reduce((total, location) => {
        const projects = parseInt(location.projects.replace('+', '')) || 0
        return total + projects
      }, 0)
    })

    const totalLocations = computed(() => {
      return mapLocations.value.length
    })

    // Fixed and simplified hover logic
    const handlePinHover = (locationId, isEntering) => {
      if (showDebug.value) {
        console.log(`handlePinHover(${locationId}, ${isEntering})`)
      }
      
      if (isEntering) {
        hoveredLocation.value = locationId
        setActiveLocation(locationId)
      } else {
        hoveredLocation.value = null
        setActiveLocation(null)
      }
      
      if (showDebug.value) {
        console.log(`hoveredLocation is now: ${hoveredLocation.value}`)
      }
    }

    const setActiveLocation = (locationId) => {
      mapLocations.value.forEach(location => {
        location.active = location.id === locationId
      })
    }

    // Enhanced pin position calculation
    const getPinPosition = (location) => {
      if (!mapImage.value || !mapContainer.value) {
        return { left: '0px', top: '0px' }
      }

      const imageRect = mapImage.value.getBoundingClientRect()
      const containerRect = mapContainer.value.getBoundingClientRect()
      
      mapSize.width = Math.round(imageRect.width)
      mapSize.height = Math.round(imageRect.height)
      containerSize.width = Math.round(containerRect.width)
      containerSize.height = Math.round(containerRect.height)
      
      let xPos = (location.xPercent / 100) * imageRect.width
      let yPos = (location.yPercent / 100) * imageRect.height
      
      const padding = 20
      xPos = Math.max(padding, Math.min(xPos, imageRect.width - padding))
      yPos = Math.max(padding, Math.min(yPos, imageRect.height - padding))
      
      return {
        left: xPos + 'px',
        top: yPos + 'px'
      }
    }

    // Action methods
    const viewDetails = (location) => {
      console.log('View details for:', location.city)
    }

    const contactUs = (location) => {
      console.log('Contact us about:', location.city)
    }

    const onMapLoad = () => {
      console.log('India map loaded successfully')
      nextTick(() => {
        mapLocations.value = [...mapLocations.value]
      })
    }

    const onMapError = () => {
      console.log('India map failed to load, using fallback')
    }

    const handleResize = () => {
      clearTimeout(handleResize.timeoutId)
      handleResize.timeoutId = setTimeout(() => {
        nextTick(() => {
          mapLocations.value = [...mapLocations.value]
        })
      }, 100)
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
      window.addEventListener('resize', handleResize)
      
      setTimeout(() => {
        animateCounter(500, 'happyCustomers')
        animateCounter(85, 'greenEnvironment')
      }, 1000)
    })

    onUnmounted(() => {
      window.removeEventListener('resize', handleResize)
      if (handleResize.timeoutId) {
        clearTimeout(handleResize.timeoutId)
      }
    })

    return {
      mapContainer,
      mapImage,
      mapLocations,
      services,
      animatedStats,
      totalProjects,
      totalLocations,
      showDebug,
      mapSize,
      containerSize,
      hoveredLocation,
      getPinPosition,
      handlePinHover,
      viewDetails,
      contactUs,
      onMapLoad,
      onMapError
    }
  }
}
</script>

<style scoped>
.where-we-work {
  padding: 60px 0;
}

/* Main Content Layout - Increased width for What We Do section */
.main-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr; /* Map: 40%, What We Do: 60% */
  gap: 60px;
  align-items: start;
  margin: 60px 0;
}

/* Left Side - Map Section */
.map-section {
  width: 100%;
}

.map-container {
  position: relative;
  width: 100%;
  aspect-ratio: 4/3;
  overflow: visible;
}

.map-svg {
  width: 58vh;
  height: 78vh;
  display: block;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  object-fit: contain;
}

/* Debug Info */
.debug-info {
  position: absolute;
  top: 10px;
  left: 10px;
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 10px;
  border-radius: 5px;
  font-size: 12px;
  z-index: 100;
}

/* Pin Styles */
.pin-container {
  position: absolute;
  transform: translate(-50%, -50%);
  cursor: pointer;
  z-index: 10;
  pointer-events: auto;
  /* Ensure hover area is large enough */
  padding: 10px;
  margin: -10px;
}

.pin {
  position: relative;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  pointer-events: auto;
}

.pin:hover {
  transform: scale(1.2);
}

.pin.active {
  transform: scale(1.3);
}

.pin-shadow {
  position: absolute;
  top: 2px;
  left: 2px;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.3);
  z-index: -1;
}

.pin-circle {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background: #ff4444;
  border: 4px solid #ffffff;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.4);
  position: relative;
  transition: all 0.3s ease;
  z-index: 1;
}

.pin:hover .pin-circle {
  background: #ff2222;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
  transform: scale(1.1);
}

.pin.active .pin-circle {
  background: #ff0000;
  box-shadow: 0 10px 25px rgba(255, 0, 0, 0.4);
  transform: scale(1.2);
}

.pin-inner {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.pin-pulse {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background: rgba(255, 68, 68, 0.4);
  animation: pulse 2s infinite;
  z-index: -1;
}

@keyframes pulse {
  0% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0.8;
  }
  100% {
    transform: translate(-50%, -50%) scale(3);
    opacity: 0;
  }
}

.pin-label {
  position: absolute;
  top: -40px;
  left: 50%;
  transform: translateX(-50%);
  background: #333333;
  color: #ffffff;
  padding: 8px 16px;
  border-radius: 25px;
  font-size: 13px;
  font-weight: 700;
  white-space: nowrap;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.3);
  transition: all 0.3s ease;
  opacity: 0;
  pointer-events: none;
  z-index: 20;
}

.pin:hover .pin-label,
.pin.active .pin-label {
  opacity: 1;
  transform: translateX(-50%) translateY(-8px);
}

.pin-label.active {
  background: #ff4444;
  color: #ffffff;
  font-weight: 800;
  font-size: 14px;
  box-shadow: 0 8px 20px rgba(255, 68, 68, 0.4);
}

.pin-label::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-top: 6px solid #333333;
}

.pin-label.active::after {
  border-top-color: #ff4444;
}

/* Location Popup Styles - Completely Fixed */
.location-popup {
  position: absolute;
  top: -80px; /* Moved further up to avoid interference */
  left: 50%;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
  border: 1px solid #e5e7eb;
  min-width: 320px;
  max-width: 400px;
  z-index: 2000; /* Higher z-index to ensure it's above everything */
  /* Always start hidden */
  opacity: 0;
  visibility: hidden;
  transform: translateX(-50%) translateY(-10px) scale(0.95);
  transition: all 0.2s ease;
  pointer-events: none; /* Prevent interference with hover events */
}

/* Show popup when visible class is added */
.location-popup.popup-visible {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) translateY(0) scale(1);
  pointer-events: auto; /* Re-enable pointer events when visible */
}

.popup-arrow {
  position: absolute;
  bottom: -8px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  border-top: 8px solid #ffffff;
}

.popup-content {
  padding: 0;
}

.popup-header {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 20px 20px 16px;
  border-bottom: 1px solid #f3f4f6;
}

.location-icon {
  font-size: 28px;
  line-height: 1;
}

.location-info {
  flex: 1;
}

.location-title {
  font-size: 20px;
  font-weight: 700;
  margin: 0 0 4px 0;
  color: #111827;
}

.location-state {
  font-size: 14px;
  color: #6b7280;
  margin: 0;
}

.popup-body {
  padding: 0 20px 20px;
}

.location-description {
  font-size: 14px;
  color: #4b5563;
  line-height: 1.6;
  margin: 0 0 20px 0;
}

.location-highlights {
  display: grid;
  grid-template-columns: 1fr;
  gap: 12px;
  margin-bottom: 20px;
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px;
  background: #f9fafb;
  border-radius: 8px;
}

.highlight-icon {
  font-size: 20px;
  line-height: 1;
}

.highlight-content {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.highlight-content strong {
  font-size: 16px;
  font-weight: 700;
  color: #111827;
}

.highlight-content span {
  font-size: 12px;
  color: #6b7280;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.location-projects {
  margin-bottom: 20px;
}

.location-projects h5 {
  font-size: 16px;
  font-weight: 600;
  margin: 0 0 12px 0;
  color: #111827;
}

.project-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.project-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  background: #f3f4f6;
  border-radius: 6px;
  font-size: 14px;
}

.project-info {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.project-info strong {
  font-weight: 600;
  color: #111827;
}

.project-info span {
  font-size: 12px;
  color: #6b7280;
}

.project-status {
  font-size: 12px;
  padding: 4px 8px;
  background: #dbeafe;
  color: #1e40af;
  border-radius: 12px;
  font-weight: 500;
}

.popup-actions {
  display: flex;
  gap: 8px;
  padding-top: 16px;
  border-top: 1px solid #f3f4f6;
}

.btn-action {
  flex: 1;
  padding: 10px 16px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  border: none;
}

.btn-action.primary {
  background: #ff4444;
  color: #ffffff;
}

.btn-action.primary:hover {
  background: #ff2222;
  transform: translateY(-1px);
}

.btn-action.secondary {
  background: #f3f4f6;
  color: #374151;
}

.btn-action.secondary:hover {
  background: #e5e7eb;
  transform: translateY(-1px);
}

/* Right Side - What We Do Section - Matching Map Background Exactly */
.what-we-do-section {
  /* Matching the exact beige/cream background that maps typically have */
  background: rgba(255, 255, 255, 0.98); 
  border-radius: 20px;
  padding: 40px;
  height: 70vh; /* Match map height */
  overflow-y: auto; /* Allow scrolling if content overflows */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1); /* Match map shadow */
}

.what-we-do-header {
  text-align: center;
  margin-bottom: 30px; /* Reduced margin to fit in height */
}

.what-we-do-title {
  font-size: 2rem; /* Slightly smaller to fit */
  font-weight: 800;
  margin: 0 0 12px 0;
  color: #111827; /* Black text */
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Added text shadow */
}

.what-we-do-subtitle {
  font-size: 1rem; /* Adjusted size */
  font-weight: 400;
  margin: 0;
  color: #374151; /* Dark gray */
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1); /* Added text shadow */
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px; /* Reduced gap to fit better */
}

/* Service Cards - Better Contrast Against Map Background */
.service-card {
  /* Light cream/white background that contrasts with the beige background */
  background: #ffffff; 
  border-radius: 16px;
  padding: 20px; /* Reduced padding */
  border: 2px solid #e5e5e5; /* Subtle border for definition */
  transition: all 0.3s ease;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08); /* Soft shadow */
}

.service-card:hover {
  background: #ffffff;
  transform: translateY(-4px);
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.12); /* Enhanced shadow on hover */
  border-color: #d1d1d1; /* Slightly darker border on hover */
}

.service-number {
  font-size: 1.2rem; /* Slightly smaller */
  font-weight: 700;
  color: #8b7355; /* Warm brown color that complements beige background */
  margin-bottom: 8px; /* Reduced margin */
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1); /* Added text shadow */
}

.service-title {
  font-size: 0.95rem; /* Adjusted size */
  font-weight: 600;
  margin: 0 0 8px 0; /* Reduced margin */
  color: #2d3748; /* Darker text for better contrast */
  line-height: 1.3;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1); /* Added text shadow */
}

.service-description {
  font-size: 0.8rem; /* Slightly smaller */
  line-height: 1.4;
  margin: 0;
  color: #4a5568; /* Medium gray for good readability */
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.05); /* Subtle text shadow */
}

/* Stats Section */
.stats-section {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 40px;
  margin-top: 80px;
  text-align: center;
}

.stat-item {
  padding: 20px;
}

.stat-number {
  display: block;
  font-size: 3rem;
  font-weight: 800;
  line-height: 1;
  margin-bottom: 8px;
  color: #111827;
}

.stat-label {
  font-size: 14px;
  color: #6b7280;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Responsive Design */
@media (max-width: 1200px) {
  .main-content {
    gap: 40px;
  }
  
  .what-we-do-section {
    padding: 32px;
    height: auto; /* Allow natural height on smaller screens */
  }
  
  .what-we-do-title {
    font-size: 1.8rem;
  }
}

@media (max-width: 768px) {
  .main-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .where-we-work {
    padding: 40px 0;
  }
  
  .map-container {
    aspect-ratio: 16/10;
  }
  
  .what-we-do-section {
    padding: 24px;
    height: auto; /* Natural height on mobile */
  }
  
  .what-we-do-title {
    font-size: 1.6rem;
  }
  
  .services-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
  
  .location-popup {
    min-width: 280px;
    max-width: calc(100vw - 40px);
  }
  
  .popup-header {
    padding: 16px 16px 12px;
  }
  
  .popup-body {
    padding: 0 16px 16px;
  }
  
  .pin-circle {
    width: 20px;
    height: 20px;
    border-width: 3px;
  }
  
  .pin-inner {
    width: 8px;
    height: 8px;
  }
  
  .pin-shadow {
    width: 20px;
    height: 20px;
  }
  
  .stats-section {
    gap: 24px;
    margin-top: 60px;
  }
}

@media (max-width: 480px) {
  .where-we-work {
    padding: 30px 0;
  }
  
  .main-content {
    gap: 30px;
  }
  
  .map-container {
    aspect-ratio: 4/3;
  }
  
  .what-we-do-section {
    padding: 20px;
  }
  
  .what-we-do-title {
    font-size: 1.4rem;
  }
  
  .what-we-do-subtitle {
    font-size: 0.9rem;
  }
  
  .service-card {
    padding: 16px;
  }
  
  .location-popup {
    min-width: 260px;
  }
  
  .popup-actions {
    flex-direction: column;
  }
  
  .pin-circle {
    width: 18px;
    height: 18px;
    border-width: 2px;
  }
  
  .pin-inner {
    width: 6px;
    height: 6px;
  }
  
  .pin-shadow {
    width: 18px;
    height: 18px;
  }
  
  .stats-section {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }
}

/* Additional precision for high-DPI displays */
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  .pin-container {
    transform: translate(-50%, -50%) translateZ(0);
  }
  
  .pin-circle {
    border-width: 3px;
  }
}
</style>