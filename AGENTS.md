# AGENTS.md — johnlevendis.com

Instructions for AI agents working on this site. This file is in a public repository; keep private details out of it.

## How the site builds

- **Stack:** Quarto website project, Bootstrap/Flatly theme, hosted on Netlify.
- **Source files:** `.qmd` pages and `_quarto.yml`. Edit source, never the rendered `_site/` folder.
- **Build command:** `quarto render` (Netlify runs this on deploy).
- **Output:** `_site/` directory. Rendered output is committed but is regenerated on each Netlify deploy.
- **Static files copied to output:** `_redirects`, `_headers`, and `robots.txt` are listed under `resources` in `_quarto.yml`.

## Page map

| Page | Source | Purpose |
|------|--------|---------|
| Home | `index.qmd` | Bio, photo, JSON-LD Person schema |
| Research | `research.qmd` | Selected publications with PDFs |
| Book | `book.qmd` | *Time Series Econometrics* (Springer, 2nd ed. 2023), JSON-LD Book schema |
| Teaching | `teaching.qmd` | Courses at Tulane with syllabi |
| CV | `cv.qmd` | Link to PDF vita |
| 404 | `404.qmd` | Custom not-found page with nav links |

External navbar links: Substack (Writing), YouTube (Videos).

## Conventions

- **Voice:** First person ("I teach...", "My research...").
- **Do not change without asking:** Book page wording, publisher links (Springer, Amazon), the endorsement quote (Prof. Sokbae "Simon" Lee), publication list entries.
- **Do not publish:** Home address, personal (non-Tulane) email, rates, or any private information.
- **No consulting or workshop content.** The site is for academic credibility, not client acquisition.
- **Accessibility:** Link color `#0e806b` (WCAG 4.5:1 on white) in `styles.css`. Empty navbar brand-logo hidden via CSS. All images have alt text.
- **SEO:** `site-url` set in `_quarto.yml` for canonical links and sitemap. Open Graph and Twitter Card enabled. Meta descriptions on all pages. `robots.txt` allows all crawlers and links to `sitemap.xml`.
- **Structured data:** JSON-LD Person block on home page (`@id: https://johnlevendis.com/#john`), Book block on book page.
- **Security headers:** `_headers` file sets X-Content-Type-Options, Referrer-Policy, X-Frame-Options, Permissions-Policy.
- **Redirects:** `/about` and `/about/` → `/` (301). `/AGENTS.md` and `/CLAUDE.md` → `/` (301).

## Workflow

- Work on a branch. Open a draft PR or use a Netlify deploy preview. Never push directly to production.
- After merge, verify live at johnlevendis.com before calling it done.
- Request re-indexing in Google Search Console only for pages whose content changed.

## Verification checklist (before asking to merge)

- `quarto render` succeeds with no new warnings.
- Changed pages render correctly at desktop (~1280px) and mobile (~390px) widths.
- Metadata on changed pages: title, description, canonical, Open Graph, JSON-LD (valid, matches visible content).
- Links on changed pages resolve.
- Re-read your own diff as a skeptical reviewer.

## Decision log

| Date | Decision | Reason |
|------|----------|--------|
| 2026-10 | `/about/` redirected to home page (301) | Old stub page ("About this site", "1 + 1") was being indexed; redirect is faster than rewriting and preserves link equity |
| 2026-10 | Link color changed to `#0e806b` | Flatly default `#18bc9c` fails WCAG 4.5:1 contrast on white (2.41:1) |
| 2026-10 | JSON-LD Person and Book schemas added | Helps search engines and AI answers identify John and his book correctly |
| 2026-10 | Security headers added | Basic hardening; no CSP (Quarto's search/scripts can break under strict CSP) |
| 2026-10 | Google Search Console verified and sitemap submitted | Site was not appearing in search results for "john levendis" |
| 2026-10 | Photo resize deferred | 448KB photo has negligible impact on an otherwise lightweight site |
| 2026-10 | No consulting/workshop contact path | John does not want consulting inquiries |
| 2026-10 | Navbar brand-logo CSS specificity fix | One-class selector was overridden by Quarto bootstrap; two-class selector (`.navbar-brand.navbar-brand-logo`) works |
| 2026-10 | `.html` → pretty URL redirects in `_redirects` | Duplicate content: both `/research` and `/research.html` served the same page; sitemap lists `.html`, so redirect `.html` to extension-less |
| 2026-10 | Person schema URL fixed to `datainstitute.tulane.edu` | `caids.tulane.edu` does not resolve (DNS error) |
