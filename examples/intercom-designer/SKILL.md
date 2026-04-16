---
name: intercom-designer
description: >-
  Design-aware orchestrator for Intercom's React codebase. Enforces Surge design system
  usage, finds existing patterns before creating new ones, critically evaluates design
  decisions, routes to specialized skills, and invokes /content-review for copy.
  For designers seeking implementation speed and engineers seeking autonomous design quality.
argument-hint: "[feature description, task, screenshot, or Figma URL]"
allowed-tools: Task, Read, Write, Edit, Glob, Grep, Bash, TodoWrite, AskUserQuestion, WebFetch, WebSearch
---

# Intercom Designer

This is a real-world example of the `/design-at-work` skill, customized for Intercom's codebase. It shows how to adapt the generic skill for a specific design system (Surge), specific codebase conventions, and specific companion skills.

Use this as a reference when customizing the skill for your own team.

---

## What was customized (and why)

### 1. Design system section — made concrete

The generic skill says "find the design system." This version names the exact design system (Surge), its component directory, its token file, its utility functions (`cn()`), and its import pattern. This eliminates ambiguity for the agent.

**Generic:**
> Search the codebase for a component library or design system package

**Customized:**
> Glob `packages/surge/src/components/` for matching components. Use design tokens from `packages/surge/tailwind.preset.js`. Import as `import { Button } from '@intercom/surge'`. Use `cn()` for classnames.

### 2. Pattern search — added real component names

The generic skill says "search for existing table pages." This version names the actual Surge components (`DataTable`, `Sheet`, `AlertDialog`, `PageHeader`, `EmptyState`) and references specific codebase patterns (nested route patterns from the `ai-categories` feature).

### 3. Content quality — wired to a specific skill

The generic skill says "if the project has a content review skill, follow it." This version explicitly invokes `/content-review` for every piece of user-facing copy, because Intercom has Russell Norris's content review skill built on Surge guidelines and the Intercom style guide.

### 4. Skill routing — added codebase-specific skills

The routing table was expanded with Intercom-specific skills:

| Skill | What it does |
|-------|-------------|
| `/content-review` | Reviews copy against Surge guidelines and Intercom style |
| `/react-architect` | Plans feature architecture for the React app |
| `/design-align` | Extracts pixel-perfect specs from Figma designs |
| `/surge` | Guidance for building Surge design system components |
| `/react` | React implementation patterns for the main app |

### 5. Aesthetic skills — restricted

Intercom's product UI prioritizes consistency. The skill explicitly blocks `/bolder`, `/colorize`, `/overdrive`, and `/delight` unless the user specifically asks for visual experimentation. The generic skill suggests this but the Intercom version enforces it.

### 6. Technology constraints — made explicit

The skill specifies TypeScript strict mode, the Ember-to-React migration context (prefer `teammate-app` over `apps/embercom`), and Figma MCP tool access for design extraction.

---

## The takeaway

The generic `/design-at-work` skill gives you 80% of the value. The remaining 20% comes from naming your exact components, tokens, import patterns, and companion skills. The more specific you are, the less the agent guesses — and the less you have to correct.
