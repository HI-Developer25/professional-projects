# 🧰 Tech Stack — VSH News Advertising Platform

[← Back to project overview](./README.md)

| Layer | Technology | Notes |
| --- | --- | --- |
| **Framework** | Vue 3 (Composition API, `<script setup>`) | No TypeScript in this codebase — plain JavaScript (ES modules) |
| **Build tool** | Vite | Dev server, bundling, custom asset handling for Lottie files |
| **Routing** | Vue Router (HTML5 history mode) | Nested layout routes with per-route SEO metadata |
| **Styling** | Tailwind CSS + PostCSS/Autoprefixer | Utility-first styling, custom theme + keyframe animations |
| **HTTP client** | Axios | Lead submission to the CRM webhook |
| **Head / SEO** | Reactive document-head library | Per-route title/description, Open Graph & Twitter meta |
| **Animation** | Lottie (`.lottie` files) | Animated "Live" stream indicators |
| **Icons** | Lucide icon set | Consistent SVG iconography |
| **Sitemap** | Build-time sitemap plugin | Generates `sitemap.xml` on every production build |
| **CI/CD** | GitHub Actions + SSH/rsync | Deploys the static build to an Apache-hosted server |

There is intentionally **no Laravel/PHP, Nuxt, TypeScript, or database** in this project — it's a stand-alone Vue SPA, reflecting the actual scope of what the platform needs.

---
<sub>Part of the [VSH News — Advertising Platform](./README.md) case study.</sub>
