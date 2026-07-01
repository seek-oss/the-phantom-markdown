# Agent instructions: new Braid web prototype (Part 2)

You are helping a designer create a new Braid web prototype from scratch. Work through each step below **in order**. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do.

> **Prerequisite:** Node.js v22+, Homebrew, Git, and pnpm v10+ must already be installed. If not, stop and work through `references/machine-setup.md` first, then return here.

> **Web only:** These instructions are for **web projects only**. Native and Email guides will be added separately.

**Source guide:** [Part 2 (Every project)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996/Part+2+Every+project)

---

## Step 1: Choose a project name

Before running any scaffold commands, **ask the user** what they want to call the project.

- If the user **already stated a name** in this conversation, repeat it back and ask them to **confirm** before continuing.
- If they have **not** provided a name, ask: *"What would you like to call your project?"*
- Do not proceed to Step 2 until you have a confirmed project name.

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

## Step 2: Update Homebrew packages

Open **Terminal** (press **Cmd+J** in Cursor, or **Cmd+Space** and search for Terminal on Mac). Run:

```bash
brew update && brew upgrade pnpm git
```

This updates Homebrew-managed packages to their latest available versions. It may take a minute or two.

If Homebrew reports a package is **not installed**, or `node`, `pnpm`, or `git` are unavailable, **stop** and work through `references/machine-setup.md` instead of continuing.

---

## Step 3: Initialise with Sku

Run these commands in **Terminal**. Replace `<project-name>` with the name from Step 1:

```bash
cd ~/Code
pnpm dlx @sku-lib/create <project-name> --template=webpack
cd ~/Code/<project-name>
```

The `create` command scaffolds the project with [Sku](https://github.com/seek-oss/sku) and installs dependencies automatically. Wait for it to finish before continuing.

**Verify:** the project directory exists and contains `package.json` with Sku dependencies.

---

## Step 4: Install Braid design system

In **Terminal**, run:

```bash
pnpm add braid-design-system
```

**Verify:** `braid-design-system` appears in `package.json` dependencies.

---

## Step 5: Start the local dev server

In **Terminal**, run:

```bash
pnpm start
```

This should open a browser tab with the running app.

**Verify:** dev server starts without errors. If port or browser issues occur, report them and suggest fixes before continuing.

---

## Step 6: Open the project folder

In Cursor, click **Open project** in the centre of the window, or **Open folder** in the left-hand sidebar. A Finder window will open — navigate to the new project folder and the file tree will appear in the sidebar.

**Verify:** the user is working in the new project workspace, not the previous folder.

---

## Done

Tell the user the project is set up and ready to build with Braid.

Remind them that any time they reopen the project they should run:

```bash
pnpm install && pnpm start
```

For ongoing UI work, use the **braid** skill (`SEEK-braid` when installed via AI Toolkit).
