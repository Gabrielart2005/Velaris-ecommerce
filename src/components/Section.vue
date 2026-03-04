<script setup>
import { computed } from 'vue';

const props = defineProps({
    text: { type: String, required: true },
    img:  { type: String, required: true }
});

const bgStyle = computed(() => ({
    backgroundImage:
    `linear-gradient(180deg, rgba(0,0,0,.6) 0%, rgba(0,0,0,.3) 100%), url('${props.img}')`
}));
</script>

<template>
    <section>
        <div class="outer">
            <div class="inner">
                <div class="bg" :style="bgStyle">
                    <h2 class="section-heading" v-html="text"></h2>
                    <div class="btn-container">
                        <button class="btn">VER COLECCIÓN</button>
                        <button class="btn">COMPRAR AHORA</button>
                    </div>
                    <div class="scroll-down">
                        <span class="scroll-text">DESLIZA PARA DESCUBRIR</span>
                        <img src="../assets/down-arrow.png" alt="Scroll down">
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>


<style scoped>
.bg { 
    background-repeat: no-repeat; 
    background-size: cover;
    height: 78vh;
    width: 100%;
    margin: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-bottom: 20px;
}

.section-heading {
    margin-top: auto;
}

section {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 78vh;
}

.btn-container {
    display: flex;
    gap: 40px;
    margin-top: 5px;
}

.btn {
    padding: 12px 24px;
    background-color: transparent;
    border: 1px solid #fff;
    color: #fff;
    font-size: 12px;
    letter-spacing: 2px;
    cursor: pointer;
    transition: all 0.3s ease;
    align-items: center;
    justify-content: center;
}

.btn:hover {
    background-color: #fff;
    color: #000;
}

.scroll-down {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: auto;
    margin-bottom: 10px;
}

.scroll-text {
    position: absolute;
    font-size: 0.65rem;
    letter-spacing: 2px;
    color: #ffffffcc;
}

.scroll-down img {
    width: 15px;
    height: 15px;
    margin-top: 40px;
    bottom: 50px;
    left: 50%;
    animation: scroll-down 4s ease-in-out infinite;
}

@keyframes scroll-down {
    0% {
        transform: translateY(0); opacity: 0;
    }
    50% {
        transform: translateY(10px); opacity: 1;
    }
    100% {
        transform: translateY(0); opacity: 0;
    }
}
</style>