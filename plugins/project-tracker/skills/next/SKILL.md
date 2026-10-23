---
name: next
description: Pick the next task from PROJECT-PLAN.md, or the one the user names (for example "P-007"), and work on it in a tracked way. Claude announces the task and its plan, does only that task, checks the result against the task's "done when" condition, and records it in the work log. Use when the user says "work on the next task", "keep going", "do P-012", or wants Claude to move the project forward one step at a time.
---

# Work on the next planned task

Move the project forward by one task, and leave a record of exactly what was done.

## 1. Choose the task

- If the user named a task ID, use that one.
- Otherwise, read `PROJECT-PLAN.md` and the latest `SITE-TODO.md`. Pick the first task, in phase order and then ID order, that:
  - isn't Done and isn't struck through,
  - isn't marked `(owner)`,
  - has all the tasks in its `Depends on` list done,
  - is a **Must** task. Only move on to **Should** tasks once no Must tasks are left, then to **Could** tasks.
- Before choosing, check the task's current state in the code quickly, because the audit may be out of date. If it's already done, say so and pick the next one.
- If there is no `PROJECT-PLAN.md`, stop and suggest `/project-tracker:plan`.

## 2. Announce before working

Tell the user, in a few lines:
- the task ID and title,
- its **Done when** condition,
- the files you expect to create or change, and your approach.

If the task needs something only the owner can provide, such as real copy, images, or account access, ask for it instead of using a placeholder. If the user asked you to confirm before starting, wait for their go-ahead.

## 3. Do the task

- Stay within the task's scope. If you notice other problems, list them for the log instead of fixing them.
- Don't add placeholder content, such as lorem ipsum or fake images, unless the user agrees. The `todo` audit flags placeholders as unfinished work.
- If you have to choose between real alternatives, such as a library, a structure, or a design approach, record the choice with `/project-tracker:decision`.

## 4. Check the result

Go through each part of the **Done when** condition and confirm it in the code. Run the build or tests if the project has them. Give the task one result:
- **Done:** every part of the condition is met.
- **Partly done:** say what's left and why.
- **Stuck:** say what blocks it.

Don't call a task Done unless you checked it. Don't tick its box in `PROJECT-PLAN.md`, because the `todo` audit works out status from the code.

## 5. Log it

Add an entry to `PROJECT-LOG.md` following the `log` skill's format: the task ID and result, the files changed, any decisions, the problems you noticed, and the next step.

## 6. Report back

In a few lines, tell the user the task, its result, the files changed, and what the next task will be. Ask whether to continue with it.
