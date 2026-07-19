# 🧗 Challenges & Solutions — Gwadar Gymkhana Public Website

[← Back to project overview](./README.md)

### Handling real money without touching card data

**Challenge:** The club needed to accept online membership payments, but neither the frontend nor the backend should ever handle raw card details, and the flow needed to satisfy 3D Secure requirements.

**Solution:** All card entry happens on the payment gateway's own hosted checkout page. The application's job is limited to building a signed initiation request and, on return, re-validating an HMAC-signed, expiring redirect before displaying any success or failure state. A tampered or expired redirect is rejected outright rather than trusted.

### Zero layout shift on a visually rich, animation-heavy site

**Challenge:** A site with a cinematic hero, scroll-triggered animations, and dynamic banners is an easy way to accumulate layout shift, which hurts both user experience and SEO.

**Solution:** Layout-affecting values — header height, banner visibility, image aspect ratios — are resolved server-side before the page reaches the browser, and every animation is implemented through a single composable that respects `prefers-reduced-motion` and cleans up automatically on navigation.

### Keeping content editable without a developer in the loop

**Challenge:** Club staff needed to update pricing, testimonials, and construction-progress photos regularly, without waiting on a code deploy each time.

**Solution:** All of that content is served from the Laravel backend as read-only API endpoints and fetched at render time via `useAsyncData`, so updates on the backend appear on the live site without touching the frontend codebase.

### Running production and staging safely with a team of one

**Challenge:** With no dedicated QA or ops team, changes needed a safe place to be verified before reaching real visitors and real payments.

**Solution:** Separate production and staging environments, each with its own PM2 process and deployment target, driven by a branch-based GitHub Actions pipeline — `main` to production, `dev` to staging — with deploys serialized per branch so concurrent pushes can't race the same target.

---
<sub>Part of the [Gwadar Gymkhana — Public Website](./README.md) case study.</sub>
