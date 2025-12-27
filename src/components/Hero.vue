<template>
  <section
    ref="sectionRef"
    class="relative w-full min-h-[80vh] overflow-hidden bg-black opacity-0 transition-opacity duration-1000"
    :class="{ 'opacity-100': isVisible }"
  >
    <img
      :src="image13Src"
      alt="Stage presence"
      class="absolute inset-0 w-full h-full object-contain "
      loading="eager"
      decoding="async"
    />
    <div class="absolute inset-0 bg-black/45"></div>
    <div class="relative z-10 container mx-auto px-4 h-full flex items-center justify-center text-center">
      <div class="translate-y-10 opacity-0 transition-all duration-1000" :class="{ 'translate-y-0 opacity-100': isVisible }">
        <h1 class="text-white text-5xl md:text-6xl font-extrabold tracking-tight">
          {{ fullName }}
        </h1>
        <a href="#about" class="mt-6 inline-flex items-center rounded-md bg-amber-500 hover:bg-amber-600 px-6 py-3 text-white shadow-md shadow-amber-200/40">
          despre mine
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import claudiuData from '../data/claudiuData.js'

const fullName = claudiuData.personal.name

const heroImage = claudiuData.gallery?.images?.find?.(img => img.id === 2)
const image13Src = computed(() => heroImage?.src || claudiuData.personal.heroImage)

const sectionRef = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(([entry]) => {
    isVisible.value = entry.isIntersecting
  }, { threshold: 0.1 })

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<style scoped>
</style>
