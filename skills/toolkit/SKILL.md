---
name: toolkit
description: Pull up the production-toolkit repo -- visual galleries, component libraries, DESIGN.md template, AI build instructions, and universal project rules. Use when starting any web design/frontend project or when you need to browse design resources.
user-invocable: true
allowed-tools: "Read Write Edit Bash"
---

# Production Toolkit

Load the production-toolkit repo for design resources, visual galleries, and project scaffolding files.

## What to do

1. Check if `/tmp/production-toolkit/` exists locally. If not, clone it:
   ```
   git clone https://github.com/Kevsosmooth/production-toolkit.git /tmp/production-toolkit
   ```
   If it already exists, pull the latest:
   ```
   cd /tmp/production-toolkit && git pull
   ```

2. Read these files in order, summarizing each to the user:

   | File | Purpose |
   |------|---------|
   | `README.md` | Visual galleries, component libraries, boilerplates, theme editors, inspiration sites |
   | `AI-INSTRUCTIONS.md` | Decision framework: how to pick libraries, browsing workflow, quality checklist |
   | `DESIGN.md` | Fillable design system template (copy into new projects) |
   | `RULES.md` | Universal AI project rules (phase discipline, simplicity, frontend, accessibility) |

3. After reading, present the user with a short summary:
   - Number of visual galleries and component libraries available
   - The 5-step design workflow (study niche, browse inspiration, pick components, customize theme, build)
   - Offer to copy DESIGN.md and RULES.md into the current project if they don't already exist

## When starting a new project

If the user is starting a new web project, offer to:
1. Copy `DESIGN.md` template into the project root
2. Copy `RULES.md` into the project root
3. Copy `AI-INSTRUCTIONS.md` into the project root
4. Walk through the DESIGN.md template together to fill in their brand identity

## Quick reference

The toolkit README contains links to:
- **15+ copy-paste component galleries** (shadcn Blocks, Magic UI, Aceternity UI, 21st.dev, React Bits, Flowbite, Preline, etc.)
- **Admin templates and SaaS boilerplates** with live demos
- **Visual theme editors** (tweakcn, 10000+ Themes, shadcn Themes)
- **Design inspiration sites** (Godly, Land-book, Mobbin, SiteInspire, Httpster)
- **Component library comparison** (HeroUI, shadcn, Mantine, Ant Design, Tremor)
- **Animation library guide** (Framer Motion, GSAP, Magic UI, Motion Primitives)

Always show the user what's available visually before writing any CSS or component code.
