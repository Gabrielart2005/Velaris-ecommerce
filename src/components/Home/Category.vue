<script setup>
import imgRopa from '../../assets/category-ropa.jpeg'
import imgZapatos from '../../assets/category-zapatos.png'
import imgAccesorios from '../../assets/category-accesorios.jpeg'
import imgCarteras from '../../assets/category-carteras.png'

const items = [
    {
        id: 1,
        name: 'Ropa',
        img: imgRopa,
        link: '#',
        class: 'tall'
    },
    {
        id: 2,
        name: 'Zapatos',
        img: imgZapatos,
        link: '#',
        class: 'tall'
    },
    {
        id: 3,
        name: 'Accesorios',
        img: imgAccesorios,
        link: '#',
        class: 'short'
    },
    {
        id: 4,
        name: 'Carteras',
        img: imgCarteras,
        link: '#',
        class: 'short'
    }
]
</script>

<template>
    <section class="category-section">
        <h2 class="category-title">COMPRA POR CATEGORÍA</h2>
        
        <div class="bento-grid">
            <a
                v-for="item in items"
                :key="item.id"
                :href="item.link"
                :class="['bento-item', item.class]"
            >
                <img :src="item.img" :alt="item.name" class="bento-img">
                <span class="bento-label">{{ item.name }}</span>
            </a>
        </div>
    </section>
</template>

<style scoped>
.category-section {
    padding: 60px 5%;
    max-width: 1400px;
    margin: 0 auto;
}

.category-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.6rem;
    font-weight: 400;
    letter-spacing: 0.2em;
    text-align: center;
    color: #1a1a1a;
    margin: 0 0 48px;
}

/* Bento Grid: 3 columnas */
.bento-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: repeat(2, 320px);
    gap: 12px;
}

.bento-item {
    position: relative;
    overflow: hidden;
    text-decoration: none;
    cursor: pointer;
    display: block;
    border: 1px solid #e8e8e8;
}

.bento-item.tall {
    grid-row: span 2;
}

.bento-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
}

.bento-item:hover .bento-img {
    transform: scale(1.08);
}

.bento-label {
    position: absolute;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
    font-family: 'Cormorant Garamond', serif;
    font-size: 1rem;
    font-style: italic;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: #fff;
    padding: 10px 20px;
    background: rgba(0, 0, 0, 0.4);
    backdrop-filter: blur(4px);
    border: 1px solid rgba(255, 255, 255, 0.5);
    transition: all 0.4s ease;
}

.bento-item:hover .bento-label {
    background: #fff;
    color: #1a1a1a;
    border-color: #fff;
}

/* Ajuste para carteras - imagen posicionada */
.bento-item:last-child .bento-img {
    object-position: 50% 80%;
}

/* Responsive: Tablet */
@media (max-width: 900px) {
    .bento-grid {
        grid-template-rows: repeat(2, 280px);
    }
}

/* Responsive: Mobile - vuelve a grid simple */
@media (max-width: 640px) {
    .category-section {
        padding: 40px 5%;
    }
    
    .category-title {
        font-size: 1.3rem;
        margin-bottom: 32px;
    }
    
    .bento-grid {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: repeat(4, 240px);
        gap: 16px;
    }
    
    .bento-item.tall {
        grid-row: span 1;
    }
}
</style>