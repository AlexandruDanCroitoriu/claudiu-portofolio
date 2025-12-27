<template>
  <section id="about" ref="sectionRef" class="relative bg-white text-zinc-900 flex items-center py-16 opacity-0 transition-opacity duration-1000" :class="{ 'opacity-100': isVisible }">
    <div class="w-full container mx-auto px-4 grid md:grid-cols-[1fr_1.2fr] gap-8 items-start">
      <div class="relative translate-y-10 opacity-0 transition-all duration-1000 h-full" :class="{ 'translate-y-0 opacity-100': isVisible }">
        <img :src="aboutImageSrc" alt="About photo" class="rounded-xl shadow-[0_12px_30px_rgba(17,24,39,0.15)] object-cover w-full h-full"/>
      </div>
      <article class="bg-amber-50 border border-[#F1DEC6] rounded-xl p-6 md:p-8 shadow-[0_8px_30px_rgba(17,24,39,0.06)] translate-y-10 opacity-0 transition-all duration-1000 delay-200 h-full" :class="{ 'translate-y-0 opacity-100': isVisible }">
        <h4 class="text-zinc-900 text-xl font-semibold tracking-tight mb-3">{{ name }}</h4>
        <p class="text-slate-700 leading-relaxed whitespace-pre-line">{{ bio }}</p>
      </article>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import claudiuData from '../data/claudiuData.js'

const name = claudiuData.personal.name
const bio = claudiuData.personal.bio

const aboutImage = claudiuData.gallery?.images?.find?.(img => img.id === 2)
const aboutImageSrc = computed(() => aboutImage?.src || claudiuData.personal.profileImage)

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

<style scoped></style>
