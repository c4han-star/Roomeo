# Sumu Hotel Design System — Token Reference

> Always read this file first. For component specs see [design-components.md](design-components.md). For accessibility and do's/don'ts see [design-guidelines.md](design-guidelines.md).

Sumu is a boutique apartment hotel brand designed for travelers who wish to "live" rather than merely visit. The design language emphasizes cultural depth, minimalist elegance, and local authenticity. The primary typeface is a clean, modern sans-serif with generous line spacing, supporting both Japanese and English content. Base spacing unit is 8dp, with platform coverage spanning responsive web (mobile-first), desktop, and print materials.

## Colors

### Accent — Primary
| Role | Hex | Usage |
|---|---|---|
| Primary Action | #000000 | Buttons, links, critical CTAs |
| Primary Hover | #333333 | Button hover state |
| Primary Focus | #1a1a1a | Keyboard focus ring |

### Surface & Neutral
| Role | Hex | Usage |
|---|---|---|
| Background | #FFFFFF | Page background, card surfaces |
| Surface Subtle | #F5F5F5 | Secondary surfaces, dividers |
| Surface Muted | #EEEEEE | Disabled states, subtle contrast |
| Text Primary | #1a1a1a | Body text, headlines |
| Text Secondary | #666666 | Supporting text, metadata |
| Text Tertiary | #999999 | Disabled text, captions |
| Border | #D9D9D9 | Dividers, subtle borders |

### Semantic & Status
| Role | Hex | Usage |
|---|---|---|
| Success | #4CAF50 | Confirmations, positive states |
| Warning | #FF9800 | Alerts, caution messages |
| Error | #F44336 | Errors, destructive actions |
| Info | #2196F3 | Information messages |

## Typography

Default font family: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", sans-serif` (with Japanese fallback to Yu Gothic, Hiragino Sans).

| Style | Size | Weight | Line Height | Spacing |
|---|---|---|---|---|
| Display Large | 48px | 700 | 1.2 | -1.5px |
| Display | 40px | 700 | 1.25 | -1px |
| Headline | 32px | 700 | 1.3 | -0.5px |
| Title Large | 24px | 700 | 1.4 | 0px |
| Title | 20px | 600 | 1.5 | 0.15px |
| Body Large | 18px | 400 | 1.6 | 0.5px |
| Body | 16px | 400 | 1.6 | 0.5px |
| Body Small | 14px | 400 | 1.5 | 0.25px |
| Label Large | 14px | 600 | 1.5 | 0.1px |
| Label | 12px | 600 | 1.4 | 0.4px |
| Caption | 11px | 400 | 1.4 | 0.4px |

## Shape

| Token | Radius | Components |
|---|---|---|
| Corner None | 0px | Images, full-bleed sections |
| Corner Small | 4px | Buttons, input fields, badges |
| Corner Medium | 8px | Cards, modals, overlays |
| Corner Large | 12px | Large containers, rounded cards |

## Elevation

| Level | dp | CSS Shadow | Usage |
|---|---|---|---|
| None | 0 | none | Flat surfaces |
| Level 1 | 1 | 0 1px 3px rgba(0, 0, 0, 0.12) | Hovered cards, subtle lift |
| Level 2 | 2 | 0 2px 6px rgba(0, 0, 0, 0.16) | Floating actions, modals |
| Level 3 | 4 | 0 4px 12px rgba(0, 0, 0, 0.15) | Dropdowns, popovers |
| Level 4 | 8 | 0 8px 24px rgba(0, 0, 0, 0.18) | Dialogs, full-screen overlays |

## Interaction States

| State | Layer Opacity | Notes |
|---|---|---|
| Enabled | 100% | Default interactive state |
| Hover | 95% | Slight darkening; 200ms transition |
| Focus | 100% + ring | 2px solid focus ring at 4px offset |
| Pressed | 85% | Immediate response; active feedback |
| Dragged | 80% | Sustained feedback during drag |
| Disabled | 50% | Reduced opacity; no interaction |

## Layout

| Breakpoint | Width | Grid | Navigation |
|---|---|---|---|
| Mobile (xs) | 320–480px | 4 columns, 16px gutter | Bottom nav, drawer menu |
| Tablet (sm) | 480–768px | 8 columns, 24px gutter | Side nav drawer, expanded tabs |
| Desktop (md) | 768–1024px | 12 columns, 32px gutter | Top nav bar, tab navigation |
| Large (lg) | 1024px+ | 12 columns, 48px gutter | Top nav, persistent sidebar |

Mobile-first responsive design with touch targets ≥ 48×48dp. Lazy loading for images; viewport meta tag enforces `width=device-width, initial-scale=1`.

## Motion

| Easing | Curve | Use |
|---|---|---|
| Standard | cubic-bezier(0.4, 0, 0.2, 1) | General transitions |
| Decelerate | cubic-bezier(0, 0, 0.2, 1) | Incoming elements |
| Accelerate | cubic-bezier(0.4, 0, 1, 1) | Exiting elements |
| Sharp | cubic-bezier(0.4, 0, 0.6, 1) | Snappy feedback |

Duration tokens: Short 150ms (hover, focus), Medium 300ms (transitions), Long 500ms (page entry).

## Design Tokens

Naming convention: `{category}.{role}.{state}` (e.g., `color.text.primary`, `spacing.unit.base`, `shadow.elevation.2`).

Core tokens: `color.*`, `spacing.*`, `typography.*`, `shape.*`, `shadow.*`, `motion.*`.

---