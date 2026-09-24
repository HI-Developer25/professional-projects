# 🧰 Tech Stack — Vision Gwadar Management System

[← Back to project overview](./README.md)

| Layer | Technology | Why |
| --- | --- | --- |
| **Backend** | PHP 8.3, Laravel 13 | Mature framework with auth, queues, mail, and PDFs covered out of the box |
| **Frontend bridge** | Inertia.js 3 | SPA feel with server-side routing — no separate API or frontend deploy |
| **Frontend** | Vue 3.5 (Composition API, `<script setup>`), TypeScript 5 | Typed components and composables end to end |
| **UI components** | shadcn-vue (on Reka UI), Lucide icons | Accessible, consistent primitives instead of hand-rolled UI |
| **Styling** | Tailwind CSS 4 | Fast, consistent styling and a responsive layout from ~320px up |
| **Tables** | TanStack Table | Sorting and filtering for large registers and reports |
| **Typed routing** | Laravel Wayfinder | TypeScript route functions generated from PHP routes — no hardcoded URLs |
| **Auth** | Laravel Fortify, passkeys (WebAuthn) | 2FA, passkeys, password confirmation, and email verification |
| **Database** | MySQL (production), SQLite (CI & tests) | Real database in production, fast in-memory database for tests |
| **PDF** | DomPDF | Schedules, invoices, receipts, and reports from Blade templates |
| **Queue / cache / session** | Database driver | Simple to run on a single VPS without extra services |
| **Testing** | Pest 4, Mockery, Faker | Readable feature tests that mirror the controllers |
| **Static analysis** | PHPStan via Larastan — level 7 | Catches type bugs before they reach production |
| **Code style** | Laravel Pint, ESLint 9, Prettier 3 | One consistent style for PHP, TypeScript, and Vue |
| **CI/CD** | GitHub Actions, rsync/SSH | Branch-based deploys to production and staging after checks pass |
| **Package managers** | Composer 2, pnpm | Fast installs and a strict lockfile |

## Runtime targets

PHP 8.3, Node.js 22, pnpm 11, MySQL 8.

---
<sub>Part of the [Vision Gwadar — Management System](./README.md) case study.</sub>
