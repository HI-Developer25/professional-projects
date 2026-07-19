# 🧗 Challenges & Solutions — VSH News Advertising Platform

[← Back to project overview](./README.md)

### Selling a real product with no backend

**Challenge:** The platform needed to run a genuine sales flow — tiered pricing, lead capture, CRM delivery — without justifying the ongoing cost and maintenance of a first-party API and database for what is fundamentally a brochure site.

**Solution:** Designed the entire dynamic experience around third-party integrations: a CRM webhook handles lead delivery, YouTube handles the live stream, and a CDN handles flag imagery. The result is a fully static, backend-free deployment that still supports a real revenue-generating flow.

### International lead capture without a phone-validation service

**Challenge:** Visitors from multiple countries needed to submit a phone number in a format the sales team could actually use, without integrating a paid phone-validation API.

**Solution:** Built a self-contained country/dial-code selector using a local country-data package and CDN-served flag images, with preferred countries surfaced first and client-side length validation per country.

### Preserving context through a state change, not a page change

**Challenge:** Selecting an advertising plan needed to carry that selection into the lead form and pre-tag the CRM submission with it, without a jarring page navigation.

**Solution:** Implemented the pricing-to-lead-capture transition as an in-place state swap within a single form component, so the selected plan travels with the user without a route change or lost context.

---
<sub>Part of the [VSH News — Advertising Platform](./README.md) case study.</sub>
