<template>
  <div id="app">
    <AppHeader :is-dark="isDark" @toggle-theme="toggleTheme" />
    <main id="contact" class="main">
      <div class="container">
        <div class="left-column">
          <img src="https://picsum.photos/600/800?random=1" alt="Store Image" class="store-image" />
        </div>
        <div class="right-column">
          <CustomerForm />
        </div>
      </div>
    </main>
    <AboutSection />
    <ProductsSection />
    <AppFooter />
    <a href="https://wa.me/1234567890" target="_blank" class="whatsapp-float">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
        <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.488"/>
      </svg>
    </a>
  </div>
</template>

<script>
import AppHeader from './components/Header.vue'
import AppFooter from './components/Footer.vue'
import CustomerForm from './components/CustomerForm.vue'
import AboutSection from './components/AboutSection.vue'
import ProductsSection from './components/ProductsSection.vue'

export default {
  name: 'App',
  components: { AppHeader, AppFooter, CustomerForm, AboutSection, ProductsSection },
  data() {
    return {
      isDark: false
    }
  },
  mounted() {
    this.isDark = localStorage.getItem('theme') === 'dark' || !localStorage.getItem('theme')
    this.applyTheme()
  },
  methods: {
    toggleTheme() {
      this.isDark = !this.isDark
      localStorage.setItem('theme', this.isDark ? 'dark' : 'light')
      this.applyTheme()
    },
    applyTheme() {
      document.documentElement.setAttribute('data-theme', this.isDark ? 'dark' : 'light')
    }
  }
}
</script>

<style>
:root {
  /* Light theme */
  --bg-color: #f8fafc;
  --text-color: #1e293b;
  --header-bg: #ffffff;
  --footer-bg: #f1f5f9;
  --footer-text: #64748b;
  --brand-color: #1e293b;
  --nav-color: #475569;
  --accent-color: #3b82f6;
  --btn-bg: #3b82f6;
  --btn-text: #ffffff;
  --card-bg: #ffffff;
  --shadow: rgba(0, 0, 0, 0.1);
}

[data-theme="dark"] {
  --bg-color: #0f172a;
  --text-color: #f1f5f9;
  --header-bg: #1e293b;
  --footer-bg: #0f172a;
  --footer-text: #94a3b8;
  --brand-color: #f1f5f9;
  --nav-color: #cbd5e1;
  --accent-color: #60a5fa;
  --btn-bg: #1d4ed8;
  --btn-text: #ffffff;
  --card-bg: #1e293b;
  --shadow: rgba(0, 0, 0, 0.3);
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: var(--bg-color);
  color: var(--text-color);
  transition: background 0.3s ease, color 0.3s ease;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main {
  flex: 1;
  padding: 2rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  padding: 0 2rem;
}

.left-column {
  display: flex;
  justify-content: center;
  align-items: center;
}

.store-image {
  width: 100%;
  height: 500px;
  object-fit: cover;
  border-radius: 12px;
  box-shadow: 0 10px 30px var(--shadow);
}

.right-column {
  display: flex;
  justify-content: center;
  align-items: start;
}

.whatsapp-float {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  background: #25d366;
  color: white;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease;
  text-decoration: none;
}

.whatsapp-float:hover {
  transform: scale(1.1);
}

@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
    gap: 1rem;
    padding: 0 1rem;
  }

  .left-column {
    order: 2;
  }

  .right-column {
    order: 1;
  }

  .store-image {
    max-width: 100%;
  }
}
</style>
