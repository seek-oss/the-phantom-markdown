# Setting up an IDE for AI prototyping

## Part 1 — Android: Set up your machine (Do this once)

> Install Android Studio and a GitHub Packages token for private SEEK Android packages. Complete **[Part 1 — Shared](<!-- link to Part 1 Shared -->)** first.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install **Android Studio** from **SEEK Self Service** (in addition to your AI-enabled IDE from Shared).

> **Note panel:** Please ensure you've completed **[Part 1 — Shared: Set up your machine](<!-- link to Part 1 Shared -->)** (Homebrew, Git, GitHub access for Terminal, SEEK AI Toolkit) before continuing.

---

### Step 1: Install Android Studio

Install **Android Studio** from **SEEK Self Service**, then launch it once to complete the setup wizard and install the Android SDK.

Verify that `adb` is available (optional):

```bash
adb --version
```

---

### Step 2: Set up GitHub access for Android packages

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

### Step 3: Confirm access to android-app-template

In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/android-app-template.git HEAD
```

If this fails, you do not yet have access. Request access via your team or GitHub onboarding before continuing.

---

### Step 4: Install IDE extensions (optional)

If you edit Kotlin in a VS Code–compatible IDE, consider the **Kotlin** extension (`fwcd.kotlin`).

GitLens is covered in [Part 1 — Shared](<!-- link to Part 1 Shared -->).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — Android: Set up your project](<!-- link to Part 2 Android page when published -->)**.
