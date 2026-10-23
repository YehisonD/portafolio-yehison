<script setup>
defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
})

const emit = defineEmits(['close'])

function close() {
  emit('close')
}
</script>

<template>
  <Transition
    enter-active-class="transition-all duration-300 ease-out"
    leave-active-class="transition-all duration-200 ease-in"
    enter-from-class="opacity-0"
    enter-to-class="opacity-100"
    leave-from-class="opacity-100"
    leave-to-class="opacity-0"
  >
    <div
      v-if="isOpen"
      class="fixed inset-0 z-50 flex items-center justify-center p-3 sm:p-6 bg-term-bg/80 backdrop-blur-md"
      @click.self="close"
    >
      <div
        class="relative w-full max-w-4xl h-[85vh] bg-term-panel border border-term-cyan/40 rounded-xl flex flex-col shadow-2xl shadow-term-cyan/10 overflow-hidden animate-fadeUp"
      >
        <!-- Modal Header -->
        <div class="flex items-center justify-between px-4 py-3 bg-term-bg/90 border-b border-term-border">
          <div class="flex items-center gap-2">
            <span class="w-3 h-3 rounded-full bg-red-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-yellow-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-green-500/80"></span>
            <span class="ml-2 text-xs sm:text-sm font-semibold text-term-text">
              Hoja de Vida — Yehison Delgado (Vista Previa)
            </span>
          </div>

          <div class="flex items-center gap-2">
            <a
              href="/cv-yehison-delgado.pdf"
              download="CV-Yehison-Delgado.pdf"
              class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-md bg-term-green text-term-bg text-xs font-bold hover:bg-term-green/90 transition-all"
            >
              <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              Descargar PDF
            </a>
            <button
              @click="close"
              class="p-1.5 rounded-md text-term-muted hover:text-term-text hover:bg-term-bg border border-term-border transition-colors text-xs font-bold"
              aria-label="Cerrar modal"
            >
              ✕
            </button>
          </div>
        </div>

        <!-- PDF Viewer Container -->
        <div class="flex-1 w-full bg-term-bg/50 overflow-hidden">
          <iframe
            src="/cv-yehison-delgado.pdf#toolbar=1"
            class="w-full h-full border-0"
            title="Vista previa de Hoja de Vida"
          ></iframe>
        </div>
      </div>
    </div>
  </Transition>
</template>
