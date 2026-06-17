---

name: SEEK-braid
description:
 Usage guidance for SEEK Braid design system, seekJobs theme, including web, native and email platforms and accessibility, plus Backstage docs and URLs. Use when building or reviewing SEEK UI, choosing tones and components, auditing Braid usage, or fetching live Braid documentation.
type: skill
metadata:
  author: "@SEEK-Jobs/design-systems"
  tags: [braid, design-system, frontend, design, seekJobs, web, native, email, accessibility]

---

# Braid design system

SEEK **Braid** for the SEEK Group: shared foundations, platform guides, accessibility, adoption, and live documentation pointers. **Theme:** `seekJobs` (SEEK Jobs) unless the user specifies otherwise.

Design rules live in `references/`. Ownership, APIs and runbooks come from **Backstage** — see `references/docs-and-urls.md`.

## What to read


| Task / context                | Read (in order)                                  |
| ----------------------------- | ------------------------------------------------ |
| Web UI (**default**)          | `references/systems.md` → `references/web.md`    |
| iOS or Android                | `references/systems.md` → `references/native.md` |
| Email / MJML / CNS            | `references/systems.md` → `references/email.md`  |
| Support, live docs, ownership, catalog | `references/docs-and-urls.md`                    |


- **Default platform:** Web unless the user specifies otherwise.
- **UI work:** shared foundations first (`systems.md`), then **one** platform file — do not load every platform guide.
- **Within each file:** use section maps; load only the sections that match the task.

---

## When to use this skill

- User is **designing or building SEEK UI** with Braid
- SEEK-hosted frontend experiences **should** use Braid (per technology strategy)
- Questions about **tones**, **components**, **layout**, **typography**, **icons**, **elevation**
- User specifies or implies a **platform** (web, iOS, Android, email)
- **Accessibility** review or WCAG questions for Braid UIs
- User needs **live Braid documentation** (Backstage, Playroom, catalog entities)
- User needs **support channels**, ownership, or repo links
- User references **design guidelines** or **seekJobs** theme

## When NOT to use this skill

- **Backend services** — no UI
- **Third-party partner UIs** — partners may use Braid or accessible primitives like Radix UI / React Aria (per frontend experience guidelines)
- **Deep Sku, Gantry, or deploy mechanics** — use Tools plugin **sku**, **gantry**, etc. (see Ecosystem below)
- **Non-SEEK** UI

---

## Ecosystem

Braid sits alongside other SEEK frontend tools. For **deep** guidance on each, use the Tools plugin skill when available:


| Tool                   | Role                                                         |
| ---------------------- | ------------------------------------------------------------ |
| **Sku**                | Bundling, SSR, dev server for Braid web apps                 |
| **Vocab**              | Translated copy inside Braid components                      |
| **Melways**            | Routes traffic to Braid-powered apps; multi-site/locale      |
| **Metropolis**         | Custom and bespoke UI elements shared as packages |
| **Playroom**           | Browser prototyping with real Braid components               |
| **Static Site Deploy** | Sku build output to production                               |


---

## Support

Support channels, ownership, repo links, and Backstage queries — see `references/docs-and-urls.md`.

