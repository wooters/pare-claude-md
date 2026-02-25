# CLAUDE.md

Claude Code skill plugin that pares CLAUDE.md/AGENTS.md files to bare essentials using the "obviousness" principle.

## Architecture

No executable code. The entire implementation is a single structured markdown workflow:

```
.claude-plugin/marketplace.json   — registry entry; `source` points to ./pare-claude-md
pare-claude-md/
  .claude-plugin/plugin.json      — plugin manifest (just names the plugin)
  skills/pare-claude-md/SKILL.md  — the implementation (Claude Code interprets this directly)
```

The double nesting (`pare-claude-md/skills/pare-claude-md/`) is required by the plugin convention: the outer directory is the plugin root (referenced by marketplace.json `source`), the inner path follows the `skills/<skill-name>/SKILL.md` layout that Claude Code expects.

## Development

No build, lint, or test commands. No dependencies.

**To test locally:** copy `pare-claude-md/skills/pare-claude-md/SKILL.md` to `~/.claude/skills/pare-claude-md/SKILL.md`, then invoke with `/pare-claude-md` in any Claude Code session.

**marketplace.json schema:** top-level `plugins` array where each entry needs `name`, `source` (relative path to plugin dir), `description`, `version`, and `category`.
