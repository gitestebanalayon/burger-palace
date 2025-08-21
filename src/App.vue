<template>
  <div class="app">
    <!-- Header fijo -->
    <header class="header" :class="{ 'header-scrolled': scrolled }">
      <nav class="nav" style="max-width: 1200px; margin: auto; padding-left: 1.3rem; padding-right: 1.3rem;">
        <div class="nav-content">
          <div class="logo">
            <div class="logo-icon">🍔</div>
            <h1 class="logo-text">Burger Palace</h1>
          </div>

          <!-- Menú desktop -->
          <ul class="nav-menu desktop-menu">
            <li v-for="item in menuItems" :key="item.id">
              <a @click="scrollToSection(item.id)" class="nav-link">
                {{ item.name }}
              </a>
            </li>
          </ul>

          <!-- Botón menú móvil -->
          <button @click="mobileMenuOpen = !mobileMenuOpen" class="mobile-menu-btn">
            <svg class="menu-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>

        <!-- Menú móvil -->
        <div v-if="mobileMenuOpen" class="mobile-menu">
          <ul class="mobile-menu-list">
            <li v-for="item in menuItems" :key="item.id">
              <a @click="scrollToSection(item.id); mobileMenuOpen = false" class="mobile-menu-link">
                {{ item.name }}
              </a>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <!-- Sección Inicio -->
    <section id="inicio" class="hero-section">
      <div class="container mx-auto px-4 py-4">
        <div class="hero-content">
          <div class="hero-text" :class="{ 'fade-in-left': isVisible.inicio }">
            <h2 class="hero-title">
              Las Mejores
              <span class="hero-highlight">Hamburguesas</span>
              de la Ciudad
            </h2>
            <p class="hero-description">
              Ingredientes frescos, sabores únicos y la mejor experiencia gastronómica te esperan en Burger Palace.
            </p>
            <button @click="scrollToSection('menu')" class="btn btn-primary hero-cta">
              Ver Nuestro Menú
            </button>
          </div>
          <div class="hero-image" :class="{ 'fade-in-right': isVisible.inicio }">
            <img src="../public/gourmet-burger-prep.png" alt="Hamburguesa gourmet" class="hero-img">
            <div class="hero-badge">¡Nuevo!</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección Menú -->
    <section id="menu" class="menu-section">
      <div class="container">
        <div class="section-header" :class="{ 'fade-in-up': isVisible.menu }">
          <h2 class="section-title">Nuestro Menú</h2>
          <p class="section-description">
            Descubre nuestras deliciosas hamburguesas preparadas con ingredientes frescos y de la más alta calidad
          </p>
        </div>

        <div class="menu-grid">
          <div v-for="(burger, index) in burgers" :key="burger.id" class="menu-card"
            :class="{ 'fade-in-up': isVisible.menu }" :style="{ animationDelay: `${index * 0.1}s` }">
            <div class="menu-card-image">
              <img :src="burger.image" :alt="burger.name" class="card-img">
              <div class="price-badge">
                ${{ burger.price }}
              </div>
            </div>
            <div class="menu-card-content">
              <h3 class="card-title">{{ burger.name }}</h3>
              <p class="card-description">{{ burger.description }}</p>
              <button class="btn btn-secondary card-btn">
                Ordenar Ahora
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección Acerca de -->
    <section id="acerca" class="about-section">
      <div class="container">
        <div class="about-content">
          <div class="about-image" :class="{ 'fade-in-left': isVisible.acerca }">
            <img src="../public/spicy-jalapeno-avocado-burger.png" alt="Nuestra cocina" class="about-img">
          </div>
          <div class="about-text" :class="{ 'fade-in-right': isVisible.acerca }">
            <h2 class="about-title">Nuestra Historia</h2>
            <p class="about-description">
              Desde 2015, Burger Palace ha sido el hogar de las hamburguesas más deliciosas de la ciudad.
              Comenzamos como un pequeño negocio familiar con una gran pasión por la comida de calidad.
            </p>
            <p class="about-description">
              Utilizamos solo ingredientes frescos y locales, carnes de la mejor calidad y recetas secretas
              que han sido perfeccionadas a lo largo de los años. Cada hamburguesa es preparada con amor y dedicación.
            </p>
            <div class="stats-grid">
              <div class="stat-card">
                <div class="stat-number">9+</div>
                <div class="stat-label">Años de experiencia</div>
              </div>
              <div class="stat-card">
                <div class="stat-number">75k+</div>
                <div class="stat-label">Clientes felices</div>
              </div>
              <div class="stat-card">
                <div class="stat-number">20</div>
                <div class="stat-label">Variedades únicas</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección Contacto -->
    <section id="contacto" class="contact-section">
      <div class="container">
        <div class="section-header" :class="{ 'fade-in-up': isVisible.contacto }">
          <h2 class="section-title">Contáctanos</h2>
          <p class="section-description">¿Tienes alguna pregunta? ¡Nos encantaría escucharte!</p>
        </div>

        <div class="contact-content">
          <div class="contact-info" :class="{ 'fade-in-left': isVisible.contacto }">
            <h3 class="contact-title">Información de Contacto</h3>
            <div class="contact-items">
              <div class="contact-item">
                <div class="contact-icon">📍</div>
                <div class="contact-details">
                  <h4 class="contact-label">Dirección</h4>
                  <p class="contact-value">Av. Principal 123, Centro, Ciudad</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">📞</div>
                <div class="contact-details">
                  <h4 class="contact-label">Teléfono</h4>
                  <p class="contact-value">+1 (555) 123-4567</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">⏰</div>
                <div class="contact-details">
                  <h4 class="contact-label">Horarios</h4>
                  <p class="contact-value">Lun - Dom: 11:00 AM - 11:00 PM</p>
                </div>
              </div>
            </div>
          </div>

          <div class="contact-form-wrapper" :class="{ 'fade-in-right': isVisible.contacto }">
            <form @submit.prevent="submitForm" class="contact-form">
              <div class="form-group">
                <label class="form-label">Nombre</label>
                <input v-model="form.name" type="text" class="form-input" required>
              </div>
              <div class="form-group">
                <label class="form-label">Email</label>
                <input v-model="form.email" type="email" class="form-input" required>
              </div>
              <div class="form-group">
                <label class="form-label">Mensaje</label>
                <textarea v-model="form.message" rows="4" class="form-textarea" required></textarea>
              </div>
              <button type="submit" class="btn btn-primary form-submit">
                Enviar Mensaje
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <div class="footer-logo">
              <div class="footer-logo-icon">🍔</div>
              <h3 class="footer-logo-text">Burger Palace</h3>
            </div>
            <p class="footer-description">
              Las mejores hamburguesas de la ciudad, preparadas con amor y ingredientes frescos.
            </p>
          </div>

          <div class="footer-section">
            <h4 class="footer-title">Enlaces Rápidos</h4>
            <ul class="footer-links">
              <li><a href="#inicio" class="footer-link">Inicio</a></li>
              <li><a href="#menu" class="footer-link">Menú</a></li>
              <li><a href="#acerca" class="footer-link">Acerca de</a></li>
              <li><a href="#contacto" class="footer-link">Contacto</a></li>
            </ul>
          </div>

          <div class="footer-section">
            <h4 class="footer-title">Horarios</h4>
            <div class="footer-hours">
              <p>Lunes - Viernes: 11:00 AM - 11:00 PM</p>
              <p>Sábado - Domingo: 10:00 AM - 12:00 AM</p>
            </div>
          </div>

          <div class="footer-section">
            <h4 class="footer-title">Síguenos</h4>
            <div class="social-links">
              <a href="#" class="social-link" style="font-size: 25px; color: white;"><i
                  class="fa-brands fa-facebook"></i></a>
              <a href="#" class="social-link" style="font-size: 25px; color: white;"><i
                  class="fa-brands fa-instagram"></i></a>
              <a href="#" class="social-link" style="font-size: 25px; color: white;"><i
                  class="fa-brands fa-tiktok"></i></a>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <p>&copy; {{ anio }} Burger Palace. Todos los derechos reservados.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const anio = new Date().getFullYear()

// Estado reactivo
const scrolled = ref(false)
const mobileMenuOpen = ref(false)
const isVisible = ref({
  inicio: false,
  menu: false,
  acerca: false,
  contacto: false
})

const form = ref({
  name: '',
  email: '',
  message: ''
})

// Datos del menú de navegación
const menuItems = [
  { id: 'inicio', name: 'Inicio' },
  { id: 'menu', name: 'Menú' },
  { id: 'acerca', name: 'Acerca de' },
  { id: 'contacto', name: 'Contacto' }
]

// Datos de las hamburguesas
const burgers = [
  {
    id: 1,
    name: 'Classic Burger',
    description: 'Carne de res, lechuga, tomate, cebolla y nuestra salsa especial',
    price: 12.99,
    image: './classic-burger.png' // Ruta CORRECTA
  },
  {
    id: 2,
    name: 'Cheese Deluxe',
    description: 'Doble carne, queso cheddar, bacon crujiente y salsa BBQ',
    price: 15.99,
    image: './double-cheeseburger-pickles.png'
  },
  {
    id: 3,
    name: 'Veggie Supreme',
    description: 'Hamburguesa vegetal, aguacate, brotes y mayonesa de hierbas',
    price: 11.99,
    image: './veggie-burger.jpg'
  },
  {
    id: 4,
    name: 'Spicy Jalapeño',
    description: 'Carne picante, jalapeños, queso pepper jack y salsa chipotle',
    price: 14.99,
    image: './spicy-jalapeno-avocado-burger.png'
  },
  {
    id: 5,
    name: 'Mushroom Swiss',
    description: 'Carne de res, hongos salteados, queso suizo y cebolla caramelizada',
    price: 13.99,
    image: './mushroom-swiss-burger.png'
  },
  {
    id: 6,
    name: 'BBQ Ranch',
    description: 'Carne ahumada, aros de cebolla, queso cheddar y salsa ranch BBQ',
    price: 16.99,
    image: './bbq-bacon-burger.png'
  }
]

// Funciones
const handleScroll = () => {
  scrolled.value = window.scrollY > 50

  // Detectar visibilidad de secciones para animaciones
  const sections = ['inicio', 'menu', 'acerca', 'contacto']
  sections.forEach(section => {
    const element = document.getElementById(section)
    if (element) {
      const rect = element.getBoundingClientRect()
      const isInViewport = rect.top < window.innerHeight && rect.bottom > 0
      if (isInViewport && !isVisible.value[section]) {
        isVisible.value[section] = true
      }
    }
  })
}

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    const offsetTop = element.offsetTop - 80 // Ajuste para el header fijo
    window.scrollTo({
      top: offsetTop,
      behavior: 'smooth'
    })
  }
}

const submitForm = () => {
  // Aquí iría la lógica para enviar el formulario
  alert('¡Gracias por tu mensaje! Te contactaremos pronto.')
  form.value = { name: '', email: '', message: '' }
}

// Lifecycle hooks
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Activar animación inicial
  setTimeout(() => {
    isVisible.value.inicio = true
  }, 100)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
/* Layout principal */
.app {
  min-height: 100vh;
  background-color: var(--soft-cream);
}

/* Header */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: linear-gradient(135deg, var(--primary-red), #e53e3e);
  box-shadow: var(--shadow-lg);
  z-index: 50;
  transition: all var(--transition-smooth);
}

.header-scrolled {
  background: linear-gradient(135deg, #b91c1c, var(--primary-red));
}

.nav {
  padding: 1rem 0;
}

.nav-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.logo-icon {
  width: 2.5rem;
  height: 2.5rem;
  background-color: var(--primary-yellow);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.25rem;
}

.logo-text {
  color: var(--pure-white);
  font-family: var(--font-primary);
  font-weight: 700;
  font-size: 1.5rem;
  margin: 0;
}

.desktop-menu {
  display: none;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-link {
  color: var(--pure-white);
  text-decoration: none;
  font-weight: 500;
  cursor: pointer;
  transition: color var(--transition-smooth);
}

.nav-link:hover {
  color: var(--primary-yellow);
}

.mobile-menu-btn {
  display: block;
  background: none;
  border: none;
  color: var(--pure-white);
  cursor: pointer;
}

.menu-icon {
  width: 1.5rem;
  height: 1.5rem;
}

.mobile-menu {
  margin-top: 1rem;
  padding-bottom: 1rem;
}

.mobile-menu-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.mobile-menu-link {
  display: block;
  color: var(--pure-white);
  text-decoration: none;
  padding: 0.5rem 0;
  cursor: pointer;
  transition: color var(--transition-smooth);
}

.mobile-menu-link:hover {
  color: var(--primary-yellow);
}

/* Hero Section */
.hero-section {
  padding-top: 5rem;
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: linear-gradient(135deg, var(--primary-red), var(--accent-orange));
}

.hero-content {
  display: grid;
  gap: 3rem;
  align-items: center;
}

.hero-text {
  color: var(--pure-white);
}

.hero-title {
  font-family: var(--font-primary);
  font-size: 3rem;
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 1.5rem;
}

.hero-highlight {
  color: var(--primary-yellow);
}

.hero-description {
  font-size: 1.25rem;
  margin-bottom: 2rem;
  color: rgba(255, 255, 255, 0.9);
}

.hero-cta {
  background: linear-gradient(135deg, var(--primary-yellow), var(--accent-orange));
  color: var(--primary-red);
  font-weight: 700;
  font-size: 1.125rem;
  padding: 1rem 2rem;
  border-radius: 2rem;
}

.hero-image {
  position: relative;
}

.hero-img {
  width: 100%;
  max-width: 32rem;
  margin: 0 auto;
  border-radius: 0.5rem;
  box-shadow: var(--shadow-lg);
  transition: transform var(--transition-smooth);
}

.hero-img:hover {
  transform: scale(1.05);
}

.hero-badge {
  position: absolute;
  top: -1rem;
  right: -1rem;
  background-color: var(--primary-yellow);
  color: var(--primary-red);
  border-radius: 50%;
  width: 5rem;
  height: 5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1.125rem;
  box-shadow: var(--shadow-lg);
}

/* Menu Section */
.menu-section {
  padding: 5rem 0;
  background-color: var(--soft-cream);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-family: var(--font-primary);
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--primary-red);
  margin-bottom: 1rem;
}

.section-description {
  font-size: 1.25rem;
  color: var(--charcoal);
  max-width: 32rem;
  margin: 0 auto;
}

.menu-grid {
  display: grid;
  gap: 2rem;
}

.menu-card {
  background-color: var(--pure-white);
  border-radius: 0.75rem;
  box-shadow: var(--shadow-lg);
  overflow: hidden;
  transition: all var(--transition-smooth);
}

.menu-card:hover {
  transform: scale(1.05);
  box-shadow: var(--shadow-lg);
}

.menu-card-image {
  position: relative;
  overflow: hidden;
}

.card-img {
  width: 100%;
  height: 12rem;
  object-fit: cover;
  transition: transform var(--transition-smooth);
}

.menu-card:hover .card-img {
  transform: scale(1.1);
}

.price-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background-color: var(--primary-red);
  color: var(--pure-white);
  padding: 0.5rem 0.75rem;
  border-radius: 2rem;
  font-weight: 700;
}

.menu-card-content {
  padding: 1.5rem;
}

.card-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--primary-red);
  margin-bottom: 0.5rem;
}

.card-description {
  color: var(--charcoal);
  margin-bottom: 1rem;
}

.card-btn {
  width: 100%;
  padding: 0.75rem;
  border-radius: 0.5rem;
  font-weight: 700;
}

/* About Section */
.about-section {
  padding: 5rem 0;
  background-color: var(--primary-red);
  color: var(--pure-white);
}

.about-content {
  display: grid;
  gap: 3rem;
  align-items: center;
}

.about-img {
  width: 100%;
  border-radius: 0.5rem;
  box-shadow: var(--shadow-lg);
}

.about-title {
  font-family: var(--font-primary);
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--primary-yellow);
  margin-bottom: 1.5rem;
}

.about-description {
  font-size: 1.125rem;
  margin-bottom: 1.5rem;
  color: rgba(255, 255, 255, 0.9);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  text-align: center;
}

.stat-card {
  background-color: rgba(139, 69, 19, 0.3);
  padding: 1rem;
  border-radius: 0.5rem;
}

.stat-number {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-yellow);
}

.stat-label {
  font-size: 0.875rem;
}

/* Contact Section */
.contact-section {
  padding: 5rem 0;
  background-color: var(--soft-cream);
}

.contact-content {
  display: grid;
  gap: 3rem;
}

.contact-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-red);
  margin-bottom: 1.5rem;
}

.contact-items {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.contact-icon {
  width: 3rem;
  height: 3rem;
  background-color: var(--primary-red);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.25rem;
}

.contact-label {
  font-weight: 700;
  color: var(--charcoal);
  margin: 0 0 0.25rem 0;
}

.contact-value {
  color: var(--charcoal);
  margin: 0;
}

.contact-form-wrapper {
  background-color: var(--pure-white);
  padding: 2rem;
  border-radius: 0.75rem;
  box-shadow: var(--shadow-lg);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-label {
  color: var(--charcoal);
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.form-input,
.form-textarea {
  padding: 0.75rem 1rem;
  border: 2px solid #e2e8f0;
  border-radius: 0.5rem;
  font-family: var(--font-secondary);
  transition: border-color var(--transition-smooth);
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--primary-red);
}

.form-submit {
  width: 100%;
  padding: 0.75rem;
  border-radius: 0.5rem;
  font-weight: 700;
}

/* Footer */
.footer {
  background-color: #991b1b;
  color: var(--pure-white);
  padding: 3rem 0;
}

.footer-content {
  display: grid;
  gap: 2rem;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.footer-logo-icon {
  width: 2rem;
  height: 2rem;
  background-color: var(--primary-yellow);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.footer-logo-text {
  font-size: 1.25rem;
  font-weight: 700;
  margin: 0;
}

.footer-description {
  color: rgba(255, 255, 255, 0.8);
}

.footer-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: var(--primary-yellow);
  margin-bottom: 1rem;
}

.footer-links {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer-link {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  transition: color var(--transition-smooth);
}

.footer-link:hover {
  color: var(--pure-white);
}

.footer-hours {
  color: rgba(255, 255, 255, 0.8);
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  width: 2.5rem;
  height: 2.5rem;
  background-color: rgba(139, 69, 19, 0.3);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  transition: background-color var(--transition-smooth);
}

.social-link:hover {
  background-color: rgba(139, 69, 19, 0.5);
}

.footer-bottom {
  border-top: 1px solid rgba(139, 69, 19, 0.3);
  margin-top: 2rem;
  padding-top: 2rem;
  text-align: center;
  color: rgba(255, 255, 255, 0.8);
}

/* Responsive Design */
@media (min-width: 768px) {
  .desktop-menu {
    display: flex;
  }

  .mobile-menu-btn {
    display: none;
  }

  .hero-content {
    grid-template-columns: 1fr 1fr;
  }

  .hero-title {
    font-size: 4rem;
  }

  .section-title {
    font-size: 3rem;
  }

  .menu-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .about-content {
    grid-template-columns: 1fr 1fr;
  }

  .contact-content {
    grid-template-columns: 1fr 1fr;
  }

  .footer-content {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (min-width: 1024px) {
  .hero-title {
    font-size: 4.5rem;
  }

  .menu-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
