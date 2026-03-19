<script setup>
import { ref, onMounted } from 'vue'

import imgBelt from '../../assets/Item-belt.jpeg'
import imgCorset from '../../assets/Item-corset.jpeg'
import imgBag from '../../assets/Item-bag.jpeg'
import imgSkirt from '../../assets/Item-skirt.jpeg'
import imgHeels from '../../assets/Item-heels.jpeg'
import imgDress from '../../assets/Item-dress.jpg'
import imgGlasses from '../../assets/Item-glasses.jpeg'
import imgFlats from '../../assets/Item-flats.jpeg'

const products = [
    {
        id: 1,
        name: 'ELEGANTE CINTURÓN ANCHO',
        price: '$10',
        image: imgBelt
    },
    {
        id: 2,
        name: 'CORSET BLANCO CON ENCAJES',
        price: '$24',
        image: imgCorset
    },
    {
        id: 3,
        name: 'CARTERA BLANCA DE LAZO MINI',
        price: '$14',
        image: imgBag
    },
    {
        id: 4,
        name: 'FALDA MARRON PLIZADA CON DISEÑO DE CINTURÓN',
        price: '$18',
        image: imgSkirt
    },
    {
        id: 5,
        name: 'BOTAS ALTAS DE TACÓN DE AGUJA',
        price: '$25',
        image: imgHeels
    },
    {
        id: 6,
        name: 'VESTIDO ELEGANTE CON CINTURA ANUDADA',
        price: '$30',
        image: imgDress
    },
    {
        id: 7,
        name: 'LENTES DE ACETATO CON ESTAMPADO',
        price: '$12',
        image: imgGlasses
    },
    {
        id: 8,
        name: 'ZAPATOS DE TACÓN BAJO BURDEOS',
        price: '$26',
        image: imgFlats
    }
]

const slider = ref(null)

const scrollLeft = () => {
    slider.value.scrollBy({ left: -280, behavior: 'smooth' })
}

const scrollRight = () => {
    slider.value.scrollBy({ left: 280, behavior: 'smooth' })
}
</script>

<template>
    <section class="bestsellers">
       <div class="section-header">
            <div class="header-spacer"></div>
            <h2>BESTSELLERS</h2>
            <div class="header-actions">
                <button class="btn-text">Ver todo</button>
            </div>
       </div>

       <div class="slider-wrapper">
            <button class="arrow arrow-left" @click="scrollLeft" aria-label="Anterior">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                    <path d="M15 18l-6-6 6-6"/>
                </svg>
            </button>

            <div class="products-slider" ref="slider">
                <div v-for="product in products" :key="product.id" class="product-card">
                    <div class="image-container">
                        <img :src="product.image" :alt="product.name">
                    </div>

                    <div class="product-info">
                        <h3>{{ product.name }}</h3>
                        <span class="price">{{ product.price }}</span>
                    </div>
                </div>
            </div>

            <button class="arrow arrow-right" @click="scrollRight" aria-label="Siguiente">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                    <path d="M9 18l6-6-6-6"/>
                </svg>
            </button>
       </div>
    </section>
</template>

<style scoped>
.bestsellers {
    padding: 0 5% 60px;
    text-align: center;
    max-width: 1400px;
    margin: 0 auto;
}

.section-header {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    margin-bottom: 40px;
    padding: 0 10px;
}

.section-header h2 {
    text-align: center;
}

.header-actions {
    display: flex;
    justify-content: flex-end;
}

.bestsellers h2 {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.8rem;
    font-weight: 400;
    letter-spacing: 0.25em;
    margin: 0;
    color: #1a1a1a;
}

.btn-text {
    background: none;
    border: none;
    color: #666;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    cursor: pointer;
    padding: 8px 0;
    position: relative;
    transition: color 0.3s ease;
}

.btn-text::after {
    content: '';
    position: absolute;
    bottom: 4px;
    left: 0;
    width: 0;
    height: 1px;
    background: #1a1a1a;
    transition: width 0.3s ease;
}

.btn-text:hover {
    color: #1a1a1a;
}

.btn-text:hover::after {
    width: 100%;
}

/* Slider */
.slider-wrapper {
    position: relative;
    display: flex;
    align-items: center;
}

.products-slider {
    display: flex;
    gap: 24px;
    overflow-x: auto;
    scroll-behavior: smooth;
    scrollbar-width: none;
    -ms-overflow-style: none;
    padding: 10px 5px;
    width: 100%;
}

.products-slider::-webkit-scrollbar {
    display: none;
}

.arrow {
    flex-shrink: 0;
    width: 44px;
    height: 44px;
    border: 1px solid #e0e0e0;
    background: #fff;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    color: #333;
    z-index: 2;
}

.arrow:hover {
    background: #1a1a1a;
    border-color: #1a1a1a;
    color: #fff;
}

.arrow-left { margin-right: 16px; }
.arrow-right { margin-left: 16px; }

/* Cards */
.product-card {
    flex: 0 0 220px;
    background: #fff;
    cursor: pointer;
    transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    border: 1px solid #e8e8e8;
}

.product-card:hover {
    transform: translateY(-8px);
}

.image-container {
    position: relative;
    aspect-ratio: 3/4;
    overflow: hidden;
    background: #f5f5f5;
    margin-bottom: 16px;
}

.image-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.product-card:hover .image-container img {
    transform: scale(1.05);
}

.product-info {
    text-align: left;
    padding: 0 4px;
}

.product-info h3 {
    font-size: 0.65rem;
    font-weight: 400;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: #333;
    margin: 0 0 8px;
    line-height: 1.5;
}

.price {
    font-size: 0.75rem;
    font-weight: 500;
    color: #1a1a1a;
    letter-spacing: 0.05em;
}

/* Responsive */
@media (max-width: 768px) {
    .arrow { display: none; }
    
    .product-card {
        flex: 0 0 160px;
    }
    
    .bestsellers h2 {
        font-size: 1.4rem;
    }
    
    .section-header {
        justify-content: center;
        gap: 20px;
    }
    
    .btn-text {
        position: absolute;
        right: 5%;
    }
}
</style>