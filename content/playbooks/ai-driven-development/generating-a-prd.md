---
title: "Generating a PRD"
description: "Interrogate requirements with AI research and produce a product requirements document with clear acceptance criteria."
tags:
  - engineering
weight: 1
---

# Generating a PRD

The PRD is where you slow down before you speed up. Most wasted development time comes from building the wrong thing, not building the right thing slowly. This phase uses the AI to research the codebase, interrogate the requirements, and produce a document that everyone can point to when they need to know what "done" looks like.

## Start with the raw input

You're working from a ticket, user story, Slack thread, meeting notes, or some combination. Paste it all into the AI session. Don't clean it up first. Contradictions and ambiguity in the raw material are exactly what you want to surface now, not during implementation.

Tell the AI to start by researching the codebase using `/research_codebase`. This grounds the conversation in what actually exists. The AI will spawn agents (codebase-locator, codebase-analyzer, thoughts-locator) to map out the relevant code, find similar implementations, and check for prior research or decisions. The research output gets saved to your [thoughts/ directory](../../best-practices/thoughts-directory.md) as a dated document, so it's available to every later phase. Let this finish before you start discussing requirements.

## Interrogate the requirements

With the codebase research in hand, work through the requirements with the AI. Push hard on specifics:

- **What exactly should change?** Not "improve the search," but "add filtering by date range to the search results endpoint and expose it in the UI."
- **What's the scope boundary?** Name what you're not doing. This prevents scope creep during implementation and gives the AI clear guardrails when planning.
- **What are the acceptance criteria?** Be concrete. "User can filter search results by start and end date. If no end date is provided, it defaults to today. The date picker matches the existing component library."
- **What needs manual verification?** Some things can't be checked by automated tests. A UI that feels right, a workflow that makes sense to a user, performance under real data. Call these out explicitly. They become the manual verification steps in every plan.
- **What are the constraints?** Existing APIs you can't change, performance requirements, backwards compatibility, compliance rules. The AI needs to know these before it starts planning.

Don't accept the AI's first pass. If it restates the ticket without adding anything, push back: "What assumptions are you making? What's ambiguous here? What would you ask the product owner?" The AI is good at identifying gaps when you explicitly ask it to.

## Surface architectural questions early

The research phase often reveals that what seemed like a simple feature touches something structural. Maybe the data model doesn't support the new use case. Maybe there's no existing pattern for the kind of API you need.

When the AI surfaces these, take them seriously. Some belong in the PRD as constraints ("requires a database migration"). Others need to be resolved before planning can start. For significant architectural choices, use `/create_adr` to document the decision now rather than embedding it in the PRD where it'll get lost.

## Record your analysis in thoughts/

As you work through requirements and surface architectural questions, the analysis you're building has value beyond this session. Save the PRD itself and any requirements analysis to your `thoughts/` directory. The codebase research is already there (from `/research_codebase`). Add the PRD alongside it so the planning phase can reference both.

For a single-app repo, the PRD goes in `thoughts/shared/plans/` next to where the implementation plans will land. For a monorepo, scope it to the relevant package (e.g., `thoughts/api/shared/plans/`). If the feature spans packages, use `thoughts/shared/plans/cross-cutting/`.

This also means the thoughts-locator agent can find your PRD and research in future sessions. If someone starts a related feature later, the prior analysis is discoverable rather than buried in a chat log.

## Write the PRD

Ask the AI to draft the PRD from the conversation. A useful structure:

**Problem statement** — What's the situation and why does this work need to happen?

**Scope** — What's included and what's explicitly excluded.

**Requirements** — Specific, testable statements of what the system should do when this work is complete.

**Acceptance criteria** — How you know each requirement is met. Separate automated checks (tests pass, API returns expected response) from manual verification (UI renders correctly, workflow feels right).

**Constraints** — Technical limitations, compatibility requirements, performance targets.

**Open questions** — Anything unresolved. These must be answered before moving to task breakdown. Don't carry them forward.

**Related** — Links to the ticket, any ADRs created during this phase, and the codebase research document in `thoughts/`. These cross-references are how later sessions trace the reasoning chain from requirements through to implementation.

## Review and approve

Read the PRD as if you're the person who has to implement it without access to the original conversation. Is anything ambiguous? Are the acceptance criteria specific enough to write tests against? Are the manual verification steps clear enough that someone else could perform them?

If the PRD has open questions, resolve them now. The rule is simple: no open questions leave this phase. Every question deferred here becomes a wrong assumption discovered during implementation.

Once you're satisfied, the PRD is your contract for the rest of the workflow. Changes are fine, but they should be deliberate, not accidental.

## Prompts

### Requirements interrogation

```text
I'm starting work on a feature. Here's the raw input (ticket, user story, notes):

[paste raw input]

Before we discuss requirements, research the codebase to understand what exists today
that's relevant. Use /research_codebase to map out the affected code, find similar
implementations, and check for prior decisions.

Once that's done, help me interrogate these requirements:
- What's ambiguous or underspecified?
- What assumptions are we making?
- What questions would you ask the product owner?
- What's the scope boundary — what are we explicitly not doing?
```

### PRD draft

```text
Based on our discussion, draft a PRD with this structure:

- Problem statement
- Scope (included and excluded)
- Requirements (specific, testable)
- Acceptance criteria (separated into automated and manual verification)
- Constraints
- Open questions (these must be resolved before we proceed)
- Related (links to ticket, ADRs, research docs in thoughts/)

Write it so someone who wasn't in this conversation could implement from it.
Save the PRD to the thoughts/ directory alongside the codebase research document.
```
