<template>
  <section class="relative bg-white py-16">
    <div class="container mx-auto px-4 grid md:grid-cols-[1fr_1.2fr] gap-8 items-start">
      <div class="relative">
        <img src="https://images.unsplash.com/photo-1511379938547-c1f69419868d?auto=format&fit=crop&w=900&q=80" alt="About photo" class="rounded-xl shadow-[0_12px_30px_rgba(17,24,39,0.15)] object-cover w-full h-[340px] md:h-[420px]"/>
      </div>
      <article class="bg-amber-50 border border-[#F1DEC6] rounded-xl p-6 md:p-8 shadow-[0_8px_30px_rgba(17,24,39,0.06)]">
        <h3 class="text-amber-700 tracking-[0.2em] uppercase text-sm mb-2">About Me</h3>
        <h4 class="text-zinc-900 text-xl font-semibold tracking-tight mb-3">{{ name }}</h4>
        <p class="text-slate-700 leading-relaxed">{{ bio }}</p>
        <a href="#" class="mt-4 inline-block text-amber-600 hover:text-amber-700 font-medium">Read my full bio →</a>
      </article>
    </div>
  </section>
</template>

<script setup>
import claudiuData from '../data/claudiuData.js'

const name = claudiuData.personal.name
const bio = claudiuData.personal.bio
</script>

<style scoped></style>
