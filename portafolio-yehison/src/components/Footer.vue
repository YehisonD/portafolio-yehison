<script setup>
const year = new Date().getFullYear()
</script>

<template>
  <footer class="border-t border-term-border py-8">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 text-center text-sm text-term-muted">
      © {{ year }} Yehison Jesús Delgado Fuentes · Hecho con Vue 3 y Tailwind CSS
    </div>
  </footer>
</template>
