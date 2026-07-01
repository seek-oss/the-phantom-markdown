---
name: machine-setup
description: >-
  Set up a macOS machine for Braid web prototyping — Node.js, Homebrew, Git, pnpm,
  SEEK AI Toolkit with Braid skill, and Cursor extensions. Use when the user needs
  Part 1 machine setup, is on a new Mac, or prerequisites for a Braid prototype
  are missing. Do not use on Windows/Linux or when only a new project is needed.
type: skill
compatible_tools: [cursor]
compatibility: >-
  macOS with administrator access for Homebrew, network access, permission to run
  terminal commands, and Cursor installed via SEEK Self Service. Step 5 (AI Toolkit)
  requires GitHub access to SEEK-Jobs and SSH keys in 1Password — skippable if
  unavailable.
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - design
    - prototyping
    - onboarding
    - cursor
    - macos
    - ai-toolkit
    - internal
---
# Machine setup for Braid prototyping

Procedural workflow for setting up a **designer's Mac** to run, build, and preview Braid web projects locally. This is **Part 1: machine setup** — do this once. Part 2 (scaffolding a new prototype) is a separate skill.

**References** (read when executing this workflow):

- `references/machine-setup.md` — full step-by-step instructions with verification gates

**Related skill (Part 2):**

- `new-braid-web-prototype` — scaffold a new Sku + Braid web prototype after Part 1 is complete. In this repo: `../new-braid-web-prototype/SKILL.md`

**Source guide:** [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759/Part+1+Do+once)

---

## Agent behavior

**Be interactive, not autonomous.** Work through `references/machine-setup.md` **step by step**. After each step, verify success before continuing. If a step fails, stop and explain what went wrong.

- Confirm the user is on **macOS** with **Cursor** installed via SEEK Self Service before starting.
- **Step 2 (Homebrew)** requires the user to run the installer themselves — it prompts for a password. Do not skip or simulate.
- **Step 5 (AI Toolkit)** is skippable if the user lacks GitHub access to SEEK-Jobs — note this and continue to Step 6.
- **Step 6 (extensions)** is optional but recommended.

---

## Workflow summary (Part 1)

| Step | Action |
| --- | --- |
| 1 | Install Node.js via nvm (v22+) |
| 2 | Install Homebrew (user runs installer) |
| 3 | Install Git |
| 4 | Install pnpm and configure PATH |
| 5 | Install SEEK AI Toolkit and Braid skill *(skippable without GitHub access)* |
| 6 | Install recommended Cursor extensions *(optional)* |

Full commands and verification: `references/machine-setup.md`.

---

## NEVER

- Never skip Homebrew install or simulate the interactive password prompt — the user must run it themselves
- Never append duplicate pnpm PATH blocks to `~/.zshrc` — check before writing
- Never fail the whole workflow because Step 5 was skipped — Part 2 has a conditional workaround for Braid guidelines
- Never proceed past a failed verification step without stopping and reporting the error

---

## After setup

Tell the user Part 1 is complete and their machine is ready for a Braid web prototype.

Report a short completion summary:

- `node`, `pnpm`, and `git` versions from verification
- Whether AI Toolkit and the Braid skill were installed or skipped (and why)
- Whether Cursor extensions were installed or skipped

Ask whether they want to create a new project now. If yes, switch to the **new-braid-web-prototype** skill (`../new-braid-web-prototype/SKILL.md` or `SEEK-new-braid-web-prototype` when installed via AI Toolkit).
