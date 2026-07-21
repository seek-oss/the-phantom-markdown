# Agent instructions: Braid email prototype workspace

Email preview is always **Playroom** (browser). The AI assistant helps write code; Playroom is where templates are composed and previewed.

**Do not** scaffold a Sku-style app for email.

---

## Track A: Playroom only (no setup)

Use when the user wants visual exploration **without** a local clone / AI project context.

1. Open [Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/) (SEEK SSO)
2. Use **Snippets**, edit code, preview in frames
3. **Share** to copy a URL

Stop here unless they want Track B.

Docs: https://braid-email.skinfra.xyz/

---

## Track B: Playroom + AI assistant

> **Prerequisite:** `common.md` and `email.md` machine setup complete (`git`, `node`, `yarn`, email repo SSH access).

### Step 1: Choose a workspace name

One clone is reused for many prototypes. Naming: lowercase, numbers, hyphens.

Validate:

```bash
test ! -e ~/Code/<workspace-name> && echo "OK" || echo "Folder already exists"
```

### Step 2: Clone the email monorepo (once)

```bash
cd ~/Code
git clone git@github.com:SEEK-Jobs/mjml-react-email-templates.git <workspace-name>
cd ~/Code/<workspace-name>
yarn install
```

### Step 3: Open the workspace in the AI IDE

Open `~/Code/<workspace-name>` in Cursor / Copilot / Claude Code.

### Step 4: Prototype in Playroom

**Option A — Hosted (recommended):**

1. Open https://braid-email.skinfra.xyz/playroom/
2. Ask the assistant to draft React + `@seek/braid-email-ui` code
3. Paste into Playroom; preview; **Share**

**Option B — Local (optional):**

```bash
yarn playroom
```

Opens Playroom locally (typically `http://localhost:9000`).

### Step 5: Keep prototypes organised

- Name Playroom frames clearly
- Save Share links per design
- Do **not** commit personal prototypes to the shared monorepo unless the team owns that work

### Conditional: Braid skill missing

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/email.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

## Done

| Goal | Action |
| --- | --- |
| Preview | Hosted Playroom or `yarn playroom` |
| AI help | Open the workspace folder in the IDE + braid skill |
| Share | Playroom **Share** link |
