<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Get In Touch</h2>
        <p class="section-subtitle">Schedule your site visit today and experience the BIMLA MANGAL GARDENSH difference</p>
      </div>

      <div class="contact-grid">
        <div class="contact-info">
          <div class="contact-item">
            <h4>Developer</h4>
            <p>ABHA ENGICON PVT. LTD.
</p>
          </div>
          <div class="contact-item">
            <h4>Office Address</h4>
            <p>Flat 301 Shri Ganesh Arpan, Bihar Sharif - Ekangarsarai Road, Maghra, BiharSharif, Nalanda - 803101</p>
            <br>
            <p>GE, AMBIKA ENCLAVE, SHIV BAGAN, MAKEY ROAD, NEAR RAJ BHAWAN, RANCHI</p>
          </div>
          <div class="contact-item">
            <h4>Contact Numbers</h4>
            <p><a href="tel:8521456165">8521456165</a> | <a href="tel:9905705709">9905705709</a></p>
          </div>
          <div class="contact-item">
            <h4>Email</h4>
            <p><a href="mailto:arpanmega6565@gmail.com">arpanmega6565@gmail.com</a></p>
          </div>
        </div>

        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <input 
              type="text" 
              class="form-control" 
              placeholder="Your Name" 
              v-model="form.name"
              required
            >
          </div>
          <div class="form-group">
            <input 
              type="email" 
              class="form-control" 
              placeholder="Email Address" 
              v-model="form.email"
              required
            >
          </div>
          <div class="form-group">
            <input 
              type="tel" 
              class="form-control" 
              placeholder="Phone Number" 
              v-model="form.phone"
              required
            >
          </div>
          <div class="form-group">
            <select class="form-control" v-model="form.interest" required>
              <option value="">Select Your Interest</option>
              <option value="block-a">Interested in Block A</option>
              <option value="block-b">Interested in Block B</option>
              <option value="general">General Inquiry</option>
              <option value="site-visit">Site Visit Request</option>
            </select>
          </div>
          <div class="form-group">
            <textarea 
              class="form-control" 
              rows="4" 
              placeholder="Your Message" 
              v-model="form.message"
            ></textarea>
          </div>
          <button 
            type="submit" 
            class="btn btn--primary btn--3d btn--full-width"
            :disabled="isSubmitting"
          >
            <span v-if="!isSubmitting">Schedule Site Visit</span>
            <span v-else>Sending...</span>
            <div class="btn-ripple"></div>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, reactive } from 'vue'

export default {
  name: 'Contact',
  setup() {
    const isSubmitting = ref(false)
    const form = reactive({
      name: '',
      email: '',
      phone: '',
      interest: '',
      message: ''
    })

    const handleSubmit = async () => {
      isSubmitting.value = true
      
      // Simulate form submission
      setTimeout(() => {
        alert('Thank you! Your message has been sent successfully. We will contact you soon.')
        // Reset form
        Object.keys(form).forEach(key => {
          form[key] = ''
        })
        isSubmitting.value = false
      }, 2000)
    }

    return {
      form,
      isSubmitting,
      handleSubmit
    }
  }
}
</script>
