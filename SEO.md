# UEL Website SEO Plan

> Tracking document for the UEL Lubricant site SEO work. Updated as items ship.

**Status:** Batch 1 + Batch 2 complete · GSC verified, sitemap submitted (Success, 6 pages) · Last updated 2026-05-14

---

## 1. Audit Snapshot

### Already in place
- Per-page `<title>` + meta description on every page
- Canonical URL on every page (`https://uellubricant.com.my/...`)
- Open Graph + Twitter card tags (partial — missing image)
- Organization JSON-LD on `index.html` (name, contactPoint, areaServed: MY)
- `<meta name="robots" content="index,follow,max-image-preview:large">`
- Mobile-responsive layout, proper viewport tag
- Semantic HTML (`<header>`, `<main>`, `<section>`, `<footer>`)
- Three-language UI (EN / 中文 / BM) via JS toggle

### Gaps
| Area | Issue | Why it matters |
|---|---|---|
| Indexing | No `sitemap.xml` | Google can't reliably discover all pages |
| Indexing | No `robots.txt` | No explicit crawl signal, no sitemap pointer |
| Indexing | `oil-advisor.html` orphaned but still in filesystem | Will get crawled; dilutes link equity; risks "soft 404" |
| Sharing | No `og:image` set | Bare previews on FB, WhatsApp, Google |
| Schema | No Product JSON-LD on products.html | Missing rich snippets (star ratings, price hooks) |
| Schema | No LocalBusiness JSON-LD | Hurts ranking for "engine oil Malaysia" / "lubricant supplier near me" |
| Schema | api-guide.html has long content but no Article schema | Lost article rich result eligibility |
| Schema | No BreadcrumbList | Lost breadcrumb display in SERP |
| Perf | `uel-logo.png` is 1 MB | Hurts Core Web Vitals → ranking penalty |
| Perf | Product mockup PNGs are 1–3 MB each | Same as above, products page is heaviest |
| i18n | EN / 中文 / BM is JS-toggled, single URL | Only English content gets indexed; 中文 + BM searches won't find the site |
| Verification | No Google Search Console verification meta | Can't submit sitemap or monitor coverage after launch |

---

## 2. Batch 1 — Technical foundations ✓
> Low risk, high impact. Shipped 2026-05-13.

- [x] `sitemap.xml` at site root listing all canonical pages
- [x] `robots.txt` at site root, points to sitemap
- [x] `oil-advisor.html` deleted from repo
- [x] `og:image` + `twitter:image` on every page (using `images/uel-logo.png` as default)
- [x] LocalBusiness JSON-LD on `index.html` (extends Organization: telephone, email, openingHours Mon-Sat 09:00-18:00, areaServed MY, sameAs Facebook)
- [x] Product JSON-LD on `products.html` — dynamic ItemList generated from the `products` array on load (covers all 21 products incl. SKU, brand, SAE grade and specification)
- [x] Article + FAQPage JSON-LD on `api-guide.html` (5 FAQ entries derived from page content)
- [x] BreadcrumbList JSON-LD on `products.html`, `api-cert.html`, `api-guide.html`, `contact.html`, `where-to-buy.html`

## 2b. Performance + GSC scaffolding ✓
> Shipped 2026-05-14.

- [x] All product mockups, charts and logo converted to WebP (PNG originals retained for `og:image` / `apple-touch-icon` / JSON-LD where social and iOS need raster):
  - `uel-logo.png` 1040KB → `uel-logo.webp` **17KB** (-98%)
  - `api-diesel-chart.png` 2657KB → `api-diesel-chart.webp` **60KB** (-98%)
  - `api-petrol-chart.png` 1552KB → `api-petrol-chart.webp` **46KB** (-97%)
  - All 21 `transparent_png/*_FIXED.png` mockups + `front/` + `back/` subdirs converted (avg ~92% reduction)
- [x] `<img loading="lazy">` added to 59 images across all 7 HTML pages (skipped nav `brand-logo` which is the LCP candidate)
- [x] Dynamic `sideImage()` in products.html updated to use `.webp` extensions
- [x] Google Search Console verification meta tag scaffolded in `index.html` (commented out — uncomment + paste token after creating GSC property)

## 3. Batch 2 — Keyword & content ✓
> Shipped 2026-05-14.

### Answered
1. **Primary audience priority:** Workshops > Car owners > B2B/Fleet > Industrial
2. **Top 5 target keywords** (refined after competitor research — head term "engine oil malaysia" dropped as unwinnable vs Petronas/Shell/Castrol):
   - `engine oil klang`
   - `lubricant supplier klang / selangor`
   - `API CK-4 diesel oil malaysia`
   - `malaysian engine oil brand`
   - `engine oil wholesale malaysia`
3. **Realistic competitors** (mid-tier local — beatable with focused on-page SEO):
   - Hi-Rev, Add Oil/HIPRO, Feoso, Weblube (local manufacturers)
   - Mascot Lubricants (Klang-based direct rival, owns `engine oil klang` #1)
   - Synvoline (Klang small brand)
   - Facebook-only workshops (easy outranks for hyper-local terms)
4. **Out of reach:** Petronas, Shell, Castrol, Total, Caltex, Liqui Moly, Motul, Mobil (global brands + listicle sites lock head terms)

### Tasks shipped
- [x] All 6 pages — title rewritten with target keywords
- [x] All 6 pages — meta description rewritten with keywords + geo (Klang/Selangor) + audience (workshops/fleets)
- [x] All 6 pages — OG and Twitter card tags aligned with new titles/descriptions for consistent social share previews
- [x] `api-guide.html` — visible FAQ section added (5 Q&A items matching existing FAQPage JSON-LD; required by Google for rich snippet eligibility)
- [x] `api-guide.html` — `.faq-list` / `.faq-item` CSS added in page style; `.reveal.d4` delay added
- [x] `index.html` "Who We Are" lead — added "Malaysian engine oil brand based in Klang, Selangor" + keyword-anchor link to api-cert.html
- [x] `contact.html` hero lead — added "Klang-based Malaysian engine oil supplier serving workshops, fleets and motorists across Selangor and Malaysia" (JS i18n EN copy updated to match)
- [x] `where-to-buy.html` hero lead — added "supplied from Klang, Selangor across all of Malaysia" (JS i18n EN copy updated to match)

### Carry-forward (not done)
- [ ] Long-form blog/comparison pages (e.g. "How to choose engine oil for Proton Saga" / "API CK-4 vs FA-4 for fleet diesel trucks") — bigger content effort, treat as Batch 4
- [ ] Translate the new EN hero leads to ZH/BM in JS i18n object (only matters if multilingual strategy A is chosen)

## 4. Batch 3 — Strategic
> Bigger decisions, bigger scope.

### Decisions
- [ ] **Multilingual strategy** — pick one:
  - **A.** Keep JS toggle, only EN indexes (easiest, lose 中文/BM search traffic)
  - **B.** Split into `/zh/`, `/bm/` URL paths + `hreflang` (best for SEO, ~1 day of work)
  - **C.** Hybrid: only translate `index.html` and `products.html` to URL paths, keep others EN-only
- [x] ~~**Image compression strategy:**~~ Done 2026-05-14 (see section 2b)
- [ ] **Google Search Console:**
  - [x] Verification meta tag scaffolded in `index.html` (commented out)
  - [ ] Create the property at search.google.com/search-console, paste token into the existing meta tag
  - [ ] Submit `sitemap.xml` in GSC after deploy
- [ ] **Google Business Profile** (external, not code):
  - Register at google.com/business
  - Keep NAP consistent with site (Name: UEL — Unique Excellent Lubricant; Phone: +60 10-898 9120)

---

## 5. Decision Log
| Date | Decision | Notes |
|---|---|---|
| 2026-05-13 | Delete `oil-advisor.html` from repo | User confirmed; no inbound links |
| 2026-05-13 | Use `images/uel-logo.png` as default `og:image` | Interim; replace with dedicated 1200×630 OG card later |
| 2026-05-13 | `where-to-buy.html` kept and included in sitemap | Not in main nav but content exists; reassess in Batch 2 |
| 2026-05-13 | Product JSON-LD generated dynamically in JS rather than static blocks | Googlebot renders JS; single source of truth from `products` array |
| 2026-05-14 | WebP everywhere except `og:image` / `apple-touch-icon` / JSON-LD `logo` | Social previews + iOS still expect PNG; in-page WebP is supported in 96%+ browsers |
| 2026-05-14 | Nav `brand-logo` not lazy-loaded | LCP candidate; even at 17KB we want it eager so first paint is fast |
| 2026-05-14 | Official domain locked in: `uellubricant.com.my` (registered, status pending) | `.com.my` is a strong local-SEO signal to Google for Malaysian searches. All canonical / og:url / JSON-LD / sitemap updated. |
| 2026-05-14 | Vercel routing: apex is primary, `www.` redirects to apex | Originally www was primary which caused `Couldn't fetch` on sitemap submission (cross-host redirect) + canonical mismatch (all code uses apex). Flipped in Vercel dashboard, sitemap now Success in GSC. |
| 2026-05-14 | Removed `makesOffer` from homepage LocalBusiness JSON-LD | Six bare `{@type: Product, name: ...}` entries failed Google's Product schema validator ("offers / review / aggregateRating required"). Full Product schema lives on products.html — homepage block was a thin duplicate. |
| 2026-05-14 | Drop generic head term `engine oil malaysia` from target list | SERP locked by Petronas / Shell / Castrol / TotalEnergies + productnation / mordor listicles. 6-12 months and a content engine to crack; not realistic for UEL. Target mid-tail + local instead. |
| 2026-05-14 | GSC property type: Domain (not URL prefix) | One property covers all subdomains + protocols. DNS TXT verified via Exabytes support. |

## 6. Open Questions (waiting on user)
1. ~~Should `oil-advisor.html` be deleted from the repo, or kept and noindexed?~~ ✓ Deleted
2. ~~Do we have a custom OG card image, or use `uel-logo.png` for now?~~ ✓ Logo for now
3. Should `where-to-buy.html` also be deleted (not in main nav)? Currently kept and in sitemap.
4. ~~Audience priority + top 5 keywords (Batch 2 Q1, Q2)~~ ✓ Answered + shipped
5. Multilingual strategy A / B / C (Batch 3) — still open
6. ~~Do we want the Google Search Console verification meta tag added now?~~ ✓ Domain property verified via DNS TXT instead

---

## 7. Notes for future sessions
- Sitemap should be regenerated whenever pages are added/removed
- After site is published to Vercel, submit sitemap in Google Search Console → Sitemaps → enter `sitemap.xml`
- LocalBusiness schema only useful if NAP is consistent across site, Google Business, Facebook, etc.
- Track Core Web Vitals at pagespeed.web.dev after every major change
