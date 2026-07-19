# 🧗 Challenges & Solutions — Gwadar Gymkhana Member Portal

[← Back to project overview](./README.md)

### Making cookie-based auth work across a BFF boundary

**Challenge:** Laravel Sanctum's stateful (cookie) auth expects the frontend and backend to cooperate closely on origins, CSRF tokens, and cookie domains — easy to get right in a same-origin monolith, much less obvious once a Nuxt BFF sits in between.

**Solution:** Built a dedicated proxy utility that forwards the incoming cookie header, replays the CSRF token as an outgoing header on mutating requests, sets the origin/referer to the frontend's own domain so Sanctum treats calls as stateful, and rewrites the `Set-Cookie` domain attribute so sessions bind to the frontend. The result: no auth token ever touches client-side JavaScript, and the browser only ever needs an `httpOnly` cookie.

### Bilingual, RTL-aware forms with cascading data

**Challenge:** The introduction-letter request flow needed to support both English and Urdu (right-to-left), while also cascading a country → city → club selection where each level's options depend on the previous one.

**Solution:** Built the form with a full RTL-aware toggle and wired the cascading selects to fetch dependently, with auto-calculated fees based on duration and included family members — all validated client-side with Zod before submission.

### Reusing a payment pattern safely in an authenticated context

**Challenge:** The dues-payment flow needed the same hosted-gateway redirect pattern used on the public site, but now inside an authenticated dashboard where a failed or tampered redirect shouldn't be able to affect another member's session.

**Solution:** The payment-status route is deliberately public and stateless — it only trusts what the backend's signed verification endpoint reports for that specific transaction, independent of whoever is currently logged in.

### Keeping a one-person codebase consistent over time

**Challenge:** With no second engineer to catch UI drift, small inconsistencies in spacing, color, or component usage compound quickly.

**Solution:** Wrote `DESIGN.md` early as the single source of truth for the design system, and made following it (plus passing lint/typecheck) a hard requirement before any UI change ships.

---
<sub>Part of the [Gwadar Gymkhana — Member Portal](./README.md) case study.</sub>
