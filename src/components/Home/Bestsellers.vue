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
        name: 'BOTAS ALTEAS DE TACON DE AGUJA',
        price: '$25',
        image: imgHeels
    },
    {
        id: 6,
        name: 'VESTIDO ELEGANTE CON CINTURA ANUDADA MARRON',
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
        name: 'ZAPATOS DE TACON BAJO COLOR BURDEOS',
        price: '$26',
        image: imgFlats
    }
]

const slider = ref(null)

const scrollLeft = () => {
    slider.value.scrollBy({ left: -300, behavior: 'smooth' })
}

const scrollRight = () => {
    slider.value.scrollBy({ left: 300, behavior: 'smooth' })
}
</script>

<template>
    <section class="bestsellers">
       <div class="section-header">
           <h2>BESTSELLERS</h2>
           <button class="btn">VER TODO</button>
       </div>

       <div class="slider-wrapper">
           <button class="arrow arrow-left" @click="scrollLeft">&#8249;</button>

           <div class="products-slider" ref="slider">
               <div v-for="product in products" :key="product.id" class="product-card">
                   <span class="badge">Top ventas</span>

                   <div class="image-container">
                       <img :src="product.image" :alt="product.name">
                   </div>

                   <div class="product-info">
                       <h3>{{ product.name }}</h3>
                       <p>{{ product.price }}</p>
                   </div>
               </div>
           </div>

           <button class="arrow arrow-right" @click="scrollRight">&#8250;</button>
       </div>
    </section>
</template>

<style scoped>

.bestsellers {
    padding: 0 2% 10px;
    text-align: center;
}

.section-header {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 1200px;
    margin: 0 auto 10px;
    padding: 0 10px;
}

.bestsellers h2 {
    font-size: 2rem;
    letter-spacing: 3px;
    margin: 0;
    text-align: center;
}


.btn {
    position: absolute;
    padding: 5px 10px;
    right: 0;
    background-color: transparent;
    border: 1px solid #161616;
    color: #161616;
    font-size: 12px;
    letter-spacing: 1px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn:hover {
    background-color: #161616;
    color: #ffffff;
}

/* ── Slider ── */
.slider-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    max-width: 1280px;
    margin: 0 auto;
}

.products-slider {
    display: flex;
    gap: 20px;
    overflow-x: auto;
    scroll-behavior: smooth;
    scrollbar-width: none;
    -ms-overflow-style: none;
    padding: 10px 0;
}

.products-slider::-webkit-scrollbar {
    display: none;
}

.arrow {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 2;
    background: rgba(255, 255, 255, 0.9);
    border: 1px solid #ccc;
    font-size: 28px;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    color: #333;
}

.arrow:hover {
    background: #000;
    color: #fff;
    border-color: #000;
}

.arrow-left {
    left: -15px;
}

.arrow-right {
    right: -15px;
}

/* ── Cards ── */
.product-card {
    flex: 0 0 calc(25% - 15px);
    min-width: 240px;
    background-color: #fff;
    border: 1px solid #e6e6e6;
    padding: 15px;
    text-align: center;
    position: relative;
    transition: transform 0.3s ease;
}

.product-card:hover {
    transform: translateY(-5px);
}

.badge {
    position: absolute;
    top: 0;
    left: 0;
    background-color: #000;
    color: #fff;
    padding: 5px 10px;
    font-size: 10px;
    letter-spacing: 1px;
}

.image-container {
    margin-bottom: 15px;
}

.image-container img {
    width: 100%;
    height: auto;
    display: block;
}

.product-info h3 {
    font-size: 0.70rem;
    margin-bottom: 5px;
    font-weight: 500;
    letter-spacing: 1px;
    text-align: left;
    color: #2c2c2c;
}

.product-info p {
    font-size: 0.70rem;
    font-weight: 600;
    margin-bottom: 15px;
    text-align: left;
    color: #555555;
}
</style>