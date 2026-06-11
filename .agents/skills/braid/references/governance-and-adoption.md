# Governance and adoption guidance

Use this when advising on Braid adoption, auditing usage, or assessing design system health.

## 80/20 rule

Rough guidance at SEEK: about **80%** of UI needs should be met by Braid components. If a team builds many custom components, review whether Braid already covers the use case or whether a **contribution back to Braid** is warranted.

## Audit pattern

To see how much a codebase uses Braid, grep for imports such as:

- `from 'braid-design-system'`
- `@braid-design-system`

Absence of these in a React frontend at SEEK is a **red flag** (subject to product-specific exceptions).

## Compliance signals

- **`BraidProvider` missing** at the app root → theming and tokens will not work as intended
- **Hardcoded pixels or hex colours** instead of Braid tokens → not using the design system correctly
- **Custom CSS overriding** Braid components → accessibility may be broken
- **Raw HTML** (`<div>`, `<p>`, `<button>`) where Braid primitives (`Box`, `Text`, `Button`) exist → inconsistent and potentially inaccessible

## Accessibility

Braid's built-in **AA** compliance only holds if components are used as intended. Customisation that overrides ARIA, focus rings, or colour contrast is **non-compliant**.

## Official checklist

Fetch current criteria from Backstage (wording and checks change over time):

```
backstage-search({ query: "Braid checklist compliance adoption", types: ["techdocs"] })
```
