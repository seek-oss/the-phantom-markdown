# Setting up an IDE for AI prototyping

## Part 2 — iOS: Set up your project (Do this for every project)

> Creates a new Braid iOS prototype from the [ios-app-template](https://github.com/SEEK-Jobs/ios-app-template), so you can start building in Xcode and use your AI assistant in your IDE.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Note panel:** Please ensure you've completed **[Part 1 — iOS: Set up your machine](<!-- link to Part 1 iOS page -->)** before continuing — especially **SSH in 1Password** and the **git SSH configuration** (Part 1, Steps 3–5).

> **Info panel:** These instructions are for **iOS projects only**. Build and preview in **Xcode**. Use your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) to open the same project folder for assistant help.

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

### Step 2: Clone the iOS app template

In **Terminal**, run (replace `<project-name>`):

```bash
cd ~/Code
git clone git@github.com:SEEK-Jobs/ios-app-template.git <project-name>
cd ~/Code/<project-name>
```

This template includes Braid pre-configured via Swift Package Manager.

---

### Step 3: Open the project and resolve the Braid package

1. Open **Xcode**
2. **File → Open…** and select `~/Code/<project-name>/Template.xcodeproj`
3. Wait for Xcode to start resolving packages, or trigger it manually:
   - **File → Packages → Reset Package Caches**
   - **File → Packages → Resolve Package Versions**

The first resolve may take a few minutes. With Part 1 SSH configured, Xcode fetches [braid-ios](https://github.com/SEEK-Jobs/braid-ios) over SSH automatically.

**Verify:** In the Project navigator, expand **Package Dependencies** — **braid-ios** should appear without errors.

> **Info panel:** The template stores the package URL as `https://github.com/SEEK-Jobs/braid-ios`. You do not need to change this in Xcode — the git SSH configuration from Part 1 Step 4 handles authentication.

#### If you see “Missing package product 'Braid'” or “credentials were rejected”

Work through these in order:

1. Confirm Part 1 Steps 3–5 work in Terminal:

   ```bash
   ssh -T git@github.com
   git ls-remote git@github.com:SEEK-Jobs/braid-ios.git HEAD
   ```

2. Confirm the git SSH rewrite is set:

   ```bash
   git config --global --get-regexp url
   ```

3. In Xcode: **File → Packages → Reset Package Caches**, then **Resolve Package Versions** again.

4. If it still fails, **remove and re-add** the package using an SSH URL:
   - Select the **Template** project (blue icon) in the navigator
   - Open the **Package Dependencies** tab
   - Select **braid-ios** and click **−** (minus) to remove it
   - **File → Add Package Dependencies…**
   - Enter: `git@github.com:SEEK-Jobs/braid-ios.git`
   - Set dependency rule: **Up to Next Major Version**, starting at **1.50.0**
   - Add the **Braid** product to the **Template** target

5. If SSH works in Terminal but not in Xcode, quit Xcode and reopen the project from Terminal (so Xcode inherits your SSH agent):

   ```bash
   open -a Xcode ~/Code/<project-name>/Template.xcodeproj
   ```

---

### Step 4: Rename the project in Xcode

The template project is named **Template**. Rename it so multiple prototypes are easy to tell apart.

1. In the Project navigator (left sidebar), click the blue **Template** project icon once, then press **Enter**
2. Type your prototype name (e.g. `Job Alert Settings`) and press **Enter**
3. When Xcode asks to rename related items, click **Rename**

Update the **bundle identifier** so each prototype is unique:

1. Select the project in the navigator, then select the app **target**
2. Open the **Signing & Capabilities** tab
3. Change **Bundle Identifier** from `com.seek.Template` to something unique (e.g. `com.seek.<project-name>`)

---

### Step 5: Run the app in the simulator

1. In the Xcode toolbar, select your renamed **scheme** (formerly `Template`)
2. Select a simulator (e.g. **iPhone 16**)
3. Click **Run** (▶) or press **Cmd+R**

You should see a running app with Braid components (e.g. an info alert and a button).

---

### Step 6: Open the project in your IDE

Open the project folder in your AI-enabled IDE so your assistant can help with Swift and Braid code:

- **Cursor / VS Code / Copilot:** **File → Open Folder…** → select `~/Code/<project-name>`
- **Claude Code:** open the same folder from the terminal or your IDE workflow

> **Info panel:** You edit code in your IDE and **run/preview in Xcode**. There is no separate dev-server command for iOS.

---

### [Conditional] Step 7: If AI Toolkit has not been installed

This step is only required if you were unable to install the [Braid skill using AI Toolkit](<!-- link to Part 1 iOS Step 6 -->) during Part 1.

Copy and paste this prompt into your **Agent** chat:

```
Read all SEEK design guidelines upfront at: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md and https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md

Follow all guidelines from those files. Let me know when this has been done.
```

---

### From then on, anytime you open the project

1. Open the project in **Xcode** and press **Cmd+R** to run in the simulator
2. Open the same folder in your IDE when you want AI assistant help

For ongoing Braid guidance, use the **Braid skill** installed via AI Toolkit (`SEEK-braid`).
