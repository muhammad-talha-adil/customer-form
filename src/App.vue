<template>
  <CustomerForm />
</template>

<script>
import CustomerForm from './components/CustomerForm.vue'

export default {
  name: 'App',
  components: { CustomerForm }
}
</script>

<style>
#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  transition: background 0.5s ease;
  position: relative;
  overflow: hidden;
}

/* LIGHT MODE = Purple gradient */
[data-theme="light"] #app {
  background: linear-gradient(
    135deg,
    #0c0a1a 0%,
    #1e1b4b 30%,
    #312e81 60%,
    #4c1d95 100%
  );
}

[data-theme="light"] #app::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 20% 80%, rgba(139, 92, 246, 0.22) 0%, transparent 55%),
    radial-gradient(circle at 80% 20%, rgba(168, 85, 247, 0.20) 0%, transparent 55%),
    radial-gradient(circle at 40% 40%, rgba(59, 130, 246, 0.16) 0%, transparent 55%);
  pointer-events: none;
}

/* DARK MODE = Dark purple/navy gradient */
[data-theme="dark"] #app {
  background: linear-gradient(
    135deg,
    #050510 0%,
    #0c0a1a 25%,
    #1a1a2e 50%,
    #16213e 75%,
    #1e1b4b 100%
  );
}

[data-theme="dark"] #app::before {
  background:
    radial-gradient(circle at 20% 80%, rgba(139, 92, 246, 0.18) 0%, transparent 55%),
    radial-gradient(circle at 80% 20%, rgba(168, 85, 247, 0.18) 0%, transparent 55%),
    radial-gradient(circle at 40% 40%, rgba(59, 130, 246, 0.12) 0%, transparent 55%);
}
</style>
