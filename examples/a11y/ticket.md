# Example: try the a11y guide on this ticket

**Ticket (task):** Add a "Copy link" icon button to each release in the changelog page.

**What a good run looks like**

- The button is a real `<button>` with an accessible name ("Copy link to v2.3.0"), not an icon alone.
- It is reachable with Tab, works with Enter and Space, and shows a visible focus ring.
- "Link copied" is announced to screen readers (a polite live region), not only shown as a toast.
- The icon meets 3:1 contrast in both themes.
- The checklist answers each item; `pa11y-ci` passes, or each issue it reports is fixed or explained.
