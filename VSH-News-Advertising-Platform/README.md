<div align="center">

# 📺 VSH News — Advertising Platform

**Marketing and ad-sales web platform for a 24/7 Balochi-language satellite TV channel.**

[![Vue.js](https://img.shields.io/badge/Vue.js-3.5-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vite.dev)
[![Vue Router](https://img.shields.io/badge/Vue_Router-4-42B883?style=flat-square&logo=vuedotjs&logoColor=white)](https://router.vuejs.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Status](https://img.shields.io/badge/Status-Live%20in%20Production-success?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#-license--confidentiality)

🌐 **Live:** [vshnews.tv](https://vshnews.tv)

</div>

---

> **Confidentiality note**
> This project was developed for Visionary Group. Source code and internal infrastructure details are private. This case study describes the engineering work at a level appropriate for a public portfolio.

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Solution](#-solution)
- [My Role](#-my-role)
- [Tech Stack](#-tech-stack)
- [Architecture Overview](#-architecture-overview)
- [Key Features](#-key-features)
- [Technical Highlights](#-technical-highlights)
- [APIs & Integrations](#-apis--integrations)
- [Challenges & Solutions](#-challenges--solutions)
- [Business Impact](#-business-impact)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)
- [License & Confidentiality](#-license--confidentiality)

---

## 📖 Project Overview

| | |
| --- | --- |
| **Industry** | Media & Broadcasting |
| **My Role** | Developer |
| **Status** | 🟢 Live in production |

VSH News is a satellite TV channel operated by Visionary Group in Karachi, Pakistan. This project is the channel's public web platform: a fast, animated single-page application whose primary business goal is **advertising sales** — visitors browse tiered TV/social-media advertising packages, submit a lead through an international contact form, read the archived issues of the channel's print magazine, and jump straight to its YouTube live stream.

## 🎯 Business Problem

The channel needed a modern, conversion-focused web presence to sell advertising packages directly, capture and route sales leads into a CRM without manual handling, and give its print-magazine archive a permanent digital home — all without standing up a backend service, since the site itself carries no first-party data of its own.

## 💡 Solution

I built a 100% client-side single-page application — no bundled backend or database — that gets its dynamic behavior entirely from third-party integrations: a CRM webhook for lead delivery, YouTube for the live stream, and a flag-image CDN for the international phone selector. This kept the platform simple to host and deploy while still supporting a real, revenue-generating sales flow.

## 👤 My Role

Developer on the platform's public-facing SPA: the advertising-package pricing UI, the lead-capture form and its CRM integration, the magazine archive, and the CI/CD pipeline that deploys it.

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| **Framework** | Vue 3 (Composition API, `<script setup>`) |
| **Build tool** | Vite |
| **Routing** | Vue Router (HTML5 history mode) |
| **Styling** | Tailwind CSS |
| **HTTP client** | Axios |
| **SEO** | Reactive document-head management, per-route metadata |
| **Animation** | Lottie for animated live-stream indicators |
| **CI/CD** | GitHub Actions, SSH/rsync deploy to an Apache host |

## 🏗️ Architecture Overview

```
Vue app (SPA)
   │
   ├─▶ Pricing & lead-capture form ──▶ CRM webhook (lead delivery)
   ├─▶ Header "Live" indicator ──────▶ YouTube live stream
   ├─▶ Phone country selector ───────▶ Flag-image CDN
   └─▶ Magazine archive ─────────────▶ Static PDFs served from the app itself
```

There is no first-party API or authentication in this project — it's a public, unauthenticated marketing front-end whose only outbound data flow is the lead-capture webhook. Everything else (YouTube, WhatsApp, flag images) is a direct link or client-side call to a third-party service.

## ✨ Key Features

- **Tiered advertising packages** — multiple pricing tiers covering TV airtime, social posts, reels/shorts, and magazine placements, presented as animated pricing cards with a "Most Popular" highlight.
- **Lead-capture flow** — selecting a plan swaps the pricing grid for a pre-tagged contact form, with international phone input and inline validation, ending in a polished confirmation state.
- **Magazine archive** — a featured latest issue plus an archive of past monthly issues, opened directly in the browser's PDF viewer.
- **Live-stream shortcuts** — animated "Live" indicators linking straight to the channel's YouTube stream, plus WhatsApp contact CTAs.
- **SEO & PWA** — per-route metadata, automatic sitemap generation, and a installable PWA manifest.

## 🔍 Technical Highlights

- Built a fully client-side international phone-code selector (preferred countries surfaced first, full list beneath, CDN-served flag artwork) without any backend lookup.
- Designed the pricing-to-lead-capture transition as a single form component that swaps state rather than routing away, preserving the selected plan context end to end.
- Kept the entire application backend-free by design, routing all dynamic behavior through third-party webhooks and embeds rather than standing up infrastructure for a brochure-style site.

## 🔌 APIs & Integrations

- **CRM lead webhook** — plan selection and contact details are posted directly to a CRM's incoming-leads endpoint.
- **YouTube** — live-stream links throughout the header and mobile navigation.
- **WhatsApp** — direct-chat call-to-action links.
- **Flag image CDN** — country flags for the phone-number selector.

## 🧗 Challenges & Solutions

See [`challenges.md`](./challenges.md) for the full write-up.

## 📈 Business Impact

Gives the channel a self-serve advertising storefront that converts visitor interest directly into CRM leads, without requiring any backend infrastructure to operate or maintain.

## 🖼️ Screenshots

See [`screenshots.md`](./screenshots.md).

## 🔮 Future Improvements

- A pre-configured API client already exists in the codebase for a future first-party backend, if the platform's needs outgrow a fully static/third-party integration model.

## 📄 License & Confidentiality

This project was developed for **Visionary Group**. Source code and infrastructure configuration are private and belong to the organization; they are not included in this repository. The live product is public at [vshnews.tv](https://vshnews.tv).

See also: [`architecture.md`](./architecture.md) · [`tech-stack.md`](./tech-stack.md) · [`responsibilities.md`](./responsibilities.md) · [`challenges.md`](./challenges.md) · [`screenshots.md`](./screenshots.md)

---

<div align="center">
<sub>Case study — see the <a href="../README.md">portfolio index</a> for more projects.</sub>
</div>
