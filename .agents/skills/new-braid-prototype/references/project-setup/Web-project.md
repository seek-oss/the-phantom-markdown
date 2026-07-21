# Agent instructions: new Braid web prototype

You are helping create a new Braid **web** prototype. Work through each step **in order**. Verify after each step.

> **Prerequisite:** `common.md` and `Web.md` machine setup complete (`brew`, `git`, `node`, `pnpm` available). If not, stop and finish those first.

---

## Step 1: Choose a project name

**Ask** for (or confirm) the project name before scaffolding.

**Naming rules:**

- Lowercase letters, numbers, and hyphens only (e.g. `job-alert-settings`)
- No spaces
- Short and readable

Validate:

```bash
test ! -e ~/Code/<project-name> && echo "OK" || echo "Folder already exists"
```

If the folder exists, ask for a different name.

---

## Step 2: Update Homebrew packages

```bash
brew update && brew upgrade pnpm git
```

If `node`, `pnpm`, or `git` are missing, return to machine setup.

---

## Step 3: Initialise with Sku

```bash
cd ~/Code
pnpm dlx @sku-lib/create <project-name> --template=webpack
cd ~/Code/<project-name>
```

Wait for scaffolding and install to finish.

**Verify:** `package.json` exists with Sku dependencies.

---

## Step 4: Install Braid design system

```bash
pnpm add braid-design-system
```

**Verify:** `braid-design-system` is in `package.json` dependencies.

---

## Step 5: Start the local dev server

```bash
pnpm start
```

**Verify:** dev server starts; a browser tab should open with the app.

---

## Step 6: Open the project folder

Have the user open `~/Code/<project-name>` in their IDE (**File → Open Folder…** / Open project).

**Verify:** they are working in the new project workspace.

---

## Done

Remind them that when reopening the project:

```bash
pnpm install && pnpm start
```

For ongoing UI work, use the **braid** skill (`SEEK-braid` via AI Toolkit).
