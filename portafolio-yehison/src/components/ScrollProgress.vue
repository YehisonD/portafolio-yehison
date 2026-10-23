<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const progress = ref(0)

function updateProgress() {
  const scrollTop = window.scrollY || document.documentElement.scrollTop
  const docHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight
  if (docHeight > 0) {
    progress.value = Math.min(100, Math.max(0, (scrollTop / docHeight) * 100))
  }
}

onMounted(() => {
  window.addEventListener('scroll', updateProgress, { passive: true })
  updateProgress()
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateProgress)
})
</script>

<template>
  <div class="fixed top-0 left-0 right-0 h-[2.5px] z-[60] bg-term-border/40 pointer-events-none">
    <div
      class="h-full bg-gradient-to-r from-term-green via-term-cyan to-term-amber transition-all duration-100 ease-out shadow-[0_0_8px_rgba(34,211,238,0.5)]"
      :style="{ width: `${progress}%` }"
    />
  </div>
</template>
