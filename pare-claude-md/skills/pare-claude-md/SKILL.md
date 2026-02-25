---
name: pare-claude-md
description: Pare down a CLAUDE.md or AGENTS.md file to its bare essentials using the "obviousness" principle. Removes anything a staff-level engineer or AI assistant would already know, and ensures the file starts with core engineering principles.
argument-hint: "[path to CLAUDE.md or AGENTS.md]"
---

# Pare CLAUDE.md / AGENTS.md

Trim a CLAUDE.md or AGENTS.md file to only what matters: non-obvious, project-specific information that deviates from convention.

## Step 1: Identify the target file

If `$ARGUMENTS` is provided, use it as the file path. Otherwise, look for CLAUDE.md or AGENTS.md in the current working directory. If multiple exist, ask the user which one to pare.

Read the file in full before making any changes.

## Step 2: Explore the repository

Before deciding what's obvious vs. non-obvious, build context about the project. Use the Explore agent or Glob/Grep/Read tools to survey:

- **Project type and stack**: language(s), framework(s), build system, package manager
- **Repo structure**: top-level directories, monorepo vs single project, workspace layout
- **Config files**: package.json, tsconfig.json, pyproject.toml, Makefile, Dockerfile, CI configs, etc.
- **Key architectural patterns**: how modules connect, entry points, API boundaries
- **Existing tooling**: linters, formatters, test frameworks, pre-commit hooks

Spend no more than a few minutes on this. The goal is not a full audit — it's enough context to judge which CLAUDE.md entries are genuinely non-obvious for *this specific repo* versus which are standard for its stack.

## Step 3: Prepend core engineering principles

Ensure the file begins with this block (add it if missing, replace any existing version):

```markdown
## Core Engineering Principles

1. **Clarity over cleverness** — Write code that's maintainable, not impressive
2. **Explicit over implicit** — No magic. Make behavior obvious
3. **Composition over inheritance** — Small units that combine
4. **Fail fast, fail loud** — Surface errors at the source
5. **Delete code** — Less code = fewer bugs. Question every addition
6. **Verify, don't assume** — Run it. Test it. Prove it works
```

## Step 4: Apply the Obviousness Principle

Go through every remaining section, bullet, and instruction in the file. For each piece of information, ask:

> "Would a staff-level software engineer, or a capable AI coding assistant, already know this or consider it standard practice?"

**Remove** anything that is:
- Standard language/framework conventions (e.g., "use `const` instead of `let` when the value doesn't change")
- Generic best practices any senior engineer follows (e.g., "write tests," "handle errors," "use meaningful variable names")
- Default tool behavior (e.g., "run `npm install` before `npm start`")
- Obvious project structure descriptions that match convention (e.g., "src/ contains source code," "tests/ contains tests")
- Restating what's already in package.json, tsconfig, pyproject.toml, or other config files
- Generic coding style rules that a formatter/linter enforces

**Keep** anything that is:
- Unexpected architectural decisions or deviations from convention
- Non-obvious project-specific setup steps or gotchas
- Custom conventions that differ from community norms
- Surprising dependency choices or version constraints with reasons
- Environment-specific quirks (e.g., "CI uses Node 18 but local dev uses Node 20")
- Historical context that prevents repeating past mistakes
- Non-obvious relationships between components
- Anything that would take significant time to rediscover by reading the codebase

**Important clarification:** This is about obviousness, not discoverability. Even if something *could* be found by searching the codebase, if it's non-obvious or surprising, keep it. The point is to avoid wasting time rediscovering things.

## Step 5: Tighten the prose

For any content that survives the obviousness filter:
- Use short, direct sentences
- Prefer bullets over paragraphs
- Remove filler words and hedging
- One idea per bullet
- No preambles or explanations of what the file is

## Step 6: Present the result

Show the user a before/after comparison:
1. State how many lines/sections were removed and why (group by reason)
2. Show the final file content
3. Ask for confirmation before writing the changes

If the file was already lean, say so and suggest no changes.
