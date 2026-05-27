# MyRoomeo documentation

Product and engineering docs for this repo. These files are **not** loaded by the live site — they are for the team, collaborators, and AI tooling.

**Language:** English only.

---

## Quick index

| Document | Purpose | Status |
|----------|---------|--------|
| [result page.md](./result%20page.md) | Full product spec: quiz flow, 6 types, result page sections, share/compare vision | Active spec |
| [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md) | How `resolveType()` works — votes, mapping tables, examples | Matches `quiz.html` |
| [roomeo_landing.md](./roomeo_landing.md) | Landing page copy (sections, CTAs, positioning) | Copy reference |
| [roomeo-design.md](./roomeo-design.md) | Design tokens (colors, type, spacing) | Legacy — Sumu Hotel template |
| [roomeo-design-components.md](./roomeo-design-components.md) | Component specs | Legacy — Sumu Hotel template |
| [roomeo-design-guidelines.md](./roomeo-design-guidelines.md) | Accessibility & do's/don'ts | Legacy — Sumu Hotel template |

---

## By topic

### Quiz & results

1. **Product intent** → [result page.md](./result%20page.md)  
   What to build: questions, tone, result layout, compatibility story, viral/share goals.

2. **Scoring implementation** → [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md)  
   What the code actually does today in `quiz.html` (`QUIZ`, `TYPES`, `resolveType`).

3. **Live code** → [`../quiz.html`](../quiz.html)  
   Source of truth for UI and behavior.

### Marketing

- [roomeo_landing.md](./roomeo_landing.md) — hero, nav, sections, CTA copy for `index.html`.

### Design system (reference)

The three `roomeo-design*.md` files describe a **Sumu Hotel** design system (different brand). They were kept as a generic token/component reference. MyRoomeo’s live UI uses its own styles in `index.html` / `quiz.html` — do not assume these docs match production pixels.

---

## Conventions

| Rule | Detail |
|------|--------|
| Language | English |
| Filenames | Keep existing names unless renaming in a dedicated cleanup PR (some files use spaces) |
| Scoring doc | Single file: `quiz-scoring-logic-en.md` (no duplicate Chinese/English pair) |
| Updates | When quiz logic changes, update `quiz-scoring-logic-en.md` in the same PR |

---

## Suggested maintenance

- **After quiz changes** — sync [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md).
- **After result copy changes** — sync [result page.md](./result%20page.md) or mark sections as “implemented / deferred”.
- **After landing copy changes** — sync [roomeo_landing.md](./roomeo_landing.md).
- **Design system** — either rewrite `roomeo-design*.md` for MyRoomeo or move Sumu docs to an `archive/` folder if they cause confusion.

---

## Local preview

Docs are Markdown on GitHub. To preview locally, open files in your editor or use any Markdown viewer. The app itself:

```bash
python3 -m http.server 8765
# http://127.0.0.1:8765/quiz.html
```
