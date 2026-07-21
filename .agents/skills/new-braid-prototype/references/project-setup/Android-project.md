# Agent instructions: new Braid Android prototype

You are helping create a new Braid **Android** prototype from [android-app-template](https://github.com/SEEK-Jobs/android-app-template). Work step by step.

> **Prerequisite:** `common.md` and `android.md` complete — GitHub Packages token ready.

---

## Step 1: Choose a project name

Ask for (or confirm) a name: lowercase, numbers, hyphens only.

Validate:

```bash
test ! -e ~/Code/<project-name> && echo "OK" || echo "Folder already exists"
```

---

## Step 2: Clone the Android app template

```bash
cd ~/Code
git clone git@github.com:SEEK-Jobs/android-app-template.git <project-name>
cd ~/Code/<project-name>
```

---

## Step 3: Add GitHub authentication

Create or edit `local.properties` in the project root (git-ignored):

```properties
github.username=YourGithubUsername
github.token=YourGithubToken
```

Use values from machine setup. Do not commit this file.

---

## Step 4: Rename the project

Help update:

- `app/src/main/res/values/strings.xml` → `app_name`
- `app/build.gradle.kts` → `applicationId = "com.seek.<project-name>"`
- Optional: `settings.gradle.kts` → `rootProject.name`

---

## Step 5: Open in Android Studio

Guide: **Open** → `~/Code/<project-name>` → wait for Gradle sync.

---

## Step 6: Run the app

Guide: emulator or device → **Run** (▶).

**Verify:** sample Braid Compose UI appears.

---

## Step 7: Open in the AI IDE

Open the same folder in Cursor / Copilot / Claude Code.

> Edit in the IDE; **run/preview in Android Studio**.

---

## Conditional: Braid skill missing

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

## Done

Remind: reopen in **Android Studio** + Run; open the folder in the IDE for AI help.
