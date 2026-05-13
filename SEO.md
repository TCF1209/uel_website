# UEL Website SEO Plan

> Tracking document for the UEL Lubricant site SEO work. Updated as items ship.

**Status:** Batch 1 not started · Last updated 2026-05-13

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

## 2. Batch 1 — Technical foundations
> Low risk, high impact. Claude implements without further discussion.

- [ ] `sitemap.xml` at site root listing all canonical pages
- [ ] `robots.txt` at site root, points to sitemap
- [ ] Resolve `oil-advisor.html`: delete the file (recommended, no inbound links) **or** add `<meta name="robots" content="noindex">`
- [ ] `og:image` (and `twitter:image`) on every page — needs a dedicated image asset (~1200×630 px). Default to `images/uel-logo.png` if no custom OG card yet
- [ ] LocalBusiness JSON-LD on `index.html` (extends the existing Organization block: telephone, address, openingHours, areaServed, sameAs Facebook)
- [ ] Product JSON-LD per product on `products.html` (name, image, description, brand, sku, dataSheet URL)
- [ ] Article + FAQPage JSON-LD on `api-guide.html`
- [ ] BreadcrumbList JSON-LD on `products.html`, `api-cert.html`, `api-guide.html`, `contact.html`

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
- [ ] **Image compression strategy:**
  - Convert `uel-logo.png` 1 MB → WebP ~50 KB
  - Convert all `transparent_png/` mockups to WebP, keep PNG as fallback
  - Add `<img loading="lazy">` where missing
- [ ] **Google Search Console:**
  - Add verification meta tag once you create the property at search.google.com/search-console
  - Submit sitemap after batch 1
- [ ] **Google Business Profile** (external, not code):
  - Register at google.com/business
  - Keep NAP consistent with site (Name: UEL — Unique Excellent Lubricant; Phone: +60 10-898 9120)

---

## 5. Decision Log
| Date | Decision | Notes |
|---|---|---|
| _ | _ | _ |

## 6. Open Questions (waiting on user)
1. Should `oil-advisor.html` be deleted from the repo, or kept and noindexed?
2. Do we have a custom OG card image, or use `uel-logo.png` for now?
3. Audience priority + top 5 keywords (Batch 2 Q1, Q2)
4. Multilingual strategy A / B / C (Batch 3)
5. Do we want the Google Search Console verification meta tag added now (so it's ready when you create the property)?

---

## 7. Notes for future sessions
- Sitemap should be regenerated whenever pages are added/removed
- After site is published to Vercel, submit sitemap in Google Search Console → Sitemaps → enter `sitemap.xml`
- LocalBusiness schema only useful if NAP is consistent across site, Google Business, Facebook, etc.
- Track Core Web Vitals at pagespeed.web.dev after every major change
