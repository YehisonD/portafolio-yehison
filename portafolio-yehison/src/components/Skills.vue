<script setup>
const categories = [
  {
    title: '// Backend & APIs',
    chips: ['Java (Spring Boot)', 'PHP (Laravel)', 'Python (Django)', 'Arquitectura por capas', 'MVC/MVT', 'APIs REST'],
  },
  {
    title: '// Frontend',
    chips: ['Vue.js', 'Tailwind CSS', 'JavaScript', 'HTML5', 'CSS3'],
  },
  {
    title: '// Bases de Datos',
    chips: ['MySQL', 'PostgreSQL', 'Supabase', 'JPA/Hibernate'],
  },
  {
    title: '// Herramientas & DevOps',
    chips: ['Docker', 'Git/Gitflow', 'GitHub', 'Postman'],
  },
]
</script>

<template>
  <section id="habilidades" class="scroll-mt-20 py-16 md:py-24">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <h2 class="text-2xl sm:text-3xl font-bold mb-10">
        <span class="text-term-cyan">#</span> Habilidades
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div
          v-for="(cat, i) in categories"
          :key="i"
          class="group rounded-lg border border-term-border bg-term-panel p-6 transition-all duration-300 hover:border-term-cyan/60 hover:-translate-y-1 hover:shadow-lg hover:shadow-term-cyan/5"
        >
          <h3 class="text-term-muted text-sm font-medium mb-4 group-hover:text-term-cyan transition-colors">
            {{ cat.title }}
          </h3>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="chip in cat.chips"
              :key="chip"
              class="px-3 py-1 text-xs rounded-full border border-term-border bg-term-bg text-term-text transition-all duration-200 hover:border-term-cyan hover:text-term-cyan hover:bg-term-cyan/5 cursor-default"
            >
              {{ chip }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
