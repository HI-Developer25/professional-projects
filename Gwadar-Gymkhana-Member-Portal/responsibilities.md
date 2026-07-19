# ✅ Responsibilities — Gwadar Gymkhana Member Portal

[← Back to project overview](./README.md)

As sole developer on this project, from initial architecture to production operation:

## Architecture & backend-for-frontend

- Designed and implemented the entire Nitro-based BFF proxy layer, including the Sanctum cookie/CSRF contract with the external Laravel backend.
- Defined the server-route API surface consumed by the dashboard (auth, payments, letters, complaints, clubs, settings).

## Product features

- Built the OTP-based login flow, including the country-aware phone input and resend/paste handling.
- Built the dashboard home, dues/payment flow, streamed-PDF document views, bilingual introduction-letter requests, reciprocal-clubs directory, and complaints/inquiries flow.
- Implemented dark/light mode, a collapsible sidebar, command palette, and keyboard shortcuts.

## Design system

- Authored `DESIGN.md`, the single source of truth for colors, typography, spacing, and component conventions across the dashboard.

## Infrastructure & operations

- Configured CI (lint + typecheck gate) and CD (branch-based deploy to production/staging) in GitHub Actions.
- Set up PM2 process management for zero-downtime reloads on both environments.
- Manage ongoing maintenance and dependency hygiene for the live portal.

---
<sub>Part of the [Gwadar Gymkhana — Member Portal](./README.md) case study.</sub>
