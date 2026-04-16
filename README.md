# Design Skills

A portable design skill package for AI coding agents (Claude Code, Cursor, Codex, and others). Gives your agent design taste, design system discipline, and the ability to critically evaluate what it builds.

## What's in here

### The Orchestrator: `/design-at-work`

The core skill. It makes your agent:

- **Use your design system first** — searches for existing components before writing custom ones
- **Match existing patterns** — finds similar pages/features in your codebase and follows their layout approach
- **Think before building** — critically evaluates proposals, suggests alternatives when they exist
- **Review copy** — routes to content review for any user-facing text
- **Route to specialists** — dispatches to the right design skill based on what's needed

This skill is meant to be customized for your codebase. See [Customizing for Your Workplace](#customizing-for-your-workplace).

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

This installs the orchestrator skill. You'll still want to install the third-party skills above separately.

### Option 2: Manual install

Copy `skills/design-at-work/SKILL.md` into your agent's skill directory:

- **Claude Code**: `~/.claude/commands/design-at-work.md` (or `.claude/skills/design-at-work/SKILL.md` in your repo)
- **Cursor**: `.cursor/rules/design-at-work.md`
- **Codex**: `.codex/skills/design-at-work/SKILL.md`

### Option 3: Fork and customize

Fork this repo, then customize the orchestrator for your design system. See below.

## Customizing for Your Workplace

The orchestrator skill (`skills/design-at-work/SKILL.md`) is designed as a template. The version in this repo is a **generic starting point**. To make it work for your team:

### 1. Replace the design system references

Search for `[YOUR DESIGN SYSTEM]` and replace with your actual design system name, import paths, component directory, and token file.

### 2. Add your pattern search strategies

The "Patterns Over Invention" section has placeholder search strategies. Replace these with the actual directory structure, naming conventions, and common components in your codebase.

### 3. Add your content/copy skill

If your team has a content review skill or writing guidelines, add a reference in the "Content Quality" section. If not, the generic guidance works fine.

### 4. Adjust the skill routing table

The "Routing to Other Skills" table lists which specialized skills to invoke. Remove skills you haven't installed and add any custom skills your team has.

### 5. Save it in your repo

Put the customized skill in your project's `.claude/skills/` directory so everyone on the team gets it automatically.

### Example: Asking Claude to customize it for you

Once you've installed the skills, you can ask Claude Code to do the customization:

```
I've installed the design-at-work skill from daria-intercom/design-skills.
Our design system is called [name] and lives at [path].
Can you read our design system and customize the skill for our codebase?
```

## The Intercom Example

The `examples/intercom-designer/` directory contains the Intercom-specific version of this skill. It's a real-world example showing how to customize the orchestrator for a specific design system (Surge), specific codebase conventions (React in teammate-app), and specific companion skills (`/content-review`, `/react-architect`, `/design-align`).

Use it as a reference when building your own.

## Skill Reference

### What each skill does (quick reference)

| Skill | From | Purpose |
|-------|------|---------|
| `/design-at-work` | This repo | Orchestrator — enforces design system, finds patterns, evaluates decisions |
| `/impeccable` | Impeccable | Full design build with anti-AI-slop rules |
| `/shape` | Impeccable | Discovery interview → design brief |
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
