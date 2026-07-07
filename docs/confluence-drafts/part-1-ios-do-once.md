# Setting up an IDE for AI prototyping

## Part 1 — iOS: Set up your machine (Do this once)

> Install the tools your machine needs to run, build and preview Braid iOS prototypes locally.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install **Xcode** and your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **Already completed [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759)?** If you have already set up Git and the SEEK AI Toolkit for web prototyping, you can skip Steps 1–2 and Step 5 below.

---

### Step 1: Install Git

Open **Terminal** (press **Cmd+Space** and search for Terminal on Mac) and run:

```bash
brew install git
```

If Homebrew is not installed, complete Steps 2–4 of [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759) first.

Verify:

```bash
git --version
```

You should see a version starting with `git version 2` or higher.

---

### Step 2: Install Xcode

Install **Xcode** from **SEEK Self Service**, then launch Xcode once to install the iOS SDKs and accept the licence agreement.

Verify:

```bash
xcodebuild -version
```

You should see an Xcode version printed.

---

### Step 3: Set up GitHub access for Xcode

The iOS app template depends on private SEEK packages (including [braid-ios](https://github.com/SEEK-Jobs/braid-ios)). Xcode needs GitHub authentication to download them.

> **Info panel:** You need a GitHub licence and access to the **SEEK-Jobs** organisation. SSH keys in 1Password are recommended for git — see [setup details](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) and [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

#### Generate a GitHub token

1. Visit [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Name it `Xcode GitHub`
4. Grant these permissions:
   - `admin:public_key`
   - `write:discussion`
   - `repo`
   - `user`
5. Generate the token and copy it — you **cannot** view it again
6. Click **Enable SSO** and authorise access to **SEEK-Jobs**

#### Add your GitHub account in Xcode

1. Open **Xcode**
2. Menu bar: **Xcode → Settings…**
3. Open the **Accounts** tab
4. Click **+** (bottom left) and choose **GitHub**
5. Enter your GitHub username or email and paste the token, then click **Sign in**

---

### Step 4: Confirm access to braid-ios

In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/braid-ios.git HEAD
```

If this fails, you do not yet have access to the Braid iOS repository. Request access via your team or GitHub onboarding before continuing.

---

### Step 5: Install [SEEK AI Toolkit](https://backstage.myseek.xyz/docs/default/component/seek-ai-toolkit/)

This step requires a GitHub licence and access to the SEEK-Jobs organisation. If you don't yet have access, skip to Step 6.

> **Info panel:** You'll need SSH keys in 1Password to authenticate the Homebrew tap (see links in Step 3).

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

### Step 6: Install IDE extensions (optional but recommended)

Install these extensions via your IDE's **Extensions** marketplace (names are the same across VS Code–compatible editors):

| Extension | ID |
| --- | --- |
| GitLens | `eamodio.gitlens` |

If you also edit Swift in a VS Code–compatible IDE, consider the **Swift** extension (`swiftlang.swift-vscode`).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — iOS: Set up your project](<!-- link to Part 2 iOS page when published -->)**.
