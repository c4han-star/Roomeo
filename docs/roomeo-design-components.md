# MyRoomeo Components

> Component specs extracted from [`index.html`](../index.html) and [`quiz.html`](../quiz.html).  
> Tokens: [roomeo-design.md](roomeo-design.md) · Rules: [roomeo-design-guidelines.md](roomeo-design-guidelines.md)

---

## Landing (`index.html`)

### Navigation (`.nav`)

- Fixed top bar, logo + anchor links + **Take the quiz** pill
- `.scrolled` state after 10px scroll
- Mobile hamburger toggles menu class (no separate panel markup)

### Hero (`.landing-hero`)

- Split: copy left, mascot right (`banner.png`)
- Primary: filled dark CTA → quiz
- Secondary: text link → `#types`

### Feature columns (`.feature-col`)

- Three tilted cards (`--feature-tilt` per column)
- Photo + H3 + body + text link with arrow SVG

### Trust block (`.landing-trust`)

- Full-width quote over background image + silhouette overlay

### How it works (`.landing-how`)

- Three numbered steps in a row

### Roommate type cards (`.personality-section`)

- Six large PNG cards in `.house-wrap` cream section
- Card CTA button with inline arrow SVG

### Final CTA (`.final-cta`)

- Full-bleed background image, centered headline + button

### Footer (`.footer`)

- Copyright + four social icon links (SVG inline)

---

## Quiz (`quiz.html`)

### Split layout (`#quiz-split-wrap`)

- Left: `#quiz-art-panel` — question illustration (`#quiz-art-img`)
- Right: intro / questions / results stack

### Quiz intro (`#quiz-intro`)

- Cover art: `assets/quiz/questions/quiz cover.png`
- **Start the survey** → `#btn-start`

### Quiz flow (`#quiz-flow`)

- Section label + question text + four option buttons
- Progress: `#progress-segments` (12 segments, coral = current)
- Fixed footer: `#quiz-flow-footer` with **back** + **continue** / **see results**
- Keyboard: keys 1–4 select options

### Result hero (`#results-hero`, `.rfinal-hero`)

- Kicker: “Your roommate type is”
- Emoji + type name, subtitle, mascot image
- **Do not change layout** — full-width split, mascot left, blue stripes right

### Result sections (`.rfinal-sec`)

| Section | ID | Content source |
|---------|-----|----------------|
| Quote | `#res-rfinal-quote` | `TYPES[].signatureQuote` |
| Roast | `#res-roast` | `TYPES[].roast` |
| Stats | `#res-stats` | `TYPES[].stats` (progress bars) |
| Why you got this | `#res-why-list` | `getWhyBullets()` or `whyFallback` |
| Living habits | `#res-live-with` | `whatLiving` |
| Main-character moments | `#res-scenarios` | `scenarios` |
| The vibe check | `#res-others` | `othersFeel` |
| Compatibility radar | `#res-compat` | `compat` (2 cards: Soulmate + Roommate war) |
| Survival manual | `#res-survival`, `#res-ideal` | `survivalTip` + `idealBullets` |
| What happens next | `#btn-build-profile`, `#btn-skip-profile` | Profile flow entry |

### Share pills (`.share-pills`)

Three buttons on results + waitlist:

| ID | Action |
|----|--------|
| `#share-pill-share` | Open share modal |
| `#share-pill-email` | Open email modal (`mailto:`) |
| `#share-pill-compare` | Open compare-with-friend modal |

### Share results modal (`#share-results-modal`)

- 9:16 preview `#share-story-card` (MyRoomeo, type, emoji, `shareTrait`, QR placeholder)
- **Download image** → PNG via html2canvas
- **Copy link** → `quiz.html#{slug}`

### Compare friend modal (`#compare-friend-modal`)

Two steps:

1. **Form** — email, name, tips checkbox, terms checkbox; submit copies invite
2. **Success** — compare story card (You vs Friend `?`), download PNG, copy link, Done

### Profile flow

| Panel | Fields |
|-------|--------|
| `#flow-profile-1` | Name, email, city |
| `#flow-profile-2` | Photo, intro, rhythm/clean/social (prefilled via `deriveLifestyle()`) |
| `#flow-waitlist` | Success state + share pills (no API) |

### Buttons

| Class | Use |
|-------|-----|
| `.card-btn` | Quiz continue (dark pill + arrow tail) |
| `.btn-back-quiz` | Quiz back |
| `.share-pill` | Share actions (icon + label) |
| `.share-copy-link-btn` | Modal secondary actions |

---

## Modals

All use `<dialog>` with `.share-modal-dialog` styling (wide, story-card preview area).

Toast feedback: `#share-modal-toast`, `#compare-modal-toast`.

---

## Animation

- Landing: `.fade-up` + IntersectionObserver scroll reveal
- Results: `scheduleResultsReveal()` stagger on sections
