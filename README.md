# MyRoomeo

Personality-driven roommate matching — marketing landing page (`index.html`) and 12-question roommate type quiz (`quiz.html`).

**Brand:** MyRoomeo (logo: `assets/brand/logo02.svg`)

## Run locally

Opening HTML via `file://` can break paths. From the project root:

```bash
python3 -m http.server 8765
```

- Landing: **http://127.0.0.1:8765/**
- Quiz: **http://127.0.0.1:8765/quiz.html**
- Preview a result: **http://127.0.0.1:8765/quiz.html#turtle**

With Node.js:

```bash
npx --yes serve -l 8765
```

## Documentation

All docs live in [`docs/`](docs/). Start with **[docs/README.md](docs/README.md)**.

| Doc | What it covers |
|-----|----------------|
| [result page.md](docs/result%20page.md) | Quiz flow, result page, share/compare modals (matches `quiz.html`) |
| [quiz-scoring-logic-en.md](docs/quiz-scoring-logic-en.md) | Type assignment algorithm + full vote mapping |

Landing page and design live in [`index.html`](index.html) and [`quiz.html`](quiz.html) — no separate copy/design docs.

## Repository access

This GitHub repository is **private**. Invite collaborators under **Settings → Collaborators** (or **Manage access**).

## Asset layout

| Path | Contents |
|------|----------|
| `assets/brand/` | `logo02.svg` (nav), `logo.svg` |
| `assets/site/` | Landing imagery, trust bg, share QR placeholder |
| `assets/quiz/questions/` | `quiz cover.png`, `q1.png`–`q12` (q4, q10 are `.jpg`) |
| `assets/characters/` | Type avatars: `beaver.png` … `turtle.png` |
| `assets/result-hero/` | Result hero mascots per type (transparent PNG) |
| `assets/roommate-type-cards/` | Six cards on landing `#types` section |
| `assets/quiz-result-1-0/` | Legacy result SVG assets |
| `docs/` | Product + design Markdown (not loaded by pages) |

## Stack

Static HTML/CSS/JS — no build step. Quiz uses **html2canvas** (CDN) for share/compare card downloads.
