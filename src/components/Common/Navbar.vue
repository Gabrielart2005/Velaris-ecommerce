<script setup>
import { ref, nextTick } from 'vue'

const cartCount = ref(0)
const isSearchOpen = ref(false)
const searchInput = ref(null)
const isMobileMenuOpen = ref(false)

const searchQuery = ref('')
let timer = null

const toggleSearch = async () => {
  isSearchOpen.value = !isSearchOpen.value 
  
  if (isSearchOpen.value) {
    await nextTick()
    searchInput.value?.focus()
    iniciarTemporizador()
  } else {
    searchQuery.value = ''
  }
}

const iniciarTemporizador = () => {
  clearTimeout(timer)
  timer = setTimeout(() => {
    if (searchQuery.value === '') {
      isSearchOpen.value = false
    }
  }, 4000)
}

const detenerReloj = () => {
  clearTimeout(timer)
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}
</script>

<template>
  <header class="navbar">
    <nav class="nav-left">
      <button class="mobile-menu-btn" @click="toggleMobileMenu" aria-label="Menú">
        <span :class="{ 'open': isMobileMenuOpen }"></span>
      </button>
      
      <ul class="nav-links" :class="{ 'is-open': isMobileMenuOpen }">
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#tienda">Tienda</a></li>
        <li><a href="#coleccion">Colección</a></li>
        <li><a href="#compania">Compañía</a></li>
      </ul>
    </nav>

    <div class="nav-center">
      <a href="/" class="logo">VELARIS</a>
    </div>

    <div class="nav-right">
      <div class="search-wrapper">
        <input 
          type="text" 
          placeholder="BUSCAR" 
          class="search-input"
          :class="{ 'is-open': isSearchOpen }"
          ref="searchInput"
          maxlength="20"
          v-model="searchQuery"
          @input="detenerReloj"
        >
        <button class="search-btn" @click="toggleSearch" aria-label="Buscar">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <circle cx="11" cy="11" r="8"/>
            <path d="m21 21-4.35-4.35"/>
          </svg>
        </button>
      </div>
      
      <div class="nav-icons">
        <a href="#" class="icon-link" aria-label="Mi cuenta">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>
            <circle cx="12" cy="7" r="4"/>
          </svg>
        </a>
        
        <a href="#" class="icon-link cart-link" aria-label="Carrito">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/>
            <path d="M3 6h18"/>
            <path d="M16 10a4 4 0 0 1-8 0"/>
          </svg>
          <span class="cart-count" v-if="cartCount > 0">{{ cartCount }}</span>
        </a>
      </div>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 0 5%;
  box-sizing: border-box;
  background: #fff;
  border-bottom: 1px solid #f0f0f0;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;  
  z-index: 1000;
  height: 70px;
}

/* Logo */
.nav-center { justify-self: center; }
.logo {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.8rem;
  font-weight: 400;
  color: #1a1a1a;
  text-decoration: none;
  letter-spacing: 0.35em;
}

/* Nav Links - Left */
.nav-left { 
  justify-self: start;
  display: flex;
  align-items: center;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 2.5rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links a {
  text-decoration: none;
  color: #303030;
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  position: relative;
  transition: color 0.3s ease;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 1px;
  background: #1a1a1a;
  transition: width 0.3s ease;
}

.nav-links a:hover {
  color: #1a1a1a;
}

.nav-links a:hover::after {
  width: 100%;
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  width: 24px;
  height: 18px;
  background: none;
  border: none;
  cursor: pointer;
  position: relative;
  margin-right: 20px;
}

.mobile-menu-btn span,
.mobile-menu-btn span::before,
.mobile-menu-btn span::after {
  display: block;
  width: 100%;
  height: 1.5px;
  background: #1a1a1a;
  position: absolute;
  left: 0;
  transition: all 0.3s ease;
}

.mobile-menu-btn span {
  top: 50%;
  transform: translateY(-50%);
}

.mobile-menu-btn span::before {
  content: '';
  top: -7px;
}

.mobile-menu-btn span::after {
  content: '';
  top: 7px;
}

.mobile-menu-btn span.open {
  background: transparent;
}

.mobile-menu-btn span.open::before {
  top: 0;
  transform: rotate(45deg);
}

.mobile-menu-btn span.open::after {
  top: 0;
  transform: rotate(-45deg);
}

/* Right Nav */
.nav-right {
  justify-self: end;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

/* Search */
.search-wrapper {
  display: flex;
  align-items: center;
}

.search-input {
  width: 0;
  opacity: 0;
  border: none;
  border-bottom: 1px solid #ccc;
  outline: none;
  background: transparent;
  padding: 6px 0;
  font-size: 0.65rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #1a1a1a;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.search-input.is-open {
  width: 120px;
  opacity: 1;
}

.search-input::placeholder { color: #999; }

.search-btn {
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  color: #444;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: color 0.3s ease;
}

.search-btn:hover {
  color: #1a1a1a;
}

/* Icons */
.nav-icons {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.icon-link {
  color: #444;
  display: flex;
  align-items: center;
  transition: color 0.3s ease;
}

.icon-link:hover {
  color: #1a1a1a;
}

.cart-link {
  position: relative;
}

.cart-count {
  position: absolute;
  top: -6px;
  right: -8px;
  font-size: 0.55rem;
  background: #1a1a1a;
  color: #fff;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Responsive */
@media (max-width: 900px) {
  .mobile-menu-btn {
    display: block;
  }
  
  .nav-links {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: #fff;
    flex-direction: column;
    gap: 0;
    padding: 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    border-bottom: 1px solid #f0f0f0;
  }
  
  .nav-links.is-open {
    max-height: 300px;
    padding: 20px 0;
  }
  
  .nav-links li {
    width: 100%;
    text-align: center;
  }
  
  .nav-links a {
    display: block;
    padding: 12px;
  }
  
  .logo {
    font-size: 1.5rem;
    letter-spacing: 0.25em;
  }
}
</style>