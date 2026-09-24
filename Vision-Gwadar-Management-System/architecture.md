# 🏗️ Architecture — Vision Gwadar Management System

[← Back to project overview](./README.md)

## Laravel monolith with an Inertia-driven Vue frontend

```
Browser (Vue 3 SPA)
  │
  ├─ Inertia page visit ──► routes/*.php ──► middleware (auth, verified, permission:key)
  │                                            │
  │                                            ├─► Controllers ──► Models / Services
  │                                            └─► Inertia::render() ──► pages/*.vue
  │
Public marketing website
  └─ JSON request ────────► routes/api.php ─► middleware (website token, throttle)
                                               └─► Api controllers ──► JSON
```

There is no separate frontend build to deploy and no client-side API client. Controllers return Inertia pages, and **Laravel Wayfinder** generates typed TypeScript functions from the PHP route definitions, so the frontend never hardcodes a URL. If a route is renamed or removed, the TypeScript build fails instead of a page breaking in production.

## Code organisation

- **Controllers are grouped by business area** — `Customers`, `Payments`, `Reports`, `Content`, `Admin`, `Settings`, and `Api` — and each area has its own route file. The Vue pages and the test folders mirror the same structure, so it is easy to find everything for one feature.
- **Services hold the heavier logic** — dashboard assembly, report building, schedule PDFs, and recovery notices live in service classes, not controllers.
- **Contracts mark the swappable parts** — for example, a `Payable` interface for anything a payment can settle, and a `RecoveryNoticeChannel` interface for how reminders are delivered.
- **Enums model status** — payment, invoice-payment, schedule, and recovery-notice states are PHP enums, not loose strings.

## Authorization model

```
User ── role: admin | user
  │
  └── permissions (key, label, group) ── via pivot ── e.g. reports.view

Route ──► middleware('permission:reports.view') ──► Gate::before → admin passes
                                                  └► otherwise: key must be granted
```

- **Admins** pass every check through a single `Gate::before` hook.
- **Users** can only do what they have been granted — 59 keys across five groups.
- The user's permission keys are shared with the frontend on every request, and a global `can()` helper hides UI the user can't use. This is **cosmetic only** — the route middleware is the real check.
- Adding a permission means adding one row to an idempotent seeder and gating the route. No changes to the middleware, the gate, or the frontend helper.

## Background work and output

- **Recovery notices** are sent from the recovery report, pushed onto a queue (`SendRecoveryNoticeJob`), and logged against the report row. The delivery channel is chosen by config — `mail` today, WhatsApp planned.
- **PDFs** (schedules, invoices, receipts, and both recovery reports) are rendered from Blade templates with DomPDF.
- **Emails** for invoices, receipts, and recovery notices use Laravel mailables.

## Public website API

- Read-only content endpoints (payment plans, projects, bank accounts, documents, photo gallery, price comparisons) return display-ready JSON for the marketing site.
- A lead endpoint forwards contact-form enquiries to the CRM. It needs a shared bearer token and is throttled to 30 requests per minute.
- Customer files, payments, and reports are **never** exposed through the API — they stay behind session auth and permission middleware.

## Why a monolith instead of a separate API + SPA

This is an internal tool used by one company's staff. A single Laravel app with Inertia gives SPA-style navigation without the cost of a second codebase, a second deploy, token handling in the browser, or keeping two sets of types in sync. Session auth stays simple, and Wayfinder gives the frontend typed routes for free.

---
<sub>Part of the [Vision Gwadar — Management System](./README.md) case study.</sub>
