<script setup>
import Navbar from './components/Common/Navbar.vue';
import Footer from './components/Common/Footer.vue';
</script>

<template>
  <div id="app">
    <Navbar />
    <router-view />
    <Footer />
  </div>
</template>

<style>
#app {
  margin: 0;
  padding: 0;
  width: 100%;
}
</style>
