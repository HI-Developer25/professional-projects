# 🧰 Tech Stack — Gwadar Gymkhana Reciprocal Outreach Review

[← Back to project overview](./README.md)

| Layer | Technology | Why |
| --- | --- | --- |
| **Framework** | Nuxt 4 (`ssr: false`) | Nuxt's structure and tooling, built as a static SPA with no server to run |
| **Frontend** | Vue 3.5 (Composition API, `<script setup>`) | Simple, typed components and composables |
| **Language** | TypeScript 5 | Typed composables, components, and database row shapes |
| **Backend-as-a-service** | Supabase (`@supabase/supabase-js`) | Auth, database, and an auto-generated API in one managed service |
| **Database** | PostgreSQL 17 | RLS, column-level grants, and CHECK constraints keep data safe without a server |
| **Data API** | PostgREST (via Supabase) | No custom endpoints to write; nested selects load related data in one call |
| **Auth** | Supabase Auth (email + password) | Session-based access with automatic token refresh |
| **State** | Nuxt `useState` | Shared reactive state without an extra store library |
| **Styling** | Plain CSS (one hand-written file) | A small app does not need a CSS framework |
| **Map** | Inline SVG world map | Countries can be shaded from data with no map library |
| **Automation** | Scheduled Claude task | Researches clubs and inserts the daily batch of drafts into Supabase |
| **Build** | Vite 8 | Nuxt's fast build toolchain |
| **Quality** | `vue-tsc` / `nuxt typecheck` | Full type check across the app |
| **Database tooling** | Supabase CLI | Versioned migrations with `db push` and dry runs |

## Deployment target

Any static host (for example Netlify, Vercel, Cloudflare Pages, or nginx). `npm run generate` outputs static files; Supabase settings are passed as `NUXT_PUBLIC_*` variables at build time. Database changes are shipped separately with the Supabase CLI.

## Runtime targets

Node.js 20+ for building, PostgreSQL 17 on Supabase.

---
<sub>Part of the [Gwadar Gymkhana — Reciprocal Outreach Review](./README.md) case study.</sub>
