# Setting up an IDE for AI prototyping

## Part 2 — iOS: Set up your project (Do this for every project)

> Creates a new Braid iOS prototype from the [ios-app-template](https://github.com/SEEK-Jobs/ios-app-template), so you can start building in Xcode and use your AI assistant in your IDE.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Note panel:** Please ensure you've completed **[Part 1 — iOS: Set up your machine](<!-- link to Part 1 iOS page -->)** (or the shared Git and AI Toolkit steps from [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759)) before continuing.

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

### Step 3: Rename the project in Xcode

The template project is named **Template**. Rename it so multiple prototypes are easy to tell apart.

1. Open **Xcode**
2. **File → Open…** and select `~/Code/<project-name>/Template.xcodeproj`
3. In the Project navigator (left sidebar), click the blue **Template** project icon once, then press **Enter**
4. Type your prototype name (e.g. `Job Alert Settings`) and press **Enter**
5. When Xcode asks to rename related items, click **Rename**

Update the **bundle identifier** so each prototype is unique:

1. Select the project in the navigator, then select the app **target**
2. Open the **Signing & Capabilities** tab
3. Change **Bundle Identifier** from `com.seek.Template` to something unique (e.g. `com.seek.<project-name>`)

---

### Step 4: Run the app in the simulator

1. In the Xcode toolbar, select your renamed **scheme** (formerly `Template`)
2. Select a simulator (e.g. **iPhone 16**)
3. Click **Run** (▶) or press **Cmd+R**

The first build may take a few minutes while Xcode resolves Swift packages (including Braid).

You should see a running app with Braid components (e.g. an info alert and a button).

---

### Step 5: Open the project in your IDE

Open the project folder in your AI-enabled IDE so your assistant can help with Swift and Braid code:

- **Cursor / VS Code / Copilot:** **File → Open Folder…** → select `~/Code/<project-name>`
- **Claude Code:** open the same folder from the terminal or your IDE workflow

> **Info panel:** You edit code in your IDE and **run/preview in Xcode**. There is no separate `pnpm start` step for iOS.

---

### [Conditional] Step 6: If AI Toolkit has not been installed

This step is only required if you were unable to install the [Braid skill using AI Toolkit](<!-- link to Part 1 iOS Step 5 -->) during Part 1.

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
