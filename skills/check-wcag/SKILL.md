---
name: check-wcag
description: Review UI work against WCAG 2.1 AA. Use when asked to evaluate accessibility, keyboard support, focus handling, semantics, contrast, forms, or screen reader behavior.
---

# Check WCAG

Use this skill when reviewing or improving accessibility in this repository.

## Repository context

- This project uses Svelte 5, not SvelteKit.
- Accessibility reviews in this repository are always scoped to one specific app under `server_src/webapps/apps/<AppName>/`, never the entire repository.
- Styles must use Envision CSS variables from `utils/envision.css`.
- Do not hardcode colors, spacing, border radii, or font values unless explicitly asked.
- Reuse the `@outline-focus` mixin from `client_src/sass/abstracts/_mixins.scss` for custom focus-visible styling.
- Prefer semantic HTML first. Add ARIA only when native elements are not enough.
- Theme and color values often come from CSS custom properties such as `--env-*` and `--sol-color*`. Do not treat unresolved variable names as automatic contrast failures.
- This project uses Sitevision's `env-assistive-text` class for screen-reader-only text.

## Review process

1. Confirm the exact app name before starting. If the user did not specify the app, ask which directory under `server_src/webapps/apps/` should be reviewed.
2. Limit all investigation and recommendations to that app's files unless the user explicitly expands the scope.
3. Find the relevant Svelte, JavaScript, Sass, and template files before making recommendations.
4. Check semantic structure first: headings, landmarks, lists, buttons vs links, labels, tables, and form relationships.
5. Check keyboard behavior: tab order, escape routes, focus trapping where relevant, and visible focus states.
6. Check screen reader behavior: accessible names, descriptions, state changes, status/error messaging, and hidden content patterns.
7. Pay extra attention to buttons or controls that trigger meaningful changes such as submit, reset, filtering, or other state updates. Make sure their purpose or changed behavior is communicated for screen reader users, using `env-assistive-text` where appropriate.
8. Check visual accessibility: color contrast, zoom/reflow risks, target size concerns, and non-color cues.
9. Treat CSS custom properties carefully during contrast review. Variables such as `--env-*` and `--sol-color*` may resolve correctly in the real theme even if the raw source does not reveal final colors.
10. Check motion and interaction risks: autoplay, unexpected context changes, hover-only interactions, and timing issues.
11. First complete the audit and present the findings before making code changes.
12. After presenting the findings, ask the user which issues they want to fix. Do not start implementing fixes until the user chooses the findings to address or explicitly asks to fix all of them.
13. When code changes are requested, fix root causes instead of layering ARIA on broken markup.

## WCAG focus areas

Prioritize these criteria unless the task clearly points elsewhere:

- 1.1.1 Non-text Content
- 1.3.1 Info and Relationships
- 1.3.2 Meaningful Sequence
- 1.3.3 Sensory Characteristics
- 1.4.1 Use of Color
- 1.4.3 Contrast (Minimum)
- 1.4.10 Reflow
- 2.1.1 Keyboard
- 2.1.2 No Keyboard Trap
- 2.4.3 Focus Order
- 2.4.4 Link Purpose
- 2.4.7 Focus Visible
- 3.2.1 On Focus
- 3.2.2 On Input
- 3.3.1 Error Identification
- 3.3.2 Labels or Instructions
- 4.1.2 Name, Role, Value
- 4.1.3 Status Messages

## How to report findings

When auditing, use this format:

1. **Issue:** short description
2. **WCAG:** criterion number and name
3. **Why it fails:** concrete explanation tied to the current UI
4. **Fix:** the smallest correct change that solves the problem
5. **Severity:** blocker, serious, moderate, or minor

If no issues are found, say that plainly and list what was checked.

After listing the findings, ask the user which of them they want to fix. If they say to fix all findings, proceed with all of them.

## Repo-specific implementation rules

- For interactive controls, prefer native `<button>`, `<a>`, `<input>`, `<select>`, and `<textarea>` elements over clickable generic elements.
- Decorative or redundant SVG icons should be hidden from assistive tech with `aria-hidden="true"`. Do not hide icons that carry unique meaning on their own.
- If a component needs custom focus styling, use the shared focus mixin rather than ad hoc outlines.
- If a visual fix requires color or spacing changes, use Envision variables instead of raw values.
- For contrast findings, prefer resolved colors or actual rendered output over assumptions based only on variable names.
- When buttons trigger important changes, especially submit or reset behavior, ensure screen-reader-only context is present using Sitevision's `env-assistive-text` class where needed.
- If an icon is the only visible content of a control, usually hide the icon itself and give the control an accessible name with `env-assistive-text` or `aria-label`.
- In Svelte components, keep accessibility logic close to the markup it affects. Do not hide important behavior in vague helper abstractions.

For a reusable audit checklist, see [checklist.md](./checklist.md).
