<template>
  <section id="where-we-work" class="where-we-work">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Where We Work</h2>
        <p class="section-subtitle">
          We work for our clients and develop ideals for lasting success. So that your wish is met with a new building and also for the construction of your future
        </p>
      </div>

      <div class="main-content">
        <!-- Left Side - Map -->
        <div class="map-section">
          <div class="map-container">
            <svg
              ref="mapSvg"              
              viewBox="0 0 600 800"
              preserveAspectRatio="xMidYMid meet"
              class="map-svg"
            >
               
                <image href="/indiaHigh.svg" x="0" y="0" width="100%" height="100%" />
             
              <g
                v-for="location in mapLocations"
                :key="location.id"
                @mouseenter="handlePinHover(location.id, true)"
                @mouseleave="handlePinHover(location.id, false)"
              >
                <circle
                  class="pin-circle"
                  :cx="getPinCoordinates(location).x"
                  :cy="getPinCoordinates(location).y"
                  :r="location.active ? 6 : 8"
                  :class="{ active: location.active }"
                />
                <circle
                  v-if="location.active"
                  class="pin-pulse"
                  :cx="getPinCoordinates(location).x"
                  :cy="getPinCoordinates(location).y"
                  r="10"
                />
                <foreignObject
                  v-if="hoveredLocation === location.id"
                  :x="getPinCoordinates(location).x - 165"
                  :y="getPinCoordinates(location).y - 195"
                  width="330"
                  height="180"
                >
                  <div xmlns="http://www.w3.org/1999/xhtml" class="popup-card">
                    <div class="popup-header">
                      <span class="popup-icon">{{ location.icon }}</span>
                      <div class="popup-info">
                        <h4>{{ location.city }}</h4>
                        <p>{{ location.state }}</p>
                      </div>
                    </div>
                    <p class="popup-desc">{{ location.description }}</p>
                    <div class="popup-highlights">
                      <div><strong>{{ location.projects }}</strong> Projects</div>
                      <div><strong>{{ location.status }}</strong></div>
                      <div><strong>{{ location.totalUnits }}</strong> Units</div>
                    </div>
                  </div>
                </foreignObject>
              </g>
            </svg>
          </div>
        </div>

        <!-- Right Side - What We Do -->
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

      <!-- Stats Section -->
      <div class="stats-section">
        <div class="stat-item">
          <span class="stat-number">{{ animatedStats.happyCustomers }} +</span>
          <span class="stat-label">Happy Customers</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">{{ animatedStats.greenEnvironment }}</span>
          <span class="stat-label">Upcomming Projects</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">{{ totalLocations }}</span>
          <span class="stat-label">Cities</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">20 +</span>
          <span class="stat-label">Total Projects</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, reactive, computed, onMounted } from "vue";

export default {
  name: "WhereWeWork",
  setup() {
    const hoveredLocation = ref(null);
    const mapLocations = ref([
      {
        id: 1,
        icon: "🏙️",
        city: "Ranchi",
        state: "Jharkhand",
        xPercent: 35,
        yPercent: 43,
        active: false,
        description: "Our primary hub in Jharkhand with luxury residential projects.",
        projects: "5+",
        status: "Active",
        totalUnits: "500+"
      },
      {
        id: 2,
        icon: "🏘️",
        city: "Bihar Sharif",
        state: "Bihar",
        xPercent: 36.3,
        yPercent: 38,
        active: false,
        description: "Affordable living solutions with modern amenities.",
        projects: "1",
        status: "Active",
        totalUnits: "108"
      },
      {
        id: 3,
        icon: "🏛️",
        city: "Patna",
        state: "Bihar",
        xPercent: 35.3,
        yPercent: 36,
        active: false,
        description: "World-class residential and commercial developments.",
        projects: "3+",
        status: "Planning",
        totalUnits: "300+"
      },
      {
        id: 4,
        icon: "🏜️",
        city: "Jaipur",
        state: "Rajasthan",
        xPercent: 15,
        yPercent: 35,
        active: false,
        description: "Premium living experiences in Rajasthan's Pink City.",
        projects: "2+",
        status: "Future",
        totalUnits: "200+"
      }
    ]);
    const services = ref([
      { id: 1, number: "01.", title: "World Class Amenities", description: "Exclusive access to high-class amenities." },
      { id: 2, number: "02.", title: "Affordable Prices", description: "Affordable flats, buildings for everyone." },
      { id: 3, number: "03.", title: "Eco & Safety Commitment", description: "We create safe, eco-friendly environments." },
      { id: 4, number: "04.", title: "Construction Management", description: "Our engineers plan, monitor, and inspect systems." }
    ]);
    const animatedStats = reactive({ happyCustomers: 0, greenEnvironment: 0 });
    const totalProjects = computed(() => {
      return mapLocations.value.reduce((t, l) => t + (parseInt(l.projects) || 0), 0);
    });
    const totalLocations = computed(() => mapLocations.value.length);
    const handlePinHover = (id, enter) => {
      hoveredLocation.value = enter ? id : null;
      mapLocations.value.forEach((l) => (l.active = l.id === id && enter));
    };
    const getPinCoordinates = (loc) => {
      const baseW = 1000, baseH = 1000;
      return { x: (loc.xPercent / 100) * baseW, y: (loc.yPercent / 100) * baseH };
    };
    const animateCounter = (target, key) => {
      let cur = 0;
      const step = () => {
        cur += target / 60;
        animatedStats[key] = Math.min(target, Math.floor(cur));
        if (cur < target) requestAnimationFrame(step);
      };
      step();
    };
    onMounted(() => {
      setTimeout(() => {
        animateCounter(500 , "happyCustomers");
        animateCounter(5, "greenEnvironment");
      }, 500);
    });
    return { mapLocations, services, animatedStats, totalProjects, totalLocations, hoveredLocation, handlePinHover, getPinCoordinates };
  }
};
</script>

<style scoped>
.where-we-work {
  padding: 60px 0;
}

.main-content {
  display: grid;
  grid-template-columns: 3fr 2fr;  /* Bigger map column */
  gap:60px;
  align-items: flex-start;
  margin: 40px 0;
}

.map-section {
  width: 100%;
}

.map-container {
  width: 100%;
  max-width: 1000px; /* Bigger max width */
  margin: auto;
}

.map-svg {
  width: 100%;
  height: auto;
  display: block;
}

/* Pin styles */
.pin-circle {
  fill: #ffffff;
  stroke: #ff4444;
  stroke-width: 3px;
  cursor: pointer;
  transition: 0.3s;
}
.pin-circle.active {
  stroke: #ff0000;
}

/* Bigger pulse on active pin */
.pin-pulse {
  fill: rgba(255, 68, 68, 0.25);
  animation: pulse 2s infinite;
}
@keyframes pulse {
  0% { r:28; opacity:0.6; }
  100% { r:56; opacity:0; }
}

/* Popup styles with relative/em font sizes */
.popup-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 8px 28px rgba(0,0,0,0.2);
  padding: 1em;
  font-size: 1em;
  border: 1px solid #ddd;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}
.popup-header {
  display: flex;
  align-items: center;
  gap: 0.5em;
  margin-bottom: 0.5em;
}
.popup-icon {
  font-size: 1.5em;
}
.popup-info h4 {
  margin: 0;
  font-size: 1.1em;
  font-weight: bold;
}
.popup-info p {
  margin: 0;
  font-size: 0.9em;
  color: #666;
}
.popup-desc {
  margin: 0.5em 0;
  font-size: 1em;
  color: #444;
}
.popup-highlights {
  display: flex;
  justify-content: space-between;
  font-size: 0.9em;
  color: #222;
}

/* What We Do Section */
.what-we-do-section {
  background: rgba(255, 255, 255, 0.98);
  border-radius: 20px;
  padding: 2em;
  height: 100%;
  overflow-y: auto;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}
.services-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25em;
}
.service-card {
  background: #fff;
  border: 1px solid #eee;
  border-radius: 12px;
  padding: 1em;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
}

/* Stats Section */
.stats-section {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2.5em;
  margin-top: 5em;
  text-align: center;
}
.stat-number {
  font-size: 2.5rem;
  font-weight: 800;
  color: #111827;
}
.stat-label {
  font-size: 0.9rem;
  color: #6b7280;
  letter-spacing: 1px;
}

/* Responsive */
@media (max-width: 768px) {
  .main-content {
    grid-template-columns: 1fr;
    gap: 2.5em;
  }
  .services-grid {
    grid-template-columns: 1fr;
  }
}
</style>
