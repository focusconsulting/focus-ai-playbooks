---
description: Implement technical plans from thoughts/shared/plans with verification
---


# Implement Plan

You are tasked with implementing an approved technical plan from `thoughts/shared/plans/`. These plans contain phases with specific changes and success criteria.

## Getting Started

When given a plan path:
- Read the plan completely and check for any existing checkmarks (- [x])
- Read the original issue/task and all files mentioned in the plan
- **Read files fully** - never use limit/offset parameters, you need complete context
- Think deeply about how the pieces fit together
- Create a todo list to track your progress
- Start implementing if you understand what needs to be done

If no plan path provided, ask for one or list likely plans from the actual shared plan directories used in this repository:
```bash
ls -lt thoughts/shared/plans/ 2>/dev/null
ls -lt thoughts/shared/plans/supper-client/ 2>/dev/null
ls -lt thoughts/shared/plans/prep-manager/ 2>/dev/null
```

## Implementation Philosophy

Plans are carefully designed, but reality can be messy. Your job is to:
- Follow the plan's intent while adapting to what you find
- Implement each phase fully before moving to the next
- Verify your work makes sense in the broader codebase context
- Update checkboxes in the plan as you complete sections

When things don't match the plan exactly, think about why and communicate clearly. The plan is your guide, but your judgment matters too.

If you encounter a mismatch:
- STOP and think deeply about why the plan can't be followed
- Present the issue clearly:
  ```
  Issue in Phase [N]:
  Expected: [what the plan says]
  Found: [actual situation]
  Why this matters: [explanation]

  How should I proceed?
  ```

## Verification Approach

After implementing a phase:

1. **Identify the affected area(s)** from the plan's "Area" field and file paths

2. **Run the plan-specific success criteria checks**:
   - Use the commands explicitly listed in the chosen plan's success criteria.
   - If the plan does not list commands, derive checks from this repository's actual build/test scripts rather than assuming old area directories.

3. **Fix any issues before proceeding**

3. **Update your progress**:
   - Update your todo list and session notes
   - Do not assume direct mutation of plan checkboxes is allowed unless the local workflow explicitly permits it

4. **Pause for human verification**:
   After completing all automated verification for a phase, pause and inform the human:
   ```
   Phase [N] Complete - Ready for Manual Verification

   Automated verification passed:
   - [List automated checks that passed]

   Please perform the manual verification steps listed in the plan:
   - [List manual verification items from the plan]

   Let me know when manual testing is complete so I can proceed to Phase [N+1].
   ```

If instructed to execute multiple phases consecutively, skip the pause until the last phase. Otherwise, assume you are doing one phase at a time.

Do not check off items in the manual testing steps until confirmed by the user.

## Task Tracking Notes

If the repository uses beads or another tracker for the specific task, follow the current repo workflow rather than assuming beads commands are always required.

# Example: git checkout -b feature/bd-f7a3-integration-tests

bd comment ${BEADS_ID} "Starting implementation on branch feature/${BEADS_ID}-..."

# If you discover new tasks
bd create "Discovered issue: description" -t bug -p 2
bd dep add ${NEW_ID} ${BEADS_ID}

# At completion
bd close ${BEADS_ID} --reason "Completed - PR #XXX"
bd sync
```

**Branch naming convention:**
- `feature/<task-id>-short-description` for features
- `fix/<task-id>-short-description` for bugs

Always verify you're on the correct branch before committing:
```bash
git branch --show-current
```

## If You Get Stuck

When something isn't working as expected:
- First, make sure you've read and understood all the relevant code
- Consider if the codebase has evolved since the plan was written
- Present the mismatch clearly and ask for guidance

Use sub-tasks sparingly - mainly for targeted debugging or exploring unfamiliar territory.

## Resuming Work

If the plan has existing checkmarks:
- Trust that completed work is done
- Pick up from the first unchecked item
- Verify previous work only if something seems off

## Committing Progress

After completing a phase or significant milestone:

```bash
# Stage changes
git add .

# Commit with descriptive message referencing the plan
git commit -m "feat: implement Phase N - [description]

- Change 1
- Change 2

Plan: thoughts/shared/plans/YYYY-MM-DD-xxx.md
Task: bd-XXXX or #XXX"
```

## Completion

When all phases are complete:

1. **Run full verification for affected components**:
   - Use the exact success-criteria commands from the plan for the files and products touched.
   - If the plan lacks explicit commands, derive them from this repository's actual package scripts, test commands, and CI patterns.

   **For local integration (all changes):**
    ```bash
    docker compose build
    docker compose up -d
    docker compose ps  # verify all services healthy
    ```

2. **Update task tracking if applicable**:
    - If the task is tracked in beads or another tracker, follow the repository's current tracking workflow.

3. **Suggest next steps**:
   ```
   Implementation complete! All phases finished and verified.

   Next steps:
   1. Run `/describe_pr` to generate PR description
   2. Create PR: `gh pr create --fill`
   3. Close beads task after PR is merged

   Would you like me to proceed with the PR description?
   ```

Remember: You're implementing a solution, not just checking boxes. Keep the end goal in mind and maintain forward momentum.
