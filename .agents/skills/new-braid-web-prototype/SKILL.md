---
name: new-braid-web-prototype
description: >-
  Scaffold a new Braid web prototype with Sku and braid-design-system on macOS.
  Use when the user wants to start a new Braid web prototype, set up a Braid project,
  create a Sku app with Braid, or run Part 2 project setup after machine setup.
  Do not use for native apps, email templates, existing repos, or backend-only work.
type: skill
compatible_tools: [cursor]
compatibility: >-
  macOS with Homebrew, nvm (Node v22+), pnpm v10+, git, network access, Cursor,
  and permission to run terminal commands. Part 1 machine setup must be complete.
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - sku
    - design
    - prototyping
    - web
    - frontend
    - onboarding
    - internal
---
# New Braid web prototype

Procedural workflow for designers (and others) creating a **new Braid web prototype** on macOS with Cursor. This is **Part 2: project setup** — do this for every new project. Part 1 (machine setup) is a prerequisite.

**References** (read when executing this workflow):

- `references/new-web-prototype.md` — scaffold Sku project, add Braid, start dev server, open in Cursor

**Related skill (Part 1):**

- `machine-setup` — Node, Homebrew, Git, pnpm, AI Toolkit, extensions (**run first if prerequisites are missing**). In this repo: `../machine-setup/SKILL.md`

**Source guide:** [Part 2 (Every project)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996/Part+2+Every+project)

---

## Agent behavior

**Be interactive, not autonomous.** Work through `references/new-web-prototype.md` **step by step**. After each step, verify success before continuing. If a step fails, stop and explain what went wrong.

- **Step 0 (before Step 1):** Ask for (or confirm) the project name — do not scaffold with a placeholder.
- If `brew`, `pnpm`, `node`, or `git` are missing or fail, redirect to **machine-setup** (`../machine-setup/SKILL.md` or `SEEK-machine-setup`).
- **Step 6 is conditional** — only run the Braid guidelines workaround when the user did not install the Braid skill via AI Toolkit during Part 1 Step 5 of **machine-setup**

---

## Workflow summary (Part 2)

| Step | Action |
| --- | --- |
| 0 | Ask for (or confirm) project name; validate before scaffolding |
| 1 | `brew update && brew upgrade pnpm git` |
| 2 | Scaffold with `pnpm dlx @sku-lib/create` (webpack template) |
| 3 | Add `braid-design-system` |
| 4 | Start dev server (`pnpm start`) |
| 5 | Open project folder in Cursor (UI: Open project / Open folder) |
| 6 | *(Conditional)* Load Braid guidelines via prompt — only if AI Toolkit Braid skill was not installed in Part 1 |

Full commands, verification, and user handoffs: `references/new-web-prototype.md`.

---

## NEVER

- Never scaffold without a confirmed project name — placeholders cause wrong paths and overwrite risk
- Never skip Part 1 prerequisites — if `node`, `pnpm`, or `git` are missing, follow **machine-setup** first
- Never run Step 6 when the user already has the **braid** skill installed via AI Toolkit (`SEEK-braid`)
- Never use `cd ~/Code new-cool-project` — the path separator must be `/` (`cd ~/Code/<project-name>`)

---

## After setup

Remind the user that when they reopen the project they should run:

```bash
pnpm install && pnpm start
```

For ongoing UI work, use the **braid** skill from [braid-context](https://github.com/seek-oss/braid-context) (`SEEK-braid` when installed via AI Toolkit).
