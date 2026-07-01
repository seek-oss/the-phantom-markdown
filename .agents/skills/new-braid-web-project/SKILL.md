---
name: New-braid-web-project
description: >-
  Set up a new Braid web design project from scratch with Sku and braid-design-system.
  Use when the user wants to start a new Braid web prototype, scaffold a designer project,
  or run Part 2 project setup after machine setup is complete.
type: skill
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - sku
    - design
    - prototyping
    - web
    - frontend
    - internal
---
# New Braid web project

Procedural workflow for designers (and others) creating a **new Braid web project** on macOS with Cursor. This is **Part 2: project setup**. Part 1 (machine setup) is a prerequisite.

**References** (read when executing this workflow):

- `references/new-web-project.md` — scaffold Sku project, add Braid, start dev server, connect design context

**Related skill (Part 1):**

- `Machine-setup` — Node, Homebrew, Git, pnpm, Cursor rule, extensions (**run first if prerequisites are missing**). In this repo: `../machine-setup/SKILL.md`

---

## When to use this skill

- User wants to **start a new Braid web prototype** or design project
- User asks to **set up a Braid project**, **create a Sku app with Braid**, or **scaffold a designer project**
- User has finished machine setup and is ready for **Part 2**
- User is a **designer** prototyping in Cursor with Braid

## When NOT to use this skill

- **Native iOS/Android** — use Braid Native, not this web workflow
- **Email templates** — use the email platform guide, not Sku/webpack scaffolding
- **Existing repo** — do not scaffold; help inside the current project instead
- **Backend or infra only** — no UI scaffolding needed

---

## Before you start

Work through `references/new-web-project.md` **step by step** from Step 0. After each step, verify success before continuing. If a step fails, stop and explain what went wrong.

- **Step 0:** Ask for (or confirm) the project name — do not scaffold with a placeholder.
- **Step 1:** Targeted `brew update && brew upgrade pnpm git`, then verify `node`, `pnpm`, and `git`. If prerequisites fail, follow **machine-setup** first (`../machine-setup/SKILL.md` or `Machine-setup`).

---

## Workflow summary (Part 2)

| Step | Action |
| --- | --- |
| 0 | Ask for (or confirm) project name; validate before scaffolding |
| 1 | `brew update && brew upgrade pnpm git`; verify node, pnpm, git |
| 2 | Scaffold with `pnpm dlx @sku-lib/create` (webpack template) |
| 3 | Add `braid-design-system` |
| 4 | Start dev server (`pnpm start`) |
| 5 | Open project in Cursor (`cursor .`) |
| 6 | Load design context via **braid** skill (`../braid/SKILL.md`) or public URLs |

Full commands, verification, and user handoffs: `references/new-web-project.md`.

---

## After setup

Remind the user that when they reopen the project they should run:

```bash
pnpm install && pnpm start
```

For ongoing UI work, use the **braid** skill (`../braid/SKILL.md`) or the public [systems.md](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md) and [web guide](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/web.md).
