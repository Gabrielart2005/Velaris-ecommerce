<script setup>
import { ref } from 'vue'

const title = ref('SILUETAS NOCTURNAS')
const description = ref('Una oda a la forma y la textura en su expresión más pura.<br>Descubre una colección que juega con las sombras y la luz donde cada pieza <br> cuenta una historia de elegancia y misterio.')
const buttonText = ref('VER COLECCIÓN')

</script>

<template>
    <div class="container-collection">
        <div class="collection-box">
            <div class="collection-image">
                <img src="../../assets/banner-large.png" alt="banner-collection">
            </div>
            <div class="collection-info">
                <h2>SILUETAS NOCTURNAS</h2>
                <p>Una oda a la forma y la textura en su expresión más pura.<br>
                    Descubre una colección que juega con las sombras y la luz 
                    donde cada pieza <br> cuenta una historia de elegancia y misterio.
                </p>
                <button class="btn">VER COLECCIÓN</button>
            </div>
        </div>
    </div>
</template>

<style scoped>

@font-face {
    font-family: 'The Season';
    src: url('../../assets/fonts/the-season.ttf') format('truetype');
}   

.container-collection {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.collection-box {
    position: relative;
    width: 90%;
    height: 90%;
    overflow: hidden;
}

.collection-image {
    width: 100%;
    height: 100%;
}

.collection-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.collection-info {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20px;
    background-color: rgba(26, 0, 0, 0.35);
    text-align: center;
}

.collection-info h2 {
    font-family: 'The Season';
    color: #fff;    
    font-size: 2.5rem;
    margin-bottom: 24px;
    letter-spacing: 2px;
    text-shadow: 0 0 3px rgba(39, 39, 39, 0.5);
}

.collection-info p {
    font-size: 1.4rem;
    margin-bottom: 20px;
    line-height: 1.5;
    color: #ececec;
}

.btn {
    padding: 12px 24px;
    background-color: transparent;
    border: 1px solid #fff;
    color: #fff;
    font-size: 12px;
    letter-spacing: 1px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn:hover {
    background-color: #fff;
    color: #161616;
}
</style>
