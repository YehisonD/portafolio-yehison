<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from './components/NavBar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Timeline from './components/Timeline.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import AppFooter from './components/Footer.vue'
import BootSplash from './components/BootSplash.vue'
import ScrollProgress from './components/ScrollProgress.vue'
import ScrollTop from './components/ScrollTop.vue'
import CvModal from './components/CvModal.vue'

const showSplash = ref(true)
const isCvModalOpen = ref(false)

const mouseX = ref(500)
const mouseY = ref(300)
const isMouseMoving = ref(false)

function onMouseMove(e) {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
  isMouseMoving.value = true
}

function onSplashFinish() {
  showSplash.value = false
}

function openCvModal() {
  isCvModalOpen.value = true
}

function closeCvModal() {
  isCvModalOpen.value = false
}

onMounted(() => {
  window.addEventListener('mousemove', onMouseMove, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('mousemove', onMouseMove)
})
</script>

<template>
  <div class="relative min-h-screen overflow-x-hidden selection:bg-term-cyan/20 selection:text-term-cyan">
    <!-- Boot Terminal Animation -->
    <BootSplash v-if="showSplash" @finish="onSplashFinish" />

    <!-- Top Scroll Progress Bar -->
    <ScrollProgress />

    <!-- Interactive Cursor Spotlight Glow -->
    <div
      class="pointer-events-none fixed inset-0 -z-10 transition-opacity duration-700 hidden sm:block"
      :class="isMouseMoving ? 'opacity-100' : 'opacity-0'"
      :style="{
        background: `radial-gradient(650px circle at ${mouseX}px ${mouseY}px, rgba(34,211,238,0.045), transparent 70%)`
      }"
    ></div>

    <!-- Ambient background glows -->
    <div
      class="pointer-events-none fixed inset-0 -z-20"
      style="background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(34,211,238,0.06) 0%, transparent 60%), radial-gradient(ellipse 60% 40% at 85% 90%, rgba(74,222,128,0.04) 0%, transparent 50%)"
    ></div>

    <!-- Tech Grid Overlay -->
    <div
      class="pointer-events-none fixed inset-0 -z-20 opacity-[0.035]"
      style="background-image: linear-gradient(rgba(226,232,240,0.3) 1px, transparent 1px), linear-gradient(90deg, rgba(226,232,240,0.3) 1px, transparent 1px); background-size: 50px 50px"
    ></div>

    <!-- Navigation -->
    <NavBar @open-cv="openCvModal" />

    <!-- Main Content -->
    <main>
      <Hero @open-cv="openCvModal" />
      <About />
      <Skills />
      <Timeline />
      <Projects />
      <Contact />
    </main>

    <!-- Footer -->
    <AppFooter />

    <!-- Floating Scroll-To-Top Button -->
    <ScrollTop />

    <!-- Modal for Previewing CV -->
    <CvModal :is-open="isCvModalOpen" @close="closeCvModal" />
  </div>
</template>
