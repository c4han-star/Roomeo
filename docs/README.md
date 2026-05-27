# MyRoomeo documentation

Product and engineering docs for this repo. These files are **not** loaded by the live site — they mirror the vibe-coded prototype in `index.html` and `quiz.html`.

**Language:** English only. **Source of truth for behavior:** the HTML files; update docs when code changes.

---

## Quick index

| Document | Purpose | Synced to |
|----------|---------|-----------|
| [result page.md](./result%20page.md) | Quiz flow, result sections, share/compare, profile, storage | `quiz.html` |
| [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md) | `resolveType()` votes, mapping tables, examples | `quiz.html` |
| [roomeo_landing.md](./roomeo_landing.md) | Landing copy, nav, sections, CTAs | `index.html` |
| [roomeo-design.md](./roomeo-design.md) | Colors, type, spacing tokens | CSS in both pages |
| [roomeo-design-components.md](./roomeo-design-components.md) | UI components (landing + quiz) | Both pages |
| [roomeo-design-guidelines.md](./roomeo-design-guidelines.md) | Hero rules, voice, a11y, don'ts | Team conventions |

---

## By topic

### Quiz & results

1. **What’s built** → [result page.md](./result%20page.md)  
2. **How types are scored** → [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md)  
3. **Live code** → [`../quiz.html`](../quiz.html)

### Marketing

- [roomeo_landing.md](./roomeo_landing.md) — [`../index.html`](../index.html)

### Design

- [roomeo-design.md](./roomeo-design.md) — tokens  
- [roomeo-design-components.md](./roomeo-design-components.md) — components  
- [roomeo-design-guidelines.md](./roomeo-design-guidelines.md) — rules (incl. locked result hero)

---

## Conventions

| Rule | Detail |
|------|--------|
| Brand | **MyRoomeo**, logo `assets/brand/logo02.svg` |
| Scoring doc | Single file: `quiz-scoring-logic-en.md` |
| Copy changes | Update `quiz.html` / `index.html` first, then sync docs |

---

## Local preview

```bash
python3 -m http.server 8765
# http://127.0.0.1:8765/
# http://127.0.0.1:8765/quiz.html#turtle
```
