<template>
  <div class="form-container">
    <header>
      <div class="header-content">
        <div class="logo-section">
          <BuildingOfficeIcon class="logo" />
          <h1><span>Place Your Order</span></h1>
        </div>
        <p class="subtitle">Fill out the form below and we'll get back to you soon!</p>
      </div>
      <button @click="toggleTheme" class="theme-toggle">
        <SunIcon v-if="isDark" class="icon" />
        <MoonIcon v-else class="icon" />
        {{ isDark ? 'Light' : 'Dark' }}
      </button>
    </header>

    <form @submit.prevent="sendEmail" ref="form" class="customer-form">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="form.name" required />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>

      <div class="form-group">
        <label for="address">Address</label>
        <textarea id="address" v-model="form.address" required></textarea>
        <span v-if="errors.address" class="error">{{ errors.address }}</span>
      </div>

      <div class="form-group">
        <label for="phone">WhatsApp/Contact</label>
        <input type="tel" id="phone" v-model="form.phone" required />
        <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
      </div>

      <button type="submit" class="submit-btn" :disabled="isSubmitting">
        {{ isSubmitting ? 'Sending...' : 'Submit' }}
      </button>
    </form>

    <p v-if="message" :class="['message', messageType]">{{ message }}</p>
  </div>
</template>

<script>
import emailjs from '@emailjs/browser';
import { BuildingOfficeIcon, SunIcon, MoonIcon } from '@heroicons/vue/24/outline';

export default {
  name: 'CustomerForm',
  components: { BuildingOfficeIcon, SunIcon, MoonIcon },
  data() {
    return {
      isDark: false,
      form: { name: '', address: '', phone: '' },
      errors: { name: '', address: '', phone: '' },
      isSubmitting: false,
      message: '',
      messageType: ''
    };
  },
  mounted() {
    this.isDark = localStorage.getItem('theme') === 'dark';
    this.applyTheme();
  },
  methods: {
    toggleTheme() {
      this.isDark = !this.isDark;
      localStorage.setItem('theme', this.isDark ? 'dark' : 'light');
      this.applyTheme();
    },
    applyTheme() {
      document.documentElement.setAttribute('data-theme', this.isDark ? 'dark' : 'light');
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
      } else if (!/^\+?\d{10,15}$/.test(this.form.phone.replace(/\s/g, ''))) {
        this.errors.phone = 'Please enter a valid phone number.';
        isValid = false;
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
        this.message = 'Form submitted successfully!';
        this.messageType = 'success';
        this.form = { name: '', address: '', phone: '' };
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

<style>
/* ========= THEME TOKENS ========= */
:root {
  /* Light mode */
  --bg-color: rgba(255, 248, 240, 0.95);
  --text-color: #2d1810;

  --input-bg: rgba(255, 255, 255, 0.95);
  --input-border: #000000;              /* light mode border black */
  --input-focus-bg: #f3e8ff;            /* focus bg purple */
  --input-focus-border: #7c3aed;        /* focus border purple */

  --btn-bg: linear-gradient(135deg, #f97316 0%, #ea580c 50%, #dc2626 100%);
  --btn-text: #ffffff;

  --header-bg: linear-gradient(135deg, #fed7aa 0%, #fdba74 50%, #fb923c 100%);
  --accent-gold: #d97706;
  --premium-purple: #7c3aed;            /* heading color/gradient (light) */

  --glow-bg: radial-gradient(circle at 30% 20%, rgba(124, 58, 237, 0.35) 0%, transparent 55%), radial-gradient(circle at 70% 80%, rgba(168, 85, 247, 0.28) 0%, transparent 55%), radial-gradient(circle at 50% 50%, rgba(192, 132, 252, 0.22) 0%, transparent 60%);
  --shadow-color: rgba(124, 58, 237, 0.18);

  --success-color: #059669;
  --error-color: #dc2626;
}

[data-theme="dark"] {
  /* Dark mode */
  --bg-color: rgba(15, 23, 42, 0.95);
  --text-color: #d4af37;                /* golden text */

  --input-bg: #ffffff;                  /* dark mode inputs white bg */
  --input-border: rgba(0, 0, 0, 0.25);
  --input-focus-bg: #ffffff;
  --input-focus-border: #fbbf24;        /* focus outline golden */

  --btn-bg: linear-gradient(135deg, #7c3aed 0%, #a855f7 50%, #c084fc 100%);
  --btn-text: #ffffff;

  --header-bg: linear-gradient(135deg, #1e1b4b 0%, #312e81 50%, #4c1d95 100%);
  --accent-gold: #fbbf24;
  --premium-purple: #8b5cf6;

  --glow-bg: radial-gradient(circle at 30% 20%, rgba(212, 175, 55, 0.3) 0%, transparent 50%), radial-gradient(circle at 70% 80%, rgba(184, 134, 11, 0.25) 0%, transparent 50%), radial-gradient(circle at 50% 50%, rgba(139, 101, 8, 0.2) 0%, transparent 50%);
  --shadow-color: rgba(212, 175, 55, 0.1);

  --success-color: #10b981;
  --error-color: #ef4444;
}
</style>

<style scoped>
/* ========= CONTAINER ========= */
.form-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 20px;
  position: relative;
  overflow: hidden;
  background: var(--bg-color);
  color: var(--text-color);
  box-shadow: 0 20px 60px var(--shadow-color);
}

/* Background layer */
.form-container::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 20px;
  z-index: -1;
  backdrop-filter: blur(15px);
  background: var(--glow-bg);
  pointer-events: none;
}

/* ========= HEADER ========= */
header {
  text-align: center;
  margin-bottom: 30px;
  background: var(--header-bg);
  padding: 25px;
  border-radius: 16px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  position: relative;
  overflow: hidden;
}

header::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    45deg,
    rgba(255, 255, 255, 0.1) 0%,
    transparent 50%,
    rgba(255, 255, 255, 0.05) 100%
  );
  pointer-events: none;
}

.header-content {
  margin-bottom: 15px;
}

.logo-section {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-bottom: 8px;
}

.logo {
  width: 2.5rem;
  height: 2.5rem;
  color: var(--accent-gold);
  animation: bounce 2s infinite;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
}

/* Heading color */
h1 {
  margin: 0;
  font-size: 2.2rem;
  font-weight: 800;
  color: var(--premium-purple);
  letter-spacing: -0.02em;
  line-height: 1.2;
}

h1 span {
  background: linear-gradient(135deg, var(--premium-purple), var(--accent-gold));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  margin: 0;
  font-size: 1rem;
  color: var(--text-color);
  opacity: 0.85;
}

.theme-toggle {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  padding: 10px 16px;
  border-radius: 25px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 600;
  transition: transform 0.3s ease, box-shadow 0.3s ease, filter 0.3s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.theme-toggle:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  filter: brightness(1.05);
}

/* ========= FORM ========= */
.customer-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: 800;
}

/* Inputs */
input,
textarea {
  width: 100%;
  padding: 10px;
  border: 1.5px solid var(--input-border);
  border-radius: 8px;
  background-color: var(--input-bg);
  color: var(--text-color);
  box-sizing: border-box;
  transition: border-color 0.2s ease, box-shadow 0.2s ease, background-color 0.2s ease;
  outline: none; /* we'll handle focus ourselves */
}

input:focus,
textarea:focus {
  background-color: var(--input-focus-bg);
  border-color: var(--input-focus-border);
  box-shadow: 0 0 0 3px rgba(124, 58, 237, 0.18);
}

/* Dark mode focus glow */
[data-theme="dark"] input:focus,
[data-theme="dark"] textarea:focus {
  box-shadow: 0 0 0 3px rgba(251, 191, 36, 0.25);
}

textarea {
  resize: vertical;
  min-height: 80px;
}

/* Button */
.submit-btn {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  padding: 12px;
  border-radius: 10px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 700;
  transition: transform 0.2s ease, filter 0.2s ease, box-shadow 0.2s ease;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.12);
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-1px);
  filter: brightness(1.05);
  box-shadow: 0 14px 30px rgba(0, 0, 0, 0.16);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

/* Messages */
.message {
  margin-top: 15px;
  text-align: center;
  font-weight: bold;
  padding: 10px;
  border-radius: 8px;
  animation: fadeIn 0.5s ease-in;
}

.message.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.message.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

.error {
  color: #dc3545;
  font-size: 0.875rem;
  margin-top: 5px;
  display: block;
}

/* Animations */
@keyframes bounce {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
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

/* Responsive */
@media (max-width: 768px) {
  .form-container {
    padding: 15px;
  }

  header {
    padding: 15px;
  }

  .logo-section {
    flex-direction: column;
    gap: 5px;
  }

  h1 {
    font-size: 1.5rem;
  }

  .subtitle {
    font-size: 0.9rem;
  }
}
</style>
