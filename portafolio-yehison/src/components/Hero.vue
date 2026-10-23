<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

const lines = [
  { cmd: '$ whoami', output: 'Yehison Jesús Delgado Fuentes' },
  { cmd: '$ cat perfil.txt', output: 'Aprendiz Tecnólogo en Análisis y Desarrollo de Software (ADSO) | Desarrollador Backend' },
  { cmd: '$ status --disponibilidad', output: 'Disponible para Contrato de Aprendizaje (Etapa Productiva) hasta abril de 2027' },
]

const prefersReducedMotion = ref(false)
const currentLineIndex = ref(0)
const currentCharIndex = ref(0)
const phase = ref('cmd') // 'cmd' | 'output' | 'done'
const displayedLines = ref([])

let timer = null

const currentText = computed(() => {
  if (currentLineIndex.value >= lines.length) return ''
  const line = lines[currentLineIndex.value]
  const source = phase.value === 'cmd' ? line.cmd : line.output
  return source.slice(0, currentCharIndex.value)
})

function typeNext() {
  if (currentLineIndex.value >= lines.length) {
    clearInterval(timer)
    return
  }

  const line = lines[currentLineIndex.value]
  const source = phase.value === 'cmd' ? line.cmd : line.output

  if (currentCharIndex.value < source.length) {
    currentCharIndex.value++
  } else {
    if (phase.value === 'cmd') {
      displayedLines.value.push({ text: line.cmd, type: 'cmd' })
      phase.value = 'output'
      currentCharIndex.value = 0
    } else {
      displayedLines.value.push({ text: line.output, type: 'output' })
      currentLineIndex.value++
      phase.value = 'cmd'
      currentCharIndex.value = 0
    }
  }
}

onMounted(() => {
  const mq = window.matchMedia('(prefers-reduced-motion: reduce)')
  prefersReducedMotion.value = mq.matches

  if (mq.matches) {
    // Show everything at once
    lines.forEach(l => {
      displayedLines.value.push({ text: l.cmd, type: 'cmd' })
      displayedLines.value.push({ text: l.output, type: 'output' })
    })
    currentLineIndex.value = lines.length
  } else {
    timer = setInterval(typeNext, 40)
  }
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>

<template>
  <section id="inicio" class="scroll-mt-20 pt-24 pb-16 md:pt-32 md:pb-24">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <!-- Terminal window -->
      <div class="rounded-lg border border-term-border bg-term-panel overflow-hidden shadow-2xl shadow-term-green/5 animate-fadeUp">
        <!-- Terminal title bar -->
        <div class="flex items-center gap-2 px-4 py-2.5 bg-term-bg/60 border-b border-term-border">
          <span class="w-3 h-3 rounded-full bg-red-500/80"></span>
          <span class="w-3 h-3 rounded-full bg-yellow-500/80"></span>
          <span class="w-3 h-3 rounded-full bg-green-500/80"></span>
          <span class="ml-3 text-xs text-term-muted">yehison@portfolio:~</span>
        </div>

        <!-- Terminal content -->
        <div class="p-4 sm:p-6 text-sm sm:text-base space-y-1 min-h-[200px]">
          <!-- Already typed lines -->
          <div v-for="(line, i) in displayedLines" :key="i">
            <span :class="line.type === 'cmd' ? 'text-term-green' : 'text-term-text'">
              {{ line.text }}
            </span>
          </div>

          <!-- Currently typing line -->
          <div v-if="currentLineIndex < lines.length">
            <span :class="phase === 'cmd' ? 'text-term-green' : 'text-term-text'">
              {{ currentText }}
            </span>
            <span class="inline-block w-2 h-4 bg-term-green align-middle animate-blink ml-0.5"></span>
          </div>

          <!-- Final cursor after all lines done -->
          <div v-else>
            <span class="text-term-green">$ </span>
            <span class="inline-block w-2 h-4 bg-term-green align-middle animate-blink ml-0.5"></span>
          </div>
        </div>
      </div>

      <!-- Hero text content -->
      <div class="mt-10 md:mt-14 space-y-6 animate-fadeUp" style="animation-delay: .3s">
        <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold">
          Hola, soy <span class="text-term-green">Yehison</span>
        </h1>
        <p class="text-term-muted text-base sm:text-lg max-w-2xl leading-relaxed">
          Desarrollador Backend enfocado en construir APIs robustas y escalables con
          <span class="text-term-text font-medium">Java/Spring Boot</span>,
          <span class="text-term-text font-medium">PHP/Laravel</span>,
          <span class="text-term-text font-medium">Python/Django</span> y
          <span class="text-term-text font-medium">APIs REST</span>.
        </p>

        <!-- Availability badge -->
        <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full border border-term-green/30 bg-term-green/5 text-sm">
          <span class="relative flex h-2.5 w-2.5">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-term-green opacity-75"></span>
            <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-term-green"></span>
          </span>
          <span class="text-term-green font-medium">Disponible: Contrato de Aprendizaje (Etapa Productiva)</span>
        </div>

        <!-- CTA Buttons -->
        <div class="flex flex-wrap gap-4 pt-2">
          <a
            href="#proyectos"
            class="inline-flex items-center gap-2 px-6 py-2.5 rounded-lg bg-term-green text-term-bg font-semibold text-sm hover:bg-term-green/90 transition-all hover:shadow-lg hover:shadow-term-green/20 focus:outline-none focus:ring-2 focus:ring-term-green focus:ring-offset-2 focus:ring-offset-term-bg"
          >
            <!-- Arrow icon -->
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
            </svg>
            Ver Proyectos
          </a>
          <a
            href="#contacto"
            class="inline-flex items-center gap-2 px-6 py-2.5 rounded-lg border border-term-cyan text-term-cyan font-semibold text-sm hover:bg-term-cyan/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-cyan focus:ring-offset-2 focus:ring-offset-term-bg"
          >
            Contactar
          </a>
          <a
            href="/cv-yehison-delgado.pdf"
            download="CV-Yehison-Delgado.pdf"
            target="_blank"
            class="inline-flex items-center gap-2 px-6 py-2.5 rounded-lg border border-term-amber text-term-amber font-semibold text-sm hover:bg-term-amber/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-amber focus:ring-offset-2 focus:ring-offset-term-bg"
          >
            <!-- Download icon -->
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            Descargar CV
          </a>
        </div>
      </div>
    </div>
  </section>
</template>
