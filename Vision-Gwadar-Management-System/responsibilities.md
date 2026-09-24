# ✅ Responsibilities — Vision Gwadar Management System

[← Back to project overview](./README.md)

As sole developer on this project, from first design to production operation:

## Data model & backend

- Designed the data model (21 Eloquent models, 40 migrations) for customer files, instalment schedules, invoices, receipts, payments, and website content.
- Built the business logic that keeps schedules, invoices, payments, and receipts in sync, including automatically raised payments and receipts.
- Built the monthly and total recovery reports, with carry-forward of unpaid amounts and PDF export.
- Built queued recovery notices behind a pluggable channel interface.

## Access control & security

- Designed the role + permission model (59 keys across five groups) and enforced it with middleware on every route.
- Set up Laravel Fortify with two-factor authentication, passkeys, password confirmation, and email verification.
- Built the token-protected, rate-limited lead endpoint and kept customer and financial data out of the public API.

## Frontend

- Built every screen in Vue 3 + TypeScript with Inertia, using shadcn-vue components and Tailwind CSS.
- Built the permission-aware dashboard, the registers, and the reports, all responsive from ~320px up.
- Added light/dark mode, saved sidebar state, and toast notifications.

## Website content & integrations

- Built the content-management screens and the read-only JSON API used by the public marketing website.
- Connected website contact-form leads to the CRM (Privyr).

## Quality & operations

- Wrote the Pest test suite (35 test files) and kept PHPStan at level 7.
- Set up the GitHub Actions pipeline: lint, type checks, static analysis, and tests, then automatic deploys to production (`main`) and staging (`dev`).
- Manage releases, migrations, and ongoing maintenance of the live system.

---
<sub>Part of the [Vision Gwadar — Management System](./README.md) case study.</sub>
