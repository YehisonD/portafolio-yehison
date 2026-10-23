<script setup>
import { ref, onMounted } from 'vue'

const copied = ref(false)

async function copyEmail() {
  try {
    await navigator.clipboard.writeText('yehisondelgado8@gmail.com')
    copied.value = true
    setTimeout(() => { copied.value = false }, 2000)
  } catch {
    alert('No se pudo copiar el email. Cópialo manualmente: yehisondelgado8@gmail.com')
  }
}

const contacts = [
  {
    label: '+57 301 522 0050',
    href: 'tel:+573015220050',
    icon: 'phone',
  },
  {
    label: 'yehisondelgado8@gmail.com',
    href: 'mailto:yehisondelgado8@gmail.com',
    icon: 'email',
  },
  {
    label: 'github.com/YehisonD',
    href: 'https://github.com/YehisonD',
    icon: 'github',
    external: true,
  },
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-revealed')
        }
      })
    },
    { threshold: 0.15 }
  )

  document.querySelectorAll('#contacto .reveal-item').forEach((el) => observer.observe(el))
})
</script>

<template>
  <section id="contacto" class="scroll-mt-20 py-16 md:py-24">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <div class="reveal-item flex items-center gap-3 mb-4">
        <h2 class="text-2xl sm:text-3xl font-bold tracking-tight">
          <span class="text-term-cyan">//</span> Contacto
        </h2>
        <span class="h-px flex-1 bg-gradient-to-r from-term-border to-transparent"></span>
      </div>

      <p class="reveal-item text-term-muted mb-10 max-w-xl text-sm sm:text-base leading-relaxed">
        ¿Interesado en vincularme mediante contrato de aprendizaje o colaborar en un proyecto?
        No dudes en contactarme.
      </p>

      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-8">
        <a
          v-for="(c, i) in contacts"
          :key="i"
          :href="c.href"
          :target="c.external ? '_blank' : undefined"
          :rel="c.external ? 'noopener noreferrer' : undefined"
          class="reveal-item group flex items-center gap-4 p-4 rounded-xl border border-term-border bg-term-panel/90 transition-all duration-300 hover:border-term-cyan/60 hover:-translate-y-1.5 hover:shadow-xl hover:shadow-term-cyan/5"
          :style="{ transitionDelay: `${i * 100}ms` }"
        >
          <!-- Phone icon -->
          <div v-if="c.icon === 'phone'" class="flex-shrink-0 w-10 h-10 rounded-lg bg-term-bg flex items-center justify-center border border-term-border group-hover:border-term-cyan/40 transition-colors">
            <svg class="w-5 h-5 text-term-cyan" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
            </svg>
          </div>

          <!-- Email icon -->
          <div v-else-if="c.icon === 'email'" class="flex-shrink-0 w-10 h-10 rounded-lg bg-term-bg flex items-center justify-center border border-term-border group-hover:border-term-cyan/40 transition-colors">
            <svg class="w-5 h-5 text-term-cyan" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
          </div>

          <!-- GitHub icon -->
          <div v-else-if="c.icon === 'github'" class="flex-shrink-0 w-10 h-10 rounded-lg bg-term-bg flex items-center justify-center border border-term-border group-hover:border-term-cyan/40 transition-colors">
            <svg class="w-5 h-5 text-term-cyan" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.477 2 12c0 4.42 2.865 8.166 6.839 9.489.5.092.682-.217.682-.482 0-.237-.009-.866-.013-1.7-2.782.604-3.369-1.34-3.369-1.34-.454-1.156-1.11-1.463-1.11-1.463-.908-.62.069-.608.069-.608 1.003.07 1.531 1.03 1.531 1.03.892 1.529 2.341 1.087 2.91.831.092-.646.35-1.086.636-1.336-2.22-.253-4.555-1.11-4.555-4.943 0-1.091.39-1.984 1.029-2.683-.103-.253-.446-1.27.098-2.647 0 0 .84-.269 2.75 1.025A9.578 9.578 0 0112 6.836a9.59 9.59 0 012.504.337c1.909-1.294 2.747-1.025 2.747-1.025.546 1.377.203 2.394.1 2.647.64.699 1.028 1.592 1.028 2.683 0 3.842-2.339 4.687-4.566 4.935.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.743 0 .267.18.578.688.48C19.138 20.163 22 16.418 22 12c0-5.523-4.477-10-10-10z" clip-rule="evenodd" />
            </svg>
          </div>

          <span class="text-sm text-term-text group-hover:text-term-cyan transition-colors break-all">
            {{ c.label }}
          </span>
        </a>
      </div>

      <!-- Copy email button -->
      <div class="reveal-item">
        <button
          @click="copyEmail"
          class="inline-flex items-center gap-2 px-5 py-2.5 rounded-lg border border-term-cyan/40 text-term-cyan text-sm font-medium hover:bg-term-cyan/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-cyan focus:ring-offset-2 focus:ring-offset-term-bg"
          :aria-label="copied ? 'Email copiado' : 'Copiar email al portapapeles'"
        >
          <!-- Copy icon -->
          <svg v-if="!copied" class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
            <rect x="9" y="9" width="13" height="13" rx="2" ry="2" />
            <path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1" />
          </svg>
          <!-- Check icon -->
          <svg v-else class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
            <polyline points="20 6 9 17 4 12" />
          </svg>
          {{ copied ? '¡Copiado!' : 'Copiar email' }}
        </button>
      </div>
    </div>
  </section>
</template>
