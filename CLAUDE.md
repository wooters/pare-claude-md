# CLAUDE.md

## Core Engineering Principles

1. **Clarity over cleverness** — Write code that's maintainable, not impressive
2. **Explicit over implicit** — No magic. Make behavior obvious
3. **Composition over inheritance** — Small units that combine
4. **Fail fast, fail loud** — Surface errors at the source
5. **Delete code** — Less code = fewer bugs. Question every addition
6. **Verify, don't assume** — Run it. Test it. Prove it works

## What This Is

Claude Code skill plugin that pares CLAUDE.md/AGENTS.md files to bare essentials using the "obviousness" principle. No executable code — pure markdown workflow.

## Architecture

The double nesting (`pare-claude-md/skills/pare-claude-md/`) is required by plugin convention: outer dir is the plugin root (referenced by marketplace.json `source`), inner path follows `skills/<skill-name>/SKILL.md`.

## Development

- **Test locally:** copy `pare-claude-md/skills/pare-claude-md/SKILL.md` to `~/.claude/skills/pare-claude-md/SKILL.md`, then invoke `/pare-claude-md`
- **marketplace.json schema:** top-level `plugins` array; each entry needs `name`, `source`, `description`, `version`, `category`
