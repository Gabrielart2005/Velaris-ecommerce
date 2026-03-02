<template>
    <section>
        <div class="outer">
            <div class="inner">
                <div class="bg" :style="bgStyle">
                    <h2 class="section-heading">{{ text }}</h2>
                </div>
            </div>
        </div>
    </section>
</template>

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

<style scoped>
.bg { 
    background-repeat: no-repeat; 
    background-size: cover;
    height: 100vh;
    width: 100%;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: center;
}

section {
    display: flex;
    align-items: center;
    justify-content: center;

    height: 100vh;
}
</style>