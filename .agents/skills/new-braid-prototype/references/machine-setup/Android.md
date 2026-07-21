# Agent instructions: Android machine setup

Complete `common.md` first. Then work through these Android-only steps.

> **Before starting:** The user must install **Android Studio** from **SEEK Self Service** (in addition to their AI IDE).

---

## Step 1: Install / launch Android Studio

If Android Studio is not installed, direct the user to **SEEK Self Service**. Launch it once to finish the setup wizard and install the Android SDK.

Optional verify:

```bash
adb --version
```

---

## Step 2: Generate a GitHub Packages token

The Android app template depends on private SEEK packages on GitHub Packages (including Braid via [android-app-platform](https://github.com/SEEK-Jobs/android-app-platform)).

Guide the user:

1. Visit [github.com/settings/tokens](https://github.com/settings/tokens)
2. **Generate new token (classic)**
3. Name it `Android Studio GitHub`
4. Grant **`read:packages`** (and **`repo`** if cloning via HTTPS)
5. Generate and copy the token — they cannot view it again
6. **Enable SSO** → authorise **SEEK-Jobs**

Keep username + token handy for project setup (`local.properties`).

---

## Step 3: Confirm access to android-app-template

```bash
git ls-remote git@github.com:SEEK-Jobs/android-app-template.git HEAD
```

If this fails, they need SEEK-Jobs access / SSO before continuing.

---

## Step 4: IDE extensions (optional)

If they edit Kotlin in a VS Code–compatible IDE, suggest **Kotlin** (`fwcd.kotlin`).

---

## Done

Continue with `references/project-setup/android-project.md`.
