# Setting up an IDE for AI prototyping

## Part 1 — iOS: Set up your machine (Do this once)

> Install the tools your machine needs to run, build and preview Braid iOS prototypes locally.



> **Before starting:** Install **Xcode** and your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **Already completed [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759)?** If you have already set up Git and the SEEK AI Toolkit for web prototyping, you can skip Step 1 and Step 6 below.

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



### Step 3: Set up SSH keys in 1Password

The iOS app template depends on private SEEK packages (including [braid-ios](https://github.com/SEEK-Jobs/braid-ios)). Authentication uses **SSH via 1Password** — the same setup used for git at SEEK.

> **Info panel:** You need a GitHub licence and access to the **SEEK-Jobs** organisation. Follow [SSH key setup in 1Password](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) and [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

Ensure:

1. Your **1Password SSH key** is configured for GitHub
2. The **1Password SSH agent** is running
3. You can authenticate to GitHub over SSH

Verify GitHub SSH access:

```bash
ssh -T git@github.com
```

You should see a success message mentioning your GitHub username.

---



### Step 4: Configure git to use SSH for GitHub

The iOS app template references Braid using an `https://github.com/…` URL. Swift Package Manager uses git to fetch packages. This one-time configuration makes those HTTPS URLs use SSH instead (so 1Password credentials apply).

In **Terminal**, run:

```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

Verify the setting:

```bash
git config --global --get-regexp url
```

You should see `url.git@github.com:.insteadof https://github.com/`.

---



### Step 5: Confirm access to braid-ios

In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/braid-ios.git HEAD
```

If this fails, you do not yet have access to the Braid iOS repository. Check your 1Password SSH setup and SEEK-Jobs GitHub access before continuing.

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

Install these extensions via your IDE's **Extensions** marketplace (names are the same across VS Code–compatible editors):


| Extension | ID                |
| --------- | ----------------- |
| GitLens   | `eamodio.gitlens` |


If you also edit Swift in a VS Code–compatible IDE, consider the **Swift** extension (`swiftlang.swift-vscode`).

---



### Done!

> **Note panel:** You can now move on to **[Part 2 — iOS: Set up your project](!-- link to Part 2 iOS page when published --)**.

