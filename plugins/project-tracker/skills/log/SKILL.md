---
name: log
description: Record what Claude did in this session as a new entry in PROJECT-LOG.md. Covers the tasks worked on, the files changed, decisions, problems, and next steps, so the next session (or another person) can see exactly what happened. Use at the end of a work session, after finishing a task, or when the user asks to log, record, or write down what was done.
---

# Work log entry

Add one entry to `PROJECT-LOG.md` at the project root, describing the work done in this session. The log is the running history of what Claude did on the project.

## 1. Gather the facts

- Go back over this conversation: what the user asked for, what you changed, and what you checked.
- If the folder is a git repository, see what changed:
  - `git status --short` for uncommitted changes.
  - `git log --oneline` for commits made since the last log entry's date.
  - `git diff --stat` for the size of the changes.
- If `PROJECT-PLAN.md` exists, connect the work to its task IDs.
- Read the newest entry already in `PROJECT-LOG.md`, so you don't repeat it.

## 2. Write the entry

If `PROJECT-LOG.md` doesn't exist, create it with the heading `# Project Log` and the line `_Newest entries first. Each entry is added by Claude at the end of a work session._`.

Put the new entry directly under that intro, above all older entries:

```markdown
## YYYY-MM-DD HH:MM: <short title of what was done>

**Summary:** 1-2 sentences on what this session achieved.

**Tasks**
- **P-004** Create the Services page: Done (checked against its Done when condition)
- **P-005** Add a mobile menu: Partly done. The toggle works, but `aria-expanded` isn't updated yet.

**Files changed**
- `services.html` (new)
- `css/nav.css`, `js/menu.js`

**Decisions**
- D-003 Use a CSS-only dropdown for the submenus

**Problems noticed (not fixed)**
- The footer link to `/privacy` goes to a missing page.

**Next steps**
- Finish P-005: update `aria-expanded` in `js/menu.js`.

**Commits:** `a1b2c3d`, `e4f5g6h` (or "Uncommitted")
```

Leave out any section that has nothing in it.

## 3. Rules

- Record only what actually happened. Don't mark a task Done unless you checked it. Label anything you didn't check, for example "not tested."
- Never edit or delete older entries. If an older entry was wrong, say so in the new entry.
- Keep it concise. List the files changed, but don't describe every line of code.
- Use the time from the system clock, for example with `date "+%Y-%m-%d %H:%M"`.

## 4. Report back

Tell the user in one or two lines that the session is logged, and give the entry's title.
