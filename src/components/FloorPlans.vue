<template>
  <section id="floor-plans" class="floor-plans">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Floor Plans</h2>
        <p class="section-subtitle">Choose from our carefully designed 3BHK apartments ranging from 1575 to 3815 sq ft</p>
      </div>

      <div class="floor-plan-tabs">
        <button 
          class="tab-btn" 
          :class="{ active: activeBlock === 'blockA' }"
          @click="setActiveBlock('blockA')"
        >
          Block A
        </button>
        <button 
          class="tab-btn" 
          :class="{ active: activeBlock === 'blockB' }"
          @click="setActiveBlock('blockB')"
        >
          Block B
        </button>
      </div>

      <div class="floor-plan-content">
        <div class="block-content" :class="{ active: activeBlock === 'blockA' }">
          <div class="plan-grid">
            <div 
              class="plan-card" 
              :class="{ featured: plan.featured }"
              v-for="plan in blockAPlans" 
              :key="plan.id"
              @click="showFloorPlanModal(plan)"
            >
              <div class="plan-header">
                <h4>{{ plan.name }}</h4>
                <span class="plan-type">{{ plan.type }}</span>
              </div>
              <div class="plan-area">{{ plan.area }} sq ft</div>
              <button class="btn btn--primary btn--3d plan-btn">
                <span>Download Brochure</span>
                <div class="btn-ripple"></div>
              </button>
            </div>
          </div>
        </div>

        <div class="block-content" :class="{ active: activeBlock === 'blockB' }">
          <div class="plan-grid">
            <div 
              class="plan-card" 
              :class="{ featured: plan.featured }"
              v-for="plan in blockBPlans" 
              :key="plan.id"
              @click="showFloorPlanModal(plan)"
            >
              <div class="plan-header">
                <h4>{{ plan.name }}</h4>
                <span class="plan-type">{{ plan.type }}</span>
              </div>
              <div class="plan-area">{{ plan.area }} sq ft</div>
              <button class="btn btn--primary btn--3d plan-btn">
                <span>Download Brochure</span>
                <div class="btn-ripple"></div>
              </button>
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
  name: 'FloorPlans',
  setup() {
    const activeBlock = ref('blockA')

    const blockAPlans = ref([
      { id: 1, name: 'Flat 101A', type: '3 BHK', area: '1985', featured: false },
      { id: 2, name: 'Flat 102A', type: '3 BHK', area: '1820', featured: false },
      { id: 3, name: 'Flat 103A', type: '3 BHK', area: '1645', featured: false },
      { id: 4, name: 'Flat 105A', type: '3 BHK', area: '1860', featured: false },
      { id: 5, name: 'Flat 106A', type: '3 BHK', area: '2040', featured: false },
      { id: 6, name: 'Flat 101B', type: '3 BHK Premium', area: '3815', featured: true },
      { id: 7, name: 'Flat 101C', type: '3 BHK Premium', area: '3695', featured: true }
    ])

    const blockBPlans = ref([
      { id: 8, name: 'Flat 201A', type: '3 BHK', area: '1575', featured: false },
      { id: 9, name: 'Flat 203B', type: '3 BHK', area: '1690', featured: false },
      { id: 10, name: 'Flat 204C', type: '3 BHK', area: '1665', featured: false },
      { id: 11, name: 'Flat 205D', type: '3 BHK', area: '1725', featured: false },
      { id: 12, name: 'Flat 206E', type: '3 BHK Premium', area: '3269', featured: true },
      { id: 13, name: 'Flat 207F', type: '3 BHK Premium', area: '3385', featured: true }
    ])

    const setActiveBlock = (block) => {
      activeBlock.value = block
    }

    const showFloorPlanModal = (plan) => {
      alert(`Floor Plan - ${plan.name}\n\nDetailed floor plan and pricing information will be shared during your site visit. Our team will provide comprehensive layouts and discuss all available options.`)
    }

    return {
      activeBlock,
      blockAPlans,
      blockBPlans,
      setActiveBlock,
      showFloorPlanModal
    }
  }
}
</script>
