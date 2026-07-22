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

Optional: create a **Pixel** emulator via **Tools → Device Manager → Create Virtual Device** (Phone → Pixel, default API level). They can also do this during project setup.

---

## Step 2: Get a Cloudsmith Gradle token

Braid Android packages are hosted on SEEK’s private [Cloudsmith](https://cloudsmith.com) Gradle repo (see [braid-android](https://github.com/SEEK-Jobs/braid-android)). Token guidance also lives in [Backstage artifact management docs](https://backstage.myseek.xyz/docs/default/component/artifact-management-docs/).

Guide the user:

1. Get access to **Cloudsmith** via **Lumos / Okta**
2. Open and sign in at [cloudsmith.com](https://cloudsmith.com)
3. Open the **Gradle** repository settings
4. Copy the **entitlement token**

They will add it to each project’s `local.properties` during project setup:

```properties
cloudsmith.gradle=YOUR_TOKEN
```

Keep the token handy. Do not commit it.

---

## Step 3: IDE extensions (optional)

If they edit Kotlin in a VS Code–compatible IDE, suggest **Kotlin** (`fwcd.kotlin`).

---

## Done

Continue with `references/project-setup/android-project.md`.
