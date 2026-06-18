# Braid design system: Email platform

## Overview

Platform-specific guide for Braid on **Email**. For shared foundations, see [Braid design system overview](systems.md).

**Themes included in this document:** `seekJobs` (SEEK Jobs).

### Section map

| §   | Topic                      |
| --- | -------------------------- |
| 1   | Visual theme & style       |
| 2   | Colour                     |
| 3   | Typography                 |
| 4   | Layout and space scale     |
| 5   | Iconography                |
| 6   | Components                 |
| 7   | Depth & elevation          |
| 8   | Accessibility              |
| 9   | Custom and bespoke         |
| 10  | Email clients & testing    |
| 11  | Delivery, CNS, and tooling |

---

## 1. Visual theme & style

Shared brand intent for **SEEK Jobs** is in the [design system overview §1](systems.md#1-visual-theme--style).

**On email**, the theme is delivered as **React components** via `@seek/braid-email-ui`, which wraps `@faire/mjml-react` to produce responsive HTML email. **Light and dark mode** tokens are available, but most email clients do not support `prefers-color-scheme` — background colours render in light mode only.

---

## 2. Colour

### Groupings

Colour tokens are organised by **group**. Each group defines where a token applies in the UI.

| Group              | Purpose               |
| ------------------ | --------------------- |
| `color.foreground` | Text, icons           |
| `color.background` | Backgrounds, fills    |
| `border.color`     | Borders               |

### Prominence levels

| Level    |Role                                            |
| -------- | ---------------------------------------------- |
| `soft`   | Soft button backgrounds                        |
| `light`  | Lighter tints for section fills                |
| `(base)` | Default tone for text, backgrounds and borders |

### Naming conventions

- **Colour tokens** are accessed via the `useTokens()` hook.
- **Background** values are plain hex strings.
- **Foreground and border** tokens return `{ light, dark }` objects — `.light` / `.dark` are **color-mode variants** for light vs dark backgrounds, not prominence. Braid components resolve these via `BackgroundLightnessProvider`; pick `.light` or `.dark` explicitly only in custom styles (most email clients render light mode only).

| Access       | Pattern                                      | Example                                       |
| ------------ | -------------------------------------------- | --------------------------------------------- |
| Background   | `useTokens().color.background.{tokenName}`   | `useTokens().color.background.positiveLight`  |
| Foreground   | `useTokens().color.foreground.{tone}.{mode}` | `useTokens().color.foreground.critical.light` |
| Border       | `useTokens().border.color.{tone}.{mode}`     | `useTokens().border.color.formAccent.light`   |

### Key rules

- Use Braid component `tone` props or `useTokens()` for colour — never hardcode hex values.
- There are no interactive tones (`hover`, `active`) — email has no interactive states.

---

## 3. Typography

**Font family:** `SeekSans`, `Arial`, `Tahoma`, `sans-serif`
**Web font:** loaded automatically by `BraidHead` from `https://www.seek.com/static/shared-web/seeksans.css`

#### Heading weight

| Platform | Heading weight         |
| -------- | ---------------------- |
| Email    | strong (700)           |

#### Text weight

| Prop      | Token weight | Font file |
| --------- | ------------ | --------- |
| `regular` | 400          | Regular   |
| `strong`  | 700          | Medium    |

`strong` sets CSS weight 700 but resolves to the **Medium** SeekSans face — same as on web.

### Line height model

| Platform | Model                                                                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Email    | Explicit `lineHeight` in **px** per style, sourced directly from `seekJobs` theme tokens. |

**Links:** `underline` decoration by default, using the `link` foreground token.

---

## 4. Layout and space scale

**Token access:** `useTokens().space.`* for raw values, or `useAtoms({ paddingX: 'small' })` for ergonomic padding and border props. Spacing values are in **px** — see the shared space scale in [§4 of the design system overview](systems.md#4-layout-and-space-scale).

`gutter` is a semantic value for consistent component insets (Card, Button). `xxxxsmall` is not available on email.

### Layout components

Email uses **MJML table-based layout** — there is no `Stack`, `Columns`, `Box`, `Inline`, `Spread`, `Hidden`, or `HiddenVisually` as on web.

| Component   | Purpose                                                                                         |
| ----------- | ----------------------------------------------------------------------------------------------- |
| `PageBlock` | Page-level container; applies horizontal gutters and optional background                        |
| `CardBlock` | Wrapper for one or more `Card` components; manages spacing between cards                        |
| `Card`      | Bordered surface card — must be rendered inside `CardBlock`                                     |
| `Tiles`     | Multi-column layout; collapses to single column on mobile by default (`collapseBelow="tablet"`) |

- **Content width:** Set on the outer MJML shell (e.g. `MjmlBody` width in the template wrapper) — not via `PageBlock`. Theme tokens define `contentWidth` values (e.g. `small` 660px) for reference when configuring the shell.
- `**PageBlock` gutters:** Applies horizontal inset using the `small` space token (`pageBlockGutter`) — not a `width` prop.
- Layout is primarily **single-column**. Use `Tiles` for multi-column — be cautious, as multi-column can break in some email clients.
- Apply all spacing via `paddingBottom` props on components or `useAtoms()` — do not write inline CSS for spacing.

---

## 5. Iconography

Email icons are **limited** compared to web and native. Only the following named icons are available. You can also supply any icon via a custom `url`.

### Available icons

`search` · `visibility` · `location` · `money` · `time` · `company` · `positive` · `rocket`

These are hosted as `.png` images on `seekcdn.com`. Do not invent other names.

### Icon props

| Prop            | Type                                                         | Notes                                                          |
| --------------- | ------------------------------------------------------------ | -------------------------------------------------------------- |
| `name`          | one of the 8 named icons above                               | One of `name` or `url` is required — not both                  |
| `url`           | `string`                                                     | Custom icon URL — use when the icon is not in the named set    |
| `alt`           | `string?`                                                    | Accessible description — provide when the icon conveys meaning |
| `size`          | `'xsmall'` · `'small'` · `'standard'` · `'large'` · `'fill'` | Default `'standard'`. `'fill'` omits explicit width/height     |
| `align`         | `'left'` · `'center'` · `'right'`                            | Default `'center'`                                             |
| `paddingBottom` | `Space`                                                      | Spacing below the icon                                         |

### Inline icons

Pass an `<Icon />` element to the `icon` prop on `Text` or `Button` to render it inline with text.

---

## 6. Components

All components are imported from `@seek/braid-email-ui`. Do not use raw MJML elements for content that Braid components already cover.

### Props reference

This table shows commonly used components and their key props. Do not invent props — see the installed `@seek/braid-email-ui` package for full type definitions.

| Component   | Available properties                                                                                                                                 |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Heading`   | `level`(required: `'1'`–`'4'`) · `weight` · `align` · `paddingBottom` · `children`                                                                   |
| `Text`      | `size` · `tone` · `weight` · `align` · `icon` · `paddingBottom` · `children`                                                                         |
| `Strong`    | `children`                                                                                                                                           |
| `TextLink`  | `href`(required) · `weight` · `allowDeepLink` · `children` — must be nested inside `Text` or `Heading`                                               |
| `Button`    | `href`(required) · `size` · `tone` · `variant` · `align` · `icon` · `iconPosition` · `allowDeepLink` · `paddingBottom` · `children`                  |
| `Badge`     | `tone` · `weight` · `paddingBottom` · `children`                                                                                                     |
| `Divider`   | `weight` · `paddingBottom`                                                                                                                           |
| `Card`      | `children` — must be rendered inside `CardBlock`. Inter-card spacing comes from `CardBlock`, not `Card`                                              |
| `CardBlock` | `paddingBottom` · `children` — wraps one or more `Card` components; controls spacing between cards                                                   |
| `PageBlock` | `background` · `backgroundPadding` · `paddingBottom` · `children` — `background` and `backgroundPadding` must be used together or omitted            |
| `List`      | `type` · `size` · `tone` · `weight` · `space` · `paddingBottom` · `children` — `ListItem` spacing is controlled by `space`, not on `ListItem` itself |
| `ListItem`  | `children` — must be rendered inside `List`                                                                                                          |
| `Logo`      | `brand`(required) · `alt`(required) · `href` · `align` · `allowDeepLink` · `paddingBottom`                                                           |
| `Tiles`     | `columns`(required) · `space`(required) · `collapseBelow` · `paddingBottom` · `children`                                                             |
| `Icon`      | see §5                                                                                                                                               |

---

## 7. Depth & elevation

Email clients do **not** reliably support CSS `box-shadow`. There are no shadow tokens in `@seek/braid-email-ui`.

Visual separation is achieved through:

- **Surface colour:** `Card` applies a `surface` background by default.
- **Borders:** apply via `useAtoms({ border: 'neutral' })` or `useAtoms({ borderTop: 'formAccent' })`.
- **Background fills:** use component `tone` props or `BackgroundRenderer` to differentiate sections.

Do not attempt to apply shadow styles manually — they will not render consistently across clients.

---

## 8. Accessibility

Shared Braid accessibility rules and WCAG resources: [design system overview §8](systems.md#8-accessibility).

**On email:**

- Email has no keyboard navigation or interactive focus states — WCAG interactive rules do not apply.
- **Images and icons:** always provide `alt` text when the image or icon conveys meaning. Use `alt=""` for decorative images.
- **Colour contrast:** semantic tokens on `seekJobs` are designed for contrast — verify any custom colour combinations.
- **Link and button text:** make it descriptive — email clients can surface links out of context.

---

## 9. Custom and bespoke

Email templates should use **`@seek/braid-email-ui` components** for all standard patterns. Custom elements are acceptable when Braid does not provide a component — but must still use **theme tokens** via `useTokens()` and `useAtoms()`.

### Allowed custom patterns

- **`Icon` with `url`** — custom icon images hosted on a CDN (§5).
- **`useTokens()` / `useAtoms()`** — bespoke section backgrounds, borders, or spacing outside standard components.
- **`BackgroundRenderer`** — differentiated section fills when layouts cannot be expressed via `PageBlock` or `Card`.

### Do not

- Hardcode hex colours or px spacing — resolve values from `useTokens()` (§2, §4).
- Use raw MJML for content Braid components already cover (§6).
- Apply CSS `box-shadow` — email clients do not support it reliably (§7).
- Embed images — serve from a CDN (§11).

Shared rules: [design system overview §9](systems.md#9-custom-and-bespoke).

---

## 10. Email clients & testing

### Client testing

Email HTML renders differently across clients. Test templates in [Email on Acid](https://www.emailonacid.com/) before release (credentials in the shared Candiman 1Password folder).

After running `nx start storybook`, compiled HTML files are available in `src/stories/` within each package — paste these into Email on Acid for cross-client testing.

### Deep linking (Universal Links)

To support deep linking into the SEEK native app from email, pass `universalLinks={true}` to `BraidHead` and `allowDeepLink={true}` to any `Button` that should deep link. Only enable this when the target URL has confirmed native app support.

### Translations

Email templates use [Vocab](https://github.com/seek-oss/vocab) for localisation. Run `yarn compile-vocab` or `nx start storybook` (which includes the watcher) to generate translation files before developing.

### Creating a new template

Use the Nx generator in VS Code (`nx console` → Generate → `workspace-generator > new-email-template`) or CLI:

```shell
yarn nx g workspace-plugin:new-email-template 'your-template-name' --domain={hirer|candidate}
```

---

## 11. Delivery, CNS, and tooling

The standard email stack at SEEK is [SEEK-Jobs/mjml-react-email-templates](https://github.com/SEEK-Jobs/mjml-react-email-templates) — an internal monorepo that renders React components to MJML (email-safe HTML). `@seek/braid-email-ui` (`packages/braid-email-ui`) is the design-system layer.

**Ownership and support:** Resolve from Backstage — `get-catalog-entity({ name: "braid-email-ui", kind: "component", namespace: "default" })` (and `resource:seek-jobs/mjml-react-email-templates` for the monorepo). Day-to-day help: `#braid-email-support`. Published docs: [https://braid-email.skinfra.xyz/](https://braid-email.skinfra.xyz/)

**How templates reach customers:**

- Templates are React components that compile to MJML → HTML via an **nx** command
- Each template is exported as a standalone function — consumers invoke it to get rendered HTML, then pass it to the **Customer Notification System (CNS)** as the `html` field
- Templates are **registered with CNS** per environment using a stable template ID
- A **Storybook** is generated per template for visual development and review

**Constraints:**

- **Images must be served from a CDN** (e.g. seekcdn.com) — embedded images are not supported
- **Payload size:** keep templates under ~**70kb** pre-enrichment; Gmail truncates above ~**120kb**
- The **Engagement** team recommends this repo for email templating (they do not own the repo)

Raw MJML lacks SEEK patterns; `react-mjml` is less modular and lacks SEEK support. This monorepo provides SEEK specific patterns, Storybook generation, and Vocab integration.

---

### Source of truth

Braid email source: [SEEK-Jobs/mjml-react-email-templates](https://github.com/SEEK-Jobs/mjml-react-email-templates). Verify props and APIs against installed `@seek/braid-email-ui` package types when building beyond the tables above.