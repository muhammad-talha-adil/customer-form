<template>
  <div class="form-card">
    <h2>Place Your Order</h2>
    <p>Fill out the form below and we'll get back to you soon!</p>

    <div v-if="!submitted">
      <form @submit.prevent="sendEmail" ref="form" class="customer-form">
        <div class="form-group">
          <label for="name">Name</label>
          <input type="text" id="name" v-model="form.name" placeholder="Enter your full name" required />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>

        <div class="form-group">
          <label for="address">Address</label>
          <textarea id="address" v-model="form.address" placeholder="Enter your full address" required></textarea>
          <span v-if="errors.address" class="error">{{ errors.address }}</span>
        </div>

        <div class="form-group">
          <label for="phone">WhatsApp/Contact</label>
          <input type="text" id="phone" :value="form.phone" @input="formatPhone" @keypress="isNumber" inputmode="numeric" maxlength="12" placeholder="0321-1144567" required />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>

        <button type="submit" class="submit-btn" :disabled="isSubmitting">
          {{ isSubmitting ? 'Sending...' : 'Submit' }}
        </button>
      </form>

      <p v-if="message" :class="['message', messageType]">{{ message }}</p>
    </div>

    <div v-else class="success-message">
      <h2>🎉 Congratulations! 🎉</h2>
      <p>Your order has been placed successfully!</p>
      <p>Our team will contact you soon.</p>
      <vue-confetti :active="confettiActive" :duration="0" />
    </div>
  </div>
</template>

<script>
import emailjs from '@emailjs/browser';
import VueConfetti from 'vue-confetti';

export default {
  name: 'CustomerForm',
  components: { VueConfetti },
  data() {
    return {
      form: { name: '', address: '', phone: '' },
      errors: { name: '', address: '', phone: '' },
      isSubmitting: false,
      message: '',
      messageType: '',
      submitted: false,
      confettiActive: false
    };
  },
  methods: {
    formatPhone(event) {
      let value = event.target.value.replace(/\D/g, '');
      if (value.length > 11) value = value.slice(0, 11);
      if (value.length >= 4) {
        value = value.slice(0, 4) + '-' + value.slice(4);
      }
      this.form.phone = value;
    },
    isNumber(event) {
      if (!/[0-9]/.test(event.key) && event.key !== 'Backspace' && event.key !== 'Delete' && event.key !== 'Tab') {
        event.preventDefault();
      }
    },
    validateForm() {
      this.errors = { name: '', address: '', phone: '' };
      let isValid = true;

      if (!this.form.name.trim()) {
        this.errors.name = 'Name is required.';
        isValid = false;
      }

      if (!this.form.address.trim()) {
        this.errors.address = 'Address is required.';
        isValid = false;
      }

      if (!this.form.phone.trim()) {
        this.errors.phone = 'Phone number is required.';
        isValid = false;
      } else {
        const phoneDigits = this.form.phone.replace(/\D/g, '');
        if (phoneDigits.length !== 11 || !phoneDigits.startsWith('03')) {
          this.errors.phone = 'Please enter a valid Pakistani phone number (11 digits starting with 03).';
          isValid = false;
        }
      }

      return isValid;
    },
    async sendEmail() {
      if (!this.validateForm()) return;

      this.isSubmitting = true;
      this.message = '';

      try {
        await emailjs.sendForm(
          'YOUR_SERVICE_ID',
          'YOUR_TEMPLATE_ID',
          this.$refs.form,
          'YOUR_PUBLIC_KEY'
        );
        this.submitted = true;
        this.confettiActive = true;
      } catch (error) {
        this.message = 'Failed to send form. Please try again.';
        this.messageType = 'error';
        console.error('EmailJS error:', error);
      } finally {
        this.isSubmitting = false;
      }
    }
  }
};
</script>

<style scoped>
.form-card {
  background: var(--card-bg);
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 10px 30px var(--shadow);
  max-width: 500px;
  width: 100%;
}

.form-card h2 {
  margin: 0 0 0.5rem 0;
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text-color);
}

.form-card p {
  margin: 0 0 2rem 0;
  color: var(--text-color);
  opacity: 0.8;
}

.customer-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: var(--text-color);
}

input,
textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  background-color: #ffffff;
  color: #000000;
  box-sizing: border-box;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
  outline: none;
}

input:focus,
textarea:focus {
  border-color: var(--accent-color);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

textarea {
  resize: vertical;
  min-height: 80px;
}

.submit-btn {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 600;
  transition: background 0.3s ease, transform 0.2s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.message {
  margin-top: 1rem;
  text-align: center;
  font-weight: 500;
  padding: 0.75rem;
  border-radius: 8px;
  animation: fadeIn 0.5s ease-in;
}

.message.success {
  background-color: #d1fae5;
  color: #065f46;
  border: 1px solid #a7f3d0;
}

.message.error {
  background-color: #fee2e2;
  color: #991b1b;
  border: 1px solid #fecaca;
}

.error {
  color: #dc2626;
  font-size: 0.875rem;
  margin-top: 0.25rem;
  display: block;
}

.success-message {
  text-align: center;
  padding: 2rem 0;
  color: var(--text-color);
}

.success-message h2 {
  margin: 0 0 1rem 0;
  font-size: 1.5rem;
}

.success-message p {
  margin: 0.5rem 0;
  opacity: 0.9;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .form-card {
    padding: 1.5rem;
    max-width: 100%;
  }

  .form-card h2 {
    font-size: 1.5rem;
  }
}
</style>
