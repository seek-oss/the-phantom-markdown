---
name: SEEK-braid
description: >-
  SEEK Braid design system — seekJobs design language (web, native, email), accessibility,
  adoption and governance, plus Backstage docs and URLs. Use when building or reviewing SEEK UI,
  choosing tones and components, auditing Braid usage, or fetching live Braid documentation.
type: skill
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - design-system
    - design
    - web
    - native
    - email
    - accessibility
    - seekJobs
    - seek-internal
---
# Braid design system

SEEK **Braid** for the SEEK Group: shared foundations, platform guides, accessibility, adoption, and live documentation pointers. **Theme:** `seekJobs` (SEEK Jobs) unless the user specifies otherwise.

Design rules live in `references/`; volatile facts (ownership, APIs, runbooks) come from **Backstage** — see `references/docs-and-urls.md`.

## What to read

| Task / context | Read (in order) |
| --- | --- |
| Web UI (**default**) | `references/systems.md` → `references/web.md` |
| iOS or Android | `references/systems.md` → `references/native.md` |
| Email / MJML / CNS | `references/systems.md` → `references/email.md` |
| Adoption / audit / compliance | `references/governance-and-adoption.md` |
| Live docs, ownership, catalog | `references/docs-and-urls.md` |

- **Default platform:** Web unless the user specifies otherwise.
- **UI work:** shared foundations first (`systems.md`), then **one** platform file — do not load every platform guide.
- **Within each file:** use section maps; load only the sections that match the task.

---

## When to use this skill

- User is **designing or building SEEK UI** with Braid
- User is building a **React web app** at SEEK and needs accessible, brand-consistent UI
- SEEK-hosted frontend experiences **should** use Braid (per technology strategy)
- Questions about **tones**, **components**, **layout**, **typography**, **icons**, **elevation**
- User specifies or implies a **platform** (web, iOS, Android, email)
- **Accessibility** review or WCAG questions for Braid UIs
- **Adoption or audit** questions about Braid at SEEK
- User needs **live Braid documentation** (Backstage, Playroom, catalog entities)
- User references **phantom markdown** or **seekJobs** theme

## When NOT to use this skill

- **Native apps** — use `references/native.md`, not web `braid-design-system` components
- **Non-React web** — Braid web is React-only
- **Backend services** — no UI
- **Third-party partner UIs** — partners may use Braid or accessible primitives like Radix UI / React Aria (per frontend experience guidelines)
- **Deep Sku, Gantry, or deploy mechanics** — use Tools plugin **sku**, **gantry**, etc. (see Ecosystem below)
- **Machine or project setup** — use `../machine-setup/` or `../new-braid-web-project/`
- **Non-SEEK** UI

---

## Ecosystem

Braid sits alongside other SEEK frontend tools. For **deep** guidance on each, use the Tools plugin skill when available:

| Tool | Role |
| --- | --- |
| **Sku** | Bundling, SSR, dev server for Braid web apps |
| **Vocab** | Translated copy inside Braid components |
| **Melways** | Routes traffic to Braid-powered apps; multi-site/locale |
| **Metropolis** | Shared Braid UI published as packages across micro-frontends |
| **Playroom** | Browser prototyping with real Braid components |
| **Static Site Deploy** | Sku build output to production |

---

## Support

- `#braid-support` — Web implementation help
- `#braid-design-support` — UX and patterns
- `#braid-announcements` — Releases and changes
- `#braid-email-support` — Email templates (see `references/email.md`)
- `#experience-platforms` — Broader frontend questions

**Ownership and repo links** — resolve from Backstage (`references/docs-and-urls.md`):

```
get-catalog-entity({ name: "braid", kind: "system", namespace: "default" })
get-catalog-entity({ name: "braid-ios", kind: "component", namespace: "default" })
get-catalog-entity({ name: "braid-email-ui", kind: "component", namespace: "default" })
```

---

## Related skills

- `../machine-setup/SKILL.md` — Part 1: prepare Mac for Braid prototyping
- `../new-braid-web-project/SKILL.md` — Part 2: scaffold Sku + Braid web project
