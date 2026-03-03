<script setup>
import { ref, nextTick } from 'vue'

const cartCount = ref(0)
const isSearchOpen = ref(false)
const searchInput = ref(null)

const searchQuery = ref('') // Para saber si el usuario escribió algo
let timer = null // Para guardar el reloj

const toggleSearch = async () => {
  isSearchOpen.value = !isSearchOpen.value 
  
  if (isSearchOpen.value) {
    await nextTick()
    searchInput.value.focus()
    
    // --- NUEVO: Iniciar cuenta atrás de 4 segundos al abrir ---
    iniciarTemporizador()
  } else {
    // Si lo cerramos manualmente, limpiamos el texto
    searchQuery.value = ''
  }
}

// --- NUEVAS FUNCIONES ---
const iniciarTemporizador = () => {
  clearTimeout(timer)
  timer = setTimeout(() => {
    // Si pasan 4 seg y no hay texto, se cierra
    if (searchQuery.value === '') {
      isSearchOpen.value = false
    }
  }, 4000)
}

const detenerReloj = () => {
  // Si el usuario escribe, el reloj se detiene y no se cierra solo
  clearTimeout(timer)
}
</script>

<template>
  <header class="navbar">
    
    <nav class="nav-left">
      <ul class="nav-links">
        <li><a href="#inicio">INICIO</a></li>
        <li><a href="#tienda">TIENDA</a></li>
        <li><a href="#coleccion">COLECCIÓN</a></li>
        <li><a href="#compania">COMPANÍA</a></li>
      </ul>
    </nav>

    <div class="nav-center">
      <span class="logo">VELARIS</span>
    </div>

    <div class="nav-right">
      
      <div class="search-wrapper">
        <input 
          type="text" 
          placeholder="BUSCAR..." 
          class="search-input"
          :class="{ 'is-open': isSearchOpen }"
          ref="searchInput"
          maxlength="20"
          v-model="searchQuery"
          @input="detenerReloj"
        >
        <img src="../assets/lupa.png" alt="Search" class="custom-icon" @click="toggleSearch">
      </div>
      
      <div class="nav-icons">
        <img src="../assets/usuario.png" alt="User" class="custom-icon">
        
        <div class="cart-container">
          <img src="../assets/bolsa-de-la-compra.png" alt="Cart" class="custom-icon">
          <span class="cart-count" v-if="cartCount > 0">({{ cartCount }})</span>
        </div>
      </div>

    </div>

  </header>
</template>

<style scoped>

.navbar {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 0.5rem 4%;
  box-sizing: border-box;
  background-color: #ffffff;
  border-bottom: 1px solid #eaeaea;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;  
  z-index: 1000;
}

.nav-left { justify-self: start; }
.nav-links {
  display: flex;
  align-items: center;
  gap: 2rem;
  list-style: none;
  margin: 0;
  padding: 0;
}
.nav-links a {
  text-decoration: none;
  color: #333;
  font-size: 0.70rem;
  letter-spacing: 1.5px;
  transition: color 0.3s ease;
}
.nav-links a:hover { color: #7a7979; }

.nav-center { justify-self: center; }
.logo {
  font-family: 'The Seasons', serif;
  font-size: 2rem;
  color: #000;
  text-decoration: none;
  letter-spacing: 3px;
  line-height: 1;
}

.nav-right {
  justify-self: end;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

/* ==========================================
    NUEVOS ESTILOS PARA LA BÚSQUEDA ANIMADA
   ========================================== */
.search-wrapper {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.search-input {
  width: 0; /* Empieza con ancho cero (oculto) */
  opacity: 0; /* Totalmente transparente */
  border: none;
  border-bottom: 1px solid #000;
  outline: none;
  background: transparent;
  padding: 0.3rem 0;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #000;
  transition: all 0.4s ease; /* Esta línea hace que la animación sea suave */
  pointer-events: none; /* Evita que se le pueda hacer clic cuando está invisible */
}

/* Esta clase se activa mágicamente con Vue cuando haces clic */
.search-input.is-open {
  width: 130px; /* La línea se estira hasta este tamaño */
  opacity: 1; /* Se hace visible */
  pointer-events: auto;
}

.search-input::placeholder { color: #aaa; }


.nav-icons {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.custom-icon {
  width: 18px;
  height: 18px;
  cursor: pointer;
  display: flex;
}

.cart-container {
  display: flex;
  align-items: center;
  gap: 0.3rem;
}
.cart-count {
  font-size: 0.8rem;
  color: #333;
}
</style>