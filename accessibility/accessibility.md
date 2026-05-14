_Original created by Richard Simms. Thanks Rich!_

# Accessibility Reference — WCAG AA for SEEK

**Target**: WCAG 2.1 Level AA compliance

## Critical Checks (Must Pass)

### Colour Contrast

| Element                          | Minimum Ratio | How to Check                 |
| -------------------------------- | ------------- | ---------------------------- |
| Normal text (18px or 14px bold)  | 4.5:1         | Contrast checker tool        |
| Large text (≥18px or ≥14px bold) | 3:1           | Contrast checker tool        |
| UI components & graphics         | 3:1           | Buttons, icons, form borders |
| Focus indicators                 | 3:1           | Against adjacent colours     |

**Tools**:

- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [APCA Calculator](https://apcacontrast.com/) (more accurate perceptual contrast)
- Browser DevTools accessibility panel

**Common failures**:

- Placeholder text too light
- Disabled states with insufficient contrast
- Link colour indistinguishable from body text
- Icons without sufficient contrast

---

### Touch Targets

| Requirement             | Minimum Size                         |
| ----------------------- | ------------------------------------ |
| Touch targets (mobile)  | 44×44px                              |
| Click targets (desktop) | 24×24px minimum, 44×44px recommended |
| Spacing between targets | 8px minimum                          |

**Check for**:

- Small icon buttons without padding
- Close buttons in corners
- Checkbox/radio hit areas
- Links in dense text

---

### Keyboard Navigation

| Requirement                        | Implementation                        |
| ---------------------------------- | ------------------------------------- |
| All interactive elements focusable | Tab reaches everything                |
| Logical focus order                | Matches visual order                  |
| Focus visible                      | Clear focus indicator on all elements |
| No keyboard traps                  | Can always Tab out                    |
| Skip links                         | "Skip to content" for long nav        |

**Focus indicator requirements**:

- Visible on all focusable elements
- 3:1 contrast against adjacent colours
- Not relying solely on colour change
- Prefer `focus-visible` over `focus` (keyboard only)

**Code patterns to check**:
jsx
// ✓ Good - focusable with visible focus
Click me

// ✗ Bad - removed focus outline
<button style={{ outline: 'none' }}>Click me

// ✗ Bad - div pretending to be button

Click me

// ✓ Fixed - if div must be used

Click me

---

### Screen Reader Support

| Requirement                 | Implementation                       |
| --------------------------- | ------------------------------------ |
| Images have alt text        | Descriptive or empty for decorative  |
| Icons have accessible names | `aria-label` or visually hidden text |
| Form inputs have labels     | Visible or `aria-label`              |
| Dynamic content announced   | `aria-live` regions                  |
| Headings are hierarchical   | h1 → h2 → h3 (no skipping)           |

**Common fixes**:
jsx
// Icon-only button

// Decorative image

// Informative image

// Form input

// Dynamic status

{statusMessage}

---

### Semantic HTML

| Use                    | Instead of                      |
| ---------------------- | ------------------------------- |
| `<button>`             | `<div onClick>`                 |
| `<a href>`             | `<span onClick>` for navigation |
| `<nav>`                | `<div class="nav">`             |
| `<main>`               | `<div class="main">`            |
| `<header>`, `<footer>` | Generic divs                    |
| `<ul>`, `<ol>`         | Divs for lists                  |
| `<table>`              | Divs for tabular data           |

**Landmarks** should be present:

- `<header>` or `role="banner"`
- `<nav>` or `role="navigation"`
- `<main>` or `role="main"`
- `<footer>` or `role="contentinfo"`

---

### Motion & Animation

| Requirement                      | Implementation                 |
| -------------------------------- | ------------------------------ |
| Respect `prefers-reduced-motion` | Reduce or remove animations    |
| No auto-playing content over 5s  | Provide pause control          |
| No flashing content              | Nothing flashes 3 times/second |

**Code pattern**:
css
/_ Respect user preference _/
@media (prefers-reduced-motion: reduce) {
_, _::before, ::after {
animation-duration: 0.01ms !important;
animation-iteration-count: 1 !important;
transition-duration: 0.01ms !important;
}
}

jsx
// React hook pattern
const prefersReducedMotion = useMediaQuery('(prefers-reduced-motion: reduce)');

<motion.div
animate={{ opacity: 1, y: 0 }}
transition={{ duration: prefersReducedMotion ? 0 : 0.3 }}
/>

---

## Important Checks (Should Pass)

### Forms

| Requirement                     | Implementation                            |
| ------------------------------- | ----------------------------------------- |
| Error messages linked to inputs | `aria-describedby` or `aria-errormessage` |
| Required fields indicated       | Visual + `aria-required`                  |
| Error prevention                | Confirmation for destructive actions      |
| Input purpose identified        | `autocomplete` attributes                 |

**Error pattern**:
jsx
<TextField
label="Email"
tone={hasError ? 'critical' : undefined}
message={hasError ? 'Enter a valid email address' : undefined}
/>

---

### Content

| Requirement             | Implementation      |
| ----------------------- | ------------------- |
| Language declared       | `<html lang="en">`  |
| Page titles descriptive | Unique per page     |
| Link text meaningful    | Not "click here"    |
| Tables have headers     | `<th>` with `scope` |

---

### Visual Design

| Requirement               | Implementation              |
| ------------------------- | --------------------------- |
| Colour not only indicator | Add icons, text, patterns   |
| Text resizable to 200%    | No loss of content          |
| Content reflows at 320px  | No horizontal scroll        |
| Spacing adjustable        | Works with user stylesheets |

---

## Testing Approach

### Automated Testing

- axe DevTools browser extension
- Lighthouse accessibility audit
- eslint-plugin-jsx-a11y

### Manual Testing

1. **Keyboard only**: Navigate entire flow with Tab, Enter, Escape, arrows
2. **Screen reader**: Test with VoiceOver (Mac) or NVDA (Windows)
3. **Zoom**: Test at 200% browser zoom
4. **High contrast**: Test with Windows High Contrast Mode
5. **Reduced motion**: Enable reduced motion preference

### SEEK-Specific Considerations

**Candidate flows**:

- Job search must be keyboard navigable
- Application forms must be screen reader compatible
- Job alerts must announce dynamically

**Hirer flows**:

- Candidate review must work with assistive tech
- Data tables must have proper headers
- Bulk actions must be keyboard accessible

**All flows**:

- Error recovery must be accessible
- Success confirmations must be announced
- Loading states must be communicated
