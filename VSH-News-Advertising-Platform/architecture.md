# 🏗️ Architecture — VSH News Advertising Platform

[← Back to project overview](./README.md)

## System diagram

```
Vue 3 SPA (Vite)
   │
   ├── Pricing view ──▶ Lead-capture form ──▶ CRM webhook (POST)
   ├── Header / mobile nav ──▶ YouTube live stream
   ├── Phone country selector ──▶ Flag-image CDN
   ├── Magazine archive ──▶ Static PDFs bundled with the app
   └── Footer ──▶ WhatsApp deep links, Google Maps links
```

## Key design decisions

- **No first-party backend.** The site's entire purpose is to sell advertising and capture leads; every dynamic behavior is delivered through third-party integrations rather than custom infrastructure, which keeps hosting and maintenance minimal for a brochure-style marketing site.
- **Layout-nested routing.** A single root component renders a router outlet; a shared layout wraps every page with a common header/footer and injects per-route SEO metadata, so new pages only need to define their content and a route entry.
- **Lightweight state.** No global state-management library — local component state is enough for a site with no authentication and no cross-page shared data.
- **Static-first assets.** Images are processed and optimized through the build tool; PDFs and favicons are served as-is from the public folder without any processing.

## Why no backend

Standing up and maintaining a database and API for a site whose only "write" operation is a lead-capture form would have added ongoing operational cost for no real benefit — a CRM webhook does that job directly. This keeps the entire platform's attack surface and hosting footprint to a single static build.

---
<sub>Part of the [VSH News — Advertising Platform](./README.md) case study.</sub>
