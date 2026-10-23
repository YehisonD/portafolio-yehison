# Portafolio — Yehison Jesús Delgado Fuentes

Portafolio profesional construido con **Vue 3**, **Vite** y **Tailwind CSS v3**.
Diseño oscuro tipo terminal, orientado a desarrolladores backend.

## Scripts

```bash
# Instalar dependencias
npm install

# Servidor de desarrollo
npm run dev

# Build de producción
npm run build

# Vista previa del build
npm run preview
```

## Desplegar en Render (Static Site)

1. Sube el repositorio a GitHub.
2. En [Render](https://render.com), crea un nuevo **Static Site** vinculado al repositorio.
3. Configura:
   - **Build Command:** `npm install && npm run build`
   - **Publish Directory:** `dist`
   - **Environment Variable:** `NODE_VERSION` = `20`
4. Haz clic en **Deploy**. También puedes usar el archivo `render.yaml` incluido para un despliegue automático con Infrastructure as Code.

## Tecnologías

- Vue 3 (Composition API + `<script setup>`)
- Vite 8
- Tailwind CSS 3
- JetBrains Mono (Google Fonts)
