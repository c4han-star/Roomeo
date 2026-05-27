# MyRoomeo Landing Page — Production Copy

> **Source of truth:** [`index.html`](../index.html)  
> **Last synced:** vibe-coded build (MyRoomeo branding, `logo02.svg`)

---

## Product positioning

MyRoomeo helps people **search, match, and connect** with roommates based on how they actually live — sleep schedules, cleanliness, social energy — not just rent and location.

Primary conversion: **Take the quiz** → `quiz.html` (~3 minutes, no account needed).

---

## 0. Top navigation

| Item | Target |
|------|--------|
| Logo (MyRoomeo) | `/` |
| How it works | `#how` |
| Roommate types | `#types` |
| About | `#about` |
| Log in | Button only (not wired) |
| **Take the quiz** | `quiz.html` |

Logo asset: `assets/brand/logo02.svg`

---

## 1. Hero

| Element | Copy |
|---------|------|
| Kicker | For people who share a home |
| H1 line 1 | Find a roommate who fits. |
| H1 line 2 | Not just the space. |
| Lead | Search, match, and connect with confidence. Every living situation deserves a good start. |
| Primary CTA | **Take the quiz** → `quiz.html` |
| Secondary | **See the six types** → `#types` |
| Note | About 3 minutes · no account needed |

Hero mascot: `assets/site/banner.png`

---

## 2. Features / About (`#about`)

**Label:** Why MyRoomeo  

**H2:** Find a room, save with roommates, or list your space to earn  

**Lead:** MyRoomeo helps you search, match, and connect with confidence, so every living situation starts off right.

### Three feature columns

| H3 | Body | Link |
|----|------|------|
| Live with someone who gets you | Sleep schedules, cleanliness, social energy — the stuff that actually matters when you share a kitchen. | Find your match → `quiz.html` |
| No surprises. No guesswork | Real preferences up front, so you're not learning someone's habits after you've signed the lease. | Browse safely → `#` (placeholder) |
| Find or list a room | The space matters — but the person you share it with matters more. | Find or list a room → `#` (placeholder) |

Images: `assets/site/feature-living-room.png`, `feature-sofa-conversation.png`, `feature-vintage-bedroom.png`

---

## 3. Trust quote block

**Quote:** Feel confident every step of the way. Real preferences, verified profiles, no guesswork before move-in day.  

**Cite:** That's the whole point.

Background: `assets/site/trust-bg.png`, silhouette: `assets/site/trust-silhouette.png`

---

## 4. How it works (`#how`)

**Label:** How it works  

**H2:** Three steps to your perfect match

| Step | Title | Body |
|------|-------|------|
| 1 | Answer real-life questions | Quick questions about how you actually live at home. |
| 2 | Get your roommate type | Find out your home personality, and what kind of roommate you really are. |
| 3 | Match with compatible people | Connect with roommates who share your rhythm and respect your space. |

---

## 5. Roommate types (`#types`)

**Label:** Roommate types  

**H2:** Which one are you?

Six cards (image only in HTML — no per-type blurbs on landing):

| Type | Asset |
|------|-------|
| The Beaver | `assets/roommate-type-cards/RoommateTypeCard_beaver.png` |
| The Bunny | `RoommateTypeCard_bunny.png` |
| The Cat | `RoommateTypeCard_cat.png` |
| The Fox | `RoommateTypeCard_fox.png` |
| The Owl | `RoommateTypeCard_owl.png` |
| The Turtle | `RoommateTypeCard_turtle.png` |

**CTA:** Find your type → → `quiz.html`

---

## 6. Final CTA

| Element | Copy |
|---------|------|
| H2 | Ready to meet your match? |
| Body | Build your profile and connect with roommates who live like you do. |
| Button | **Start my profile** — button only (not wired to quiz or profile) |

Background: `assets/site/background-image-02.png` (CSS)

---

## 7. Footer

**Copyright:** © 2026 MyRoomeo. All rights reserved.

Social links (generic platform homepages): Facebook, Instagram, X, TikTok.

---

## Typography & fonts

- **Display:** Fraunces (Google Fonts)
- **Body:** Roboto (Google Fonts)

---

## User flow (implemented)

```text
index.html → Take the quiz → quiz.html → results → optional profile → waitlist
```

Landing does **not** embed the quiz. All quiz CTAs point to `quiz.html`.

---

## Placeholders / not wired

- Log in button
- Browse safely / Find or list a room links (`#`)
- Final CTA “Start my profile” button
- Verified profiles (copy claim only — no backend)
