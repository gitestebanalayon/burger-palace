<template>
  <div id="app" class="min-h-screen bg-background">
    <!-- Header -->
    <header 
      :class="[
        'fixed top-0 left-0 right-0 z-50 transition-all duration-300',
        isScrolled ? 'bg-background/95 backdrop-blur-sm shadow-lg' : 'bg-transparent'
      ]"
    >
      <nav class="container mx-auto px-4 py-4">
        <div class="flex items-center justify-between">
          <!-- Logo -->
          <div class="flex items-center space-x-2">
            <div class="w-10 h-10 bg-primary rounded-full flex items-center justify-center">
              <span class="text-primary-foreground font-bold text-xl">🍔</span>
            </div>
            <h1 class="text-2xl font-bold text-primary font-sans">Burger Palace</h1>
          </div>

          <!-- Desktop Navigation -->
          <ul class="hidden md:flex space-x-8">
            <li v-for="item in navItems" :key="item.id">
              <a 
                :href="`#${item.id}`"
                @click="scrollToSection(item.id)"
                class="text-foreground hover:text-primary transition-colors duration-300 font-medium"
              >
                {{ item.name }}
              </a>
            </li>
          </ul>

          <!-- Mobile Menu Button -->
          <button 
            @click="toggleMobileMenu"
            class="md:hidden p-2 text-foreground hover:text-primary transition-colors"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>

        <!-- Mobile Menu -->
        <div v-if="mobileMenuOpen" class="md:hidden mt-4 pb-4">
          <ul class="space-y-2">
            <li v-for="item in navItems" :key="item.id">
              <a 
                :href="`#${item.id}`"
                @click="scrollToSection(item.id); toggleMobileMenu()"
                class="block py-2 text-foreground hover:text-primary transition-colors duration-300"
              >
                {{ item.name }}
              </a>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="inicio" class="relative min-h-screen flex items-center justify-center overflow-hidden">
      <div 
        class="absolute inset-0 bg-gradient-to-br from-primary/20 to-accent/20"
        style="background-image: url('/placeholder.svg?height=800&width=1200'); background-size: cover; background-position: center;"
      ></div>
      <div class="absolute inset-0 bg-black/40"></div>
      
      <div class="relative z-10 text-center text-white px-4 max-w-4xl mx-auto">
        <h2 
          class="text-5xl md:text-7xl font-bold mb-6 animate-fade-in-up font-sans"
          :class="{ 'animate-fade-in-up': isVisible.hero }"
        >
          Las Mejores<br>
          <span class="text-accent">Hamburguesas</span>
        </h2>
        <p 
          class="text-xl md:text-2xl mb-8 animate-fade-in-up font-serif"
          style="animation-delay: 0.2s"
        >
          Ingredientes frescos, sabores únicos y la mejor experiencia gastronómica
        </p>
        <button 
          @click="scrollToSection('menu')"
          class="bg-primary hover:bg-primary/90 text-primary-foreground px-8 py-4 rounded-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 animate-bounce-gentle"
        >
          Ver Nuestro Menú
        </button>
      </div>
    </section>

    <!-- Menu Section -->
    <section id="menu" class="py-20 bg-muted">
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-foreground mb-4 font-sans">Nuestro Menú</h2>
          <p class="text-xl text-muted-foreground max-w-2xl mx-auto font-serif">
            Descubre nuestras hamburguesas artesanales, preparadas con los mejores ingredientes
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="(burger, index) in burgers" 
            :key="index"
            class="bg-card rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-all duration-300 transform hover:-translate-y-2"
            :class="{ 'animate-fade-in-up': isVisible.menu }"
            :style="{ 'animation-delay': `${index * 0.1}s` }"
          >
            <div class="relative h-64 overflow-hidden">
              <img 
                :src="burger.image" 
                :alt="burger.name"
                class="w-full h-full object-cover transition-transform duration-300 hover:scale-110"
              >
              <div class="absolute top-4 right-4 bg-primary text-primary-foreground px-3 py-1 rounded-full font-bold">
                ${{ burger.price }}
              </div>
            </div>
            <div class="p-6">
              <h3 class="text-2xl font-bold text-card-foreground mb-2 font-sans">{{ burger.name }}</h3>
              <p class="text-foreground mb-4 font-serif">{{ burger.description }}</p>
              <button class="w-full bg-secondary hover:bg-secondary/90 text-secondary-foreground py-3 rounded-lg font-semibold transition-colors duration-300">
                Ordenar Ahora
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="acerca" class="py-20 bg-background">
      <div class="container mx-auto px-4">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <div 
            class="space-y-6"
            :class="{ 'animate-slide-in-left': isVisible.about }"
          >
            <h2 class="text-4xl md:text-5xl font-bold text-foreground font-sans">Nuestra Historia</h2>
            <p class="text-lg text-muted-foreground font-serif">
              Desde 2010, Burger Palace ha sido el hogar de las hamburguesas más deliciosas de la ciudad. 
              Comenzamos como un pequeño local familiar con una gran pasión por la comida de calidad.
            </p>
            <p class="text-lg text-muted-foreground font-serif">
              Utilizamos solo ingredientes frescos y locales, carne 100% premium y nuestras recetas secretas 
              que han sido perfeccionadas a lo largo de los años. Cada hamburguesa es una obra de arte culinaria.
            </p>
            
            <div class="grid grid-cols-3 gap-4 pt-8">
              <div class="text-center">
                <div class="text-3xl font-bold text-primary font-sans">15+</div>
                <div class="text-sm text-muted-foreground">Años de experiencia</div>
              </div>
              <div class="text-center">
                <div class="text-3xl font-bold text-primary font-sans">50k+</div>
                <div class="text-sm text-muted-foreground">Clientes felices</div>
              </div>
              <div class="text-center">
                <div class="text-3xl font-bold text-primary font-sans">20+</div>
                <div class="text-sm text-muted-foreground">Variedades únicas</div>
              </div>
            </div>
          </div>
          
          <div class="relative">
            <img 
              src="/placeholder.svg?height=500&width=600"
              alt="Chef preparando hamburguesa"
              class="rounded-xl shadow-lg w-full"
            >
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contacto" class="py-20 bg-muted">
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-foreground mb-4 font-sans">Contáctanos</h2>
          <p class="text-xl text-muted-foreground max-w-2xl mx-auto font-serif">
            ¿Tienes alguna pregunta? ¡Nos encantaría escucharte!
          </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
          <!-- Contact Form -->
          <div 
            class="bg-card p-8 rounded-xl shadow-lg"
            :class="{ 'animate-fade-in-up': isVisible.contact }"
          >
            <form @submit.prevent="submitForm" class="space-y-6">
              <div>
                <label class="block text-card-foreground font-semibold mb-2">Nombre</label>
                <input 
                  v-model="form.name"
                  type="text" 
                  required
                  class="w-full px-4 py-3 bg-input border border-border rounded-lg focus:ring-2 focus:ring-ring focus:border-transparent transition-all duration-300"
                  placeholder="Tu nombre completo"
                >
              </div>
              <div>
                <label class="block text-card-foreground font-semibold mb-2">Email</label>
                <input 
                  v-model="form.email"
                  type="email" 
                  required
                  class="w-full px-4 py-3 bg-input border border-border rounded-lg focus:ring-2 focus:ring-ring focus:border-transparent transition-all duration-300"
                  placeholder="tu@email.com"
                >
              </div>
              <div>
                <label class="block text-card-foreground font-semibold mb-2">Mensaje</label>
                <textarea 
                  v-model="form.message"
                  required
                  rows="4"
                  class="w-full px-4 py-3 bg-input border border-border rounded-lg focus:ring-2 focus:ring-ring focus:border-transparent transition-all duration-300 resize-none"
                  placeholder="Cuéntanos cómo podemos ayudarte..."
                ></textarea>
              </div>
              <button 
                type="submit"
                class="w-full bg-primary hover:bg-primary/90 text-primary-foreground py-3 rounded-lg font-semibold transition-colors duration-300"
              >
                Enviar Mensaje
              </button>
            </form>
          </div>

          <!-- Contact Info -->
          <div class="space-y-8">
            <div 
              v-for="(info, index) in contactInfo" 
              :key="index"
              class="flex items-start space-x-4 p-6 bg-background rounded-xl shadow-lg"
              :class="{ 'animate-slide-in-left': isVisible.contact }"
              :style="{ 'animation-delay': `${index * 0.1}s` }"
            >
              <div class="w-12 h-12 bg-primary rounded-full flex items-center justify-center flex-shrink-0">
                <span class="text-primary-foreground text-xl">{{ info.icon }}</span>
              </div>
              <div>
                <h3 class="text-xl font-bold text-foreground mb-2 font-sans">{{ info.title }}</h3>
                <p class="text-muted-foreground font-serif">{{ info.content }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-foreground text-background py-12">
      <div class="container mx-auto px-4">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
          <div class="col-span-1 md:col-span-2">
            <div class="flex items-center space-x-2 mb-4">
              <div class="w-10 h-10 bg-primary rounded-full flex items-center justify-center">
                <span class="text-primary-foreground font-bold text-xl">🍔</span>
              </div>
              <h3 class="text-2xl font-bold text-primary font-sans">Burger Palace</h3>
            </div>
            <p class="text-background/80 mb-4 font-serif">
              Las mejores hamburguesas de la ciudad, preparadas con amor y los ingredientes más frescos.
            </p>
            <div class="flex space-x-4">
              <a href="#" class="text-background/60 hover:text-primary transition-colors duration-300">
                <span class="text-2xl">📘</span>
              </a>
              <a href="#" class="text-background/60 hover:text-primary transition-colors duration-300">
                <span class="text-2xl">📷</span>
              </a>
              <a href="#" class="text-background/60 hover:text-primary transition-colors duration-300">
                <span class="text-2xl">🐦</span>
              </a>
            </div>
          </div>
          
          <div>
            <h4 class="text-lg font-bold mb-4 text-accent font-sans">Enlaces Rápidos</h4>
            <ul class="space-y-2">
              <li v-for="item in navItems" :key="item.id">
                <a 
                  :href="`#${item.id}`"
                  @click="scrollToSection(item.id)"
                  class="text-background/80 hover:text-primary transition-colors duration-300 font-serif"
                >
                  {{ item.name }}
                </a>
              </li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-lg font-bold mb-4 text-accent font-sans">Horarios</h4>
            <div class="space-y-2 text-background/80 font-serif">
              <p>Lun - Jue: 11:00 - 22:00</p>
              <p>Vie - Sáb: 11:00 - 23:00</p>
              <p>Domingo: 12:00 - 21:00</p>
            </div>
          </div>
        </div>
        
        <div class="border-t border-background/20 mt-8 pt-8 text-center">
          <p class="text-background/60 font-serif">
            © 2024 Burger Palace. Todos los derechos reservados.
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Reactive data
const isScrolled = ref(false)
const mobileMenuOpen = ref(false)
const isVisible = ref({
  hero: false,
  menu: false,
  about: false,
  contact: false
})

const form = ref({
  name: '',
  email: '',
  message: ''
})

// Navigation items
const navItems = [
  { id: 'inicio', name: 'Inicio' },
  { id: 'menu', name: 'Menú' },
  { id: 'acerca', name: 'Acerca de' },
  { id: 'contacto', name: 'Contacto' }
]

// Burger menu data
const burgers = [
  {
    name: 'Classic Burger',
    description: 'Carne de res premium, lechuga, tomate, cebolla y nuestra salsa especial',
    price: '12.99',
    image: '/placeholder.svg?height=300&width=400'
  },
  {
    name: 'BBQ Bacon',
    description: 'Carne de res, bacon crujiente, salsa BBQ, cebolla caramelizada y queso cheddar',
    price: '15.99',
    image: '/placeholder.svg?height=300&width=400'
  },
  {
    name: 'Mushroom Swiss',
    description: 'Carne de res, champiñones salteados, queso suizo y salsa de ajo',
    price: '14.99',
    image: '/placeholder.svg?height=300&width=400'
  },
  {
    name: 'Spicy Jalapeño',
    description: 'Carne de res, jalapeños, queso pepper jack, salsa picante y aguacate',
    price: '13.99',
    image: '/placeholder.svg?height=300&width=400'
  },
  {
    name: 'Veggie Delight',
    description: 'Hamburguesa vegetal, lechuga, tomate, aguacate y salsa tahini',
    price: '11.99',
    image: '/placeholder.svg?height=300&width=400'
  },
  {
    name: 'Double Cheese',
    description: 'Doble carne, doble queso cheddar, pickles y salsa especial',
    price: '17.99',
    image: '/placeholder.svg?height=300&width=400'
  }
]

// Contact information
const contactInfo = [
  {
    icon: '📍',
    title: 'Ubicación',
    content: 'Av. Principal 123, Centro de la Ciudad'
  },
  {
    icon: '📞',
    title: 'Teléfono',
    content: '+1 (555) 123-4567'
  },
  {
    icon: '✉️',
    title: 'Email',
    content: 'info@burgerpalace.com'
  }
]

// Methods
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  
  // Check visibility of sections for animations
  const sections = ['hero', 'menu', 'about', 'contact']
  sections.forEach(section => {
    const element = document.getElementById(section === 'hero' ? 'inicio' : section)
    if (element) {
      const rect = element.getBoundingClientRect()
      const isInView = rect.top < window.innerHeight * 0.8 && rect.bottom > 0
      isVisible.value[section] = isInView
    }
  })
}

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    const headerHeight = 80
    const elementPosition = element.offsetTop - headerHeight
    
    window.scrollTo({
      top: elementPosition,
      behavior: 'smooth'
    })
  }
}

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const submitForm = () => {
  // Handle form submission
  console.log('Form submitted:', form.value)
  alert('¡Gracias por tu mensaje! Te contactaremos pronto.')
  
  // Reset form
  form.value = {
    name: '',
    email: '',
    message: ''
  }
}

// Lifecycle hooks
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll() // Initial check
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
/* Additional custom styles if needed */
.container {
  max-width: 1200px;
}

/* Smooth scrolling for the entire page */
html {
  scroll-behavior: smooth;
}

/* Custom hover effects */
.hover\:scale-105:hover {
  transform: scale(1.05);
}

/* Ensure images are properly sized */
img {
  max-width: 100%;
  height: auto;
}
</style>
