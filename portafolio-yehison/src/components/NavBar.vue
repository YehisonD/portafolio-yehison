<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits(['open-cv'])

const menuOpen = ref(false)

const links = [
  { label: 'Inicio', href: '#inicio' },
  { label: 'Habilidades', href: '#habilidades' },
  { label: 'Proyectos', href: '#proyectos' },
  { label: 'Contacto', href: '#contacto' },
]

const scrolled = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 20
}

function closeMenu() {
  menuOpen.value = false
}

function handleCvClick() {
  closeMenu()
  emit('open-cv')
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-300 border-b',
      scrolled
        ? 'bg-term-bg/95 backdrop-blur-md border-term-border shadow-lg shadow-black/20'
        : 'bg-transparent border-transparent',
    ]"
    aria-label="Navegación principal"
  >
    <div class="max-w-5xl mx-auto px-4 sm:px-6 flex items-center justify-between h-14">
      <!-- Logo -->
      <a href="#inicio" class="text-term-green font-bold text-lg tracking-tight hover:text-term-cyan transition-colors flex items-center gap-1.5">
        <span class="text-term-green">&gt;_</span>
        <span class="text-term-text hover:text-term-cyan transition-colors">yehison</span>
      </a>

      <!-- Desktop links -->
      <ul class="hidden md:flex items-center gap-6">
        <li v-for="link in links" :key="link.href">
          <a
            :href="link.href"
            class="text-sm text-term-muted hover:text-term-cyan transition-colors"
          >
            {{ link.label }}
          </a>
        </li>
        <li>
          <button
            @click="handleCvClick"
            class="inline-flex items-center gap-1.5 px-3 py-1 text-xs font-semibold rounded-md border border-term-amber/70 text-term-amber hover:bg-term-amber/10 transition-all focus:outline-none focus:ring-1 focus:ring-term-amber"
          >
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
            </svg>
            Ver CV
          </button>
        </li>
      </ul>

      <!-- Mobile hamburger -->
      <button
        class="md:hidden flex flex-col gap-1.5 p-2 -mr-2"
        :aria-label="menuOpen ? 'Cerrar menú' : 'Abrir menú'"
        :aria-expanded="menuOpen"
        @click="menuOpen = !menuOpen"
      >
        <span
          :class="[
            'block w-5 h-0.5 bg-term-text transition-all duration-300',
            menuOpen ? 'rotate-45 translate-y-2' : '',
          ]"
        />
        <span
          :class="[
            'block w-5 h-0.5 bg-term-text transition-all duration-300',
            menuOpen ? 'opacity-0' : '',
          ]"
        />
        <span
          :class="[
            'block w-5 h-0.5 bg-term-text transition-all duration-300',
            menuOpen ? '-rotate-45 -translate-y-2' : '',
          ]"
        />
      </button>
    </div>

    <!-- Mobile menu -->
    <Transition
      enter-active-class="transition-all duration-300 ease-out"
      leave-active-class="transition-all duration-200 ease-in"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <ul
        v-if="menuOpen"
        class="md:hidden bg-term-panel/95 backdrop-blur-md border-t border-term-border px-4 py-4 space-y-3"
      >
        <li v-for="link in links" :key="link.href">
          <a
            :href="link.href"
            class="block text-sm text-term-muted hover:text-term-cyan transition-colors py-1"
            @click="closeMenu"
          >
            {{ link.label }}
          </a>
        </li>
        <li class="pt-2 border-t border-term-border">
          <button
            @click="handleCvClick"
            class="w-full inline-flex items-center justify-center gap-2 px-3 py-2 text-sm text-term-amber border border-term-amber/50 rounded-md hover:bg-term-amber/10 transition-colors"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
            </svg>
            Ver Hoja de Vida (PDF)
          </button>
        </li>
      </ul>
    </Transition>
  </nav>
</template>
