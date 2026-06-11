# Design system strategy and vision

Use this when advising on **design-system adoption**, **audits**, **roadmaps**, or **OKRs** — not for day-to-day component API questions (those belong in Backstage TechDocs).

Braid sits in SEEK's **Frontend Platforms (Mobile & Web)** domain. It is the shared layer for consistent, accessible customer UI across the SEEK Group.

## Strategic themes

- **Consistency at scale**: Braid reduces the cost of per-team visual and interaction decisions. Teams should be **consumers** of primitives first, not parallel design systems.
- **Multi-brand by design**: Theming is first-class — one component tree can serve SEEK AU, SEEK NZ, JobsDB, and related brands. That is a deliberate platform choice.
- **Accessibility as default**: SEEK's technology strategy expects **AA**-level accessibility for customer-facing web. Braid is the standard way to meet that without every team re-solving the same problems.

## Catalog signals (Backstage)

These values come from the Braid **System** entity in Backstage; re-fetch if you need the latest:

- **Lifecycle**: `supported` — actively maintained, not deprecated or experimental
- **Business criticality**: `Medium`
- **Resilience / criticality**: `businessOperational` — failures would affect business operations

## Contribution model

Teams can propose **new components or patterns** to Braid. The Braid maintainers (see the Braid system in Backstage) own quality, consistency, and accessibility; contributions expand what the system can cover without every product forking the same widget.

## Native alignment

**Braid Native** shares tokens and principles with web Braid so mobile and web stay visually aligned. Strategy conversations should treat web + native as one design system family, with different implementation surfaces.

## "Should we invest in Braid?"

For SEEK customer-facing React web, the default answer is **yes** — it is the organisational standard and the path to accessible, on-brand UI without reinventing primitives. Nuance lives in product-specific constraints; validate those in TechDocs and with `#braid-support` / `#braid-design-support`.
