<script setup>
import { ref, onMounted } from 'vue'
import claudiuData from '../data/claudiuData.js'

const { title, subtitle, images } = claudiuData.gallery

const sectionRef = ref(null)
const isVisible = ref(false)

// Lightbox state
const selectedImage = ref(null)
const selectedIndex = ref(null)

const openLightbox = (image, index) => {
  selectedImage.value = image
  selectedIndex.value = index
}

const closeLightbox = () => {
  selectedImage.value = null
  selectedIndex.value = null
}

const nextImage = () => {
  if (selectedIndex.value < images.length - 1) {
    selectedIndex.value++
    selectedImage.value = images[selectedIndex.value]
  }
}

const prevImage = () => {
  if (selectedIndex.value > 0) {
    selectedIndex.value--
    selectedImage.value = images[selectedIndex.value]
  }
}

// Keyboard navigation
const handleKeydown = (e) => {
  if (!selectedImage.value) return
  if (e.key === 'Escape') closeLightbox()
  if (e.key === 'ArrowRight') nextImage()
  if (e.key === 'ArrowLeft') prevImage()
}

// Add keyboard listener when component mounts
if (typeof window !== 'undefined') {
  window.addEventListener('keydown', handleKeydown)
}

onMounted(() => {
  const observer = new IntersectionObserver(([entry]) => {
    isVisible.value = entry.isIntersecting
  }, { threshold: 0.1 })
  
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section ref="sectionRef" id="gallery" class="bg-amber-50 text-zinc-900 min-h-screen flex items-center py-16 px-4 opacity-0 transition-opacity duration-1000" :class="{ 'opacity-100': isVisible }">
    <div class="w-full container mx-auto max-w-7xl">
      <!-- Section Header -->
      <div class="text-center mb-12">
        <h2 class="text-4xl md:text-5xl font-bold text-zinc-900 mb-4">
          {{ title }}
        </h2>
        <p class="text-lg text-slate-700 max-w-2xl mx-auto">
          {{ subtitle }}
        </p>
      </div>

      <!-- Gallery Grid - Bento Layout -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 auto-rows-[200px] md:auto-rows-[250px]">
        <div
          v-for="(image, index) in images"
          :key="image.id"
          :class="[
            'group relative overflow-hidden rounded-lg cursor-pointer bg-white shadow-sm hover:shadow-lg transition-all duration-700 translate-y-10 opacity-0',
            image.size === 'large' ? 'md:col-span-2 md:row-span-2' : 'col-span-1',
            isVisible && `delay-${(index % 5) * 100}`
          ]"
          :style="isVisible ? { opacity: 1, transform: 'translateY(0)' } : {}"
          @click="openLightbox(image, index)"
        >
          <img
            :src="image.src"
            :alt="image.alt"
            class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
            loading="lazy"
          />
          <div class="absolute inset-0 bg-gradient-to-t from-zinc-900/60 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300">
            <div class="absolute bottom-0 left-0 right-0 p-4">
              <p v-if="image.caption" class="text-white text-sm font-medium">
                {{ image.caption }}
              </p>
            </div>
          </div>
          <!-- View Icon -->
          <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
            <div class="bg-white/90 rounded-full p-3">
              <svg class="w-6 h-6 text-zinc-900" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM10 7v3m0 0v3m0-3h3m-3 0H7" />
              </svg>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Lightbox Modal -->
    <Transition name="fade">
      <div
        v-if="selectedImage"
        class="fixed inset-0 z-50 bg-zinc-900/95 flex items-center justify-center p-4"
        @click="closeLightbox"
      >
        <!-- Close Button -->
        <button
          class="absolute top-4 right-4 text-white hover:text-amber-400 transition-colors duration-200 z-10"
          @click.stop="closeLightbox"
          aria-label="Close lightbox"
        >
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>

        <!-- Previous Button -->
        <button
          v-if="selectedIndex > 0"
          class="absolute left-4 text-white hover:text-amber-400 transition-colors duration-200 z-10"
          @click.stop="prevImage"
          aria-label="Previous image"
        >
          <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>

        <!-- Next Button -->
        <button
          v-if="selectedIndex < images.length - 1"
          class="absolute right-4 text-white hover:text-amber-400 transition-colors duration-200 z-10"
          @click.stop="nextImage"
          aria-label="Next image"
        >
          <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>

        <!-- Image Container -->
        <div class="max-w-6xl max-h-full flex items-center justify-center" @click.stop>
          <img
            :src="selectedImage.src"
            :alt="selectedImage.alt"
            class="max-w-full max-h-[90vh] object-contain rounded-lg shadow-2xl"
          />
        </div>

        <!-- Image Counter -->
        <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 text-white text-sm">
          {{ selectedIndex + 1 }} / {{ images.length }}
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Prevent body scroll when lightbox is open */
body:has(.fixed.z-50) {
  overflow: hidden;
}
</style>
