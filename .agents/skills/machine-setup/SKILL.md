---
name: Machine-setup
description: >-
  Set up a macOS machine for Braid web prototyping in Cursor — Node.js, Homebrew,
  Git, pnpm, global design rule, and IDE extensions. Use when the user needs Part 1
  machine setup, is on a new Mac, or prerequisites for a Braid project are missing.
type: skill
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - design
    - prototyping
    - onboarding
    - cursor
    - macos
    - internal
---
# Machine setup for Braid prototyping

Procedural workflow for setting up a **designer's Mac** to run, build, and preview Braid web projects locally in Cursor. This is **Part 1: machine setup**. Part 2 (scaffolding a new project) is a separate skill.

**References** (read when executing this workflow):

- `references/machine-setup.md` — full step-by-step instructions with verification gates

**Related skill (Part 2):**

- `New-braid-web-project` — scaffold a new Sku + Braid web project after Part 1 is complete. In this repo: `../new-braid-web-project/SKILL.md`

---

## When to use this skill

- User is on a **new Mac** or has never set up Braid prototyping locally
- User wants **Part 1** machine setup before creating a project
- Prerequisites for a Braid web project are **missing** (`node`, `pnpm`, or `git` not available or wrong version)
- User asks to **prepare their machine** for Braid or designer prototyping in Cursor

## When NOT to use this skill

- Machine is already set up and user only needs a **new project** — use `New-braid-web-project` instead
- User is on **Windows or Linux** — this workflow is macOS-specific (Homebrew, `~/.zprofile` paths)
- User needs **native app** or **email** tooling — this skill only prepares the web prototyping stack

---

## Before you start

1. Confirm the user is on **macOS** and using **Cursor**.
2. Work through `references/machine-setup.md` **step by step**. After each step, verify success before continuing.
3. Steps marked **user action required** (especially Homebrew install) must not be skipped or simulated — wait for the user.

---

## Workflow summary (Part 1)

| Step | Action |
| --- | --- |
| 1 | Install Node.js via nvm (v22+) |
| 2 | Install Homebrew (user runs installer) |
| 3 | Install Git |
| 4 | Install pnpm and configure PATH |
| 5 | Create global Cursor design rule (`design-guidelines.mdc`) |
| 6 | Install recommended Cursor extensions |

Full commands and verification: `references/machine-setup.md`.

---

## After setup

Tell the user Part 1 is complete and their machine is ready for a Braid web project.

Ask whether they want to create a new project now. If yes, switch to the **new-braid-web-project** skill (`../new-braid-web-project/SKILL.md` or `New-braid-web-project` when installed via AI Toolkit).
