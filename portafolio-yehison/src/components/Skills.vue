<script setup>
import { onMounted } from 'vue'

const categories = [
  {
    title: '// Backend & APIs',
    chips: ['Java (Spring Boot)', 'PHP (Laravel)', 'Python (Django)', 'Arquitectura por capas', 'MVC/MVT', 'APIs REST'],
    accent: 'cyan',
  },
  {
    title: '// Frontend',
    chips: ['Vue.js', 'Tailwind CSS', 'JavaScript', 'HTML5', 'CSS3'],
    accent: 'green',
  },
  {
    title: '// Bases de Datos',
    chips: ['MySQL', 'PostgreSQL', 'Supabase', 'JPA/Hibernate'],
    accent: 'amber',
  },
  {
    title: '// Herramientas & DevOps',
    chips: ['Docker', 'Git/Gitflow', 'GitHub', 'Postman'],
    accent: 'cyan',
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

  document.querySelectorAll('#habilidades .reveal-item').forEach((el) => observer.observe(el))
})
</script>

<template>
  <section id="habilidades" class="scroll-mt-20 py-16 md:py-24">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <div class="reveal-item flex items-center gap-3 mb-10">
        <h2 class="text-2xl sm:text-3xl font-bold tracking-tight">
          <span class="text-term-cyan">#</span> Habilidades
        </h2>
        <span class="h-px flex-1 bg-gradient-to-r from-term-border to-transparent"></span>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div
          v-for="(cat, i) in categories"
          :key="i"
          class="reveal-item group relative rounded-xl border border-term-border bg-term-panel/90 p-6 transition-all duration-300 hover:border-term-cyan/60 hover:-translate-y-1.5 hover:shadow-xl hover:shadow-term-cyan/5 overflow-hidden"
          :style="{ transitionDelay: `${i * 120}ms` }"
        >
          <!-- Corner decorative dot -->
          <div class="absolute top-3 right-3 w-1.5 h-1.5 rounded-full bg-term-border group-hover:bg-term-cyan transition-colors"></div>

          <h3 class="text-term-muted text-sm font-semibold mb-4 group-hover:text-term-cyan transition-colors flex items-center gap-2">
            <span>{{ cat.title }}</span>
          </h3>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="chip in cat.chips"
              :key="chip"
              class="px-3 py-1 text-xs rounded-md border border-term-border/80 bg-term-bg/80 text-term-text transition-all duration-200 hover:border-term-cyan hover:text-term-cyan hover:bg-term-cyan/10 hover:scale-105 cursor-default"
            >
              {{ chip }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
