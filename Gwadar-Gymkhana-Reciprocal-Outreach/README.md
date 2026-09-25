<div align="center">

# 🌍 Gwadar Gymkhana — Reciprocal Outreach Review

**A daily review dashboard for the club's reciprocal-club outreach — check each drafted email, approve or reject it, track what was sent, and see on a world map where the club's invitations have reached.**

[![Nuxt](https://img.shields.io/badge/Nuxt-4.5-00DC82?style=flat-square&logo=nuxt&logoColor=white)](https://nuxt.com)
[![Vue](https://img.shields.io/badge/Vue-3.5-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-Auth%20%2B%20Postgres-3ECF8E?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![Vite](https://img.shields.io/badge/Vite-8-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vite.dev)
[![Automation](https://img.shields.io/badge/Daily%20import-Claude%20schedule-D97757?style=flat-square&logo=claude&logoColor=white)](#-technical-highlights)
[![Status](https://img.shields.io/badge/Status-Live-success?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#-license--confidentiality)

</div>

---

> **Confidentiality note**
> This project was developed for Visionary Group (for Gwadar Gymkhana) as a work made for hire. Source code, club contact data, and infrastructure details are private and belong to the employer. This case study describes the engineering work at a level that is safe for a public portfolio.

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Solution](#-solution)
- [My Role](#-my-role)
- [Tech Stack](#-tech-stack)
- [Architecture Overview](#-architecture-overview)
- [Key Features](#-key-features)
- [Technical Highlights](#-technical-highlights)
- [Authentication & Security](#-authentication--security)
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
| **Duration** | 4 days (about 6.5 hours a day, alongside other projects) |
| **My Role** | Sole Developer (frontend, database design, security model, automation) |
| **Status** | 🟢 Live (internal tool) |

Gwadar Gymkhana is growing its **reciprocal affiliation network** — a list of partner clubs around the world whose members can use each other's facilities. To grow it, the club sends invitation emails to well-known clubs in other countries.

Every day, a new batch of outreach emails is drafted. This app is where a reciprocal officer reviews them: read each email, approve or reject it, send it by hand from the club mailbox, and mark it as sent. A world map shows which countries the club has already reached.

## 🎯 Business Problem

Outreach emails go to important clubs, so each one must be checked by a person before it is sent. The club also needed to make sure the **same club is never contacted twice**, and that the record of what was sent is correct on every reviewer's device. A spreadsheet or a single HTML page could not do this safely once the list started to grow every day.

## 💡 Solution

I built a **client-only single-page app** with Nuxt 4 (SSR turned off) that talks directly to a **Supabase** Postgres database. There is **no application server** and no custom API.

Because there is no server, all security lives **inside the database** — Row Level Security and column-level grants. The dashboard can change only two things: a draft's **status** and its **sent time**. Everything else (clubs, email text, recipients) is written only by the daily import.

The daily import is automated with a **scheduled Claude task**. Each day it researches clubs, collects the outreach data, and inserts **10 new drafts** into Supabase — checking the master club list first so no club is drafted twice. The reviewer only has to press **Refresh**.

> **Sending is manual on purpose.** The app never sends email. A person approves a draft, copies it into their webmail with the brochure attached, sends it, and marks it *Sent*.

## 👤 My Role

Sole developer: the Vue/TypeScript frontend, the database schema and migrations, the Row Level Security and grant model, the Supabase Auth sign-in, the world map, and the scheduled Claude task that fills the database each day.

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| **Framework** | Nuxt 4 (`ssr: false` — static, client-only SPA) |
| **Frontend** | Vue 3.5 (Composition API, `<script setup>`) · TypeScript 5 |
| **Backend-as-a-service** | Supabase — Auth, auto-generated PostgREST API, `supabase-js` |
| **Database** | PostgreSQL 17 — 7 tables, CHECK constraints, RLS, column-level grants |
| **State** | Nuxt `useState` composables (no store library) |
| **Styling** | One hand-written CSS file (no CSS framework) |
| **Automation** | Scheduled Claude task for the daily data import |
| **Tooling** | Vite 8 · `vue-tsc` · Supabase CLI (migrations) |

See [`tech-stack.md`](./tech-stack.md) for the reasons behind each choice.

## 🏗️ Architecture Overview

```
Browser (static SPA — Nuxt / Vue / TypeScript)
  │
  │  supabase-js  (publishable key + user session)
  ▼
Supabase
  ├─ Auth ─────────── email + password sign-in
  ├─ PostgREST API ── auto-generated from the schema
  └─ PostgreSQL 17
        anon           → no access at all
        authenticated  → read everything, update only status + sent time
        service_role   → daily import (scheduled Claude task)
```

Two write paths are kept apart: the **dashboard** can only move a draft through its status, and the **daily import** is the only thing that creates clubs and drafts. See [`architecture.md`](./architecture.md) for the full breakdown.

## ✨ Key Features

- **Review pipeline** — every draft moves `pending → approved → sent`, or is `rejected`, with one-click actions (approve, reject, mark as sent, undo, restore).
- **Instant updates with rollback** — the card changes at once; if the database refuses, the change is undone and an error message is shown. A failed save is never silent.
- **Live counts** — exact Pending / Approved / Sent / Rejected numbers, using count-only queries.
- **Filtered views** — All, Pending, Approved, Sent, Rejected, and a World Map view.
- **Infinite scroll with server paging** — drafts load page by page, so the list stays fast as it grows every day.
- **Copy-friendly cards** — copy the recipient, subject, body, or the full email in one tap, with a fallback for browsers that block the clipboard.
- **Recipient source note** — each club shows where its email address came from: green if verified on the club's own site, amber if not.
- **Attachment reminders** — each draft lists which files to attach by hand and which links the email mentions.
- **World map** — countries are shaded by how many emails were sent there; very small countries and territories get a marker dot so a send is always visible. A sorted country list sits under the map.

## 🔍 Technical Highlights

- **Security in the database, not the UI** — the publishable key ships inside the JavaScript bundle, but it opens nothing on its own: `anon` has no access to any table, and a signed-in user can update only two columns of one table.
- **Column-level grant as the main write limit** — `GRANT UPDATE (status_code, sent_at)` is harder to widen by mistake than a policy, because someone would have to add a new grant on purpose.
- **Strong data rules** — CHECK constraints for lower-case emails, slug format, `sent_at` matching the `sent` status, and "every country must be placeable on the map".
- **Data-driven map** — the country-to-map mapping is stored in a `countries` table, so adding a country is a new row, not a code change.
- **One request per page** — nested PostgREST selects load each draft with its club, country, attachments, and links in a single call.
- **AI-assisted daily import** — a scheduled Claude task researches clubs and writes 10 new drafts a day into Supabase, checking the master club list first so there are no duplicates.
- **Safe migrations** — applied migrations are never edited; fixes are added as new migrations.

## 🔐 Authentication & Security

- **Supabase Auth** with email and password. The password is never checked in the browser — the session is the access control.
- **No public sign-up** — staff accounts are created in the Supabase dashboard only.
- **Session kept across reloads** and refreshed automatically; the sign-in screen does not flash while the session is loading.
- **Clean sign-out** — all loaded data is cleared, so the next reviewer starts fresh.
- **Role model in Postgres** — `anon` gets nothing, `authenticated` gets read + two-column update, `service_role` is used only by the daily import. The service-role key is never placed in the frontend.

## 🧗 Challenges & Solutions

See [`challenges.md`](./challenges.md) for the full write-up. In short: the hardest part was making an app with **no server** safe, by moving every security rule into Postgres, and making sure a status change is never lost.

## 📈 Business Impact

Turns the club's reciprocal outreach into a simple daily routine: fresh drafts arrive automatically each morning, a person checks and sends them, and every reviewer sees the same up-to-date record. The master club list makes sure no club is contacted twice, and the world map shows the programme's reach at a glance.

## 🖼️ Screenshots

See [`screenshots.md`](./screenshots.md). The app shows real club contact details, so any published screenshot must use demo data.

## 🔮 Future Improvements

- Add sanitized screenshots of the sign-in screen, the daily review list, and the world map.
- More reporting on reply rates and new affiliations as the programme grows.

## 📄 License & Confidentiality

This project was developed for **Visionary Group** (for Gwadar Gymkhana) as a work made for hire. Source code, club contact data, and infrastructure configuration are private and belong to the employer; they are not included in this repository.

The world map is based on *"Simple World Map"* by Al MacDonald (editor: Fritz Lekschas), licensed [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

See also: [`architecture.md`](./architecture.md) · [`tech-stack.md`](./tech-stack.md) · [`responsibilities.md`](./responsibilities.md) · [`challenges.md`](./challenges.md) · [`screenshots.md`](./screenshots.md)

---

<div align="center">
<sub>Case study — see the <a href="../README.md">portfolio index</a> for more projects.</sub>
</div>
