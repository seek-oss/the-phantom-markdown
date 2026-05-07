# Agent Instructions: Set up a new Braid project

You are helping a designer create a new Braid design system project from scratch. Work through each step below in order. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do.

> **Prerequisite:** This assumes Part 1 (machine setup) has already been completed — Node.js, Homebrew, Git, and pnpm must already be installed.
>
> **Scope:** These instructions are for web projects only.

---

## Step 1: Initialise the project with sku

Ask the user what they want to name their project if they haven't already specified. Use that name in place of `my-project-name` below.

Run from the home directory:

```bash
cd ~
pnpm dlx @sku-lib/create my-project-name
```

This will scaffold the project and install dependencies automatically. Wait for it to finish before continuing.

Then move into the project directory:

```bash
cd ~/my-project-name
```

Verify the scaffold succeeded by checking the directory exists and contains a `package.json`:

```bash
ls package.json
```

If `package.json` is listed, continue. Otherwise stop and report the error.

---

## Step 2: Install Braid design system

```bash
pnpm add braid-design-system
```

Verify it was added to `package.json`:

```bash
grep '"braid-design-system"' package.json
```

If the package appears in the output, continue. Otherwise stop and report the error.

---

## Step 3: Wire up BraidProvider

Replace the contents of `src/App/App.tsx` with the following:

```tsx
import "braid-design-system/reset"; // Must be first
import seekJobsTheme from "braid-design-system/themes/seekJobs";
import { BraidProvider, Text } from "braid-design-system";

export default function App() {
  return (
    <BraidProvider theme={seekJobsTheme}>
      <Text>Hello from Braid!</Text>
    </BraidProvider>
  );
}
```

> The `reset` import must be the first line — Braid's styles will not work correctly otherwise.

Confirm the file was written correctly:

```bash
head -1 src/App/App.tsx
```

If the first line is `import 'braid-design-system/reset';`, continue. Otherwise stop and report the error.

---

## Step 4: Start the local dev server

```bash
pnpm start
```

This will open a browser tab with the running app. Let the user know their project is ready and the dev server is running.

---

## Done

Let the user know the project is set up and ready to build with Braid. Remind them that any time they reopen the project they should run:

```bash
pnpm install
pnpm start
```
