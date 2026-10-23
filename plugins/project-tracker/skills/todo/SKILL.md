---
name: todo
description: Audit a website project and write SITE-TODO.md, a launch-readiness to-do list. Covers unfilled placeholders, pages with missing content, missing images or videos, broken links, navigation menu problems, and best-practice issues. If PROJECT-PLAN.md exists (made by the plan skill), it also checks each planned task against the code and reports its status. Use when the user asks what is left to do on the site, whether the site is ready to launch, for a status update or progress report, or for an updated to-do list.
---

# Website launch to-do list

Scan the website's source code and write `SITE-TODO.md` at the project root. The file lists everything that still has to be handled before the site is ready to launch. Rebuild the whole file on every run so it matches the current state of the code. Items that have been fixed drop off the list.

## 1. Understand the project

- Find out how the site is built: plain HTML, a static site generator (Hugo, Jekyll, Eleventy, Astro), or a framework (React, Next.js, Vue, Svelte). To work this out, read `package.json`, the config files, and the folder layout.
- Find the source files that produce pages, such as `.html`, `.md`, `.jsx`, `.tsx`, `.vue`, `.svelte`, `.astro`, and template files. Also find the stylesheets, scripts, and asset folders.
- Skip folders that hold dependencies or build output: `node_modules`, `.git`, `dist`, `build`, `.next`, `out`, `public/build`, and `vendor`.
- If an old `SITE-TODO.md` exists, read it first. Carry over any notes the user added by hand under a `## Notes` heading. Also note each plan task's status from last time, so you can report what changed.
- If `PROJECT-PLAN.md` exists, read it. Its tasks get checked in step 3. If it doesn't exist, skip step 3 and, in the final report, mention that `/project-tracker:plan` can make one.

## 2. Run the checks

For every issue you find, record the file path and line number in the form `path/to/file.html:42`.

### Placeholders that still need filling
- Template variables that were never replaced, such as `{{ ... }}`, `[[...]]`, `%VAR%`, `${...}` inside static text, or `__PLACEHOLDER__`.
- Filler text, such as "lorem ipsum", "TBD", "TODO", "FIXME", "XXX", "coming soon", "your text here", "insert ... here", "sample text", "example.com", "John Doe", "Company Name", and "123 Main St".
- Fake contact details, such as `555-` phone numbers, `email@example.com`, `test@`, and `info@yourdomain`.
- Default text that came with a starter or theme, such as "My Website", "Welcome to React", or the framework's demo content.
- Placeholder copyright years or names in footers.

### Pages with missing information
- Pages with an empty or missing `<title>` or meta description, or one copied unchanged from another page.
- Pages without an `<h1>`, and pages with empty headings, paragraphs, or sections.
- Pages that have very little real content, such as only a heading or only filler.
- Contact, About, Privacy, and Terms pages that are linked but missing or empty.
- Forms that have no `action` or submit handler, and inputs that have no `<label>`.
- No `404` page, or no favicon.

### Missing images and videos
- `src`, `srcset`, `poster`, and CSS `url(...)` references that point at files that don't exist in the project.
- Image services used as placeholders, such as `placeholder.com`, `placehold.co`, `via.placeholder`, `picsum.photos`, `dummyimage`, and `unsplash.it`.
- `<img>` tags with an empty `src`, and video or iframe embeds with empty or placeholder sources.
- Images with a missing or empty `alt` attribute. An empty `alt` is fine for decorative images, so flag it for review.
- Images bigger than about 500 KB, which slow the page down.

### Broken links
- **Internal links:** Check that each `href` points to an existing page, file, or route. Check that each `#anchor` matches an `id` on the target page.
- **External links:** If the network is available, check each unique URL with a quick request, for example `curl -sI -L -o /dev/null -w "%{http_code}" --max-time 10 <url>`. Flag any link that returns 4xx, 5xx, or times out. If the network isn't available, list the external links as "not checked."
- Links that go nowhere, such as `href="#"`, an empty `href`, and `javascript:void(0)`.
- `mailto:` and `tel:` links that contain placeholder details.

### Menu functionality
- Every link in the navigation, header, and footer goes to a page that exists.
- Each menu is the same across pages, or comes from one shared component.
- A mobile menu exists. If there is a toggle (hamburger) button, check that its script exists and is connected. Look at the click handler, the class it toggles, and the CSS for the open state. Check that the button has `aria-expanded` and `aria-controls` and an accessible label.
- Dropdowns or submenus can be reached with the keyboard as well as by hovering.
- The current page is marked in the menu, for example with `aria-current="page"` or an active class.

### Best practices
- **SEO:** Look for `lang` on `<html>`, `<meta name="viewport">`, `<meta charset>`, canonical tags, Open Graph and Twitter tags, `robots.txt`, and `sitemap.xml`.
- **Accessibility:** Look for alt text, labels on form fields, a sensible heading order, buttons used for actions and links used for navigation, focus styles that were not removed, and color contrast that looks too low.
- **Performance:** Look for images without `width` and `height`, offscreen images without `loading="lazy"`, scripts that block page rendering, and very large files.
- **Security:** Look for `target="_blank"` links without `rel="noopener"`, `http://` resources loaded on an `https://` site, and API keys or secrets in the client-side code.
- **Code quality:** Look for leftover `console.log` or `debugger` lines, large commented-out blocks, inline styles that should live in CSS, and duplicate `id`s.
- **Launch basics:** Look for analytics or a cookie notice if the site needs them, a favicon and app icons, and links in the footer to the legal pages.

## 3. Check progress against the plan

Skip this step if there is no `PROJECT-PLAN.md`.

Check every task in the plan that isn't struck through. Compare its **Done when** condition with the actual code, and give it one status:

- **Done:** every part of the Done when condition is met in the code.
- **In progress:** some of the work exists but not all of it. Say what's missing.
- **Not started:** none of the work is in the code yet.
- **Blocked:** a task listed in its `Depends on` isn't done yet.
- **Needs owner:** the task is marked `(owner)` and isn't done yet. These usually can't be checked in code.
- **Can't verify:** the condition can't be checked from the code alone, for example "the domain is bought" or "the client approved the design." Say what the user should confirm.

Rules:
- Decide based on the code, not on any checkboxes the user ticked by hand. If a task is ticked in `PROJECT-PLAN.md` but the code doesn't meet its condition, mark it **In progress** or **Not started** and point out the mismatch.
- Give evidence for every status: the files or lines that meet the condition, or what's missing. Keep it to one line.
- Connect the plan to the audit. If an issue from step 2 is part of a plan task, mention the task ID with the issue, for example `**[Broken link]** ... (P-004)`. A task with Critical issues in its area can't be **Done**.
- Don't edit `PROJECT-PLAN.md`. The status report goes in `SITE-TODO.md` only.

## 4. Write SITE-TODO.md

Use this structure. Leave out any section that has no items, and say in the summary that it passed. Leave out both plan sections if there is no plan.

```markdown
# Site To-Do List

_Last updated: YYYY-MM-DD_

## Summary
- **Plan progress:** N of M tasks done (X%) · In progress: N · Not started: N · Blocked: N · Needs owner: N
- **Must-have tasks left before launch:** N
- **Critical:** N · **Important:** N · **Nice to have:** N
- Passed: <the categories that had no issues>

## Plan status

### Changed since last update
- **P-004** Create the Services page: Not started → **Done**

### 1. Setup
| ID | Task | Priority | Status | Evidence |
|----|------|----------|--------|----------|
| P-001 | Set up the project with Vite | Must | ✅ Done | `package.json` has `dev` and `build` scripts |
| P-002 | Configure deployment | Must | 🟡 In progress | `netlify.toml` exists but has no build command |

### 2. Structure and navigation
| ID | Task | Priority | Status | Evidence |
|----|------|----------|--------|----------|
| P-005 | Add a mobile menu | Must | ⛔ Blocked | Waiting on P-003 (shared header) |
| P-006 | Supply the logo (owner) | Must | 👤 Needs owner | `images/logo.png` is still the template logo |

## Critical (blocks launch)
- [ ] **[Broken link]** "Services" in the nav points to `/servces`, which doesn't exist (`index.html:18`)

## Important
- [ ] **[Placeholder]** Lorem ipsum in the hero paragraph (`about.html:34`)

## Nice to have
- [ ] **[Best practice]** 6 images have no `loading="lazy"` (`gallery.html:12-48`)

## Notes
<notes the user added by hand, kept from the previous version>
```

How to assign priority:
- **Critical:** broken links or menu items, missing pages, missing images, forms that don't work, a mobile menu that doesn't work, filler text that visitors can see, and exposed secrets.
- **Important:** missing titles or meta descriptions, missing alt text, placeholder contact details, a missing 404 page or favicon, and SEO basics.
- **Nice to have:** performance tweaks, code cleanup, and small best-practice improvements.

Group repeats into one item. For example, write "12 images have no alt text" and list the locations, rather than writing 12 separate items. Keep each item to one line that says exactly what to fix and where to fix it.

Status icons: ✅ Done · 🟡 In progress · ⬜ Not started · ⛔ Blocked · 👤 Needs owner · ❓ Can't verify. In the "Changed since last update" list, compare with the statuses in the previous `SITE-TODO.md`. Leave the list out on the first run.

## 5. Report back

When you finish, give the user a short status update. Include:
- Plan progress, such as "14 of 32 tasks done (44%)", and which tasks changed status since the last run.
- The number of Must-have tasks left and the number of Critical issues. If both are zero, say the site looks ready to launch.
- The top three things to do next, choosing from Critical issues and unblocked Must tasks.

Point them to `SITE-TODO.md`, and don't repeat the whole list in chat.
