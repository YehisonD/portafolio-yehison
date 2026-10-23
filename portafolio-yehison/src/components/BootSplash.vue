<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['finish'])

const steps = [
  'BIOS / KERNEL BOOT 2.4.0 ... [OK]',
  'INITIALIZING SYSTEM ARCHITECTURE ... [OK]',
  'LOADING BACKEND SERVICES (Java, Spring Boot, Python, PHP) ... [OK]',
  'ESTABLISHING DATABASE CONNECTIONS (PostgreSQL, MySQL) ... [OK]',
  'CONFIGURING DOCKER CONTAINERS & REST APIS ... [OK]',
  'STATUS: APPRENTICE DEVELOPER READY FOR RECRUITERS ... [ONLINE]',
]

const displayedSteps = ref([])
const progress = ref(0)
const isDone = ref(false)

function skip() {
  isDone.value = true
  setTimeout(() => emit('finish'), 350)
}

onMounted(() => {
  // Check prefers-reduced-motion
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    emit('finish')
    return
  }

  let current = 0
  const interval = setInterval(() => {
    if (current < steps.length) {
      displayedSteps.value.push(steps[current])
      progress.value = Math.round(((current + 1) / steps.length) * 100)
      current++
    } else {
      clearInterval(interval)
      setTimeout(() => {
        isDone.value = true
        setTimeout(() => emit('finish'), 450)
      }, 300)
    }
  }, 180)
})
</script>

<template>
  <Transition
    enter-active-class="transition-opacity duration-300"
    leave-active-class="transition-all duration-500 ease-in-out"
    leave-from-class="opacity-100 scale-100"
    leave-to-class="opacity-0 scale-105"
  >
    <div
      v-if="!isDone"
      class="fixed inset-0 z-[100] flex flex-col justify-between p-6 sm:p-12 bg-term-bg font-mono select-none"
    >
      <!-- Top Bar -->
      <div class="flex items-center justify-between text-xs text-term-muted border-b border-term-border pb-3">
        <div class="flex items-center gap-2">
          <span class="inline-block w-2.5 h-2.5 rounded-full bg-term-green animate-ping"></span>
          <span class="text-term-green font-bold">BOOT SEQUENCE // YEHISON DELGADO</span>
        </div>
        <button
          @click="skip"
          class="text-term-cyan hover:text-term-text border border-term-cyan/40 hover:border-term-cyan px-2.5 py-1 rounded text-xs transition-colors"
        >
          Saltar [ESC] &gt;&gt;
        </button>
      </div>

      <!-- Terminal Output Center -->
      <div class="my-auto max-w-2xl w-full mx-auto space-y-2 text-xs sm:text-sm">
        <div
          v-for="(step, index) in displayedSteps"
          :key="index"
          class="flex items-start gap-2"
        >
          <span class="text-term-cyan">&gt;</span>
          <span
            :class="index === displayedSteps.length - 1 ? 'text-term-green font-bold' : 'text-term-text/80'"
          >
            {{ step }}
          </span>
        </div>

        <div v-if="displayedSteps.length < steps.length" class="flex items-center gap-2">
          <span class="text-term-cyan">&gt;</span>
          <span class="inline-block w-2 h-4 bg-term-green animate-blink"></span>
        </div>

        <!-- Progress Bar -->
        <div class="pt-6 space-y-2">
          <div class="flex justify-between text-xs text-term-muted">
            <span>CARGANDO RECURSOS...</span>
            <span class="text-term-cyan font-bold">{{ progress }}%</span>
          </div>
          <div class="h-1.5 w-full bg-term-panel rounded-full overflow-hidden border border-term-border">
            <div
              class="h-full bg-gradient-to-r from-term-green via-term-cyan to-term-amber transition-all duration-200"
              :style="{ width: `${progress}%` }"
            ></div>
          </div>
        </div>
      </div>

      <!-- Bottom Hint -->
      <div class="text-center text-[11px] text-term-muted">
        Iniciando entorno interactivo para reclutadores &middot; Presiona en cualquier parte para continuar
      </div>
    </div>
  </Transition>
</template>
