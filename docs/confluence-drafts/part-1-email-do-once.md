# Setting up an IDE for AI prototyping

## Part 1 — Email: Set up your machine (Do this once)

> Install the tools needed for **AI-assisted** Braid email prototyping. If you only use hosted Playroom in the browser, you can skip this page — go straight to [Part 2 — Email](<!-- link -->), Track A.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **Info panel:** **Track A (Playroom only)** — no machine setup required. Open [Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/) in your browser (SEEK SSO sign-in required).

> **Track B (Playroom + AI assistant)** — complete the steps below so your IDE agent can help write Braid email code with full project context.

> **Already completed [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759)?** If Node.js, Homebrew, Git, and AI Toolkit are already installed, you only need **Step 5 (Yarn)** below.

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

### Step 2: Install Homebrew

In **Terminal**, run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When it finishes, follow the printed instructions to add Homebrew to your PATH. They'll look something like this — run both lines:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify:

```bash
brew --version
```

---

### Step 3: Install Git

In **Terminal**, run:

```bash
brew install git
```

Verify:

```bash
git --version
```

You should see a version starting with `git version 2` or higher.

---

### Step 4: Confirm GitHub access

The email repository is private. In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/mjml-react-email-templates.git HEAD
```

If this fails, you do not yet have access. Request access via your team or [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

> **Info panel:** SSH keys in 1Password are recommended — see [setup details](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358).

---

### Step 5: Install Yarn

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

### Step 6: Install [SEEK AI Toolkit](https://backstage.myseek.xyz/docs/default/component/seek-ai-toolkit/)

This step requires a GitHub licence and access to the SEEK-Jobs organisation. If you don't yet have access, skip to Step 7.

In **Terminal**, run:

```bash
# First time: add the tap
brew tap SEEK-Jobs/homebrew-tools git@github.com:SEEK-Jobs/homebrew-tools.git

# Install the CLI
brew install SEEK-Jobs/homebrew-tools/ai-toolkit

# Run the CLI
ai-toolkit
```

Once AI Toolkit is running, install the **Braid skill**:

```bash
ai-toolkit install skill Braid --catalog seek-oss/braid-context/.agents@master
```

You will be prompted to select your IDE (**Cursor**, **Claude Code**, or **Copilot**) and installation target (**Workspace** or user profile).

---

### Step 7: Install IDE extensions (optional but recommended)

Install these extensions via your IDE's **Extensions** marketplace:

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |
| GitLens | `eamodio.gitlens` |

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — Email: Set up your workspace](<!-- link to Part 2 Email page when published -->)**.
