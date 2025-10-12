<template>
  <section id="projects" class="projects">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Our Projects</h2>
        <p class="section-subtitle">Discover our portfolio of premium residential and commercial developments across Bihar</p>
      </div>

      <div class="project-tabs">
        <button 
          class="tab-btn" 
          :class="{ active: activeTab === 'ongoing' }"
          @click="setActiveTab('ongoing')"
        >
          Ongoing Projects
        </button>
        <button 
          class="tab-btn" 
          :class="{ active: activeTab === 'completed' }"
          @click="setActiveTab('completed')"
        >
          Completed Projects
        </button>
      </div>

      <div class="project-content">
        <!-- Ongoing Projects -->
        <div class="tab-content" :class="{ active: activeTab === 'ongoing' }">
          <div class="projects-grid">
            <div 
              class="project-card" 
              v-for="project in ongoingProjects" 
              :key="project.id"
              @click="showProjectDetails(project)"
            >
              <div class="project-image">
                <img :src="project.image" :alt="project.name" />
                <div class="project-overlay">
                  <div class="project-status ongoing">{{ project.status }}</div>
                  <div class="project-progress">
                    <div class="progress-bar">
                      <div class="progress-fill" :style="{ width: project.progress + '%' }"></div>
                    </div>
                    <span class="progress-text">{{ project.progress }}% Complete</span>
                  </div>
                </div>
              </div>
              <div class="project-info">
                <h3 class="project-name">{{ project.name }}</h3>
                <p class="project-location">{{ project.location }}</p>
                <div class="project-details">
                  <div class="detail-item">
                    <span class="detail-label">Type:</span>
                    <span class="detail-value">{{ project.type }}</span>
                  </div>
                  <div class="detail-item">
                    <span class="detail-label">Units:</span>
                    <span class="detail-value">{{ project.units }}</span>
                  </div>
                  <div class="detail-item">
                    <span class="detail-label">Area:</span>
                    <span class="detail-value">{{ project.area }}</span>
                  </div>
                </div>
                <div class="project-features">
                  <span 
                    class="feature-tag" 
                    v-for="feature in project.features.slice(0, 3)" 
                    :key="feature"
                  >
                    {{ feature }}
                  </span>
                </div>
                <button class="btn btn--primary btn--3d project-btn">
                  <span>View Details</span>
                  <div class="btn-ripple"></div>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Completed Projects -->
        <div class="tab-content" :class="{ active: activeTab === 'completed' }">
          <div class="projects-grid">
            <div 
              class="project-card" 
              v-for="project in completedProjects" 
              :key="project.id"
              @click="showProjectDetails(project)"
            >
              <div class="project-image">
                <img :src="project.image" :alt="project.name" />
                <div class="project-overlay">
                  <div class="project-status completed">{{ project.status }}</div>
                  <div class="project-year">{{ project.completionYear }}</div>
                </div>
              </div>
              <div class="project-info">
                <h3 class="project-name">{{ project.name }}</h3>
                <p class="project-location">{{ project.location }}</p>
                <div class="project-details">
                  <div class="detail-item">
                    <span class="detail-label">Type:</span>
                    <span class="detail-value">{{ project.type }}</span>
                  </div>
                  <div class="detail-item">
                    <span class="detail-label">Units:</span>
                    <span class="detail-value">{{ project.units }}</span>
                  </div>
                  <div class="detail-item">
                    <span class="detail-label">Area:</span>
                    <span class="detail-value">{{ project.area }}</span>
                  </div>
                </div>
                <div class="project-features">
                  <span 
                    class="feature-tag" 
                    v-for="feature in project.features.slice(0, 3)" 
                    :key="feature"
                    
                  >
                    {{ feature }}
                  </span>
                </div>
                <button class="btn btn--primary btn--3d project-btn">
                  <span>View Details</span>
                  <div class="btn-ripple"></div>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Projects',
  setup() {
    const activeTab = ref('ongoing')

    const ongoingProjects = ref([
      {
        id: 1,
        name: 'Bimla Mangal Gardens',
        location: 'Bihar Sharif, Nalanda',
        type: 'Residential Complex',
        units: '108 Units',
        area: '15 Acres',
        status: 'Under Construction',
        progress: 75,
        features: ['3BHK Apartments', 'Premium Amenities', 'Commercial Space', 'Green Landscaping'],
        image: '/Arpan_Vilas/images/building-frontal-view.jpg'
      },
      {
        id: 2,
        name: 'Arpan Heights',
        location: 'Patna, Bihar',
        type: 'Mixed Use Development',
        units: '200 Units',
        area: '25 Acres',
        status: 'Under Construction',
        progress: 45,
        features: ['Luxury Apartments', 'Shopping Mall', 'Office Complex', 'Club House'],
        image: '/Arpan_Vilas/images/building-overview.jpg'
      },
      {
        id: 3,
        name: 'Green Valley Residency',
        location: 'Gaya, Bihar',
        type: 'Residential Township',
        units: '150 Units',
        area: '20 Acres',
        status: 'Under Construction',
        progress: 60,
        features: ['2BHK & 3BHK', 'Swimming Pool', 'Gymnasium', 'Parking'],
        image: '/Arpan_Vilas/images/courtyard-pool-view.jpg'
      },
      {
        id: 4,
        name: 'Urban Plaza',
        location: 'Muzaffarpur, Bihar',
        type: 'Commercial Complex',
        units: '50 Shops',
        area: '8 Acres',
        status: 'Under Construction',
        progress: 35,
        features: ['Retail Shops', 'Food Court', 'Parking', 'Modern Design'],
        image: '/Arpan_Vilas/images/building-facade-detail.jpg'
      }
    ])

    const completedProjects = ref([
      {
        id: 5,
        name: 'BIMLA MANGAL GARDENS Phase 1',
        location: 'Bihar Sharif, Nalanda',
        type: 'Residential Complex',
        units: '84 Units',
        area: '12 Acres',
        status: 'Completed',
        completionYear: '2022',
        features: ['3BHK Apartments', 'Club House', 'Swimming Pool', '24/7 Security'],
        image: '/Arpan_Vilas/images/building-frontal-view.jpg'
      },
      {
        id: 6,
        name: 'City Center Mall',
        location: 'Patna, Bihar',
        type: 'Commercial Complex',
        units: '100 Shops',
        area: '10 Acres',
        status: 'Completed',
        completionYear: '2021',
        features: ['Shopping Mall', 'Multiplex', 'Food Court', 'Parking'],
        image: '/Arpan_Vilas/images/building-overview.jpg'
      },
      {
        id: 7,
        name: 'Garden Residency',
        location: 'Darbhanga, Bihar',
        type: 'Residential Complex',
        units: '72 Units',
        area: '8 Acres',
        status: 'Completed',
        completionYear: '2020',
        features: ['2BHK Apartments', 'Garden Area', 'Children Park', 'Power Backup'],
        image: '/Arpan_Vilas/images/courtyard-passage.jpg'
      },
      {
        id: 8,
        name: 'Business Park',
        location: 'Bhagalpur, Bihar',
        type: 'Office Complex',
        units: '30 Offices',
        area: '5 Acres',
        status: 'Completed',
        completionYear: '2019',
        features: ['Modern Offices', 'Conference Hall', 'Cafeteria', 'Parking'],
        image: '/Arpan_Vilas/images/street-view.jpg'
      }
    ])

    const setActiveTab = (tab) => {
      activeTab.value = tab
    }

    const showProjectDetails = (project) => {
      alert(`Project Details - ${project.name}\n\nLocation: ${project.location}\nType: ${project.type}\nUnits: ${project.units}\nArea: ${project.area}\n\nFor detailed information and site visits, please contact our sales team.`)
    }

    return {
      activeTab,
      ongoingProjects,
      completedProjects,
      setActiveTab,
      showProjectDetails
    }
  }
}
</script>

<style scoped>
.projects {
  background: var(--color-light-tan);
  padding: 100px 0;
}

.project-tabs {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-bottom: 48px;
}

.tab-btn {
  padding: 16px 32px;
  background: transparent;
  border: 2px solid var(--color-border);
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  color: var(--color-text);
  cursor: pointer;
  transition: all 0.3s ease;
}

.tab-btn.active,
.tab-btn:hover {
  background: var(--color-black);
  color: var(--color-white);
  border-color: transparent;
  transform: translateY(-2px);
  box-shadow: var(--shadow-black);
}

.tab-content {
  display: none;
}

.tab-content.active {
  display: block;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 32px;
}

.project-card {
  background: var(--color-white);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  border: 1px solid var(--color-card-border);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.project-image {
  position: relative;
  height: 250px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.1) 0%, rgba(0, 0, 0, 0.4) 100%);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 16px;
}

.project-status {
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  align-self: flex-start;
}

.project-status.ongoing {
  background: #ff6b35;
  color: white;
}

.project-status.completed {
  background: #28a745;
  color: white;
}

.project-progress {
  align-self: flex-end;
  background: rgba(255, 255, 255, 0.9);
  padding: 8px 12px;
  border-radius: 20px;
  backdrop-filter: blur(10px);
}

.progress-bar {
  width: 100px;
  height: 4px;
  background: rgba(0, 0, 0, 0.2);
  border-radius: 2px;
  overflow: hidden;
  margin-bottom: 4px;
}

.progress-fill {
  height: 100%;
  background: #ff6b35;
  border-radius: 2px;
  transition: width 0.3s ease;
}

.progress-text {
  font-size: 10px;
  font-weight: 600;
  color: var(--color-black);
}

.project-year {
  align-self: flex-end;
  background: rgba(255, 255, 255, 0.9);
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
  color: var(--color-black);
  backdrop-filter: blur(10px);
}

.project-info {
  padding: 24px;
}

.project-name {
  font-size: 20px;
  font-weight: 600;
  color: var(--color-black);
  margin-bottom: 8px;
}

.project-location {
  color: var(--color-text-secondary);
  font-size: 14px;
  margin-bottom: 16px;
}

.project-details {
  margin-bottom: 16px;
}

.detail-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

.detail-label {
  font-size: 14px;
  color: var(--color-text-secondary);
  font-weight: 500;
}

.detail-value {
  font-size: 14px;
  color: var(--color-black);
  font-weight: 600;
}

.project-features {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.feature-tag {
  background: var(--color-light-beige);
  color: var(--color-black);
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 500;
}

.project-btn {
  width: 100%;
}

/* Mobile Responsive Styles */
@media (max-width: 768px) {
  .projects {
    padding: 60px 0;
  }
  
  .project-tabs {
    flex-direction: row;
    justify-content: center;
    gap: 12px;
    margin-bottom: 32px;
  }
  
  .tab-btn {
    padding: 12px 24px;
    font-size: 14px;
    border-radius: 25px;
    flex: 1;
    max-width: 160px;
  }
  
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 24px;
  }
  
  .project-image {
    height: 200px;
  }
  
  .project-info {
    padding: 20px;
  }
  
  .project-name {
    font-size: 18px;
  }
  
  .project-details {
    margin-bottom: 12px;
  }
  
  .detail-item {
    margin-bottom: 6px;
  }
  
  .detail-label,
  .detail-value {
    font-size: 13px;
  }
  
  .feature-tag {
    font-size: 11px;
    padding: 3px 6px;
  }
}

@media (max-width: 480px) {
  .project-tabs {
    flex-direction: column;
    gap: 10px;
  }
  
  .tab-btn {
    width: 100%;
    max-width: 200px;
    margin: 0 auto;
  }
  
  .project-image {
    height: 180px;
  }
  
  .project-info {
    padding: 16px;
  }
  
  .project-name {
    font-size: 16px;
  }
  
  .project-location {
    font-size: 13px;
  }
  
  .detail-label,
  .detail-value {
    font-size: 12px;
  }
  
  .feature-tag {
    font-size: 10px;
  }
}
</style>
