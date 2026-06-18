# Braid design system: Web platform

## Overview

Platform-specific guide for Braid on **Web**. For shared foundations, see [Braid design system overview](systems.md).

**Themes included in this document:** `seekJobs` (SEEK Jobs).

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
| 10  | Responsive behavior    |

---

## 1. Visual theme & style

Shared brand intent for **SEEK Jobs** is in the [design system overview §1](systems.md#1-visual-theme--style).

**On web**, the theme is delivered as **React components** and **vanilla-extract** CSS variables (`vars.*`).

**Reference:** Playroom `.snippets.tsx` templates in `node_modules/braid-design-system` for composition patterns.

---

## 2. Colour

### Groupings

Colour tokens are organised by **group**. Each group defines where a token applies in the UI.

| Group             | Purpose                                    |
| ----------------- | ------------------------------------------ |
| `foregroundColor` | Text, Icons                             |
| `backgroundColor` | Backgrounds, fills (e.g. Button, Alert) |
| `borderColor`     | Borders                                    |

### Prominence levels

| Level    | Role                                                 |
| -------- | ---------------------------------------------------- |
| `light`  | Lighter tints for section fills                      |
| `(base)` | Default tone for text, backgrounds and borders       |

### Interactive tones

| Level    | Role                             |
| -------- | -------------------------------- |
| `soft`   | Soft button backgrounds          |
| `hover`  | Hover state button backgrounds   |
| `active` | Pressed state button backgrounds |

### Naming conventions

Colour tokens are accessed via the [vars](https://seek-oss.github.io/braid-design-system/css/vars/) object. Prefix with `vars.`, then the group name, then the tone value (camelCase).

| Platform | Pattern                      | Example                              |
| -------- | ---------------------------- | ------------------------------------ |
| Web      | `vars.{group}.{tone}{Level}` | `vars.backgroundColor.positiveLight` |

---

## 3. Typography

**Font family:** `SeekSans`, `"SeekSans Fallback"`, `Arial`, `Tahoma`, `sans-serif`  
**Web font URL (reference):** [https://www.seek.com/static/shared-web/seeksans.css](https://www.seek.com/static/shared-web/seeksans.css)
**After building any page or component**, ensure `<link rel="stylesheet" href="https://www.seek.com/static/shared-web/seeksans.css">` is present in the `<head>` in `src/render.tsx`

Sizes are **px**; **line gap** is the Capsize line-gap token (implementation computes final line height and cap trims).

#### Heading weight

| Platform | Default heading weight | "Weak" heading weight                    |
| -------- | ---------------------- | ---------------------------------------- |
| Web      | medium (600)           | regular (400) — via `weight="weak"` prop |

#### Text weight

| Prop      | CSS weight | Font file | Notes                                             |
| --------- | ---------- | --------- | ------------------------------------------------- |
| `regular` | 400        | Regular   | Default body                                      |
| `strong`  | 700        | Medium    | Use for emphasis                                  |
| `medium`  | 600        | Medium    | **Avoid** — legacy; renders the same as `strong`  |

SeekSans web fonts map CSS weights 500–700 to the same Medium `@font-face` — see [seeksans.css](https://www.seek.com/static/shared-web/seeksans.css).

### Line height model

| Platform | Model                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web      | **Capsize:** `precomputeValues(fontSize, lineGap, fontMetrics)` → computed `lineHeight` + `capsizeTrims`. Negative cap trims remove excess whitespace above/below glyphs. |

**Links:** System default is **underlined** text links using link/visited foreground tokens.

**Responsive:** Heading and text sizes step up at the **tablet** breakpoint — see §10.

---

## 4. Layout and space scale

**Token path:** `vars.space.*`. Spacing values are in **px**.

**Base grid:** **4px**. All spacing tokens are multiples of the grid (`grid: 4`). Do not hard-code spacing outside this grid without a strong reason.

**Content max widths (px):** `xsmall` 400 · `small` 660 · `medium` 940 · `large` 1280 — use for readable copy columns and centered layouts.

### Layout components

| Component            | Purpose                                                                       |
| -------------------- | ----------------------------------------------------------------------------- |
| `Stack`              | Vertical rhythm with uniform spacing between children                         |
| `Columns` + `Column` | Horizontal multi-column layout with responsive widths, collapse, and ordering |
| `Inline`             | Flowing horizontal content that wraps across lines                            |
| `Tiles`              | Wraps children in a fixed column count, left-to-right then top-to-bottom      |
| `Spread`             | Distributes children with equal spacing (horizontal or vertical)              |
| `Box`                | Lowest-level primitive for applying theme-based styles to a single element    |
| `Bleed`              | Lets content extend into surrounding layout using negative margins            |
| `ContentBlock`       | Constrains content to a maximum width                                         |
| `PageBlock`          | Page-level container with max width and responsive gutters                    |
| `Page`               | Top-level page shell that controls footer placement                           |
| `Hidden`             | Hides children at specified breakpoints or on print                           |
| `HiddenVisually`     | Hides content visually while keeping it accessible to screen readers          |

- Web is the only platform with responsive layout primitives (`Columns` collapse, `Hidden` breakpoints, `Tiles` column count per breakpoint).
- `Bleed` on web is a standalone layout component. On native it exists only as a prop on specific components.
- `ContentBlock` and `PageBlock` are web-only — native platforms handle max-width constraints at the OS/app shell level.

---

## 5. Iconography

### Naming conventions

| Platform | Pattern                      | Example   |
| -------- | ---------------------------- | --------- |
| Web      | `Icon{Name}` React component | `IconAdd` |

### Available icons

All icons are named exports from `braid-design-system`. Only the names below exist — do not invent names. For a full visual reference see [Iconography](https://seek-oss.github.io/braid-design-system/foundations/iconography) in the docs.

`IconAI` · `IconAdd` · `IconArrow` · `IconAttachment` · `IconBluetooth` · `IconBold` · `IconBookmark` · `IconBulletList` · `IconCareer` · `IconCategory` · `IconCaution` · `IconChecklist` · `IconChevron` · `IconClear` · `IconCompany` · `IconCompose` · `IconCopy` · `IconCoverLetter` · `IconCreditCard` · `IconCritical` · `IconDate` · `IconDelete` · `IconDesktop` · `IconDisallow` · `IconDocument` · `IconDocumentBroken` · `IconDownload` · `IconEdit` · `IconEducation` · `IconEnlarge` · `IconExperience` · `IconFilter` · `IconFlag` · `IconGift` · `IconGlobe` · `IconGrid` · `IconHash` · `IconHeart` · `IconHelp` · `IconHistory` · `IconHome` · `IconImage` · `IconImageBroken` · `IconInfo` · `IconInvoice` · `IconItalic` · `IconLanguage` · `IconLicence` · `IconLink` · `IconLinkBroken` · `IconLocation` · `IconMail` · `IconMessage` · `IconMicrophone` · `IconMinus` · `IconMobile` · `IconMoney` · `IconNewWindow` · `IconNote` · `IconNotification` · `IconNumberedList` · `IconOverflow` · `IconPeople` · `IconPersonAdd` · `IconPersonVerified` · `IconPhone` · `IconPhotoAdd` · `IconPlatformAndroid` · `IconPlatformApple` · `IconPositive` · `IconPrint` · `IconProfile` · `IconPromote` · `IconQR` · `IconRecommended` · `IconRedo` · `IconRefresh` · `IconResume` · `IconRocket` · `IconSearch` · `IconSecurity` · `IconSend` · `IconSent` · `IconSentiment` · `IconSettings` · `IconShare` · `IconSkills` · `IconSocialFacebook` · `IconSocialGitHub` · `IconSocialInstagram` · `IconSocialLinkedIn` · `IconSocialMedium` · `IconSocialTiktok` · `IconSocialX` · `IconSocialYouTube` · `IconSort` · `IconStar` · `IconStatistics` · `IconSubCategory` · `IconTag` · `IconThumb` · `IconTick` · `IconTime` · `IconTip` · `IconTitle` · `IconUndo` · `IconUpload` · `IconVideo` · `IconVisibility` · `IconWorkExperience` · `IconZoomIn` · `IconZoomOut`

### Icon props

All icons share these props:

| Prop                | Type                                                                                                                                  | Notes                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `size`              | `'large'`, `'standard'`, `'small'`, `'xsmall'`, `'fill'`                                                                              | Standalone only — do not set when icon is inside `Text` or `Heading` (inherits size from context) |
| `tone`              | `'neutral'`, `'secondary'`, `'critical'`, `'caution'`, `'positive'`, `'info'`, `'promote'`, `'brandAccent'`, `'formAccent'`, `'link'` | Overrides inherited text tone                                                                     |
| `alignY`            | `'uppercase'`, `'lowercase'`                                                                                                          | Inline only — adjusts vertical alignment when inside `Text` or `Heading`                          |
| `title` + `titleId` | `string`                                                                                                                              | Accessible label — must provide both or neither                                                   |
| `data`              | `DataAttributeMap`                                                                                                                    | e.g. `{ testid: 'my-icon' }`                                                                      |

### Variant props (select icons only)

| Icon                                                                                                             | Extra prop  | Type                                    | Default     |
| ---------------------------------------------------------------------------------------------------------------- | ----------- | --------------------------------------- | ----------- |
| `IconArrow`                                                                                                      | `direction` | `'up'`, `'down'`, `'left'`, `'right'`   | `'up'`      |
| `IconChevron`                                                                                                    | `direction` | `'up'`, `'down'`, `'left'`, `'right'`   | `'down'`    |
| `IconThumb`                                                                                                      | `direction` | `'up'`, `'down'`                        | `'up'`      |
| `IconSentiment`                                                                                                  | `feeling`   | `'positive'`, `'negative'`, `'neutral'` | `'neutral'` |
| `IconVisibility`                                                                                                 | `hidden`    | `boolean`                               | `false`     |
| `IconBookmark`, `IconCareer`, `IconCompany`, `IconEnlarge`, `IconHeart`, `IconPeople`, `IconProfile`, `IconStar` | `active`    | `boolean`                               | `false`     |

---

## 6. Components

Prefer Braid components and **vars** / atoms over custom CSS. Do not hard-code styles using `style={{ ... }}` unless absolutely necessary — use component props instead.

### Props reference

This table shows commonly used components and their key props. Do not invent props — see the installed `braid-design-system` package for full type definitions.

| Component      | Available properties                                                                                                                   |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `Button`       | `id` · `size` · `tone` · `variant` · `bleed` · `loading` · `type` · `icon` · `iconPosition` · `onClick` · `data` · `children`          |
| `ButtonIcon`   | `id` · `icon`(required) · `label`(required) · `size` · `tone` (`neutral` · `formAccent`) · `variant` (`soft` · `transparent`) · `type` · `bleed` · `tooltipPlacement` · `onClick` · `data` |
| `Card`         | `tone` (`promote` · `formAccent`) · `height` · `component` · `data`                                                                  |
| `Heading`      | `level`(required) · `weight` · `align` · `icon` · `maxLines` · `component` · `data`                                                    |
| `Text`         | `size` · `tone` · `weight` · `align` · `icon` · `maxLines` · `baseline` · `component` · `data`                                         |
| `TextLink`     | `href`(required) · `weight` · `showVisited` · `hitArea` · `icon` · `iconPosition` · `data`                                             |
| `PageBlock`    | `width` · `component` · `data`                                                                                                         |
| `ContentBlock` | `width` · `align` · `data`                                                                                                             |
| `Badge`        | `tone` · `weight` · `bleedY` · `title` · `data`                                                                                        |
| `List`         | `size` · `space` · `tone` · `type` · `icon` · `start` · `data`                                                                         |
| `Divider`      | `weight`                                                                                                                               |

---

## 7. Depth & elevation

**Token path:** `vars.shadow.*`. Shadows use cool grey at low opacity for a soft, neutral float.

| Shadow   | Role                                           |
| -------- | ---------------------------------------------- |
| `small`  | Popovers, menus, tooltips                      |
| `medium` | Dialogs, drawers, and mid-weight overlays      |
| `large`  | Prominent overlays needing strongest elevation |

Apply shadows via `Box` props, atoms, or theme variables — do not hardcode `box-shadow` values.

### Focus

Keyboard focus uses a **6px** ring via the `focusRingSize` token.

- **Colour:** `vars.borderColor.focus` — see [vars](https://seek-oss.github.io/braid-design-system/css/vars/) (`borderColor` group)
- **Utility:** `[outlineStyle](https://seek-oss.github.io/braid-design-system/css/outlineStyle/)` for indirect focus styling in vanilla-extract
- **Components:** set `outline="focus"` on `Box`, or rely on built-in focus styles on interactive components

Do not remove or shrink focus styles for keyboard users. Do not bypass **focus-visible** styling on custom interactive elements.

---

## 8. Accessibility

Shared Braid accessibility rules and WCAG resources: [design system overview §8](systems.md#8-accessibility).

**On web:**

- **Keyboard / focus:** Tab order must match visual and task order; use **focus-visible** for keyboard focus. Focus tokens and styling: §7. Manage focus in modals and dialogs (move focus in on open, trap while open, return to trigger on close).
- **`ButtonIcon`:** required `label` is injected into **`aria-label`** — action-oriented text (e.g. "Close dialog"), not icon names.
- **Composition:** prefer `<button>`, `<a href>`, and landmarks (`<main>`, `<nav>`, etc.); use **`HiddenVisually`** (§4) for screen-reader-only text; respect **`prefers-reduced-motion`** for custom animation.

---

## 9. Custom and bespoke

Prefer Braid components and component props over custom CSS. When Braid does not cover a need, build on **`Box`**, **`vars`**, and **atoms** — not raw HTML and inline styles.

### Last resort patterns

- **`Box`** — lowest-level primitive for applying theme tokens to a single element (padding, background, border, outline).
- **`vars.*` and atoms** — use theme variables and vanilla-extract atoms for one-off styling; do not hardcode values.
- **`style={{ ... }}`** — only when component props and atoms cannot express the layout; document why.

### Do not

- Override Braid component CSS to change tones, focus rings, or spacing — compose with Braid components instead.
- Use raw `<div>`, `<button>`, or `<p>` when `Box`, `Button`, or `Text` would work.
- Hardcode `box-shadow`, colours, or spacing outside the token scale (§2, §4, §7).

Shared rules: [design system overview §9](systems.md#9-custom-and-bespoke).

---

## 10. Responsive behavior

**Breakpoints** (`min-width`, from [breakpoints.ts](https://github.com/seek-oss/braid-design-system/blob/master/packages/braid-design-system/src/lib/css/breakpoints.ts)):

| Name        | Min width | Notes                                                 |
| ----------- | --------- | ----------------------------------------------------- |
| **mobile**  | 0         | Default; single-column layouts, smaller heading sizes |
| **tablet**  | 740px     | Larger heading sizes, multi-column layouts            |
| **desktop** | 992px     | Full two- and three-column shells                     |
| **wide**    | 1200px    | Maximum horizontal use                                |

**Typography:** Heading and text **sizes and gaps** are defined separately for **mobile** and **tablet**; from **tablet upward** the tablet values apply unless a component uses custom responsive props.

**Touch targets:** Treat **48px** minimum height as the baseline for **primary** interactive controls (standard button / touchable row).

**Collapsing strategy:** **Stack** on **mobile**; introduce **columns** from **tablet** or **desktop** depending on density. **Hide or move** secondary nav into **drawers, menus, or progressive disclosure** at narrow widths rather than squeezing horizontal nav.

---

### Source of truth

Braid web source: [seek-oss/braid-design-system](https://github.com/seek-oss/braid-design-system). Verify props and APIs against installed `braid-design-system` package types when building beyond the tables above.

