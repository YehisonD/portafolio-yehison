<script setup>
import { ref, onMounted, onUnmounted, computed, nextTick } from 'vue'

const emit = defineEmits(['open-cv'])

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
const cmdInput = ref('')
const cmdInputRef = ref(null)
const interactiveHistory = ref([])
const terminalContainer = ref(null)

let timer = null

const currentText = computed(() => {
  if (currentLineIndex.value >= lines.length) return ''
  const line = lines[currentLineIndex.value]
  const source = phase.value === 'cmd' ? line.cmd : line.output
  return source.slice(0, currentCharIndex.value)
})

const isIntroDone = computed(() => currentLineIndex.value >= lines.length)

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

function executeCommand() {
  const raw = cmdInput.value.trim()
  if (!raw) return
  const clean = raw.toLowerCase()
  cmdInput.value = ''

  let output = ''

  switch (clean) {
    case 'help':
      output = `Comandos disponibles:
  • help      : Muestra esta lista de comandos
  • whoami    : Información del desarrollador
  • skills    : Resumen del stack tecnológico
  • projects  : Lista de proyectos destacados
  • contact   : Canales directos de contacto
  • cv        : Ver / descargar hoja de vida
  • clear     : Limpiar consola
  • date      : Fecha y hora actual`
      break
    case 'whoami':
      output = 'Yehison Jesús Delgado Fuentes — Aprendiz ADSO SENA, Desarrollador Backend enfocado en arquitecturas limpias y APIs REST.'
      break
    case 'skills':
      output = 'Backend: Java (Spring Boot), PHP (Laravel), Python (Django) | DB: MySQL, PostgreSQL, Supabase | Herramientas: Docker, Git, Postman'
      break
    case 'projects':
      output = '1. PCMATCH (Vue + Spring Boot + Docker)\n2. Sistema Gestión Parqueadero (Java + Spring Boot + JPA)\n3. Apps Web Backend Modulares (PHP/Laravel + Python/Django)'
      break
    case 'contact':
      output = 'Teléfono: +57 301 522 0050\nEmail: yehisondelgado8@gmail.com\nGitHub: github.com/YehisonD'
      break
    case 'cv':
      emit('open-cv')
      output = '[OK] Abriendo visor de Hoja de Vida de Yehison Delgado...'
      break
    case 'clear':
      interactiveHistory.value = []
      return
    case 'date':
      output = new Date().toLocaleString('es-CO')
      break
    default:
      output = `Comando no reconocido: "${raw}". Escribe "help" para ver los comandos disponibles.`
  }

  interactiveHistory.value.push({ input: raw, output })

  nextTick(() => {
    if (terminalContainer.value) {
      terminalContainer.value.scrollTop = terminalContainer.value.scrollHeight
    }
  })
}

function focusTerminalInput() {
  if (cmdInputRef.value) {
    cmdInputRef.value.focus()
  }
}

onMounted(() => {
  const mq = window.matchMedia('(prefers-reduced-motion: reduce)')
  prefersReducedMotion.value = mq.matches

  if (mq.matches) {
    lines.forEach(l => {
      displayedLines.value.push({ text: l.cmd, type: 'cmd' })
      displayedLines.value.push({ text: l.output, type: 'output' })
    })
    currentLineIndex.value = lines.length
  } else {
    timer = setInterval(typeNext, 35)
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
      <div
        class="rounded-xl border border-term-border bg-term-panel/90 backdrop-blur-md overflow-hidden shadow-2xl shadow-term-green/5 transition-all duration-300 hover:border-term-green/40 hover:shadow-term-green/10"
        @click="focusTerminalInput"
      >
        <!-- Terminal title bar -->
        <div class="flex items-center justify-between px-4 py-2.5 bg-term-bg/80 border-b border-term-border">
          <div class="flex items-center gap-2">
            <span class="w-3 h-3 rounded-full bg-red-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-yellow-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-green-500/80"></span>
            <span class="ml-3 text-xs text-term-muted">yehison@portfolio:~</span>
          </div>
          <div v-if="isIntroDone" class="text-[11px] text-term-cyan/70 font-mono hidden sm:block">
            Terminal interactiva activa (escribe "help")
          </div>
        </div>

        <!-- Terminal content -->
        <div
          ref="terminalContainer"
          class="p-4 sm:p-6 text-xs sm:text-sm space-y-2 min-h-[220px] max-h-[380px] overflow-y-auto font-mono scrollbar-thin scrollbar-thumb-term-border"
        >
          <!-- Already typed lines -->
          <div v-for="(line, i) in displayedLines" :key="i">
            <span :class="line.type === 'cmd' ? 'text-term-green' : 'text-term-text'">
              {{ line.text }}
            </span>
          </div>

          <!-- Currently typing line -->
          <div v-if="!isIntroDone">
            <span :class="phase === 'cmd' ? 'text-term-green' : 'text-term-text'">
              {{ currentText }}
            </span>
            <span class="inline-block w-2 h-4 bg-term-green align-middle animate-blink ml-0.5"></span>
          </div>

          <!-- Interactive terminal history -->
          <div v-for="(hist, idx) in interactiveHistory" :key="'h-' + idx" class="space-y-1 pt-1">
            <div class="text-term-green flex items-center gap-1.5">
              <span>$</span>
              <span>{{ hist.input }}</span>
            </div>
            <div class="text-term-text/90 whitespace-pre-wrap pl-3 border-l-2 border-term-border/60">
              {{ hist.output }}
            </div>
          </div>

          <!-- Interactive Input Prompt -->
          <form
            v-if="isIntroDone"
            @submit.prevent="executeCommand"
            class="flex items-center gap-2 pt-1"
          >
            <span class="text-term-green font-bold">$</span>
            <input
              ref="cmdInputRef"
              v-model="cmdInput"
              type="text"
              class="flex-1 bg-transparent border-0 outline-none text-term-text text-xs sm:text-sm p-0 focus:ring-0 placeholder:text-term-muted/50"
              placeholder="Escribe 'help', 'skills', 'cv'..."
              aria-label="Línea de comandos de terminal"
            />
            <span class="inline-block w-2 h-4 bg-term-green align-middle animate-blink"></span>
          </form>
        </div>
      </div>

      <!-- Hero text content -->
      <div class="mt-10 md:mt-14 space-y-6">
        <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold tracking-tight">
          Hola, soy <span class="text-transparent bg-clip-text bg-gradient-to-r from-term-green via-term-cyan to-term-green">Yehison</span>
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
        <div class="flex flex-wrap items-center gap-3 pt-2">
          <a
            href="#proyectos"
            class="inline-flex items-center gap-2 px-6 py-2.5 rounded-lg bg-term-green text-term-bg font-semibold text-sm hover:bg-term-green/90 transition-all hover:shadow-lg hover:shadow-term-green/20 focus:outline-none focus:ring-2 focus:ring-term-green focus:ring-offset-2 focus:ring-offset-term-bg"
          >
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

          <!-- Botón Ver CV (Modal) -->
          <button
            @click="emit('open-cv')"
            class="inline-flex items-center gap-2 px-5 py-2.5 rounded-lg border border-term-amber text-term-amber font-semibold text-sm hover:bg-term-amber/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-amber focus:ring-offset-2 focus:ring-offset-term-bg"
          >
            <!-- Document preview icon -->
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
            </svg>
            Ver Hoja de Vida
          </button>

          <!-- Botón Descargar CV directo -->
          <a
            href="/cv-yehison-delgado.pdf"
            download="CV-Yehison-Delgado.pdf"
            target="_blank"
            class="inline-flex items-center gap-1.5 p-2.5 rounded-lg border border-term-border text-term-muted hover:text-term-amber hover:border-term-amber/50 transition-colors"
            title="Descargar PDF directamente"
            aria-label="Descargar PDF de hoja de vida"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>
