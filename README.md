# Design Skills

A portable design skill package for AI coding agents (Claude Code, Cursor, Codex, and others). Gives your agent design taste, design system discipline, and the ability to critically evaluate what it builds.

## What's in here

### The Orchestrator: `/design-at-work`

The core skill. Works out of the box in any codebase — it automatically discovers your design system, components, and patterns. It makes your agent:

- **Use your design system first** — searches for existing components before writing custom ones
- **Match existing patterns** — finds similar pages/features in your codebase and follows their layout approach
- **Think before building** — critically evaluates proposals, suggests alternatives when they exist
- **Review copy** — checks user-facing text for quality and consistency
- **Route to specialists** — dispatches to the right design skill based on what's needed

### Third-Party Design Skills

These are standalone design skills from the community that the orchestrator can route to. Install them separately:

```bash
# Impeccable — anti-AI-slop design system with 17 specialized skills
# Covers: typography, color, spatial design, motion, interaction, responsive, UX writing
# Skills: /impeccable, /shape, /critique, /layout, /distill, /clarify, /typeset, /polish,
#         /audit, /bolder, /quieter, /colorize, /delight, /animate, /adapt, /optimize, /overdrive
npx skills add pbakaus/impeccable --yes

# Emil Kowalski — animation philosophy, component design, invisible details
# Skills: /emil-design-eng
npx skills add emilkowalski/skill --yes
```

**Source repos:**
- [Impeccable](https://github.com/pbakaus/impeccable) by Paul Bakaus
- [Emil Kowalski's skill](https://github.com/emilkowalski/skill) by Emil Kowalski

## Install

### Option 1: Install via skills CLI

```bash
npx skills add daria-intercom/design-skills --yes
```

This installs the orchestrator skill. Install the third-party skills above separately for the full package.

> **Note:** If this repo is private, you'll need access to install it. Ask the owner to add you as a collaborator, or fork it to your own account.

### Option 2: Manual install

Copy `skills/design-at-work/SKILL.md` into your agent's skill directory:

- **Claude Code**: `~/.claude/commands/design-at-work.md` or `.claude/skills/design-at-work/SKILL.md` in your repo
- **Other agents**: Add to your agent's rules or skills directory

### Option 3: Fork and customize

Fork this repo, customize the orchestrator for your design system, then install from your fork. See [Advanced Customization](#advanced-customization) below.

## How it works

The skill works out of the box. When invoked, it:

1. **Discovers your design system** by searching for component libraries, UI packages, and token files in your codebase
2. **Searches for existing patterns** — before building anything, it looks for similar pages and features
3. **Adapts to your intent** — questions get full evaluation and discussion; direct instructions get fast implementation with guardrails; "just do it" skips the discussion entirely
4. **Routes to specialized skills** when installed (layout, typography, animation, etc.) — if a skill isn't installed, it applies the underlying principle itself
5. **Self-checks** its work against a verification checklist before finishing

## Skill Reference

### What each skill does

| Skill | From | Purpose |
|-------|------|---------|
| `/design-at-work` | This repo | Orchestrator — enforces design system, finds patterns, evaluates decisions |
| `/impeccable` | Impeccable | Full design build with anti-AI-slop rules |
| `/shape` | Impeccable | Discovery interview that produces a design brief |
| `/critique` | Impeccable | UX evaluation with Nielsen heuristic scoring |
| `/layout` | Impeccable | Fix spacing and visual hierarchy |
| `/distill` | Impeccable | Simplify cluttered UI |
| `/clarify` | Impeccable | Fix unclear copy and labels |
| `/typeset` | Impeccable | Fix typography hierarchy |
| `/polish` | Impeccable | Final quality checklist |
| `/audit` | Impeccable | Technical quality audit (a11y, perf, theming) |
| `/bolder` | Impeccable | Amplify bland designs |
| `/quieter` | Impeccable | Tone down aggressive designs |
| `/colorize` | Impeccable | Add strategic color |
| `/delight` | Impeccable | Add moments of joy |
| `/animate` | Impeccable | Add purposeful animation |
| `/adapt` | Impeccable | Responsive design |
| `/optimize` | Impeccable | Performance fixes |
| `/overdrive` | Impeccable | Technically ambitious effects |
| `/emil-design-eng` | Emil Kowalski | Animation philosophy and component polish |

### Recommended workflows

**Building a new feature:**
`/shape` (plan) → `/design-at-work` (implement) → `/polish` (final pass)

**Quick UI tweak:**
`/design-at-work` (just tell it what to change)

**Design review:**
`/critique` (UX evaluation) → `/audit` (technical quality)

**Something looks off:**
`/layout` (spacing) · `/typeset` (fonts) · `/clarify` (copy) · `/distill` (simplify)

---

## Advanced Customization

The orchestrator works without customization, but you can make it significantly more effective by tailoring it to your specific codebase. The more specific you are, the less the agent guesses.

### What to customize

**1. Name your design system explicitly**

Instead of the agent discovering your design system each time, tell it exactly where to look and how to import. This eliminates ambiguity and speeds up every interaction.

Example: Instead of "search for a component library," say "Glob `packages/your-ds/src/components/` and import as `import { Button } from '@yourcompany/design-system'`."

**2. Name your actual components in the pattern search**

The generic skill says "search for table components." Your customized version should name them: "Search for `DataTable`, `ListView`, look at the `/settings` routes for page layout patterns."

**3. Wire up your content/copy skill**

If your team has a content review skill or style guide, add an explicit instruction to invoke it for every piece of user-facing text. This turns content review from optional to automatic.

**4. Add your codebase-specific skills to the routing table**

If your team has skills for architecture planning, Figma extraction, component building, or testing, add them to the routing table so the orchestrator knows to delegate.

**5. Restrict aesthetic skills if needed**

Product codebases with established design systems usually shouldn't invoke `/bolder`, `/colorize`, or `/overdrive` freely. Add an explicit restriction if consistency matters more than novelty.

### The Intercom example

The `examples/intercom-designer/` directory shows a real-world customization. It documents exactly what was changed from the generic version and why — including naming the design system (Surge), wiring up a content review skill, adding codebase-specific skills to the routing table, and restricting aesthetic experimentation.

### Ask Claude to customize it for you

Once installed, you can ask your AI agent to do the customization:

```
I've installed the design-at-work skill. Our design system is called [name]
and lives at [path]. Can you read our design system and customize the skill
for our codebase?
```

The agent will read your design system, find your component directory, token files, and import conventions, then rewrite the skill with your specifics.

## License

MIT — see [LICENSE](LICENSE).
