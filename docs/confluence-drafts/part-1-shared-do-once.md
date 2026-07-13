# Setting up an IDE for AI prototyping

## Part 1 — Shared: Set up your machine (Do this once)

> Install the tools every platform needs — admin access, Homebrew, Git, GitHub access for Terminal, SEEK AI Toolkit, and GitLens. Then complete the **Part 1** page for your platform (Web, iOS, Android, or Email).

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **Info panel:** **Email — Track A (Playroom only):** No machine setup required. Open [Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/) in your browser (SEEK SSO sign-in required) and go straight to [Part 2 — Email](<!-- link to Part 2 Email -->), Track A.

---

### Step 1: Request administrator access

To install software you must first **Request administrator access** in the top right-hand menu of your machine (checkmark icon).

<!-- Confluence: insert screenshot from existing web Part 1 page -->

---

### Step 2: Install Homebrew

In **Terminal** (press **Cmd+Space** and search for Terminal on Mac), run:

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

You should see a version number printed (e.g. `4.1.8`).

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

### Step 4: Set up GitHub access (Terminal)

You'll need a GitHub licence and access to the **SEEK-Jobs** organisation. For Terminal, `git`, and AI Toolkit, SSH keys in **1Password** are recommended:

* Follow the developer [setup guide](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) + [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended)
* Or use the [Agent-assisted copy and paste prompt](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5606015700) (non-engineer friendly)

Verify GitHub SSH access:

```bash
ssh -T git@github.com
```

You should see a success message mentioning your GitHub username.

> **Info panel:** Some platforms need extra one-time credentials (for example a disk-based SSH key for **Xcode**, or a GitHub Packages token for **Android**). Those steps are on the platform Part 1 pages — not here.

---

### Step 5: Install [SEEK AI Toolkit](https://backstage.myseek.xyz/docs/default/component/seek-ai-toolkit/)

This step requires a GitHub licence and access to the SEEK-Jobs organisation. If you don't yet have access, skip to Step 6.

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

### Step 6: Install GitLens (optional but recommended)

Install via your IDE's **Extensions** marketplace, or (for Cursor) from **Terminal**:

```bash
cursor --install-extension eamodio.gitlens
```

| Extension | ID |
| --- | --- |
| GitLens | `eamodio.gitlens` |

Platform-specific extensions (Prettier, ESLint, Swift, Kotlin) are on the platform Part 1 pages.

---

### Done!

> **Note panel:** Next, complete the Part 1 page for your platform, then Part 2:
>
> - **[Part 1 — Web](<!-- link -->)** → [Part 2 — Web](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996)
> - **[Part 1 — iOS](<!-- link -->)** → [Part 2 — iOS](<!-- link -->)
> - **[Part 1 — Android](<!-- link -->)** → [Part 2 — Android](<!-- link -->)
> - **[Part 1 — Email](<!-- link -->)** → [Part 2 — Email](<!-- link -->)
