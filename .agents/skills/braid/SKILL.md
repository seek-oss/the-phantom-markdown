---

name: Braid
description:
 Usage guidance for SEEK Braid design system, seekJobs theme, including web, native and email platforms and accessibility, plus Backstage docs and URLs. Use when building or reviewing SEEK UI, choosing tones and components, auditing Braid usage, or fetching live Braid documentation.
type: skill
metadata:
  author: "@SEEK-Jobs/design-systems"
  tags: [braid, design-system, frontend, design, seekJobs, web, native, email, accessibility]

---

# Braid design system

SEEK **Braid** for the SEEK Group: shared foundations, platform guides, accessibility and live documentation pointers. **Theme:** `seekJobs` (SEEK Jobs) unless the user specifies otherwise.

Design rules live in `references/`. Ownership, APIs and runbooks come from **Backstage** — see `references/docs-and-urls.md`.

## What to read

### Always read

1. `references/systems.md` — shared foundations (required for every platform).
2. **One** platform guide — matched to the task. **Do not** load every platform guide.

#### Choosing the platform guide

| Platform           | Read                   | Codebase signals                                                                     |
| ------------------ | ---------------------- | ------------------------------------------------------------------------------------ |
| Web                | `references/web.md`    | `braid-design-system` in `package.json` or imports                                   |
| iOS or Android     | `references/native.md` | Braid Native iOS or Android deps, Swift `Braid` modules, or Compose Braid components |
| Email / MJML / CNS | `references/email.md`  | `@seek/braid-email-ui`, `@faire/mjml-react`, or MJML email templates                 |

- If the platform is not clear from the user's request or codebase signals, **ask the user to clarify** before loading a platform guide.
- **Within each file:** use section maps; load only the sections that match the task.

### Read as needed

| Task / context                                   | Read                          |
| ------------------------------------------------ | ----------------------------- |
| Support, live docs, ownership, Backstage queries | `references/docs-and-urls.md` |

---

## When to use this skill

- User is **designing or building SEEK UI** with Braid
- SEEK hosted frontend experiences **should** use Braid (per technology strategy)
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

| Tool                   | Role                                                    |
| ---------------------- | ------------------------------------------------------- |
| **Sku**                | Bundling, SSR, dev server for Braid web apps            |
| **Vocab**              | Translated copy inside Braid components                 |
| **Melways**            | Routes traffic to Braid-powered apps; multi-site/locale |
| **Metropolis**         | Custom and bespoke UI elements shared as packages       |
| **Playroom**           | Browser prototyping with real Braid components          |
| **Static Site Deploy** | Sku build output to production                          |

