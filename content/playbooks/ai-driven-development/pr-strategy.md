---
title: "PR Strategy"
description: "Structure pull requests for meaningful review using a PRD branch with task-level PRs."
tags:
  - engineering
---

# PR Strategy

The PR strategy you choose determines whether reviewers can give meaningful feedback or just rubber-stamp a wall of diffs. For AI-driven development, where a single feature can produce a lot of code quickly, this matters more than usual.

## The approach: PRD branch with task PRs

Create a feature branch from main for the overall PRD. Call it something like `feature/issue-123-search-filters` or `prd/user-authentication`. This is your PRD branch.

For each task or plan, create a short-lived branch off the PRD branch. Implement, validate, then open a PR back into the PRD branch. Each of these PRs is small, focused, and reviewable.

Once all task PRs are merged into the PRD branch:

1. Run the full test suite on the PRD branch
2. Perform a final round of manual verification against the PRD's acceptance criteria
3. Open a single PR from the PRD branch to main

```
main
 │
 └── feature/issue-123-search-filters  (PRD branch)
      │
      ├── task/123-e2e-tests           → PR into PRD branch
      ├── task/123-date-filter-api     → PR into PRD branch
      ├── task/123-date-filter-ui      → PR into PRD branch
      └── task/123-filter-validation   → PR into PRD branch
                                          │
                                          ▼
                                    Final PR into main
```

## Why this structure

**Small PRs get real reviews.** A reviewer looking at 50 changed lines across 3 files will actually read the code. A reviewer looking at 800 changed lines across 40 files will skim.

**Each task PR matches a plan.** The reviewer can read the plan (linked in the PR description) and check the implementation against it. This is structured review, not "does this code look okay to me."

**The PRD branch is a clean integration point.** You can catch conflicts between parallel tasks early, on the feature branch, without polluting main.

**Rollback is simple.** If the feature needs to be pulled, you revert one merge commit on main. You don't need to untangle interleaved commits from other work.

**The final PR to main is a formality.** Every piece was already reviewed at the task level. The final PR is a sanity check on the integration, not a first review of the code.

## Generating PR descriptions

Use `/describe_pr` for each task PR. The command will:

1. Analyze the diff against the PRD branch
2. Read the implementation plan and embed it in a collapsible section
3. Run automated verification checks
4. Generate a structured description with summary, changes, and test instructions

The embedded plan is the audit trail. After the PR merges, the plan file in `thoughts/shared/plans/` can be cleaned up since the PR preserves its content.

## The final PR to main

For the final PR from the PRD branch to main, write a description that covers the whole feature:

- Reference the PRD and link to it
- Summarize all the task PRs that were merged
- Note the acceptance criteria and their verification status
- Call out anything the reviewer should pay special attention to

Use a squash merge or a well-structured merge commit so main's history stays readable. The detailed commit history lives on the PRD branch for anyone who needs it.

## Getting human review

AI-driven development produces code fast. That speed is wasted if the review is sloppy. A few things help:

- **Link the plan in every PR.** The reviewer should see what was intended, not just what was produced.
- **Ask for review of the approach, not just the code.** "Does this data model make sense for our use case?" is a better review prompt than "please review."
- **Don't merge without a human reviewer.** The AI validated the implementation against the plan. A human validates that the plan was the right plan.
