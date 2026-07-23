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

Optional: create a **Pixel** emulator via **Tools → Device Manager → Create Virtual Device** (Phone → Pixel, default API level). Follow the prompts; the first time may also offer an **SDK Component Installer** — accept/install. They can also do this during project setup.

---

## Step 2: Get a Cloudsmith Gradle token

Braid Android packages are hosted on SEEK’s private [Cloudsmith](https://cloudsmith.com) Gradle repo (see [braid-android](https://github.com/SEEK-Jobs/braid-android)). Token guidance also lives in [Backstage artifact management docs](https://backstage.myseek.xyz/docs/default/component/artifact-management-docs/gradle/).

Guide the user:

1. Get access to **Cloudsmith** via **Lumos / Okta** (request **Cloudsmith → Member** if needed)
2. Sign in at [cloudsmith.com](https://cloudsmith.com) (use **app.cloudsmith.com**, not cloudsmith.io)
3. Open the SEEK Gradle repo: [https://app.cloudsmith.com/seek/gradle](https://app.cloudsmith.com/seek/gradle)
4. Open **Entitlement Tokens** in the sidebar → create/copy a **read-only** token

They will add it to each project’s `local.properties` during project setup:

```properties
cloudsmith.gradle=YOUR_TOKEN
```

Keep the token handy. Do **not** paste it into chat. Do not commit it.

If they can browse packages but see no Entitlement Tokens controls, they likely need Cloudsmith member access via Lumos first. Still stuck? Ask in `#support-cloudsmith`.

---

## Step 3: IDE extensions (optional)

If they edit Kotlin in a VS Code–compatible IDE, suggest **Kotlin** (`fwcd.kotlin`).

---

## Done

Continue with `references/project-setup/android-project.md`.
