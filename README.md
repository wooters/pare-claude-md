# pare-claude-md

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that pares CLAUDE.md and AGENTS.md files to their bare essentials.

## Motivation

A February 2026 paper from ETH Zurich, ["Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?"](https://arxiv.org/abs/2502.11901) (Gloaguen, Mündler, Müller, Raychev, and Vechev), found that bloated context files hurt more than they help. LLM-generated context files reduced agent success rates by 0.5-2% while increasing inference costs by over 20%. Even developer-written files improved success rates by only ~4%, at the cost of extra tokens and tool steps.

The core finding: agents follow every instruction faithfully, and most of those instructions repeat what the agent already knows. The extra constraints cause agents to explore more files, run more tests, and burn more tokens without solving more problems.

This skill exists to fix that. It strips context files down to what matters.

## The Problem

CLAUDE.md files accumulate boilerplate: generic best practices, standard conventions, and information that any experienced engineer or AI assistant already knows. This bloat wastes context tokens and buries what matters.

## The Solution

This skill applies the **obviousness principle**: if a staff-level software engineer or a capable AI coding assistant would already know it, remove it.

The skill:

1. Explores the repo to understand the stack and architecture
2. Prepends concise core engineering principles
3. Removes anything obvious for the project's stack
4. Keeps anything non-obvious: deviations from convention, gotchas, surprising decisions
5. Tightens the surviving prose

### What Gets Removed

- Standard language and framework conventions
- Generic best practices
- Default tool behavior
- Obvious project structure descriptions
- Information already in config files
- Style rules enforced by linters or formatters

### What Stays

- Unexpected architectural decisions
- Non-obvious setup steps or gotchas
- Custom conventions that differ from community norms
- Environment-specific quirks
- Historical context that prevents repeating past mistakes

> **Obviousness, not discoverability.** Something may appear elsewhere in the codebase, but if it is non-obvious or surprising, it stays. The goal is to save time by surfacing what would otherwise require rediscovery.

## Install

### As a plugin (recommended)

```
/plugin marketplace add wooters/pare-claude-md
/plugin install pare-claude-md
```

### Manual

Copy `pare-claude-md/skills/pare-claude-md/SKILL.md` into your `~/.claude/skills/pare-claude-md/` directory.

## Usage

```
/pare-claude-md
/pare-claude-md ./path/to/CLAUDE.md
```

## Credits

The core engineering principles come from [Daniel Bernal's post on X](https://x.com/afterxleep/status/2025469103972970882).

## License

MIT
