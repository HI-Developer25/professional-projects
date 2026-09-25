# ✅ Responsibilities — Gwadar Gymkhana Reciprocal Outreach Review

[← Back to project overview](./README.md)

As sole developer on this project, from first version to daily use:

## Database & security

- Designed the 7-table PostgreSQL schema, with CHECK constraints and an `updated_at` trigger.
- Wrote the Row Level Security policies and the column-level grant that limits the dashboard to status and sent-time updates.
- Wrote the migrations and the one-off import that moved the original hard-coded drafts into the database.

## Frontend

- Rebuilt the first single-file HTML dashboard as a Nuxt 4 + Vue 3 + TypeScript SPA.
- Built the review workflow: status actions, optimistic updates with rollback, live counts, filters, and infinite scroll.
- Built the draft cards with one-tap copy, recipient source notes, and attachment reminders.
- Built the SVG world map with data-driven shading, marker dots, hover details, and a country list.
- Wrote all styling in one hand-written CSS file.

## Auth

- Set up Supabase Auth sign-in with session persistence, auto-refresh, and a clean sign-out.

## Automation

- Set up the scheduled Claude task that researches clubs and inserts 10 new drafts into Supabase each day, checking the master club list first.
- Documented the daily import process and the SQL each draft touches.

## Operations

- Set up static builds (`npm run generate`) and database deploys with the Supabase CLI.
- Maintain the app and the database for daily use.

---
<sub>Part of the [Gwadar Gymkhana — Reciprocal Outreach Review](./README.md) case study.</sub>
