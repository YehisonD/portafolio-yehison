<script setup>
const projects = [
  {
    title: 'PCMATCH',
    stack: ['Vue.js', 'Spring Boot', 'Supabase', 'Docker'],
    description: 'Desarrollo fullstack y contenedorización de un sistema de emparejamiento de componentes. Trabajo colaborativo bajo metodologías Gitflow.',
    repo: 'https://github.com/xGabinho/PCMATCH.git',
  },
  {
    title: 'Sistema de Gestión de Parqueadero',
    stack: ['Java', 'Spring Boot', 'JPA/Hibernate', 'MySQL', 'Postman'],
    description: 'Backend para gestionar accesos y calcular tarifas mediante servicios API REST. Manejo global de excepciones y arquitectura por capas.',
    repo: null,
  },
  {
    title: 'Aplicaciones web backend modulares',
    stack: ['PHP', 'Laravel', 'Python', 'Django', 'Docker'],
    description: 'Patrones MVC/MVT, paneles administrativos y control de acceso basado en roles (RBAC) con entornos portables en Docker.',
    repo: null,
  },
]
</script>

<template>
  <section id="proyectos" class="scroll-mt-20 py-16 md:py-24">
    <div class="max-w-5xl mx-auto px-4 sm:px-6">
      <h2 class="text-2xl sm:text-3xl font-bold mb-10">
        <span class="text-term-cyan">#</span> Proyectos
      </h2>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <article
          v-for="(project, i) in projects"
          :key="i"
          class="group flex flex-col rounded-lg border border-term-border bg-term-panel p-6 transition-all duration-300 hover:border-term-green/60 hover:-translate-y-1 hover:shadow-lg hover:shadow-term-green/5"
        >
          <!-- Project title -->
          <h3 class="text-lg font-bold text-term-text mb-3 group-hover:text-term-green transition-colors">
            {{ project.title }}
          </h3>

          <!-- Stack chips -->
          <div class="flex flex-wrap gap-1.5 mb-4">
            <span
              v-for="tech in project.stack"
              :key="tech"
              class="px-2 py-0.5 text-[11px] rounded border border-term-border text-term-muted bg-term-bg"
            >
              {{ tech }}
            </span>
          </div>

          <!-- Description -->
          <p class="text-sm text-term-muted leading-relaxed flex-1 mb-5">
            {{ project.description }}
          </p>

          <!-- Link / disabled label -->
          <div class="mt-auto">
            <a
              v-if="project.repo"
              :href="project.repo"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-term-green/40 text-term-green text-sm font-medium hover:bg-term-green/10 transition-all focus:outline-none focus:ring-2 focus:ring-term-green focus:ring-offset-2 focus:ring-offset-term-bg"
            >
              <!-- GitHub icon -->
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.477 2 12c0 4.42 2.865 8.166 6.839 9.489.5.092.682-.217.682-.482 0-.237-.009-.866-.013-1.7-2.782.604-3.369-1.34-3.369-1.34-.454-1.156-1.11-1.463-1.11-1.463-.908-.62.069-.608.069-.608 1.003.07 1.531 1.03 1.531 1.03.892 1.529 2.341 1.087 2.91.831.092-.646.35-1.086.636-1.336-2.22-.253-4.555-1.11-4.555-4.943 0-1.091.39-1.984 1.029-2.683-.103-.253-.446-1.27.098-2.647 0 0 .84-.269 2.75 1.025A9.578 9.578 0 0112 6.836a9.59 9.59 0 012.504.337c1.909-1.294 2.747-1.025 2.747-1.025.546 1.377.203 2.394.1 2.647.64.699 1.028 1.592 1.028 2.683 0 3.842-2.339 4.687-4.566 4.935.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.743 0 .267.18.578.688.48C19.138 20.163 22 16.418 22 12c0-5.523-4.477-10-10-10z" clip-rule="evenodd" />
              </svg>
              Ver código
            </a>
            <a
              v-else
              href="#contacto"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-term-border text-term-muted text-sm hover:text-term-cyan hover:border-term-cyan/50 hover:bg-term-cyan/5 transition-all group-hover/btn"
              title="Haz clic para solicitar el código a Yehison"
            >
              <!-- Lock icon -->
              <svg class="w-4 h-4 text-term-amber" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
                <rect x="3" y="11" width="18" height="11" rx="2" ry="2" />
                <path d="M7 11V7a5 5 0 0110 0v4" />
              </svg>
              Código bajo solicitud (Contactar)
            </a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
