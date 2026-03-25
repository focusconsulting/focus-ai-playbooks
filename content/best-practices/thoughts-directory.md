---
title: "The thoughts/ Directory"
description: "How to set up and use the thoughts/ directory as a shared knowledge layer for AI-assisted development."
tags:
  - engineering
weight: 3
---

# The thoughts/ Directory

The `thoughts/` directory is a committed-to-git knowledge layer that sits alongside your code. It holds implementation plans, research documents, handoff documents, and PR descriptions. The AI development commands (`/create_plan`, `/implement_plan`, `/validate_plan`, `/research_codebase`, `/create_handoff`) all read from and write to it.

Architecture Decision Records live separately in `docs/adrs/`. ADRs are permanent project documentation, not ephemeral session artifacts. They belong alongside your other docs where developers will find them without knowing about the thoughts directory. The `/create_adr` command writes there.

The directory exists because AI sessions are ephemeral but the context they produce is not. A planning session generates detailed codebase analysis, architectural decisions, and implementation steps. Without a place to put those, the next session starts from zero. With `thoughts/`, each session builds on the last.

## Structure

For a single-application repo:

```text
thoughts/
├── shared/              # Committed to git, visible to the team
│   ├── plans/           # Implementation plans (by area)
│   │   ├── api/
│   │   ├── frontend/
│   │   └── cross-cutting/
│   └── research/        # Codebase research documents (by area)
│       ├── api/
│       └── general/
└── local/               # Gitignored, personal scratchpad
    ├── handoffs/        # Session handoff documents (by task)
    │   ├── issue-123/
    │   └── bd-a1b2/
    └── prs/             # PR descriptions (working files)

docs/
└── adrs/                # Architecture decision records (permanent docs)
```

For a monorepo, the breakdown goes one level deeper. Each top-level package or service gets its own `thoughts/` subtree so plans, research, and handoffs stay scoped to the area they belong to:

```text
thoughts/
├── api/                 # Scoped to the api/ package
│   ├── shared/
│   │   ├── plans/
│   │   └── research/
│   └── local/
│       └── handoffs/
├── web/                 # Scoped to the web/ package
│   ├── shared/
│   │   ├── plans/
│   │   └── research/
│   └── local/
│       └── handoffs/
├── shared/              # Cross-cutting concerns
│   ├── plans/
│   │   └── cross-cutting/
│   └── research/
│       └── general/
└── local/               # Personal scratchpad (gitignored)
    └── prs/

docs/
└── adrs/                # Architecture decision records (permanent docs)
```

The key principle: the AI's plans and research should be findable in the same place you'd look for the code they describe. If a plan is about the API, it lives under `thoughts/api/`. If it spans multiple packages, it goes in `thoughts/shared/plans/cross-cutting/`. Handoffs are local because they're session-to-session working state, not shared documentation. ADRs live in `docs/adrs/` because they're permanent project documentation that developers should find alongside other docs, not buried in a directory for ephemeral AI artifacts.

### shared/

Everything in `shared/` (and in monorepos, everything outside `local/`) is committed to git. It's the team's shared knowledge base for AI-assisted work. When an AI agent runs `/research_codebase` or the thoughts-locator agent searches for prior work, this is where it looks.

### local/

Session artifacts and personal scratchpads. Add `thoughts/local/` (and `thoughts/*/local/` for monorepos) to your `.gitignore`. Handoffs and PR descriptions live here because they're working state between sessions, not shared documentation. Notes-to-self and draft ideas go here too.

## What goes where

### plans/

Implementation plans created by `/create_plan`, organized by area (matching your repo's top-level directories). Each plan is dated and tied to an issue or task.

**Naming:** `YYYY-MM-DD-issue-XXX-description.md`

**Lifecycle:** A plan is created during the planning phase, updated by `/iterate_plan` as you refine it, referenced by `/implement_plan` during execution, and checked by `/validate_plan` afterward. When the PR merges, the plan content lives in the PR description (embedded by `/describe_pr`), and the plan file can be deleted with `/cleanup`.

### research/

Codebase research documents created by `/research_codebase`. These are point-in-time snapshots of how the code works, produced before planning begins. They include file:line references, data flow traces, and architectural observations.

**Naming:** `YYYY-MM-DD-description.md`

**Lifecycle:** Research documents are reference material. They're most valuable during the planning phase but remain useful as historical context. The thoughts-locator and thoughts-analyzer agents search them when looking for prior knowledge about a part of the codebase. They go stale as the code changes, so treat them as "what was true on this date" rather than current documentation.

### handoffs/ (local)

Session handoff documents created by `/create_handoff`, organized by task ID. These live in `thoughts/local/handoffs/` (or `thoughts/<package>/local/handoffs/` in monorepos) because they're working state between sessions, not shared documentation. When you need to stop work in one session and continue in another, the handoff captures what was done, what was learned, and what's next. `/resume_handoff` picks up from the most recent handoff for a task.

**Naming:** `YYYY-MM-DD_HH-MM-SS_description.md` inside a task-ID directory

**Lifecycle:** Handoffs are consumed by the resuming session. After work is complete and merged, they can be cleaned up.

### prs/ (local)

PR descriptions generated by `/describe_pr`. These live in `thoughts/local/prs/` and are used to create or update PRs via `gh pr create --body-file`. They don't get committed since the content goes into the PR itself.

### docs/adrs/ (separate from thoughts)

Architecture Decision Records created by `/create_adr`. These live in `docs/adrs/`, not in `thoughts/`, because they're permanent project documentation. ADRs capture the context, options considered, and rationale behind significant technical decisions. Developers should find them alongside other docs, not buried in a directory for ephemeral AI artifacts.

**Naming:** `NNNN-short-title.md` (zero-padded sequential number)

**Lifecycle:** ADRs are immutable. When a decision is superseded, create a new ADR and update the old one's status. They don't get deleted. A template lives at `docs/adrs/0000-adr-template.md`.

## Setting up thoughts/ in a new repo

### Single-application repo

```bash
mkdir -p thoughts/shared/{plans,research}
mkdir -p thoughts/local/{handoffs,prs}
mkdir -p docs/adrs
```

Add to `.gitignore`:

```text
thoughts/local/
```

Create area subdirectories under `plans/` and `research/` that match your repo's top-level structure. If your app has `api/` and `frontend/` directories:

```bash
mkdir -p thoughts/shared/plans/{api,frontend,cross-cutting}
mkdir -p thoughts/shared/research/{api,frontend,general}
```

### Monorepo

Create a `thoughts/` subtree for each package, plus the repo-level shared directory:

```bash
# Per-package thoughts
for pkg in api web worker; do
  mkdir -p thoughts/$pkg/shared/{plans,research}
  mkdir -p thoughts/$pkg/local/handoffs
done

# Repo-level shared (cross-cutting plans)
mkdir -p thoughts/shared/{plans/cross-cutting,research/general}
mkdir -p thoughts/local/{handoffs,prs}

# ADRs in docs
mkdir -p docs/adrs
```

Add to `.gitignore`:

```text
thoughts/local/
thoughts/*/local/
```

### Finish setup

Create the ADR template at `docs/adrs/0000-adr-template.md`. The `/create_adr` command references this file. Copy it from an existing repo or let the AI generate one on first use.

Add `.gitkeep` files to empty directories if you want them tracked before any content exists, then commit:

```bash
find thoughts -type d -empty -exec touch {}/.gitkeep \;
find docs/adrs -type d -empty -exec touch {}/.gitkeep \;
git add thoughts/ docs/adrs/
git commit -m "chore: add thoughts/ and docs/adrs/ directory structure"
```

### Adapting the commands

The area paths in your thoughts directory need to match what your adapted commands expect. When `/create_plan` writes a plan, it needs to know whether to put it in `thoughts/shared/plans/api/` (single repo) or `thoughts/api/shared/plans/` (monorepo). Similarly, `/create_adr` needs to point at `docs/adrs/`, and `/create_handoff` needs to write to `thoughts/local/handoffs/`. Update the path templates in your commands accordingly. See [Adapting Development Skills to Your Repo]({{< relref "adapting-dev-skills" >}}) for the full list of what to change.

## Keeping it clean

The thoughts directory accumulates artifacts. After a feature ships, plans and handoffs for that feature are no longer actively useful. Research documents go stale as the code changes. Without periodic cleanup, the directory becomes noisy and the AI agents waste time reading outdated material.

**After a PR merges:** Delete the plan file (its content is embedded in the PR). Handoff files in `local/` will naturally get cleaned up since they're gitignored. The `/cleanup` command automates plan removal.

**Periodically:** Review research documents. Delete ones about code that has significantly changed. If an area of the codebase has been heavily refactored, old research about it will mislead more than help.

**Never delete ADRs.** They live in `docs/adrs/` and are the historical record of why decisions were made. Update their status if superseded, but keep them.

**Rule of thumb:** If the thoughts-locator agent would return a document and that document would give the AI wrong information about the current codebase, delete it.
