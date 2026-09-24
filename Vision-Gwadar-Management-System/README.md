<div align="center">

# 🏢 Vision Gwadar — Management System

**Back-office platform for a property developer — customer files, payment schedules, invoicing, recovery reporting, and the content behind the public website, all in one place.**

[![Laravel](https://img.shields.io/badge/Laravel-13-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![PHP](https://img.shields.io/badge/PHP-8.3-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net)
[![Vue](https://img.shields.io/badge/Vue-3-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![Inertia.js](https://img.shields.io/badge/Inertia.js-3-9553E9?style=flat-square)](https://inertiajs.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![PHPStan](https://img.shields.io/badge/PHPStan-level%207-1B5E20?style=flat-square)](https://phpstan.org)
[![Pest](https://img.shields.io/badge/Tests-Pest%204-56C02B?style=flat-square)](https://pestphp.com)
[![Status](https://img.shields.io/badge/Status-Live%20in%20Production-success?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#-license--confidentiality)

</div>

---

> **Confidentiality note**
> This project was developed for Visionary Group as a work made for hire. Source code, customer data, and infrastructure details are private and belong to the employer. This case study describes the engineering work at a level appropriate for a public portfolio.

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Solution](#-solution)
- [My Role](#-my-role)
- [Tech Stack](#-tech-stack)
- [Architecture Overview](#-architecture-overview)
- [Key Features](#-key-features)
- [Technical Highlights](#-technical-highlights)
- [Authentication & Security](#-authentication--security)
- [Challenges & Solutions](#-challenges--solutions)
- [Business Impact](#-business-impact)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)
- [License & Confidentiality](#-license--confidentiality)

---

## 📖 Project Overview

| | |
| --- | --- |
| **Industry** | Real Estate / Property Development |
| **Team Size** | Solo |
| **Duration** | Jul 2026 – Sep 2026 |
| **My Role** | Sole Developer (backend, frontend, database, CI/CD & deployment) |
| **Status** | 🟢 Live in production |

The Vision Gwadar Management System is the internal admin platform for a property development business. It keeps the customer register — who bought what, and on which payment plan — and everything that follows from it: the instalment schedule for each file, the invoices raised against it, the receipts issued when money arrives, and the monthly recovery report the accounts office uses to chase unpaid instalments.

The same app also manages the content on the company's public marketing website — payment plans, projects and plots, bank accounts, development photos, downloadable documents, and a Karachi-vs-Gwadar price comparison — and serves it to the website through a small read-only JSON API.

## 🎯 Business Problem

The accounts, sales, and marketing teams needed one reliable system for their daily work. Customer files, instalment schedules, invoices, and receipts had to stay in sync, and the accounts office needed a clear monthly view of who owed what so it could chase arrears. At the same time, the marketing team needed to update the public website's content without asking a developer for every change. Because the data is financial and personal, every screen had to be locked to the right people.

## 💡 Solution

I designed and built a Laravel 13 monolith with an Inertia.js + Vue 3 single-page frontend. There is no separate frontend to deploy and no hand-written API client: controllers return Inertia pages, and Laravel Wayfinder generates typed TypeScript route functions from the PHP routes, so the frontend never hardcodes a URL.

Access is controlled by a role plus **59 permission keys** across five groups, and **every route is gated by middleware** — hiding a button in the UI is never the real check. A small, separate JSON API feeds the public website, and a token-protected endpoint forwards website contact-form leads to the CRM (Privyr).

## 👤 My Role

Sole developer for the whole system: data model and migrations, backend logic, the Vue/TypeScript frontend, PDF and email output, the permission model, the test suite, and the CI/CD pipeline that deploys it to production and staging.

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| **Backend** | PHP 8.3 · Laravel 13 |
| **Frontend bridge** | Inertia.js 3 |
| **Frontend** | Vue 3.5 (Composition API) · TypeScript 5 |
| **UI** | shadcn-vue (on Reka UI) · Tailwind CSS 4 · TanStack Table |
| **Typed routing** | Laravel Wayfinder |
| **Auth** | Laravel Fortify · two-factor (TOTP) · passkeys (WebAuthn) |
| **Database** | MySQL (production) · SQLite (CI & tests) |
| **PDF** | DomPDF |
| **Queue / cache / session** | Database driver |
| **Quality** | Pest 4 · PHPStan (Larastan) level 7 · Pint · ESLint · Prettier |
| **CI/CD** | GitHub Actions → rsync/SSH to a Linux VPS |
| **Package managers** | Composer · pnpm |

See [`tech-stack.md`](./tech-stack.md) for the reasons behind each choice.

## 🏗️ Architecture Overview

```
Browser (Vue 3 SPA)
  │
  ├─ Inertia page visit ──► Laravel routes ──► middleware (auth, verified, permission:key)
  │                                              │
  │                                              ├─► Controllers ──► Models / Services
  │                                              └─► Inertia::render() ──► Vue page
  │
Public website
  └─ JSON request ────────► api routes ──────► middleware (website token, throttle)
                                                 └─► API controllers ──► JSON
```

A classic Laravel monolith with Inertia as the view layer. The back office and the public-website API live in the same app but are separated by their own routes and middleware — customer files, payments, and reports are **never** exposed through the API. See [`architecture.md`](./architecture.md) for the full breakdown.

## ✨ Key Features

- **Permission-aware dashboard** — collection figures for the month, register status, worklists (files owing the most, files not chased this month, lapsed schedules, failed payments, open invoices), a 12-month billed-vs-recovered trend, and collections by payment method. Panels a user can't access are not sent to the browser at all.
- **Customer register** — customer files with validated contact and property details, and an instalment schedule opened automatically with each file.
- **Invoicing** — an item catalogue, one invoice per file with line-item editing, invoice PDFs, and emailed invoices and receipts.
- **Payments register** — payments raised automatically by the backend; money that never arrived is marked *failed*, never deleted.
- **Recovery reporting** — a monthly report of what each file owes (carrying forward anything unpaid), recovery notices sent from the report and logged against it, and a total-recovery report across a date range with a chart and PDF export.
- **Website content management** — payment plans, projects and plots, bank accounts, documents, a photo gallery, and price comparisons, served to the public site over a read-only JSON API.
- **Lead relay** — website contact-form leads forwarded to the CRM through a token-protected, rate-limited endpoint.
- **Platform polish** — light/dark mode, saved sidebar state, toast notifications, and a responsive UI from ~320px up.

## 🔍 Technical Highlights

- **Backend is the real gate** — a role plus 59 permission keys, enforced by middleware on every route; admins pass through a single `Gate::before` hook. Adding a new permission needs no changes to the middleware, gate, or frontend helper.
- **Type safety end to end** — PHPStan at **level 7** on the backend, strict TypeScript and `vue-tsc` on the frontend, and Wayfinder-generated route functions so a renamed route breaks the build instead of a page.
- **Pluggable recovery notices** — reminders go through a channel interface and a queued job; `mail` works today, and WhatsApp can be added as a new channel without touching the report.
- **Records are kept, not deleted** — invoiced items are retired and failed payments are marked failed, so the financial history stays complete.
- **Tested** — 35 Pest feature and unit test files, organised to mirror the controllers, running on in-memory SQLite in CI.

## 🔐 Authentication & Security

- **No public sign-up** — accounts are created by administrators only.
- **Laravel Fortify** with two-factor authentication (TOTP + recovery codes), **passkeys (WebAuthn)**, password confirmation, and email verification.
- **Per-route permission middleware** — the UI's `can()` helper only hides things; the server always makes the decision.
- **Least-data dashboard** — panels a user is not allowed to see are `null` in the response, not just hidden.
- **Separated public API** — content endpoints are read-only; the lead endpoint needs a shared bearer token and is throttled to 30 requests per minute.

## 🧗 Challenges & Solutions

See [`challenges.md`](./challenges.md) for the full write-up. In short: the hardest parts were keeping schedules, invoices, payments, and receipts consistent with each other, and building a permission model strict enough for financial data but simple enough to extend.

## 📈 Business Impact

Gives the accounts, sales, and marketing teams one system for the full customer lifecycle — from opening a file to recovering the last instalment — and lets marketing update the public website's content without a developer or a deploy.

## 🖼️ Screenshots

See [`screenshots.md`](./screenshots.md). This app shows real customer and financial data, so any published screenshot must use sanitized demo data.

## 🔮 Future Improvements

- WhatsApp recovery notices through a new notice channel (planned).
- Continued growth of the reporting and dashboard modules.

## 📄 License & Confidentiality

This project was developed for **Visionary Group** as a work made for hire. Source code, customer data, and infrastructure configuration are private and belong to the employer; they are not included in this repository.

See also: [`architecture.md`](./architecture.md) · [`tech-stack.md`](./tech-stack.md) · [`responsibilities.md`](./responsibilities.md) · [`challenges.md`](./challenges.md) · [`screenshots.md`](./screenshots.md)

---

<div align="center">
<sub>Case study — see the <a href="../README.md">portfolio index</a> for more projects.</sub>
</div>
