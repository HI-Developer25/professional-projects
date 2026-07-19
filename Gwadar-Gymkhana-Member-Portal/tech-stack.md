# 🧰 Tech Stack — Gwadar Gymkhana Member Portal

[← Back to project overview](./README.md)

| Layer | Technology | Why |
| --- | --- | --- |
| **Framework** | Nuxt 4 (SSR), Vue 3 Composition API | SSR + a built-in server layer that doubles as the BFF |
| **Language** | TypeScript (strict) | Typed props, composables, and API contracts end to end |
| **UI** | Nuxt UI v4 + Tailwind CSS v4 | A consistent, accessible component library over hand-rolled UI |
| **Server / BFF** | Nitro server routes | Same-repo proxy layer, no separate BFF service to deploy |
| **Validation** | Zod | Shared validation between forms and API boundaries |
| **Tables** | TanStack Table (via Nuxt UI) | Sorting/filtering for complaints and installment tables |
| **Forms** | International phone input component | Country-aware phone entry for OTP login |
| **Auth (external)** | Laravel + Sanctum | Cookie/session auth, no client-side tokens |
| **Quality** | ESLint, Prettier, strict typecheck | CI blocks merges on lint/typecheck failure |
| **CI/CD** | GitHub Actions, rsync/SSH, PM2 | Branch-based deploy to production/staging with zero-downtime reloads |
| **Package manager** | pnpm | Faster installs, strict dependency resolution |
| **Dependency hygiene** | Automated dependency-update tooling (Nuxt preset) | Keeps dependencies and the lockfile current automatically |

## Runtime targets

Node.js 22, pnpm 10+.

---
<sub>Part of the [Gwadar Gymkhana — Member Portal](./README.md) case study.</sub>
