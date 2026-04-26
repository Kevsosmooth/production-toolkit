# Production Toolkit

Curated frameworks, libraries, and tools for shipping high-quality projects fast.
Built for developers and AI coding assistants who want to stop building sites that all look the same.

Last updated: 2026-04-26.

## What's In This Repo

| File | Purpose |
|------|---------|
| [README.md](README.md) | The parts catalog -- every framework, library, and tool worth using, organized by category |
| [AI-INSTRUCTIONS.md](AI-INSTRUCTIONS.md) | How AI should use this toolkit -- decision frameworks, anti-patterns, quality checklists, and the philosophy that separates professional output from generic template slop |
| [RULES.md](RULES.md) | Universal project rules for AI assistants -- phase discipline, simplicity gatekeeping, frontend quality, security, testing, context management. Drop into any project root. |
| [DESIGN.md](DESIGN.md) | Fillable design system template -- YAML tokens + prose rationale. Compatible with Google/Stitch spec. Covers colors, typography, spacing, elevation, components (with all states), responsive behavior, motion, accessibility, SEO, and security headers. |

### How to Use

1. Copy all four files into your project root
2. Fill in `DESIGN.md` with your project's actual design values (replace every `<PLACEHOLDER>`)
3. The AI reads the files in order: `DESIGN.md` (how it looks) > `RULES.md` (how to behave) > `AI-INSTRUCTIONS.md` (how to decide) > `README.md` (what tools exist)
4. Run `npx @google/design.md lint DESIGN.md` to validate tokens and WCAG contrast

---

## Visual Galleries (Browse Before You Build)

Stop coding from imagination. Open these sites, browse visually, find what you like, then build.

### Copy-Paste Component Galleries

Live previews where you click a component, see it running, and grab the code.

| Gallery | What You Browse | URL |
|---------|----------------|-----|
| **shadcn/ui Blocks** | Full page layouts -- dashboards, login, settings, music player, mail client. Copy the whole page. | [ui.shadcn.com/blocks](https://ui.shadcn.com/blocks) |
| **Magic UI** | Animated sections -- shimmer cards, particle heroes, glow effects, cursor trails. Tailwind + Framer Motion. | [magicui.design](https://magicui.design) |
| **Aceternity UI** | High-impact landing page sections -- 3D cards, spotlight effects, animated gradients, typewriter text. | [ui.aceternity.com](https://ui.aceternity.com) |
| **21st.dev** | Marketplace of designer-made shadcn blocks -- hero sections, pricing tables, feature grids, footers. Filter by category. | [21st.dev](https://21st.dev) |
| **React Bits** (38k stars) | Animated interactive React components with live demos -- text effects, animations, backgrounds, buttons. | [reactbits.dev](https://reactbits.dev) |
| **Flowbite** (9.2k stars) | 600+ Tailwind components with visual docs -- navbars, forms, modals, cards, dropdowns, tables. | [flowbite.com](https://flowbite.com) |
| **Preline UI** (6.3k stars) | Large Tailwind component set with live previews -- layouts, overlays, navigation, data display. | [preline.co](https://preline.co) |
| **TW Elements** (13k stars) | 500+ Tailwind components -- carousels, accordions, timelines, charts, steppers. All previewable. | [tw-elements.com](https://tw-elements.com) |
| **Float UI** (3.5k stars) | Beautiful responsive sections for React + Tailwind -- hero, features, pricing, CTA, testimonials. | [floatui.com](https://floatui.com) |
| **Meraki UI** (2.7k stars) | Clean Tailwind components with RTL support. Visual gallery with code toggle. | [merakiui.com](https://merakiui.com) |
| **Inspira UI** (4.6k stars) | Vue/Nuxt component library with animated previews. | [inspira-ui.com](https://inspira-ui.com) |
| **Creative Tim** (11.8k stars) | Open-source blocks, page sections, and full templates. Import into any project. | [creative-tim.com](https://www.creative-tim.com) |
| **Pattern Craft** (2.8k stars) | Background patterns and gradients -- visual gallery, copy the CSS. | [github.com/megh-bari/pattern-craft](https://github.com/megh-bari/pattern-craft) |
| **Fancy** (2.8k stars) | Animated component collection -- text reveals, transitions, scroll effects. Visual previews. | [fancy.dev](https://fancy.dev) |
| **Motion Primitives** (5.5k stars) | Subtle, design-forward animated UI kit. Higher taste than Magic UI. | [motion-primitives.com](https://motion-primitives.com) |

### Full Admin & Dashboard Templates

Complete working apps you can clone and run. Browse the live demo, then fork.

| Template | Stars | What You Get | URL |
|----------|-------|-------------|-----|
| **shadcn-admin** | 11.8k | Full admin dashboard -- sidebar nav, charts, data tables, auth pages, dark mode. Live demo. | [github.com/satnaing/shadcn-admin](https://github.com/satnaing/shadcn-admin) |
| **next-shadcn-dashboard-starter** | 6.3k | Next.js 16 + shadcn admin with tables, forms, charts, Kanban board. | [github.com/Kiranism/next-shadcn-dashboard-starter](https://github.com/Kiranism/next-shadcn-dashboard-starter) |
| **TailAdmin** | 2k | Free Tailwind dashboard with 200+ UI components. | [github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template](https://github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template) |
| **Vue Vben Admin** | 32k | Full Vue3 admin panel with shadcn + Vite. Production-ready. | [github.com/vbenjs/vue-vben-admin](https://github.com/vbenjs/vue-vben-admin) |
| **shadcn-admin-kit** | -- | React-admin framework for admin SPAs with shadcn components. | [github.com/marmelab/shadcn-admin-kit](https://github.com/marmelab/shadcn-admin-kit) |

### SaaS Boilerplates (Full Apps You Can See Running)

Start a SaaS project with auth, payments, email, and dashboard already built.

| Boilerplate | Stars | Stack | URL |
|------------|-------|-------|-----|
| **Next.js SaaS Starter** | 15.7k | Next.js + Postgres + Stripe + shadcn. Official Vercel starter. | [github.com/nextjs/saas-starter](https://github.com/nextjs/saas-starter) |
| **Open SaaS** | 14.2k | 100% free. Auth, payments, email, analytics, blog, admin. React + Node + Prisma. | [github.com/wasp-lang/open-saas](https://github.com/wasp-lang/open-saas) |
| **SaaS Boilerplate** | 7k | Next.js + Tailwind + shadcn + TypeScript. Full-stack with i18n, email, monitoring. | [github.com/ixartz/SaaS-Boilerplate](https://github.com/ixartz/SaaS-Boilerplate) |
| **Invoify** | 6.2k | Invoice generator -- good example of a polished Next.js + shadcn production app. | [github.com/al1abb/invoify](https://github.com/al1abb/invoify) |

### Visual Theme Editors

Tweak designs live in the browser -- adjust colors, spacing, radii and see changes instantly.

| Tool | Stars | What It Does | URL |
|------|-------|-------------|-----|
| **tweakcn** | 9.7k | Visual no-code theme editor for shadcn/ui. Drag sliders, see components update live. | [tweakcn.com](https://tweakcn.com) |
| **Puck** | 6k+ | Drag-and-drop visual page editor for React. MIT licensed. | [github.com/measuredco/puck](https://github.com/measuredco/puck) |

### Design Inspiration (Look, Then Build)

Not code -- these are galleries of real shipped websites to study before you start.

| Site | What You Browse | URL |
|------|----------------|-----|
| **Godly** | Curated high-quality web design. Filterable by style, color, industry. | [godly.website](https://godly.website) |
| **Land-book** | Landing page gallery. Filter by color, style, industry. | [land-book.com](https://land-book.com) |
| **Mobbin** | Real app and web UI. Filter by industry, screen type, and UI pattern. Best for studying how real products handle specific flows. | [mobbin.com](https://mobbin.com) |
| **SiteInspire** | Design-focused gallery of real websites. | [siteinspire.com](https://siteinspire.com) |
| **One Page Love** | Curated one-page websites. Great for portfolios and landing pages. | [onepagelove.com](https://onepagelove.com) |
| **Httpster** | Clean, minimal, well-designed sites. | [httpster.net](https://httpster.net) |
| **Codrops** | Experimental CSS/JS techniques with tutorials. | [tympanus.net/codrops](https://tympanus.net/codrops) |
| **maxibestof** | Filterable by fonts used -- find sites using the typeface you chose. | [maxibestof.one](https://maxibestof.one) |
| **Dribbble** | Designer portfolios and UI concepts. Good for color and layout ideas, not for copying wholesale. | [dribbble.com](https://dribbble.com) |

### The Workflow

1. **Browse inspiration** (Godly, Land-book, Mobbin) -- find the vibe
2. **Pick components** (shadcn Blocks, Magic UI, Aceternity, 21st.dev) -- grab the pieces
3. **Customize the theme** (tweakcn) -- make it yours
4. **Reference the toolkit** (this README) -- pick the right libraries
5. **Follow the rules** (RULES.md, AI-INSTRUCTIONS.md) -- ship it clean

---

## Component Libraries

| Tool | What It Does | URL |
|------|-------------|-----|
| **shadcn/ui** (112k stars) | Copy-paste accessible components on Radix + Tailwind. You own the code. | [ui.shadcn.com](https://ui.shadcn.com) |
| **HeroUI** (29k stars) | Polished React components with Tailwind + Framer Motion built in. | [heroui.com](https://heroui.com) |
| **Radix UI Primitives** (19k stars) | Unstyled, fully accessible headless primitives. Foundation of shadcn/ui. | [radix-ui.com](https://radix-ui.com) |
| **Mantine** (31k stars) | 100+ components, hooks, forms, date pickers, rich text -- batteries included. | [mantine.dev](https://mantine.dev) |
| **Chakra UI** (40k stars) | Themeable component system. v3 rebuilt on Panda CSS. | [chakra-ui.com](https://chakra-ui.com) |
| **MUI** (98k stars) | Google Material Design for React. Enterprise-grade, massive ecosystem. | [mui.com](https://mui.com) |
| **Ant Design** (98k stars) | Enterprise UI design language. Best for data-heavy admin panels. | [ant.design](https://ant.design) |
| **Tremor** (3.4k stars) | Copy-paste components purpose-built for dashboards and analytics. | [tremor.so](https://tremor.so) |
| **Floating UI** (33k stars) | Low-level positioning engine for tooltips, dropdowns, popovers. | [floating-ui.com](https://floating-ui.com) |

---

## Animated / Visual Effect Libraries

| Tool | What It Does | URL |
|------|-------------|-----|
| **Magic UI** (21k stars) | Copy-paste animated components -- particles, shimmer, glow, cursor trails. Tailwind + Framer Motion. | [magicui.design](https://magicui.design) |
| **Aceternity UI** | Spotlight effects, 3D cards, animated gradients. High wow-factor landing page components. | [ui.aceternity.com](https://ui.aceternity.com) |
| **Motion Primitives** (5.5k stars) | Design-forward animated UI kit. Higher subtlety than Magic UI. | [motion-primitives.com](https://motion-primitives.com) |
| **pqoqubbw/icons** (7.5k stars) | Beautifully animated SVG icons. Drop-in replacements for static icons. | [icons.pqoqubbw.dev](https://icons.pqoqubbw.dev) |

---

## Animation Engines

| Tool | What It Does | URL |
|------|-------------|-----|
| **Motion / Framer Motion** (32k stars) | The React animation standard. Declarative, performant, gesture + scroll support. | [motion.dev](https://motion.dev) |
| **GSAP** (25k stars) | Professional timeline-based animations. ScrollTrigger plugin is unmatched. | [gsap.com](https://gsap.com) |
| **Anime.js** (67k stars) | Lightweight engine for keyframe animations and SVG morphing. | [animejs.com](https://animejs.com) |
| **React Spring** (29k stars) | Spring physics-based animations that feel natural. | [react-spring.dev](https://react-spring.dev) |
| **AutoAnimate** (14k stars) | One line of code adds smooth list transitions. Zero config. | [auto-animate.formkit.com](https://auto-animate.formkit.com) |

---

## CSS Frameworks

| Tool | What It Does | URL |
|------|-------------|-----|
| **Tailwind CSS** (95k stars) | Utility-first CSS. v4 uses pure CSS `@theme` blocks, no config file. | [tailwindcss.com](https://tailwindcss.com) |
| **UnoCSS** (19k stars) | Instant atomic CSS engine. Faster build times, Tailwind-compatible presets. | [unocss.dev](https://unocss.dev) |

---

## Icon Libraries

| Tool | What It Does | URL |
|------|-------------|-----|
| **Lucide** (22k stars) | 1,500+ clean icons. Default in shadcn/ui. Tree-shakable, typed. | [lucide.dev](https://lucide.dev) |
| **Tabler Icons** (21k stars) | 6,000+ free MIT icons. Largest high-quality free set. | [tabler.io/icons](https://tabler.io/icons) |
| **Heroicons** | Tailwind team's official icon set. Outline and solid variants. | [heroicons.com](https://heroicons.com) |
| **Phosphor Icons** (6.6k stars) | 6 weight variants per icon (thin, light, regular, bold, fill, duotone). | [phosphoricons.com](https://phosphoricons.com) |
| **Simple Icons** (25k stars) | SVG icons for 3,000+ brand logos. Consistent styling. | [simpleicons.org](https://simpleicons.org) |

---

## Templates and Starter Kits

| Tool | What It Does | URL |
|------|-------------|-----|
| **create-t3-app** (29k stars) | Full-stack Next.js scaffold with tRPC, Prisma, Auth.js, Tailwind. | [create.t3.gg](https://create.t3.gg) |
| **Taxonomy** (19k stars) | shadcn's reference app -- App Router, auth, MDX blog, Stripe billing. | [github.com/shadcn-ui/taxonomy](https://github.com/shadcn-ui/taxonomy) |
| **Bulletproof React** (35k stars) | Architecture guide for scalable React apps. Folder structure and patterns. | [github.com/alan2207/bulletproof-react](https://github.com/alan2207/bulletproof-react) |
| **next-saas-stripe-starter** (3k stars) | SaaS boilerplate with subscriptions, user roles, email, admin panel. | [github.com/mickasmt/next-saas-stripe-starter](https://github.com/mickasmt/next-saas-stripe-starter) |

---

## Forms

| Tool | What It Does | URL |
|------|-------------|-----|
| **React Hook Form** (45k stars) | Performant forms with zero re-renders. Pairs with Zod via resolvers. | [react-hook-form.com](https://react-hook-form.com) |
| **Zod** (43k stars) | TypeScript-first schema validation. `z.infer<>` gives you types for free. | [zod.dev](https://zod.dev) |
| **TanStack Form** (6.5k stars) | Headless, type-safe form state. Framework-agnostic. | [tanstack.com/form](https://tanstack.com/form) |

---

## Data Fetching and State

| Tool | What It Does | URL |
|------|-------------|-----|
| **TanStack Query** (49k stars) | Server state standard. Caching, background refetch, optimistic updates. | [tanstack.com/query](https://tanstack.com/query) |
| **SWR** (32k stars) | Stale-while-revalidate data fetching hooks from Vercel. | [swr.vercel.app](https://swr.vercel.app) |
| **Zustand** (58k stars) | Minimal global state. Zero boilerplate, hooks-based. Replaced Redux for most apps. | [zustand.docs.pmnd.rs](https://zustand.docs.pmnd.rs) |
| **Jotai** (21k stars) | Atomic state for granular subscriptions and derived state. | [jotai.org](https://jotai.org) |
| **tRPC** (40k stars) | End-to-end type-safe APIs. Call backend like local functions. | [trpc.io](https://trpc.io) |
| **XState** (30k stars) | State machines for complex multi-step flows (wizards, auth, async). | [stately.ai/docs](https://stately.ai/docs) |

---

## Auth

| Tool | What It Does | URL |
|------|-------------|-----|
| **Auth.js / NextAuth v5** (28k stars) | Authentication for Next.js. 70+ OAuth providers, credentials, magic links. Free, self-hosted. | [authjs.dev](https://authjs.dev) |
| **Clerk** | Complete user management platform. Pre-built UI, org/team support, MFA. | [clerk.com](https://clerk.com) |
| **Lucia** (11k stars) | Minimal auth library. Thin abstraction over sessions and cookies. Full control. | [lucia-auth.com](https://lucia-auth.com) |
| **Stack Auth** (6.7k stars) | Open-source Auth0/Clerk alternative. Self-hostable, full-featured. | [github.com/stack-auth/stack-auth](https://github.com/stack-auth/stack-auth) |

---

## Database and ORM

| Tool | What It Does | URL |
|------|-------------|-----|
| **Supabase** (101k stars) | Open-source Firebase alternative. Postgres + Auth + Storage + Realtime. | [supabase.com](https://supabase.com) |
| **Prisma** (46k stars) | Declarative schema, auto-generated type-safe client, GUI browser. | [prisma.io](https://prisma.io) |
| **Drizzle ORM** (34k stars) | SQL-first TypeScript ORM. Near-zero overhead. Works on Edge. | [orm.drizzle.team](https://orm.drizzle.team) |

---

## CMS and Content

| Tool | What It Does | URL |
|------|-------------|-----|
| **Payload CMS** (42k stars) | Open-source fullstack CMS that runs inside Next.js. Auto-generates APIs. | [payloadcms.com](https://payloadcms.com) |
| **Sanity** (6.1k stars) | Structured content platform with real-time collaborative editing. GROQ queries. | [sanity.io](https://sanity.io) |
| **Strapi** (72k stars) | Leading open-source headless CMS. Self-hostable, plugin ecosystem. | [strapi.io](https://strapi.io) |
| **Directus** (35k stars) | Wrap any SQL database with a CMS and instant API. | [directus.io](https://directus.io) |

---

## Email

| Tool | What It Does | URL |
|------|-------------|-----|
| **React Email** (19k stars) | Build HTML emails using React components. No more table-soup HTML. | [react.email](https://react.email) |
| **Resend** | Email API with best-in-class deliverability. 3,000 emails/month free. | [resend.com](https://resend.com) |

---

## Payments

| Tool | What It Does | URL |
|------|-------------|-----|
| **Stripe** | The payment infrastructure standard. Subscriptions, invoicing, global tax. | [stripe.com](https://stripe.com) |
| **Lemon Squeezy** | Merchant of record -- handles sales tax and VAT globally so you don't. | [lemonsqueezy.com](https://lemonsqueezy.com) |

---

## Testing

| Tool | What It Does | URL |
|------|-------------|-----|
| **Vitest** (16k stars) | Vite-powered testing. Jest-compatible API, 10-20x faster. | [vitest.dev](https://vitest.dev) |
| **Playwright** (87k stars) | Cross-browser E2E testing. Built-in codegen and trace viewer. | [playwright.dev](https://playwright.dev) |
| **Storybook** (90k stars) | UI component workshop. Visual docs, interaction tests, a11y checks. | [storybook.js.org](https://storybook.js.org) |

---

## Charts and Data Viz

| Tool | What It Does | URL |
|------|-------------|-----|
| **Recharts** (27k stars) | Declarative charts built with React + D3. Default in shadcn/ui. | [recharts.org](https://recharts.org) |
| **Chart.js** (67k stars) | Simple Canvas-based charts. 8 types, works anywhere. | [chartjs.org](https://chartjs.org) |
| **Nivo** (14k stars) | Rich dataviz with SVG, Canvas, and HTML renders. Best docs in category. | [nivo.rocks](https://nivo.rocks) |
| **React Flow** (36k stars) | Node-based UIs -- workflow editors, AI agent visualizers, mind maps. | [reactflow.dev](https://reactflow.dev) |

---

## Dev Tooling

| Tool | What It Does | URL |
|------|-------------|-----|
| **Biome** (24k stars) | Rust-based formatter + linter. 10-100x faster than Prettier + ESLint. | [biomejs.dev](https://biomejs.dev) |
| **Turborepo** (30k stars) | Monorepo build system with remote caching. Only changed packages rebuild. | [turbo.build](https://turbo.build) |
| **Vercel AI SDK** (24k stars) | TypeScript toolkit for LLM-powered apps. Streaming, tool calling, multi-provider. | [sdk.vercel.ai](https://sdk.vercel.ai) |
| **Trigger.dev** (15k stars) | Type-safe background jobs and AI workflows. Replaces cron + queue infra. | [trigger.dev](https://trigger.dev) |
| **cmdk** (13k stars) | Unstyled command palette component. Powers cmd+K in most React apps. | [cmdk.paco.me](https://cmdk.paco.me) |
| **Sonner** (12k stars) | Opinionated toast notifications. One import, instant polish. Default in shadcn/ui. | [sonner.emilkowal.ski](https://sonner.emilkowal.ski) |
| **Vaul** (8.3k stars) | Mobile-first bottom sheet drawer. Smooth drag-to-dismiss. | [vaul.emilkowal.ski](https://vaul.emilkowal.ski) |

---

## Deployment

| Tool | What It Does | URL |
|------|-------------|-----|
| **Vercel** | Zero-config deploys for Next.js. Edge Network, preview URLs per PR. | [vercel.com](https://vercel.com) |
| **Cloudflare Workers/Pages** | Edge-first serverless compute. 0ms cold starts. Competitive free tier. | [workers.cloudflare.com](https://workers.cloudflare.com) |
| **Coolify** (54k stars) | Self-hosted Vercel/Heroku/Netlify alternative. Deploy anything with Docker. | [coolify.io](https://coolify.io) |
| **Dokploy** (33k stars) | Open-source PaaS alternative to Vercel/Heroku. Simpler than Coolify. | [dokploy.com](https://dokploy.com) |
| **Dokku** (31k stars) | Docker-powered mini-Heroku. Single-server PaaS. | [dokku.com](https://dokku.com) |
| **Bun** (89k stars) | JS runtime, bundler, test runner, package manager. 3-5x faster than Node. | [bun.sh](https://bun.sh) |

---

## AI and LLM Tools

| Tool | What It Does | URL |
|------|-------------|-----|
| **Vercel AI SDK** (24k stars) | TypeScript toolkit for LLM-powered apps. Streaming, tool calling, multi-provider. | [sdk.vercel.ai](https://sdk.vercel.ai) |
| **Dify** (139k stars) | Visual agentic workflow platform. Build LLM apps with drag-and-drop. | [dify.ai](https://dify.ai) |
| **LangChain** (135k stars) | The agent engineering framework. Python and JS. | [langchain.com](https://www.langchain.com) |
| **Open WebUI** (134k stars) | Self-hosted ChatGPT-style UI for local LLMs (Ollama, OpenAI API). | [openwebui.com](https://openwebui.com) |
| **Ollama** (120k+ stars) | Run LLMs locally. One command to download and run any model. | [ollama.com](https://ollama.com) |
| **ComfyUI** (110k stars) | Node-based Stable Diffusion UI. The image generation powerhouse. | [github.com/Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI) |
| **Firecrawl** (112k stars) | API to search, scrape, and interact with the web for AI pipelines. | [firecrawl.dev](https://www.firecrawl.dev) |
| **Browser Use** (90k stars) | Let AI agents browse the web autonomously. | [github.com/browser-use/browser-use](https://github.com/browser-use/browser-use) |
| **OpenHands** (72k stars) | AI-driven development agent. Open-source Devin alternative. | [github.com/OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) |
| **LlamaFactory** (70k stars) | Fine-tune 100+ LLMs with a unified interface. | [github.com/hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) |
| **Crawl4AI** (64k stars) | LLM-friendly web scraper. Converts pages to clean markdown. | [github.com/unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) |
| **MarkItDown** (117k stars) | Convert any file or office document to Markdown. By Microsoft. | [github.com/microsoft/markitdown](https://github.com/microsoft/markitdown) |

---

## DevOps and Infrastructure

| Tool | What It Does | URL |
|------|-------------|-----|
| **act** (70k stars) | Run GitHub Actions locally. Test workflows without pushing. | [github.com/nektos/act](https://github.com/nektos/act) |
| **Netdata** (78k stars) | Real-time infrastructure monitoring with AI-powered insights. | [netdata.cloud](https://www.netdata.cloud) |
| **Sentry** (43k stars) | Error tracking and performance monitoring for any stack. | [sentry.io](https://sentry.io) |
| **Watchtower** (24k stars) | Auto-update Docker containers when new images are pushed. | [github.com/containrrr/watchtower](https://github.com/containrrr/watchtower) |
| **Argo CD** (22k stars) | GitOps continuous deployment for Kubernetes. | [argoproj.github.io/cd](https://argoproj.github.io/cd/) |
| **SOPS** (21k stars) | Secrets management for config files. Encrypt values in YAML/JSON. | [github.com/getsops/sops](https://github.com/getsops/sops) |
| **Kestra** (26k stars) | Event-driven orchestration and scheduling. Visual workflow builder. | [kestra.io](https://kestra.io) |
| **n8n** (185k stars) | Fair-code workflow automation with native AI. Visual Zapier alternative. | [n8n.io](https://n8n.io) |

---

## Self-Hosted Essentials

Tools the Reddit r/selfhosted community (1M+ members) swears by.

| Tool | What It Does | URL |
|------|-------------|-----|
| **Immich** (98k stars) | Self-hosted Google Photos replacement. Face recognition, mobile app, sharing. | [immich.app](https://immich.app) |
| **Uptime Kuma** (85k stars) | Fancy self-hosted monitoring. Beautiful dashboard, notifications. | [github.com/louislam/uptime-kuma](https://github.com/louislam/uptime-kuma) |
| **Stirling-PDF** (77k stars) | All-in-one PDF toolkit. Merge, split, convert, OCR, watermark. Self-hosted. | [github.com/Stirling-Tools/Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) |
| **Paperless-NGX** (25k+ stars) | Scan, index, and archive all your physical documents. OCR + tagging. | [docs.paperless-ngx.com](https://docs.paperless-ngx.com) |
| **Jellyfin** (40k+ stars) | Media server. Plex alternative that is actually free. | [jellyfin.org](https://jellyfin.org) |
| **Syncthing** (70k+ stars) | P2P file sync. No cloud, no accounts, no limits. | [syncthing.net](https://syncthing.net) |
| **Home Assistant** (80k+ stars) | Smart home automation hub. Local control, privacy first. | [home-assistant.io](https://www.home-assistant.io) |
| **Dockge** (16k+ stars) | Simple Docker Compose management UI. By the Uptime Kuma developer. | [github.com/louislam/dockge](https://github.com/louislam/dockge) |
| **Reactive Resume** (36k stars) | Privacy-first resume builder. No tracking, fully self-hostable. | [rxresu.me](https://rxresu.me) |
| **TriliumNext** (35k stars) | Personal knowledge base. Notion alternative, self-hosted, hierarchical notes. | [github.com/TriliumNext/Trilium](https://github.com/TriliumNext/Trilium) |
| **LocalSend** (60k+ stars) | AirDrop for all platforms. Send files to nearby devices over local network. | [localsend.org](https://localsend.org) |
| **Bitwarden / Vaultwarden** | Password manager. Vaultwarden is the lightweight self-hosted server. | [bitwarden.com](https://bitwarden.com) |

---

## Communication (Self-Hosted)

| Tool | What It Does | URL |
|------|-------------|-----|
| **Matrix / Element** | Federated encrypted chat. The #1 community pick for Discord replacement. | [element.io](https://element.io) |
| **Mattermost** (32k stars) | Open-source Slack alternative. Team chat with channels, threads, integrations. | [mattermost.com](https://mattermost.com) |
| **Zulip** (22k stars) | Threaded team chat. Best threading model of any chat tool. | [zulip.com](https://zulip.com) |
| **Mumble** | Open-source voice chat. TeamSpeak alternative, own your voice data. | [mumble.info](https://www.mumble.info) |
| **Rocket.Chat** (45k stars) | Feature-rich team chat. Self-hostable. Free tier caps at 50 users. | [rocket.chat](https://rocket.chat) |

---

## Backend Platforms

| Tool | What It Does | URL |
|------|-------------|-----|
| **Appwrite** (55k stars) | Backend-as-a-service. Auth, database, storage, functions, messaging. Firebase alternative. | [appwrite.io](https://appwrite.io) |
| **OpenBB** (66k stars) | Financial data platform for analysts, quants, and AI agents. | [openbb.co](https://openbb.co) |
| **Daytona** (72k stars) | Secure infrastructure for running AI-generated code. Dev environments. | [daytona.io](https://www.daytona.io) |

---

## Curated Resource Lists

Awesome lists and reference repos to bookmark. Open any of these when you need inspiration, tools, or patterns for a specific area.

### Design and UI

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-design-md** | -- | Design system markdown templates for AI-assisted development. | [github.com/VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md) |
| **design-resources-for-developers** | 65k | Stock photos, CSS frameworks, UI libraries, tools -- everything design. | [github.com/bradtraversy/design-resources-for-developers](https://github.com/bradtraversy/design-resources-for-developers) |
| **Awesome-Design-Tools** | 40k | Best design tools and plugins for Figma, prototyping, color, typography. | [github.com/goabstract/Awesome-Design-Tools](https://github.com/goabstract/Awesome-Design-Tools) |
| **awesome-design-systems** | 24k | Design systems from companies across the industry. | [github.com/alexpate/awesome-design-systems](https://github.com/alexpate/awesome-design-systems) |
| **spark-joy** | 10k | 2000+ ways to add design flair, delight, and whimsy to your product. | [github.com/swyxio/spark-joy](https://github.com/swyxio/spark-joy) |

### React and Next.js

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-react** | 73k | The canonical collection of React ecosystem resources. | [github.com/enaqx/awesome-react](https://github.com/enaqx/awesome-react) |
| **awesome-react-components** | 47k | Curated list of React component libraries. | [github.com/brillout/awesome-react-components](https://github.com/brillout/awesome-react-components) |
| **awesome-nextjs** | 11k | Books, videos, and articles about Next.js. | [github.com/unicodeveloper/awesome-nextjs](https://github.com/unicodeveloper/awesome-nextjs) |
| **awesome-react-hooks** | 10k | React Hooks resources, libraries, and examples. | [github.com/rehooks/awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks) |
| **awesome-shadcn-ui** | 19k | Themes, blocks, components, and extensions for shadcn/ui. | [github.com/birobirobiro/awesome-shadcn-ui](https://github.com/birobirobiro/awesome-shadcn-ui) |

### Tailwind CSS

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-tailwindcss** | 15k | Plugins, components, templates, and tools for Tailwind. | [github.com/aniftyco/awesome-tailwindcss](https://github.com/aniftyco/awesome-tailwindcss) |

### Landing Pages and Templates

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-landing-page** | 3.8k | Beautiful, practical landing page templates. | [github.com/nordicgiant2/awesome-landing-page](https://github.com/nordicgiant2/awesome-landing-page) |
| **awesome-landing-pages** | 950 | Free landing pages for SaaS founders, freelancers, agencies. | [github.com/PaulleDemon/awesome-landing-pages](https://github.com/PaulleDemon/awesome-landing-pages) |

### Portfolio Inspiration

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **developer-portfolios** | 22k | Developer portfolios submitted by the community. | [github.com/emmabostian/developer-portfolios](https://github.com/emmabostian/developer-portfolios) |
| **portfolio-ideas** | 5.9k | Portfolio website ideas for developers and designers. | [github.com/Evavic44/portfolio-ideas](https://github.com/Evavic44/portfolio-ideas) |

### Animation

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-web-animation** | 1.5k | Web animation libraries, books, and apps (CSS, JS, canvas, SVG). | [github.com/sergey-pimenov/awesome-web-animation](https://github.com/sergey-pimenov/awesome-web-animation) |
| **animate.css** | 83k | Cross-browser CSS animation library. | [github.com/animate-css/animate.css](https://github.com/animate-css/animate.css) |

### Accessibility

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-a11y** | 2k | Tools, articles, guidelines, testing, ARIA patterns. | [github.com/brunopulis/awesome-a11y](https://github.com/brunopulis/awesome-a11y) |
| **a11yproject.com** | 3.9k | Community-driven accessibility patterns, checklists, and resources. | [github.com/a11yproject/a11yproject.com](https://github.com/a11yproject/a11yproject.com) |

### SEO

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-seo (bmpi-dev)** | 2.7k | SEO research and web traffic monetization strategies. | [github.com/bmpi-dev/awesome-seo](https://github.com/bmpi-dev/awesome-seo) |
| **awesome-seo-tools** | 950 | Technical auditing, keyword research, rank tracking tools. | [github.com/serpapi/awesome-seo-tools](https://github.com/serpapi/awesome-seo-tools) |

### Color and Typography

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **open-color** | 5.5k | Open-source color scheme optimized for UI design. | [github.com/yeun/open-color](https://github.com/yeun/open-color) |
| **css-protips** | 30k | CSS tips for color contrast, custom properties, layout. | [github.com/AllThingsSmitty/css-protips](https://github.com/AllThingsSmitty/css-protips) |

### AI and LLM Tools

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-llm-apps** | 107k | 100+ AI Agent and RAG apps you can clone and ship. | [github.com/Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) |
| **awesome-mcp-servers** | 85k | MCP servers for Claude and AI assistants. | [github.com/punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) |
| **awesome-ai-coding-tools** | 1.7k | AI-powered coding tools: copilots, code review, test gen. | [github.com/ai-for-developers/awesome-ai-coding-tools](https://github.com/ai-for-developers/awesome-ai-coding-tools) |

### Free APIs and Resources

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **public-apis** | 426k | The largest list of free APIs for building apps. | [github.com/public-apis/public-apis](https://github.com/public-apis/public-apis) |
| **frontend-dev-bookmarks** | 47k | Manually curated resources for frontend developers. | [github.com/dypsilon/frontend-dev-bookmarks](https://github.com/dypsilon/frontend-dev-bookmarks) |

### Open Source Alternatives

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome-oss-alternatives** | 19k | Open-source alternatives to popular SaaS products. | [github.com/RunaCapital/awesome-oss-alternatives](https://github.com/RunaCapital/awesome-oss-alternatives) |
| **awesome-selfhosted** | 288k | Free software and web apps you can self-host. | [github.com/awesome-selfhosted/awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) |

### Checklists and Standards

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **Front-End-Checklist** | 73k | The perfect front-end checklist for modern websites. | [github.com/thedaviddias/Front-End-Checklist](https://github.com/thedaviddias/Front-End-Checklist) |
| **Front-End-Performance-Checklist** | 17k | Front-end performance checklist for fast sites. | [github.com/thedaviddias/Front-End-Performance-Checklist](https://github.com/thedaviddias/Front-End-Performance-Checklist) |
| **HEAD** | 30k | Guide to everything in the HTML `<head>`: meta, OG, Twitter, CSP, PWA. | [github.com/joshbuchea/HEAD](https://github.com/joshbuchea/HEAD) |
| **awesome-guidelines** | 11k | High-quality coding style conventions and standards. | [github.com/Kristories/awesome-guidelines](https://github.com/Kristories/awesome-guidelines) |

### Meta

| Resource | Stars | What It Is | URL |
|----------|-------|-----------|-----|
| **awesome** | 458k | The master list of all awesome lists on GitHub. Start here. | [github.com/sindresorhus/awesome](https://github.com/sindresorhus/awesome) |
| **the-book-of-secret-knowledge** | 217k | Lists, manuals, cheatsheets, blogs, hacks, CLI/web tools, and more. | [github.com/trimstray/the-book-of-secret-knowledge](https://github.com/trimstray/the-book-of-secret-knowledge) |
