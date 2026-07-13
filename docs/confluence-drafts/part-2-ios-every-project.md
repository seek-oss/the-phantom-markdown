# Setting up an IDE for AI prototyping

## Part 2 — iOS: Set up your project (Do this for every project)

> Creates a new blank iOS app in Xcode and adds [braid-ios](https://github.com/SEEK-Jobs/braid-ios) as a Swift package dependency, so you can start building in Xcode and use your AI assistant in your IDE.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Note panel:** Please ensure you've completed **[Part 1 — iOS: Set up your machine](<!-- link to Part 1 iOS page -->)** before continuing — especially the **disk-based SSH key for Xcode**, selecting that private key in Xcode, and **braid-ios access** (Part 1, Steps 3–6).

> **Info panel:** These instructions are for **iOS projects only**. Build and preview in **Xcode**. Use your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) to open the same project folder for assistant help.

---

### Step 1: Choose a project name

Before creating the project, decide what to call your prototype.

**Naming rules:**

- Use **letters, numbers, and spaces or hyphens** (e.g. `Job Alert Settings`, `seek-home-explore`)
- Keep it short and readable — this becomes your Xcode project and app name

In **Terminal**, check the folder does not already exist (use a folder-safe version of the name, e.g. `JobAlertSettings` or `job-alert-settings`):

```bash
test ! -e ~/Code/<project-folder> && echo "OK" || echo "Folder already exists"
```

If the folder already exists, pick a different name.

Use the confirmed folder name as `<project-folder>` in later steps.

---

### Step 2: Create a blank iOS app in Xcode

1. Open **Xcode**
2. **File → New → Project…** (or choose **Create New Project** on the welcome screen)
3. Select **iOS** → **App** → **Next**
4. Fill in:
   - **Product Name:** your prototype name (e.g. `Job Alert Settings`)
   - **Team:** your SEEK team (if prompted)
   - **Organization Identifier:** e.g. `com.seek` (bundle ID becomes something like `com.seek.Job-Alert-Settings`)
   - **Interface:** **SwiftUI**
   - **Language:** **Swift**
5. Click **Next**, save to `~/Code/`, and click **Create**

**Verify:** Xcode opens a new project with a default `ContentView.swift` and your app builds with **Cmd+B**.

---

### Step 3: Add the braid-ios package

1. In Xcode, select the **project** (blue icon) in the Project navigator
2. Open the **Package Dependencies** tab
3. Click **+** (or **File → Add Package Dependencies…**)
4. Enter the package URL:

   ```text
   git@github.com:SEEK-Jobs/braid-ios.git
   ```

5. Set dependency rule: **Up to Next Major Version**, starting at **3.0.0**
6. Click **Add Package**
7. When prompted for products, add **BraidSwiftUI** to your **app target** (check the box next to your app name), then click **Add Package**

The first resolve may take a few minutes. When Xcode asks for an SSH key, choose **Choose…** and select `~/.ssh/id_ed25519_xcode` (the **private** key from Part 1 — not the `.pub` file).

**Verify:** In the Project navigator, expand **Package Dependencies** — **braid-ios** should appear without errors.

> **Info panel:** Prefer the **SSH** URL above. Xcode uses the **disk-based** key from Part 1 (it does **not** use the 1Password SSH agent). If you paste an `https://github.com/…` URL instead, the git SSH rewrite from Part 1 is a safety net.

#### If you see “Missing package product” or “credentials were rejected”

Work through these in order:

1. Confirm Part 1 braid-ios access works in Terminal:

   ```bash
   git ls-remote git@github.com:SEEK-Jobs/braid-ios.git HEAD
   ```

2. Confirm Xcode is using the **disk-based private key** (`~/.ssh/id_ed25519_xcode`), not a 1Password/agent key and not the `.pub` file. Re-select it if Xcode prompts again.

3. Confirm the git SSH rewrite is set (optional safety net):

   ```bash
   git config --global --get-regexp url
   ```

4. In Xcode: **File → Packages → Reset Package Caches**, then **Resolve Package Versions** again.

5. If it still fails, remove and re-add the package:
   - Select the project (blue icon) → **Package Dependencies**
   - Select **braid-ios** and click **−** (minus) to remove it
   - **File → Add Package Dependencies…**
   - Enter: `git@github.com:SEEK-Jobs/braid-ios.git`
   - Set dependency rule: **Up to Next Major Version**, starting at **3.0.0**
   - Add the **BraidSwiftUI** product to your app target
   - When prompted, select `~/.ssh/id_ed25519_xcode` again

---

### Step 4: Smoke-test Braid in ContentView

Replace the body of `ContentView.swift` with a small Braid example so you know the package is wired correctly:

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

**Verify:** The file compiles with no red errors (`Cmd+B`).

---

### Step 5: Run the app in the simulator

1. In the Xcode toolbar, select your app **scheme**
2. Select a simulator (e.g. **iPhone 16**)
3. Click **Run** (▶) or press **Cmd+R**

You should see the info alert and Braid button from Step 4.

---

### Step 6: Open the project in your IDE

Open the project folder in your AI-enabled IDE so your assistant can help with Swift and Braid code:

- **Cursor / VS Code / Copilot:** **File → Open Folder…** → select `~/Code/<project-folder>`
- **Claude Code:** open the same folder from the terminal or your IDE workflow

> **Info panel:** You edit code in your IDE and **run/preview in Xcode**. There is no separate dev-server command for iOS.

---

### [Conditional] Step 7: If AI Toolkit has not been installed

This step is only required if you were unable to install the [Braid skill using AI Toolkit](<!-- link to Part 1 iOS Step 7 -->) during Part 1.

Copy and paste this prompt into your **Agent** chat:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

### From then on, anytime you open the project

1. Open the project in **Xcode** and press **Cmd+R** to run in the simulator
2. Open the same folder in your IDE when you want AI assistant help

For ongoing Braid guidance, use the **Braid skill** installed via AI Toolkit (`SEEK-braid`). Docs: [Braid iOS documentation](https://braid-native.skinfra.xyz/documentation/ios/documentation/braid).
