---
name: status
description: Give a quick read-only briefing on where a project stands. Reads the plan, the latest to-do audit, the work log, the decision log, and git history, then summarizes progress, what Claude did last, what's in progress, and what to do next. Writes no files. Use at the start of a session, when resuming work, or when the user asks "where are we?", "what's been done?", or "what was Claude working on?".
---

# Project status briefing

Give the user a short, accurate picture of where the project is. This skill only reads. It doesn't audit the code in depth or change any files. For a full audit, the user runs `/project-tracker:todo`.

## 1. Gather what exists

Read whichever of these exist at the project root. Skip any that are missing, and note which ones are missing.

- `PROJECT-PLAN.md`: the task list (from `/project-tracker:plan`).
- `SITE-TODO.md`: the latest audit and plan status (from `/project-tracker:todo`). Note its "Last updated" date.
- `PROJECT-LOG.md`: the work log (from `/project-tracker:log`). Read the newest three entries.
- `DECISIONS.md`: the decision log (from `/project-tracker:decision`). Read the newest five decisions.

Also run these if the folder is a git repository:
- `git log --oneline -15 --date=short --format="%h %ad %s"` to see recent commits.
- `git status --short` to see uncommitted changes.

## 2. Check how fresh the audit is

Compare the `SITE-TODO.md` date with the newest commit and the newest log entry. If code has changed since the last audit, say the plan status may be out of date and suggest running `/project-tracker:todo`. Don't present old statuses as current.

## 3. Brief the user in chat

Keep it to about 15 lines and use these headings:

- **Progress:** tasks done out of the total and the percentage, from the latest audit, with its date. Name the phase the project is in (the earliest phase that still has unfinished Must tasks).
- **Last session:** what the newest log entry says was done, with its date and task IDs.
- **In progress:** tasks marked In progress in the audit or left unfinished in the log, plus any uncommitted changes from `git status`.
- **Blockers:** Blocked and Needs owner tasks, and open questions from the plan or log.
- **Recent decisions:** one line for each decision made since the last session, if any.
- **Next up:** the three best next tasks. Pick unblocked Must tasks first, then Should tasks, in phase order. Also list any Critical issues from the audit.

If none of the tracking files exist, say so and suggest starting with `/project-tracker:plan`.

Report only what the files and git show. If two sources disagree, for example the log says a task is done but the audit says it isn't, point out the conflict instead of picking one.
