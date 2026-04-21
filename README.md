# Astro Agent Skills

**Teach your AI coding assistant to build better Astro sites.**

A curated collection of [agent skills](https://github.com/vercel-labs/skills) that give AI assistants deep knowledge of Astro patterns, best practices, and workflows. Works with Codex, Cursor, Claude Code, and other agents that support the open skills ecosystem.

## Why Use These Skills?

AI assistants are powerful, but they don't always know the _right_ way to build with Astro. These skills provide structured guidance so your assistant can:

- **Follow official patterns** — Uses Astro's recommended approaches for components, content collections, and integrations instead of outdated or generic patterns
- **Build accessibly by default** — Every component scaffold and pattern prioritizes semantic HTML and WCAG compliance
- **Stay current** — Looks up documentation in real-time to handle version-specific APIs and breaking changes
- **Ship less JavaScript** — Embraces Astro's islands architecture and static-first philosophy

## Quick Start

```bash
# Install all skills
npx skills add incluud/astro-agent-skills

# Preview what's available
npx skills add incluud/astro-agent-skills --list

# Install a specific skill
npx skills add incluud/astro-agent-skills --skill create-component
```

### Target a Specific Agent

```bash
npx skills add incluud/astro-agent-skills -a codex
npx skills add incluud/astro-agent-skills -a cursor
```

## Skills

| Skill                      | What It Does                                                                                                             |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **`create-component`**     | Scaffolds Astro components, pages, and layouts with proper TypeScript props, slot patterns, and accessibility attributes |
| **`content-collection`**   | Sets up typed content collections with Zod schemas, reference relationships, and efficient querying patterns             |
| **`add-integration`**      | Configures Astro integrations, adapters, and UI frameworks (React, Vue, Svelte) with correct setup and common gotchas    |
| **`docs-lookup`**          | Queries official Astro documentation to answer version-sensitive questions and validate approaches                       |
| **`migrate`**              | Plans and executes migrations to Astro from other frameworks, or between major Astro versions                            |
| **`astro-best-practices`** | Applies performance, accessibility, and maintainability patterns across all Astro work                                   |

## Design Philosophy

These skills are built around a few core beliefs:

1. **Portable by design** — No hard dependencies on specific editors or MCP servers. Install once, use everywhere.
2. **Official sources first** — Prefers Astro's own integrations and documented patterns over community workarounds.
3. **Accessible and performant** — Defaults to semantic HTML, progressive enhancement, and minimal client-side JavaScript.
4. **Composable** — Each skill is focused and task-specific. Combine them as needed.

## Contributing

We welcome contributions that improve Astro support across the AI tooling ecosystem.

1. Fork the repository
2. Edit or create skills in `skills/<name>/SKILL.md`
3. Test with `npx skills add . --list` and install against your preferred agent
4. Submit a pull request

## About

Built by [Incluud](https://incluud.dev) These skills reflect our commitment to building the web the right way — fast, accessible, and maintainable.
