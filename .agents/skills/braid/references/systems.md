# Braid design system

## Overview

Braid is the themeable design system for the SEEK Group.

**Themes included in this document:** `seekJobs` (SEEK Jobs).

This document covers **shared foundations** — the cross-platform concepts and rules used across the Braid product suite: visual theme, semantic tones, typography roles, layout principles, iconography, and component composition. It describes *what* is shared and *when* to use it, not platform-specific token names or APIs.

Where platforms differ — token naming, typography values, colour groupings, prominence levels — see **Platform guides**.

### Platform guides

**Platform-specific implementation.** Braid supports **Web**, **Native Apps (iOS and Android)**, and **Email**. Each platform has its own guide for token names, conventions, and platform-only behaviour:

- [Web platform](web.md)
- [Native Apps platforms (iOS and Android)](native.md)
- [Email platform](email.md)

### Section map


| §   | Topic                  |
| --- | ---------------------- |
| 1   | Visual theme & style   |
| 2   | Colour                 |
| 3   | Typography             |
| 4   | Layout and space scale |
| 5   | Iconography            |
| 6   | Components             |
| 7   | Depth & elevation      |
| 8   | Accessibility          |
| 9   | Custom and bespoke     |
| 10  | Do's and Don'ts        |


---

## 1. Visual theme & style

SEEK Jobs is a clean, modern marketplace: **confident magenta** brand accent on a **white** canvas, **SEEK Sans** typography, and a **neutral, content-first** palette where colour signals tone, status, or brand — not decoration. Layout feels **open** and systematic.

- **Spacing:** Components do not own surrounding whitespace — apply gaps, padding, and insets with **layout components** and the shared space scale (§4).
- **Implementation:** Map spacing, colour, type, radii, and depth to **Braid theme tokens or component APIs** — not bespoke styling.
- **Theme:** Use `seekJobs` only — not other SEEK themes.
- **Voice:** Clear, direct, professional, human, optimistic — never gimmicky or ornamental for its own sake.

---

## 2. Colour

Braid provides a shared spectrum of `Tones`, used across the entire component suite on all platforms. These tones correlate with tone of voice. Token names and prominence levels vary by platform — see **Platform guides** in the Overview.

### Semantic tones


| Tone       | Role                                           |
| ---------- | ---------------------------------------------- |
| `critical` | High risk, High urgency, Error, Failed, Delete |
| `caution`  | Low risk, Low urgency, Warning, Upcoming       |
| `positive` | New, Success, Complete                         |
| `info`     | Help, Advice, Updated, Scheduled               |
| `promote`  | Active, Beta, Promotional                      |


### Brand accent tones


| Tone          | Role                                                                                               |
| ------------- | -------------------------------------------------------------------------------------------------- |
| `brandAccent` | Hero actions like starting a key flow, submitting a form or payment (limit 1 per screen)           |
| `formAccent`  | A step down from brandAccent, used to emphasize actions. May be used repeatedly on the same screen |
| `brand`       | Hero banner backgrounds                                                                            |


### Neutral and surface tones


| Tone        | Role                                                                      |
| ----------- | ------------------------------------------------------------------------- |
| `body`      | Default page background                                                   |
| `surface`   | Background for items sitting on the page body (e.g. Card, Dialog, Drawer) |
| `neutral`   | Body copy, Text, Headings, default Buttons, TextLinks                     |
| `secondary` | Optional and supporting text (foreground only)                            |


### Link and focus tones


| Tone          | Role                             |
| ------------- | -------------------------------- |
| `link`        | Standard text links (foreground) |
| `linkVisited` | Visited links (foreground)       |
| `focus`       | Keyboard focus outline (border)  |
| `field`       | Default field outlines (border)  |


### Prominence levels

Each tone may provide prominence levels to adjust its **visual weight**, not semantic meaning. Available levels vary by tone and platform.


| Platform               | Prominence levels                        | Examples                                  |
| ---------------------- | ---------------------------------------- | ----------------------------------------- |
| Web                    | `Soft` → `Light` → `(base)`              | `criticalLight`, `criticalSoft`           |
| Native (iOS & Android) | `Weakest` → `Weak` → `(base)` → `Strong` | `criticalWeakest`, `criticalStrong` (iOS) |


Native platforms use different naming for equivalent levels (e.g. Android `CriticalWeakest` ≈ iOS `criticalWeakest`).

### Key rules

1. Always use semantic tokens. Never use palette values (e.g. grey700).
2. Match the tone to its semantic intent.

---

## 3. Typography

The Braid theme `seekJobs` uses the custom font family `SeekSans`.

### Heading

Note: iOS and Android only expose heading levels `1` and `2`. Heading levels `3` and `4` are web and email only.


| Level | Role                                           |
| ----- | ---------------------------------------------- |
| `1`   | Page titles, hero headings. Limit 1 per screen |
| `2`   | Major section headings                         |
| `3`   | Subsection headings (web only)                 |
| `4`   | Minor headings, card titles (web only)         |


### Text


| Size       | Role                                   |
| ---------- | -------------------------------------- |
| `large`    | Hero copy                              |
| `standard` | Default body copy                      |
| `small`    | Metadata, captions, secondary labels   |
| `xsmall`   | Fine print, legal copy (use sparingly) |


#### Text weight

SeekSans ships **Regular** and **Medium** font files only — there is no separate Bold face. Both `medium` and `strong` resolve to the Medium font file. Use `stong` for emphasis and avoid using `medium`.


| Weight    | Role                                             | Available on       |
| --------- | ------------------------------------------------ | ------------------ |
| `regular` | Default body                                     | Web, native, email |
| `strong`  | Emphasis                                         | Web, native, email |
| `medium`  | **Avoid** — legacy; renders the same as `strong` | Web and iOS only   |


---

## 4. Layout and space scale

Braid provides a standard white space scale across the entire component suite. As much as possible, use this scale rather than custom spacing or arbitrary values. Keep **related content closer** than **unrelated content**.

### Space scale

Note: `xxxxsmall` is available on Native platforms only. `xxxsmall` is available on Native and Email. `gutter` is available on Web, Android, and Email.

**gutter** is a semantic value used to maintain consistent insets across components, e.g. Card, Alert, Button, etc. This value should only be used for aligning to this concept.


| Space       | Role                                                                                                            |
| ----------- | --------------------------------------------------------------------------------------------------------------- |
| `none`      | No spacing                                                                                                      |
| `xxxxsmall` | Finest spacing increment (Native only)                                                                          |
| `xxxsmall`  | Very tight spacing (Native and Email only)                                                                      |
| `xxsmall`   | Tight icon gaps, dense rows                                                                                     |
| `xsmall`    | Compact inline spacing                                                                                          |
| `small`     | Default tight stacks                                                                                            |
| `gutter`    | Horizontal page gutter and consistent component insets, e.g. Card, Alert, Button (Web, Android, and Email only) |
| `medium`    | Standard block gap, card padding                                                                                |
| `large`     | Section separation                                                                                              |
| `xlarge`    | Large gaps, hero spacing                                                                                        |
| `xxlarge`   | Major vertical breaks                                                                                           |
| `xxxlarge`  | Page-level rhythm                                                                                               |
| `custom`    | Variable spacing value (Android only)                                                                           |


### Layout components

Layout spacing is always applied using Braid spacing tokens, not hardcoded values. The core layout patterns — vertical stacking, horizontal arrangement, overlapping layers, and dividers — exist on all platforms, though the component names differ.


| Concept          | Web                  | iOS               | Android                          |
| ---------------- | -------------------- | ----------------- | -------------------------------- |
| Vertical stack   | `Stack`              | `VStack` / Column | Compose `Column` + Braid spacing |
| Horizontal stack | `Columns` + `Column` | `HStack` / `Row`  | Compose `Row` + Braid spacing    |
| Overlay / layer  | `Box`                | `ZStack`          | `Surface` / Compose `Box`        |
| Divider          | `Divider`            | `Divider`         | `Divider`                        |
| Page shell       | `Page`               | —                 | `Page` / `LazyPage`              |


Email uses a different layout paradigm (MJML table-based, `PageBlock` / `Card` / `Tiles`) with no direct equivalents to the components above — see the Email platform guide §4.

### Key rules

- Always use Braid spacing tokens for gaps, padding, and insets — never hardcoded pixel values.
- `Divider` is available on web and native and uses Braid border colour tokens.

---

## 5. Iconography

Web and Native share the same icon suite and art grid. Icon naming follows the same family names across platforms, though the syntax differs. **Email has a limited set of 8 named icons** — see the Email platform guide §5.


| Concept             | Web                 | iOS                  | Android              | Email                     |
| ------------------- | ------------------- | -------------------- | -------------------- | ------------------------- |
| Colour              | `tone` prop         | `foregroundColor`    | `tint`: `IconColor`  | image-based; no tone prop |
| Accessibility label | `title` + `titleId` | `accessibilityLabel` | `contentDescription` | `alt` prop                |
| Icon button         | `ButtonIcon`        | `IconButton`         | `IconButton`         | `Button` with `icon` prop |


- Icons are always sized relative to text — use the icon size that matches the text size in the same context.
- Colour is always applied via tokens, never hardcoded.
- Icons are decorative by default (hidden from assistive technology). Provide a label only when the icon conveys meaning that has no adjacent text label.

---

## 6. Components

Use Braid components for all UI — do not invent custom primitives or props when a Braid component exists.

- Prefer **layout components** for spacing (see §4) rather than ad-hoc padding or margins.
- Use **semantic tones** for meaning — see §2 and platform guides for available tone props per component.
- Keep **primary actions** visually dominant with **formAccent**; secondary actions in **neutral** tone.
- Use **brandAccent** sparingly for hero actions — limit to **one per screen**.
- **Disabled buttons** are not supported — they are not accessible.
- Form controls (`Checkbox`, `RadioGroup`, `TextField`, etc.) must always include a **visible label**.
- Icon-only controls must provide an **accessible name** when the icon conveys an action without adjacent text.
- Interactive targets should meet the **48px minimum** touch target where possible.
- Do not invent props — use only those documented in the **platform guides** or the installed package API.

Component sets and props differ accross platforms, see the relevant **Platform guide**.

---

## 7. Depth & elevation

Braid uses depth sparingly. Most UI is **flat by default** — content sits on the same surface plane without drop shadows.

**When to use elevation**

- **Light elevation** — popovers, menus, and tooltips floating above nearby content
- **Medium / heavy elevation** — dialogs, drawers, sheets, and other prominent overlays

**Shadow character** — When shadows are used, they should feel like a **soft, neutral float** (cool grey at low opacity), not harsh black drops.

**Focus** — Interactive elements must retain visible focus indicators. Do not remove or shrink focus styles.

Use Braid theme tokens or component APIs for depth — never hardcode shadow or elevation values. Token names and values differ by platform; see **Platform guides**.

---

## 8. Accessibility

SEEK targets [WCAG 2.2](https://www.w3.org/TR/WCAG22/) Level AA. Braid components provide a strong accessible baseline on **seekJobs**; **composition, content, state, and product flows** still need accessibility review.

### Braid rules

- Use Braid components — do not invent custom controls when a Braid component fits.
- **Disabled buttons** are not supported (see §6).
- Form controls need a **visible label**; mark optional fields with `secondaryLabel` where the platform supports it.
- **Icon-only controls** need an action-oriented accessible name (see §5).
- Do not use **colour alone** for critical meaning.
- Keep **focus indicators** visible — do not remove or shrink them (see §7).
- **Touch targets:** aim for **48px** on primary controls (§6).
- **Contrast:** semantic tokens on **seekJobs** are designed for contrast; verify custom or non-token colour combinations.
- Respect **heading hierarchy** and platform heading limits (see §3).

Platform-specific accessibility (keyboard, screen readers, APIs): see §8 in **Platform guides**.

---

## 9. Custom and bespoke

### 80/20 rule

About **80%** of UI should be built from Braid components (§6). When a pattern is not covered, custom UI is acceptable if it still follows Braid foundations.

### When custom UI is appropriate

- The interaction or layout is **genuinely unique** to the product and not a candidate for a Braid component
- A Braid component is close but needs **composition** of existing primitives — not a fork with custom styling
- You have confirmed **no existing Braid component** fits (check platform guides and Backstage docs)

### Rules for custom work

- Use **theme tokens** for spacing, colour, typography, radii, and depth — see §2–§7. Never hardcode hex, px, or palette values.
- Prefer **layout components** (§4) and platform primitives (`Box`, `Surface`, etc.) over raw markup.
- Maintain **accessibility** (§8) — custom controls need labels, focus, contrast, and keyboard support where applicable.
- Do not **override** Braid component styles in ways that break focus rings, ARIA, or semantic tones.

### Contribute back

If a custom pattern repeats across teams, **propose it to Braid** rather than maintaining a fork.

Platform-specific constraints for custom UI: see §9 in **Platform guides**.

---

## 10. Do's and Don'ts

**Do**

- Use **Braid components** with the **seekJobs** theme so colours, styles, and type match production.
- Prefer Braid components and **theme tokens** over bespoke styling.
- Use colour **Tones** in line with their **semantic meaning** — see §2.

**Don't**

- Substitute **other SEEK themes** (e.g. Business) or arbitrary colours when this document specifies **SEEK Jobs**.
- Use **colour alone** for critical meaning — pair with relevant **text or icon**.
- Bypass visible **focus styling** on interactive elements.
- Hard-code **spacing**, **colours**, or **styles** outside Braid tokens and component APIs without a strong reason.

For component composition rules (tones on actions, labels, touch targets), see §6. For accessibility, see §8. For custom UI, see §9. For platform-specific styling constraints, see **Platform guides**.