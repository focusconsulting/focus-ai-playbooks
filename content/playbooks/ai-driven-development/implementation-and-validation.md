---
title: "Implementation and Validation"
description: "Execute plans with AI, then validate in a fresh session to catch blind spots."
tags:
  - engineering
weight: 3
---

# Implementation and Validation

You have approved plans. Now the AI executes them and you verify the results. The key discipline here is separation: the AI that wrote the code should not be the only one checking it. A fresh session running validation has no memory of the implementation, no attachment to the approach, and no tendency to gloss over its own shortcuts.

## Implement

Use `/implement_plan` to execute each plan. Run as many in parallel as your dependency graph allows. If tasks A and B are in the same wave with no dependencies between them, run them in separate sessions at the same time.

The `/implement_plan` command works phase by phase:

1. Reads the full plan and all referenced files
2. Implements the changes for one phase
3. Runs the automated verification (tests, type checking, linting)
4. Pauses and reports results, asking you to perform the manual verification steps
5. Moves to the next phase only after you confirm

### Stay engaged during implementation

This isn't a "hand it off and come back later" step. The AI will surface issues when the codebase doesn't match what the plan expected. When it does:

- Read the issue it's reporting. Don't just say "figure it out."
- Decide whether the plan needs updating (use `/iterate_plan`) or whether the AI should adapt within the spirit of the plan.
- If the issue reveals a real architectural question, stop and use `/create_adr` before continuing.

The manual verification between phases is real work, not a rubber stamp. Open the app. Click through the flow. Check the edge cases the plan calls out. If something is wrong, say so now, not after three more phases have been built on top of it.

### Handle parallel implementations

When running multiple implementations in parallel, they'll eventually need to be integrated. Merge conflicts are normal. What you want to avoid is *semantic* conflicts: two implementations that each work alone but break when combined because they made incompatible assumptions about shared code.

Reduce this risk by:

- Defining shared interfaces during task breakdown, before implementation starts
- Having the first wave land and merge before the second wave begins
- Running the full test suite after merging parallel work, not just the tests each task added

## Validate in a fresh session

This is the most important step in the workflow, and the one most likely to be skipped when you're in a hurry. Don't skip it.

Open a **new session** with no history from the implementation. Run `/validate_plan` and point it at the plan and the recent commits. The validator will:

1. Read the plan and identify what should have been implemented
2. Examine the actual code changes via git diff
3. Run all automated verification commands
4. Compare what was planned against what was built
5. Produce a validation report with pass/fail status, deviations, and issues

**Why a fresh session matters:** An AI that just spent an hour implementing a plan has context that biases its evaluation. It knows what it *meant* to do, and it reads the code through that lens. A fresh session only sees what's actually there. It catches missing error handling, skipped edge cases, incomplete implementations, and deviations from the plan that the implementing session normalized.

### Act on the validation report

The report will flag three categories:

- **Matches plan** — Code does what the plan said. No action needed.
- **Deviations from plan** — Code differs from what was planned. Some deviations are improvements (the AI found a better approach). Others are bugs. Review each one.
- **Potential issues** — Things the validator noticed that aren't strictly deviations but are worth attention: missing tests, performance concerns, incomplete error handling.

For issues that need fixing, go back to the implementation session (or start a new one with the plan) and address them. Then validate again. The cycle is: implement, validate, fix, validate.

## Commit your work

After validation passes and you've completed manual testing, commit the changes. Use `/commit` to create well-structured commits that reference the plan and task.

Don't batch everything into one commit. Aim for commits that correspond to plan phases or logical units of work. This makes review easier and gives you rollback granularity if something goes wrong later.

## Prompts

### Validation in fresh session

```text
I need to validate an implementation against its plan.

Plan: [path to plan file]
Implementation commits: [commit range or "last N commits"]

Run /validate_plan to check:
1. Were all phases implemented as specified?
2. Do automated verification commands pass?
3. Are there deviations from the plan? If so, are they improvements or issues?
4. What manual verification steps remain for me to perform?
```

### Post-validation fix

```text
The validation report flagged these issues:

[paste relevant issues from validation report]

The plan is at [path]. Fix the flagged issues while staying within the plan's
intent. If a fix requires changing the approach, explain why before making the change.
```
