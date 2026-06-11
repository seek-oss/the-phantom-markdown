# Accessibility Reference - WCAG 2.2 AA at SEEK

SEEK targets WCAG 2.2 Level AA accessibility across product experiences. This reference covers critical, actionable checks for Content, Design, and Development teams.

Role tags indicate primary responsibility: `CONTENT`, `DESIGN`, `DEVELOPMENT`.

Braid is built with accessibility in mind. Using Braid components gets teams a long way, but implementation, composition, content, state management, and product flow decisions still need accessibility review.

## Colour Contrast

| Element | Minimum Ratio | Role |
| --- | --- | --- |
| Normal text | 4.5:1 | `DESIGN` |
| Large text | 3:1 | `DESIGN` |
| UI components and graphics | 3:1 | `DESIGN` |
| Focus indicators | 3:1 against adjacent colours | `DESIGN` |

WCAG large text means at least 18pt regular or 14pt bold, roughly 24 CSS px regular or 18.66 CSS px bold.

Common failures:

- Placeholder text too light.
- Disabled states below 3:1.
- Links indistinguishable from body text.
- Icons or form borders with insufficient contrast.

Tools:

- WebAIM Contrast Checker.
- APCA Calculator for perceptual contrast exploration.
- Browser DevTools accessibility panel.
- Figma plugins such as Able, Contrast, and A11y - Color Contrast Checker.

Braid note: Braid components meet contrast requirements across supported themes. Verify contrast when using custom, brand, or non-standard colour combinations outside of Braid tokens.

## Touch And Click Targets

| Context | Requirement | Role |
| --- | --- | --- |
| Mobile touch targets | 44x44 CSS px recommended; 24x24 CSS px minimum per WCAG 2.2 AA | `DESIGN` |
| Desktop click targets | 24x24 CSS px minimum; 44x44 CSS px recommended | `DESIGN` |
| Spacing between targets | A 24 CSS px circle on one target should not overlap adjacent targets | `DESIGN` |

Check for:

- Small icon-only buttons without padding.
- Close or dismiss buttons in corners.
- Checkbox and radio hit areas.
- Tappable links in dense text.
- Adjacent controls that are easy to activate accidentally.

Braid note: Standard Braid interactive controls target generous touch sizes. Smaller variants should still meet WCAG 2.2 AA minimum requirements.

## Keyboard Navigation

`DESIGN` `DEVELOPMENT`

| Requirement | Implementation |
| --- | --- |
| All interactive elements focusable | Tab reaches every button, link, input, and control |
| Logical focus order | Matches the visual and task order |
| Focus always visible | Clear focus indicator on all interactive elements |
| No keyboard traps | User can always Tab out; Escape closes dismissible overlays |
| Skip links | "Skip to content" visible on focus for repeated navigation |
| No positive tabindex | Never use `tabindex` values above 0 |
| Hover content keyboard accessible | Content appearing on hover must also appear on focus and be dismissible |

Focus indicator requirements:

- Visible on all focusable elements.
- 3:1 contrast against adjacent colours.
- Does not rely only on colour change.
- Uses `focus-visible` for keyboard focus where appropriate.
- Never remove `outline` without providing an accessible replacement.

WCAG 2.2 focus not obscured: when an element receives keyboard focus, it must not be completely hidden by sticky headers, sticky footers, or overlapping content.

Braid note: When implementing modals, dialogs, drawers, or custom overlays, ensure focus moves into the surface on open, is managed while open, and returns to the trigger element on close.

## Screen Reader Support

`CONTENT` `DESIGN` `DEVELOPMENT`

| Element | Requirement |
| --- | --- |
| Informative images | Concise, contextual alt text |
| Decorative images | `alt=""` so assistive technology ignores them |
| Complex images | Adjacent explanation or long description |
| Icon-only buttons | Accessible name describing the action |
| Form inputs | Visible label or accessible name; never placeholder text alone |
| Dynamic content | `aria-live` or equivalent pattern for relevant results, alerts, and status updates |
| Heading hierarchy | Sequential structure that reflects the page outline |
| Landmarks | `<header>`, `<nav>`, `<main>`, and `<footer>` where applicable |

Annotate in handoff:

- Accessible names for icon buttons.
- Alt text for informative images.
- Decorative image treatment.
- Live regions for dynamic content.
- Heading levels for content sections.

## Semantic HTML

`DEVELOPMENT`

| Use | Instead of |
| --- | --- |
| `<button>` | `<div onClick>` or `<span onClick>` |
| `<a href>` | `<span onClick>` for navigation |
| `<nav>`, `<main>`, `<header>`, `<footer>` | Generic wrappers |
| `<ul>` or `<ol>` | Divs for lists of related items |
| `<table>` with `<th scope>` | Divs for tabular data |

If a custom element is unavoidable, add the correct role, keyboard behaviour, focus management, and accessible name. Do not add ARIA to compensate for avoidable non-semantic markup.

## Forms

`CONTENT` `DESIGN` `DEVELOPMENT`

| Requirement | Role |
| --- | --- |
| Visible, persistent labels on all inputs; never placeholder-only | `CONTENT` `DESIGN` |
| Required fields indicated visually and programmatically | `DESIGN` `DEVELOPMENT` |
| Error messages describe what went wrong and how to fix it | `CONTENT` |
| Errors linked to inputs via `aria-describedby` or component-supported equivalent | `DEVELOPMENT` |
| `autocomplete` attributes on common fields | `DEVELOPMENT` |
| Confirmation or undo for destructive or irreversible actions | `DESIGN` |
| No redundant re-entry of information in multi-step flows | `DESIGN` `DEVELOPMENT` |

WCAG 2.2 redundant entry: if information has already been provided earlier in a process, auto-populate it or make it available for selection rather than requiring users to re-enter it.

Braid note: Form fields are considered required unless marked optional. Use `secondaryLabel` to indicate optional fields. Avoid disabling submit buttons; keep them active and surface errors on submission to help screen reader and keyboard users.

## Controls, Links, Buttons, And Interactive Components

`CONTENT` `DESIGN` `DEVELOPMENT`

- Use descriptive labels. Avoid "Click here", "Read more", or generic "Submit" when the action can be specific.
- Follow label in name. The accessible name must include the visible label text.
- Make links distinguishable from surrounding body text without relying on colour alone.
- Warn users when a link opens a new tab or window, either visibly or with visually hidden text in the accessible name.
- Ensure hover, focus, active, selected, disabled, and error states are distinguishable.

Braid note: When using icons alongside visible text, ensure the accessible name includes the visible text. For icon-only controls, the accessible name must describe the action. `ButtonIcon` content is injected into the `aria-label`, so its content should be action-oriented, such as "Close dialog" or "Remove candidate".

## Touch And Pointer Interactions

`DESIGN` `DEVELOPMENT`

- Dragging alternatives: provide non-drag alternatives for any drag interaction, such as up/down buttons to reorder or a text input for slider values.
- Activate on release: controls should activate on pointer or touch release, not press, so users can cancel accidental actions by moving away before releasing.
- Avoid path-based gestures as the only way to complete a task.

## Content

`CONTENT` `DESIGN`

- Do not rely on sensory characteristics alone. Avoid instructions like "click the green button on the right"; use the control name or label.
- Use plain language where possible. Provide a simplified summary for complex or technical content.
- Define jargon and abbreviations on first use, such as "Applicant Tracking System (ATS)".
- Prefer left-aligned body text.
- Aim for readable line lengths, generally around 45 to 75 characters.

## Images And Data Visualisation

`CONTENT` `DESIGN` `DEVELOPMENT`

- Informative images need concise, contextual alt text covering what users need to know.
- Decorative images must have `alt=""` and should be annotated clearly in handoff.
- Complex images need adjacent explanation or a long description.
- Data visualisations must not rely on colour alone.
- Provide a text summary and structured data table alternative for data visualisations.
- Avoid images of text. Use real, CSS-styled text that can be resized and read by screen readers.
- Decorative icons use `aria-hidden="true"` or the Braid-supported equivalent.

## Motion And Animation

`DESIGN` `DEVELOPMENT`

- Respect `prefers-reduced-motion`; remove or significantly reduce non-essential motion when detected.
- Nothing should flash more than 3 times per second.
- Auto-playing content longer than 3 seconds must not play audio.
- Moving, blinking, scrolling, or auto-updating content longer than 5 seconds needs a visible pause, stop, or hide control.
- Background video and slideshows must have a pause control.

Braid note: Braid components with built-in animation should respect reduced motion. For custom motion, scope reduced-motion handling to the relevant component or animation system rather than adding broad global overrides by default.

## Responsive Design And Zoom

`DESIGN` `DEVELOPMENT`

| Requirement | Detail |
| --- | --- |
| Reflow at 320 CSS px | No horizontal scrolling at narrow viewport widths |
| Portrait and landscape | Do not lock orientation |
| Text resize to 200% | Content remains readable and usable |
| Text spacing | Content does not break when users override line height, letter spacing, word spacing, or paragraph spacing |

For web products, test at 400% zoom where possible for robust low-vision support.

## Consistency

`DESIGN` `DEVELOPMENT`

- Consistent identification: components with the same function must have the same label across pages and views.
- Consistent help: help mechanisms such as contact information, chat, and FAQs must appear in the same relative location across pages.

## SEEK-Specific Considerations

Candidate flows:

- Job search results must be fully keyboard navigable.
- Application forms require full screen reader compatibility.
- Job alert confirmations must be announced through an accessible status pattern.
- Card focus order should be annotated in handoff.

Hirer flows:

- Candidate review tables must use column and row headers with `scope` where appropriate.
- Bulk actions must be keyboard accessible with explicit focus and selection states.
- Complex data views must not rely on visual position alone to convey meaning.

All flows:

- Error recovery must be accessible end-to-end.
- Success confirmations must be visible and announced when they affect the task.
- Loading and processing states must communicate progress to screen reader users when relevant.

## Testing

Automated testing:

- axe DevTools browser extension.
- Lighthouse accessibility audit.
- `eslint-plugin-jsx-a11y` in development workflow.

Automated tools catch only a portion of accessibility issues. Manual testing is essential.

Manual testing:

- Keyboard only: navigate the entire flow with Tab, Shift+Tab, Enter, Space, arrow keys, and Escape.
- Screen reader: test with VoiceOver on macOS/iOS, NVDA on Windows, or TalkBack on Android.
- Zoom: test at 200% minimum; 400% recommended for web products.
- High contrast: test with Windows High Contrast Mode or macOS Increase Contrast.
- Reduced motion: enable reduced motion in system preferences and verify animations are removed or reduced.
- Touch targets: verify target sizes on real devices where possible.

## References

- WCAG 2.2 Quick Reference: https://www.w3.org/WAI/WCAG22/quickref/
- Braid Design System: https://seek-oss.github.io/braid-design-system/
- WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
- Inclusive Components: https://inclusive-components.design/
