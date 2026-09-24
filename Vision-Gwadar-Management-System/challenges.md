# 🧗 Challenges & Solutions — Vision Gwadar Management System

[← Back to project overview](./README.md)

### Keeping financial records consistent

**Challenge:** A customer file, its instalment schedule, its invoice, the payments against it, and the receipts for those payments all depend on each other. If staff had to create each record by hand, they would drift out of sync — and in a financial system, a missing or duplicated record is a real problem.

**Solution:** The backend creates the dependent records itself. A schedule opens automatically with a new file, a payment is raised when the thing it settles is created, and a receipt opens when an amount is entered. Nothing financial is deleted: invoiced items are retired, and money that never arrived is marked *failed*. This keeps a full, honest history.

### A permission model that is strict but easy to extend

**Challenge:** Different staff need very different access — accounts, sales, and marketing should each see only their part — and checks hidden only in the UI are not safe for financial data.

**Solution:** A role plus key-based permissions, enforced by middleware on every route, with admins handled once in a `Gate::before` hook. The frontend gets the same keys through a `can()` helper, but only to hide UI. New permissions are added through an idempotent seeder, with no change to the middleware or the helper. The dashboard goes further: panels a user can't see are not sent at all.

### A monthly recovery view the accounts office can act on

**Challenge:** The accounts office needed to see, each month, exactly what every file owes — including anything left unpaid from earlier months — and then contact defaulting customers and keep a record of it.

**Solution:** A recovery report that carries forward unpaid amounts, with recovery notices sent straight from each report row and logged against it. Notices go through a queue and a channel interface, so email works today and WhatsApp can be added later without changing the report.

### Keeping a one-person codebase safe to change

**Challenge:** With no second engineer to review changes, small mistakes — a renamed route, a wrong type, a missing permission check — could easily reach production.

**Solution:** Strong automated checks. PHPStan runs at level 7, the frontend is strictly typed, Wayfinder makes routes type-checked, and 35 Pest test files mirror the controllers. CI runs all of it, and nothing deploys to production or staging unless it passes.

---
<sub>Part of the [Vision Gwadar — Management System](./README.md) case study.</sub>
