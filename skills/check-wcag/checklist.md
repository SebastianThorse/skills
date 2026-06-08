# WCAG review checklist

Use this checklist when running a manual accessibility review.

Scope the review to one app under `server_src/webapps/apps/<AppName>/`. If the app is not specified, ask for it before auditing.

## Semantics

- Is the page or component using the correct native elements?
- Are headings nested logically without skipping levels unnecessarily?
- Are form fields associated with visible labels?
- Are lists, tables, and landmarks announced correctly by structure alone?

## Keyboard

- Can every interactive element be reached and operated with a keyboard?
- Is focus order logical?
- Is focus always visible?
- Can popovers, dialogs, and menus be exited without a mouse?

## Screen reader support

- Does every control have an accessible name?
- For important action buttons such as submit or reset, is extra screen-reader context added with `env-assistive-text` when the visible label alone is not enough?
- Are errors and status messages announced when they appear?
- Is decorative content hidden from assistive tech when appropriate?
- Is dynamic state exposed through native semantics or well-formed ARIA?

## Visual accessibility

- Does text meet contrast requirements against its background?
- If colors come from `--env-*` or `--sol-color*` variables, have you checked the resolved or rendered colors before flagging contrast?
- Is information conveyed by more than color alone?
- Does the UI still work at 200% zoom and under reflow conditions?
- Are interactive targets large enough and clearly identifiable?

## Content and behavior

- Do links describe their destination or purpose?
- Do controls avoid unexpected changes on focus or input?
- Are instructions present before the user makes an error?
- Does motion, autoplay, or timing create an accessibility problem?
