# 🧗 Challenges & Solutions — Gwadar Gymkhana Reciprocal Outreach Review

[← Back to project overview](./README.md)

### Making an app with no server safe

**Challenge:** The app is a static SPA. The Supabase key is inside the JavaScript that every visitor downloads, and there is no server to check requests. Any rule kept only in the UI could be skipped.

**Solution:** Every rule lives in Postgres. `anon` gets no access to any table, so the key alone opens nothing. A signed-in user can read, but can update only two columns — `status_code` and `sent_at` — through a column-level grant. Only the daily import, running as `service_role`, can create clubs and drafts.

### Never losing a status change

**Challenge:** Reviewers want the screen to react instantly. But if the screen shows "Sent" and the database did not save it, the record is wrong — and the club might be contacted again.

**Solution:** Optimistic updates with rollback. The card changes at once; if the database refuses the change, it is reverted and a toast explains the error. The stat counts move in step with the change.

### Never contacting the same club twice

**Challenge:** New drafts arrive every day, and over time the same club could easily be drafted again.

**Solution:** A `clubs` table acts as the permanent master list — one row per club, ever. The daily import checks this list before writing any new draft.

### Filling the database every day without manual work

**Challenge:** Finding suitable clubs, checking contact details, and writing drafts each day is slow, repeated work.

**Solution:** A scheduled Claude task does the daily import. It researches clubs, connects to Supabase, and inserts 10 new drafts a day. A person still reviews and sends every email, so the automation saves time without removing human control.

### Showing small countries on a world map

**Challenge:** Some countries (like Singapore or the UAE) are too small to see on a world map, and some places (like Hong Kong) have no shape in the base map at all.

**Solution:** The `countries` table stores either a map path id or a marker position for each country, and a CHECK constraint makes sure every country has one of them. Small places get a marker dot, so every send is visible. Adding a new country is just a new row.

### Changing a live database safely

**Challenge:** Editing a migration that has already run can leave the live database and the code out of sync.

**Solution:** Applied migrations are treated as fixed. Every fix is a new migration, and changes are previewed with `supabase db push --dry-run` before being applied.

---
<sub>Part of the [Gwadar Gymkhana — Reciprocal Outreach Review](./README.md) case study.</sub>
