# Agent instructions: new Braid iOS prototype

You are helping create a new Braid **iOS** prototype: blank Xcode app + [braid-ios](https://github.com/SEEK-Jobs/braid-ios). Work step by step. Many steps are **user actions in Xcode** — guide them; do not pretend Xcode UI steps ran yourself.

> **Prerequisite:** `common.md` and `ios.md` complete — especially the disk-based SSH key `~/.ssh/id_ed25519_xcode`.

---

## Step 1: Choose a project name

Ask for (or confirm) the prototype name and a folder-safe name under `~/Code/` (e.g. `JobAlertSettings` or `job-alert-settings`).

Validate:

```bash
test ! -e ~/Code/<project-folder> && echo "OK" || echo "Folder already exists"
```

---

## Step 2: Create a blank iOS app in Xcode

Guide the user:

1. Open **Xcode** → **File → New → Project…**
2. **iOS** → **App** → **Next**
3. **Product Name:** their prototype name
4. **Organization Identifier:** e.g. `com.seek`
5. **Interface:** **SwiftUI**, **Language:** **Swift**
6. Save to `~/Code/`, create

**Verify:** project opens with `ContentView.swift`; **Cmd+B** succeeds.

---

## Step 3: Add the braid-ios package

Guide the user:

1. Select the project (blue icon) → **Package Dependencies** → **+**
2. URL:

   ```text
   git@github.com:SEEK-Jobs/braid-ios.git
   ```

3. Dependency rule: **Up to Next Major Version** (accept the suggested starting version)
4. Add product **BraidSwiftUI** to the app target

When Xcode asks for an SSH key: **Choose…** → `~/.ssh/id_ed25519_xcode` (private key, not `.pub`).

**Verify:** **braid-ios** appears under Package Dependencies without errors.

---

## Step 4: Smoke-test Braid in ContentView

Help them replace `ContentView` body with:

```swift
import BraidSwiftUI
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack(alignment: .leading, spacing: .medium) {
            Alert(
                tone: .info,
                text: "Braid is connected. You can start prototyping."
            )

            Button("Hello World") {
                print("hello")
            }
            .buttonStyle(braid: .solid)
            .buttonTone(.formAccent)
        }
        .padding()
    }
}
```

**Verify:** **Cmd+B** succeeds.

---

## Step 5: Run in the simulator

Guide: select a simulator → **Run** (▶) / **Cmd+R**.

**Verify:** alert and button appear.

---

## Step 6: Open the project in the AI IDE

Open `~/Code/<project-folder>` in Cursor / Copilot / Claude Code.

> Edit in the IDE; **run/preview in Xcode**.

---

## Conditional: Braid skill missing

If AI Toolkit / Braid skill was skipped, have them paste:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

## Done

Remind: reopen in **Xcode** + **Cmd+R**; open the same folder in the IDE for AI help. Docs: https://braid-native.skinfra.xyz/documentation/ios/documentation/braid
