<div align="center">

# 🏛️ Gwadar Gymkhana — Public Website

**Server-rendered marketing website and payments portal for Balochistan's premier private members' club.**

[![Nuxt](https://img.shields.io/badge/Nuxt_4-00DC82?style=flat-square&logo=nuxt&logoColor=white)](https://nuxt.com)
[![Vue.js](https://img.shields.io/badge/Vue_3-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![GSAP](https://img.shields.io/badge/GSAP-88CE02?style=flat-square&logo=greensock&logoColor=black)](https://gsap.com)
[![Status](https://img.shields.io/badge/Status-Live%20in%20Production-success?style=flat-square)](https://gwadargymkhana.com.pk)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#-license--confidentiality)

🌐 **Live:** [gwadargymkhana.com.pk](https://gwadargymkhana.com.pk)

</div>

---

> **Confidentiality note**
> This project was developed during professional employment with Gwadar Gymkhana. Source code, backend infrastructure, and credentials are private and belong to the employer. This case study describes the engineering work at a level appropriate for a public portfolio; the live site itself is public.

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Solution](#-solution)
- [My Role](#-my-role)
- [Tech Stack](#-tech-stack)
- [Architecture Overview](#-architecture-overview)
- [Key Features](#-key-features)
- [Technical Highlights](#-technical-highlights)
- [Performance & SEO](#-performance--seo)
- [APIs & Integrations](#-apis--integrations)
- [Security](#-security)
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
| **My Role** | Sole Developer (frontend, backend API, infrastructure & DevOps) |
| **Status** | 🟢 Live in production |

Gwadar Gymkhana is a private members' club at Gwadar Smart Port City, Pakistan. This project is the club's official public website — a server-side-rendered marketing site that presents its facilities, membership tiers, reciprocal club network, and construction progress, and handles two real transactional flows end to end: **online membership payments** and **lead capture** for membership applications.

## 🎯 Business Problem

A premium private club needed a public digital presence that matched the quality of the physical experience it was selling — one that could clearly present membership tiers and facilities, accept real online payments securely, and convert visitor interest into qualified membership leads, all without a large engineering team behind it.

## 💡 Solution

I built and deployed a complete SSR web platform from the ground up: a Nuxt 4 frontend for every public-facing page, backed by a Laravel REST API that serves all CMS-driven content (testimonials, pricing, articles, development photos). On top of that, I integrated a bank payment gateway for membership dues and a CRM pipeline for lead capture — then designed, configured, and now operate the production and staging infrastructure the whole platform runs on.

## 👤 My Role

As sole developer, I owned the entire lifecycle: UI/UX implementation, the Laravel API contract, the payment and CRM integrations, and the Linux VPS infrastructure, CI/CD, and DNS/SSL configuration the site runs on in production.

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| **Frontend** | Nuxt 4 (SSR) · Vue 3 · TypeScript · Tailwind CSS · GSAP · Swiper · Lenis smooth scroll |
| **Backend** | Laravel REST API (separate service) |
| **Payments** | Bank Alfalah Payment Gateway (APG) — Alfa Wallet, Raast QR, credit/debit card |
| **CRM** | Privyr (server-side lead forwarding) |
| **Infrastructure** | Linux VPS · Apache reverse proxy · PM2 · Cloudflare |
| **CI/CD** | GitHub Actions (build → rsync deploy → zero-downtime PM2 reload) |

## 🏗️ Architecture Overview

```
┌─────────────────────────────┐        ┌──────────────────────────────┐
│   Nuxt 4 Frontend (this)    │  REST  │   Laravel API backend        │
│   SSR on Node, managed by   │◄──────►│   (separate repository)      │
│   PM2 behind Apache/Cloudflare│      │                              │
│                             │        │  • Website content endpoints │
│                             │        │  • Payment initiate/verify   │
│                             │        │  • Lead forwarding ──────────┼──► CRM
└─────────────────────────────┘        └──────────────┬───────────────┘
                                                       ▼
                                        Bank Payment Gateway
                                        (hosted checkout, 3D Secure)
```

The frontend never talks to the payment gateway or CRM directly — every sensitive operation is initiated and verified server-side by the Laravel API, with the frontend only rendering the result. Content that changes often (pricing, testimonials, announcements, development photos) is fetched from the API at render time rather than hardcoded, so it can be updated without a frontend deploy.

## ✨ Key Features

- **Full public site** — home, about, membership tiers, a multi-step membership application form with an international phone-code selector, and a dedicated "Club" section covering facilities, privileges, partner offers, reciprocal clubs, and live development progress.
- **Online payments** — a pay-online flow supporting Alfa Wallet, Raast QR, and card payments, with automatic bank-charge calculation before submission.
- **CMS-driven content** — pricing, testimonials, articles, announcements, and construction-progress photos are all editable from the backend without a redeploy.
- **Motion & UX** — GSAP + ScrollTrigger animation toolkit with automatic cleanup and `prefers-reduced-motion` support, Lenis smooth scrolling, and Swiper carousels throughout.
- **Development tracker** — animated construction-progress bars and a paginated, keyboard-navigable photo gallery documenting the club's build-out.

## 🔍 Technical Highlights

- Built a reusable GSAP + ScrollTrigger composable that powers every scroll animation on the site (reveal, parallax, fade, draw) with automatic cleanup on route change.
- Implemented the full hosted-checkout handshake for the bank payment gateway: a backend-signed request, a hidden auto-submitting form to the gateway's SSO page, and a signed, expiring redirect back into the app.
- Engineered the site for **zero cumulative layout shift** — header height, image aspect ratios, and banner visibility are all resolved server-side before the page ever reaches the browser.

## ⚡ Performance & SEO

- Full SSR on every page via `useAsyncData`, with no client-only content flashes.
- Responsive `<picture>` sources with WebP + fallback formats, `fetchpriority` hints, and lazy loading.
- Self-hosted variable fonts with preloading.
- Per-page metadata (Open Graph, Twitter cards, canonical URLs), JSON-LD organization schema, sitemap, and a PWA manifest.

## 🔌 APIs & Integrations

- **Bank Alfalah Payment Gateway (APG)** — hosted checkout with 3D Secure; card data never touches this application.
- **Privyr CRM** — membership and contact enquiries are forwarded server-side, so no CRM credentials exist in the frontend.
- **Laravel content API** — testimonials, pricing, articles, reciprocal clubs, privileges, and development photos, all fetched server-side.

## 🔐 Security

This is a public marketing site with no user login, so the security surface is entirely about the payment flow: the redirect back from the gateway carries an **HMAC-signed, expiring** query string that the backend re-validates before any success/failure detail is rendered — tampered or expired links are rejected outright.

## 🧗 Challenges & Solutions

| Challenge | Solution |
| --- | --- |
| Integrating a bank-hosted payment checkout without ever handling raw card data | Delegated all card entry to the gateway's hosted page; the app only builds the signed handshake and verifies the signed return redirect |
| Avoiding layout shift on a content-heavy, animation-rich site | Resolved header height and image dimensions server-side, and gated all scroll animations behind `prefers-reduced-motion` checks |
| Keeping marketing content editable by non-technical staff | Moved every piece of dynamic content (pricing, testimonials, photos, announcements) behind CMS-style API endpoints instead of hardcoding it |

## 📈 Business Impact

Serves as the club's official public web presence and its only online channel for membership payments and lead capture, running in production with a separate staging environment for safe iteration.

## 🖼️ Screenshots

See [`screenshots.md`](./screenshots.md) for planned visual documentation of this project.

## 🔮 Future Improvements

- Expanding the digital platform with additional business modules alongside the companion [Member Portal](../Gwadar-Gymkhana-Member-Portal).
- Continued performance and SEO refinement as content volume grows.

## 📄 License & Confidentiality

This project was developed during professional employment with **Gwadar Gymkhana** and is a work made for hire. Source code, infrastructure configuration, and business content are private and belong to the employer; they are not included in this repository. The live product is public at [gwadargymkhana.com.pk](https://gwadargymkhana.com.pk).

See also: [`architecture.md`](./architecture.md) · [`tech-stack.md`](./tech-stack.md) · [`responsibilities.md`](./responsibilities.md) · [`challenges.md`](./challenges.md) · [`screenshots.md`](./screenshots.md)

---

<div align="center">
<sub>Case study — see the <a href="../README.md">portfolio index</a> for more projects.</sub>
</div>
