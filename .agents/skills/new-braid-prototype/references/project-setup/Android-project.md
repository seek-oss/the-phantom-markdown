# Agent instructions: new Braid Android prototype

You are helping create a new Braid **Android** prototype: blank Android Studio app + [braid-android](https://github.com/SEEK-Jobs/braid-android) (`seek.braid:braid-compose`). Work step by step. Many steps are **user actions in Android Studio** — guide them; do not pretend UI steps ran yourself.

> **Prerequisite:** `common.md` and `android.md` complete — Cloudsmith Gradle token ready.

---

## Step 1: Choose a project name

Ask for (or confirm) a single folder-safe name under `~/Code/` (e.g. `JobAlertSettings` or `job-alert-settings`). Use that same name as the Android Studio project / app name.

Validate:

```bash
test ! -e ~/Code/<project-folder> && echo "OK" || echo "Folder already exists"
```

---

## Step 2: Create a blank Android app in Android Studio

Guide the user:

1. Open **Android Studio** → **New Project…**
2. **Empty Activity** → **Next**
3. Set:
   - **Name:** the confirmed project name
   - **Package name:** e.g. `com.seek.<projectfolder>` (lowercase, no hyphens in the last segment if needed)
   - **Save location:** `~/Code/<project-folder>`
   - **Minimum SDK:** API 26 or higher
   - **Build configuration language:** **Kotlin DSL**
4. Ensure the project uses **Jetpack Compose** (Empty Activity template does by default on current Android Studio)
5. Finish and wait for the first Gradle sync

**Verify:** project opens with `MainActivity.kt`; Gradle sync succeeds.

---

## Step 3: Add the Cloudsmith token

Android Studio creates `local.properties` in the project root (git-ignored) with `sdk.dir=…`. Edit it and add the token from machine setup:

```properties
cloudsmith.gradle=YOUR_TOKEN
```

Do not commit this file.

---

## Step 4: Add the Cloudsmith Maven repository

In `settings.gradle.kts`, ensure **dependencyResolutionManagement → repositories** includes SEEK’s Cloudsmith Gradle repo (keep existing `google()` / `mavenCentral()`).

Add a token read + maven block, for example:

```kotlin
val localProperties = java.util.Properties()
val localPropertiesFile = file("local.properties")
if (localPropertiesFile.exists()) {
    localPropertiesFile.inputStream().use { localProperties.load(it) }
}
val cloudsmithGradleToken =
    localProperties.getProperty("cloudsmith.gradle")
        ?: System.getenv("CLOUDSMITH_GRADLE_READ_TOKEN")

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven {
            url = uri("https://dl.cloudsmith.io/$cloudsmithGradleToken/seek/gradle/maven/")
        }
    }
}
```

Merge with the file’s existing structure — do not duplicate `dependencyResolutionManagement` blocks. Put the `localProperties` / token vars above the block if needed.

**Verify:** Gradle sync still succeeds after the edit.

---

## Step 5: Add the braid-compose dependency

In `app/build.gradle.kts`, add:

```kotlin
dependencies {
    // …
    implementation("seek.braid:braid-compose:20.2.0")
}
```

`20.2.0` is a known-good starting version. For the latest, check [Cloudsmith — braid-compose](https://app.cloudsmith.com/seek/gradle?page=1&query=name%3Abraid-compose) (SEEK login required).

**Verify:** Gradle sync succeeds and the dependency resolves (no “Could not find seek.braid:braid-compose” errors). Do **not** write the smoke-test UI until this passes.

**If sync fails on auth / missing package:** re-check `cloudsmith.gradle` in `local.properties`, Cloudsmith access (Lumos/Okta), and that the token was pasted without extra spaces.

---

## Step 6: Smoke-test Braid in MainActivity

Help them replace the `MainActivity` content with a minimal Braid screen. Keep the project’s real `package` declaration. Example:

```kotlin
package com.seek.example // use the project's package

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.padding
import androidx.compose.ui.Modifier
import seek.braid.compose.components.Alert
import seek.braid.compose.components.AlertNoticeTone
import seek.braid.compose.components.Button
import seek.braid.compose.components.ButtonTone
import seek.braid.compose.components.ButtonVariant
import seek.braid.compose.components.TextAlertNoticeContent
import seek.braid.compose.theme.Spacings
import seek.braid.compose.theme.WithBraidTheme
import seek.braid.compose.theme.seekJobs.SeekJobsTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            WithBraidTheme(theme = SeekJobsTheme()) {
                Column(
                    modifier = Modifier.padding(Spacings.medium),
                    verticalArrangement = Arrangement.spacedBy(Spacings.medium)
                ) {
                    Alert(tone = AlertNoticeTone.Info) { tone ->
                        TextAlertNoticeContent(
                            tone,
                            "Braid is connected. You can start prototyping."
                        )
                    }

                    Button(
                        text = "Hello World",
                        variant = ButtonVariant.Solid,
                        tone = ButtonTone.FormAccent,
                        onClick = { }
                    )
                }
            }
        }
    }
}
```

Remove unused default theme / scaffold imports if the build complains.

**Verify:** **Build → Make Project** (or the Run button’s build) succeeds.

---

## Step 7: Run on an emulator

Guide: start a **Pixel** emulator (or any device) → **Run** (▶).

**Verify:** info alert and “Hello World” button appear. Do **not** mark setup complete until this succeeds.

---

## Step 8: Open the project in the AI IDE

Open `~/Code/<project-folder>` in Cursor / Copilot / Claude Code.

> Edit in the IDE; **run/preview in Android Studio**.

---

## Conditional: Braid skill missing

If AI Toolkit / Braid skill was skipped, have them paste:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

## Done

Remind: reopen in **Android Studio** + Run; open the same folder in the IDE for AI help. Docs: https://braid-android.skinfra.xyz/
