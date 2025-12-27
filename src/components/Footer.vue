<template>
  <footer ref="sectionRef" class="bg-gradient-to-br from-amber-100 via-orange-50 to-amber-50 text-zinc-900 min-h-screen flex items-center py-14 border-t border-[#F1DEC6] opacity-0 transition-opacity duration-1000" :class="{ 'opacity-100': isVisible }">
    <div class="w-full container mx-auto px-4">
      <div class="max-w-6xl mx-auto grid md:grid-cols-[1.6fr_1fr] gap-10 items-start">

        <!-- Brand & Social -->
        <div>
          <h3 class="text-2xl font-bold tracking-tight mb-2">
            {{ firstName }} <span class="text-amber-700">{{ lastName }}</span>
          </h3>
          <p class="text-slate-700 mb-3">{{ claudiuData.personal.title }}</p>
          <p class="text-slate-600 italic">"{{ claudiuData.footer.tagline }}"</p>

          <div class="flex gap-3 mt-6">
            <a v-for="social in socials" :key="social.label" :href="social.href" :aria-label="social.label"
              class="w-10 h-10 rounded-full bg-white border border-[#F1DEC6] shadow-[0_6px_18px_rgba(17,24,39,0.06)] text-amber-700 grid place-items-center hover:bg-amber-500 hover:text-white transition-colors">
              <span class="text-sm font-semibold">{{ social.short }}</span>
            </a>
          </div>
        </div>

        <!-- Contact Info -->
        <div class="bg-white rounded-xl border border-[#F1DEC6] shadow-[0_8px_30px_rgba(17,24,39,0.06)] p-6">
          <h4 class="text-lg font-semibold mb-4">Contact</h4>
          <div class="space-y-3 text-slate-700">
            <p>{{ claudiuData.personal.phone }}</p>
            <p>{{ claudiuData.personal.email }}</p>
            <p>{{ claudiuData.personal.location }}</p>
          </div>
        </div>

      </div>

      <div class="border-t border-[#F1DEC6] mt-10 pt-6 text-sm text-slate-600 flex flex-col md:flex-row md:items-center md:justify-between gap-3">
        <span>© {{ currentYear }} {{ claudiuData.personal.name }}. All rights reserved.</span>
        <span class="text-slate-500">Handcrafted in a light, warm palette.</span>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import claudiuData from '../data/claudiuData.js'

const currentYear = computed(() => new Date().getFullYear())
const [firstName, ...restName] = claudiuData.personal.name.split(' ')
const lastName = restName.join(' ')

const sectionRef = ref(null)
const isVisible = ref(false)

const socials = [
  { label: 'Instagram', href: claudiuData.socialMedia.instagram, short: 'ig' },
  { label: 'YouTube', href: claudiuData.socialMedia.youtube, short: 'yt' },
  { label: 'Facebook', href: claudiuData.socialMedia.facebook, short: 'fb' },
  { label: 'LinkedIn', href: claudiuData.socialMedia.linkedin, short: 'in' },
]

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
