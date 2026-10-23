<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const visible = ref(false)

function onScroll() {
  visible.value = window.scrollY > 400
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<template>
  <Transition
    enter-active-class="transition-all duration-300 ease-out"
    leave-active-class="transition-all duration-200 ease-in"
    enter-from-class="opacity-0 translate-y-4 scale-90"
    enter-to-class="opacity-100 translate-y-0 scale-100"
    leave-from-class="opacity-100 translate-y-0 scale-100"
    leave-to-class="opacity-0 translate-y-4 scale-90"
  >
    <button
      v-if="visible"
      @click="scrollToTop"
      class="fixed bottom-6 right-6 z-40 p-3 rounded-lg border border-term-border bg-term-panel/90 backdrop-blur-md text-term-cyan hover:text-term-green hover:border-term-green/60 hover:shadow-lg hover:shadow-term-green/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-green"
      aria-label="Volver al inicio"
      title="Volver arriba"
    >
      <!-- Arrow Up icon with terminal prompt -->
      <div class="flex items-center gap-1.5 text-xs font-mono font-bold">
        <span>&gt;</span>
        <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" aria-hidden="true">
          <path stroke-linecap="round" stroke-linejoin="round" d="M5 15l7-7 7 7" />
        </svg>
      </div>
    </button>
  </Transition>
</template>
