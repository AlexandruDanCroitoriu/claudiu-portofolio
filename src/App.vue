<script setup>
import { onMounted } from 'vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Footer from './components/Footer.vue'

onMounted(() => {
  console.log('App mounted')
})
</script>

<template>
  <div class="bg-white text-zinc-900"> 
    <Hero />
    <About />
    <Footer />
  </div>
</template>

<style scoped>
/* Styles will be added as needed */
</style>
