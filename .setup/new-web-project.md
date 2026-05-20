# Agent Instructions: Set up a new Braid web project

You are helping a designer create a new Braid web design project from scratch. Work through each step below in order. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do.

Some steps are environment-specific — check the label before running each one:

- **Local environment** — an IDE or terminal-based tool (e.g. Cursor, Claude Code, VS Code). Can run shell commands and install packages.
- **Web-based tool** — a browser tool that manages its own project environment (e.g. v0, Figma Make, Lovable). Cannot run terminal commands.

Steps marked **(local only)** should be skipped in web-based tools.

> **Prerequisite (local only):** This assumes Part 1 (machine setup) has already been completed — Node.js, Homebrew, Git, and pnpm must already be installed.

---

## Step 1: Name the project _(local only)_

**Skip this step** if you are running in a web-based tool — it manages its own project structure and does not need a name up front.

Otherwise, ask the user:

> "What would you like to name your project?"

Wait for their response before continuing. Use that name in place of `my-project-name` in all steps below.

---

## Step 2: Initialise the project with sku _(local only)_

**Skip this step** if you are running in a web-based tool — it handles project initialisation itself.

Otherwise, you will not be able to run these commands directly — the scaffold creates a new folder outside the current workspace, which requires terminal access. Ask the user to do this themselves.

Prompt them with something like:

> "To get your project set up, I'll need you to run a couple of commands in your terminal. Open Terminal, then run these one at a time:
>
> ```
> cd ~/Code
> ```
>
> ```
> pnpm dlx @sku-lib/create my-project-name --template=webpack
> ```
>
> This will create your project and install its dependencies — it may take a minute or two. Once it's done, run:
>
> ```
> cd ~/Code/my-project-name
> ```
>
> ```
> cursor .
> ```
>
> That will open the project in Cursor. Just let me know when you're ready and I'll take it from there!"

Wait for the user to confirm before continuing.

---

## Step 3: Install Braid design system

```bash
pnpm add braid-design-system
```

Verify it was added to `package.json`:

```bash
grep '"braid-design-system"' package.json
```

If the package appears in the output, continue. Otherwise stop and report the error.

---

## Step 4: Import the SeekSans font

Add the following `@import` to `src/styles/fonts.css` (create the file if it doesn't exist):

```css
@import url("https://www.seek.com.au/static/shared-web/seeksans.css");
```

This must be imported at the app root level so the font is available globally.

Verify the file contains the import:

```bash
grep 'seeksans' src/styles/fonts.css
```

If the import appears in the output, continue. Otherwise stop and report the error.

---

## Step 5: Wire up BraidProvider

Replace the contents of `src/App/App.tsx` with the following:

```tsx
import "braid-design-system/reset"; // Must be first

import seekJobs from "braid-design-system/themes/seekJobs";
import { BraidProvider, Stack, Heading, Text } from "braid-design-system";

export default function App() {
  return (
    <BraidProvider theme={seekJobs}>
      <Stack space="large">
        <Heading level="1">Welcome to Braid</Heading>
        <Text>Your app is now using the Braid Design System!</Text>
      </Stack>
    </BraidProvider>
  );
}
```

> The `reset` import must be the first line — Braid's styles will not work correctly otherwise.
>
> Braid uses Vanilla Extract for styling internally. Avoid custom CSS or style overrides — use Braid component props and theme tokens instead.

Confirm the file was written correctly:

```bash
head -1 src/App/App.tsx
```

If the first line is `import 'braid-design-system/reset';`, continue. Otherwise stop and report the error.

---

## Step 6: React Server Components (conditional)

If the project uses a React Server Components environment (e.g. Next.js, v0), add `"use client"` as the very first line of any file that imports Braid components. Braid components require React Context to function and will not work in a server component without this directive.

Skip this step if the project is a standard client-side app (e.g. scaffolded with sku in Step 2).

---

## Step 7: Read the SEEK design guidelines

Fetch and read the file at the following URL:

```
https://raw.githubusercontent.com/seek-oss/the-phantom-markdown/refs/heads/master/seek-design.md
```

Follow all guidelines from that file, including the accessibility, content, systems, and visual design requirements. Let the user know once this has been done.

---

## Step 8: Start the local dev server _(local only)_

**Skip this step** if you are running in a web-based tool — it provides its own live preview.

Otherwise, run:

```bash
pnpm start
```

This will open a browser tab with the running app. Let the user know their project is ready and the dev server is running.

---

## Done

Let the user know the project is set up and ready to build with Braid.

If in a local environment, remind them that any time they reopen the project they should run:

```bash
pnpm install
pnpm start
```
