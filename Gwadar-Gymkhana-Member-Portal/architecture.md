# 🏗️ Architecture — Gwadar Gymkhana Member Portal

[← Back to project overview](./README.md)

## Backend-for-Frontend (BFF) proxy

```
┌──────────────┐     /api/**      ┌──────────────────────┐   Sanctum session    ┌──────────────────┐
│              │  ───────────────▶│   Nuxt / Nitro (BFF)  │  ──────────────────▶ │  Laravel Backend │
│   Browser    │                  │  server routes        │   Cookie + XSRF      │  (external API)  │
│  (Vue app)   │◀───────────────  │  proxy layer          │  ◀────────────────── │                  │
└──────────────┘   Set-Cookie     └──────────────────────┘   JSON / PDF         └──────────────────┘
        │                                     │
        │                                     ├── main API   (member, payments, letters, complaints…)
        │                                     └── system API (payment gateway + reciprocal-clubs directory)
        ▼
  Payment gateway SSO (bank-hosted) ──▶ redirect back to /payment-status
```

The proxy layer handles the full Sanctum contract on the server, so no piece of frontend code ever needs to think about cookies or CSRF directly:

- **Forwards** the incoming cookie header (carries the session and XSRF token).
- **Replays** the XSRF token as a header on every mutating request.
- **Sets the origin/referer** to the frontend's own origin so Sanctum treats the call as stateful.
- **Relays `Set-Cookie`** back to the browser with the cookie's domain attribute stripped, so sessions bind correctly to the frontend's own origin rather than the backend's.
- **Re-throws backend errors** with their original status codes, so the client always sees a faithful failure reason.

## Rendering & state

- SSR-first: pages await their data fetches so content is present in the initial render, with cookies forwarded automatically during server-side rendering.
- Authentication state is held in lightweight reactive state (no external state-management library needed for this size of app).
- Components, composables, and utilities are auto-registered per Nuxt convention.

## Why a BFF instead of calling the backend directly

Calling Laravel directly from the browser would mean either exposing a bearer token to client-side JavaScript (a real XSS risk) or fighting cross-origin cookie restrictions from a different frontend domain. Proxying through the app's own server routes means the session cookie can be `httpOnly` and scoped to the frontend's own origin, while the backend still sees the correct Sanctum stateful-domain headers on every request.

---
<sub>Part of the [Gwadar Gymkhana — Member Portal](./README.md) case study.</sub>
