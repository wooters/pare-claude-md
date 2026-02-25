# pare-claude-md

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that pares down CLAUDE.md and AGENTS.md files to their bare essentials.

## The Problem

CLAUDE.md files tend to accumulate obvious boilerplate — generic best practices, standard conventions, and information that any experienced engineer or AI assistant already knows. This bloat wastes context tokens and buries the information that actually matters.

## The Solution

This skill applies the **obviousness principle**: if a staff-level software engineer or a capable AI coding assistant would already know it, it doesn't belong in the file.

The skill:

1. Explores the repo to understand the stack and architecture
2. Prepends a concise set of core engineering principles
3. Removes anything obvious for that specific project's stack
4. Keeps anything non-obvious — deviations from convention, gotchas, surprising decisions
5. Tightens the surviving prose

### What Gets Removed

- Standard language/framework conventions
- Generic best practices
- Default tool behavior
- Obvious project structure descriptions
- Information already in config files
- Style rules enforced by linters/formatters

### What Gets Kept

- Unexpected architectural decisions
- Non-obvious setup steps or gotchas
- Custom conventions that differ from community norms
- Environment-specific quirks
- Historical context that prevents repeating past mistakes

> **Obviousness, not discoverability.** Even if something *could* be found by searching the codebase, if it's non-obvious or surprising, it stays. The point is to avoid wasting time rediscovering things.

## Install

### As a plugin (recommended)

```
/plugin marketplace add wooters/pare-claude-md
/plugin install pare-claude-md
```

### Manual

Copy `skills/pare-claude-md/SKILL.md` into your `~/.claude/skills/pare-claude-md/` directory.

## Usage

```
/pare-claude-md
/pare-claude-md ./path/to/CLAUDE.md
```

## Credits

The core engineering principles used by this skill are based on [Daniel Bernal's post on X](https://x.com/afterxleep/status/2025469103972970882).

## License

MIT
