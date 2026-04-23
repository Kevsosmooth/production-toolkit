---
# DESIGN.md — [Project Name]
#
# Machine-readable tokens (YAML front matter) + human-readable rationale (markdown body).
# Tokens are the normative values. Prose explains *why* and *how* to apply them.
# Spec: https://stitch.withgoogle.com/docs/design-md/specification  (version: alpha)
#
# HOW TO FILL THIS IN
# Replace every <PLACEHOLDER> with a real value.
# Delete comments and guidance lines once filled.
# Run: npx @google/design.md lint DESIGN.md   (validates tokens + WCAG contrast)

version: alpha
name: <Project Name>
description: <One sentence: what this product is and what it should feel like>

# --- COLORS ---
# Hex only. sRGB color space. Start with "#".
# Required: at minimum define "primary".
# Common pattern: primary (brand), secondary (support), tertiary (accent), neutral (base).
# Add -container, on-*, surface-* variants as needed.
colors:
  # Brand palette
  primary: "#<HEX>"            # Main brand color — used for CTAs, key highlights
  on-primary: "#<HEX>"         # Text/icon color on top of primary
  primary-container: "#<HEX>"  # Tinted surface for backgrounds containing primary content
  on-primary-container: "#<HEX>"

  secondary: "#<HEX>"          # Supporting color — trust, calm, secondary actions
  on-secondary: "#<HEX>"
  secondary-container: "#<HEX>"
  on-secondary-container: "#<HEX>"

  tertiary: "#<HEX>"           # Accent — sparingly, for highlights or tags
  on-tertiary: "#<HEX>"
  tertiary-container: "#<HEX>"
  on-tertiary-container: "#<HEX>"

  # Surfaces (light theme example — flip for dark)
  background: "#<HEX>"         # Page canvas
  on-background: "#<HEX>"      # Default text on canvas

  surface: "#<HEX>"            # Cards, panels (one step above background)
  surface-dim: "#<HEX>"        # Subdued surface (below baseline)
  surface-bright: "#<HEX>"     # Emphasized surface
  surface-container-lowest: "#<HEX>"
  surface-container-low: "#<HEX>"
  surface-container: "#<HEX>"
  surface-container-high: "#<HEX>"
  surface-container-highest: "#<HEX>"
  on-surface: "#<HEX>"         # Primary text on surfaces
  on-surface-variant: "#<HEX>" # Secondary text, icons, captions on surfaces

  outline: "#<HEX>"            # Default border, divider
  outline-variant: "#<HEX>"    # Subtle border

  inverse-surface: "#<HEX>"    # Dark surface for snackbars/toasts in light theme
  inverse-on-surface: "#<HEX>"
  inverse-primary: "#<HEX>"    # Primary tint visible on inverse surfaces

  # Semantic
  error: "#<HEX>"
  on-error: "#<HEX>"
  error-container: "#<HEX>"
  on-error-container: "#<HEX>"

  success: "#<HEX>"            # Optional — not in spec core but widely used
  warning: "#<HEX>"            # Optional

# --- TYPOGRAPHY ---
# fontWeight must be a quoted string or bare number (both valid YAML)
# lineHeight can be unitless (1.5 = 1.5× font size) or a Dimension (24px)
# letterSpacing is a Dimension (em preferred: -0.02em, 0.05em)
# Naming convention: {role}-{size} where role = display|headline|title|body|label|caption
typography:
  display:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"   # e.g. "800"
    lineHeight: <ratio>      # e.g. 1.05
    letterSpacing: <em>      # e.g. -0.04em

  headline-lg:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>
    letterSpacing: <em>

  headline-md:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>
    letterSpacing: <em>

  headline-sm:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  title-lg:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  body-lg:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  body-md:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  body-sm:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  label-lg:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>
    letterSpacing: <em>   # Labels often track out slightly: 0.05em–0.1em

  label-md:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>
    letterSpacing: <em>

  label-sm:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>
    letterSpacing: <em>

  caption:
    fontFamily: <Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

  mono:
    fontFamily: <Monospace Font Name>
    fontSize: <px>
    fontWeight: "<number>"
    lineHeight: <ratio>

# --- ROUNDED ---
# Border radius scale. All values are Dimensions (px or rem).
rounded:
  none: 0px
  sm: <px or rem>    # e.g. 4px — tight, technical
  md: <px or rem>    # e.g. 8px — standard
  lg: <px or rem>    # e.g. 12px — cards, modals
  xl: <px or rem>    # e.g. 16px — large containers
  2xl: <px or rem>   # e.g. 24px — rounded panels
  full: 9999px       # pills, avatars, circular buttons

# --- SPACING ---
# All values are Dimensions (px) or unitless numbers (column counts, ratios).
spacing:
  base: <px>         # Grid unit (typically 4px or 8px)
  xs: <px>           # e.g. 4px
  sm: <px>           # e.g. 8px
  md: <px>           # e.g. 16px
  lg: <px>           # e.g. 24px
  xl: <px>           # e.g. 40px
  2xl: <px>          # e.g. 64px
  3xl: <px>          # e.g. 96px
  gutter: <px>       # Column gutter in grid
  margin: <px>       # Outer page margin (mobile)
  margin-desktop: <px>  # Outer page margin (desktop)
  container-max: <px>   # Max content width

# --- COMPONENTS ---
# Map component names to design token groups.
# Values can be literals or token references using {path.to.token} syntax.
# Variants (hover, active, disabled) use a related key suffix.
components:
  # --- Buttons ---
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: <px>        # e.g. 44px (WCAG touch target minimum)
    padding: <px>       # e.g. 0 20px (vertical horizontal)

  button-primary-hover:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"

  button-primary-active:
    backgroundColor: "{colors.on-primary}"
    textColor: "{colors.primary}"

  button-primary-disabled:
    backgroundColor: "{colors.surface-container}"
    textColor: "{colors.on-surface-variant}"

  button-secondary:
    backgroundColor: transparent
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: <px>
    padding: <px>
    # Note: add a border in component CSS: 1px solid var(--color-primary)

  button-secondary-hover:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"

  button-ghost:
    backgroundColor: transparent
    textColor: "{colors.on-surface}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: <px>
    padding: <px>

  button-ghost-hover:
    backgroundColor: "{colors.surface-container-high}"

  button-destructive:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-error}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: <px>
    padding: <px>

  button-destructive-hover:
    backgroundColor: "{colors.error-container}"
    textColor: "{colors.on-error-container}"

  # --- Inputs & Forms ---
  input-field:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    height: <px>
    padding: <px>
    # Border defined in CSS: 1px solid var(--color-outline)

  input-field-focus:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.on-surface}"
    # Focus ring in CSS: 2px solid var(--color-primary), outline-offset: 2px

  input-field-error:
    backgroundColor: "{colors.error-container}"
    textColor: "{colors.on-error-container}"
    # Border in CSS: 1px solid var(--color-error)

  input-field-disabled:
    backgroundColor: "{colors.surface-container}"
    textColor: "{colors.on-surface-variant}"

  textarea:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: <px>

  # --- Cards ---
  card-default:
    backgroundColor: "{colors.surface-container-lowest}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: "{spacing.md}"
    # Border: 1px solid var(--color-outline-variant)
    # Shadow: defined in elevation section

  card-elevated:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: "{spacing.md}"

  card-interactive:
    backgroundColor: "{colors.surface-container-lowest}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: "{spacing.md}"

  card-interactive-hover:
    backgroundColor: "{colors.surface-container}"
    textColor: "{colors.on-surface}"

  # --- Navigation ---
  nav-item:
    backgroundColor: transparent
    textColor: "{colors.on-surface-variant}"
    typography: "{typography.label-md}"
    rounded: "{rounded.sm}"
    padding: <px>

  nav-item-active:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"

  nav-item-hover:
    backgroundColor: "{colors.surface-container-high}"
    textColor: "{colors.on-surface}"

  # --- Badges / Chips ---
  badge-default:
    backgroundColor: "{colors.surface-container-high}"
    textColor: "{colors.on-surface-variant}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: <px>

  badge-primary:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: <px>

  badge-success:
    backgroundColor: "{colors.success}"     # or your semantic success color
    textColor: "#ffffff"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: <px>

  badge-error:
    backgroundColor: "{colors.error-container}"
    textColor: "{colors.on-error-container}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: <px>

  # --- Modals / Dialogs ---
  modal:
    backgroundColor: "{colors.surface-container-lowest}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.xl}"
    padding: "{spacing.lg}"
    # Overlay backdrop: rgba of inverse-surface at 60% opacity

  # --- Tooltips ---
  tooltip:
    backgroundColor: "{colors.inverse-surface}"
    textColor: "{colors.inverse-on-surface}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.sm}"
    padding: <px>

  # --- List items ---
  list-item:
    backgroundColor: transparent
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.sm}"
    padding: <px>

  list-item-hover:
    backgroundColor: "{colors.surface-container-high}"

  list-item-active:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"

  # --- Code blocks ---
  code-block:
    backgroundColor: "{colors.surface-container-highest}"
    textColor: "{colors.on-surface}"
    typography: "{typography.mono}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
---

# [Project Name] Design System

> One-sentence description of the product's purpose and audience.

---

## Overview

<!-- FILL IN: 2-4 sentences describing the product's personality, target feel,
     and design philosophy. This is the most important prose section — it sets
     the direction for every decision below. Be specific about mood, density,
     and the emotional response the UI should create.

EXAMPLE (Stripe-like):
"This design system targets developers and finance operators. It should feel
precise and trustworthy — a tool that is confident in its engineering without
being cold. The interface is information-dense but never cluttered, using white
space to signal hierarchy rather than decoration. Every visual decision earns
its place by improving legibility or reducing cognitive load."

EXAMPLE (consumer/friendly):
"Built for busy pet owners booking on mobile. The personality is optimistic
and trustworthy — premium enough to build confidence, approachable enough to
feel like a friend. The interface breathes. Nothing crowds. Whitespace signals
care, not emptiness."
-->

**Personality keywords:** <adjective>, <adjective>, <adjective>, <adjective>

**Density:** airy | balanced | compact  <!-- pick one -->

**Visual temperature:** cool | neutral | warm  <!-- pick one -->

**Motion stance:** minimal | moderate | expressive  <!-- pick one -->

**Must feel like:** <3-5 words — e.g. "precision engineering with warmth">

**Must not feel like:** <3-5 words — e.g. "a generic SaaS dashboard">

### Brand

| Field | Value |
|-------|-------|
| Product name | <Name> |
| Tagline | <Tagline> |
| Audience | <Who uses this and in what context> |
| Stage | Early product / Growth / Mature |

### Design References

<!-- List any real-brand design systems consulted for inspiration. Be specific
     about what was borrowed.
- Vercel — monochrome precision, grid discipline
- Linear — ultra-minimal, keyboard-native density
- Stripe — typographic weight hierarchy, developer trust signals
-->

---

## Colors

<!-- FILL IN: Describe the color strategy in prose. Name any signature colors,
     explain the role of each palette, and state rules for usage.

EXAMPLE:
"The palette is anchored in deep obsidian and a single electric green accent.
The green is used for exactly one purpose: primary CTAs and active states.
Everything else stays monochrome. Introducing a second accent color is a
violation — if something needs to stand out, it must earn it through size or
weight, not hue."
-->

### Palette

| Token | Hex | Role |
|-------|-----|------|
| `primary` | `#<HEX>` | <Role description, e.g. "Brand CTA, active states"> |
| `on-primary` | `#<HEX>` | Text/icon on primary surfaces |
| `primary-container` | `#<HEX>` | Tinted backgrounds for primary content |
| `on-primary-container` | `#<HEX>` | Text/icon on primary-container |
| `secondary` | `#<HEX>` | <Role> |
| `on-secondary` | `#<HEX>` | Text/icon on secondary |
| `tertiary` | `#<HEX>` | <Role — sparingly> |
| `background` | `#<HEX>` | Page canvas |
| `on-background` | `#<HEX>` | Default text on canvas |
| `surface` | `#<HEX>` | Cards, panels |
| `on-surface` | `#<HEX>` | Primary text on surfaces |
| `on-surface-variant` | `#<HEX>` | Secondary text, captions |
| `outline` | `#<HEX>` | Default borders, dividers |
| `outline-variant` | `#<HEX>` | Subtle borders |
| `error` | `#<HEX>` | Errors, destructive states |

### Color Usage Rules

- <Rule 1, e.g. "Primary used for at most one CTA per screen.">
- <Rule 2, e.g. "Never mix primary and tertiary in the same UI region.">
- <Rule 3, e.g. "All text must meet WCAG AA (4.5:1 body, 3:1 large/bold).">
- <Rule 4, e.g. "surface-container variants define elevation layers — do not pick arbitrarily.">

### Dark Mode

<!-- Describe how the palette inverts for dark mode, or state if dark mode
     is not supported. If supported, define a second color block here.
     Typical pattern: swap surface/background to near-black, invert
     on-* colors, keep primary/tertiary close to their light values. -->

Dark mode is: supported | not supported  <!-- pick one -->

---

## Typography

<!-- FILL IN: Describe the type strategy. Name every font used, its role,
     and the reasoning behind the choice. Describe weight usage rules.

EXAMPLE (dual-font):
"Space Grotesk carries the brand voice — geometric, technical, with enough
character quirks to avoid being generic. It appears in all headings and labels.
Inter handles long-form body content; its extreme neutrality keeps reading
comfortable. Weight 300 is never used — it fails contrast at small sizes on
our dark surfaces."

EXAMPLE (single-font):
"Plus Jakarta Sans handles the entire hierarchy. Its rounded terminals and
excellent weight range let us create clear distinction between display (800),
heading (700), UI (600), and body (400) without switching fonts. Monospace
blocks use JetBrains Mono for code and data."
-->

### Font Stacks

| Token | Family | Fallback | Used for |
|-------|--------|----------|----------|
| Display/Heading | <Font Name> | system-ui, sans-serif | Headlines, labels |
| Body | <Font Name> | system-ui, sans-serif | Body copy, UI prose |
| Mono | <Font Name> | ui-monospace, monospace | Code, data, labels |

### Type Scale

| Token | Size | Weight | Line-height | Letter-spacing | Use case |
|-------|------|--------|-------------|----------------|----------|
| `display` | <px> | <num> | <ratio> | <em> | Hero headlines, large numbers |
| `headline-lg` | <px> | <num> | <ratio> | <em> | Page titles (H1) |
| `headline-md` | <px> | <num> | <ratio> | <em> | Section titles (H2) |
| `headline-sm` | <px> | <num> | <ratio> | — | Subsection titles (H3) |
| `title-lg` | <px> | <num> | <ratio> | — | Card titles, sidebar headers |
| `body-lg` | <px> | <num> | <ratio> | — | Lead paragraphs |
| `body-md` | <px> | <num> | <ratio> | — | Default body copy |
| `body-sm` | <px> | <num> | <ratio> | — | Supporting text, captions |
| `label-lg` | <px> | <num> | <ratio> | <em> | Button text (large), nav |
| `label-md` | <px> | <num> | <ratio> | <em> | Button text (default), form labels |
| `label-sm` | <px> | <num> | <ratio> | <em> | Badges, chips, small tags |
| `caption` | <px> | <num> | <ratio> | — | Timestamps, metadata |
| `mono` | <px> | <num> | <ratio> | — | Code, technical data |

### Typography Rules

- <Rule 1, e.g. "H1 appears once per page. No exceptions.">
- <Rule 2, e.g. "Never use weight 300. Minimum weight for body text is 400.">
- <Rule 3, e.g. "Display font is reserved for headlines. No display font in body copy.">
- <Rule 4, e.g. "Labels tracking: 0.05em–0.1em. Body tracking: 0 or slightly negative.">
- <Rule 5, e.g. "Max line length for body copy: 72ch. Cap reading columns at this width.">

---

## Layout

<!-- FILL IN: Describe the grid system, spacing philosophy, and container strategy.

EXAMPLE (fixed grid):
"12-column fixed grid on desktop (max 1280px, 24px gutters, 64px outer margin).
4-column on mobile (16px gutters, 16px outer margin). Spacing is strictly
8px-based. Section vertical margins jump in multiples of 64px. No half-steps
between section breaks — either 64px or 128px."

EXAMPLE (fluid):
"Content-width max at 1024px, centered. Outer padding scales from 16px
(mobile) to 48px (desktop) using clamp(). No rigid grid — layout uses
CSS Grid areas defined per section. Vertical rhythm is 24px between
content groups, 80px between page sections."
-->

### Grid

| Property | Mobile | Tablet (≥768px) | Desktop (≥1280px) |
|----------|--------|-----------------|-------------------|
| Columns | <num> | <num> | <num> |
| Gutter | <px> | <px> | <px> |
| Outer margin | <px> | <px> | <px> |
| Max content width | — | — | <px> |

### Spacing Scale

The base unit is `<px>` (typically 4px or 8px). All spacing values are multiples.

| Token | Value | Common use |
|-------|-------|------------|
| `xs` | <px> | Icon gaps, tight inline spacing |
| `sm` | <px> | Component internal padding (dense) |
| `md` | <px> | Component internal padding (default) |
| `lg` | <px> | Between components in a group |
| `xl` | <px> | Between content sections (tight) |
| `2xl` | <px> | Between content sections (default) |
| `3xl` | <px> | Between page-level sections |

### Layout Rules

- <Rule 1, e.g. "Reading columns cap at 72ch. Never let body copy span full viewport.">
- <Rule 2, e.g. "Sidebar widths are fixed. Content area is fluid.">
- <Rule 3, e.g. "Use spacing to group; use borders only when spacing alone is insufficient.">
- <Rule 4, e.g. "Touch targets: minimum 44×44px (WCAG 2.5.5).">

---

## Elevation & Depth

<!-- FILL IN: Describe how visual hierarchy is conveyed through depth.
     Common strategies: tonal layers (Material 3 style), shadows (traditional),
     glassmorphism (backdrop-filter), flat+border (no shadows at all).

EXAMPLE (tonal / flat):
"Elevation is expressed entirely through surface tone, not shadow. The five
surface-container levels define a Z-stack from lowest (page canvas) to highest
(modals). No drop shadows anywhere — borders provide edge definition where
needed. This gives the UI a sharp, editorial precision."

EXAMPLE (shadow-based):
"Three shadow levels: sm for cards at rest, md for dropdowns and sticky
headers, lg for modals. Shadows use a warm tint (primary color at 8% opacity)
rather than neutral gray to avoid the 'dirty' look of pure gray shadows."

EXAMPLE (glassmorphism):
"All interactive surfaces are semi-transparent with backdrop-filter blur.
Standard cards: blur(20px), rgba(255,255,255,0.1). Modal: blur(40px),
rgba(255,255,255,0.2). Every glass surface has a 1px solid white border at
20% opacity to simulate light refraction."
-->

### Surface Stack

| Level | Token | Use case | Border | Shadow / Depth method |
|-------|-------|----------|--------|-----------------------|
| 0 | `background` | Page canvas | none | none |
| 1 | `surface` | Sectioned areas | optional | <method> |
| 2 | `surface-container-low` | Cards at rest | `outline-variant` | <method> |
| 3 | `surface-container` | Raised cards | `outline-variant` | <method> |
| 4 | `surface-container-high` | Hover states, sidebars | optional | <method> |
| 5 | `surface-container-highest` | Modals, popovers | optional | <method> |

### Elevation Rules

- <Rule 1, e.g. "Never use shadows for decoration. Shadows only signal elevation.">
- <Rule 2, e.g. "Modals use a scrim overlay (inverse-surface at 60%) behind the dialog.">
- <Rule 3, e.g. "Interactive elevation change (hover lift) uses a 150ms ease-out transition.">

---

## Shapes

<!-- FILL IN: Describe the corner radius philosophy and when each radius is used.

EXAMPLE (soft-modern):
"Rounded corners throughout. Buttons and inputs use 8px for a modern feel.
Cards use 12px. Large panels and modals use 16px. Pills (full radius) are
reserved for badges and avatar images. Sharp (0px) corners are never used
— they signal error or system state, not design intent."

EXAMPLE (technical-precise):
"Minimum rounding. All interactive elements use 4px. Cards use 6px.
Full-radius pills are only for status badges. Sharp corners signal system
boundaries — modals, code blocks, and data tables use 0px."
-->

### Radius Scale

| Token | Value | Use case |
|-------|-------|----------|
| `none` | 0px | <e.g. Data tables, code blocks, system boundaries> |
| `sm` | <px> | <e.g. Inline badges, tight chips> |
| `md` | <px> | <e.g. Buttons, inputs, default components> |
| `lg` | <px> | <e.g. Cards, dropdowns> |
| `xl` | <px> | <e.g. Large cards, image containers> |
| `2xl` | <px> | <e.g. Featured panels, hero sections> |
| `full` | 9999px | <e.g. Pills, avatars, circular icon buttons> |

### Shape Rules

- <Rule 1, e.g. "Never mix sharp and rounded corners in the same visual group.">
- <Rule 2, e.g. "Buttons and their adjacent inputs must share the same radius.">

---

## Components

<!-- FILL IN: Describe the visual behavior and state coverage for each
     component. The YAML front matter defines exact token values; this
     section explains the *reasoning* and any CSS behavior tokens cannot capture
     (transitions, focus rings, border logic, shadow specifics).
-->

### Buttons

**Variants:** primary | secondary | ghost | destructive
**Sizes:** sm (36px height) | md (44px) | lg (52px)
**States:** default | hover | active (pressed) | focus-visible | disabled | loading

- Primary button is the sole high-emphasis action on any view. One primary button per screen.
- <Rule, e.g. "Ghost buttons inherit text color from context. They do not introduce color.">
- <Rule, e.g. "Disabled buttons use surface-container background and on-surface-variant text at 40% opacity. Never use reduced opacity on the whole element — it affects focus visibility.">
- Focus ring: `2px solid {colors.primary}`, `outline-offset: 2px`. Always `:focus-visible`, never `:focus`.
- Loading state: replace label with a spinner. Button width should not change.
- Transitions on base selector (not inside :hover): `background-color 150ms ease-out, color 150ms ease-out`.
- Touch target minimum: 44×44px. Small size buttons must pad to this minimum via padding or min-height.

### Cards

**Variants:** default | elevated | interactive | featured
**States:** default | hover (interactive variant only) | focus-visible (interactive)

- Cards never contain primary buttons unless the card is the only element in a section.
- <Rule, e.g. "Internal padding is always md (16px). Never use sm inside a card.">
- Interactive cards lift on hover — increase shadow level or darken background by one tonal step.
- Card borders: `1px solid {colors.outline-variant}` on default; none on elevated (shadow provides edge).
- Max image aspect ratio inside a card: 16:9 or 1:1. Images fill width, are never cropped in height without `object-fit: cover`.

### Inputs & Forms

**Variants:** text | textarea | select | checkbox | radio | toggle | file
**States:** default | focus | filled | error | disabled | read-only

- Every input must have a visible label. Placeholder text is not a label.
- Error state: red border (`{colors.error}`) + error icon + `aria-describedby` pointing to error message span.
- Error messages appear below the field, never inside it.
- Focus ring matches button focus ring for system-wide consistency.
- `aria-invalid="true"` on invalid fields. `aria-live="polite"` on error message region.
- Form groups (label + input + helper + error) have `md` vertical spacing between them.
- <Rule, e.g. "Date/time inputs use native browser controls with styled wrappers. No custom date pickers.">

### Navigation

**Variants:** top nav | sidebar | mobile nav (drawer) | tabs | breadcrumbs
**States:** default | hover | active/current | focus-visible

- Active nav item uses `primary-container` background and `on-primary-container` text.
- Nav items that are links must be `<a>` elements. Nav items that trigger actions must be `<button>`.
- Mobile nav collapses to a drawer or bottom bar at `<breakpoint>`.
- Skip-to-content link is the first focusable element in the DOM.
- <Rule, e.g. "Breadcrumbs use body-sm typography and on-surface-variant color except the current page (on-surface).">

### Modals & Dialogs

**Variants:** dialog (confirmation) | sheet (complex form) | drawer (side panel)
**States:** closed | open | closing (animated)

- Dialogs trap focus within the modal while open.
- Close on: Escape key, backdrop click (optional, confirm with product), explicit close button.
- Close button is in the top-right corner with an `aria-label="Close"` and a minimum 44×44px touch target.
- `role="dialog"`, `aria-modal="true"`, `aria-labelledby` pointing to the dialog title.
- Backdrop: `{colors.inverse-surface}` at 60% opacity.
- <Rule, e.g. "Confirmation dialogs: destructive action button is on the right. Cancel is always on the left.">

### Badges & Chips

**Variants:** status | count | filter (chip) | removable chip
**States:** default | hover | selected (chips) | disabled

- Status badges are read-only indicators. They are never interactive.
- Filter chips are interactive. They must have a visible selected state beyond color alone (border, checkmark, or weight change).
- Badge text is always `label-sm`. Never truncate badge text.

### Data Tables

**Variants:** basic | sortable | selectable | dense
**States:** row default | row hover | row selected | cell focus

- Tables must scroll horizontally on mobile. Never truncate column content without a full-content tooltip.
- Sortable columns: show sort icon on hover (not by default). Active sort shows direction arrow.
- Row hover uses `surface-container-high` background.
- Selected rows use `primary-container` background.
- <Rule, e.g. "Numeric columns are right-aligned. Text columns are left-aligned. Never center-align data.">

### Code Blocks

- Background: `{colors.surface-container-highest}`.
- Typography: `{typography.mono}`.
- Padding: `{spacing.md}` all sides.
- Rounded: `{rounded.md}`.
- Copy button in top-right corner. Icon-only with `aria-label="Copy code"`.
- Syntax highlighting uses a separate token set (not defined here — reference your syntax theme).

---

## Do's and Don'ts

<!-- FILL IN: Add 5-10 concrete guardrails. These are the rules agents and
     developers most often violate. Be specific — vague rules are ignored.
-->

### Do

- Use `primary` for exactly one CTA per screen. If a screen has multiple actions, secondary and ghost buttons carry the others.
- Use spacing to group related content before reaching for borders or backgrounds.
- Apply `body-md` (16px) as the default body size. Go up to `body-lg` for marketing copy; go down to `body-sm` for metadata and captions only.
- Ensure every interactive element has a visible `:focus-visible` ring — even custom components and icon buttons.
- Use token references (`{colors.primary}`) in component definitions so a color change propagates everywhere.
- Test all text/background pairs with a contrast checker before shipping. Minimum 4.5:1 for normal text, 3:1 for large text (18px+ or 14px bold+).
- <Project-specific do>
- <Project-specific do>

### Don't

- Do not use color alone to convey meaning. Pair color with an icon, pattern, or text label.
- Do not introduce a hex value directly in a component. Every color must go through a token.
- Do not use `outline: none` on interactive elements without providing an equivalent visible focus style.
- Do not use `!important` to override design token values. Fix the token or the component structure instead.
- Do not use `rgba` or `opacity` on entire components to create disabled states — it breaks focus visibility.
- Do not add drop shadows to cards that are already distinguished by border or tonal background.
- Do not truncate body copy. Truncate only metadata (labels, titles) and always provide the full value via `title` attribute or tooltip.
- <Project-specific don't>
- <Project-specific don't>

---

## Responsive Behavior

<!-- FILL IN: Define breakpoints, what collapses at each breakpoint, and
     any mobile-specific behavior (bottom nav, swipe gestures, etc.).
-->

### Breakpoints

Mobile-first. Use `min-width` queries.

| Name | Value | Target |
|------|-------|--------|
| `sm` | 640px | Large phones, landscape |
| `md` | 768px | Tablets portrait |
| `lg` | 1024px | Tablets landscape, small laptops |
| `xl` | 1280px | Desktops |
| `2xl` | 1536px | Wide desktops |

### Collapse Strategy

| Component | Mobile (<640px) | Tablet (640–1024px) | Desktop (>1024px) |
|-----------|----------------|---------------------|-------------------|
| Navigation | <e.g. Bottom nav or hamburger drawer> | <e.g. Compact sidebar> | <e.g. Full sidebar> |
| Data table | <e.g. Card stack view> | <e.g. Scrollable table> | <e.g. Full table> |
| Multi-col layout | Single column | <col count> | <col count> |
| Hero section | Stacked, full-width image | <behavior> | <behavior> |

### Mobile-Specific Rules

- Touch targets: minimum 44×44px. Pad small controls with transparent hit area rather than enlarging the visible element.
- Use `svh`/`dvh` (with `vh` fallback) for full-height viewport sections to handle iOS Safari's dynamic toolbar.
- Bottom navigation (if used): max 5 items. Labels visible at all times (no icon-only on mobile).
- Tap states use the same `:active` token as `:hover` — no hover state on touch-only interactions.
- Font sizes: minimum 16px for input fields on iOS (prevents auto-zoom on focus).
- <Project-specific mobile rule>

---

## Motion & Animation

<!-- FILL IN: Define easing curves, duration scale, and rules for motion.
     Describe which UI moments use animation and what kind.
-->

### Timing

| Token | Value | Use case |
|-------|-------|----------|
| `duration-instant` | 80ms | Micro-feedback (button press) |
| `duration-fast` | 120ms | State changes (hover, active) |
| `duration-base` | 200ms | Component transitions |
| `duration-slow` | 350ms | Page-level transitions, modals |
| `duration-xslow` | 500ms | Scroll-triggered entrances |

### Easing

| Token | Curve | Use case |
|-------|-------|----------|
| `ease-standard` | `cubic-bezier(0.2, 0, 0, 1)` | Most state changes |
| `ease-emphasized` | `cubic-bezier(0.2, 0, 0, 1)` | Expressive transitions |
| `ease-decelerate` | `cubic-bezier(0, 0, 0, 1)` | Elements entering the screen |
| `ease-accelerate` | `cubic-bezier(0.3, 0, 1, 1)` | Elements leaving the screen |
| `ease-linear` | `linear` | Progress bars, loaders |

### Motion Rules

- Define CSS transitions on the **base selector**, not inside `:hover`. This ensures the out-animation plays as well as the in-animation.
  ```css
  /* Correct */
  .button { transition: background-color 150ms ease-standard; }
  .button:hover { background-color: var(--color-primary-container); }

  /* Wrong */
  .button:hover { background-color: ...; transition: ...; }
  ```
- Scroll-reveal animations: guard behind `.js-enabled` on `<html>`. Initial state (`opacity: 0`, `transform`) must not hide content when JS is disabled.
- All animations must respect `prefers-reduced-motion: reduce`. Default to `transition: none` inside the query.
- Stagger delay between list items: 60ms–100ms. Never stagger more than 5 items.
- Page transitions (if used): entrance is decelerate easing; exit is accelerate easing.
- <Project-specific motion rule>

---

## Accessibility

<!-- FILL IN: Document the accessibility baseline for this project.
     Check each item and mark as required or not applicable.
-->

### Requirements

| Area | Standard | Status |
|------|----------|--------|
| Color contrast (body) | WCAG AA (4.5:1) | required |
| Color contrast (large text) | WCAG AA (3:1) | required |
| Keyboard navigation | All interactive elements reachable and operable | required |
| Focus visibility | `:focus-visible` on all interactive elements | required |
| Touch targets | 44×44px minimum (WCAG 2.5.5) | required |
| Skip link | Skip-to-content as first DOM element | required |
| Semantic HTML | Proper heading hierarchy, landmark regions | required |
| Form accessibility | Labels, `aria-describedby`, `aria-invalid`, `aria-live` | required |
| Images | `alt` text or `aria-hidden="true"` for decorative | required |
| Motion | `prefers-reduced-motion` respected | required |
| Dark mode | `prefers-color-scheme: dark` respected | <required/optional> |
| Screen reader tested | VoiceOver (macOS/iOS) + NVDA (Windows) | <required/optional> |

### Focus Ring

All interactive elements use a consistent focus ring:
```css
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
  border-radius: var(--rounded-sm); /* match element radius */
}
```

---

## SEO & Structured Data

<!-- FILL IN: Specify which JSON-LD schema types this project uses per page type.
     Delete entries that don't apply. Add project-specific ones.
-->

| Page type | JSON-LD schema |
|-----------|---------------|
| Home / marketing | `ProfessionalService` or `Organization` |
| Product / service page | `Service` or `Product` |
| Blog / article | `BlogPosting` or `Article` |
| FAQ section | `FAQPage` (required if FAQ markup exists) |
| Nested pages | `BreadcrumbList` |
| Author bio | `Person` |

### OG / Social Meta

- OG images must reference local assets — no external hotlinks.
- Minimum OG image size: 1200×630px.
- `og:title` and `og:description` are unique per page.
- Twitter card type: `summary_large_image`.

---

## Security Headers

<!-- FILL IN: Required before shipping. Configure in deployment host's
     config file (next.config.ts, vercel.json, _headers, nginx.conf, etc.).
     Remove any headers not applicable to your stack.
-->

```
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self'; connect-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

Tighten CSP to remove `'unsafe-inline'` from `style-src` once inline styles are eliminated.

---

## Agent Prompt Guide

<!-- FILL IN: A quick-reference block for AI agents starting new UI work.
     This is the cheatsheet — put the highest-value constraints here in
     terse, unambiguous language.
-->

When generating UI for this project:

1. **Always read the YAML front matter first.** Every color, font size, radius, spacing, and component token is defined there. Never invent values.
2. **Primary action = `{colors.primary}` background + `{colors.on-primary}` text + `{rounded.md}` radius.** One per screen.
3. **Body copy = `{typography.body-md}` (`<px>`, weight `<num>`, line-height `<ratio>`).** Never go below `body-sm` for readable content.
4. **Page canvas = `{colors.background}`. Cards = `{colors.surface-container-low}`.** Step up the surface stack for modals.
5. **Borders = `1px solid {colors.outline-variant}`.** Never hardcode a hex border color.
6. **Focus ring = `2px solid {colors.primary}`, `outline-offset: 2px`, always `:focus-visible`.**
7. **Touch targets: 44px minimum height.** All buttons and nav items.
8. **Transitions on base selector, not `:hover`.** Duration: `<ms>`. Easing: `ease-standard`.
9. **`prefers-reduced-motion: reduce` disables all transitions.** Guard every animation.
10. **No hex, rgba, or hardcoded values in component code.** Use token references only.

**Quick palette:**

| Purpose | Token | Value |
|---------|-------|-------|
| CTA button | `{colors.primary}` | `#<HEX>` |
| Page background | `{colors.background}` | `#<HEX>` |
| Card surface | `{colors.surface-container-low}` | `#<HEX>` |
| Primary text | `{colors.on-surface}` | `#<HEX>` |
| Secondary text | `{colors.on-surface-variant}` | `#<HEX>` |
| Border | `{colors.outline-variant}` | `#<HEX>` |
| Error | `{colors.error}` | `#<HEX>` |

**Sample prompt to kick off a new page:**
> "Read DESIGN.md. Build a [page name] using the token system defined there. Primary action is a single `button-primary`. Use `surface-container-low` for card backgrounds. Follow the breakpoint collapse strategy in the Responsive Behavior section."
