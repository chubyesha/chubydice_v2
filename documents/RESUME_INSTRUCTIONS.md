# Resume Instructions — Chuby Dice Website V2

**For the next Claude Code session to continue where this one left off.**

---

## Quick Start

1. **Read this file first**, then `documents/SESSION_RECOVERY.md` for full context.
2. **Check current branch:** `git branch --show-current`
3. **Check for uncommitted work:** `git status`
4. **Check remote:** `git remote -v` (should point to `chubyesha/chubydice_v2.git`)
5. **List all branches:** `git branch -a`

---

## Project Context

- **Project:** Chuby Dice V2 — static HTML website for a Dancehall artist/educator
- **Live URL:** https://www.chubydice.com
- **Hosting:** Netlify (auto-deploys from GitHub)
- **Repo:** `git@github.com:chubyesha/chubydice_v2.git` (newly set, NOT pushed yet)
- **Previous repo (V1):** `git@github.com:chubyesha/chubydice.git` — separate project, do NOT use
- **Tech:** Static HTML (no build tools), inline CSS/JS per page, `shared-theme.css` for design system, Netlify Functions for chatbot
- **Design:** Purple/dark theme with Outfit + DM Sans fonts, CSS custom properties for tokens

## What Was Completed (as of 2026-04-01)

### Release 2A (Previous Sessions)
All 7 product requirements from the PRD implemented on `feat/release-2a-requirements`.

### Current Session — 4 Branches (All Unpushed)

#### 1. `feat/wire-stripe-links-all-series`
- 5 Stripe payment links wired to series.html class pass buttons (now live "Buy Now")
- lovers-rock.html and full-series.html archived (Stripe links removed, "Past Series" messaging)
- march-back-in-time.html Stripe link corrected to 5-Class Pass URL
- Security hardening: `noopener,noreferrer` on all `window.open` calls

#### 2. `fix/center-dropdown-navigation`
- Dropdown menu centered below MENU toggle (was far right near Book Now)
- All 16 HTML files updated: `right: 24px` → `left: 50%; translateX(-50%)`
- Mobile overrides updated for consistent behavior
- series.html missing mobile width override added

#### 3. `fix/unified-font-brand-consistency`
- shared-theme.css extended with 30+ missing font selectors
- All sub-pages now render Outfit (headings/UI) + DM Sans (body) matching index.html
- clash.html was missing shared-theme.css link — added
- `.menu-overlay a` and `.footer-links a` now correctly render Outfit

#### 4. `docs/session-and-readme-update`
- README.md updated for V2 with current project state
- SESSION_RECOVERY.md and RESUME_INSTRUCTIONS.md updated

## What Still Needs To Be Done

### Immediate Priority
- **Push all branches** to new remote (`chubyesha/chubydice_v2.git`) — user's responsibility
- **Merge branches** to main (or create PRs) — user's responsibility
- **Verify Stripe links work** in production after deploy
- **Test dropdown centering** across browsers and mobile devices

### Pre-existing Issues to Fix
- **Broken OG image:** All 16 pages reference `chuby-profile-CkJq2sVN.jpg` which doesn't exist. Update all `og:image` and `twitter:image` meta tags.
- **CORS wildcard:** `netlify.toml` and `netlify/functions/chat.js` use `Access-Control-Allow-Origin: *`. Restrict to actual domain.
- **Chat function input validation:** Add message length/count limits to `netlify/functions/chat.js`.
- **`--border` CSS variable conflict:** shared-theme.css (`rgba(255,255,255,0.08)`) vs page-local definitions (`#242424`).
- **Security headers:** Add `X-Frame-Options`, `Content-Security-Policy`, `Referrer-Policy` to `netlify.toml`.
- **Dead inline Barlow declarations:** Sub-pages still have inline `font-family: 'Barlow'` declarations that are overridden by shared-theme.css `!important`. Can be cleaned up in a refactor.
- **shared-theme.css mobile `right: 16px !important`:** Technically stale after dropdown centering fix (should be removed or changed to match `left: 50%`).

### Release 2B (Future)
- **Clash Inna Dancehall pricing:** Workshop and clash pass pricing
- **Terms & Conditions page**
- **Brand Ambassadorship dedicated page** (currently links to contact.html)

## Key Patterns

### Stripe Link Pattern
All active series pages use: `onclick="window.open('https://buy.stripe.com/...','_blank','noopener,noreferrer')"`

Series-specific pages (praise-flow, motherland, dancehall-royalty) use interactive pricing selectors with `data-link` attributes and `selectPrice(el)` / `openSelectedPrice()` JS functions.

### Dropdown Menu Centering
Desktop: `position: fixed; top: 64px; left: 50%; transform: translateX(-50%)`
Mobile: inherits centering, width set to `calc(100vw - 32px)` for 16px margins
Open state: `transform: translateX(-50%) translateY(0) scale(1)`

### Font Override System
`shared-theme.css` uses `!important` to enforce:
- Outfit on all heading, UI, button, label, badge, pricing, and menu selectors
- DM Sans on body, paragraphs, and general text
- Sub-page inline Barlow/Barlow Condensed declarations are dead code (overridden)

### Nav Menu Updates
All 16 HTML files have independent nav menus. Use Python batch script to update consistently:
- Find `<div class="menu-overlay" id="menuOverlay">` block
- Replace inner links, set `class="active"` per page

### Accordion Pattern (coaching.html, about.html)
- CSS: `.acc-item.open .acc-body { max-height: Xpx; }` with transition
- JS: Click handler toggles `.open` class, single-open behavior

## Critical Warnings

- **NEVER checkout main/master** — work only on feature branches
- **NEVER git stash** — it erases current changes
- **NEVER force push** to any shared branch
- **Remote changed** — now `chubyesha/chubydice_v2.git` (not the V1 repo)
- **Nav menus are duplicated** across 16 files — any change must be applied to ALL pages
- **`shared-theme.css` `!important`** — All font overrides rely on `!important`. Adding inline `!important` font declarations in sub-pages will break the cascade.
- **index.html is standalone** — Does NOT load `shared-theme.css`. Any shared-theme changes won't affect it.
- **Test on mobile** — Breakpoints at 900px and 640px

## File Quick Reference

| Need to... | File(s) |
|------------|---------|
| Update nav menu | All 16 `.html` files |
| Add/modify series | `series.html`, `index.html`, create new sub-page |
| Update coaching content | `coaching.html` |
| Update biography | `about.html` |
| Change design tokens / fonts | `shared-theme.css` |
| Modify chatbot | `chatbot.js`, `netlify/functions/chat.js` |
| Update Netlify config | `netlify.toml` |
| Add/modify Stripe links | Series sub-pages + `series.html` pricing section |
| Check client notes | `documents/Info Architecture - RELEASE 2 STRIPE WORKING NOTES.docx` |

## Branch State (as of 2026-04-01)

```
Remote: git@github.com:chubyesha/chubydice_v2.git (NOT pushed yet)

Branches (all local, unpushed):
  main
  feat/wire-stripe-links-all-series    (2 commits: Stripe links + noopener)
  fix/center-dropdown-navigation       (2 commits: centering + series mobile)
  fix/unified-font-brand-consistency   (2 commits: shared-theme selectors + clash.html)
  docs/session-and-readme-update       (current: README + session docs)
```
