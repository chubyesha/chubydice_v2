# Session Recovery — Chuby Dice Website V2

**Last Updated:** 2026-04-01
**Active Branches (unpushed):**
- `feat/wire-stripe-links-all-series` — Stripe payment links wired + archived series
- `fix/center-dropdown-navigation` — Dropdown menu centered below MENU toggle
- `fix/unified-font-brand-consistency` — Unified font system across all pages
- `docs/session-and-readme-update` — README + session docs update (current)

---

## What Was Done This Session (2026-04-01)

### Task 1: Git Remote Migration
- **Problem:** Remote origin pointed to `chubyesha/chubydice.git` (V1 repo), causing collision risk with the V1 codebase
- **Fix:** Changed remote to `git@github.com:chubyesha/chubydice_v2.git`
- **Status:** Remote updated locally. Not pushed yet (user's responsibility).

### Task 2: Stripe Payment Links — `feat/wire-stripe-links-all-series`

**Commits:**
- `198c1cd` — feat: wire Stripe payment links to series class passes
- `eba2613` — fix: add noopener,noreferrer to Stripe window.open calls

**What was done:**
- Parsed client document `documents/Info Architecture - RELEASE 2 STRIPE WORKING NOTES.docx` to extract 5 Stripe payment links
- **series.html:** Activated 5 class pass buttons — removed `pending` class, replaced "Coming Soon" with "Buy Now", added live `onclick="window.open('https://buy.stripe.com/...')"` handlers
- **lovers-rock.html:** Archived — replaced Book Now + Stripe link with "Past Series" messaging
- **full-series.html:** Archived — replaced Book Now + Stripe link with "Past Series" messaging
- **march-back-in-time.html:** Fixed incorrect Stripe link (was sharing lovers-rock's link) to correct 5-Class Pass URL
- **Security hardening:** Added `noopener,noreferrer` to all `window.open` Stripe calls
- **Verified:** praise-flow.html, motherland.html, dancehall-royalty.html already had correct Stripe links

**Stripe Link Mapping (from client document):**

| Pass | Price | Link Suffix |
|------|-------|-------------|
| Single Class | $30 | `...5cX4F20b` |
| 4 Classes | $100 | `...fRB4F20c` |
| 5 Classes | $125 | `...bBl4F20d` |
| 10 Classes | $230 | `...cFp4F20e` |
| 20 Classes | $450 | `...8p94F20f` |

**Archived by client (Stripe links removed):**
- Feb Lovers' Rock
- Adelaide — In Ya City (already archived previously)
- Full Chuby Dice Series (Q1 cohort)

**Review status:** Code review APPROVED, Security review APPROVED (0 critical, 0 high).

---

### Task 3: Center Dropdown Navigation — `fix/center-dropdown-navigation`

**Commits:**
- `2c6584f` — fix: center dropdown navigation panel below menu toggle
- `0639a4b` — fix: add missing mobile width override for series.html dropdown

**Problem:** Dropdown navigation panel was positioned `right: 24px`, visually appearing under the "Book Now" button instead of the "MENU" toggle.

**Fix applied to all 16 HTML files:**
- Desktop: `right: 24px` → `left: 50%`
- Transform: added `translateX(-50%)` to both closed and `.open` states
- Mobile overrides: removed `right: 16px` (centering inherited from base; `width: calc(100vw - 32px)` with `translateX(-50%)` produces 16px margins each side)
- series.html: added missing mobile `top: 56px; width: calc(100vw - 32px)` override

**Note:** `shared-theme.css` has `right: 16px !important` in its mobile `@media` block (line 332). This does NOT conflict because CSS ignores `right` when both `left` and `width` are set on a `position: fixed` element.

**Review status:** Code review APPROVED. All 5 verification requirements passed across all 16 files.

---

### Task 4: Unified Font Brand Consistency — `fix/unified-font-brand-consistency`

**Commits:**
- `3cdd3b0` — fix: unify font families across all pages to match brand guide
- `c32eeca` — fix: add shared-theme.css and Outfit font import to clash.html

**Problem:** Sub-pages used Barlow/Barlow Condensed/Bebas Neue fonts while the brand reference (index.html) uses Outfit/DM Sans. `shared-theme.css` partially fixed this via `!important` but had gaps — 30+ selectors were not covered.

**Fix (shared-theme.css only — single file cascades to all 15 sub-pages):**

Added to heading/title group (`Outfit !important`):
- `.section-heading`, `.booking-card-title`, `.location-label`, `.location-name`
- `.info-pill`, `.hero-tag`
- `.pricing-label`, `.pricing-title`
- `.price-card-classes`, `.price-card-amount`, `.price-card-label`, `.price-card-per`, `.price-card-best-tag`
- `.price-option-label`, `.price-option-amount`, `.price-option-save`
- `.best-value-badge`, `.full-collection-label`, `.single-label`
- `.middle-section-label`, `.focus-label`
- `.card-presenter`, `.card-price-highlight`

Added to button group (`Outfit !important`):
- `.btn-book-now`, `.btn-book-series`, `.btn-book-primary`
- `.btn-book`, `.btn-more`, `.btn-design`, `.price-card-btn`

New rule added:
- `.menu-overlay a, .footer-links a { font-family: 'Outfit' !important }` — fixed live render deviation where inline `.menu-overlay a { Barlow }` was overriding the non-!important `a { DM Sans }` rule

**clash.html fix:** Was the only sub-page missing `shared-theme.css` link and Outfit/DM Sans Google Font import. Both added.

**Brand font system (enforced):**
- **Outfit** — headings, UI components, buttons, labels, badges, pricing, menu links
- **DM Sans** — body text, paragraphs
- **Bebas Neue** — hero display on index.html only

**Review status:** Code review APPROVED. All 30 new selectors verified against HTML files. No typos. index.html unaffected (doesn't load shared-theme.css).

---

## Files Modified This Session

| File | Changes |
|------|---------|
| `series.html` | Stripe links activated (5 price cards), dropdown centered, mobile override added |
| `lovers-rock.html` | Archived booking card, dropdown centered |
| `full-series.html` | Archived booking card, dropdown centered |
| `march-back-in-time.html` | Stripe link corrected, dropdown centered, noopener added |
| `shared-theme.css` | 30+ font selectors added, button group expanded, menu/footer link overrides |
| `clash.html` | Added shared-theme.css + Outfit font import, dropdown centered |
| `index.html` | Dropdown centered |
| `about.html` | Dropdown centered |
| `academy.html` | Dropdown centered |
| `coaching.html` | Dropdown centered |
| `contact.html` | Dropdown centered |
| `dancehall-royalty.html` | Dropdown centered |
| `in-ya-city.html` | Dropdown centered |
| `in-ya-city-adelaide.html` | Dropdown centered |
| `motherland.html` | Dropdown centered |
| `past-series.html` | Dropdown centered |
| `praise-flow.html` | Dropdown centered |
| `README.md` | Updated for V2 with current project state |

---

## What Was NOT Changed (Intentionally)

- **index.html** fonts/styles — It does NOT load `shared-theme.css` and is the brand reference. No font changes made to it.
- `netlify.toml` — CORS and cache headers are pre-existing concerns
- `netlify/functions/chat.js` — Input validation not in scope
- `chatbot.js` — No changes needed
- OG image meta tags — Pre-existing broken reference, flagged for future fix
- Inline Barlow `font-family` declarations in sub-pages — Left as dead code (shared-theme !important overrides them). Can be cleaned up in a future refactor.

---

## Git State

```
Remote: git@github.com:chubyesha/chubydice_v2.git (newly set — NOT pushed yet)

Branch tree (all unpushed):
main
  └── feat/wire-stripe-links-all-series (198c1cd, eba2613)
  └── fix/center-dropdown-navigation (2c6584f, 0639a4b)
  └── fix/unified-font-brand-consistency (3cdd3b0, c32eeca)
  └── docs/session-and-readme-update (current)
```

**User must push all branches manually.**

---

## Pre-existing Issues (Unchanged)

1. **Broken OG image** — `chuby-profile-CkJq2sVN.jpg` doesn't exist (all 16 pages)
2. **CORS wildcard** — `Access-Control-Allow-Origin: *` in netlify.toml and chat function
3. **Chat function** — No input validation or rate limiting
4. **`--border` CSS variable conflict** — shared-theme.css vs page-local definitions
5. **shared-theme.css mobile `right: 16px !important`** — Technically conflicts with centered dropdown `left: 50%`, but CSS resolves it correctly (right ignored when left + width both set)
