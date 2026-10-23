<script setup>
import NavBar from './components/NavBar.vue'
import Hero from './components/Hero.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import AppFooter from './components/Footer.vue'
</script>

<template>
  <div class="relative min-h-screen overflow-x-hidden">
    <!-- Subtle radial gradient background -->
    <div
      class="pointer-events-none fixed inset-0 -z-10"
      style="background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(34,211,238,0.06) 0%, transparent 60%), radial-gradient(ellipse 60% 40% at 80% 100%, rgba(74,222,128,0.04) 0%, transparent 50%)"
    ></div>

    <!-- Subtle grid overlay -->
    <div
      class="pointer-events-none fixed inset-0 -z-10 opacity-[0.03]"
      style="background-image: linear-gradient(rgba(226,232,240,0.3) 1px, transparent 1px), linear-gradient(90deg, rgba(226,232,240,0.3) 1px, transparent 1px); background-size: 60px 60px"
    ></div>

    <NavBar />

    <main>
      <Hero />
      <Skills />
      <Projects />
      <Contact />
    </main>

    <AppFooter />
  </div>
</template>
