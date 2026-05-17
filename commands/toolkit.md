---
description: "Active project scaffolder and design-system tool. Probes the current directory, runs an adaptive interview, previews what it will do, then scaffolds the project end-to-end. Use when starting any new web project (marketing, dashboard, SaaS, admin, e-commerce, frontend for existing API), adding a design system to an existing project, picking a font / palette / component library, or fixing a UI that looks generic. Fires on intents like scaffold, start, build a dashboard, design system, pick a font, pick a library, fix the look, make the UI look better."
---

Invoke the production-toolkit:toolkit skill and follow it exactly.

The skill runs six phases in order:
0. **Target** -- ensure templates are present locally (clone from GitHub if missing); ask which directory to scaffold into so you can run /toolkit from anywhere
1. **Probe** -- silent context detection in the target directory (what's in cwd, siblings, package.json, DESIGN.md, etc.)
2. **Present context** -- one-paragraph summary of the situation, user confirms scope
3. **Interview** -- adaptive multiple-choice questions; skips dimensions the probe already answered
4. **Preview** -- summary of every file + command that will run, user approves
5. **Execute** -- scaffold framework, install libs, write tokens, copy templates, build sample pages, commit

Do not abbreviate the flow. Each phase is required; skipping produces generic output, which is the
problem this skill exists to solve.

See the skill file for the full question bank, the context-classification rules, and the adaptive
question matrix (which questions to ask vs skip for `empty-new`, `empty-with-sibling-backend`,
`existing-project`, and `existing-with-design` situations).

Source files live at `/volume1/playground/dev-tool-docs/production-toolkit/` (Kevin's working copy).
The plugin install at `/root/.claude/plugins/marketplaces/production-toolkit/` is a read-only mirror.
