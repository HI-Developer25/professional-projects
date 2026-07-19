<div align="center">

# 👋 Professional Projects — Hamza Razzaque

**A curated portfolio of production applications I've architected, built, and shipped as a full-stack software engineer.**

[![Full-Stack Engineer](https://img.shields.io/badge/Role-Full--Stack%20Software%20Engineer-2b6cb0?style=for-the-badge)](#-about)
[![Location](https://img.shields.io/badge/Based%20in-Karachi%2C%20Pakistan-informational?style=for-the-badge)](#-contact)
[![Status](https://img.shields.io/badge/Status-Actively%20Building-success?style=for-the-badge)](#-projects-overview)

[![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![Nuxt](https://img.shields.io/badge/Nuxt-00DC82?style=flat-square&logo=nuxtdotjs&logoColor=white)](https://nuxt.com)
[![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com)
[![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)](#-engineering-practices)
[![Linux](https://img.shields.io/badge/Linux%20VPS-FCC624?style=flat-square&logo=linux&logoColor=black)](#-devops--infrastructure)

</div>

---

## 📖 About

I'm a full-stack software engineer specializing in **Laravel** backends and **Vue.js / Nuxt.js** frontends, with hands-on ownership of the infrastructure, CI/CD, and DevOps that get those applications into production and keep them there. I currently work as the sole engineer behind a live, multi-application platform, owning everything from database design to server hardening.

This repository is **not a code archive** — it's a **portfolio of case studies**. Each folder documents one complete, real production application: the business problem it solves, the architecture behind it, the engineering decisions I made, and the outcomes it delivered.

## 🔒 Why These Repositories Are Private

Every project listed here was built during professional employment, for a real employer or client, and is running in production today. The source code, infrastructure configuration, and business data belong to those organizations and cannot be made public.

> This repository exists so that recruiters, hiring managers, and fellow engineers can understand **what I built and how I think**, without exposing any proprietary code, credentials, or confidential business information. Every diagram, snippet, and figure below is either already public-facing (the live products themselves) or has been generalized to remove anything sensitive.

## 🗂️ Navigation

| Section | Description |
| --- | --- |
| [📁 Projects Overview](#-projects-overview) | Table of every production application, at a glance |
| [🧰 Technology Summary](#-technology-summary) | Full stack across all projects |
| [🏗️ Architecture Overview](#-architecture-overview) | Recurring architectural patterns I reach for |
| [⚙️ Engineering Practices](#-engineering-practices) | How I build, test, and ship |
| [🚀 DevOps & Infrastructure](#-devops--infrastructure) | How these applications run in production |
| [🏆 Achievements](#-achievements) | Measurable outcomes |
| [🧩 Featured Skills](#-featured-skills) | Core competencies |
| [📬 Contact](#-contact) | Let's talk |

---

## 📁 Projects Overview

| # | Project | My Role | Type | Primary Stack | Status |
| :-: | --- | --- | --- | --- | :-: |
| 1 | **[Gwadar Gymkhana — Public Website](./Gwadar-Gymkhana-Website)** | Sole Developer | Marketing site + payments | Nuxt 4 · Laravel · Bank Alfalah APG | 🟢 Live |
| 2 | **[Gwadar Gymkhana — Member Portal](./Gwadar-Gymkhana-Member-Portal)** | Sole Developer | Member self-service dashboard | Nuxt 4 (BFF) · Laravel Sanctum | 🟢 Live |
| 3 | **[VSH News — Advertising Platform](./VSH-News-Advertising-Platform)** | Sole Developer | Marketing SPA + lead capture | Vue 3 · Vite · CRM integration | 🟢 Live |
| 4 | **[ERP & Logistics Systems](./ERP-Logistics-System)** | Backend Developer | Multi-module ERP | Laravel · Yii · CodeIgniter | ✅ Completed |

<details>
<summary><strong>📋 Quick project cards (click to expand)</strong></summary>
<br>

**🏛️ Gwadar Gymkhana — Public Website**
Server-rendered marketing site for a private members' club, with a full hosted-checkout payment integration (Bank Alfalah APG) and CRM-connected lead capture. SSR, zero-CLS rendering, and CMS-driven content throughout.

**👤 Gwadar Gymkhana — Member Portal**
A Backend-for-Frontend (BFF) dashboard where members log in with OTP, pay dues online, request bilingual introduction letters, and manage their account — architected so the browser never talks to the backend directly.

**📺 VSH News — Advertising Platform**
A fast, animated single-page application for a satellite TV channel's ad-sales business: tiered pricing packages, an international lead-capture form wired into a CRM, and a digital magazine archive.

**📦 ERP & Logistics Systems**
A set of ERP modules — inventory, POS, purchasing, sales, and courier tracking — built to run real day-to-day order volume for SME retail clients, with multi-courier API integration for shipment tracking.

</details>

---

## 🧰 Technology Summary

<table>
<tr>
<td valign="top" width="50%">

**Backend**

[![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat&logo=laravel&logoColor=white)](https://laravel.com)
[![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)](https://www.php.net)
[![Yii](https://img.shields.io/badge/Yii-005A9C?style=flat&logo=yii&logoColor=white)](https://www.yiiframework.com)
[![CodeIgniter](https://img.shields.io/badge/CodeIgniter-EE4623?style=flat&logo=codeigniter&logoColor=white)](https://codeigniter.com)
[![REST API](https://img.shields.io/badge/REST%20API-005571?style=flat&logo=fastapi&logoColor=white)](https://restfulapi.net)
[![Laravel Sanctum](https://img.shields.io/badge/Laravel%20Sanctum-FF2D20?style=flat&logo=laravel&logoColor=white)](https://laravel.com/docs/sanctum)

**Frontend**

[![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![Nuxt.js](https://img.shields.io/badge/Nuxt.js-00DC82?style=flat&logo=nuxtdotjs&logoColor=white)](https://nuxt.com)
[![Nuxt UI](https://img.shields.io/badge/Nuxt%20UI-00DC82?style=flat&logo=nuxtdotjs&logoColor=white)](https://ui.nuxt.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![GSAP](https://img.shields.io/badge/GSAP-88CE02?style=flat&logo=greensock&logoColor=black)](https://gsap.com)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)](https://vite.dev)

</td>
<td valign="top" width="50%">

**Data & Integrations**

[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)](https://www.mysql.com)
[![MSSQL](https://img.shields.io/badge/MSSQL-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)](https://www.microsoft.com/en-us/sql-server)
[![Zod](https://img.shields.io/badge/Zod-3E67B1?style=flat&logo=zod&logoColor=white)](https://zod.dev)

Payment gateways · CRM webhooks (Privyr) · courier tracking APIs · WordPress/Shopify integrations

**DevOps & Infrastructure**

[![Linux](https://img.shields.io/badge/Linux%20Administration-FCC624?style=flat&logo=linux&logoColor=black)](https://www.linux.org)
[![Apache](https://img.shields.io/badge/Apache%20Reverse%20Proxy-D22128?style=flat&logo=apache&logoColor=white)](https://httpd.apache.org)
[![PM2](https://img.shields.io/badge/PM2-2B037A?style=flat&logo=pm2&logoColor=white)](https://pm2.keymetrics.io)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat&logo=cloudflare&logoColor=white)](https://www.cloudflare.com)
[![Webuzo](https://img.shields.io/badge/Webuzo-2C3E50?style=flat)](https://webuzo.com)
[![Plesk](https://img.shields.io/badge/Plesk-52BBE6?style=flat&logo=plesk&logoColor=white)](https://www.plesk.com)

</td>
</tr>
</table>

---

## 🏗️ Architecture Overview

Across these projects, a few architectural patterns show up repeatedly — they're the defaults I reach for unless a project needs something else:

```
┌────────────────────────┐        ┌──────────────────────────┐
│   Nuxt / Vue Frontend    │  REST  │   Laravel REST API        │
│   SSR or BFF proxy layer │◄──────►│   (auth, data, payments)  │
└────────────────────────┘        └──────────────┬────────────┘
                                                    │
                          ┌─────────────────────────┼─────────────────────────┐
                          ▼                         ▼                         ▼
                 Payment Gateways           CRM / Lead Systems         Courier / 3rd-party APIs
                 (hosted checkout,          (lead forwarding,          (shipment tracking,
                  HMAC-verified redirects)   webhook delivery)          status sync)
```

- **SSR-first frontends** — Nuxt/Vue apps fetch data server-side so pages arrive fully rendered, SEO-ready, and hydration-safe.
- **Backend-for-Frontend (BFF) proxying** — for authenticated apps, the browser never talks to the API directly; a server layer forwards requests, manages session cookies, and keeps tokens off the client.
- **Signed, verifiable redirects** — anywhere a third-party payment gateway redirects a user back into an app, the return URL is signed (HMAC) and re-validated server-side before anything is shown to the user.
- **CMS-driven content** — marketing content (pricing, testimonials, announcements) is fetched from the backend at render time rather than hardcoded, so non-technical stakeholders can update it without a deploy.
- **Modular ERP domains** — larger systems are split into clear bounded modules (inventory, sales, purchasing, reporting) that share a common data layer but stay independently maintainable.

---

## ⚙️ Engineering Practices

- **Ownership across the stack** — for the projects where I'm the sole developer, I own frontend, backend, database design, infrastructure, CI/CD, and day-2 operations, not just feature code.
- **Environment-driven configuration** — no hardcoded secrets or endpoints; runtime config is injected through environment variables and validated at startup.
- **Typed, validated boundaries** — TypeScript on the frontend and schema validation (Zod) on form and API boundaries, so bad data fails fast and close to the source.
- **Zero-downtime deploys** — production releases use process managers (PM2) with reload strategies that don't drop in-flight requests.
- **Separate staging and production** — every active project has an isolated staging environment (often protected behind Cloudflare Access) for changes to be verified before they reach real users.
- **Security-conscious defaults** — session cookies are `httpOnly`, CSRF tokens are primed and replayed automatically, and redirect-based payment flows are cryptographically verified rather than trusted at face value.

## 🚀 DevOps & Infrastructure

| Concern | Approach |
| --- | --- |
| **CI/CD** | GitHub Actions pipelines per project — build, then deploy over SSH/rsync to a Linux VPS |
| **Process management** | PM2 ecosystem configs for SSR Node processes, with `startOrReload` for zero-downtime releases |
| **Reverse proxy & SSL** | Apache reverse proxy, Cloudflare for DNS/CDN/SSL and Zero Trust access on staging |
| **Environments** | Separate production and staging targets per project, driven from `main`/`dev` branches |
| **Panels & hosting** | Webuzo and Plesk for VPS/hosting administration |
| **Email infrastructure** | Self-hosted mail identities and webmail where managed services didn't cover business requirements |

---

## 🏆 Achievements

- Sole developer responsible for architecting, building, and operating a live, multi-application production platform from the ground up.
- Engineered a Laravel-backed media gallery API paired with a Vue 3 frontend, cutting perceived load time by roughly **50%**.
- Delivered 5+ ERP modules (inventory, invoicing, sales) across Laravel, Yii, and CodeIgniter, and integrated 4+ third-party courier APIs for real-time shipment tracking.
- Reworked POS inventory-sync logic, reducing stock discrepancies by roughly **50%** while the system processed **500+ daily orders** for SME retail clients with zero regression incidents.
- Maintained 3+ production WordPress/PHP sites with zero security incidents.

## 🧩 Featured Skills

<table>
<tr>
<td valign="top" width="33%">

**Full-Stack Architecture**
- Production-ready Laravel APIs
- SSR / SSG / CSR / hybrid rendering with Nuxt
- BFF proxy patterns & session security
- Real-time frontend/backend data sync

</td>
<td valign="top" width="33%">

**Integration Engineering**
- Payment gateway integrations (hosted checkout, 3DS, signed redirects)
- CRM lead-forwarding pipelines
- Courier / logistics API integrations
- WordPress & Shopify integrations

</td>
<td valign="top" width="33%">

**Production Operations**
- Linux VPS management & hardening
- CI/CD pipeline design (GitHub Actions)
- Zero-downtime deployment strategies
- Reverse proxy, DNS, CDN & SSL configuration

</td>
</tr>
</table>

---

## 📬 Contact

I'm always happy to talk about full-stack architecture, Laravel, Vue/Nuxt, or production engineering in general.

[![Email](https://img.shields.io/badge/Email-hamzarazzaque5%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:hamzarazzaque5@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-HI--Developer25-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/HI-Developer25)
[![Website](https://img.shields.io/badge/Live%20Project-gwadargymkhana.com.pk-2b6cb0?style=flat-square&logo=googlechrome&logoColor=white)](https://gwadargymkhana.com.pk)

<div align="center">
<sub>⭐ If this portfolio gives you a useful picture of how I build software, feel free to star the repo.</sub>
</div>
