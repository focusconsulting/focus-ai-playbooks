---
title: "Task Breakdown and Planning"
description: "Break a PRD into parallelizable tasks with dependency ordering, then create detailed implementation plans."
tags:
  - engineering
weight: 2
---

# Task Breakdown and Planning

You have an approved PRD. Now you need to turn it into work that can actually be executed, ideally as much of it in parallel as the dependencies allow. This phase breaks the PRD into discrete tasks, orders them by dependency, and produces implementation plans detailed enough that the AI (or another developer) can execute them without guessing.

## Break the PRD into tasks

Work with the AI to decompose the PRD into tasks. Each task should be a unit of work that can be planned, implemented, and verified independently.

The goal is parallelism. Ask the AI: "Which of these tasks have no dependencies on each other? What's the minimum number of waves needed to complete everything?" A wave is a set of tasks that can all run at the same time because none depends on the output of another in the same wave.

**Start with tests.** The strong default is that the first task (or first wave) is writing tests: E2E tests, integration tests, or whatever the codebase uses. Writing tests first forces you to specify the expected behavior concretely before anyone writes production code. The AI's plans are better when there's a test suite defining what "correct" looks like.

This isn't always the right call. Infrastructure work, database migrations, or foundational refactors sometimes need to land before tests can be written against them. Use your judgment, but default to test-first unless you have a reason not to.

## Approve the task graph

Before any planning starts, review the task list and dependencies with the AI. You're checking:

- **Completeness** — Do the tasks cover everything in the PRD? Is anything missing?
- **Granularity** — Is each task small enough to plan and implement in one session? If a task feels like it needs its own PRD, it's too big.
- **Dependencies** — Are the dependencies correct? Can wave 2 actually start without wave 1 being done? Are there hidden dependencies the AI missed?
- **Test coverage** — Where do tests fit in the dependency graph? Can they be written early?

Push back if the AI proposes a linear chain of tasks that could be parallelized. "Why does task 4 depend on task 3? Could they run at the same time if we define the interface first?" The AI tends to be conservative about dependencies; often a shared interface or type definition is all that's needed to unblock parallel work.

## Create implementation plans

Once you've approved the tasks and dependencies, use `/create_plan` to create a detailed implementation plan for each task in the first wave. Run as many in parallel as the dependencies allow.

The `/create_plan` command will:

1. Research the codebase with specialized agents (codebase-locator, codebase-analyzer, codebase-pattern-finder)
2. Present its understanding and ask you targeted questions
3. Surface design options and recommend an approach
4. Flag architectural decisions that warrant an ADR
5. Write a phased plan with separated automated and manual verification

### Answer the AI's questions carefully

During planning, the AI will surface questions it can't answer from the code alone. These are important. They're usually about business logic, design preferences, or tradeoffs that require human judgment.

When the AI flags an architectural decision, decide whether it needs an ADR. The `/create_adr` command documents the decision, options considered, and rationale. This matters later when someone asks "why did you do it this way?"

Don't rush through the questions to get to implementation faster. Wrong answers here become wrong code later, and the AI will implement your wrong answer with confidence.

### Review the plans

Read each plan before approving it. You're checking:

- **Automated verification is thorough.** Each phase should have commands you can run to verify correctness: tests, type checking, linting, build commands. If a phase has no automated verification, ask why.
- **Manual verification is clear.** The steps should be specific enough that someone else could perform them. Not "check that it works" but "navigate to /settings, change the date range, verify the results update without a page reload."
- **Phases are ordered correctly.** Each phase should build on the last. If a later phase would be invalidated by a change in an earlier one, the ordering is wrong.
- **No open questions.** The plan should be fully resolved. If the AI left questions in the plan, answer them now and have it update the plan with `/iterate_plan`.

## Re-evaluate parallelism

After the plans are written, look at them together. The planning process sometimes reveals new parallelism opportunities or new dependencies that weren't obvious during task breakdown.

Ask the AI: "Given what we now know from the plans, which implementations can run in parallel? Are there any new dependencies we didn't see before?"

Update the execution order if needed. The goal is always to maximize parallel work without breaking dependencies.

## Prompts

### Task breakdown

```text
Here's the approved PRD:

[paste PRD or reference the document]

Break this into discrete tasks, each one independently plannable and implementable.
Optimize for parallelism: identify which tasks can run at the same time and which
have dependencies. Organize them into waves.

The first wave should be writing tests unless there's a reason it can't be
(infrastructure that needs to land first, etc.).

For each task, specify:
- What it accomplishes
- What it depends on (if anything)
- Which wave it belongs to
```

### Plan review checklist

```text
I'm reviewing the implementation plan at [plan path]. Check it against these criteria:

1. Does every phase have automated verification commands?
2. Are the manual verification steps specific enough for someone else to perform?
3. Are the phases ordered correctly — does each build on the last?
4. Are there any open questions or unresolved decisions?
5. Does the plan match what the PRD requires?

Flag anything that doesn't meet these criteria.
```
