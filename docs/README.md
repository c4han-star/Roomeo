# MyRoomeo documentation

Product and engineering docs for this repo. These files are **not** loaded by the live site.

**Source of truth for UI and copy:** [`index.html`](../index.html) and [`quiz.html`](../quiz.html).

**Language:** English only.

---

## Docs

| Document | Purpose |
|----------|---------|
| [result page.md](./result%20page.md) | Quiz flow, result page, share/compare, profile — matches `quiz.html` |
| [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md) | Type assignment algorithm + full vote mapping |

---

## Local preview

```bash
python3 -m http.server 8765
# http://127.0.0.1:8765/
# http://127.0.0.1:8765/quiz.html#turtle
```
