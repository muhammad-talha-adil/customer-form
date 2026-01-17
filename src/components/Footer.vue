<template>
  <footer class="footer">
    <div class="container">
      <p>&copy; 2023 Elegant Store. All rights reserved.</p>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter'
};
</script>

<style scoped>
.footer {
  background: var(--footer-bg);
  padding: 1rem 0;
  text-align: center;
  color: var(--footer-text);
  transition: background 0.3s ease;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 768px) {
  .container {
    padding: 0 1rem;
  }
}
</style>