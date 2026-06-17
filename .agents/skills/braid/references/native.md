# Braid design system: Native Apps platforms (iOS and Android)

## Overview

Platform-specific guide for Braid on **Native Apps (iOS and Android)**. For shared foundations, see [Braid design system overview](systems.md).

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
| 10  | Haptics                |


---

## 1. Visual theme & style

Shared brand intent for **SEEK Jobs** is in the [design system overview §1](systems.md#1-visual-theme--style).

**On native (iOS and Android)**, the **seekJobs** theme resolves to platform semantic tokens. **Light and dark mode** adapt automatically — no conditional colour logic in app code.

---

## 2. Colour

### Groupings

Colour tokens are organised by **group**. Each group defines where a token applies in the UI.


| Group     | Role                                   |
| --------- | -------------------------------------- |
| `Surface` | Page/screen backgrounds, cards, sheets |
| `Fill`    | Buttons, badges, form fields            |
| `Border`  | Dividers, input outlines               |
| `Text`    | Typography colour                      |
| `Icon`    | Icon tints                             |
| `Overlay` | Press/interaction states               |


### Prominence levels


| Level     | Role                                        |
| --------- | ------------------------------------------- |
| `Weakest` | Soft button backgrounds                     |
| `Weak`    | Decorative shapes only and background fills |
| `(base)`  | Badge regular, IconButton soft              |
| `Strong`  | Solid button backgrounds, Badge strong      |


Reserved for shapes and decorative elements; `Weak` is not used by any current production component.

### Naming conventions


| Platform | Pattern                                              | Example                             |
| -------- | ---------------------------------------------------- | ----------------------------------- |
| iOS      | `SemanticColor.{Group}.{tone}{Level}` (camelCase)    | `SemanticColor.Fill.criticalStrong` |
| Android  | `Colors.{Group}.{Tone}{Level}` (PascalCase compound) | `Colors.Fill.CriticalStrong`        |


### Surface context


| Platform | Behaviour                                                              |
| -------- | ---------------------------------------------------------------------- |
| Android  | Text and icon tokens auto-resolve for the current surface              |
| iOS      | Requires explicit `onBrand` and `onStrong` tokens on coloured surfaces |


**Android:** `Text.Primary`, `Icon.Default`, and similar tokens resolve automatically — no separate token needed for brand or strong-coloured backgrounds.

**iOS:** Use `onBrand` tokens (e.g. `Text.onBrandPrimary`) on brand surfaces and `onStrong` tokens (e.g. `Text.onCriticalStrong`) on strong-coloured fills. `Text.primary` on a dark or coloured surface will produce unreadable text.

## 3. Typography

### Font family


| Platform | Font family / typeface                                                      | Weights                                                                   |
| -------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| iOS      | `SEEKSans-Regular` / `SEEKSans-Medium` / `SEEKSans-Bold` (PostScript names) | regular `.regular`, strong `.medium` (~600), headings `.medium`           |
| Android  | `seeksans_regular` / `seeksans_medium` (Bold mapped to medium file)         | regular `Normal`, strong `Bold` (uses medium font asset), headings `Bold` |


**Note:** iOS **strong** text resolves to the Medium weight, not Bold. Android's **Bold** font weight likewise maps to the Medium `.ttf` asset — the font file itself is the cap.

iOS sizes are in **pt**; Android sizes are in **sp**. Typography is fixed on both platforms — there is no breakpoint-based sizing.

#### Heading weight


| Platform | Default heading weight    | "Weak" heading weight                           |
| -------- | ------------------------- | ----------------------------------------------- |
| iOS      | `.medium`                 | no weak variant                                 |
| Android  | `Bold` (medium font file) | no weak variant — `Heading.Weight.Regular` only |


Android line heights follow a consistent **1.5×** ratio.

#### Text weight


| Weight                | iOS                                    | Android                              |
| --------------------- | -------------------------------------- | ------------------------------------ |
| Regular               | `.regular`                             | `FontWeight.Normal`                  |
| Medium (mid-emphasis) | `.medium`                              | —                                    |
| Strong                | `.medium` (medium font file, not Bold) | `FontWeight.Bold` (medium font file) |


### Line height model


| Platform | Model                                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| iOS      | No per-style `lineHeight` in tokens. Global `lineSpacing`: **3pt** applied via `NSParagraphStyle`. Dynamic Type scales via `UIFontMetrics`. |
| Android  | Explicit `lineHeight` in **sp** per style (stored in `SeekJobsTypographySet`). Compose **sp** units scale with system font size preference. |


---

## 4. Layout and space scale

**Token path:** `Spacing.`*. iOS values are in **pt**; Android values are in **dp**.

### Layout components


| Component           | Platform | Purpose                                                                   |
| ------------------- | -------- | ------------------------------------------------------------------------- |
| `VStack` / `Column` | iOS      | Vertical stack with Braid spacing                                         |
| `HStack` / `Row`    | iOS      | Horizontal stack with Braid spacing                                       |
| `ZStack`            | iOS      | Overlapping layers with configurable alignment                            |
| `Spacer`            | iOS      | Flexible space that expands to fill available room in a stack             |
| `EdgeInsets`        | iOS      | Padding insets built from Braid spacing tokens                            |
| `Page` / `LazyPage` | Android  | Scrollable page scaffold with header/footer slots and gutters             |
| `Surface`           | Android  | Themed background container with colour propagation and optional border   |
| `BraidScaffold`     | Android  | App scaffold wrapping toolbar, bottom nav, FAB, and snackbar in a Surface |


- Native apps don't use breakpoint tokens — adapt layout via stacks, scroll containers, and sheets; text scales via Dynamic Type / system font preferences.
- iOS layout is spacing-first: Braid provides token-aware overloads for native `VStack`, `HStack`, `LazyVStack`, `LazyHStack`, `Grid`, and `EdgeInsets` rather than replacing them with custom layout types.
- Android's `Surface` is the closest native equivalent to web's `Box` — it handles background colour, shape, and surface context propagation for nested colour tokens.
- `BraidScaffold` and `Page` / `LazyPage` are Android-only — iOS app-level chrome is handled outside Braid.
- There are no native equivalents for `Inline`, `Tiles`, `Spread`, `ContentBlock`, `PageBlock`, `Hidden`, or `HiddenVisually`.

---

## 5. Iconography

### Naming conventions


| Platform | Pattern                                       | Example              |
| -------- | --------------------------------------------- | -------------------- |
| iOS      | `BraidIconAsset.{name}` enum case (camelCase) | `BraidIconAsset.add` |
| Android  | `Icons.{name}` (camelCase)                    | `Icons.add`          |


### Available icons

Only the icon family names below exist — do not invent names. Apply the platform syntax from **Naming conventions** above (e.g. Add → `BraidIconAsset.add`, `Icons.add`).

On iOS, family names map to enum cases (e.g. `arrowUp`, `arrowDown`) — not a single `Arrow` component with a `direction` prop as on web. Android also exposes `Icons.back` (not in the shared family list above).

AI · Add · Arrow · Attachment · Bluetooth · Bold · Bookmark · BulletList · Career · Category · Caution · Checklist · Chevron · Clear · Company · Compose · Copy · CoverLetter · CreditCard · Critical · Date · Delete · Desktop · Disallow · Document · DocumentBroken · Download · Edit · Education · Enlarge · Experience · Filter · Flag · Gift · Globe · Grid · Hash · Heart · Help · History · Home · Image · ImageBroken · Info · Invoice · Italic · Language · Licence · Link · LinkBroken · Location · Mail · Message · Microphone · Minus · Mobile · Money · NewWindow · Note · Notification · NumberedList · Overflow · People · PersonAdd · PersonVerified · Phone · PhotoAdd · PlatformAndroid · PlatformApple · Positive · Print · Profile · Promote · QR · Recommended · Redo · Refresh · Resume · Rocket · Search · Security · Send · Sent · Sentiment · Settings · Share · Skills · SocialFacebook · SocialGitHub · SocialInstagram · SocialLinkedIn · SocialMedium · SocialTiktok · SocialX · SocialYouTube · Sort · Star · Statistics · SubCategory · Tag · Thumb · Tick · Time · Tip · Title · Undo · Upload · Video · Visibility · WorkExperience · ZoomIn · ZoomOut

### Icon props

All icons share these props:


| Prop                                        | iOS                     | Android             | Notes                                                                                   |
| ------------------------------------------- | ----------------------- | ------------------- | --------------------------------------------------------------------------------------- |
| `asset`                                     | `BraidIconAsset.{name}` | `Icons.{name}`      | Required — see Available icons                                                          |
| `size`                                      | `.standard`, `.small`   | `Standard`, `Small` | Standalone only — do not set when icon is inline with text (inherits size from context) |
| `foregroundColor` / `tint`                  | `SemanticColor.Icon.`*  | `IconColor.*`       | Token-based colour only — overrides inherited text tone                                 |
| `accessibilityLabel` / `contentDescription` | `String?`               | `String?`           | Accessible label — provide only when icon conveys meaning without adjacent text         |


### Variant props (select icons only)


| Icon                                                             | Extra prop  | Type                                    | Default     |
| ---------------------------------------------------------------- | ----------- | --------------------------------------- | ----------- |
| Arrow                                                            | `direction` | `'up'`, `'down'`, `'left'`, `'right'`   | `'up'`      |
| Chevron                                                          | `direction` | `'up'`, `'down'`, `'left'`, `'right'`   | `'down'`    |
| Thumb                                                            | `direction` | `'up'`, `'down'`                        | `'up'`      |
| Sentiment                                                        | `feeling`   | `'positive'`, `'negative'`, `'neutral'` | `'neutral'` |
| Visibility                                                       | `hidden`    | `boolean`                               | `false`     |
| Bookmark, Career, Company, Enlarge, Heart, People, Profile, Star | `active`    | `boolean`                               | `false`     |


---

## 6. Components

### Props reference

This table shows commonly used components and their key props by platform. Do not invent props — see the installed Braid package for full type definitions.


| iOS                   | iOS properties                                                                                                        | Android               | Android properties                                                                                                                 |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `Button`              | `text` · `icon` · `variant` · `size` · `tone` · `bleed` · `isInline` · `numberOfLines`                                | `Button`              | `text` · `onClick` · `variant` · `size` · `tone` · `icon` · `iconPosition` · `isBleeding` · `testTag`                              |
| `IconButton`          | `icon` · `variant` · `size` · `tone` · `bleed` · `accessibilityLabel`                                                 | `IconButton`          | `icon` · `contentDescription` · `onClick` · `tone` · `variant` · `size` · `isBleeding` · `testTag`                                 |
| `Card`                | `padding` · `isSelected`                                                                                              | `Card`                | `onClick` · `padding` · `testTag` · `content`                                                                                      |
| `Label`               | `text` · `typography` · `foregroundColor` · `textAlignment` · `numberOfLines`                                         | `Heading`             | `text` · `level` · `weight` · `textColor` · `textAlign` · `minLines` · `maxLines`                                                  |
| `Label`               | `text` · `typography` · `foregroundColor` · `textAlignment` · `numberOfLines`                                         | `Text`                | `text` · `typography` · `textColor` · `textAlign` · `minLines` · `maxLines` · `startIcon` · `startIconTint`                        |
| `Label`               | markdown / attributed strings on `Label` or SwiftUI `Text`                                                            | `TextWithLinks`       | `textWithLinks` · `typography` · `linkWeight` · `textColor` · `onLinkClicked`                                                      |
| `ListItem`            | `title` · `subtitle` · `icon` · `placeholder` · `indentationLevel` · `isReadOnly` · `isWithDivider` · `accessoryView` | `BraidListItem`       | `title` · `subtitle` · `icon` · `onClick` · `divider` · `indentationLevel` · `accessoryView` · `testTag`                           |
| `Badge`               | `title` · `tone` · `weight`                                                                                           | `Badge`               | `text` · `tone` · `weight` · `testTag`                                                                                             |
| `Divider`             | `width` · `indentationLevel` · `dividerColor`                                                                         | `Divider`             | `style` · `color`                                                                                                                  |
| `TextField`           | `label` · `secondaryLabel` · `message` · `tone` · `value` · `placeholder` · `icon` · `isEnabled`                      | `TextField`           | `value` · `label` · `secondaryLabel` · `placeholder` · `message` · `tone` · `enabled` · `onValueChanged` · `startIcon` · `testTag` |
| `MultiSelectListItem` | `title` · `subtitle` · `icon` · `isSelected` · `indentationLevel` · `isWithDivider`                                   | `MultiSelectListItem` | `title` · `subtitle` · `isSelected` · `onClick` · `icon` · `divider` · `indentationLevel` · `testTag`                              |


On iOS, use `Label` with `typography` `.heading1` or `.heading2` for headings.

---

## 7. Depth & elevation

Native platforms do **not** expose a three-tier shadow token scale. Depth is achieved through flat surfaces, borders, modal presentation, and component-specific styling — not `vars.shadow`-style theme tokens.

### Surfaces

- Default UI is **flat** — do not add arbitrary shadows to cards, lists, or page content
- **Android:** `Card` sets `elevation = 0.dp`; depth comes from surface colour and border tokens
- **iOS:** `Card` relies on surface colour and borders, not theme shadow tokens

### Overlays

Sheets and modals use **platform presentation** (scrim/backdrop, layered view hierarchy) rather than shared shadow tokens.

- **iOS:** `Sheet` / `SheetViewController` presentation
- **Android:** sheet and dialog composables with scrim overlays

Some components apply **local shadow styling** (e.g. Android `Menu` uses a component-level `dropShadow`) — do not generalise these into custom elevation on other components.

### Focus

Field focus uses **border colour tokens**, not a global focus ring.


| State           | iOS                                   | Android                        |
| --------------- | ------------------------------------- | ------------------------------ |
| Default border  | `SemanticColor.Border.neutralStrong`  | `Colors.Border.NeutralRegular` |
| Focused border  | `SemanticColor.Border.formAccent`     | `Colors.Border.FormAccent`     |
| Critical border | `SemanticColor.Border.criticalStrong` | `Colors.Border.CriticalStrong` |


**Android** focused fields also use a slightly thicker border (`Border.Default.width + 1.dp`). Focused field labels use `Colors.Text.FormAccent`.

Do not remove focus or border styling from form fields.

### Navigation chrome (iOS)

Tab bar shadow is configured via `UITabBar.applyBraidAppearance` using `Surface.neutral` — app chrome only, not content elevation.

---

## 8. Accessibility

Shared Braid accessibility rules and WCAG resources: [design system overview §8](systems.md#8-accessibility).

**On native:**

- **Labels:** use §5 props (`accessibilityLabel`, `contentDescription`); names must describe the action (overview §8).
- **Text scaling:** see §3 (Dynamic Type, **sp**).
- **Haptics** (§10) reinforce interaction; they do not replace visible feedback or accessible names.

---

## 9. Custom and bespoke

Native apps should use **Braid Native components** first. Custom UI must still use **semantic tokens** and platform layout patterns — not hardcoded colours or arbitrary spacing.

### When building custom views

- **iOS:** compose with `VStack`, `HStack`, `Label`, and `SemanticColor` / `Spacing` tokens.
- **Android:** compose with Compose `Column`/`Row`, Braid `Surface`, and `Colors.*` / `Spacing.*` tokens.
- Apply **surface context** rules from §2 — especially `onBrand` / `onStrong` on iOS.

### Do not

- Import web `braid-design-system` components into native apps.
- Add arbitrary shadows or elevation to cards and lists (§7).
- Skip accessible names on custom icon-only or interactive controls (§8).

Shared rules: [design system overview §9](systems.md#9-custom-and-bespoke).

---

## 10. Haptics

Haptics are **native-only** — not used on web. **iOS** provides built-in haptics on several Braid components. **Android** does not expose a Braid haptic API; press feedback is visual via themed **Material ripple** (`LocalRippleConfiguration`).

### Principles

- Use haptics to confirm taps, selection changes, or meaningful outcomes (success, warning, error).
- Avoid overusing haptics — too much tactile feedback reduces impact.
- Haptics respect system settings and device capability automatically.

### Built-in component haptics (iOS)

These fire automatically — do not duplicate them in custom action handlers.


| Component                                                    | Haptic                | Notes                                           |
| ------------------------------------------------------------ | --------------------- | ----------------------------------------------- |
| `Button`                                                     | `impactLight` on tap  | Set `isHapticsEnabled = false` to opt out       |
| `Button`, `Card`, tab bar button, `Notice` actions (SwiftUI) | Light impact on press | Via component `ButtonStyle` / `sensoryFeedback` |
| `SingleSelectListItem`, `MultiSelectListItem`                | `selection`           | On tap                                          |
| `TabBar`                                                     | `impactLight`         | When selecting a different tab                  |
| `TextEditor`                                                 | `notifyWarning`       | When typing further past the character limit    |


### Android

Do not add haptic props to Braid Android components or call vibration APIs through Braid. Rely on themed ripple for press feedback.

---

### Source of truth

Braid native source: [SEEK-Jobs/braid-ios](https://github.com/SEEK-Jobs/braid-ios) · [SEEK-Jobs/braid-android](https://github.com/SEEK-Jobs/braid-android). Verify props and APIs against installed Braid package types when building beyond the tables above.