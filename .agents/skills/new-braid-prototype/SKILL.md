---
name: new-braid-prototype
description: >-
  Set up a new Braid prototype on macOS for Web, iOS, Android, or Email — including
  one-time machine setup and per-project scaffolding. Use when the user wants to start
  a Braid prototype, scaffold a design project, or is missing prerequisites. Do not use
  for existing production apps or backend-only work.
type: skill
metadata:
  author: "@SEEK-Jobs/design-practice"
  tags:
    - braid
    - design
    - prototyping
    - web
    - ios
    - android
    - email
    - onboarding
    - ai-toolkit
    - internal
---

# New Braid prototype

Procedural workflow for creating a **new Braid prototype** on macOS. Supports **Web**, **iOS**, **Android**, and **Email**.

## When to use

- User wants a new Braid prototype / design project
- User needs machine setup before prototyping
- User asks to scaffold Sku + Braid (web), blank Xcode + braid-ios, blank Android Studio + braid-compose, or email Playroom + AI

## When not to use

- Existing production app repos (unless they explicitly want a separate prototype)
- Backend-only or non-Braid work
- Windows/Linux (this skill assumes macOS)

## References

**Machine setup** (one-time):

| File | When |
| --- | --- |
| `references/machine-setup/common.md` | Always — Homebrew, Git, Terminal GitHub SSH, AI Toolkit, GitLens |
| `references/machine-setup/web.md` | Web — Node, pnpm, Prettier/ESLint |
| `references/machine-setup/ios.md` | iOS — Xcode, disk-based SSH key, optional xcsift / Xcode MCP |
| `references/machine-setup/android.md` | Android — Android Studio, Cloudsmith Gradle token |
| `references/machine-setup/email.md` | Email Track B — Node, Yarn, email repo access |
| `references/machine-setup/ssh-keys-1password.md` | When Terminal SSH to GitHub fails — agent-assisted 1Password setup |

**Project setup** (every prototype / workspace):

| File | When |
| --- | --- |
| `references/project-setup/web-project.md` | Web — Sku scaffold + braid-design-system |
| `references/project-setup/ios-project.md` | iOS — blank Xcode app + braid-ios |
| `references/project-setup/android-project.md` | Android — blank Android Studio app + braid-compose |
| `references/project-setup/email-project.md` | Email — Track A (Playroom only) or Track B (clone + Playroom) |

---

## Agent behavior

**Be interactive, not autonomous.** Work step by step. After each step, verify success before continuing. If a step fails, stop and explain what the user must do.

### 1. Confirm platform (and track, for Email)

If the user has **not** already stated a platform, ask which one:

- **Web**
- **iOS**
- **Android**
- **Email** — if chosen, also ask in the same turn whether they want **Track A** (hosted Playroom only — no machine/project clone) or **Track B** (local clone + AI assistant). Default to Track B if they want AI help.

If they already said the platform (and track, for Email), confirm briefly and continue.

### 2. Machine setup

1. Read `references/machine-setup/common.md` and complete any **missing** steps (skip what already works).
2. Read the platform file (`web.md` / `ios.md` / `android.md` / `email.md`) and complete any **missing** steps.
3. If `ssh -T git@github.com` fails during common setup, read `references/machine-setup/ssh-keys-1password.md`.

**Email Track A:** Skip machine setup entirely. Go straight to `email-project.md` Track A.

### 3. Project setup

Read and follow the matching project file:

- Web → `references/project-setup/web-project.md`
- iOS → `references/project-setup/ios-project.md`
- Android → `references/project-setup/android-project.md`
- Email → `references/project-setup/email-project.md`

---

## NEVER

- Never scaffold or create a project without a **confirmed** project/workspace name
- Never skip machine setup when prerequisites fail — complete missing steps first
- Never simulate the Homebrew password prompt — the user must run the installer themselves
- Never use `cd ~/Code new-cool-project` — path separator must be `/` (`cd ~/Code/<name>`)

Platform-specific NEVERs live in the matching reference file (e.g. iOS SSH key handling in `ios.md`, email scaffolding in `email-project.md`).

---

## After setup

Remind the user how to reopen their prototype (commands differ by platform — see the project reference).

For ongoing Braid UI guidance, use the **braid** skill from [braid-context](https://github.com/seek-oss/braid-context) (`SEEK-braid` when installed via AI Toolkit).
