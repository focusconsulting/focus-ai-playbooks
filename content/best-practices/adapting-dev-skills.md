---
title: "Adapting Development Skills to Your Repo"
description: "How to customize the /create_plan, /implement_plan, and /validate_plan commands for a specific repository's stack, conventions, and verification commands."
tags:
  - engineering
weight: 2
---

# Adapting Development Skills to Your Repo

The `/create_plan`, `/implement_plan`, and `/validate_plan` commands that power the [AI Driven Development]({{< relref "ai-driven-development" >}}) workflow are designed to be forked and adjusted per-repository. The base versions encode one repo's directory structure, test commands, linting tools, and conventions. Your repo almost certainly has different ones.

These commands work with any AI coding harness that supports slash commands, including Claude Code (`.claude/commands/`) and OpenCode (`.opencode/commands/`). The command files are the same markdown format in both. If your team uses multiple harnesses, keep the command files in sync or symlink one directory to the other.

This page walks through what to change, what to keep, and includes a prompt you can use to generate a first draft of adapted commands from your existing codebase.

## What's repo-specific

Each command has sections that need to change when you bring it to a new repo. Here's what to look for.

### Project areas and directory structure

The base commands reference specific directories like `api/`, `docs/`, and `cross-cutting/`. Your repo will have its own layout.

In `/create_plan`, update:
- The initial response listing project areas (the "This project has these areas" block)
- The plan file path template (`thoughts/shared/plans/<area>/YYYY-MM-DD-...`)
- The area options used throughout the command
- The plan template's example file paths (e.g., `api/checkin_api/path/to/file.py`)

In `/implement_plan`, update:
- The plan listing command that shows available plans by directory
- The area-specific verification sections

In `/validate_plan`, update:
- The area detection logic (`git diff ... --name-only | cut -d'/' -f1`)
- The area-specific verification commands

### Verification commands

This is the most important thing to get right. The base commands use `pytest`, `pyright`, `ruff check`, `ruff format`, `docker compose build`, etc. Your repo's test runner, type checker, linter, and build commands will differ.

Verification commands appear in three places across the commands:

1. **`/create_plan`**: the success criteria template written into every plan. This is the most critical. If the template has the wrong commands, every plan will have wrong verification steps.

2. **`/implement_plan`**: the commands run after each phase and at completion. These must match what plans will contain.

3. **`/validate_plan`**: the commands run to check that everything passes. These must match too.

All three must be consistent. If `/create_plan` writes `npm test` into plans but `/implement_plan` runs `jest`, the workflow breaks.

Common verification command sets by stack:

| Stack | Tests | Types | Lint | Format | Build |
|-------|-------|-------|------|--------|-------|
| Python | `pytest` | `pyright` or `mypy` | `ruff check .` | `ruff format --check .` | `docker compose build` |
| Node/TS | `npm test` or `jest` | `tsc --noEmit` | `eslint .` | `prettier --check .` | `npm run build` |
| Go | `go test ./...` | (built-in) | `golangci-lint run` | `gofmt -l .` | `go build ./...` |
| Ruby/Rails | `bundle exec rspec` | `srb tc` (Sorbet) | `rubocop` | (usually part of rubocop) | `bundle exec rails assets:precompile` |

### Task tracking integration

The base commands may integrate with a specific task tracker and GitHub issues. Your team might use Linear, Jira, GitHub issues alone, or no tracker at all. Update or remove:

- The "Claim Task and Create Branch" section in `/create_plan`
- Any task tracker integration sections in `/implement_plan`
- Task ID references in branch naming conventions
- Comment/status update commands throughout

If you don't use a CLI-accessible task tracker, simplify these sections to just branch creation and GitHub issue references.

### Branch naming conventions

The base commands use `feature/<task-id>-description` and `fix/<task-id>-description`. Adjust to match your team's convention. Some repos use `<username>/feature-name`, others use `feat/JIRA-123-description`.

### Plan storage paths

Plans go in `thoughts/shared/plans/<area>/`. If your repo doesn't have a `thoughts/` directory, pick a location that works: `docs/plans/`, `.plans/`, or even a separate repo. The key requirement is that plans are committed to git so they're versioned and discoverable.

ADRs live separately in `docs/adrs/`. Handoffs and PR descriptions live in `thoughts/local/`. Update the `/create_adr`, `/create_handoff`, and `/describe_pr` commands to point at the right locations.

### Common patterns section

The `/create_plan` command includes a "Common Patterns" section with guidance for database changes, new features, and refactoring. These reflect one repo's architecture. Replace them with patterns that match yours:

- What does a typical new feature involve in your codebase?
- What's the standard sequence for database/schema changes?
- Does your repo have specific patterns for API endpoints, background jobs, UI components?

## What to keep

Some parts of the commands are repo-agnostic and should stay as-is.

- **The interactive process.** The back-and-forth of research, questions, confirmation, and iteration is the core value. Don't shortcut it.
- **The research agent workflow.** The codebase-locator, codebase-analyzer, and pattern-finder agents work regardless of stack. Keep the parallel research approach.
- **The "no open questions" rule.** Plans must be fully resolved before implementation. This is a process discipline, not a tooling detail.
- **Automated vs. manual verification separation.** Every plan should separate what a command can check from what requires a human. The specific commands change; the separation doesn't.
- **Fresh-session validation.** Running `/validate_plan` in a new session avoids context bias. This applies to every repo.
- **Pause-for-manual-verification** in `/implement_plan`. The AI should stop between phases and wait for human confirmation.

## Generating adapted commands with a prompt

Instead of editing the base commands line by line, you can give the AI your repo context and let it generate adapted versions. Run this in a session where the AI has access to your codebase.

```text
I want to adapt the /create_plan, /implement_plan, and /validate_plan commands
for this repository. Research the codebase first using /research_codebase to
understand the project structure, then generate adapted versions of each command.

Here's what you need to figure out from the codebase:

1. Project areas: What are the main directories/components? What does each contain?
2. Verification commands: What test runner, type checker, linter, formatter, and
   build tools does this repo use? Check package.json, Makefile, pyproject.toml,
   Cargo.toml, or whatever config exists.
3. Task tracking: Do we use GitHub issues, Linear, Jira, or something else?
   Is there a CLI tool for it?
4. Branch conventions: Look at recent branch names in the git history to infer
   the naming convention.
5. Plan storage: Is there an existing directory for plans, docs, or specs?
   If not, recommend one.
6. Common patterns: What does a typical new feature, bug fix, or refactor look
   like in this repo? What files are usually touched together?

For each adapted command, output the full markdown file contents ready to save to
the commands directory (.claude/commands/ or .opencode/commands/ depending on the
harness). Preserve the interactive process, research agent workflow, verification
separation, and fresh-session validation. Only change the repo-specific parts.

Mark every section you changed with a comment like <!-- ADAPTED: reason -->
so I can review what was customized.
```

After the AI generates the adapted commands, review them carefully. The most common mistakes are:

- **Wrong verification commands.** Check that every test/lint/build command actually works when you run it. Try them manually first.
- **Missing areas.** If your repo has a monorepo structure with many packages, make sure all of them are represented.
- **Overly specific patterns.** The "Common Patterns" section should reflect how work is *usually* done, not how one specific feature was built.

## Validating your adapted commands

Before you trust the adapted commands with real work, test them on a small, well-understood task:

1. Run `/create_plan` on something simple. Does it find the right files? Does the plan template have correct verification commands?
2. Run `/implement_plan` on the resulting plan. Does it run the right commands after each phase? Does it pause for manual verification?
3. Run `/validate_plan` in a fresh session. Does it find the implementation and run the right checks?

If any of these fail, fix the command files and try again. The investment in getting these right pays off across every feature you build with them.
