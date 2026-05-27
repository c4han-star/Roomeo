# MyRoomeo Design Guidelines

> Tokens: [roomeo-design.md](roomeo-design.md) · Components: [roomeo-design-components.md](roomeo-design-components.md)

---

## Brand & voice

- Use **MyRoomeo** (not standalone “Roomeo”) in user-facing copy
- Tone: playful, specific, roast-friendly, shareable — Gen Z / viral quiz energy
- Result copy lives in `TYPES` in `quiz.html` — avoid generic SaaS language

---

## Result hero (locked layout)

These constraints apply to `#results-hero` / `.rfinal-hero`:

- **Full-width split hero** — mascot on the left, decorative element on the right
- **Blue vertical stripes** belong **only** in the hero — do not add stripe motifs to body sections
- Do not replace hero with dark SaaS card layouts
- Mascot: `assets/result-hero/{slug}.png` with character fallback
- Logo in header: `assets/brand/logo02.svg`

---

## Visual do's

- Warm cream backgrounds (`#f9f5ed`, `#FAF6EF`) with espresso text
- Fraunces for display headlines; Roboto for body
- Coral (`#ff6a2a`) for quiz progress and energetic accents
- Generous radius (`24px`) on landing cards and result sections
- Share/compare cards at **9:16** for Instagram Story export

---

## Visual don'ts

- No dark generic “dashboard” result cards
- No `icon1.png` / `icon2.png` / `icon3.png` vibe pill patterns from old mocks
- No blue stripe decoration outside the result hero
- Do not change result hero structure unless explicitly requested

---

## Accessibility

- Quiz options keyboard-accessible (1–4 keys)
- Dialog modals use native `<dialog>` with `aria-controls` on share pills
- Hero emoji marked `aria-hidden` where redundant with type name text
- SR-only headings where visual hierarchy differs (`#res-headline`, `#res-tagline`)

### Contrast

- Primary text `#2D1B14` on `#FAF6EF` / `#FFFFFF` — sufficient for body copy
- Links `#0066CC` on white — use underline on inline links where clarity matters

### Touch targets

- Share pills and quiz footer buttons sized for mobile tap (min ~44px height)

---

## Copy changes

- **Only update marketing/result copy when explicitly requested** — docs should mirror code, not the reverse
- Landing copy: `index.html` + [roomeo_landing.md](roomeo_landing.md)
- Quiz questions + types: `quiz.html` `QUIZ` / `TYPES` + [result page.md](result%20page.md)

---

## Assets

- Prefer existing paths under `assets/` — see root [README.md](../README.md)
- Question art: one file per question in `assets/quiz/questions/`
- Cache busters on character images: `?v=20260418`

---

## Share & compare

- QR codes are **placeholder SVG** until real deep-link QR is ready
- Copy link format: `{origin}/quiz.html#{typeSlug}` (e.g. `#fox`)
- Download filenames: `myroomeo-{slug}-share.png`, `myroomeo-{slug}-compare.png`

---

## Not implemented (don't document as live)

- Dynamic two-person compatibility score after friend completes quiz
- Real backend for profile / waitlist / verified profiles
- Instagram/TikTok native share handlers (`shareInstagram()` exists but has no listeners)
