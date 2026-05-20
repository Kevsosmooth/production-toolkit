---
name: toolkit
description: Active project scaffolder and design-system tool. Use when starting any new web project (marketing site, dashboard, SaaS, admin panel, e-commerce, frontend for an existing API), adding a design system to an existing project, picking libraries, picking a font / palette / component kit, or fixing a UI that looks generic. Fires on intents like scaffold, start a project, set up a frontend, build a dashboard, design system, pick a font, pick a palette, pick a library, fix the look, make the UI look better, browse component galleries.
user-invocable: true
allowed-tools: "Read Write Edit Bash AskUserQuestion Agent Skill"
---

# Production Toolkit -- Active Scaffolder

This skill is a project scaffolder and design-system tool, not a reference doc.
It probes the current directory, runs an adaptive interview, previews exactly
what it will do, then scaffolds the project end-to-end with a real design system
already wired in.

## Phase flow (always run in order)

0. **Target** -- ensure templates are available locally; ask the user which directory to scaffold into
1. **Probe** -- silent context detection in the target directory, no questions
2. **Present context** -- one short paragraph summarizing what was found, user confirms scope
3. **Interview** -- adaptive multiple-choice questions, skipping anything the probe already answered
4. **Preview** -- write a summary of every file and command that will run, user approves
5. **Execute** -- scaffold the project, install deps, write tokens, copy templates, build sample pages, commit

The phases are not optional. Skipping a phase produces generic output, which is the
problem this skill exists to solve.

---

## Phase 0: Target directory + template availability

Do two things before any probe.

### 0.1 -- Ensure templates exist locally

The skill reads templates from one of these paths, first that exists wins:

1. `/volume1/playground/dev-tool-docs/production-toolkit/` (source of truth, Kevin's working copy)
2. `/tmp/production-toolkit/` (clone fallback)

If neither exists, clone the GitHub remote into the fallback path:

```bash
test -d /volume1/playground/dev-tool-docs/production-toolkit || test -d /tmp/production-toolkit || \
  git clone https://github.com/Kevsosmooth/production-toolkit.git /tmp/production-toolkit
```

If the source-of-truth path exists, run `git pull --ff-only` on it (silent; ignore failures) so the templates are current. If only the fallback exists, run `git pull --ff-only` on it for the same reason. Never read templates from `/root/.claude/plugins/marketplaces/production-toolkit/` -- that path is a read-only mirror that gets overwritten on plugin updates.

### 0.2 -- Ask the user where to scaffold

Run `pwd` to get the current shell directory. Then use `AskUserQuestion` with these two options (substitute the real pwd into the first label):

- **This directory: `<pwd>`** -- scaffold into the dir the shell is currently in
- **A different path** -- user types an absolute path; create the dir if missing

If the user picks "A different path", validate the chosen path:
- Reject paths inside `/volume1/playground/dev-tool-docs/production-toolkit/` (would create a circular reference)
- If the path doesn't exist, ask "create it?" before `mkdir -p`
- If the path is non-empty and contains files unrelated to a scaffold (not just `.git`, `.gitkeep`, or hidden dotfiles), warn before continuing; require explicit "yes overwrite" before any later phase touches a file

Once the target is confirmed, `cd` into it. All subsequent phases operate in the target directory, NOT in the invocation directory.

---

## Phase 1: Probe

Run these checks silently inside the target directory (the one chosen in Phase 0). Do not narrate. Collect the results into a context object.

```bash
pwd
ls -la .
ls -la .. 2>/dev/null | head -30
test -f package.json && cat package.json | head -50
test -f README.md && head -40 README.md
test -f DESIGN.md && echo "DESIGN-EXISTS"
test -f CLAUDE.md && echo "CLAUDE-EXISTS"
test -f AGENTS.md && echo "AGENTS-EXISTS"
test -d .git && echo "GIT-INIT" || echo "NO-GIT"
ls ../ 2>/dev/null | grep -E "(api|backend|server)" | head -5
```

Then for any sibling directories that look like a backend (matching `*-api`, `*-backend`, `*-server`, or containing `package.json` with a server framework), peek at their README to understand what's already wired:

```bash
for sib in $(ls ../ 2>/dev/null); do
  if [ -f "../$sib/package.json" ] && grep -qE "(fastify|express|hono|nestjs|koa)" "../$sib/package.json" 2>/dev/null; then
    echo "BACKEND: ../$sib"
    test -f "../$sib/README.md" && head -20 "../$sib/README.md"
  fi
done
```

Classify the situation into one of:

- `empty-new` -- current dir is empty or only has hidden files. No siblings of note.
- `empty-with-sibling-backend` -- current dir is empty, but a sibling directory contains a server framework. The user is starting a frontend for an existing API.
- `existing-project` -- current dir has package.json. We are adding to or refactoring an existing project.
- `existing-with-design` -- current dir has both package.json AND DESIGN.md. Design system already exists; the user wants to extend it or pick more components.

## Phase 2: Present context and confirm scope

Write ONE paragraph showing what the probe found, what scope follows from it, and ask the user to confirm or correct in one line. Example for `empty-with-sibling-backend`:

> I see an empty `platform-admin/` directory next to a `booking-api/` sibling that has Fastify, Drizzle, auth, Stripe, Postmark, and pg-boss wired (per its README). So this is a frontend for an existing API. The interview will skip database, server-side auth, payments backend, and email backend, and focus on: framework, visual design, component library, API client, state management, sample shell pages. Sound right?

Wait for the user's confirmation before continuing. If they correct the scope, adjust the interview question list accordingly before proceeding.

## Phase 3: Adaptive interview

Use `AskUserQuestion` for every question. Each question is multiple choice with 2-4 options plus "Other" available automatically. Each option label includes the name and a one-line tradeoff so the user can choose without reading docs.

**Which questions to ask depends on the context classification:**

| Question | empty-new | empty-with-sibling-backend | existing-project | existing-with-design |
|---|---|---|---|---|
| Framework | ask | ask | skip (detect from package.json) | skip |
| Visual style direction | ask | ask | ask (if no DESIGN.md) | skip |
| Font pairing | ask | ask | ask (if no DESIGN.md) | skip |
| Primary brand color | ask | ask | ask (if no DESIGN.md) | skip |
| Density / motion stance | ask | ask | ask (if no DESIGN.md) | skip |
| Component library | ask | ask | ask (if not installed) | confirm match |
| Icon set | ask | ask | ask (if not installed) | confirm match |
| Animation library | ask | ask | ask (if not installed) | ask |
| Auth strategy | ask | skip | ask | ask |
| Database | ask | skip | ask | ask |
| Payments | ask | skip | ask | ask |
| Email | ask | skip | ask | ask |
| API client + state | ask (if API exists) | ask | ask | ask |
| Background jobs | ask | skip | ask | ask |
| Deployment target | ask | ask | ask | ask |
| Pages to scaffold | ask | ask | ask (additive) | ask (additive) |

**Question bank** (one ask per dimension; copy options verbatim where possible):

### Q-FRAMEWORK -- "Which framework?"
- Next.js 15 App Router (recommended for most SaaS / dashboards / SSR-needed pages -- best Vercel integration, biggest ecosystem)
- Astro (best for content-heavy + marketing; ships zero JS by default)
- Remix / React Router v7 (best for nested-layout heavy apps)
- SvelteKit (smallest bundle, smaller ecosystem)

### Q-STYLE -- "Visual style direction?"
- Editorial / Brutalist (Granola, Things, Pitch -- massive type, monochrome, single accent)
- Linear / Premium Dark (Linear, Raycast, Vercel -- dark default, dense data, command palette)
- Warm / Notion / Cron (cream backgrounds, rounded, friendly serif headings)
- Bento / Apple (tiled stat cards, subtle glassmorphism, vibrant accents)
- Calendar SaaS (Cal.com, Calendly -- light, calendar-blue, generic-modern)
- Custom (open-ended, user describes)

### Q-FONT -- "Font pairing?"
- Plus Jakarta Sans + JetBrains Mono (modern, technical, default)
- Space Grotesk + Inter (geometric, clean)
- Outfit + Source Sans 3 (friendly, professional)
- Sora + DM Sans (contemporary, balanced)
- General Sans + Satoshi (editorial, premium)
- ABC Diatype / Geist / other display font (Brutalist; user names it)
- Custom pair (user names both)

### Q-COLOR -- "Primary brand color?"
Free-text hex (e.g., `#2563EB`). Validate hex format; if invalid, re-ask.
After capture, offer to derive the rest of the palette (hover, focus ring, soft bg) automatically OR have the user paste a tweakcn.com URL whose theme to import.

### Q-DENSITY -- "Density and motion?"
- Airy + minimal motion (lots of whitespace, transitions only on state changes)
- Balanced + moderate motion (default for most SaaS)
- Compact + expressive (information-dense, lots of stagger animations -- careful, easy to overdo)

### Q-COMPONENTS -- "Primary component library?"
- shadcn/ui (recommended -- you own the code; pair with the toolkit's tweakcn theme)
- HeroUI (polished defaults, gradients, faster to ship if you like the look)
- Mantine (batteries-included: 100+ components, hooks, forms, date pickers)
- Radix UI Themes (premium, geometric, opinionated -- Linear-adjacent)

### Q-ICONS -- "Icon set?"
- Lucide (recommended; default in shadcn; 1,500+ icons)
- Tabler Icons (6,000+ free MIT)
- Heroicons (Tailwind team's set; outline + solid only)
- Phosphor Icons (6 weights per icon, distinct character)

### Q-ANIMATION -- "Animation library?"
- Motion / Framer Motion (the standard; declarative; covers 90% of needs)
- Motion Primitives (subtler, design-forward presets on top of Motion)
- Magic UI (high-impact marketing components -- great for landing pages, overkill for admin)
- None (CSS transitions only; smallest bundle)

### Q-API-CLIENT -- "API client + server state?"
- TanStack Query + Zustand (recommended for most cases; caching + simple global state)
- SWR + Zustand (Vercel stack; simpler than TanStack Query)
- TanStack Query + Jotai (atomic state for granular reactivity)
- Native fetch + React Context (smallest bundle; harder to scale)

### Q-AUTH -- "Auth strategy?" (only if no sibling backend handles it)
- Backend session cookies (the API issues HttpOnly cookies; this app just reads them)
- Auth.js / NextAuth v5 (this app handles OAuth + magic link in-process)
- Clerk (managed; pre-built UI; team / org support out of box)
- Lucia (minimal; full control over sessions)
- None / public

### Q-DEPLOY -- "Deployment target?"
- Vercel (default for Next.js; preview URLs per PR)
- Render (long-running processes; good for Fastify backends too)
- Cloudflare Pages / Workers (edge; 0ms cold starts; smaller bundle ceiling)
- Self-host (Docker; user owns the box)

### Q-PAGES -- "Sample shell pages to scaffold first?"
Multi-select. Options:
- Login / signup form pages
- Dashboard home (with placeholder stats + activity feed)
- Settings shell (with tabs for profile / preferences / security)
- 404 + error pages
- Marketing landing (only for empty-new + marketing-style scope)

If the answer to Q-FONT is "Custom", ask follow-up: "Name the display font and the body font, both from Google Fonts or named with download links."

If the answer to Q-COMPONENTS is "shadcn/ui", note that the executor must run `npx shadcn@latest init` interactively-or-non-interactively with the picked theme tokens.

## Anti-AI-slop guardrail (read before locking design)

AI builds look like AI because the model defaults to the *statistical average* of its training data (the untouched Tailwind UI look). Before you preview or scaffold any UI, run the design against the full **"How People Spot AI Apps Fast -- The Tell List"** in `AI-INSTRUCTIONS.md`. Three or more tells = it reads as AI-generated. The instant giveaways to refuse by default:

- **Purple/indigo→violet gradients** and any untouched Tailwind palette (`indigo-500`, `blue-500`, `slate-*`). Use the project's own tokens only.
- **Inter / Roboto / Poppins / system fonts** at default weights. Pick a distinctive display + body pairing.
- **Three identical rounded cards**, uniform 16px radius, centered single-column symmetry, the hero→3-features→CTA skeleton.
- **Untouched shadcn defaults**, outline badges (tinted bg + colored text + border), mixed depth strategies, overused glassmorphism.
- **Vague hero copy** ("Elevate your X", "Build the future"), buzzwords, emoji bullets, lorem ipsum, undraw.co blobs.
- **Fade-in-up on everything**, linear easing, no empty/loading/error states, no `:focus-visible`.

The fix is always the same: taste lives in the constraints. Lock the tokens + voice in `DESIGN.md` first, then build only from those. If a screen could belong to any product, it is not done.

## Phase 4: Preview

Once the interview is done, write a structured preview and present it to the user.

Required preview sections:
- **Picks summary** -- table of question -> answer
- **Files to create** -- list with paths
- **Files to modify** -- list with paths (if any)
- **Dependencies to install** -- npm/pnpm install commands
- **Commands to run** -- in order, with brief rationale
- **First commit message** -- exact text

Example preview opening (use this shape; fill in real values):

> Here's what I'll do. Tell me to GO, or tell me which pick to change.
>
> **Picks:** Next.js 15 App Router, Editorial style, Plus Jakarta Sans + JetBrains Mono, #18181B primary, balanced + moderate motion, shadcn/ui, Lucide icons, Motion library, TanStack Query + Zustand, backend session cookies, Vercel deploy, login + dashboard + settings + 404 pages.
>
> **Will create:** [list of files]
>
> **Will install:** [exact npm install lines]
>
> **Will run:** [exact commands]
>
> **First commit:** `chore(scaffold): initial scaffold via /toolkit`

Wait for explicit GO before Phase 5. Do not infer approval from silence.

## Phase 5: Execute

Run the scaffold in this order. After each major step, update task tracking. If any step fails, STOP and report the failure -- do not continue past a broken step.

1. **Initialize the framework** (e.g., `npx create-next-app@latest . --typescript --tailwind --app --no-eslint --no-src-dir --import-alias "@/*"` for Next.js). Use non-interactive flags; pass `.` to scaffold in the current directory.
2. **Copy the four toolkit files** from `/volume1/playground/dev-tool-docs/production-toolkit/` (or `/tmp/production-toolkit/` if the source repo is not present):
   - `DESIGN.md` -- start with the empty template
   - `RULES.md`
   - `AI-INSTRUCTIONS.md`
   - `README.md` -- one-line project description; the toolkit's README is reference, the project README is intro
3. **Fill DESIGN.md** with the answers from Phase 3. Convert hex color into the YAML token fields. Convert font pairing into typography tokens. Add the "Design References" section listing the chosen style direction and any sites the user named.
4. **Write `app/globals.css`** with the design tokens as CSS custom properties, both light and dark mode.
5. **Install picked libraries** in the right order: framework first, then component library (`npx shadcn@latest init` for shadcn), then icon set, then animation lib, then state libs, then API client.
6. **Set up the font** in `app/layout.tsx` (Google Fonts for the picked pair; `next/font/google` for Next.js projects).
7. **Scaffold the sample pages** picked in Q-PAGES. Use shadcn Blocks where they fit; otherwise hand-roll thin shells. Pages should compile and render with the tokens applied. Do not stub with `lorem ipsum` -- use realistic content that matches the project type.
8. **Create `lib/api.ts`** (only if sibling backend exists) with a typed fetch wrapper pointing at the backend's URL. Inherit auth strategy from Q-AUTH.
9. **Set up the basic `app/(auth)` and `app/(app)` route groups** if the project has auth.
10. **Commit and check the dev server runs** -- `npm run dev` in background, fetch `http://localhost:3000` once, confirm 200 response, kill the server. Commit with the message from Phase 4 preview.

After the scaffold is committed, report back:
- What's installed and where
- The dev server command (`npm run dev`)
- The next 1-2 things the user might want to do (e.g., "Open `DESIGN.md` to review the filled tokens", "Run `/toolkit` again to add more pages")

## Adaptive rules -- when to skip phases

- If `DESIGN.md` exists and is filled (not the empty template), Phase 3's visual questions skip; ask only "extend or refactor the design system?"
- If `package.json` exists, Phase 3's framework + already-installed-library questions skip; treat as additive scaffold.
- If `.git` exists, Phase 5's `git init` step is replaced with a regular commit on the current branch.
- If the user passes an explicit phase shortcut (e.g., "just fill DESIGN.md, don't scaffold"), respect that and stop at the named phase.

## Reference: where the production-toolkit repo lives

- Source of truth (Kevin's working copy): `/volume1/playground/dev-tool-docs/production-toolkit/`
- Local cache (clone fallback): `/tmp/production-toolkit/`
- Plugin install (read-only mirror): `/root/.claude/plugins/marketplaces/production-toolkit/`
- GitHub remote: `https://github.com/Kevsosmooth/production-toolkit`

Always read templates from the source of truth or the local cache, never from the plugin install (that gets overwritten on plugin updates).

## Tone and pacing

- One AskUserQuestion call per dimension. Do not batch multiple unrelated questions into one screen.
- No filler narration between phases ("Now I will...", "Next, I'll..."). The tool call IS the announcement.
- After Phase 5 completes, end with a 2-line summary: what shipped + what the user might do next. No paragraph recap.
- Never claim "scaffolded" or "ready" without verifying the dev server returned 200 and the git commit landed.
