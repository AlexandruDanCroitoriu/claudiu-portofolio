<template>
  <section class="relative bg-amber-50 py-16 md:py-24 overflow-hidden">
    <div class="container mx-auto px-4 grid md:grid-cols-2 gap-10 items-center">
      <div>
        <span class="text-amber-600 uppercase tracking-[0.2em] text-xs">Guitarist & Composer</span>
        <h1 class="mt-3 text-5xl md:text-6xl font-extrabold tracking-tight text-zinc-900">
          {{ firstName }} <br class="md:hidden"/> {{ lastName }}
        </h1>
        <button class="mt-6 inline-flex items-center rounded-md bg-amber-500 hover:bg-amber-600 px-5 py-3 text-white shadow-md shadow-amber-200/40">
          View My Reel
        </button>
      </div>
      <div class="relative">
        <div class="absolute -inset-4 -z-10 rounded-2xl bg-gradient-to-br from-amber-100 to-orange-100"></div>
        <img :src="claudiuData.personal.heroImage" alt="Guitarist performing" class="relative rounded-2xl shadow-[0_12px_30px_rgba(17,24,39,0.15)] object-cover w-full h-[320px] md:h-[420px]"/>
        <!-- Simple vertical social bar -->
        <div class="hidden md:flex flex-col gap-2 absolute left-2 top-2">
          <span class="w-8 h-8 bg-zinc-900/80 text-white rounded-md grid place-items-center text-xs">f</span>
          <span class="w-8 h-8 bg-zinc-900/80 text-white rounded-md grid place-items-center text-xs">ig</span>
          <span class="w-8 h-8 bg-zinc-900/80 text-white rounded-md grid place-items-center text-xs">yt</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import claudiuData from '../data/claudiuData.js'

const [firstName, ...restName] = claudiuData.personal.name.split(' ')
const lastName = restName.join(' ')
</script>

<style scoped>
</style>
