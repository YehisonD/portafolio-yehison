<script setup>
import { onMounted } from 'vue'

const highlights = [
  {
    icon: 'code',
    title: 'Arquitectura Limpia & APIs REST',
    desc: 'Diseño de servicios backend desacoplados, aplicando patrones MVC/MVT, arquitectura por capas y manejo centralizado de excepciones.',
  },
  {
    icon: 'database',
    title: 'Persistencia & Modelado SQL',
    desc: 'Estructuración de esquemas relacionales eficientes en PostgreSQL y MySQL, optimizando consultas mediante JPA/Hibernate y Supabase.',
  },
  {
    icon: 'terminal',
    title: 'Contenedorización & Flujo Git',
    desc: 'Entornos de desarrollo reproducibles mediante Docker y trabajo colaborativo estandarizado con metodología Gitflow y pull requests.',
  },
  {
    icon: 'badge',
    title: 'Disponibilidad SENA ADSO',
    desc: 'Disponible de forma inmediata para vinculación mediante Contrato de Aprendizaje en Etapa Productiva (vigente hasta abril de 2027).',
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

  document.querySelectorAll('#sobre-mi .reveal-item').forEach((el) => observer.observe(el))
})
</script>

<template>
  <section id="sobre-mi" class="scroll-mt-20 py-20 md:py-28">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <div class="reveal-item flex items-center gap-3 mb-6">
        <h2 class="text-2xl sm:text-3xl font-bold tracking-tight">
          <span class="text-term-cyan">//</span> Sobre mí
        </h2>
        <span class="h-px flex-1 bg-gradient-to-r from-term-border to-transparent"></span>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start mb-12">
        <!-- Main Description -->
        <div class="lg:col-span-7 space-y-4 text-term-muted text-sm sm:text-base leading-relaxed reveal-item">
          <p>
            Soy aprendiz del tecnólogo en <strong class="text-term-text">Análisis y Desarrollo de Software (ADSO)</strong> en el SENA, con una sólida orientación hacia el <strong class="text-term-green">desarrollo backend</strong> y la construcción de sistemas robustos, seguros y escalables.
          </p>
          <p>
            Me apasiona la lógica del servidor, el flujo ordenado de datos y resolver problemas reales mediante código mantenible. Cuento con experiencia práctica desarrollando con <span class="text-term-text font-medium">Java (Spring Boot)</span>, <span class="text-term-text font-medium">PHP (Laravel)</span> y <span class="text-term-text font-medium">Python (Django)</span>, implementando arquitecturas por capas y contenedorización con <span class="text-term-text font-medium">Docker</span>.
          </p>
          <p>
            Busco una empresa donde aportar compromiso técnico, capacidad de aprendizaje ágil y disciplina durante mi <strong class="text-term-cyan">Etapa Productiva</strong> bajo la modalidad de Contrato de Aprendizaje.
          </p>
        </div>

        <!-- Terminal Quick Info Box -->
        <div class="lg:col-span-5 reveal-item" style="transition-delay: 150ms">
          <div class="rounded-xl border border-term-border bg-term-panel/80 backdrop-blur p-5 font-mono text-xs space-y-3 shadow-xl">
            <div class="flex items-center gap-1.5 pb-2 border-b border-term-border text-term-muted">
              <span class="w-2.5 h-2.5 rounded-full bg-term-green/80"></span>
              <span>dev_profile.json</span>
            </div>
            <div class="space-y-1 text-term-muted">
              <div><span class="text-term-cyan">"nombre"</span>: <span class="text-term-text">"Yehison Jesús Delgado Fuentes"</span>,</div>
              <div><span class="text-term-cyan">"programa"</span>: <span class="text-term-text">"ADSO (SENA)"</span>,</div>
              <div><span class="text-term-cyan">"especialidad"</span>: <span class="text-term-green">"Desarrollo Backend"</span>,</div>
              <div><span class="text-term-cyan">"modalidad"</span>: <span class="text-term-amber">"Contrato de Aprendizaje"</span>,</div>
              <div><span class="text-term-cyan">"vigencia_etapa"</span>: <span class="text-term-text">"Hasta Abril de 2027"</span>,</div>
              <div><span class="text-term-cyan">"ubicacion"</span>: <span class="text-term-text">"Colombia (Remoto / Presencial)"</span></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Highlights 4-box Grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
        <div
          v-for="(item, idx) in highlights"
          :key="idx"
          class="reveal-item rounded-xl border border-term-border bg-term-panel/60 p-5 transition-all duration-300 hover:border-term-cyan/50 hover:bg-term-panel/90 hover:-translate-y-1"
          :style="{ transitionDelay: `${idx * 100}ms` }"
        >
          <div class="flex items-center gap-2 mb-2 text-term-cyan font-semibold text-sm">
            <span class="text-term-green">&gt;</span>
            <span class="text-term-text">{{ item.title }}</span>
          </div>
          <p class="text-xs sm:text-sm text-term-muted leading-relaxed">
            {{ item.desc }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
