# MyRoomeo Design System — Token Reference

> **Source of truth:** inline CSS in [`index.html`](../index.html) and [`quiz.html`](../quiz.html)  
> For components see [roomeo-design-components.md](roomeo-design-components.md). For rules see [roomeo-design-guidelines.md](roomeo-design-guidelines.md).

MyRoomeo uses a warm, editorial aesthetic: cream paper backgrounds, espresso ink, coral accents, Fraunces display type. The quiz result page (`rfinal-*`) has its own extended token set.

---

## Brand

| Item | Value |
|------|-------|
| Product name | **MyRoomeo** |
| Logo (nav) | `assets/brand/logo02.svg` |
| Tone | Playful, Gen Z–friendly, personality-heavy, screenshot-able |

---

## Colors — shared

| Token / role | Hex | Usage |
|--------------|-----|-------|
| `--primary` | `#000000` | Primary buttons, strong CTAs |
| `--primary-hover` | `#333333` | Button hover |
| `--bg` / `--landing-surface` | `#FFFFFF` | Cards, nav surface |
| `--page-bg` / `--house-cream` | `#f9f5ed` | Page background (quiz, house section) |
| `--paper` / `--rfinal-paper` | `#FAF6EF` | Result page paper tone |
| `--ink` / `--rfinal-ink` | `#2D1B14` | Headlines, body |
| `--ink-soft` / `--rfinal-ink-soft` | `#4A3228` | Secondary text |
| `--ink-mute` / `--rfinal-mute` | `#6B5A50` | Muted labels |
| `--accent-coral` | `#ff6a2a` | Quiz progress, accents |
| `--accent-warm` / `--rfinal-accent` | `#D96C4B` | Warm CTAs, highlights |
| `--rfinal-sky` | `#B8D4E3` | Hero stripe accent (result hero only) |
| `--warm-line` / `--landing-line` | `rgba(74, 50, 40, 0.1)` | Dividers |
| `--link` | `#0066CC` | Text links |

---

## Typography

| Role | Stack |
|------|-------|
| Display | `'Fraunces', Georgia, serif` — `--font-display`, `--font-rfinal-display` |
| Body | `'Roboto', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif` — `--font-rfinal-body` |

Loaded via Google Fonts on both pages.

---

## Radius & spacing

| Token | Value |
|-------|-------|
| `--r-sm` | `4px` |
| `--r-md` | `8px` |
| `--r-lg` | `12px` (landing) / `16px` (quiz) |
| `--r-xl` | `20px` (quiz) |
| `--landing-radius` / `--rfinal-radius` | `24px` |
| `--max-w` | `1200px` (landing) |
| `--split-max` | `1080px` (quiz split layout) |
| `--ease` / `--rfinal-ease-out` | `cubic-bezier(0.4, 0, 0.2, 1)` |

Landing section spacing: `--landing-section-gap: clamp(72px, 8vw, 96px)`.

---

## Shadows

| Token | Value |
|-------|-------|
| `--landing-shadow` | `0 8px 32px rgba(45, 27, 20, 0.06)` |
| `--rfinal-shadow-sm` | `0 2px 14px rgba(45, 27, 20, 0.05)` |
| `--rfinal-shadow-md` | `0 8px 32px rgba(45, 27, 20, 0.08)` |

---

## Quiz-specific

| Token | Purpose |
|-------|---------|
| `--segment-todo` | `#ececec` — unanswered progress segments |
| `--accent-coral` | Current question segment |
| `--quiz-footer-h` | `108px` — fixed footer height |
| `--quiz-art-min-h` | Question illustration panel min height |

---

## Result page (`rfinal-*`)

Result hero (`.rfinal-hero` / `#results-hero`):

- Full-width split layout: mascot left, decorative vertical stripes right
- Mascot from `assets/result-hero/{slug}.png`, fallback `assets/characters/{slug}.png`
- Blue stripe decoration is **hero-only** — do not repeat elsewhere on the page

Body sections use `.rfinal-sec`, `.rfinal-sec-title`, `.result-list` on `--rfinal-paper` background.

---

## Share / compare story cards

- Aspect ratio **9:16** (1080×1920 export via html2canvas)
- Brand label: **MyRoomeo**
- QR placeholder: `assets/site/share-qr-placeholder.svg`
