_Original created by Michelle Lock. Thanks Michelle!_

# Braid Native guidelines [PLACEHOLDER FILE]

Use this file when designing in iOS and Android Native Apps.
These rules apply to all generated output.

---

## Output framing and native platform simulation

All generated output must include an additional UI frame that simulates a native mobile app environment.

These rules apply to **every screen in the prototype**, not only top‑level flows or entry points.

All output must visually follow native iOS and Android mobile design patterns and avoid web‑specific UI conventions.

### Default state

- Start in:
  - iOS
  - Light mode
- Use this state as the primary reference for layout, hierarchy, and spacing

### Device frames and controls

- Always include a mobile device frame
- Always display controls to switch between:
  - iOS and Android
  - Light and dark mode
- These controls must be visible at all times and apply to the currently viewed screen
- Do not flatten, merge, or hide the device frame or controls

### Native platform guidance

- Follow native mobile platform conventions for:
  - Layout and spacing
  - Navigation patterns
  - System UI placement
- Do not use web‑specific patterns such as:
  - Browser chrome or controls
  - Hover‑dependent interactions
  - Mouse‑based scrollbars
  - Desktop‑only affordances
- Only use platform‑specific components if they align with documented design system guidance

### Status bars and safe areas

- Always include a visible status bar
- Match the status bar to the selected platform:
  - iOS status bar for iOS
  - Android status bar for Android
- Ensure all content respects native safe areas
- Content must not clash with system UI elements

### Display modes

- Support both light and dark mode via a toggle
- Maintain readability, contrast, and hierarchy in both modes
- Do not redesign or re‑layout the UI when switching modes

### Layout consistency

- Maintain consistent core UI across:
  - All screens in the prototype
  - iOS and Android
  - Light and dark mode
- Adjust layout only when required by native platform constraints

### Do not

- Do not use web‑only UI patterns or terminology
- Do not treat device, platform, or display‑mode framing as optional

---

# Design system guidelines

Follow the design system as the source of truth.
The design system refers to **Braid**.
Use documented components, patterns, foundations, and guidance.
If something is unclear or undocumented, do not guess.

---

## Foundations

Use documented design system foundations for:

- Typography
- Spacing and layout
- Component structure
- Accessibility

Do not invent new foundations.
