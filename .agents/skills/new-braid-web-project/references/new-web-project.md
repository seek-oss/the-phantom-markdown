# Agent instructions: new Braid web project (Part 2)

You are helping a designer create a new Braid web design project from scratch. Work through each step below **in order**. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do.

> **Prerequisite:** Part 1 (machine setup) must be complete — Node.js v22+, Homebrew, Git, and pnpm v10+ must already be installed. If not, follow the **machine-setup** skill (`../machine-setup/SKILL.md` or `SEEK-machine-setup`) instead and complete that workflow first.

These instructions are for **web projects only**.

---

## Step 0: Choose a project name

Before running any scaffold commands, **ask the user** what they want to call the project.

- If the user **already stated a name** in this conversation, repeat it back and ask them to **confirm** before continuing.
- If they have **not** provided a name, ask: *“What would you like to call your project?”*
- Do not proceed to Step 1 until you have a confirmed project name.

**Naming rules** (apply before scaffolding):

- Use **lowercase letters, numbers, and hyphens** only (e.g. `job-alert-settings`, `seek-home-explore`)
- **No spaces** — suggest hyphens instead (e.g. `my-cool-project`)
- Keep it short and readable; avoid special characters

**Validate** the name before scaffolding:

```bash
test ! -e ~/Code/<project-name> && echo "OK" || echo "Folder already exists"
```

If the folder already exists under `~/Code`, stop and ask the user to pick a different name or confirm they want to use another location.

Use the confirmed name as `<project-name>` in all following steps.

---

## Step 1: Update Homebrew-managed tools

Refresh **git** and **pnpm** (installed via Homebrew in Part 1). This may take a minute or two.

Tell the user: *"I'll update git and pnpm via Homebrew — this usually takes a minute or two."*

```bash
brew update && brew upgrade pnpm git
```

If Homebrew reports a package is **not installed**, note it and continue — the user may need Part 1 machine setup instead.

**Verify** prerequisites after the upgrade:

```bash
node --version && pnpm --version && git --version
```

- `node` should be **v22+** (from nvm, not Homebrew)
- `pnpm` should be **v10+**
- `git` should be available

If any check fails or commands are missing, **stop** and follow the **machine-setup** skill (`../machine-setup/SKILL.md` or `SEEK-machine-setup`) instead of continuing.

---

## Step 2: Initialise the project with Sku

Run these commands in Terminal (press **Cmd+J** in Cursor to open it). Replace `<project-name>` with the name from Step 0:

```bash
cd ~/Code
pnpm dlx @sku-lib/create <project-name> --template=webpack
cd ~/Code/<project-name>
```

The create command scaffolds the project with Sku and installs dependencies automatically. Wait for it to finish before continuing.

**Verify:** the project directory exists and contains `package.json` with Sku dependencies.

---

## Step 3: Install Braid design system

```bash
pnpm add braid-design-system
```

**Verify:** `braid-design-system` appears in `package.json` dependencies.

---

## Step 4: Start the local dev server

```bash
pnpm start
```

This should open a browser tab with the running app.

**Verify:** dev server starts without errors. If port or browser issues occur, report them and suggest fixes before continuing.

---

## Step 5: Open the project folder

Run the following command to open the project folder in Cursor (from inside the project directory):

```bash
cursor .
```

If the command fails, ask the user to open the folder manually: in Cursor, click **Open project** in the centre of the window, or **Open folder** in the left-hand sidebar. A Finder window will open — navigate to the new project folder and the file tree will appear in the sidebar.

**Verify:** the user is working in the new project workspace, not the previous folder.

---

## Step 6: Connect with design context

Load the **braid** skill and follow its platform routing:

- In this repo: `../braid/SKILL.md` (or `SEEK-braid` when installed via AI Toolkit)
- Read `references/systems.md` and `references/web.md` from that skill (default platform is **Web**)

Alternatively, fetch the public entry points:

```
https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md
https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/web.md
```

Follow all guidelines from those sources, including accessibility requirements.

Let the user know when design context has been loaded and you are ready to help them build with Braid.

---

## Done

Tell the user the project is set up and ready to build with Braid.

Remind them that any time they reopen the project they should run:

```bash
pnpm install && pnpm start
```
