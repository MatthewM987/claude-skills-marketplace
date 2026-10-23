---
name: decision
description: Record a project decision in DECISIONS.md. Each entry has an ID, the context, the choice made, the alternatives considered, and the consequences, so it's always clear why the project is built the way it is. Use when Claude or the user picks between real alternatives (a framework, library, hosting, structure, or design approach), when the user says "remember that we decided…", or when they ask why something was done a certain way.
---

# Decision record

Keep `DECISIONS.md` at the project root as the record of why the project is built the way it is. Each decision gets a stable ID so the plan, log, and audit can refer to it.

## When to record a decision

Record one when:
- the user asks you to,
- you chose between real alternatives that would be costly to change later, such as a framework, CSS approach, hosting, form service, folder structure, or URL scheme,
- the user made a choice that changes the plan or the scope, or
- an earlier decision is reversed.

Don't record small, easily changed choices, such as the name of a variable or a single color.

If the user asks *why* something was done, look in `DECISIONS.md` first and answer from it. If there's no entry, say so.

## Write the entry

If `DECISIONS.md` doesn't exist, create it with the heading `# Decisions` and the line `_Newest first. IDs never change._`.

Use the next unused ID (`D-001`, `D-002`, …) and put the new entry above the older ones:

```markdown
## D-003: Use Netlify Forms for the contact form

- **Date:** YYYY-MM-DD
- **Status:** Accepted
- **Decided by:** User / Claude (approved by user) / Claude
- **Related tasks:** P-009

**Context:** The site is static and has no backend. The contact form needs to send email to the owner.

**Decision:** Use Netlify Forms, with the `netlify` attribute on the form.

**Alternatives considered**
- Formspree: works with any host, but the free plan has a monthly limit.
- A custom serverless function: more control, but more work to build and maintain.

**Consequences:** The site has to be hosted on Netlify. Moving to another host means redoing the form (P-009).
```

## Changing a decision

Never delete or rewrite an old decision. Add a new decision that replaces it, and change only the old entry's **Status** line to `Superseded by D-00X`.

## Report back

Tell the user in one line which decision was recorded and its ID.
