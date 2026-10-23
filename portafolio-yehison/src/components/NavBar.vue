<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

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

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-300 border-b',
      scrolled
        ? 'bg-term-bg/95 backdrop-blur-md border-term-border'
        : 'bg-transparent border-transparent',
    ]"
    aria-label="Navegación principal"
  >
    <div class="max-w-5xl mx-auto px-4 sm:px-6 flex items-center justify-between h-14">
      <!-- Logo -->
      <a href="#inicio" class="text-term-green font-bold text-lg tracking-tight hover:text-term-cyan transition-colors">
        &gt;_ yehison
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
      </ul>
    </Transition>
  </nav>
</template>
