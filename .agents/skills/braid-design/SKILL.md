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

SEEK **Braid** for the SEEK Group: shared design foundations, platform guides, accessibility, adoption, and live documentation pointers. **Theme:** `seekJobs` (SEEK Jobs) unless the user specifies otherwise.

This skill replaces the AI Toolkit **SEEK-braid** placeholder — design rules live in **references/** below; volatile facts (ownership, APIs, runbooks) come from **Backstage** via `references/docs-and-urls.md`.

**References** (read based on task — do not load everything by default):

| File | When to read |
| --- | --- |
| `references/systems.md` | Shared foundations: tones, typography, layout, components, cross-platform rules |
| `references/web.md` | **Default platform** — React web, vanilla-extract, responsive behaviour |
| `references/native.md` | iOS and Android (Braid Native) |
| `references/email.md` | Transactional email (MJML, components, CNS delivery) |
| `references/docs-and-urls.md` | Canonical URLs, Backstage MCP queries, live doc fallbacks |
| `references/governance-and-adoption.md` | Audits, 80/20 rule, compliance signals |
| `references/strategy-and-vision.md` | Adoption, OKRs, contribution model, "should we use Braid?" |
| `references/accessibility/accessibility.md` | Quick WCAG AA reference |
| `references/accessibility/reference.md` | Full WCAG checklist |
| `references/accessibility/review.md` | Structured accessibility review workflow |
| `references/accessibility/examples.md` | Review finding examples |

---

## When to use this skill

- User is **designing or building SEEK UI** with Braid
- User is building a **React web app** at SEEK and needs accessible, brand-consistent UI
- SEEK-hosted frontend experiences **should** use Braid (per technology strategy)
- Questions about **tones**, **components**, **layout**, **typography**, **icons**, **elevation**
- User specifies or implies a **platform** (web, iOS, Android, email)
- **Accessibility** review or WCAG questions for Braid UIs
- **Adoption, audit, or strategy** questions about Braid at SEEK
- User needs **live Braid documentation** (Backstage, Playroom, catalog entities)
- User references **phantom markdown** or **seekJobs** theme

## When NOT to use this skill

- **Native mobile** — still use this skill's `references/native.md`, not web Braid components
- **Non-React web** — Braid web is React-only
- **Backend services** — no UI
- **Third-party partner UIs** — partners may use Braid or accessible primitives like Radix UI / React Aria (per frontend experience guidelines)
- **Deep Sku, Gantry, or deploy mechanics** — use Tools plugin **sku**, **gantry**, etc. (see Ecosystem below)
- **Machine or project setup** — use `../machine-setup/` or `../new-braid-web-project/`
- **Non-SEEK** UI

---

## Platform routing

**Default:** Unless the user specifies a platform, assume **Web**.

| User context | Read |
| --- | --- |
| Web / React / Sku app | `references/systems.md` then `references/web.md` |
| iOS or Android | `references/systems.md` then `references/native.md` |
| Email / MJML / transactional / CNS | `references/systems.md` then `references/email.md` |
| Accessibility review | `references/accessibility/review.md` (and `examples.md` as needed) |
| Quick a11y check | `references/accessibility/accessibility.md` |
| Adoption / audit / compliance | `references/governance-and-adoption.md` |
| Strategy / OKRs / investment case | `references/strategy-and-vision.md` |
| Live docs, ownership, catalog | `references/docs-and-urls.md` |

Load **only sections** relevant to the task when files are long — use each file's section map.

---

## Progressive loading

1. Start with `references/systems.md` Overview and the section(s) that match the task.
2. Load **one** platform guide if implementation detail is needed.
3. Load accessibility references when the task is review or WCAG-related — not for every UI question.
4. Load governance, strategy, or docs-and-urls only when the question is adoption, audit, or live documentation — not for routine component work.

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
