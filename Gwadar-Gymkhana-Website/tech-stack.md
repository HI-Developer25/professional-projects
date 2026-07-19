# 🧰 Tech Stack — Gwadar Gymkhana Public Website

[← Back to project overview](./README.md)

| Layer | Technology | Why |
| --- | --- | --- |
| **Framework** | Nuxt 4 (SSR) | Server-side rendering for SEO and first-paint content, file-based routing |
| **UI** | Vue 3 (Composition API) + TypeScript | Type-safe, maintainable component logic |
| **Styling** | Tailwind CSS with an HSL design-token theme | Consistent theming without hand-rolled CSS |
| **Motion** | GSAP + ScrollTrigger, Lenis smooth scroll | Cinematic, scroll-driven animation with accessibility fallbacks |
| **Carousels** | Swiper | Articles, testimonials, membership cards, galleries |
| **Backend API** | Laravel (separate service) | Content, payments, and lead-forwarding endpoints |
| **Payments** | Bank Alfalah Payment Gateway (APG) | Hosted checkout with 3D Secure, per State Bank of Pakistan policy |
| **CRM** | Privyr | Server-side lead forwarding for membership/contact enquiries |
| **Process management** | PM2 | Zero-downtime reloads for the Node SSR process |
| **Reverse proxy / CDN** | Apache + Cloudflare | SSL, DNS, caching, staging protection |
| **CI/CD** | GitHub Actions | Build → rsync deploy → PM2 reload, per branch |
| **Runtime** | Node.js 22 | Matches CI and production |

## Notable libraries & conventions

- Components are auto-imported per Nuxt convention.
- All data fetching goes through a dedicated service module plus `useAsyncData`, never ad-hoc fetch calls in components.
- New public runtime config always follows the `NUXT_PUBLIC_*` convention so it's explicit which values are safe to ship to the browser.

---
<sub>Part of the [Gwadar Gymkhana — Public Website](./README.md) case study.</sub>
