# Sumu Hotel Guidelines — Accessibility & Do's/Don'ts

> See [design.md](design.md) for token values. See [design-components.md](design-components.md) for component specs.

## Accessibility

### Contrast Requirements

| Requirement | Ratio |
|---|---|
| WCAG AA Normal Text | 4.5:1 |
| WCAG AA Large Text (18pt+/14pt bold) | 3:1 |
| WCAG AAA Normal Text | 7:1 |
| UI Components & Graphical Objects | 3:1 |

| Component | 3:1 Against |
|---|---|
| Buttons | #666666 minimum (text on #FFFFFF) |
| Links | #0066CC minimum (underlined for clarity) |
| Form labels | #1a1a1a on #FFFFFF |
| Disabled text | #999999 acceptable for disabled states |

### Touch Targets

- Minimum touch target: 48×48dp (or 44×44dp if unavoidable, with 8dp padding).
- Button minimum height: 40dp; minimum width: 64dp.
- Spacing between interactive targets: ≥ 8dp.
- Density: use comfortable spacing on mobile; reduce slightly on desktop only if >= 48dp.
- Link padding: 4dp horizontal, 2dp vertical minimum.

### Keyboard Navigation

| Key | Action |
|---|---|
| Tab | Move focus forward through interactive elements |
| Shift + Tab | Move focus backward |
| Enter | Activate focused button or link |
| Space | Toggle checkbox/switch; activate button |
| Escape | Close modals, popovers, dropdowns |
| Arrow Keys | Navigate within lists, tabs, sliders |

### Assistive Technology

- All interactive elements must have semantic HTML (`<button>`, `<a>`, `<input>`, `<label>`).
- Use `aria-label` or `aria-labelledby` for icon-only buttons.
- Form inputs must have associated `<label>` elements.
- Use `aria-live="polite"` for dynamic content updates.
- Links must have descriptive anchor text (avoid "Click here").
- Images require `alt` text; decorative images use `alt=""`.
- Use `aria-pressed`, `aria-selected`, `aria-expanded` for state indication.
- Focus indicators must be visible (outline, ring, or highlight); never remove.

## Gestures

| Gesture | Use |
|---|---|
| Tap | Activate buttons, links, navigate |
| Double-tap | Zoom images on mobile (if enabled); zoom form inputs to prevent auto-zoom |
| Long-press | Context menus, tooltips; ≥ 500ms |
| Swipe | Carousel navigation, drawer open/close |
| Pinch-zoom | Image galleries (optional, consider fixed aspect ratios) |

## Content Design

**Writing rules:**
- Use sentence case for labels and button text (not Title Case).
- Keep button labels concise (1–3 words, ≤ 20 characters where possible).
- Line length: 50–75 characters for body text (optimal reading).
- Avoid jargon; use plain language.
- End buttons/labels with no punctuation; end full sentences with periods.
- Capitalization: Headlines use Title Case; body and labels use sentence case.
- Labels for form fields: use nouns or noun phrases (e.g., "Email address" not "Enter email").

## Do's and Don'ts

### Color
- **Do** use #000000 black for primary CTAs; ensure 4.5:1 contrast minimum.
- **Don't** rely on color alone to convey meaning (e.g., red error state needs icon + text).
- **Do** maintain consistent color usage across the site (primary always = black, success always = green).
- **Don't** use more than 3 accent colors in a single view.

### Shape
- **Do** use 4px radius for small interactive elements (buttons, inputs).
- **Don't** mix corner radii styles within the same component family.
- **Do** apply 8px radius to cards and medium containers for consistency.
- **Don't** use sharp corners (0px) for interactive elements.

### Elevation
- **Do** lift cards on hover (Level 1 shadow, 200ms transition).
- **Don't** stack multiple shadows; use a single, appropriate level.
- **Do** reserve Level 4 shadows for modals and full-screen overlays only.
- **Don't** apply shadows to text or small UI elements.

### Interaction
- **Do** provide clear visual feedback on all interactive states (hover, focus, pressed, disabled).
- **Don't** remove native focus indicators (outline, ring); customize if necessary.
- **Do** use 200ms–300ms transitions for state changes.
- **Don't** use instant state changes without transition feedback.
- **Do** disable buttons when form validation fails.
- **Don't** allow users to submit invalid data.

### Layout
- **Do** use 8dp baseline grid; keep all spacing multiples of 8 (8, 16, 24, 32, 48).
- **Don't** use arbitrary spacing values.
- **Do** apply 16dp padding inside cards on mobile; 32dp on desktop.
- **Don't** use full-width content on screens > 1024px without max-width container.
- **Do** test responsive behavior at 320px, 768px, and 1024px minimum.

### Typography
- **Do** use 16px body text minimum for readability.
- **Don't** use font sizes < 12px for body content.
- **Do** set line height ≥ 1.5 for body text.
- **Don't** use all-caps for body text; use for headings sparingly.
- **Do** pair headlines with generous line height (1.2–1.3).

### Motion
- **Do** use motion to guide user attention and provide feedback.
- **Don't** animate for decoration; every motion must have purpose.
- **Do** use standard easing curves (cubic-bezier presets).
- **Don't** use durations > 500ms for standard transitions.
- **Do** respect `prefers-reduced-motion` media query; disable animations for users who prefer reduced motion.

### Components
- **Do** use consistent button styles across all contexts (primary, secondary, tertiary).
- **Don't** create one-off button styles.
- **Do** clearly mark required form fields with asterisk (*) and aria-required.
- **Don't** use placeholder text as the only label.
- **Do** group related form fields with fieldsets and legends.
- **Don't** nest buttons or interactive elements within each other.

---