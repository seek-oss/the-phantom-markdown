# Setting up an IDE for AI prototyping

## Part 1 — Android: Set up your machine (Do this once)

> Install the tools your machine needs to run, build and preview Braid Android prototypes locally.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install **Android Studio** and your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

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

### Step 2: Install Android Studio

Install **Android Studio** from **SEEK Self Service**, then launch it once to complete the setup wizard and install the Android SDK.

Verify that `adb` is available (optional):

```bash
adb --version
```

---

### Step 3: Set up GitHub access for Android packages

The Android app template depends on private SEEK packages hosted on GitHub Packages (including Braid via [android-app-platform](https://github.com/SEEK-Jobs/android-app-platform)).

> **Info panel:** You need a GitHub licence and access to the **SEEK-Jobs** organisation. See [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

#### Generate a GitHub token

1. Visit [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Name it `Android Studio GitHub`
4. Grant the **`read:packages`** permission (and **`repo`** if you will clone via HTTPS)
5. Generate the token and copy it — you **cannot** view it again
6. Click **Enable SSO** and authorise access to **SEEK-Jobs**

Keep your username and token handy — you'll add them to each Android project in Part 2.

---

### Step 4: Confirm access to android-app-template

In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/android-app-template.git HEAD
```

If this fails, you do not yet have access. Request access via your team or GitHub onboarding before continuing.

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

Install these extensions via your IDE's **Extensions** marketplace:

| Extension | ID |
| --- | --- |
| GitLens | `eamodio.gitlens` |

If you edit Kotlin in a VS Code–compatible IDE, consider the **Kotlin** extension (`fwcd.kotlin`).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — Android: Set up your project](<!-- link to Part 2 Android page when published -->)**.
