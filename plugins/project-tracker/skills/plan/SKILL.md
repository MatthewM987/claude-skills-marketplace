---
name: plan
description: Turn a website project description into an actionable task list and save it as PROJECT-PLAN.md. Each task gets an ID and a "done when" condition that the todo skill can check against the code. Use when the user gives a project description, brief, or requirements and wants a plan or task list, or wants to update an existing plan.
---

# Project plan from a description

Turn the user's project description into `PROJECT-PLAN.md` at the project root. The file is a list of concrete tasks. The `todo` skill reads it later and checks each task against the code to report progress, so each task must be something that can be verified by looking at the site's files.

## 1. Get the description

- Use the description the user gave with the command or in the conversation.
- If they pointed to a file, such as a brief, `README.md`, or `PROJECT.md`, read it.
- If there is no description at all, ask the user for one. Don't invent a project.
- If the description leaves out something that changes the plan a lot, ask one short round of questions before writing. Examples are which pages the site needs, whether it needs a contact form, a blog, a shop, or user accounts, and what it is built with. For smaller gaps, make a sensible assumption and list it under **Assumptions** in the plan.
- Look at the project folder too. If code already exists, match tasks to the real stack and file layout (for example, name `about.html` rather than "an About page").

## 2. Break it into tasks

Group tasks into these phases, and leave out any phase that has no tasks:

1. **Setup:** the repository, build tool or framework, folder structure, and deployment target.
2. **Structure and navigation:** the pages, routes, shared layout, header, footer, and menus (desktop and mobile).
3. **Content:** the real text, images, videos, and contact details for each page.
4. **Features:** forms, galleries, maps, booking, search, CMS, e-commerce, and anything else the description asks for.
5. **Design and responsiveness:** the styles, branding, and layouts for mobile, tablet, and desktop.
6. **Quality and launch:** SEO tags, accessibility, performance, a 404 page, a favicon, analytics, legal pages, the domain, and hosting.

Rules for each task:
- Start with a verb and make it one concrete piece of work, such as "Build the contact form on `contact.html` that sends to the client's email." Avoid vague tasks like "Do the contact page."
- Keep it small enough to finish in one sitting. Split anything bigger.
- Give it a **Done when** condition that can be checked in the code. Name files, elements, or behavior. For example: "`contact.html` has a form with name, email, and message fields, each with a label, and the form has a working `action` or submit handler."
- Give it a stable ID: `P-001`, `P-002`, and so on, numbered in order through the whole plan.
- Add a priority: **Must** (needed for launch), **Should** (expected but not required to launch), or **Could** (extra).
- If it can't start until another task is done, add `Depends on: P-00X`.
- Mark tasks that only the client or owner can do with `(owner)`. Examples are supplying logos, writing copy, buying the domain, and approving the design.

## 3. Write PROJECT-PLAN.md

Use this structure:

```markdown
# Project Plan: <project name>

_Created: YYYY-MM-DD · Last revised: YYYY-MM-DD_

## Overview
<2-4 sentences restating what the site is, who it's for, and what it must do>

## Assumptions
- <assumptions you made where the description was unclear>

## Tasks

### 1. Setup
- [ ] **P-001** Set up the project with <stack> · _Must_
  - Done when: `package.json` exists with build and dev scripts, and `npm run build` produces output in `dist/`.

### 2. Structure and navigation
- [ ] **P-004** Create the Services page · _Must_ · Depends on: P-003
  - Done when: `services.html` exists, uses the shared header and footer, and is linked from the main menu.

...

## Open questions
- <things the user still has to decide>
```

## 4. Updating an existing plan

If `PROJECT-PLAN.md` already exists and the user gives a new or changed description:
- Keep the existing task IDs. Never renumber them, because `todo` status reports refer to them.
- Give new tasks the next unused number.
- Don't delete tasks that were dropped from the scope. Strike them through and add a reason, for example `~~**P-012** Add a blog~~ (dropped: not in the new brief)`.
- Update the "Last revised" date.

## 5. Report back

Tell the user how many tasks the plan has, broken down by phase and priority, and list any open questions. Point them to `PROJECT-PLAN.md`. Mention that running `/project-tracker:todo` checks the code against this plan and reports the status of each task.
