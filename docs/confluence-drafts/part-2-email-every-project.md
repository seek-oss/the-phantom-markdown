# Setting up an IDE for AI prototyping

## Part 2 — Email: Set up your workspace

> Start prototyping Braid email templates. Choose the track that fits how you want to work.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Info panel:** Email prototyping always happens in **Playroom** (a browser-based editor with live preview). Your AI assistant helps you **write code**; Playroom is where you **compose and preview** templates.

---

## Track A: Playroom only (no setup)

Best for visual exploration and quick layouts **without** an AI assistant.

### Step 1: Open Playroom

Go to **[Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/)** and sign in with SEEK SSO.

### Step 2: Start a prototype

1. Click the **Snippets** button in the toolbar to insert a layout, section, or component
2. Edit the code in the Playroom editor
3. Preview renders automatically in the frame(s) on the right

See the [Playroom guide](https://braid-email.skinfra.xyz/) for snippets, frames, and sharing.

### Step 3: Share your work

Click **Share** in the toolbar to copy a link. The URL stores your prototype state — share it with teammates or paste it into Slack.

> **Note panel:** Track A does not require Part 1 setup or a local repository. To use an **AI assistant** with Braid email context, switch to **Track B** below.

---

## Track B: Playroom + AI assistant

Best when you want Cursor, Claude Code, or GitHub Copilot to help write Braid email code. You still preview in Playroom (hosted or local).

> **Note panel:** Complete **[Part 1 — Email: Set up your machine](<!-- link -->)** before starting Track B (or the shared steps from [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759) plus Yarn).

---

### Step 1: Choose a workspace name

Pick a name for your local Playroom workspace (one clone reused for many prototypes).

**Naming rules:**

- Use **lowercase letters, numbers, and hyphens** only (e.g. `braid-email-playroom`, `job-alert-emails`)
- **No spaces**

In **Terminal**, check the folder does not already exist:

```bash
test ! -e ~/Code/<workspace-name> && echo "OK" || echo "Folder already exists"
```

Use `<workspace-name>` in the steps below.

---

### Step 2: Clone the email monorepo (once)

In **Terminal**, run:

```bash
cd ~/Code
git clone git@github.com:SEEK-Jobs/mjml-react-email-templates.git <workspace-name>
cd ~/Code/<workspace-name>
yarn install
```

This downloads `@seek/braid-email-ui` and Playroom. You only need to do this **once** — not per prototype.

---

### Step 3: Open the workspace in your IDE

Open `~/Code/<workspace-name>` in your AI-enabled IDE:

- **Cursor / VS Code / Copilot:** **File → Open Folder…**
- **Claude Code:** open the folder from your usual workflow

Your assistant can now read Braid email component APIs and the **Braid skill** (`SEEK-braid`) for guidance.

---

### Step 4: Prototype in Playroom

You have two preview options — pick one:

#### Option A: Hosted Playroom (recommended)

1. Open **[Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/)** in your browser
2. Ask your AI assistant to draft email template code (React + `@seek/braid-email-ui` components)
3. **Paste** the code into a Playroom frame
4. Preview, iterate, and **Share** the Playroom link

No local server required.

#### Option B: Local Playroom (optional)

From `~/Code/<workspace-name>`, run:

```bash
yarn playroom
```

This opens Playroom at `http://localhost:9000`. Use it the same way as hosted Playroom. Local Playroom is useful for offline work or [Email on Acid testing](https://github.com/SEEK-Jobs/mjml-react-email-templates/tree/master/packages/braid-email-ui#testing-playroom-in-email-on-acid) (advanced).

---

### Step 5: Keep prototypes organised

Unlike iOS or Android, email prototypes are **not separate project folders**. Keep track of your work by:

- **Naming Playroom frames** clearly in the editor
- **Saving Share links** for each prototype (each link is a distinct design)
- Optionally saving assistant-generated code in a personal notes file outside the monorepo

Do **not** commit personal prototype code to the shared monorepo unless your team owns that repository.

---

### [Conditional] Step 6: If AI Toolkit has not been installed

This step is only required if you were unable to install the [Braid skill using AI Toolkit](<!-- link to Part 1 Email Step 6 -->) during Part 1.

Copy and paste this prompt into your **Agent** chat:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/email.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

### From then on

| Goal | Action |
| --- | --- |
| Visual editing / preview | Open [hosted Playroom](https://braid-email.skinfra.xyz/playroom/) or run `yarn playroom` locally |
| AI help writing code | Open `~/Code/<workspace-name>` in your IDE and use the **Braid skill** |
| Share a design | Copy the Playroom **Share** link |

For ongoing Braid guidance, use the **Braid skill** installed via AI Toolkit (`SEEK-braid`).

---

## Which track should I use?

| Track | Setup | AI assistant | Best for |
| --- | --- | --- | --- |
| **A — Playroom only** | None | No (paste-only) | Quick visual exploration |
| **B — Playroom + AI** | Part 1 Email + one clone | Yes | Iterating with agent help on Braid email code |
