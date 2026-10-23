# moloney-claude-tools

A Claude Code plugin marketplace.

## Plugins

### project-tracker

Skills for planning a website project and keeping track of what Claude is doing and where the project stands.

| Skill | What it does | Writes |
|-------|--------------|--------|
| `/project-tracker:plan` | Turns a project description into tasks with IDs, priorities, dependencies, and checkable "done when" conditions | `PROJECT-PLAN.md` |
| `/project-tracker:todo` | Audits the site's code (placeholders, missing content and media, broken links, menus, best practices) and reports the status of each plan task | `SITE-TODO.md` |
| `/project-tracker:status` | Quick read-only briefing: progress, last session, what's in progress, blockers, and what's next | nothing |
| `/project-tracker:next` | Picks the next unblocked task, announces it, does it, checks it, and logs it | code, `PROJECT-LOG.md` |
| `/project-tracker:log` | Records what Claude did this session | `PROJECT-LOG.md` |
| `/project-tracker:decision` | Records why a choice was made, with the alternatives that were considered | `DECISIONS.md` |

**Typical flow**

1. `/project-tracker:plan <your project description>`
2. `/project-tracker:next` to work through the tasks one at a time.
3. `/project-tracker:todo` whenever you want a full audit and a progress report.
4. `/project-tracker:status` at the start of each new session to pick up where you left off.

## Install

```
/plugin marketplace add MatthewM987/claude-skills-marketplace
/plugin install project-tracker@moloney-claude-tools
```
