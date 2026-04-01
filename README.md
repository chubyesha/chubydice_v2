# Chuby Dice Website — Version 2

Official website for **Chuby Dice** — Dancehall artist, educator, and cultural practitioner based in Naarm (Melbourne), Australia.

**Live site:** [chubydice.com](https://www.chubydice.com)
**Hosting:** Netlify
**Repo:** [github.com/chubyesha/chubydice_v2](https://github.com/chubyesha/chubydice_v2)

---

## Project Structure

```
chubydice_version_2/
├── index.html                  # Home page (hero video, series tiles, coaching, academy, artist, vibes, connect)
├── series.html                 # Chuby Dice Series — all current series + collection pricing (Stripe live)
├── praise-flow.html            # Praise Flow series (April 2026) — 5-tier Stripe pricing
├── motherland.html             # Motherland series (May 2026) — 5-tier Stripe pricing
├── dancehall-royalty.html       # Dancehall Royalty series (June 2026) — 5-tier Stripe pricing
├── march-back-in-time.html     # March Back in Time series (March 2026) — active, Stripe linked
├── lovers-rock.html            # Lovers' Rock series (archived — Feb 2026)
├── full-series.html            # Full series collection page (archived — Q1 2026)
├── past-series.html            # 2026 Events archive / past sessions
├── clash.html                  # Clash Inna Dancehall with Passion Studio (Coming Soon)
├── coaching.html               # Professional 1:1 Coaching & Programs (Stripe live)
├── academy.html                # Dancehall Academy — Launching 2026
├── about.html                  # About Chuby Dice (biography with accordion sections)
├── contact.html                # Contact / Instagram
├── in-ya-city.html             # Chuby Dice in Ya City
├── in-ya-city-adelaide.html    # In Ya City — Adelaide (past session)
├── shared-theme.css            # Shared design system — unified typography, theme tokens, nav/button overrides
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify.toml                # Netlify config (redirects, headers, cache rules)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers
├── videos/                     # Hero background videos
├── documents/                  # Session recovery, resume instructions, client notes
├── screenshots/                # UI reference screenshots (gitignored)
└── .gitignore                  # IDE, node_modules, .env, screenshots, .claude, etc.
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Each page is self-contained with inline `<style>` and `<script>`.
- **Shared Theme** — `shared-theme.css` provides site-wide design tokens, unified typography, nav styling, and font overrides via `!important` cascade.
- **Fonts** — Outfit (headings, UI components, buttons, labels, badges), DM Sans (body text, paragraphs), Bebas Neue (hero display only on index.html).
- **Design Tokens** — Purple-dominant palette (`--void`, `--deep`, `--surface`, `--purple-600`, `--gold`, `--pink`, `--cyan`).
- **Netlify Functions** — Serverless chat endpoint at `/.netlify/functions/chat` using Anthropic Claude API.
- **Stripe** — Live payment links (`buy.stripe.com`) on series.html (5 class pass tiers), individual series pages, and coaching.html.

## Stripe Pricing (Live)

| Package | Price | Per Class | Stripe Link |
|---------|-------|-----------|-------------|
| Single Class | $30 | $30 | `...5cX4F20b` |
| 4 Classes | $100 | $25 | `...fRB4F20c` |
| 5 Classes | $125 | $25 | `...bBl4F20d` |
| 10 Classes | $230 | $23 | `...cFp4F20e` |
| 20 Classes | $450 | $22.50 | `...8p94F20f` |

These links are active on: `series.html`, `praise-flow.html`, `motherland.html`, `dancehall-royalty.html`, `march-back-in-time.html`.

**Archived series** (Stripe links removed): `lovers-rock.html`, `full-series.html`.

## Pages Overview

### Home (`index.html`)
- Hero video (`videos/hero-bg.mp4`) with poster fallback
- Series tiles grid (March Back in Time, Praise Flow, Motherland, Dancehall Royalty)
- 1:1 Coaching tile, Academy section, Artist bio, Dancehall Vibes playlist, Social connect
- Mobile: horizontal scroll with swipe dots
- Does NOT load `shared-theme.css` — fully self-contained styles

### Series (`series.html`)
- Individual series cards with images and booking buttons
- **Collection Pricing** section: 5 tiers — all Stripe links live and active

### Coaching (`coaching.html`)
- Hero with watermark background
- Expandable accordion with 5 coaching focus areas
- Booking card with live Stripe link

### About (`about.html`)
- Photo mosaic hero (auto-scrolling lanes)
- Biography in 6 collapsible accordion sections (first open by default)

## Navigation

All 16 pages share a centered dropdown menu (positioned below the MENU toggle):

1. Home
2. Chuby Dice Series
3. Clash Inna Dancehall
4. Professional 1:1 Coaching & Programs
5. Dancehall Academy — Launching 2026
6. About Chuby Dice
7. Brand Ambassadorship
8. Chuby Dice in Ya City
9. 2026 Events (Archive)
10. Contact / Instagram

**Dropdown positioning:** `left: 50%; transform: translateX(-50%)` — centered below MENU button on desktop, full-width on mobile.

## Font System

The brand font hierarchy (enforced via `shared-theme.css` with `!important`):

| Role | Font | Used for |
|------|------|----------|
| Headings / UI | **Outfit** | Nav, buttons, labels, badges, pricing, headings, menu overlay links |
| Body text | **DM Sans** | Paragraphs, descriptions, footer text |
| Display (index only) | **Bebas Neue** | Hero title on index.html only |

All 15 sub-pages load `shared-theme.css` which enforces Outfit/DM Sans via `!important`, overriding any inline Barlow/Barlow Condensed declarations.

## Development

No build step required. Open any `.html` file directly or serve with any static server.

```bash
npx serve .
# or
python3 -m http.server 8000
```

For Netlify Functions (chatbot):
```bash
npx netlify dev
```

## Git Workflow

- **main** — Production branch. Do not checkout or merge directly.
- Feature branches: `feat/<description>`
- Fix branches: `fix/<description>`
- Docs branches: `docs/<description>`
- Chore branches: `chore/<description>`

## Known Pre-existing Issues

1. **OG image broken** — All pages reference `chuby-profile-CkJq2sVN.jpg` which doesn't exist.
2. **CORS wildcard** — `netlify.toml` and chat function use `Access-Control-Allow-Origin: *`. Should restrict to actual domain.
3. **Chat function** — No input validation or rate limiting on the Netlify chat function.
4. **`--border` CSS variable** — Conflict between `shared-theme.css` (`rgba(255,255,255,0.08)`) and page-local definitions (`#242424`).

---

Site made and managed by BBK Productions.
