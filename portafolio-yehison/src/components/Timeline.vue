<script setup>
import { onMounted } from 'vue'

const milestones = [
  {
    period: '2024 — Presente',
    title: 'Tecnólogo en Análisis y Desarrollo de Software (ADSO)',
    institution: 'Servicio Nacional de Aprendizaje (SENA)',
    tag: 'Formación Tecnológica',
    tagColor: 'green',
    description: 'Formación rigurosa en ingeniería de software: modelado de bases de datos normalizadas (SQL), Programación Orientada a Objetos, diseño y consumo de APIs REST, y metodologías ágiles de trabajo en equipo.',
    skills: ['Java', 'PHP', 'Python', 'MySQL', 'PostgreSQL', 'Scrum', 'Git'],
  },
  {
    period: 'Proyecto Destacado',
    title: 'Desarrollo Fullstack & Contenedorización — PCMATCH',
    institution: 'Proyecto Colaborativo',
    tag: 'Fullstack & DevOps',
    tagColor: 'cyan',
    description: 'Participación como desarrollador backend y fullstack. Implementación de controladores, servicios y contenedorización con Docker, sincronizando el trabajo grupal mediante ramas de Gitflow.',
    skills: ['Spring Boot', 'Vue.js', 'Docker', 'Supabase', 'Gitflow'],
  },
  {
    period: 'Especialización Práctica',
    title: 'Desarrollo de Sistemas Backend & Arquitectura por Capas',
    institution: 'Proyectos de Software Autónomo',
    tag: 'Backend Core',
    tagColor: 'amber',
    description: 'Implementación de servicios REST completos: gestión de parqueadero con cálculo de tarifas y manejo global de excepciones en Spring Boot, y sistemas modulares con control de roles (RBAC) en Laravel y Django.',
    skills: ['JPA/Hibernate', 'Spring Boot', 'Laravel', 'Django', 'Postman', 'Docker'],
  },
  {
    period: 'Meta Inmediata (Hasta Abril 2027)',
    title: 'Etapa Productiva — Contrato de Aprendizaje',
    institution: 'Vinculación Empresarial SENA',
    tag: 'Disponible Ahora',
    tagColor: 'green',
    description: 'Etapa habilitada para integrarme a un equipo de desarrollo profesional, aportando capacidad técnica en el ecosistema backend y aprendiendo estándares de la industria.',
    skills: ['Contrato de Aprendizaje', 'Trabajo en Equipo', 'Backend Developer'],
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

  document.querySelectorAll('#trayectoria .reveal-item').forEach((el) => observer.observe(el))
})
</script>

<template>
  <section id="trayectoria" class="scroll-mt-20 py-20 md:py-28">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <div class="reveal-item flex items-center gap-3 mb-12">
        <h2 class="text-2xl sm:text-3xl font-bold tracking-tight">
          <span class="text-term-cyan">#</span> Trayectoria & Formación
        </h2>
        <span class="h-px flex-1 bg-gradient-to-r from-term-border to-transparent"></span>
      </div>

      <!-- Git Log Graph Timeline -->
      <div class="relative border-l-2 border-term-border ml-3 sm:ml-6 space-y-12">
        <div
          v-for="(item, i) in milestones"
          :key="i"
          class="reveal-item relative pl-6 sm:pl-10 group"
          :style="{ transitionDelay: `${i * 120}ms` }"
        >
          <!-- Commit node dot -->
          <div
            class="absolute -left-[9px] top-1.5 w-4 h-4 rounded-full border-2 border-term-bg transition-all duration-300 group-hover:scale-125"
            :class="[
              item.tagColor === 'green' ? 'bg-term-green group-hover:shadow-[0_0_10px_#4ade80]' : '',
              item.tagColor === 'cyan' ? 'bg-term-cyan group-hover:shadow-[0_0_10px_#22d3ee]' : '',
              item.tagColor === 'amber' ? 'bg-term-amber group-hover:shadow-[0_0_10px_#fbbf24]' : '',
            ]"
          ></div>

          <!-- Card content -->
          <div class="rounded-xl border border-term-border bg-term-panel/80 p-5 sm:p-6 transition-all duration-300 hover:border-term-cyan/50 hover:bg-term-panel hover:shadow-xl hover:shadow-cyan-950/20">
            <!-- Period & Tag -->
            <div class="flex flex-wrap items-center justify-between gap-2 mb-2">
              <span class="text-xs font-mono text-term-muted">
                {{ item.period }}
              </span>
              <span
                class="text-[10px] uppercase font-bold tracking-wider px-2 py-0.5 rounded border"
                :class="[
                  item.tagColor === 'green' ? 'text-term-green border-term-green/30 bg-term-green/5' : '',
                  item.tagColor === 'cyan' ? 'text-term-cyan border-term-cyan/30 bg-term-cyan/5' : '',
                  item.tagColor === 'amber' ? 'text-term-amber border-term-amber/30 bg-term-amber/5' : '',
                ]"
              >
                {{ item.tag }}
              </span>
            </div>

            <!-- Title -->
            <h3 class="text-base sm:text-lg font-bold text-term-text mb-1 group-hover:text-term-cyan transition-colors">
              {{ item.title }}
            </h3>

            <div class="text-xs text-term-muted font-medium mb-3">
              {{ item.institution }}
            </div>

            <p class="text-xs sm:text-sm text-term-muted leading-relaxed mb-4">
              {{ item.description }}
            </p>

            <!-- Skill chips -->
            <div class="flex flex-wrap gap-1.5 pt-2 border-t border-term-border/50">
              <span
                v-for="s in item.skills"
                :key="s"
                class="text-[11px] px-2 py-0.5 rounded bg-term-bg border border-term-border/70 text-term-muted"
              >
                {{ s }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
