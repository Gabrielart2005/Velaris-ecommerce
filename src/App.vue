<script setup>
import Navbar from './components/Common/Navbar.vue'

import { onMounted, ref } from 'vue'

import Section from './components/Home/Section.vue'
import Bestsellers from './components/Home/Bestsellers.vue'
import Coleccion from './components/Home/Coleccion.vue'

import { gsap } from 'gsap'
import { Observer } from 'gsap/Observer'

gsap.registerPlugin(Observer)

import img1 from './assets/Img_1.png'
import img2 from './assets/Img_2.png'
import img3 from './assets/img_3.png'

const sections = ref([
  { text: 'UN ESTILO QUE<br>TRANSCIENDE EL TIEMPO', img: img1 },
  { text: 'PEQUEÑOS LUJOS<br>PARA GRANDES INSTANTES', img: img2 },
  { text: 'VISTE LA ESENCIA VELARIS', img: img3 }
])

onMounted(() => {
  const heroSlider = document.querySelector('#hero-slider')
  const sectionEls = heroSlider.querySelectorAll('section')
  const images = heroSlider.querySelectorAll('.bg')
  const headings = gsap.utils.toArray('.section-heading', heroSlider)
  const outerWrappers = gsap.utils.toArray('.outer', heroSlider)
  const innerWrappers = gsap.utils.toArray('.inner', heroSlider)

  gsap.set(outerWrappers, { yPercent: 100 })
  gsap.set(innerWrappers, { yPercent: -100 })

  let currentIndex = -1
  const totalSlides = sectionEls.length
  let animating = false

  function gotoSection(index, direction) {
    // Clamp: don't go below 0 or above last slide
    if (index < 0 || index >= totalSlides) return
    animating = true
    const fromTop = direction === -1
    const dFactor = fromTop ? -1 : 1

    const tl = gsap.timeline({
      defaults: { duration: 1.1, ease: 'power1.inOut' },
      onComplete: () => (animating = false)
    })

    if (currentIndex >= 0) {
      gsap.set(sectionEls[currentIndex], { zIndex: 0 })
      tl.to(images[currentIndex], { yPercent: -15 * dFactor })
        .set(sectionEls[currentIndex], { autoAlpha: 0 })
    }

    gsap.set(sectionEls[index], { autoAlpha: 1, zIndex: 1 })
    tl.fromTo(
      [outerWrappers[index], innerWrappers[index]],
      { yPercent: (i) => (i ? -100 * dFactor : 100 * dFactor) },
      { yPercent: 0 },
      0
    )
      .fromTo(images[index], { yPercent: 15 * dFactor }, { yPercent: 0 }, 0)
      .fromTo(
        headings[index],
        { autoAlpha: 0, yPercent: 30 * dFactor },
        { autoAlpha: 1, yPercent: 0, duration: 0.9, ease: 'power2' },
        0.15
      )

    currentIndex = index
  }

  Observer.create({
    target: heroSlider,
    type: 'wheel,touch,pointer',
    wheelSpeed: -1,
    onDown: () => {
      if (!animating && currentIndex > 0) gotoSection(currentIndex - 1, -1)
    },
    onUp: () => {
      if (!animating && currentIndex < totalSlides - 1) gotoSection(currentIndex + 1, 1)
    },
    tolerance: 10,
    preventDefault: false
  })

  gotoSection(0, 1)
})
</script>

<template>
  <div id="app">
    <Navbar />
    <div id="hero-slider">
      <Section
        v-for="(s, i) in sections"
        :key="i"
        :text="s.text"
        :img="s.img"
      />
    </div>
    <Bestsellers />
    <Coleccion />
  </div>
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  background: #fff;
  font-family: "Cormorant Garamond", serif;
}

#app {
  margin: 0;
  padding: 0;
}

/* ── Hero Slider ── */
#hero-slider {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

#hero-slider section {
  position: absolute;
  top: 0; left: 0;
  width: 100%;
  height: 100%;
  visibility: hidden;
  will-change: transform;
}

#hero-slider section .outer,
#hero-slider section .inner {
  width: 100%;
  height: 100%;
  overflow: hidden;
  will-change: transform;
}

.bg {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  background-size: cover;
  background-position: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.section-heading {
  color: #fafafa;
  font-size: clamp(0.5rem, 4vw, 4rem);
  font-weight: 200;
  text-align: center;
  letter-spacing: 0.10em;
  font-style: italic;
}

</style>





