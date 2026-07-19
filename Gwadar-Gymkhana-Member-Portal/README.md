<div align="center">

# 👤 Gwadar Gymkhana — Member Portal

**Secure, mobile-friendly self-service dashboard for club members — sign in with OTP, pay dues, request letters, and manage an account entirely online.**

[![Nuxt](https://img.shields.io/badge/Nuxt-4-00DC82?style=flat-square&logo=nuxt&logoColor=white)](https://nuxt.com)
[![Vue](https://img.shields.io/badge/Vue-3-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Nuxt UI](https://img.shields.io/badge/Nuxt%20UI-4-00DC82?style=flat-square&logo=nuxt&logoColor=white)](https://ui.nuxt.com)
[![Laravel Sanctum](https://img.shields.io/badge/Backend-Laravel%20Sanctum-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com/docs/sanctum)
[![Status](https://img.shields.io/badge/Status-Live%20in%20Production-success?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#-license--confidentiality)

</div>

---

> **Confidentiality note**
> This project was developed during professional employment with Gwadar Gymkhana. Source code, backend infrastructure, and member data are private and belong to the employer. This case study describes the engineering work at a level appropriate for a public portfolio.

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
| **Industry** | Hospitality / Private Membership Clubs |
| **Team Size** | Solo |
| **Duration** | ~2 months to first release |
| **My Role** | Sole Developer (frontend, BFF layer, infrastructure & DevOps) |
| **Status** | 🟢 Live in production |

The Member Portal gives Gwadar Gymkhana members a secure, mobile-friendly place to handle everything about their membership online — signing in with just a phone number and an OTP, paying dues, requesting bilingual introduction letters, browsing the reciprocal-club network, and raising complaints — from one responsive dashboard.

## 🎯 Business Problem

Members previously had no self-service way to check their dues, pay online, or request documentation like introduction letters — everything ran through manual, in-person or phone-based processes. The club needed a secure digital front door for members that could handle payments and sensitive account actions without a large backend team to maintain it.

## 💡 Solution

I designed and built a Nuxt 4 application that is deliberately more than a UI — it's a **Backend-for-Frontend (BFF)**. Every request from the browser goes through the app's own server routes, which proxy to an external Laravel + Sanctum backend. That keeps session cookies `httpOnly`, hides backend URLs from the browser entirely, and centralizes CSRF and error handling in one place instead of scattering auth logic across the frontend.

## 👤 My Role

Sole developer for the entire portal: the BFF proxy layer, every dashboard feature, the design system it's built on, and the CI/CD and infrastructure it deploys to.

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| **Framework** | Nuxt 4 (SSR) · Vue 3 Composition API · TypeScript (strict) |
| **UI** | Nuxt UI v4 · Tailwind CSS v4 · custom brand theme |
| **Server / BFF** | Nitro server routes proxying to Laravel |
| **Validation** | Zod |
| **Auth** | Laravel Sanctum (cookie/session-based, OTP login) |
| **Tables** | TanStack Table (via Nuxt UI) |
| **CI/CD** | GitHub Actions · rsync/SSH · PM2 |
| **Package manager** | pnpm |

## 🏗️ Architecture Overview

```
┌──────────────┐     /api/**      ┌──────────────────────┐   Sanctum session    ┌──────────────────┐
│              │  ───────────────▶│   Nuxt / Nitro (BFF)  │  ──────────────────▶ │  Laravel Backend │
│   Browser    │                  │  server routes        │   Cookie + XSRF      │  (external API)  │
│  (Vue app)   │◀───────────────  │  proxy layer          │  ◀────────────────── │                  │
└──────────────┘   Set-Cookie     └──────────────────────┘   JSON / PDF         └──────────────────┘
```

The browser never talks to Laravel directly. Every call goes to the portal's own Nitro routes, which forward the request with the correct Sanctum headers and relay cookies back — including replaying the CSRF token as a header on every mutating request, and stripping the cookie `Domain` attribute so sessions bind correctly to the frontend's own origin. See [`architecture.md`](./architecture.md) for the full breakdown.

## ✨ Key Features

- **Passwordless login** — phone number + 6-digit OTP, fully session-based.
- **Dashboard** — membership summary, family panel, current dues with one-click Pay Now.
- **Payments** — automatic bank-charge calculation and a hosted-gateway redirect for dues.
- **Streamed documents** — payment schedule and club rules & by-laws served as in-app PDFs.
- **Bilingual introduction letters** — English/Urdu (RTL-aware) request flow with cascading country → city → club selection and auto-calculated fees.
- **Reciprocal clubs directory** — grouped by country, with live search.
- **Complaints & inquiries** — categorized submissions with image attachments and canned FAQ answers for non-actionable topics.
- **Platform polish** — dark/light mode, collapsible sidebar, command palette, keyboard shortcuts.

## 🔍 Technical Highlights

- Architected the BFF proxy layer from scratch, including the Sanctum cookie/CSRF contract — a non-trivial integration since the frontend and backend live on different origins.
- Built a fully bilingual, RTL-aware form flow (introduction letters) with cascading, dependently-loaded dropdowns.
- Implemented the same hosted-payment-gateway redirect pattern used on the public website, reused here for dues payments.
- Authored a dedicated design-system document (`DESIGN.md`) as the single source of truth for UI consistency across the whole dashboard.

## 🔐 Authentication & Security

- **Phone + OTP login**, verified server-side, with no client-readable auth token.
- **Session-based auth via Laravel Sanctum** — the session lives entirely in an `httpOnly` cookie.
- **Automatic CSRF priming** — the app fetches Sanctum's CSRF cookie before any mutating request and replays it as a header.
- **Global route guard** — unauthenticated visitors are redirected to login; the session is resolved once per app load, safely on both server and client.

## 🧗 Challenges & Solutions

See [`challenges.md`](./challenges.md) for the full write-up. In short: the hardest problem was making cross-origin, cookie-based Sanctum auth work cleanly through a BFF without ever exposing a token to client-side JavaScript.

## 📈 Business Impact

Gives members a secure self-service channel for dues payments and account actions that previously required manual, offline processes — while keeping all authentication and payment logic off the client entirely.

## 🖼️ Screenshots

See [`screenshots.md`](./screenshots.md) — this project uses sanitized demo data for any published screenshots, since real screens would expose member information.

## 🔮 Future Improvements

- Continued expansion of self-service features alongside the [Public Website](../Gwadar-Gymkhana-Website).
- Ongoing design-system refinement via `DESIGN.md`.

## 📄 License & Confidentiality

This project was developed during professional employment with **Gwadar Gymkhana** and is a work made for hire. Source code, member data, and infrastructure configuration are private and belong to the employer; they are not included in this repository. It builds on top of an open-source Nuxt UI dashboard template (MIT-licensed); all club-specific code, content, and branding remain the property of Gwadar Gymkhana.

See also: [`architecture.md`](./architecture.md) · [`tech-stack.md`](./tech-stack.md) · [`responsibilities.md`](./responsibilities.md) · [`challenges.md`](./challenges.md) · [`screenshots.md`](./screenshots.md)

---

<div align="center">
<sub>Case study — see the <a href="../README.md">portfolio index</a> for more projects.</sub>
</div>
