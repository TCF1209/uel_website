# UEL Website SEO Plan

> Tracking document for the UEL Lubricant site SEO work. Updated as items ship.

**Status:** Batch 1 complete · Perf + GSC scaffolding done · Last updated 2026-05-14

---

## 1. Audit Snapshot

### Already in place
- Per-page `<title>` + meta description on every page
- Canonical URL on every page (`https://uel-lubricant.com/...`)
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

## 3. Batch 2 — Keyword & content
> Needs user direction. **Questions below need answers before Claude can act.**

### Questions
1. **Primary audience priority** (rank 1–4):
   - [ ] Daily car owners
   - [ ] Workshops / service centres
   - [ ] Fleet / B2B distributors
   - [ ] Factory / industrial maintenance
2. **Top 5 keywords / phrases to rank for** (give me your guesses, I'll add tools to refine):
   - 1. _____
   - 2. _____
   - 3. _____
   - 4. _____
   - 5. _____
3. **Any competitor sites we want to outrank?** (e.g. Petronas, Shell, Castrol Malaysia)

### Tasks (after questions answered)
- [ ] Per-page H1 audit — keyword in H1, unique per page
- [ ] Rewrite meta descriptions with target keywords
- [ ] Internal linking pass — connect products ↔ api-cert ↔ api-guide ↔ contact contextually
- [ ] Add FAQ section to `api-guide.html` (with FAQPage schema)
- [ ] Consider new long-form pages (e.g. "How to choose engine oil for [common Malaysian car]")

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

## 6. Open Questions (waiting on user)
1. ~~Should `oil-advisor.html` be deleted from the repo, or kept and noindexed?~~ ✓ Deleted
2. ~~Do we have a custom OG card image, or use `uel-logo.png` for now?~~ ✓ Logo for now
3. Should `where-to-buy.html` also be deleted (not in main nav)? Currently kept and in sitemap.
4. Audience priority + top 5 keywords (Batch 2 Q1, Q2)
5. Multilingual strategy A / B / C (Batch 3)
6. Do we want the Google Search Console verification meta tag added now (so it's ready when you create the property)?

---

## 7. Notes for future sessions
- Sitemap should be regenerated whenever pages are added/removed
- After site is published to Vercel, submit sitemap in Google Search Console → Sitemaps → enter `sitemap.xml`
- LocalBusiness schema only useful if NAP is consistent across site, Google Business, Facebook, etc.
- Track Core Web Vitals at pagespeed.web.dev after every major change
