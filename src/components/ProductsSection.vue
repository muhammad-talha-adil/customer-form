<template>
  <section id="products" class="products-section">
    <div class="container">
      <h2 class="section-title">Our Products</h2>
      <div class="carousel-container">
        <button class="carousel-btn prev" @click="prevSlide">&lt;</button>
        <div class="carousel-track" :style="{ transform: `translateX(-${currentIndex * (100 / itemsToShow)}%)` }">
          <div
            v-for="product in products"
            :key="product.name"
            class="product-slide"
            :style="{ flex: `0 0 ${100 / itemsToShow}%` }"
          >
            <div
              class="product-card"
              @click="openModal(product)"
            >
              <img :src="product.image" :alt="product.name" class="product-image" />
              <div class="product-info">
                <h3>{{ product.name }}</h3>
                <p class="price">${{ product.price }}</p>
                <p class="short-desc">{{ product.shortDesc }}</p>
              </div>
              <div class="hover-overlay">
                <p>{{ product.hoverDesc }}</p>
                <button class="view-btn">View Details</button>
              </div>
            </div>
          </div>
        </div>
        <button class="carousel-btn next" @click="nextSlide">&gt;</button>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="selectedProduct" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <button class="close-btn" @click="closeModal">&times;</button>
        <img :src="selectedProduct.image" :alt="selectedProduct.name" class="modal-image" />
        <div class="modal-details">
          <h3>{{ selectedProduct.name }}</h3>
          <p class="price">${{ selectedProduct.price }}</p>
          <p class="description">{{ selectedProduct.description }}</p>
          <ul class="features">
            <li v-for="feature in selectedProduct.features" :key="feature">{{ feature }}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductsSection',
  data() {
    return {
      selectedProduct: null,
      currentIndex: 0,
      itemsToShow: 5,
      products: [
        {
          name: 'Premium Watch',
          price: 299,
          image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=400',
          shortDesc: 'Elegant timepiece',
          hoverDesc: 'Timeless design with precision movement',
          description: 'This premium watch combines classic elegance with modern technology. Crafted from the finest materials, it features a sapphire crystal face and automatic movement.',
          features: ['Automatic movement', 'Sapphire crystal', 'Stainless steel case', 'Water resistant']
        },
        {
          name: 'Designer Handbag',
          price: 450,
          image: 'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=400',
          shortDesc: 'Luxury leather bag',
          hoverDesc: 'Handcrafted with genuine leather',
          description: 'A sophisticated handbag made from premium leather. Perfect for both professional and casual occasions.',
          features: ['Genuine leather', 'Multiple compartments', 'Adjustable strap', 'Durable stitching']
        },
        {
          name: 'Wireless Headphones',
          price: 199,
          image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=400',
          shortDesc: 'High-quality audio',
          hoverDesc: 'Immersive sound experience',
          description: 'Experience crystal-clear audio with these wireless headphones. Featuring noise cancellation and long battery life.',
          features: ['Noise cancellation', '30-hour battery', 'Wireless charging', 'Comfortable fit']
        },
        {
          name: 'Smartphone Case',
          price: 49,
          image: 'https://images.unsplash.com/photo-1601593346740-925612772716?w=400',
          shortDesc: 'Protective cover',
          hoverDesc: 'Military-grade protection',
          description: 'Protect your device with this rugged case. Designed to withstand drops and scratches.',
          features: ['Shock absorbent', 'Screen protection', 'Wireless charging compatible', 'Slim design']
        },
        {
          name: 'Coffee Maker',
          price: 129,
          image: 'https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=400',
          shortDesc: 'Brew perfect coffee',
          hoverDesc: 'Programmable brewing system',
          description: 'Start your day right with this advanced coffee maker. Brews rich, flavorful coffee every time.',
          features: ['Programmable timer', 'Thermal carafe', 'Auto shut-off', '12-cup capacity']
        },
        {
          name: 'Fitness Tracker',
          price: 149,
          image: 'https://images.unsplash.com/photo-1575311373937-040b8e1fd5b6?w=400',
          shortDesc: 'Track your health',
          hoverDesc: 'Monitor heart rate and activity',
          description: 'Stay fit and healthy with this comprehensive fitness tracker. Tracks steps, heart rate, and sleep.',
          features: ['Heart rate monitor', 'Sleep tracking', 'Water resistant', '7-day battery']
        },
        {
          name: 'Desk Lamp',
          price: 89,
          image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400',
          shortDesc: 'Modern lighting',
          hoverDesc: 'Adjustable LED lamp',
          description: 'Illuminate your workspace with this sleek desk lamp. Features adjustable brightness and color temperature.',
          features: ['LED technology', 'Adjustable arm', 'USB charging port', 'Energy efficient']
        },
        {
          name: 'Yoga Mat',
          price: 39,
          image: 'https://images.unsplash.com/photo-1544367567-0f2fcb009e0b?w=400',
          shortDesc: 'Non-slip surface',
          hoverDesc: 'Eco-friendly and durable',
          description: 'Enhance your yoga practice with this high-quality mat. Provides excellent grip and comfort.',
          features: ['Non-slip surface', 'Eco-friendly material', '6mm thickness', 'Carrying strap included']
        },
        {
          name: 'Bluetooth Speaker',
          price: 79,
          image: 'https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?w=400',
          shortDesc: 'Portable audio',
          hoverDesc: '360-degree sound',
          description: 'Enjoy music anywhere with this compact Bluetooth speaker. Delivers rich, immersive sound.',
          features: ['360° sound', 'Water resistant', '12-hour battery', 'Voice assistant compatible']
        },
        {
          name: 'Sunglasses',
          price: 159,
          image: 'https://images.unsplash.com/photo-1572635196237-14b3f281503f?w=400',
          shortDesc: 'UV protection',
          hoverDesc: 'Polarized lenses',
          description: 'Protect your eyes in style with these premium sunglasses. Features polarized lenses and UV protection.',
          features: ['Polarized lenses', 'UV400 protection', 'Lightweight frame', 'Scratch resistant']
        },
        {
          name: 'Laptop',
          price: 999,
          image: 'https://images.unsplash.com/photo-1496181133206-80ce9b88a853?w=400',
          shortDesc: 'High-performance computing',
          hoverDesc: 'Powerful processor and sleek design',
          description: 'Experience top-tier performance with this lightweight laptop. Perfect for work, gaming, and entertainment.',
          features: ['Intel i7 processor', '16GB RAM', '512GB SSD', '15.6" Full HD display']
        },
        {
          name: 'Sneakers',
          price: 129,
          image: 'https://images.unsplash.com/photo-1549298916-b41d501d3772?w=400',
          shortDesc: 'Comfortable footwear',
          hoverDesc: 'Breathable and stylish',
          description: 'Step out in style with these versatile sneakers. Designed for comfort and durability.',
          features: ['Breathable mesh', 'Cushioned sole', 'Slip-resistant', 'Lightweight']
        },
        {
          name: 'Digital Camera',
          price: 599,
          image: 'https://images.unsplash.com/photo-1502920917128-1aa500764cbd?w=400',
          shortDesc: 'Capture memories',
          hoverDesc: 'High-resolution imaging',
          description: 'Capture stunning photos and videos with this advanced digital camera. Ideal for photography enthusiasts.',
          features: ['24MP sensor', '4K video', 'Optical zoom', 'WiFi connectivity']
        },
        {
          name: 'Novel Book',
          price: 19,
          image: 'https://images.unsplash.com/photo-1544947950-fa07a98d237f?w=400',
          shortDesc: 'Engaging storyline',
          hoverDesc: 'Bestselling fiction',
          description: 'Dive into an captivating story with this bestselling novel. A must-read for book lovers.',
          features: ['Paperback edition', '500 pages', 'Award-winning author', 'Page-turner']
        },
        {
          name: 'Perfume',
          price: 89,
          image: 'https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?w=400',
          shortDesc: 'Elegant fragrance',
          hoverDesc: 'Long-lasting scent',
          description: 'Indulge in this luxurious perfume. A blend of exotic notes for a sophisticated aroma.',
          features: ['Floral notes', 'Long-lasting', '100ml bottle', 'Suitable for all occasions']
        },
        {
          name: 'Gold Ring',
          price: 299,
          image: 'https://images.unsplash.com/photo-1605100804763-247f67b3557e?w=400',
          shortDesc: 'Timeless jewelry',
          hoverDesc: '18k gold craftsmanship',
          description: 'Adorn your fingers with this exquisite gold ring. Symbolizes elegance and style.',
          features: ['18k gold', 'Gemstone accent', 'Hypoallergenic', 'Lifetime warranty']
        },
        {
          name: 'Acoustic Guitar',
          price: 349,
          image: 'https://images.unsplash.com/photo-1510915361894-db8b60106cb1?w=400',
          shortDesc: 'Musical instrument',
          hoverDesc: 'Rich sound quality',
          description: 'Play beautiful melodies with this acoustic guitar. Perfect for beginners and professionals.',
          features: ['Spruce top', 'Mahogany back', 'Steel strings', 'Comfortable neck']
        },
        {
          name: 'Indoor Plant',
          price: 49,
          image: 'https://images.unsplash.com/photo-1416879595882-3373a0480b5b?w=400',
          shortDesc: 'Natural decor',
          hoverDesc: 'Low-maintenance greenery',
          description: 'Bring life to your space with this beautiful indoor plant. Easy to care for and air-purifying.',
          features: ['Air-purifying', 'Low light tolerant', 'Ceramic pot included', 'Pet-friendly']
        }
      ]
    };
  },
  methods: {
    openModal(product) {
      this.selectedProduct = product;
    },
    closeModal() {
      this.selectedProduct = null;
    },
    nextSlide() {
      if (this.currentIndex < this.products.length - this.itemsToShow) {
        this.currentIndex += 1;
      } else if (this.currentIndex === this.products.length - this.itemsToShow) {
        this.currentIndex = 0; // wrap around
      }
    },
    prevSlide() {
      if (this.currentIndex > 0) {
        this.currentIndex -= 1;
      } else {
        this.currentIndex = this.products.length - this.itemsToShow; // wrap around
      }
    },
    updateItemsToShow() {
      this.itemsToShow = 2;
      // Reset index if out of bounds
      if (this.currentIndex > this.products.length - this.itemsToShow) {
        this.currentIndex = Math.max(0, this.products.length - this.itemsToShow);
      }
    }
  },
  mounted() {
    this.updateItemsToShow();
    window.addEventListener('resize', this.updateItemsToShow);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.updateItemsToShow);
  }
};
</script>

<style scoped>
.products-section {
  padding: 6rem 0;
  background: linear-gradient(135deg, var(--bg-color) 0%, rgba(168, 85, 247, 0.05) 100%);
  position: relative;
  overflow: hidden;
}

.products-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 30% 20%, rgba(168, 85, 247, 0.08) 0%, transparent 50%),
    radial-gradient(circle at 70% 80%, rgba(59, 130, 246, 0.06) 0%, transparent 50%);
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
}

.product-card {
  background: var(--card-bg);
  border-radius: 16px;
  box-shadow: 0 8px 25px var(--shadow);
  overflow: hidden;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  border: 1px solid rgba(59, 130, 246, 0.1);
}

.product-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 40px var(--shadow);
}

.product-image {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.product-info {
  padding: 1.5rem;
}

.product-info h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.2rem;
  color: var(--text-color);
}

.price {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--accent-color);
  margin: 0 0 0.5rem 0;
}

.short-desc {
  margin: 0;
  color: var(--text-color);
  opacity: 0.8;
  font-size: 0.9rem;
}

.hover-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  padding: 1rem;
  text-align: center;
}

.product-card:hover .hover-overlay {
  opacity: 1;
}

.hover-overlay p {
  color: white;
  margin: 0 0 1rem 0;
  font-size: 0.9rem;
}

.view-btn {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  transition: background 0.3s ease;
}

.view-btn:hover {
  background: var(--accent-color);
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: var(--card-bg);
  border-radius: 20px;
  max-width: 700px;
  width: 90%;
  max-height: 80vh;
  overflow-y: auto;
  position: relative;
  animation: modalFadeIn 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  box-shadow: 0 25px 50px var(--shadow);
  border: 1px solid rgba(59, 130, 246, 0.2);
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: var(--text-color);
  z-index: 1;
}

.modal-image {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 12px 12px 0 0;
}

.modal-details {
  padding: 1.5rem;
  text-align: center;
}

.modal-details h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text-color);
  background: linear-gradient(135deg, var(--text-color), var(--accent-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.modal-details .price {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: var(--accent-color);
}

.description {
  margin-bottom: 1.5rem;
  color: var(--text-color);
  line-height: 1.7;
  font-size: 1.1rem;
  text-align: center;
}

.features {
  list-style: none;
  padding: 0;
  background: rgba(59, 130, 246, 0.05);
  border-radius: 12px;
  padding: 1rem;
  text-align: center;
}

.features li {
  padding: 0.75rem 0;
  border-bottom: 1px solid rgba(59, 130, 246, 0.1);
  color: var(--text-color);
  position: relative;
}

.features li:last-child {
  border-bottom: none;
}

.features li::before {
  content: '✓ ';
  color: var(--accent-color);
  font-weight: bold;
}

@keyframes modalFadeIn {
  from {
    opacity: 0;
    transform: scale(0.8) translateY(-20px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.carousel-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
}

.carousel-navigation {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  z-index: 10;
}

.carousel-track {
  display: flex;
  transition: transform 0.3s ease;
  width: 100%;
}

.product-slide {
  padding: 0 1rem;
  box-sizing: border-box;
}

.carousel-btn {
  background: var(--btn-bg);
  color: var(--btn-text);
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 10;
  font-size: 1.2rem;
  font-weight: bold;
  box-shadow: 0 4px 12px var(--shadow);
  transition: background 0.3s ease, transform 0.2s ease;
}

.carousel-btn:hover {
  background: var(--accent-color);
  transform: scale(1.1);
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }

  .modal-content {
    width: 95%;
  }

  .carousel-btn {
    width: 35px;
    height: 35px;
    font-size: 1rem;
  }
}
</style>