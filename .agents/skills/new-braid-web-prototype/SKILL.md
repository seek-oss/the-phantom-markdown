---
name: new-braid-web-prototype
description: >-
  Scaffold a new Braid web prototype with Sku and braid-design-system on macOS in Cursor.
  Use when the user wants to start a new Braid web prototype, set up a Braid project,
  create a Sku app with Braid, or needs machine prerequisites before prototyping.
  Do not use for native apps, email templates, existing repos, or backend-only work.
type: skill
compatible_tools: [cursor]
compatibility: >-
  macOS with Cursor (via SEEK Self Service), network access, and permission to run
  terminal commands. Assumes AI Toolkit is available. Node v22+, pnpm v10+, git, and
  Homebrew required — see references/machine-setup.md if missing.
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
    - ai-toolkit
    - internal
---
# New Braid web prototype

Procedural workflow for designers (and others) creating a **new Braid web prototype** on macOS with Cursor.

**References** (read when executing this workflow):

- `references/new-web-prototype.md` — Part 2: scaffold Sku project, add Braid, start dev server *(default)*
- `references/machine-setup.md` — Part 1: one-time machine setup *(read if prerequisites fail)*

**Source guides:**

- [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759/Part+1+Do+once)
- [Part 2 (Every project)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996/Part+2+Every+project)

---

## Agent behavior

**Be interactive, not autonomous.** Work through `references/new-web-prototype.md` **step by step**. After each step, verify success before continuing. If a step fails, stop and explain what went wrong.

- **Step 1:** Ask for (or confirm) the project name — do not scaffold with a placeholder.
- If `brew`, `pnpm`, `node`, or `git` are missing or fail, switch to `references/machine-setup.md`. When Part 1 is complete, return to `references/new-web-prototype.md`.
- **Homebrew install (Part 1 Step 2)** requires the user to run the installer themselves — do not skip or simulate.

---

## Workflow summary

| Part | Reference | When |
| --- | --- | --- |
| Part 2 | `references/new-web-prototype.md` | Default — every new prototype |
| Part 1 | `references/machine-setup.md` | Prerequisites missing or new Mac |

### Part 2 steps

| Step | Action |
| --- | --- |
| 1 | Ask for (or confirm) project name; validate before scaffolding |
| 2 | `brew update && brew upgrade pnpm git` |
| 3 | Scaffold with `pnpm dlx @sku-lib/create` (webpack template) |
| 4 | Add `braid-design-system` |
| 5 | Start dev server (`pnpm start`) |
| 6 | Open project folder in Cursor (UI: Open project / Open folder) |

Full commands and verification: `references/new-web-prototype.md`.

---

## NEVER

- Never scaffold without a confirmed project name — placeholders cause wrong paths and overwrite risk
- Never skip Part 1 when prerequisites fail — read `references/machine-setup.md` first
- Never simulate the Homebrew password prompt — the user must run the installer themselves
- Never use `cd ~/Code new-cool-project` — the path separator must be `/` (`cd ~/Code/<project-name>`)

---

## After setup

Remind the user that when they reopen the project they should run:

```bash
pnpm install && pnpm start
```

For ongoing UI work, use the **braid** skill from [braid-context](https://github.com/seek-oss/braid-context) (`SEEK-braid` when installed via AI Toolkit).
