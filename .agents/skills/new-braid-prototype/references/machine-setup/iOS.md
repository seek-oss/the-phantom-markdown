# Agent instructions: iOS machine setup

Complete `common.md` first. Then work through these iOS-only steps.

> **Before starting:** The user must install **Xcode** from **SEEK Self Service** (in addition to their AI IDE).

---

## Step 1: Install / launch Xcode

If Xcode is not installed, direct the user to **SEEK Self Service**. Then launch Xcode once to install iOS SDKs and accept the licence.

Verify:

```bash
xcodebuild -version
```

You should see a version number.

---

## Step 2: Create a disk-based SSH key for Xcode

Braid iOS prototypes depend on the private [braid-ios](https://github.com/SEEK-Jobs/braid-ios) package. **Xcode does not support SSH agents** (including 1Password). Create a **disk-based** key Xcode can select.

Ask for the user’s SEEK email if needed, then run (replace the email):

```bash
mkdir -p ~/.ssh
ssh-keygen -t ed25519 -C "your.name@seek.com.au" -f ~/.ssh/id_ed25519_xcode
```

Use a **passphrase** when prompted.

This creates:

- **Private key:** `~/.ssh/id_ed25519_xcode` — use in Xcode
- **Public key:** `~/.ssh/id_ed25519_xcode.pub` — add to GitHub

Keep 1Password SSH for Terminal (from `common.md`) — separate from this key.

> **NEVER tell the user the 1Password SSH agent works in Xcode.** Xcode does not support SSH agents — it needs this disk-based key.

---

## Step 3: Add the public key to GitHub

```bash
pbcopy < ~/.ssh/id_ed25519_xcode.pub
```

Guide the user:

1. GitHub → **Settings → SSH and GPG keys** → **New SSH key**
2. **Key type** = **Authentication Key**
3. Paste and save
4. **Configure SSO** → authorise **SEEK-Jobs**

---

## Step 4: Select the private key in Xcode

When Xcode prompts for an SSH key (usually while adding/resolving packages in project setup):

1. Choose **Choose…**
2. Select `~/.ssh/id_ed25519_xcode` (**not** the `.pub` file)
3. Enter the passphrase if prompted

---

## Step 5: IDE extensions (optional)

If they edit Swift in a VS Code–compatible IDE, suggest **Swift** (`swiftlang.swift-vscode`).

---

## Step 6: AI coding tools for Cursor (ask now)

Not required to scaffold a Braid prototype (project setup still uses Xcode UI), but **strongly recommended** for AI-assisted iteration afterward. Source of truth: [Candidate iOS Apps — AI Coding Agents](https://backstage.myseek.xyz/docs/default/system/candidate-ios-apps/AI%20Coding%20Agents/).

**At this step, ask the user** whether they want to install these tools **now**. Nudge yes — e.g. they improve how Cursor works with Xcode builds and tooling. Do **not** suggest deferring (“we can do this later”) unless they decline.

- If **yes** → install below, then continue
- If **no** → acknowledge briefly and continue to project setup

### xcsift

Parses `xcodebuild` / Swift build output into a token-efficient form for agents.

```bash
brew install xcsift
xcsift install-cursor --global
```

### Xcode MCP server (if Xcode 26.3+)

Lets Cursor use Xcode for builds, tests, docs, and more. Check version first:

```bash
xcodebuild -version
```

If **26.3 or later**, add to `~/.cursor/mcp.json` (merge with any existing `mcpServers`; use the standard name `xcode-tools`):

```json
{
  "mcpServers": {
    "xcode-tools": {
      "command": "xcrun",
      "args": ["mcpbridge"]
    }
  }
}
```

`xcrun mcpbridge` uses the active Xcode (`xcode-select`). If they have multiple installs, select the right one before relying on the MCP.

Skip this block if Xcode is older than 26.3.

> Do **not** treat exporting Xcode agent skills (`xcrun agent skills export…`) as part of this setup — that tooling is still evolving. Point curious users at the Backstage page instead.
---

## Done

Continue with `references/project-setup/ios-project.md`.
