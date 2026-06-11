---
name: seek-accessibility-review
description: Review SEEK product UI, React code, Braid usage, content, and designs for WCAG 2.2 accessibility risks. Use when reviewing accessibility, a11y, WCAG, keyboard navigation, screen readers, forms, Braid UI, SEEK candidate flows, SEEK hirer flows, or accessible content.
---

# SEEK Accessibility Review

Use this skill to review SEEK product experiences against WCAG 2.2 Level AA expectations, with SEEK and Braid-specific guidance.

## Review Workflow

1. Identify the surface being reviewed: code, design, content, or end-to-end flow.
2. Load [reference.md](reference.md) for full checklist details when doing a substantive review.
3. Prioritise blockers first: keyboard access, focus visibility, semantic HTML, form labels and errors, accessible names, screen reader announcements, and error recovery.
4. Prefer Braid components and established Braid patterns before recommending custom ARIA or custom controls.
5. Verify how components are combined. Braid handles many accessibility requirements, but composition, content, state management, and dynamic behaviour remain product responsibilities.
6. Include manual test steps for issues automated tools cannot prove.

## SEEK And Braid Rules

- Keep WCAG 2.2 Level AA as the baseline.
- Use Braid components where possible; do not recommend custom elements if a Braid component fits.
- Do not remove, shrink, or obscure Braid focus styles.
- Do not recommend disabled Braid buttons. Keep actions available where possible and surface validation errors on submission.
- For Braid forms, fields are considered required unless marked optional. Use `secondaryLabel` to indicate optional fields.
- For icon-only controls, require an accessible name. `ButtonIcon` content is injected into the `aria-label`; ensure that content describes the action.
- For images, alt text should be concise and contextual. Complex images need adjacent explanation or a long description.
- For dynamic content, success, error, loading, and status changes must be visible and announced to assistive technology when they affect the user's task.

## Output Format

Lead with findings, ordered by severity. Use this structure for each issue:

```markdown
### [Severity] Short Finding Title

- Area: Keyboard | Screen reader | Forms | Semantics | Content | Motion | Responsive | Braid usage
- Evidence: file, component, screen, or flow being reviewed
- Why it matters: user impact and WCAG/Braid concern
- Recommendation: concrete fix
- Manual test: focused verification step
```

Severity levels:

- `Blocker`: prevents completion for keyboard, screen reader, low vision, or other assistive technology users.
- `High`: significant WCAG 2.2 AA risk or common user failure.
- `Medium`: accessibility issue with a clear workaround or limited scope.
- `Low`: polish, clarity, consistency, or preventive improvement.

If no issues are found, say so clearly and list any residual manual testing still needed.

## Reference Files

- [reference.md](reference.md): Full WCAG 2.2 AA checklist for content, design, and development.
- [examples.md](examples.md): Example review findings and phrasing.
