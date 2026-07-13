# Setting up an IDE for AI prototyping

## Part 2 — Android: Set up your project (Do this for every project)

> Creates a new Braid Android prototype from the [android-app-template](https://github.com/SEEK-Jobs/android-app-template), so you can start building in Android Studio and use your AI assistant in your IDE.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Note panel:** Please ensure you've completed **[Part 1 — Shared](<!-- link to Part 1 Shared -->)** and **[Part 1 — Android](<!-- link to Part 1 Android page -->)** before continuing.

> **Info panel:** These instructions are for **Android projects only**. Build and preview in **Android Studio**. Use your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) to open the same project folder for assistant help.

---

### Step 1: Choose a project name

Before cloning, decide what to call your prototype.

**Naming rules:**

- Use **lowercase letters, numbers, and hyphens** only (e.g. `job-alert-settings`, `seek-home-explore`)
- **No spaces** — use hyphens instead (e.g. `my-cool-project`)
- Keep it short and readable

In **Terminal**, check the folder does not already exist:

```bash
test ! -e ~/Code/<project-name> && echo "OK" || echo "Folder already exists"
```

If the folder already exists, pick a different name.

Use the confirmed name as `<project-name>` in all following steps.

---

### Step 2: Clone the Android app template

In **Terminal**, run (replace `<project-name>`):

```bash
cd ~/Code
git clone git@github.com:SEEK-Jobs/android-app-template.git <project-name>
cd ~/Code/<project-name>
```

This template includes Braid Compose and the `seekJobs` theme pre-configured.

---

### Step 3: Add GitHub authentication

Create or edit `local.properties` in the project root (this file is git-ignored). Add your GitHub username and token from [Part 1 — Android, Step 2](<!-- link -->):

```properties
github.username=YourGithubUsername
github.token=YourGithubToken
```

Replace the placeholder values with your own.

---

### Step 4: Rename the project

Rename the template so each prototype is easy to identify.

**Display name** — edit `app/src/main/res/values/strings.xml` and change `app_name`:

```xml
<string name="app_name">Your Prototype Name</string>
```

**Application ID** — edit `app/build.gradle.kts` and update `applicationId` inside `defaultConfig`:

```kotlin
applicationId = "com.seek.<project-name>"
```

**Gradle project name** (optional) — edit `settings.gradle.kts`:

```kotlin
rootProject.name = "<Project Name>"
```

---

### Step 5: Open the project in Android Studio

1. Launch **Android Studio**
2. Choose **Open** and select `~/Code/<project-name>`
3. Wait for **Gradle sync** to finish (use **Sync Project with Gradle Files** if prompted)

The first sync may take several minutes while dependencies download.

---

### Step 6: Run the app

1. Set up an emulator via **Tools → Device Manager → Create Device**, or connect a physical device
2. Select the device in the toolbar
3. Click **Run** (▶)

You should see a running app with Braid Compose components (e.g. an alert and buttons).

---

### Step 7: Open the project in your IDE

Open the same project folder in your AI-enabled IDE:

- **Cursor / VS Code / Copilot:** **File → Open Folder…** → select `~/Code/<project-name>`
- **Claude Code:** open the same folder from the terminal or your IDE workflow

> **Info panel:** You edit code in your IDE and **run/preview in Android Studio**. There is no separate dev-server command for Android.

---

### [Conditional] Step 8: If AI Toolkit has not been installed

This step is only required if you were unable to install the [Braid skill using AI Toolkit](<!-- link to Part 1 Shared Step 5 -->) during Part 1 — Shared.

Copy and paste this prompt into your **Agent** chat:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

### From then on, anytime you open the project

1. Open the project in **Android Studio** and click **Run** (▶)
2. Open the same folder in your IDE when you want AI assistant help

For ongoing Braid guidance, use the **Braid skill** installed via AI Toolkit (`SEEK-braid`).
