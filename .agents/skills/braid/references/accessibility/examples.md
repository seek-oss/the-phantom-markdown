# Accessibility Review Examples

Use these examples as patterns for concise, actionable findings.

## Blocker Example

### Blocker: Candidate card action is not keyboard reachable

- Area: Keyboard
- Evidence: The candidate card exposes the primary action only through a clickable container.
- Why it matters: Keyboard users cannot reach or operate the action, which blocks completion of the review flow.
- Recommendation: Use a semantic `button` or Braid interactive component for the action. Ensure the Tab order follows the visual/task order and the focus indicator remains visible.
- Manual test: Navigate the card with Tab and Shift+Tab, then activate the action with Enter and Space.

## High Example

### High: Form error is visible but not announced

- Area: Forms
- Evidence: The email field shows an error message after submit, but the input is not associated with the error text.
- Why it matters: Screen reader users may not know what failed or how to fix it.
- Recommendation: Use the Braid field error pattern or link the input to the error text with the supported described-by mechanism. Keep the message specific and corrective.
- Manual test: Submit the form with invalid input while using VoiceOver or NVDA and confirm the error is announced with the field.

## Medium Example

### Medium: Icon-only control has an unclear accessible name

- Area: Screen reader
- Evidence: The icon-only remove action is labelled "Trash".
- Why it matters: The accessible name describes the icon, not the action. Users need to know what will happen.
- Recommendation: Update the `ButtonIcon` content so the injected `aria-label` is action-oriented, such as "Remove candidate".
- Manual test: Move screen reader focus to the control and confirm the announced name describes the action.

## Low Example

### Low: Link opening a new tab is not announced

- Area: Content
- Evidence: The "View profile" link opens a new tab without warning.
- Why it matters: Unexpected context changes can disorient keyboard and screen reader users.
- Recommendation: Include visible or visually hidden text in the accessible name, such as "View profile, opens in a new tab".
- Manual test: Focus the link with a screen reader and confirm the new-tab behaviour is announced before activation.
