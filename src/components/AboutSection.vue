<template>
  <section id="about" class="about-section">
    <div class="container">
      <h2 class="section-title">About Us</h2>
      <div class="about-content">
        <div class="about-text">
          <p class="about-description">
            Welcome to Elegant Store, where style meets sophistication. We curate the finest collection of premium products designed to elevate your lifestyle.
          </p>
          <p class="about-details">
            Our commitment to quality and elegance ensures that every item in our store reflects the highest standards of craftsmanship and design. From timeless classics to contemporary masterpieces, we bring you products that tell a story of luxury and refinement.
          </p>
          <div class="stats">
            <div class="stat">
              <h3>500+</h3>
              <p>Happy Customers</p>
            </div>
            <div class="stat">
              <h3>1000+</h3>
              <p>Products Sold</p>
            </div>
            <div class="stat">
              <h3>5★</h3>
              <p>Customer Rating</p>
            </div>
          </div>
        </div>
        <div class="about-image">
          <img src="https://picsum.photos/500/400?random=2" alt="About Us" class="about-img" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection'
};
</script>

<style scoped>
.about-section {
  padding: 6rem 0;
  background: linear-gradient(135deg, var(--card-bg) 0%, rgba(59, 130, 246, 0.05) 100%);
  position: relative;
  overflow: hidden;
}

.about-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 30%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(168, 85, 247, 0.08) 0%, transparent 50%);
  pointer-events: none;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  text-align: center;
  margin-bottom: 4rem;
  background: linear-gradient(135deg, var(--text-color), var(--accent-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  opacity: 0;
  animation: fadeInUp 1s ease-out forwards;
  letter-spacing: -0.02em;
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, var(--accent-color), var(--brand-color));
  border-radius: 2px;
  animation: slideIn 1.2s ease-out 0.5s both;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
}

.about-text {
  animation: fadeInLeft 1s ease-out 0.3s both;
}

.about-description {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  color: var(--text-color);
}

.about-details {
  font-size: 1rem;
  line-height: 1.6;
  color: var(--text-color);
  opacity: 0.9;
}

.stats {
  display: flex;
  gap: 3rem;
  margin-top: 3rem;
  justify-content: center;
}

.stat {
  text-align: center;
  background: var(--card-bg);
  padding: 2rem 1.5rem;
  border-radius: 16px;
  box-shadow: 0 8px 25px var(--shadow);
  border: 1px solid rgba(59, 130, 246, 0.1);
  animation: fadeInUp 1s ease-out 0.6s both;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.stat:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 35px var(--shadow);
}

.stat:nth-child(2) {
  animation-delay: 0.8s;
}

.stat:nth-child(3) {
  animation-delay: 1s;
}

.stat h3 {
  font-size: 2.5rem;
  font-weight: 800;
  background: linear-gradient(135deg, var(--accent-color), var(--brand-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin: 0 0 0.5rem 0;
}

.stat p {
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-color);
  margin: 0;
  opacity: 0.9;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.about-image {
  animation: fadeInRight 1s ease-out 0.3s both;
}

.about-img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  border-radius: 12px;
  box-shadow: 0 10px 30px var(--shadow);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideIn {
  from {
    width: 0;
  }
  to {
    width: 80px;
  }
}

@media (max-width: 768px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .stats {
    flex-direction: column;
    gap: 1rem;
  }

  .about-img {
    height: 300px;
  }
}
</style>