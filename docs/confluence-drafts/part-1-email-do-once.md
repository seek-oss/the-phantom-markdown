# Setting up an IDE for AI prototyping

## Part 1 — Email: Set up your machine (Do this once)

> Install Node.js, Yarn, and email IDE extensions for **AI-assisted** Braid email prototyping (Track B). Complete **[Part 1 — Shared](<!-- link to Part 1 Shared -->)** first.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Info panel:** **Track A (Playroom only)** — no machine setup required. Open [Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/) in your browser (SEEK SSO sign-in required) and go straight to [Part 2 — Email](<!-- link to Part 2 Email -->), Track A.

> **Track B (Playroom + AI assistant)** — complete Shared Part 1, then the steps below, so your IDE agent can help write Braid email code with full project context.

> **Note panel:** Please ensure you've completed **[Part 1 — Shared: Set up your machine](<!-- link to Part 1 Shared -->)** (Homebrew, Git, GitHub access for Terminal, SEEK AI Toolkit) before continuing with Track B.

---

### Step 1: Install Node.js

Open **Terminal** (press **Cmd+Space** and search for Terminal on Mac) and run:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

\. "$HOME/.nvm/nvm.sh"

nvm install --lts
```

Verify:

```bash
node --version
```

You should see a version starting with `v22` or higher.

---

### Step 2: Confirm GitHub access to the email repository

The email repository is private. In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/mjml-react-email-templates.git HEAD
```

If this fails, you do not yet have access. Request access via your team or [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

> **Info panel:** SSH for Terminal should already work from [Part 1 — Shared](<!-- link to Part 1 Shared -->) (1Password recommended).

---

### Step 3: Install Yarn

The email monorepo uses **Yarn 1.x** (not pnpm). In **Terminal**, run:

```bash
brew install yarn
```

Verify:

```bash
yarn --version
```

You should see version `1.x`.

---

### Step 4: Install IDE extensions (optional but recommended)

Install via your IDE's **Extensions** marketplace, or (for Cursor) from **Terminal**:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
```

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |

GitLens is covered in [Part 1 — Shared](<!-- link to Part 1 Shared -->).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — Email: Set up your workspace](<!-- link to Part 2 Email page when published -->)** (Track B).
