# SEO & Performance Changes — `paracogas.com/pool/`

**Date:** 2026-06-22
**Files:**
- `original-page.html` — untouched download of the live page (the "before")
- `pool-optimized.html` — corrected version with all fixes applied (the "after")
- `CHANGES.md` — this report

This implements the cowork **SEO Brief** (`Paraco_Pool_Page_Content_Draft` / `Paraco_Pool_SEO_Brief`). Scope selected: **structure + metadata + performance + content expansion + FAQ schema.**

> **Important — this is a live WordPress site (Rank Math + Beaver Builder).**
> Editing `pool-optimized.html` does **not** change the live page. Use it as the visual "after" reference and a spec. The **"Where to apply"** column tells you where each change is actually made in the CMS.

> **Note on the brief vs. the live page:** the brief (from an earlier crawl) listed the **canonical tag** and **schema** as *missing*. The current live page **already has both** (Rank Math now outputs a self-referencing canonical and an Organization/WebSite/WebPage/Article graph). So those two items needed **no action** — they're marked ✅ below. The brief's other findings still stand.

---

## Summary of changes

| # | Issue (before) | Fix (after) | Where to apply in WordPress |
|---|----------------|-------------|------------------------------|
| 1 | Title `Pool \| Paraco Gas` (17 chars, no keyword) | `Propane Pool Heaters — Delivery & Service \| Paraco Gas` (~54 chars) | **Rank Math** → edit the Pool page → *Edit Snippet → Title* |
| 2 | Meta description = keyword-stuffed 8-phrase list | Benefit + CTA + service area (~145 chars) | **Rank Math** → *Edit Snippet → Description* |
| 3 | **Two `<h1>`** ("Super Summer Savings" + "Choose Paraco…") | Hero slide demoted to styled text; promo heading → `<h2>`; **one** topical `<h1>` "Propane for Pool Heaters" | Beaver Builder: hero slide module (heading tag → paragraph/H2), promo heading module (tag → H2), new Heading module for the H1 |
| 4 | Only 1 `<h2>`, no `<h3>` | 11 `<h2>` (question-style) + 7 `<h3>` | Beaver Builder content modules (see content outline below) |
| 5 | Thin/promotional content | Added ~900 words of topical content + comparison table | Beaver Builder rich-text/table modules |
| 6 | No FAQ | FAQ section (5 Q&As) | Beaver Builder rich-text module |
| 7 | No FAQ/Service/Breadcrumb schema | Added `FAQPage` + `Service` + `BreadcrumbList` JSON-LD | **Rank Math** (Schema Generator: Service + FAQ) or a custom JSON-LD block |
| 8 | Schema `ImageObject` declared **200×200** for a 1920×765 banner | Corrected to 1920×765 | Rank Math (usually auto-corrects once the image meta is right; verify in Rich Results Test) |
| 9 | Visible typo: `o⇥With warm weather…` (stray list bullet) | Removed stray `o` + tab | Beaver Builder rich-text module (promo block) |
| 10 | LCP hero `<img>`/`<picture>` had invalid `loading="false"` | Changed to `loading="eager"` (keeps `fetchpriority="high"`) | Theme/slider template, or the media settings producing the slide |
| 11 | **Zero** `preconnect`/`dns-prefetch` for ~12 third-party origins | Added 8 resource hints (fonts, CookieYes, GTM, Hotjar, reCAPTCHA, Salesforce, review-alerts) | Theme `<head>` (functions.php `wp_head`, or a header-scripts plugin / Perfmatters) |
| 12 | Generic image alts on banner | (Current download already has alts on all `<img>`) ✅ no action | — |

---

## 1. Title tag
**Before:** `Pool | Paraco Gas`
**After:** `Propane Pool Heaters — Delivery & Service | Paraco Gas`
**Why:** Front-loads the real keyword and uses the full ~60-char budget. "Pool" alone matches no search intent. Updated in `<title>`, `og:title`, `twitter:title`, and the schema `headline`/`name` fields for consistency.

## 2. Meta description
**Before:** `How to Heat a Pool, Pool Heating, Propane Pool, Gas Pool, …` (keyword list)
**After:** `Heat your pool efficiently with propane. Paraco delivers reliable pool-heater propane across NY, NJ & CT — plus inspections and service contracts.`
**Why:** A keyword list reads as spam and gives no reason to click. A benefit + CTA + service area lifts CTR. Updated in `<meta name="description">`, `og:description`, `twitter:description`, and schema `description`.

## 3–6. Heading structure & content
Result: **exactly one `<h1>`**, with a logical question-style outline (good for People-Also-Ask and AI Overviews):

- **H1:** Propane for Pool Heaters *(+ BLUF intro paragraph)*
- H2: Why Is Propane a Smart Choice for Pool Heating?
- H2: How Does a Propane Pool Heater Work?
- H2: Can You Use a Propane Pool Heater for Inground and Above-Ground Pools? *(H3: Inground / H3: Above-ground)*
- H2: Propane vs. Electric Heat Pump vs. Solar *(comparison table)*
- H2: What Size Propane Tank Do You Need for a Pool Heater?
- H2: How Much Does It Cost to Heat a Pool With Propane?
- H2: Do You Inspect and Service Pool Heaters?
- H2: Where Can You Get Propane Pool Heating Near You?
- H2: Choose Paraco for All Your Summer Propane Needs! *(demoted from H1 — existing promo + form)*
- H2: Ready to Lock In Your Summer Savings? *(existing CTA)*
- H2: Frequently Asked Questions *(5 Q&As, each an H3)*

Each section opens with a direct 1–2 sentence answer (BLUF) so it's snippet-ready.

## 7. Schema markup (added)
New JSON-LD block with three types:
- **BreadcrumbList** — Home → Propane for Pool Heaters
- **Service** — "Propane Pool Heating", `areaServed` = NY, NJ, CT, MA, PA, RI (the states in the lead form), `provider` linked to the existing Organization `@id`
- **FAQPage** — the 5 FAQ Q&As (text matches the visible FAQ exactly, as required)

Validate with the [Rich Results Test](https://search.google.com/test/rich-results) after publishing.

## 8–11. Technical/performance
- **Schema image dimensions** corrected 200×200 → 1920×765.
- **LCP hero** `loading="false"` (invalid) → `loading="eager"`; `fetchpriority="high"` retained. Run [PageSpeed Insights](https://pagespeed.web.dev/) to confirm LCP after deploy.
- **Resource hints** added for the third-party origins the page actually calls.

---

## ⚠️ Items needing Paraco confirmation before publishing
The content draft flagged a few specifics that should be verified (don't publish unverified numbers):

1. **Service area** — I used the 6 states from the lead form (NY, NJ, CT, MA, PA, RI) in the body + Service schema. The title/meta use the brief's shorter "NY, NJ & CT". Confirm the correct list.
2. **Do you install heaters, or supply/service propane only?** The "near you" section currently says delivery + support. If Paraco installs, target "pool heater installation near me" explicitly and link `/locations/`.
3. **Tank sizing (250–500 gal) and BTU ranges (200k–400k)** — industry-typical figures. Confirm against what Paraco actually offers.
4. **Cost section** — intentionally kept qualitative (no dollar figures). Add Paraco-specific rate/pre-buy guidance if desired.
5. **Internal links** used confirmed footer URLs: `/residential/`, `/service-contracts/`, `/locations/`. Add a dedicated tank-sizing page link if one exists.

## Not changed (out of scope for a static edit, but recommended)
- **Render-blocking resources:** 15 stylesheets + jQuery load in `<head>`. Consider a caching/optimization plugin (WP Rocket / Perfmatters) to defer non-critical CSS/JS.
- **Third-party script weight:** Salesforce chat, reCAPTCHA, Hotjar, CookieYes, review-alerts. Audit whether all are needed on this landing page; load non-critical ones on interaction.
- **`og:type`** is `article`; `website` is more accurate for a service landing page (minor).
- **Duplicate WPForms** (`#wpforms-4237` appears twice — modal + popup). Functional, not an SEO issue.
- **Inbound internal links:** add links **to** `/pool/` from `/residential/` and any outdoor-living content, with anchor text like "propane pool heating".
