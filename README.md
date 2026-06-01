# Midday Rotary Club Website (Weebly Archive)

This repository contains a **static archive of a Weebly website** for the **Midday Rotary Club of San Miguel de Allende**.

Based on repository contents, this is not a source project in the modern sense (no build system, no app framework). It is a captured/exported website snapshot composed mostly of HTML pages plus uploaded media and Weebly theme assets.

## Quick deploy checklist (non-technical)

- [ ] Confirm `index.html` loads correctly locally first.
- [ ] Push repository to GitHub.
- [ ] Choose one static host:
  - [ ] GitHub Pages (fastest if already on GitHub)
  - [ ] Cloudflare Pages (good for managed DNS/workflows)
- [ ] Publish from repository root (no build command).
- [ ] Open the public URL and click-test top navigation, `news.html`, and multiple `/news/<slug>/` post pages.
- [ ] Share URL as temporary archive/staging reference (not final CMS).
- [ ] Continue WordPress migration work in parallel.

## What this repository is

- A legacy, static website snapshot intended for preservation, review, and possible migration.
- A Weebly-generated site using Weebly classes, templates, and external CDN assets.
- Primarily English-language content about Rotary service projects, membership, speakers, and club news.

## Provenance (best-known)

- The site has been extracted from a backed-up Weebly ZIP archive.
- Internal page metadata references:
  - Site title/content: **Midday Rotary Club of San Miguel de Allende**
  - Weebly site/user IDs embedded in page scripts
  - `IS_ARCHIVE = 1` flags in HTML pages

## Repository contents

Top-level:

- `*.html` — 30 static pages (for example: `index.html`, `our-projects.html`, `news.html`, `membership.html`, `members-only.html`, `contact-us.html`)
- `news/` — static News archive pages
  - `news/index.html` (news archive index)
  - `news/<slug>/index.html` — 81 generated post pages
- `files/` — local CSS/JS/theme resources
  - `files/main_style.css`
  - `files/theme/files/manifest.json` (theme manifest; Edison theme)
- `assets/` — mirrored vendor CSS/JS/font assets used by archived pages
- `uploads/` — uploaded media and documents (largest content area)
- `harvest/news/` — migration artifacts for WordPress
  - `harvest/news/news_posts.csv`
  - `harvest/news/wordpress_news_import.csv`
  - `harvest/news/wordpress_media_manifest.csv`
  - `harvest/news/news_posts.json`
  - `harvest/news/images/`
- `apps/` — legacy app artifacts (includes Flash `.swf`)

Approximate size:

- `uploads/`: ~346 MB
- `assets/`: ~6.9 MB
- `files/`: ~286 KB
- `news/`: ~636 KB
- `harvest/news/`: ~65.8 MB

## Local preview

This is a static site and can be previewed with any simple HTTP server.

```bash
python3 -m http.server 8000
```

Then open:

- `http://localhost:8000/index.html`

## Static hosting option (pre-WordPress staging)

Yes. In its current offline-localized state, this archive can be hosted on static platforms such as GitHub Pages or Cloudflare Pages as a temporary staging/reference site before WordPress rebuild.

### Option A: GitHub Pages

1. Push this repository to GitHub.
2. In repository settings, enable **Pages** and deploy from:
   - Branch: `main` (or your default branch)
   - Folder: `/ (root)`
3. Wait for deployment, then open the provided `*.github.io` URL.

### Option B: Cloudflare Pages

1. Connect this GitHub repository to Cloudflare Pages.
2. Create a new Pages project with:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
3. Deploy and use the generated `*.pages.dev` URL.

### Staging caveats

- This is static archival hosting only, not a production CMS.
- Dynamic functions from legacy Weebly (membership, server-side forms, account flows) are non-functional in static hosting.
- External embeds were converted for offline-safe behavior and may show placeholders rather than live remote content.

## Important limitations

Because this is an archive snapshot, some features may not function fully outside original Weebly hosting:

- Membership/login/account flows (depend on Weebly backend APIs)
- Some forms/search behavior
- External assets/scripts tied to Weebly/CDN services
- Legacy Flash asset in `apps/audioPlayer2.swf` is obsolete in modern browsers

## Recommended use

Use this repository as:

1. A historical backup of site content and media
2. A source for migration to a modern CMS/static-site stack
3. A reference for rebuilding navigation/content structure

Not recommended as a long-term production hosting target without refactoring/replacement of external dependencies and dynamic features.

## Migration checklist (WordPress on Member Minder Pro managed hosting)

Use this checklist to move this archive into a maintainable WordPress site.

### 1) Discovery and planning

- [ ] Confirm scope: full site migration vs selective content migration
- [ ] Define information architecture (new menus, page hierarchy, URL strategy)
- [ ] Inventory all legacy pages and map each to a destination WordPress page/post/CPT
- [ ] Identify must-keep assets (logos, PDFs, key historical photos) vs archival-only assets
- [ ] Define owners/approvers for content, media, and final QA

### 2) Hosting and environment setup (Member Minder Pro)

- [ ] Provision WordPress environment under Member Minder Pro managed hosting
- [ ] Configure domain/DNS plan (cutover window, TTL reduction, rollback approach)
- [ ] Enable SSL and confirm HTTPS-only redirects
- [ ] Set up staging and production environments with deployment workflow
- [ ] Configure backups and retention policy before migration work starts

### 3) Content extraction and normalization

- [ ] Build a page-by-page migration matrix from `*.html` files
- [ ] Extract clean body content from Weebly markup (`wsite-*` wrappers removed)
- [ ] Normalize heading structure (`h1`/`h2`/`h3`) for accessibility/SEO
- [ ] Standardize internal links to planned WordPress permalinks
- [ ] Rewrite or remove broken legacy references (Weebly RPC/search/membership scripts)

### 4) Media migration

- [ ] Import media from `uploads/` into WordPress Media Library
- [ ] Rename/organize files into predictable folders (projects, speakers, branding, reports)
- [ ] Replace legacy image paths in content with WordPress-managed media URLs
- [ ] Keep original high-res media archived separately as a cold backup
- [ ] Validate PDFs and downloadable documents (open, size, filename clarity)

### 5) Theme, templates, and navigation

- [ ] Choose/build a WordPress theme aligned with Rotary branding and accessibility
- [ ] Recreate primary/secondary navigation from legacy menus
- [ ] Create reusable blocks/patterns for project pages and news updates
- [ ] Rebuild footer content and organization details
- [ ] Implement responsive behavior and cross-browser testing baseline

### 6) Feature replacement

- [ ] Replace Weebly membership/login flows with WordPress-compatible membership tooling (if needed)
- [ ] Replace contact forms with WordPress form plugin + SMTP delivery
- [ ] Implement site search using WordPress native search or managed plugin
- [ ] Remove unsupported legacy assets (e.g., `apps/audioPlayer2.swf`) and replace with HTML5 alternatives
- [ ] Recreate any popups/modals previously dependent on third-party Weebly app scripts

### 7) SEO and analytics

- [ ] Preserve page titles/meta descriptions where still relevant
- [ ] Create 301 redirect map from legacy HTML filenames to new permalinks
- [ ] Generate XML sitemap and submit to search engines
- [ ] Reconnect analytics/tracking (GA4 or organization standard)
- [ ] Validate Open Graph/social sharing metadata

### 8) Security, compliance, and governance

- [ ] Apply least-privilege WordPress roles for editors/admins
- [ ] Enable WAF/security monitoring available in managed hosting stack
- [ ] Configure spam protection and form abuse controls (CAPTCHA/honeypot/rate limits)
- [ ] Confirm privacy policy/cookie disclosures for active integrations
- [ ] Establish update cadence for WordPress core, theme, and plugins

### 9) QA and launch

- [ ] Run link check (internal/external), image check, and form submission tests
- [ ] Validate mobile/responsive behavior on key templates
- [ ] Perform accessibility pass (keyboard nav, contrast, semantic headings, alt text)
- [ ] Run performance checks (Core Web Vitals baseline)
- [ ] Execute cutover, monitor logs/errors, and verify redirects post-launch

### 10) Post-launch operations

- [ ] Archive this repository as “legacy source snapshot” (read-only)
- [ ] Document ongoing editorial workflow for club volunteers/staff
- [ ] Train content maintainers on blocks/pages/media standards
- [ ] Schedule quarterly content and plugin hygiene reviews
- [ ] Track migration gaps and backlog improvements in an issue tracker

## Notes

There may be a discrepancy between oral history and page metadata regarding location naming. The archived pages repeatedly identify the club as **San Miguel de Allende**.
