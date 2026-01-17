<template>
  <header class="header">
    <div class="container">
      <div class="brand">
        <h1>Elegant Store</h1>
      </div>
      <nav class="nav">
        <a href="#contact" class="nav-link">Contact</a>
        <a href="#about" class="nav-link">About</a>
        <a href="#products" class="nav-link">Products</a>
      </nav>
      <button @click="$emit('toggle-theme')" class="theme-toggle">
        <SunIcon v-if="isDark" class="icon" />
        <MoonIcon v-else class="icon" />
      </button>
    </div>
  </header>
</template>

<script>
import { SunIcon, MoonIcon } from '@heroicons/vue/24/outline';

export default {
  name: 'AppHeader',
  components: { SunIcon, MoonIcon },
  props: {
    isDark: Boolean
  },
  emits: ['toggle-theme']
};
</script>

<style scoped>
.header {
  background: var(--header-bg);
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: background 0.3s ease;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

.brand h1 {
  margin: 0;
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--brand-color);
}

.nav {
  display: flex;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: var(--nav-color);
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-link:hover {
  color: var(--accent-color);
}

.theme-toggle {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: background 0.3s ease, transform 0.2s ease;
}

.theme-toggle:hover {
  transform: scale(1.05);
}

.icon {
  width: 1.2rem;
  height: 1.2rem;
}

@media (max-width: 768px) {
  .container {
    flex-direction: column;
    gap: 1rem;
  }

  .nav {
    gap: 1rem;
  }

  .brand h1 {
    font-size: 1.5rem;
  }
}
</style>