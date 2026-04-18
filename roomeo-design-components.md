# Sumu Hotel Components

> Full specifications for all 24 components. Grouped by workflow.
> For tokens see [design.md](design.md). For rules & accessibility see [design-guidelines.md](design-guidelines.md).

## Actions

### Button

**Types/Variants:**

| Type | Use |
|---|---|
| Primary | Single most important action (black, solid) |
| Secondary | Alternative actions (white bg, black border) |
| Tertiary | Low-emphasis actions (text-only, black underline) |
| Disabled | Unavailable actions (50% opacity, no pointer events) |

**Specs:**

| Property | Value |
|---|---|
| Height | 40dp minimum |
| Min Width | 64dp |
| Padding | 8dp vertical, 16dp horizontal |
| Border Radius | 4px |
| Touch Target | 48×48dp minimum |
| States | Rest, Hover, Focus, Pressed, Disabled |
| Typography | Label Large (14px, 600 weight) |
| Transition | 200ms standard easing on all state changes |

**Content rules:**
- Use sentence case; capitalize only the first word (e.g., "View rooms" not "View Rooms").
- Keep labels 1–3 words, ≤ 20 characters.
- Use action verbs (View, Book, Explore, Learn more).
- No trailing punctuation.

**Do/Don't:**
- **Do** use primary button for the single most important action per view.
- **Don't** use primary for multiple buttons in the same group.

**Accessibility:**
- All buttons must have semantic `<button>` tag.
- Icon-only buttons require `aria-label`.
- Focus ring must be visible (outline 2px solid at 4px offset).
- Disabled buttons must have `aria-disabled="true"` and remove from tab order.

---

### Link

**Types/Variants:**

| Type | Use |
|---|---|
| Default | Inline text links within paragraphs |
| External | Links to external sites (icon + underline) |
| Subtle | Secondary navigation or metadata links (muted color) |

**Specs:**

| Property | Value |
|---|---|
| Color | #0066CC default, #005AA0 on hover |
| Text Decoration | Underline (always underlined for visibility) |
| Transition | 200ms color change |
| Focus Ring | 2px solid, 4px offset |

**Content rules:**
- Use descriptive link text (e.g., "View room details" not "Click here").
- Avoid acronyms without explanation.
- End links with no punctuation unless within a sentence.

**Do/Don't:**
- **Do** underline all links for WCAG compliance and clarity.
- **Don't** remove underlines to reduce visual clutter.

**Accessibility:**
- Semantic `<a>` tag with `href` attribute.
- Descriptive text content (no empty links).
- `aria-label` for icon-only links.
- External links marked with `aria-label="Opens in new window"` or visual indicator.

---

### FAB (Floating Action Button)

**Types/Variants:**

| Type | Use |
|---|---|
| Default | Primary floating action (book, contact) |
| Extended | FAB with label + icon |

**Specs:**

| Property | Value |
|---|---|
| Size | 56×56dp (default), 48×48dp (compact) |
| Icon Size | 24×24dp |
| Border Radius | 50% (circular) |
| Elevation | Level 2 (rest), Level 3 (hover) |
| Transition | 200ms elevation change |
| Position | Fixed bottom-right, 16dp margin from edges |

**Content rules:**
- Use single action verb (Book, Call, Message).
- No trailing punctuation.

**Do/Don't:**
- **Do** use FAB for primary action when space is limited.
- **Don't** use FAB for secondary or tertiary actions.

---

### Toolbar

**Types/Variants:**
Single horizontal row of icon or text buttons grouped by function.

**Specs:**

| Property | Value |
|---|---|
| Height | 56dp (mobile), 64dp (desktop) |
| Padding | 8dp |
| Spacing Between Items | 8dp |
| Icon Size | 24×24dp |
| Button Size | 40×40dp minimum |

**Content rules:**
- Icon-only buttons must have tooltips and `aria-label`.
- Text labels use sentence case.

**Do/Don't:**
- **Do** group related actions (e.g., sort, filter together).
- **Don't** mix primary and secondary actions in the same toolbar.

---

## Input

### Text Field

**Types/Variants:**

| Type | Use |
|---|---|
| Outlined | Default; highest contrast |
| Filled | Secondary option (light background) |
| Single-line | Short inputs (email, name) |
| Multi-line | Longer inputs (message, address) |

**Specs:**

| Property | Value |
|---|---|
| Height | 40dp (single-line) |
| Border Radius | 4px |
| Border | 1px solid #D9D9D9 (rest), 2px solid #1a1a1a (focus) |
| Padding | 8dp vertical, 12dp horizontal |
| Typography | Body (16px) |
| Focus Ring | 2px solid #000000, 4px offset |
| Transition | 200ms border color |

**Content rules:**
- Use `<label>` element associated via `for` attribute.
- Label uses sentence case (e.g., "Email address").
- Placeholder text should not replace label; use hint text for guidance.
- Required fields marked with asterisk (*).
- Error messages must be specific and actionable.

**Do/Don't:**
- **Do** always pair inputs with visible labels.
- **Don't** use placeholder text as the only label.

**Accessibility:**
- Semantic `<input>` with type attribute.
- Associated `<label>` with `for="input-id"`.
- Error states use `aria-invalid="true"` and `aria-describedby` to link error message.
- Required inputs use `aria-required="true"`.
- Focus ring must always be visible.

---

### Checkbox

**Specs:**

| Property | Value |
|---|---|
| Size | 20×20dp |
| Border Radius | 2px |
| Border | 2px solid #1a1a1a |
| Checked Mark | 2px white stroke, centered |
| Checked Background | #000000 |
| Padding | 4dp around checkbox |
| Label Spacing | 8dp between checkbox and label |
| Touch Target | 40×40dp minimum |

**Content rules:**
- Label uses sentence case and short phrases.
- No trailing punctuation.

**Do/Don't:**
- **Do** group related checkboxes with a fieldset and legend.
- **Don't** use checkboxes for mutually exclusive options (use radio instead).

**Accessibility:**
- Semantic `<input type="checkbox">`.
- Associated `<label>` with `for` attribute.
- Use `aria-checked` for custom checkboxes.
- Focus ring visible.

---

### Radio Button

**Specs:**

| Property | Value |
|---|---|
| Size | 20×20dp |
| Border Radius | 50% (circular) |
| Border | 2px solid #1a1a1a |
| Selected Dot | 8×8dp white circle, centered |
| Selected Background | #000000 |
| Padding | 4dp around radio |
| Label Spacing | 8dp |
| Touch Target | 40×40dp minimum |

**Content rules:**
- Label uses sentence case.
- No trailing punctuation.

**Do/Don't:**
- **Do** use radio buttons for mutually exclusive options.
- **Don't** use radio buttons when multiple selections are needed (use checkboxes).

**Accessibility:**
- Semantic `<input type="radio">` with `name` attribute (grouped by name).
- Associated `<label>` with `for` attribute on each option.
- Fieldset and legend to group related radios.
- `aria-checked` for custom radio styles.

---

### Switch (Toggle)

**Specs:**

| Property | Value |
|---|---|
| Width | 48dp |
| Height | 24dp |
| Border Radius | 12dp |
| Toggle Knob | 20×20dp, 2dp offset |
| Off State | #CCCCCC background |
| On State | #000000 background |
| Transition | 200ms cubic-bezier(0.4, 0, 0.2, 1) |
| Touch Target | 40×40dp minimum |

**Content rules:**
- Label uses sentence case.
- Pair with clear on/off language.

**Do/Don't:**
- **Do** use switches for binary on/off states.
- **Don't** use switches for form submission.

**Accessibility:**
- Semantic `<input type="checkbox">` with `role="switch"`.
- Associated `<label>` or `aria-label`.
- Keyboard accessible (Space to toggle).

---

### Slider

**Specs:**

| Property | Value |
|---|---|
| Track Height | 4dp |
| Thumb Size | 20×20dp |
| Border Radius | 2dp (track), 50% (thumb) |
| Track Color | #D9D9D9 (rest), #000000 (active) |
| Thumb Color | #000000 |
| Transition | 200ms on drag completion |
| Min Touch Target | 44×44dp |

**Content rules:**
- Provide min/max labels or values.
- Current value displayed as live text or aria-valuenow.

**Do/Don't:**
- **Do** show current value and range.
- **Don't** use sliders for small ranges (< 5 values; use select instead).

**Accessibility:**
- Semantic `<input type="range">`.
- `aria-valuemin`, `aria-valuemax`, `aria-valuenow` attributes.
- Keyboard: Arrow keys to adjust.
- Label via `aria-label` or associated `<label>`.

---

### Dropdown/Select

**Specs:**

| Property | Value |
|---|---|
| Height | 40dp |
| Padding | 8dp vertical, 12dp horizontal |
| Border | 1px solid #D9D9D9 (rest), 2px solid #000000 (focus) |
| Border Radius | 4px |
| Menu Max Height | 280dp (scrollable beyond) |
| Item Height | 40dp |
| Item Padding | 8dp |
| Elevation | Level 2 |

**Content rules:**
- Options use sentence case.
- Placeholder text (e.g., "Select an option") if no default.
- No trailing punctuation.

**Do/Don't:**
- **Do** use native `<select>` for simple lists (better accessibility).
- **Don't** create custom dropdowns without proper ARIA attributes.

**Accessibility:**
- Semantic `<select>` and `<option>` tags (native) or custom with `role="listbox"`, `role="option"`.
- Associated `<label>`.
- Keyboard: Arrow keys to navigate, Enter to select, Escape to close.
- `aria-expanded`, `aria-selected` for custom implementations.

---

### Combobox

**Specs:**

| Property | Value |
|---|---|
| Input Height | 40dp |
| Dropdown Height | 280dp max (scrollable) |
| Item Height | 40dp |
| Debounce | 200ms |
| Min Characters | 1 (start filtering immediately) |

**Content rules:**
- Placeholder: "Search or select...".
- Match highlighting in results.

**Do/Don't:**
- **Do** highlight matching text in results.
- **Don't** auto-select first result on input focus.

**Accessibility:**
- `<input>` with `aria-autocomplete="list"`, `aria-expanded`, `aria-controls`.
- Results list with `role="listbox"` and `role="option"` on items.
- Arrow keys navigate; Enter selects.

---

### Picker (Date/Time)

**Specs:**

| Property | Value |
|---|---|
| Trigger Height | 40dp |
| Calendar Grid | 7 columns (days), 6 rows (weeks) |
| Cell Size | 40×40dp minimum |
| Selected Date | #000000 background, white text |
| Transition | 200ms on date selection |

**Content rules:**
- Display format: YYYY-MM-DD (ISO 8601 for storage, locale-specific for display).
- Placeholder: "Select date...".

**Do/Don't:**
- **Do** use native input type="date" on supported browsers for accessibility.
- **Don't** force custom pickers on all platforms.

**Accessibility:**
- Native `<input type="date">` preferred (best keyboard and screen reader support).
- Custom pickers require `role="dialog"`, `aria-label`, calendar grid structure.
- Focus management: initial focus on current date or "today" button.

---

### Textarea

**Specs:**

| Property | Value |
|---|---|
| Min Height | 80dp |
| Max Height | 280dp (scrollable) |
| Padding | 8dp |
| Border | 1px solid #D9D9D9 (rest), 2px solid #000000 (focus) |
| Border Radius | 4px |
| Line Height | 1.6 |
| Font Size | 16px (no zoom on focus) |
| Resize | vertical resize allowed (or disabled) |

**Content rules:**
- Associated `<label>` with `for` attribute.
- Placeholder text as hint, not label.
- Character count (current / max) below field if limit exists.

**Do/Don't:**
- **Do** show character count for limited textareas.
- **Don't** auto-resize textareas; allow user control or scroll.

**Accessibility:**
- Semantic `<textarea>` with associated `<label>`.
- Error messages linked via `aria-describedby`.
- Focus ring visible.

---

### Rating

**Specs:**

| Property | Value |
|---|---|
| Star Size | 24×24dp |
| Spacing | 4dp between stars |
| Filled Star | #FFB800 (gold) |
| Empty Star | #D9D9D9 |
| Hover Star | #FFC700 (lighter gold) |
| Touch Target | 40×40dp around each star |

**Content rules:**
- Display current rating (e.g., "4 out of 5").
- Optional: show count (e.g., "4.2 ★ (250 reviews)").

**Do/Don't:**
- **Do** show a tooltip or label on hover.
- **Don't** allow half-star ratings unless explicitly designed for it.

**Accessibility:**
- Use `role="radiogroup"` for interactive ratings.
- Each star as `role="radio"` with `aria-label="[N] stars"`.
- Keyboard: Arrow keys to select; Enter to confirm.
- Display-only: use `aria-label="Rated [N] out of 5 stars"`.

---

## Navigation

### Navigation Bar (Bottom Navigation)

**Specs:**

| Property | Value |
|---|---|
| Height | 56dp |
| Item Width | 80dp (4 items), responsive |
| Icon Size | 24×24dp |
| Label Size | 12px (60% opacity when inactive) |
| Label Color | #1a1a1a (active), #666666 (inactive) |
| Active Indicator | Bottom border 3dp, #000000 |
| Elevation | Level 1 (subtle shadow above) |

**Content rules:**
- 3–5 navigation items maximum.
- Labels use sentence case, concise (1 word ideal).
- Icons should be universally recognizable.

**Do/Don't:**
- **Do** highlight active tab with color + underline.
- **Don't** use 5+ tabs; use drawer or top nav instead.

**Accessibility:**
- `role="tablist"` on container.
- Each item: `role="tab"` with `aria-selected="true"` (active) or "false".
- `aria-controls` to link to content panels.
- Keyboard: Arrow keys navigate; Enter/Space to activate.

---

### Navigation Drawer (Sidebar)

**Specs:**

| Property | Value |
|---|---|
| Width | 280dp (standard), full-screen on mobile <= 480px |
| Item Height | 40dp |
| Item Padding | 12dp horizontal, 8dp vertical |
| Icon Size | 24×24dp |
| Active Indicator | Left border 4dp, #000000 |
| Scrim (Mobile) | Semi-transparent overlay (rgba(0,0,0,0.3)) |
| Elevation | Level 3 |
| Animation | Slide in from left, 300ms |

**Content rules:**
- Group related items with headers (sentence case, small caps optional).
- Labels use sentence case.
- No trailing punctuation.

**Do/Don't:**
- **Do** close drawer on navigation (mobile).
- **Don't** keep drawer open by default on mobile.

**Accessibility:**
- `role="navigation"` or `<nav>`.
- Active item: `aria-current="page"`.
- Keyboard: Escape to close drawer.
- Focus trap when drawer is open (mobile).

---

### Tabs

**Specs:**

| Property | Value |
|---|---|
| Tab Height | 40dp |
| Tab Padding | 16dp horizontal |
| Typography | Label Large (14px, 600) |
| Underline | 2px, #000000 (active) |
| Underline Transition | 200ms |
| Scroll (if overflow) | Horizontal scroll, centered active |

**Content rules:**
- 2–6 tabs maximum per tab group.
- Labels use sentence case, short (≤ 15 chars).
- Icons + labels (or icons-only if universal).

**Do/Don't:**
- **Do** show underline on active tab.
- **Don't** use text-only tabs without clear active state.

**Accessibility:**
- `role="tablist"` on container.
- Each tab: `role="tab"`, `aria-selected`, `aria-controls`.
- Keyboard: Arrow keys navigate tabs; Tab key moves into content.
- Focus visible on tabs.

---

### Breadcrumb

**Specs:**

| Property | Value |
|---|---|
| Item Padding | 4dp vertical, 8dp horizontal |
| Separator | "/" (space-separated) |
| Separator Color | #999999 |
| Active Item | Text (no link) |
| Inactive Item | Link (underlined or blue) |
| Typography | 14px, Body Small |

**Content rules:**
- Use > or / as separator (visual only, not in text).
- Start with home link; show 3–5 path levels max.
- Active (last) item is plain text, not clickable.

**Do/Don't:**
- **Do** show breadcrumb on pages deeper than 2 levels.
- **Don't** include breadcrumb on homepage.

**Accessibility:**
- `role="navigation"` with `aria-label="Breadcrumb"`.
- Each link: `<a>` with `aria-current="page"` on active item.
- Separators: `aria-hidden="true"`.

---

### App Bar (Header/Top Navigation)

**Specs:**

| Property | Value |
|---|---|
| Height | 56dp (mobile), 64dp (desktop) |
| Padding | 8dp horizontal (mobile), 16dp (desktop) |
| Title Size | 20px (600 weight) |
| Icon Size | 24×24dp |
| Elevation | Level 1 (subtle) |
| Background | #FFFFFF |
| Sticky | Yes (remain at top on scroll) |

**Content rules:**
- Title: use page name or brand name.
- Actions: icon or text buttons, right-aligned.
- Use descriptive labels on icon buttons (aria-label).

**Do/Don't:**
- **Do** keep app bar consistent across all pages.
- **Don't** hide app bar on scroll (unless intentional design).

**Accessibility:**
- `role="banner"` for main header.
- Title must be semantic heading (h1) or aria-label.
- Back button or breadcrumb for navigation clarity.

---

### Menu

**Specs:**

| Property | Value |
|---|---|
| Item Height | 40dp |
| Item Padding | 8dp vertical, 12dp horizontal |
| Min Width | 160dp |
| Max Width | 280dp |
| Elevation | Level 2 |
| Separator | 1px solid #EEEEEE |
| Animation | Fade + scale, 200ms |

**Content rules:**
- Labels use sentence case.
- No trailing punctuation on action labels.
- Icons optional (left-aligned if used).

**Do/Don't:**
- **Do** close menu on item selection.
- **Don't** nest submenus more than 1 level deep.

**Accessibility:**
- `role="menu"` on list, `role="menuitem"` on items.
- Keyboard: Arrow keys navigate; Enter to select; Escape to close.
- `aria-label` on menu trigger.

---

### Search Bar

**Specs:**

| Property | Value |
|---|---|
| Height | 40dp |
| Padding | 8dp vertical, 12dp horizontal |
| Border Radius | 4px |
| Background | #F5F5F5 |
| Icon Size | 20×20dp |
| Placeholder | "Search..." (light gray, #999999) |
| Results Max Height | 280dp (scrollable) |

**Content rules:**
- Placeholder: "Search...".
- Results show title + brief description.
- Highlight matching keywords.

**Do/Don't:**
- **Do** show recent searches or suggestions.
- **Don't** auto-submit on input (let user click or press Enter).

**Accessibility:**
- `<input type="search">` or `<input type="text">`.
- Results: `role="listbox"` with `role="option"` items.
- `aria-expanded`, `aria-controls` on trigger.
- Keyboard: Escape to clear/close; Arrow keys in results.

---

## Containment

### Card

**Specs:**

| Property | Value |
|---|---|
| Padding | 16dp |
| Border Radius | 8px |
| Border | 1px solid #EEEEEE |
| Elevation | Level 1 (rest), Level 2 (hover) |
| Elevation Transition | 200ms |
| Background | #FFFFFF |

**Content rules:**
- Title + supporting content.
- CTA button or link bottom-right (optional).
- Avoid excessive text; use descriptions ≤ 100 chars.

**Do/Don't:**
- **Do** show elevation change on hover.
- **Don't** use cards for simple text blocks.

**Accessibility:**
- Semantic card structure: heading + content + action.
- If card is a link: `<article>` or `<section>` with nested `<a>` or button.
- Avoid nested buttons.

---

### Dialog (Modal)

**Specs:**

| Property | Value |
|---|---|
| Max Width | 480dp (mobile), 600dp (desktop) |
| Padding | 24dp |
| Border Radius | 8px |
| Elevation | Level 4 |
| Scrim | rgba(0, 0, 0, 0.3) |
| Animation | Fade + scale, 200ms |
| Button Layout | Stacked (mobile), horizontal (desktop) |

**Content rules:**
- Title (H1 or h2).
- Body text (max 3 short paragraphs).
- 1–2 action buttons (primary + secondary).
- Optional close button (X, top-right).

**Do/Don't:**
- **Do** focus first interactive element on open.
- **Don't** allow interaction outside modal (scrim blocks it).

**Accessibility:**
- `role="dialog"` with `aria-modal="true"`.
- Title: `aria-labelledby` linked to dialog title.
- Description: `aria-describedby` (optional).
- Focus trap: Tab cycles within dialog.
- Escape key closes dialog.

---

### Bottom Sheet

**Specs:**

| Property | Value |
|---|---|
| Height | 50–80% screen height (mobile) |
| Border Radius | 16px (top corners only) |
| Padding | 24dp |
| Elevation | Level 4 |
| Scrim | rgba(0, 0, 0, 0.3) |
| Drag Handle | 4dp height, 40dp width, top-center (optional) |
| Animation | Slide up, 300ms |

**Content rules:**
- Title + content sections.
- Actions at bottom (stacked).
- Scrollable content area if needed.

**Do/Don't:**
- **Do** allow dismiss by swiping down or tapping scrim.
- **Don't** trap user in bottom sheet; allow close.

**Accessibility:**
- `role="dialog"` with `aria-modal="true"`.
- Focus trap + Escape key to close.
- Announce bottom sheet open to screen readers.

---

### Popover

**Specs:**

| Property | Value |
|---|---|
| Max Width | 280dp |
| Padding | 16dp |
| Border Radius | 8px |
| Elevation | Level 2 |
| Arrow | 8dp triangle, pointing to trigger |
| Animation | Fade + scale, 150ms |
| Auto Close | On outside click or Escape |

**Content rules:**
- Concise content (text + optional action).
- Max 2–3 lines of body text.

**Do/Don't:**
- **Do** position popover above trigger if room; below otherwise.
- **Don't** nest popovers.

**Accessibility:**
- `role="tooltip"` (read-only) or `role="dialog"` (interactive).
- `aria-label` or `aria-describedby`.
- Keyboard: Escape closes; Tab if interactive.

---

### Accordion

**Specs:**

| Property | Value |
|---|---|
| Header Height | 48dp |
| Header Padding | 16dp |
| Content Padding | 16dp |
| Border | 1px solid #EEEEEE between items |
| Border Radius | 0px (or 8px, all items together) |
| Transition | 200ms height ease |
| Icon | Chevron (24×24dp), rotates on expand |

**Content rules:**
- Header: question or summary (sentence case, short).
- Content: explanation or form section.
- Allow multiple items open or single open (configurable).

**Do/Don't:**
- **Do** animate content height smoothly.
- **Don't** truncate content; show full expanded content.

**Accessibility:**
- Header: `role="button"`, `aria-expanded="true|false"`, `aria-controls="panel-id"`.
- Content panel: `role="region"` or implicit via heading.
- Keyboard: Enter/Space to toggle; Arrow Up/Down to navigate headers.

---

### Divider

**Specs:**

| Property | Value |
|---|---|
| Height | 1px |
| Color | #EEEEEE |
| Margin | 16dp vertical (or 24dp for section dividers) |
| Padding | 0px |

**Content rules:**
- Use dividers to separate sections, lists.
- Optional: center a label within divider (less common).

**Do/Don't:**
- **Do** use dividers to clarify section breaks.
- **Don't** overuse dividers; can reduce clarity if excessive.

**Accessibility:**
- Semantic: `<hr>` or `<div role="separator" aria-orientation="horizontal">`.
- Decorative dividers: `aria-hidden="true"`.

---

## Data Display

### Avatar

**Specs:**

| Property | Value |
|---|---|
| Size | 40×40dp (default), 32×32dp (small), 56×56dp (large) |
| Border Radius | 50% (circular) |
| Border | 2px solid #FFFFFF (optional) |
| Initials Font | 14px (600), white text on colored bg |
| Image Fit | object-fit: cover |

**Content rules:**
- Initials: 1–2 letters (first letter of first and last name).
- Placeholder: generic person icon if no image.

**Do/Don't:**
- **Do** use initials or user-uploaded image.
- **Don't** show full names in avatars; use initials or icons.

**Accessibility:**
- If avatar is clickable link: `aria-label="[User name]"`.
- Image alt text: descriptive (not "avatar").

---

### Badge

**Specs:**

| Property | Value |
|---|---|
| Padding | 2dp vertical, 8dp horizontal |
| Border Radius | 12dp (pill) |
| Typography | Label (12px, 600) |
| Background | #000000 (default) |
| Text Color | #FFFFFF |
| Min Width | 20dp |
| Position | Top-right corner (if on avatar or button) |

**Content rules:**
- Short text: 1 word or number.
- Examples: "New", "3", "Beta", "Sale".

**Do/Don't:**
- **Do** use badges for counts, status, or labels.
- **Don't** use badges for long text; use chips instead.

**Accessibility:**
- If badge conveys info: `aria-label` or include in parent element's label.
- Decorative badges: `aria-hidden="true"`.

---

### List

**Specs:**

| Property | Value |
|---|---|
| Item Height | 40dp (compact), 56dp (standard), 72dp (dense) |
| Item Padding | 12dp vertical, 16dp horizontal |
| Divider | 1px solid #EEEEEE between items |
| Avatar Size | 40×40dp (leading) |
| Title | 16px (400), #1a1a1a |
| Subtitle | 14px (400), #666666 |
| Trailing | Icon or text, right-aligned |

**Content rules:**
- Title: short, descriptive.
- Subtitle: optional supporting info.
- Icon or action trailing (rarely CTA).

**Do/Don't:**
- **Do** keep list items scannable (short text).
- **Don't** make list items too tall; limit text lines.

**Accessibility:**
- `<ul>` or `<ol>` with `<li>` items.
- If items are interactive (links/buttons): semantic tags within each `<li>`.
- List with actions: `role="grid"` or `role="tree"` (if hierarchical).

---

### Carousel

**Specs:**

| Property | Value |
|---|---|
| Item Width | 100% (mobile), 50% (tablet), 33% (desktop) |
| Spacing | 16dp between items |
| Scroll Behavior | Smooth, snap to item edges |
| Navigation | Dots (pagination) + arrows (previous/next) |
| Dot Size | 8×8dp |
| Dot Spacing | 8dp |
| Animation | 300ms on scroll complete |

**Content rules:**
- Each item: image + optional caption/title.
- Indicate current position (e.g., "1 of 5").

**Do/Don't:**
- **Do** show pagination dots or slide counter.
- **Don't** auto-scroll without user control.

**Accessibility:**
- `role="region"` with `aria-label="Carousel"` or `aria-roledescription="carousel"`.
- Buttons: "Previous slide", "Next slide" (aria-label).
- Keyboard: Arrow keys navigate; Tab within carousel item links.
- Announce current position to screen readers.

---

### Icon

**Specs:**

| Property | Value |
|---|---|
| Sizes | 16×16dp, 20×20dp, 24×24dp, 32×32dp, 40×40dp |
| Stroke Width | 2px (consistent) |
| Corner Radius | 2px (if applicable) |
| Color | Inherit from parent text color or explicit #000000 |
| Viewbox | Square (e.g., 24×24) |

**Content rules:**
- Icons should be universally recognizable.
- Pair with text labels when ambiguous.
- Decorative icons: `aria-hidden="true"`.

**Do/Don't:**
- **Do** use consistent icon style (all outlined or all filled).
- **Don't** mix icon styles (outlined + filled) in the same UI.

**Accessibility:**
- Icon-only buttons require `aria-label`.
- Decorative icons: `aria-hidden="true"`.
- Icon fonts: use title or aria-label on `<i>` tag.

---

### Image

**Specs:**

| Property | Value |
|---|---|
| Max Width | 100% (responsive) |
| Height | Auto (maintain aspect ratio) |
| Border Radius | 0px (default), 8px (card images) |
| Lazy Load | Yes (intersection observer) |
| Formats | WebP (modern), JPEG fallback |

**Content rules:**
- Alt text: descriptive, ≤ 125 chars.
- Decorative images: `alt=""`.
- No "image of" in alt text.

**Do/Don't:**
- **Do** use descriptive alt text.
- **Don't** omit alt attributes.

**Accessibility:**
- All `<img>` must have `alt` attribute.
- Meaningful images: descriptive alt text (e.g., "Ueno Park cherry blossoms in spring").
- Decorative images: `alt=""` (empty).

---

### Chip (Tag)

**Specs:**

| Property | Value |
|---|---|
| Height | 32dp |
| Padding | 4dp vertical, 12dp horizontal |
| Border Radius | 16dp (pill) |
| Border | 1px solid #D9D9D9 (optional) |
| Typography | Label (12px, 600) |
| Removable | Optional X icon, 20×20dp |
| Background | #F5F5F5 (default), #000000 (active) |

**Content rules:**
- Short label: 1–3 words.
- Examples: categories, filters, tags.

**Do/Don't:**
- **Do** group chips by function (e.g., filter chips together).
- **Don't** use chips for long text; truncate or shorten.

**Accessibility:**
- Removable chips: `role="button"` with `aria-label="Remove [tag]"`.
- Selectable chips: `role="option"` with `aria-selected`.

---

### Skeleton (Loading Placeholder)

**Specs:**

| Property | Value |
|---|---|
| Background | #EEEEEE |
| Animation | Pulse or shimmer, 1.5s ease-in-out |
| Border Radius | Match content (4px, 8px, or 50%) |
| Height/Width | Match expected content dimensions |

**Content rules:**
- Create skeleton layouts matching actual content structure.
- Example: avatar (40dp circle) + title (60% width, 20px height) + subtitle (80% width, 14px).

**Do/Don't:**
- **Do** show skeleton while content loads.
- **Don't** flash skeleton briefly; hold until content ready.

**Accessibility:**
- Use `aria-busy="true"` on loading container.
- Use `aria-label="Loading [content name]"`.
- Skeletons should not be interactive.

---

### Tooltip

**Specs:**

| Property | Value |
|---|---|
| Max Width | 200dp |
| Padding | 8dp vertical, 12dp horizontal |
| Border Radius | 4px |
| Background | #1a1a1a (dark) |
| Text Color | #FFFFFF |
| Typography | Caption (11px) |
| Offset | 8dp from trigger |
| Animation | Fade in, 150ms |
| Duration | Show 2–5 seconds; hide on mouse leave or click outside |

**Content rules:**
- Brief explanation (1 short sentence, ≤ 50 chars).
- No formatting or links inside tooltips.

**Do/Don't:**
- **Do** use tooltips for icon-only buttons.
- **Don't** put essential info in tooltips; use labels instead.

**Accessibility:**
- Use semantic `title` attribute or `aria-label` (no interactive content).
- Keyboard: focus reveals tooltip.
- Screen readers: announce tooltip on focus.

---

## Feedback

### Progress Indicator (Linear)

**Specs:**

| Property | Value |
|---|---|
| Height | 4dp |
| Background | #EEEEEE (track) |
| Fill Color | #000000 (progress) |
| Border Radius | 2dp |
| Animation | 300ms ease-out |
| Overflow | Clamp to 0–100% |

**Content rules:**
- Show percentage or label (optional, e.g., "60% complete").
- Use for multi-step processes or file uploads.

**Do/Don't:**
- **Do** show percentage if known.
- **Don't** show progress bar for indeterminate waits (use spinner).

**Accessibility:**
- `role="progressbar"` with `aria-valuenow`, `aria-valuemin="0"`, `aria-valuemax="100"`.
- `aria-label` describing what's loading.

---

### Spinner (Indeterminate Progress)

**Specs:**

| Property | Value |
|---|---|
| Size | 40×40dp (default), 24×24dp (small), 56×56dp (large) |
| Stroke Width | 4dp |
| Color | #000000 |
| Animation | Rotation 360°, 1s cubic-bezier(0.4, 0, 0.2, 1) infinite |
| Centering | Absolute center or inline |

**Content rules:**
- Optional text below: "Loading..." or "Processing...".

**Do/Don't:**
- **Do** use for indeterminate loading (unknown duration).
- **Don't** show spinner for < 200ms (too quick to notice).

**Accessibility:**
- `role="status"` with `aria-label="Loading"` or `aria-busy="true"` on parent.
- Announce when loading completes.

---

### Snackbar (Toast)

**Specs:**

| Property | Value |
|---|---|
| Height | 48dp |
| Padding | 12dp vertical, 16dp horizontal |
| Border Radius | 4px |
| Background | #323232 (dark), #FFFFFF (light) |
| Text Color | #FFFFFF (dark), #1a1a1a (light) |
| Elevation | Level 2 |
| Position | Bottom-left (desktop), bottom-center (mobile) |
| Auto Dismiss | 3–6 seconds |
| Animation | Slide up / fade in, 200ms |
| Action Button | Secondary text color, optional |

**Content rules:**
- Message: ≤ 60 characters.
- Action: optional (e.g., "Undo", "Dismiss").
- No essential info in snackbars; allow dismissal.

**Do/Don't:**
- **Do** allow manual close (X button or swipe).
- **Don't** queue > 1 snackbar simultaneously.

**Accessibility:**
- `role="status"` with `aria-live="polite"`.
- Action button: semantic `<button>` or `<a>`.
- Announce dismissal.

---

### Message Bar (Alert Bar)

**Specs:**

| Property | Value |
|---|---|
| Min Height | 40dp |
| Padding | 12dp vertical, 16dp horizontal |
| Border Radius | 0px (full-width) or 8px (contained) |
| Icon | 20×20dp, left-aligned |
| Close Button | Optional X, right-aligned |
| Animation | Slide in, 200ms |
| Elevation | Level 1 (subtle) |

**Content rules:**
- Icon indicates type (error, warning, info, success).
- Message: 1–2 sentences, clear and actionable.
- Optional action link or button.

**Do/Don't:**
- **Do** use consistent icons for message types.
- **Don't** dismiss critical errors without action.

**Accessibility:**
- `role="alert"` (for error/warning) or `role="status"` (for info/success).
- `aria-live="assertive"` (error), `aria-live="polite"` (others).
- Close button: `aria-label="Close"`.

---

### Banner

**Specs:**

| Property | Value |
|---|---|
| Min Height | 56dp |
| Padding | 16dp |
| Border Radius | 0px |
| Background | Color per type (e.g., #FFF3CD for warning) |
| Icon | 24×24dp, optional |
| Text | Headline + body |
| Close Button | Optional, top-right |
| Elevation | None (flush to top) |

**Content rules:**
- Headline: concise, action-oriented.
- Body: brief explanation (1–2 sentences).
- Type-specific colors: Error (#FFEBEE), Warning (#FFF3CD), Success (#E8F5E9), Info (#E3F2FD).

**Do/Don't:**
- **Do** use banners for sitewide alerts or promotions.
- **Don't** overuse; banners compete for attention.

**Accessibility:**
- `role="region"` with `aria-label="Alert"` or `aria-roledescription="banner"`.
- `aria-live="polite"` (non-blocking), `aria-live="assertive"` (critical).
- Close button: `aria-label="Dismiss"`.