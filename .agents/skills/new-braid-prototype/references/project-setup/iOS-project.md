# Agent instructions: new Braid iOS prototype

You are helping create a new Braid **iOS** prototype: blank Xcode app + [braid-ios](https://github.com/SEEK-Jobs/braid-ios). Work step by step. Many steps are **user actions in Xcode** — guide them; do not pretend Xcode UI steps ran yourself.

> **Prerequisite:** `common.md` and `ios.md` complete — especially the disk-based SSH key `~/.ssh/id_ed25519_xcode`.

---

## Step 1: Choose a project name

Ask for (or confirm) a single folder-safe name under `~/Code/` (e.g. `JobAlertSettings` or `job-alert-settings`). Use that same name as the Xcode **Product Name**.

Validate:

```bash
test ! -e ~/Code/<project-folder> && echo "OK" || echo "Folder already exists"
```

---

## Step 2: Create a blank iOS app in Xcode

Guide the user:

1. Open **Xcode** → **File → New → Project…**
2. **iOS** → **App** → **Next**
3. **Product Name:** the confirmed project name
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
4. When Xcode shows the products list, ensure **BraidSwiftUI** is checked for the **app target**, then **Add Package**

   Xcode can resolve the package **without** linking the product. Confirm **BraidSwiftUI** is listed under the app target → **General** → **Frameworks, Libraries, and Embedded Content**.

When Xcode asks for an SSH key: **Choose…** → `~/.ssh/id_ed25519_xcode` (private key, not `.pub`).

**Verify (both required):**

1. **braid-ios** appears under **Package Dependencies** without errors
2. **BraidSwiftUI** is linked to the app target

Agent check (preferred): confirm `BraidSwiftUI` appears in `packageProductDependencies` / `XCSwiftPackageProductDependency` in `*.xcodeproj/project.pbxproj`. Do **not** write the smoke-test `ContentView` until this passes.

**If the package resolved but BraidSwiftUI is missing from the target:**

1. Select the project (blue icon) → select the **app target**
2. **General** → **Frameworks, Libraries, and Embedded Content** → **+**
3. Choose **BraidSwiftUI** → **Add**

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
            .buttonStyle(.solid)
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

**Verify:** alert and button appear. Do **not** mark setup complete until this succeeds.

---

## Step 6: Open the project in the AI IDE

Open `~/Code/<project-folder>` in Cursor / Copilot / Claude Code.

> Edit in the IDE; **run/preview in Xcode**.

---

## Done

Remind: reopen in **Xcode** + **Cmd+R**; open the same folder in the IDE for AI help. Docs: https://braid-native.skinfra.xyz/documentation/ios/documentation/braid
