---
name: SEEK-braid-design
description: >-
  SEEK Braid design language for seekJobs — shared foundations, web, native, and email
  platform guides, and accessibility references. Use when building or reviewing SEEK UI,
  choosing tones, components, layout, or platform-specific Braid implementation. Not the
  Tools plugin braid skill (that covers Sku/Backstage ecosystem); this skill is design rules.
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
# Braid design (phantom markdown)

SEEK **Braid design context** for the SEEK Group: shared foundations plus platform-specific implementation. **Theme:** `seekJobs` (SEEK Jobs) unless the user specifies otherwise.

This skill replaces placeholder braid design content in the AI Toolkit over time. The **Tools plugin `SEEK-braid` skill** covers ecosystem fit (Sku, Backstage, governance); this skill covers **what to build** (tones, components, layout, accessibility).

**References** (read based on task — do not load everything by default):

| File | When to read |
| --- | --- |
| `references/systems.md` | Shared foundations: tones, typography, layout, components, cross-platform rules |
| `references/web.md` | **Default platform** — React web, vanilla-extract, responsive behaviour |
| `references/native.md` | iOS and Android (Braid Native) |
| `references/email.md` | Transactional email (MJML, limited components) |
| `references/accessibility/accessibility.md` | Quick WCAG AA reference |
| `references/accessibility/reference.md` | Full WCAG checklist |
| `references/accessibility/review.md` | Structured accessibility review workflow |
| `references/accessibility/examples.md` | Review finding examples |

Public raw URLs for the same content remain at repo root (`systems.md`, `web/web.md`, etc.) for rules and non-Cursor tools.

---

## When to use this skill

- User is **designing or building SEEK UI** with Braid
- Questions about **tones**, **components**, **layout**, **typography**, **icons**, **elevation**
- User specifies or implies a **platform** (web, iOS, Android, email)
- **Accessibility** review or WCAG questions for Braid UIs
- User references **phantom markdown** or **seekJobs** theme

## When NOT to use this skill

- **Sku, Gantry, deploy, Backstage** stack questions — use Tools plugin skills (`sku`, `gantry`, etc.)
- **Machine or project setup** — use `SEEK-machine-setup` or `SEEK-new-braid-web-project` (`../machine-setup/`, `../new-braid-web-project/`)
- **Non-SEEK** or non-Braid UI

---

## Platform routing

**Default:** Unless the user specifies a platform, assume **Web**.

| User context | Read |
| --- | --- |
| Web / React / Sku app | `references/systems.md` then `references/web.md` |
| iOS or Android | `references/systems.md` then `references/native.md` |
| Email / MJML / transactional | `references/systems.md` then `references/email.md` |
| Accessibility review | `references/accessibility/review.md` (and `examples.md` as needed) |
| Quick a11y check | `references/accessibility/accessibility.md` |

Load **only sections** relevant to the task when files are long — use each file's section map.

---

## Progressive loading

1. Start with `references/systems.md` Overview and the section(s) that match the task.
2. Load **one** platform guide if implementation detail is needed.
3. Load accessibility references when the task is review or WCAG-related — not for every UI question.

---

## Related skills

- `../machine-setup/SKILL.md` — Part 1: prepare Mac for Braid prototyping
- `../new-braid-web-project/SKILL.md` — Part 2: scaffold Sku + Braid web project
