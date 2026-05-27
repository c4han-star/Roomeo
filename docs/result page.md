# MyRoomeo Quiz & Result Page — Implementation Spec

> **Source of truth:** [`quiz.html`](../quiz.html)  
> **Scoring detail:** [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md)  
> **Landing:** [`index.html`](../index.html)

This document describes **what is built today** in the vibe-coded prototype. Older spec items (pentagon charts, 21 pairing pages, dynamic dual-result compat) are listed under [§ Not built yet](#not-built-yet).

---

## 1) Project goal

MyRoomeo roommate type quiz:

- 12 lifestyle questions → one of **6 animal types**
- Highly shareable **result page** with personality copy
- **Share** via Instagram Story card download + copy link
- **Compare with a friend** via invite + compare card download
- Optional **profile** + **waitlist** UI (client-only, no API)

Tone: playful, viral, Gen Z, screenshot-friendly, sharp and specific.

---

## 2) User flow (implemented)

```text
quiz.html
  ├─ Intro (#quiz-intro) → Start the survey
  ├─ Q1–Q12 (#quiz-flow) → see results
  ├─ Results (#quiz-results) → applyResultUI()
  │     ├─ Build profile (#flow-profile-1 → #flow-profile-2)
  │     └─ Waitlist (#flow-waitlist)
  └─ Share pills → Share modal | Email modal | Compare modal
```

Back: results → intro clears session (except `roomeo_compare_friend`).

---

## 3) Survey structure

| Section | Questions | Count |
|---------|-----------|-------|
| 🧼 A. Cleanliness & Initiative | Q1–Q3 | 3 |
| 🎉 B. Social Energy & Guests | Q4–Q6 | 3 |
| 🧭 C. Structure vs Flexibility | Q7–Q10 | 4 |
| 🏠 D. Presence & Shared-Home Engagement | Q11–Q12 | 2 |

**Total:** 12 questions, 4 options each (A–D).

Type assignment: weighted animal votes via `resolveType()` — see [quiz-scoring-logic-en.md](./quiz-scoring-logic-en.md).

Auxiliary dimension scores (`answerScores`, A=4…D=1) feed profile prefill and “Why you got this” bullets — **they do not pick the type**.

---

## 4) Survey questions (live copy)

Questions and vote tags are defined in `QUIZ[]` in `quiz.html`. Full option → animal mapping is in [quiz-scoring-logic-en.md §3](./quiz-scoring-logic-en.md).

### A. Cleanliness & Initiative

**Q1.** Sprite at 2 a.m. — thirst, roommate asleep, unopened Sprite in fridge.  
**Q2.** Exhausted after cooking; dishes in the sink.  
**Q3.** Trash overflowing; nobody has taken it out.

### B. Social Energy & Guests

**Q4.** Brought someone over; roommate home early during intimate moment.  
**Q5.** Friday night, both home, no work tomorrow — ideal vibe?  
**Q6.** After 10:30 p.m., FaceTime / low music — not dead quiet.

### C. Structure vs Flexibility

**Q7.** Roommate hogs bathroom every morning.  
**Q8.** Messy sink, surprise guests, no quiet-hour agreement — what system?  
**Q9.** Roommate habits differ from yours — your instinct?  
**Q10.** How would your roommate describe living with you?

### D. Presence & Shared-Home Engagement

**Q11.** Saturday — where are you most likely?  
**Q12.** Roommate's fridge section leaked onto shared shelves.

Question art: `assets/quiz/questions/q1.png` … `q12.png` (q4, q10 are `.jpg`).

---

## 5) Six roommate types

Slugs: `beaver`, `cat`, `owl`, `fox`, `bunny`, `turtle`.

| slug | Display | Emoji | shareTrait (short) |
|------|---------|-------|-------------------|
| beaver | The Beaver | 🦫 | The unpaid landlord — structure, receipts… |
| cat | The Cat | 🐱 | The mystery guest — low presence… |
| owl | The Owl | 🦉 | The resident ghost — stealth kitchen runs… |
| fox | The Fox | 🦊 | The human tornado — creative clutter… |
| bunny | The Bunny | 🐰 | The main character — social battery infinite… |
| turtle | The Turtle | 🐢 | The couch CEO — packages signed… |

### `TYPES[slug]` fields

| Field | Result UI |
|-------|-----------|
| `name`, `emoji`, `subtitle` | Hero |
| `signatureQuote` | Quote block |
| `roast` | Roast paragraph |
| `stats[]` | Stat bars (`Label: N% — note`) — **static copy** |
| `whatLiving[]` | Living habits |
| `scenarios[]` | Main-character moments |
| `othersFeel[]` | The vibe check |
| `compat[]` | Compatibility radar (2 entries) |
| `survivalTip` + `idealBullets[]` | Survival manual |
| `whyFallback[]` | Why bullets when answers incomplete |
| `shareTrait` | Share / compare story cards |

Full long-form copy is in `quiz.html` `TYPES` object.

### Compatibility radar (static)

Each type has **2 preset** compat lines — Soulmate + Roommate war. Example (Beaver):

- 🦉 The Owl — Soulmate  
- 🐱 The Cat — Roommate war  

**Not** computed from two users' answers.

---

## 6) Result page sections

Rendered by `applyResultUI(typeKey, answers)`:

| Order | Section | DOM |
|-------|---------|-----|
| Hero | Your roommate type is | `#results-hero`, `#res-rfinal-*` |
| Ticker | Marquee | `.rfinal-ticker` |
| Quote | Signature quote | `#res-rfinal-quote` |
| Roast | | `#res-roast` |
| Stats | Progress bars | `#res-stats` |
| Why you got this | Dynamic or fallback | `#res-why-list` |
| Living habits | | `#res-live-with` |
| Main-character moments | | `#res-scenarios` |
| The vibe check | | `#res-others` |
| Compatibility radar | | `#res-compat` |
| Survival manual | | `#res-survival`, `#res-ideal` |
| What happens next | Profile CTAs | `#btn-build-profile`, `#btn-skip-profile` |
| Share | Speak your truth… | `#share-pill-*` |
| Footer | Retry, types link | `#btn-retry`, `index.html#types` |

**Hero constraint:** full-width split, mascot left, blue stripes right — hero only.

---

## 7) Share & compare

### Share results (`#share-results-modal`)

- Story card `#share-story-card`: MyRoomeo, emoji, type name, `shareTrait`, QR placeholder
- **Download image** — html2canvas @ 1080×1920 → `myroomeo-{slug}-share.png`
- **Copy link** — `shareUrl()` = page URL + `#slug`
- Clipboard text via `buildShareText()`

### Email results (`#email-results-modal`)

- Opens `mailto:` with share text body

### Compare with a friend (`#compare-friend-modal`)

**Step 1 — Form:** email, name, tips + terms checkboxes  
**Step 2 — Success:** compare card with inviter name/type, friend slot `?`, download PNG, copy link, Done

Invite copied on submit; stored in `sessionStorage.roomeo_compare_friend`.

QR: `assets/site/share-qr-placeholder.svg` (static, not generated).

---

## 8) Profile & waitlist

| Step | Storage key | Fields |
|------|-------------|--------|
| Profile 1 | `roomeo_profile_step1` | name, email, city |
| Profile 2 | `roomeo_profile_step2` | display, location, intro, rhythm, clean, social, homeEnergy |
| Waitlist | — | Success UI only |

`deriveLifestyle(answers)` prefills profile step 2 from dimension scores.

**No backend** — submit shows success state locally.

---

## 9) sessionStorage

| Key | Content |
|-----|---------|
| `roomeo_quiz_answers` | JSON array of 12 option indices (0–3) |
| `roomeo_type` | Result slug |
| `roomeo_profile_step1` | Profile step 1 object |
| `roomeo_profile_step2` | Profile step 2 object |
| `roomeo_compare_friend` | Compare form payload `{ email, name, tips, ts }` |

Cleared on quiz retry: first four keys.

---

## 10) Preview & debug

| Method | Example |
|--------|---------|
| Hash result | `quiz.html#turtle` — `bootFromHash()` |
| Figma capture | `quiz.html#figmacapture=1&previewResult=beaver` |
| Share link | `quiz.html#fox` |
| Console | `JSON.parse(sessionStorage.getItem('roomeo_quiz_answers'))` |

Note: `?previewResult=` alone in search params does **not** work — Figma preview uses hash query.

---

## 11) Dependencies & assets

- **html2canvas** 1.4.1 (CDN) — share/compare PNG export
- Logo: `assets/brand/logo02.svg`
- Characters: `assets/characters/{slug}.png`
- Result hero: `assets/result-hero/{slug}.png`

---

## Not built yet

Items from earlier product spec **not** in current `quiz.html`:

1. Second user completes quiz → **dynamic compatibility %** at bottom of their result
2. **21 pairing-specific** compat result pages
3. **Pentagon / radar chart** on share card (share card uses `shareTrait` text instead)
4. **Real QR** encoding of share URL
5. **Backend** waitlist, matching, verified profiles
6. Stats % **derived from live answers** (currently static in `TYPES`)
7. `buildTraitGridHtml()` — defined but not mounted on UI
8. Native Instagram/TikTok share (`shareInstagram` / `shareTikTok` — no listeners)

---

## Code index

| Symbol | Role |
|--------|------|
| `QUIZ` | 12 questions + votes |
| `TYPES` | All type copy |
| `resolveType()` | Type winner |
| `applyResultUI()` | Fill result DOM |
| `getWhyBullets()` | Dynamic why list |
| `showResults()` | Post-quiz entry |
| `openShareResultsModal()` | Share dialog |
| `openCompareFriendModal()` | Compare dialog |
| `downloadStoryCardPng()` | html2canvas export |

Line numbers drift — grep `quiz.html` for definitions.
