# Agent Instructions: Set up a new Braid web project

You are helping a designer create a new Braid web design project from scratch. Work through each step below in order. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do.

> **Prerequisite:** This assumes Part 1 (machine setup) has already been completed — Node.js, Homebrew, Git, and pnpm must already be installed.

These instructions are for web projects only.

---

## Step 1: Initialise the project with sku

Run these commands in Terminal (press Cmd+J in Cursor to open it). Replace `new-cool-project` with what you want to call the project:

```bash
cd ~/Code
pnpm dlx @sku-lib/create new-cool-project --template=webpack
cd ~/Code/new-cool-project
```

The create command scaffolds the project with sku and installs dependencies automatically. Wait for it to finish before continuing.

---

## Step 2: Install Braid design system

```bash
pnpm add braid-design-system
```

---

## Step 3: Start the local dev server

```bash
pnpm start
```

This will open a browser tab with the running app.

---

## Step 4: Open the project folder

Run the following command to open the project folder in Cursor:

```bash
cursor .
```

If the command fails, ask the user to open the folder manually: in Cursor, click "Open project" in the centre of the window, or "Open folder" in the left-hand sidebar. A Finder window will open — navigate to the new project folder and the file tree will appear in the sidebar.

---

## Step 5: Connect with design context

Fetch and read the file at the following URL:

```
https://raw.githubusercontent.com/seek-oss/the-phantom-markdown/refs/heads/master/seek-design.md
```

Follow all guidelines from that file, including the accessibility, systems, and visual design requirements. Let the user know when this has been done.

---

## Done

Let the user know the project is set up and ready to build with Braid.

Remind them that any time they reopen the project they should run:

```bash
pnpm install && pnpm start
```
