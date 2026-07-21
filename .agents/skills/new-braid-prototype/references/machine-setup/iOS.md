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

## Done

Continue with `references/project-setup/iOS-project.md`.
