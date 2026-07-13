# Setting up an IDE for AI prototyping

## Part 1 — iOS: Set up your machine (Do this once)

> Install Xcode and a disk-based SSH key so Xcode can fetch the private [braid-ios](https://github.com/SEEK-Jobs/braid-ios) package. Complete **[Part 1 — Shared](<!-- link to Part 1 Shared -->)** first.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Before starting:** Install **Xcode** from **SEEK Self Service** (in addition to your AI-enabled IDE from Shared).

> **Note panel:** Please ensure you've completed **[Part 1 — Shared: Set up your machine](<!-- link to Part 1 Shared -->)** (Homebrew, Git, GitHub access for Terminal, SEEK AI Toolkit) before continuing.

---

### Step 1: Install Xcode

Install **Xcode** from **SEEK Self Service**, then launch Xcode once to install the iOS SDKs and accept the licence agreement.

Verify:

```bash
xcodebuild -version
```

You should see an Xcode version printed.

---

### Step 2: Create a disk-based SSH key for Xcode

Braid iOS prototypes depend on the private [braid-ios](https://github.com/SEEK-Jobs/braid-ios) Swift package. **Xcode does not support SSH agents** (including 1Password), so it cannot use the Terminal SSH setup from Shared. Create a **disk-based** key that Xcode can select directly.

> **Info panel:** You need a GitHub licence and access to the **SEEK-Jobs** organisation. See [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended). Keep 1Password SSH for Terminal/`git`/AI Toolkit — that is separate from this Xcode key.

In **Terminal**, run (replace the email with your SEEK email):

```bash
mkdir -p ~/.ssh
ssh-keygen -t ed25519 -C "your.name@seek.com.au" -f ~/.ssh/id_ed25519_xcode
```

Use a **passphrase** when prompted (recommended by SEEK guidance).

This creates:

- **Private key:** `~/.ssh/id_ed25519_xcode` (no extension) — use this in Xcode
- **Public key:** `~/.ssh/id_ed25519_xcode.pub` — add this to GitHub

---

### Step 3: Add the public key to GitHub

Copy the public key:

```bash
pbcopy < ~/.ssh/id_ed25519_xcode.pub
```

Then in GitHub:

1. Go to **Settings → SSH and GPG keys**
2. Click **New SSH key**
3. Set **Key type** = **Authentication Key**
4. Paste the public key and save
5. Click **Configure SSO** and authorise access to **SEEK-Jobs**

These steps align with [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

---

### Step 4: Select the private key in Xcode

When Xcode prompts for an SSH key (for example while adding or resolving a package in Part 2):

1. Choose **Choose…**
2. Select the **private** key file: `~/.ssh/id_ed25519_xcode`
3. **Do not** select the `.pub` file

Enter the passphrase if prompted.

You'll add the `braid-ios` package itself in Part 2.

---

### Step 5: Install IDE extensions (optional)

If you also edit Swift in a VS Code–compatible IDE, consider the **Swift** extension (`swiftlang.swift-vscode`).

GitLens is covered in [Part 1 — Shared](<!-- link to Part 1 Shared -->).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — iOS: Set up your project](<!-- link to Part 2 iOS page when published -->)**.
