# 🏗️ Architecture — Gwadar Gymkhana Public Website

[← Back to project overview](./README.md)

## System diagram

```
┌─────────────────────────────┐        ┌──────────────────────────────┐
│   Nuxt 4 Frontend            │  REST  │   Laravel API backend        │
│   SSR on Node, PM2-managed   │◄──────►│   (separate repository)      │
│                              │        │                              │
│  pages/ ── components/       │        │  • Website content endpoints │
│     │          │             │        │  • /payments/initiate        │
│  services/ ◄── useAsyncData  │        │  • /payments/verify-redirect │
│     │                        │        │  • /leads/forward ───────────┼──► CRM
│  shared API client ($fetch)  │        │          │                   │
└─────────────────────────────┘        └──────────┼───────────────────┘
                                                   ▼
                                        Bank Payment Gateway
                                        (hosted checkout, 3D Secure)
```

## Layers

**Frontend (Nuxt 4 / Vue 3)**
Renders every public page server-side. A single shared API client, bound to the backend base URL at runtime, is the only way components reach the backend — there's no direct fetch scattered through the codebase. Content-fetching components go through service modules dedicated to one concern each: website content, payments, and lead forwarding.

**Backend (Laravel REST API)**
A separate service that owns all business data and every sensitive operation. The frontend never signs a payment request or talks to the CRM directly — it only calls the backend, which does that work and returns a result.

**Payment gateway integration**
A three-step handshake: the backend signs and initiates the payment, the browser is redirected to the gateway's own hosted checkout page (card data never reaches this application), and the gateway redirects back with a signed, expiring query string that the backend re-validates before the result is shown.

**Lead capture**
Membership-application and contact-enquiry submissions are relayed server-side to a CRM, so no CRM webhook URL or credentials exist anywhere in frontend code.

## Why this shape

- **Separating the frontend from the API** means the marketing site can be redeployed, cached, and scaled independently of the systems that handle money and leads.
- **Routing all sensitive operations through the backend** keeps the attack surface on the frontend limited to "render what the API says happened" — there is nothing for a browser-side attacker to forge that would change a payment outcome.
- **CMS-driven content** means the club's staff can update pricing, testimonials, and development photos without needing a code change or deployment.

## Rendering & performance architecture

- SSR on every route via `useAsyncData`, so first paint already contains real content.
- Server-resolved layout values (header height, banner visibility) to guarantee zero layout shift on load.
- Client-only plugins (animation libraries) are loaded via dynamic import so they never block SSR or add to the initial payload unnecessarily.

---
<sub>Part of the [Gwadar Gymkhana — Public Website](./README.md) case study.</sub>
