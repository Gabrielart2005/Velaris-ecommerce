<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue';
import { gsap } from 'gsap';

// Componentes
import Bestsellers from '../components/Home/Bestsellers.vue';
import Coleccion from '../components/Home/Coleccion.vue';
import Category from '../components/Home/Category.vue';

// Imágenes (usando imports directos de Vite)
import img1 from '../assets/Img_1.png';
import img2 from '../assets/Img_2.png';
import img3 from '../assets/Img_3.png';

// Datos de las slides
const slides = [
  { text: 'UN ESTILO QUE\n TRANSCIENDE EN EL TIEMPO', img: img1 },
  { text: 'PEQUEÑOS LUJOS\n PARA GRANDES INSTANTES', img: img2 },
  { text: 'VISTE LA ESENCIA VELARIS', img: img3 }
];

// Referencias DOM
const heroRef = ref(null);
const containerRef = ref(null);

// Variables para control
let autoPlayInterval = null;
const SLIDE_COUNT = slides.length;
const currentIndex = ref(0);

// Obtener ancho actual del viewport
const getSlideWidth = () => window.innerWidth;

// Función para cambiar a un slide específico
const goToSlide = (index) => {
  // Asegurar índice dentro de rango [0, SLIDE_COUNT-1]
  const safeIndex = ((index % SLIDE_COUNT) + SLIDE_COUNT) % SLIDE_COUNT;
  currentIndex.value = safeIndex;
  
  // Animar el contenedor - cada slide es 100vw
  const slideWidth = getSlideWidth();
  gsap.to(containerRef.value, {
    x: -safeIndex * slideWidth,
    duration: 1,
    ease: 'power3.inOut'
  });
};

// Función para avanzar al siguiente slide
const nextSlide = () => {
  goToSlide(currentIndex.value + 1);
};

// Reiniciar posición del slider al redimensionar
const handleResize = () => {
  if (containerRef.value) {
    gsap.set(containerRef.value, { x: -currentIndex.value * getSlideWidth() });
  }
};

// Iniciar reproducción automática
const startAutoPlay = () => {
  autoPlayInterval = setInterval(nextSlide, 4000); // Cambiar cada 4 segundos (3 seg pausa + 1 seg animación)
};

// Detener reproducción automática
const stopAutoPlay = () => {
  if (autoPlayInterval) {
    clearInterval(autoPlayInterval);
    autoPlayInterval = null;
  }
};

onMounted(async () => {
  await nextTick(); // Asegurar que el DOM esté renderizado
  if (containerRef.value) {
    // Iniciar en el primer slide
    goToSlide(0);
    // Iniciar auto-play
    startAutoPlay();
    // Escuchar redimensionamiento
    window.addEventListener('resize', handleResize);
  }
});

onUnmounted(() => {
  // Limpiar intervalo al destruir el componente
  stopAutoPlay();
  window.removeEventListener('resize', handleResize);
});
</script>

<template>
  <!-- Contenedor del Hero Horizontal (Versión Prueba) -->
  <div id="hero-horizontal" ref="heroRef">
    
    <!-- Contenedor deslizante (300% ancho) -->
    <div class="slide-container" ref="containerRef">
      
      <!-- Slide Individual -->
      <div 
        v-for="(slide, index) in slides" 
        :key="index" 
        class="slide"
      >
        <div class="outer">
          <div class="inner">
            <div class="bg" :style="{ backgroundImage: `url(${slide.img})` }">
              
              <!-- Capa de color/opacidad opcional para legibilidad -->
              <div class="overlay"></div>

              <h2 class="section-heading">{{ slide.text }}</h2>
              
              <!-- Botones -->
              <div class="btn-container">
                <button class="btn">VER COLECCIÓN</button>
                <button class="btn secondary">COMPRAR AHORA</button>
              </div>

            </div>
          </div>
        </div>
      </div>

    </div> <!-- Fin slide-container -->

    <!-- Indicador visual de progreso -->
    <div class="progress-indicator">
      <div 
        v-for="(_, i) in slides" 
        :key="i" 
        class="dot"
        :class="{ active: i === currentIndex }"
      ></div>
    </div>

  </div> <!-- Fin hero-horizontal -->

  <!-- Contenido posterior: Componentes originales -->
  <Bestsellers />
  <Coleccion />
  <Category />
</template>

<style scoped>
#hero-horizontal {
  position: relative;
  width: 100%;
  height: 70vh; /* Altura ajustada para estar justo debajo del navbar */
  overflow: hidden;
  margin-top: 60px; /* Margen superior para evitar solapamiento con el navbar fijo */
  margin-bottom: 20px; /* Espacio hacia el contenido siguiente */
}

.slide-container {
  display: flex;
  width: 300%; /* 3 slides x 100% cada una */
  height: 100%;
  will-change: transform; /* Optimización de rendimiento */
}

.slide {
  width: 100vw; /* Cada slide ocupa 100% del viewport width */
  height: 100%;
  position: relative;
  flex-shrink: 0; /* Evita que se compriman */
}

.outer, .inner {
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
}

.bg {
  position: absolute;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  filter: brightness(0.8) contrast(1.1);
  transform-origin: center center;
  background-color: #333; /* Fallback si la imagen no carga */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(180deg, rgba(0,0,0,0.2) 0%, rgba(0,0,0,0.5) 100%);
  z-index: 1;
}

.section-heading {
  color: #fafafa;
  font-family: "Cormorant Garamond", serif;
  font-size: clamp(1.5rem, 5vw, 4.5rem);
  font-weight: 300;
  text-align: center;
  letter-spacing: 0.1em;
  font-style: italic;
  text-transform: uppercase;
  text-shadow: 0 2px 10px rgba(0,0,0,0.5);
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90%;
  max-width: 800px;
  z-index: 2;
  margin: 0;
  line-height: 1;
}

.btn-container {
  position: absolute;
  top: 60%;
  left: 50%;
  transform: translate(-50%, 0);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
  z-index: 2;
}

@media (min-width: 768px) {
  .btn-container {
    flex-direction: row;
    gap: 20px;
  }
}

.btn {
  padding: 12px 28px;
  background-color: transparent;
  border: 1px solid rgba(255,255,255,0.5);
  color: #fff;
  font-family: "Helvetica Neue", sans-serif;
  font-size: 0.7rem;
  letter-spacing: 2px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  text-transform: uppercase;
  width: 100%;
  max-width: 200px;
}

@media (min-width: 768px) {
  .btn {
    width: auto;
    padding: 14px 32px;
    font-size: 0.75rem;
  }
}

.btn:hover {
  background-color: #fff;
  color: #000;
  border-color: #fff;
}

.btn.secondary {
  background-color: rgba(255,255,255,0.1);
}

/* Indicador de progreso (dots) */
.progress-indicator {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
  z-index: 10;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255,255,255,0.3);
  transition: background 0.3s;
}

.dot.active {
  background: #fff;
}
</style>
