# AI Build Instructions

How to use this toolkit and build websites that look professional, unique, and nothing like everyone else's.

This file is written for AI coding assistants (Claude, Cursor, Copilot, Codex, Gemini) but humans should read it too. It codifies real developer and designer opinions on what separates premium work from generic template output.

---

## The Problem You Are Solving

Every AI-built site looks the same. Developers and designers can spot them instantly:

- Dark hero with a vague one-liner and a floating dashboard screenshot
- Purple/blue gradient backgrounds
- Default shadcn/Tailwind color palette with zero customization
- Glassmorphism cards (rgba semi-transparent + backdrop blur)
- Scroll-triggered animations on every section
- Poppins or Inter font at default weights
- Giant meaningless headings that explain nothing
- Custom cursor blobs, marquee tickers, scroll hijacking

**Your job is to avoid all of this.** The sites you build should feel like a human designer spent weeks on them.

---

## Before You Write Any Code

### Step 1: Read the project files in this order

1. `AGENTS.md` -- dev commands, testing, PR conventions, code structure
2. `DESIGN.md` -- visual identity, tokens, typography, elevation, do's and don'ts
3. `CLAUDE.md` / `.cursorrules` / `.cursor/rules/*.mdc` -- project-specific overrides

If a `DESIGN.md` exists, it is your source of truth for every visual decision. Never override it with your own aesthetic preferences.

### Step 2: If no DESIGN.md exists, ask for one

Do not start building UI without a defined visual identity. Either:
- Ask the user to describe their brand, audience, and aesthetic preferences
- Generate a DESIGN.md using the Google/Stitch format (YAML front matter + prose sections)
- Reference `awesome-design-md` for real-brand examples to pull inspiration from

### Step 3: Research the niche

Before designing, look at what competitors in the same industry are doing. A realtor site should not look like a SaaS dashboard. A creative agency should not look like a fintech app. Context matters more than trends.

---

## The Rules

### 1. Zero Hardcoded Values -- Non-Negotiable

No hex code, rgb value, font-family string, pixel spacing, border-radius, or shadow value may ever appear in a component file. Everything must reference design tokens or CSS custom properties.

```
CORRECT:  className="bg-surface text-on-surface border-border-default"
WRONG:    className="bg-[#18181b] text-[#B8B8B8] border-[rgba(255,255,255,0.08)]"
```

This is the single most important rule. It prevents the "default Tailwind/shadcn" look that every developer can spot. When you define your own tokens, your site automatically looks different from every other shadcn site.

### 2. Typography Is Your Fastest Differentiator

Font choice is the #1 signal of whether a site was designed or generated.

**Do:**
- Pick a distinctive display font. Not Poppins. Not Inter at default weight. Not system fonts.
- Use tight letter-spacing on large headings (-0.02em to -0.04em)
- Define at least 6 typography levels (display, headline, title, body, label, caption)
- Use a dual-font strategy: one for display/headings, one for body text
- Limit to 2 font weights per screen maximum

**Don't:**
- Use Poppins -- it immediately signals "template"
- Use more than 2 typefaces total
- Leave letter-spacing at defaults for headings above 32px
- Mix font weights inconsistently across components

**Good font pairings to consider:**
- Plus Jakarta Sans + JetBrains Mono (modern, technical)
- Space Grotesk + Inter (geometric, clean)
- Outfit + Source Sans 3 (friendly, professional)
- Sora + DM Sans (contemporary, balanced)
- General Sans + Satoshi (editorial, premium)

### 3. Color Must Be Semantic, Not Decorative

Use Material Design 3 naming conventions for your tokens:

| Token | Purpose |
|-------|---------|
| `primary` | Brand color, single most important action per screen |
| `on-primary` | Text/icon color on primary surfaces |
| `surface` | Main background |
| `on-surface` | Default text color |
| `surface-container` | Elevated cards, sections |
| `outline` | Borders, dividers |
| `error` | Destructive actions, validation errors |

**The key rule:** Primary color appears on ONE action per viewport. Not two buttons, not three links. One. This alone prevents the "everything is highlighted so nothing is" problem.

### 4. Copy Must Be Specific, Not Poetic

The single most upvoted complaint about AI sites: "I scrolled three sections and still don't know what they sell."

**Do:**
- Hero headline states exactly what the product/service does and for whom
- Subheadline adds one specific proof point or differentiator
- Every section heading answers "what will I learn by reading this?"

**Don't:**
- Write vague aspirational headlines ("Elevate Your Digital Presence")
- Use buzzwords without substance ("AI-Powered Solutions for Modern Teams")
- Hide the actual value proposition below the fold
- Prioritize cleverness over clarity

**Example:**
```
BAD:   "Transforming Digital Experiences"
GOOD:  "Custom websites for realtors that actually generate leads"

BAD:   "Innovative Solutions"
GOOD:  "I design and build property listing sites that load in under 2 seconds"
```

### 5. Animation: Less Is More, and It Must Have Purpose

Every animation must answer: "What does this help the user understand?"

**Do:**
- Use entrance animations that fire once on scroll
- Stagger delay 80-120ms between list items
- Respect `prefers-reduced-motion` -- always
- Use spring/ease-out curves, never linear
- Animate opacity + translateY for entrances (subtle, 12-20px movement)

**Don't:**
- Animate every section on scroll -- pick 2-3 key moments
- Use scroll hijacking or sticky scroll takeover
- Add custom cursor effects (blobs, trails, spotlights)
- Use marquee tickers
- Make users wait for content to animate in before they can read it
- Use glassmorphism (rgba semi-transparent + backdrop blur) -- it's exhausted

### 6. Depth and Elevation: Pick One Strategy

Do not mix depth strategies. Choose one and apply it consistently:

| Strategy | When to Use | Tokens |
|----------|------------|--------|
| **Tonal layers** | Minimal, modern (Linear, Notion style) | Different surface colors, no shadows |
| **Subtle shadows** | Professional, trustworthy | 3-4 level shadow scale |
| **Borders only** | Clean, editorial | 1px borders + color contrast |

Never use `box-shadow` without defining it as a token first.

### 7. Layout: 8px Grid, Always

- Base spacing unit: 8px
- All spacing values must be multiples of 8 (8, 16, 24, 32, 48, 64, 80, 96, 128)
- Container max-width: define it (1200-1400px is standard)
- Content padding: at least 16px on mobile, 24-32px on desktop
- Section vertical spacing: 64-128px (generous whitespace signals premium)

### 8. Mobile First, Tested on Real Sizes

- Start at 375px width, enhance with breakpoints
- Touch targets: 44x44px minimum (WCAG 2.5.5)
- Test on 1366x768 -- this is what most real users have, not your 27" monitor
- Use `svh`/`dvh` viewport units with `vh` fallback for iOS Safari
- Navigation must collapse cleanly -- no horizontal overflow, no tiny hamburger

### 9. Images and Visuals

- Real photography or custom illustrations -- never stock photos of people shaking hands
- If no images are available, use abstract shapes, patterns, or solid color blocks
- OG/Twitter meta images must reference local assets, not external URLs
- Optimize all images (WebP/AVIF, proper dimensions, lazy loading)
- If grain/texture overlay is used: keep it subtle, apply to specific sections, use WebP not GIF

### 10. Accessibility Is Not Optional

- Visible `:focus-visible` states on every interactive element
- WCAG AA contrast minimum (4.5:1 body text, 3:1 large text)
- Semantic HTML, proper heading hierarchy (h1 > h2 > h3, no skipping)
- `aria-labels` on icon-only buttons
- Skip-to-content link
- Forms: `aria-describedby`, `aria-invalid`, `aria-live` for status messages
- Screen reader testing on key flows

---

## How to Pick Libraries From the Toolkit

Use TOOLKIT.md as your menu. Here is the decision framework:

### Component Library

| Situation | Pick |
|-----------|------|
| Need polished defaults, fast shipping | HeroUI |
| Need full ownership of code, Tailwind-native | shadcn/ui |
| Need 100+ components, batteries included | Mantine |
| Enterprise admin panel with data tables | Ant Design |
| Dashboard with charts and KPIs | Tremor |

**Rule:** Pick ONE primary component library. Do not mix HeroUI buttons with Chakra modals with MUI data tables. Consistency is the point.

### Animation

| Situation | Pick |
|-----------|------|
| Standard React animations, gestures, layout | Framer Motion |
| Complex timeline/scroll-driven sequences | GSAP |
| Pre-built landing page effects (shimmer, glow) | Magic UI |
| Subtle, design-forward motion patterns | Motion Primitives |
| Zero-config list transitions | AutoAnimate |

**Rule:** Framer Motion is the base layer. Add Magic UI or Motion Primitives for specific effects. Do not use all three animation libraries plus GSAP -- pick your lane.

### State Management

| Situation | Pick |
|-----------|------|
| Server data (API calls, caching) | TanStack Query |
| Simple global state (theme, user prefs) | Zustand |
| Atomic/granular reactivity | Jotai |
| Complex multi-step flows | XState |
| Light data fetching, Vercel stack | SWR |

**Rule:** Most sites need TanStack Query + Zustand at most. Do not add state management until you actually need shared state.

### Database

| Situation | Pick |
|-----------|------|
| Full backend in one service, fast prototyping | Supabase |
| Type-safe ORM, established ecosystem | Prisma |
| Edge deployments, minimal overhead | Drizzle |

### Auth

| Situation | Pick |
|-----------|------|
| Free, self-hosted, flexible | Auth.js (NextAuth v5) |
| Best DX, pre-built UI, team/org support | Clerk |
| Maximum control, thin abstraction | Lucia |

---

## Quality Checklist Before Shipping

Run through this before calling any page "done":

### Visual Quality
- [ ] No hardcoded color, font, spacing, or shadow values in any component
- [ ] Typography hierarchy is consistent (display > headline > title > body > label)
- [ ] Primary color used for maximum ONE action per viewport
- [ ] Whitespace is generous -- sections breathe
- [ ] Site does not look like default shadcn/Tailwind

### Content Quality
- [ ] Hero immediately communicates what the product/service does
- [ ] No vague buzzword headlines
- [ ] Every section heading is specific and useful
- [ ] Real images or intentional abstract visuals (no generic stock)

### Technical Quality
- [ ] Mobile responsive from 375px up
- [ ] Touch targets 44x44px minimum
- [ ] All animations respect `prefers-reduced-motion`
- [ ] No scroll hijacking or custom cursor effects
- [ ] Images optimized (WebP/AVIF, lazy loaded, properly sized)
- [ ] Lighthouse performance score above 90

### Accessibility
- [ ] Visible `:focus-visible` states on all interactive elements
- [ ] WCAG AA contrast on all text
- [ ] Proper heading hierarchy, no skipped levels
- [ ] `aria-labels` on icon-only buttons
- [ ] Skip-to-content link present
- [ ] Forms have proper `aria-describedby` and `aria-invalid`

### SEO
- [ ] Unique `<title>` and meta description per page
- [ ] JSON-LD structured data appropriate to page type
- [ ] OG images reference local assets
- [ ] Sitemap and robots.txt present

### Security
- [ ] No secrets in committed code
- [ ] Security headers configured (CSP, X-Frame-Options, Referrer-Policy)
- [ ] Form input validated client and server side

---

## Inspiration Sources (Not Awards Sites)

When you need visual direction, check these -- they show real sites in actual use, not experimental showpieces:

| Source | What It Is | URL |
|--------|-----------|-----|
| **Competitor sites in the same niche** | The most useful reference. What are others in the same industry actually doing? | (search manually) |
| **Mobbin** | Real app/web UI with filters by industry and pattern | mobbin.com |
| **Godly** | Curated high-quality web design | godly.website |
| **SiteInspire** | Design-focused, real sites | siteinspire.com |
| **Land-book** | Landing page gallery | land-book.com |
| **One Page Love** | Curated one-pagers | onepagelove.com |
| **Httpster** | Clean, well-designed sites | httpster.net |
| **Codrops** | Experimental techniques and tutorials | tympanus.net/codrops |
| **maxibestof** | Filterable by fonts used | maxibestof.one |

---

## File Structure for New Projects

Every project should have these files at root:

```
project/
  AGENTS.md          -- dev commands, testing, PR conventions
  DESIGN.md          -- visual identity, tokens, do's and don'ts
  CLAUDE.md          -- AI-specific code rules and overrides
  TOOLKIT.md         -- this toolkit reference (copy from repo)
  AI-INSTRUCTIONS.md -- this file (copy from repo)
```

`DESIGN.md` handles how it should look. `CLAUDE.md` handles how the code should be written. `AI-INSTRUCTIONS.md` handles the philosophy and decision-making framework. `TOOLKIT.md` is the parts catalog.

---

## The One Thing to Remember

The difference between a generic AI site and a professional one is not the tools -- it is the decisions. Anyone can install shadcn and Framer Motion. What matters is:

- Choosing a distinctive typeface and using it with intention
- Defining a color system with semantic roles, not just "pick a nice blue"
- Writing copy that says something specific instead of something safe
- Leaving enough whitespace that the design can breathe
- Knowing when NOT to animate, NOT to add effects, NOT to follow trends

Restraint is the skill. The best sites are defined by what they leave out.
