# Setting up an IDE for AI prototyping

## Part 1 — iOS: Set up your machine (Do this once)

> Install the tools your machine needs to run, build and preview Braid iOS prototypes locally.



> **Before starting:** Install **Xcode** and your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **Already completed [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759)?** If you have already set up Git and the SEEK AI Toolkit for web prototyping, you can skip Step 1 and Step 7 below — but still complete **Steps 3–6** (Xcode needs its own disk-based SSH key).

---



### Step 1: Install Git

Open **Terminal** (press **Cmd+Space** and search for Terminal on Mac) and run:

```bash
brew install git
```

If Homebrew is not installed, complete Steps 2–4 of [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759) first.

Verify:

```bash
git --version
```

You should see a version starting with `git version 2` or higher.

---



### Step 2: Install Xcode

Install **Xcode** from **SEEK Self Service**, then launch Xcode once to install the iOS SDKs and accept the licence agreement.

Verify:

```bash
xcodebuild -version
```

You should see an Xcode version printed.

---



### Step 3: Create a disk-based SSH key for Xcode

Braid iOS prototypes depend on the private [braid-ios](https://github.com/SEEK-Jobs/braid-ios) Swift package. **Xcode does not support SSH agents** (including 1Password), so it cannot use the same agent-based SSH setup as Terminal for web tooling. Create a **disk-based** key that Xcode can select directly.

> **Info panel:** You need a GitHub licence and access to the **SEEK-Jobs** organisation. See [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended). For Terminal/`git`/AI Toolkit you can still use [SSH keys in 1Password](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) — that is separate from this Xcode key.

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



### Step 4: Add the public key to GitHub

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



### Step 5: Select the private key in Xcode

When Xcode prompts for an SSH key (for example while adding or resolving a package):

1. Choose **Choose…**
2. Select the **private** key file: `~/.ssh/id_ed25519_xcode`
3. **Do not** select the `.pub` file

Enter the passphrase if prompted.

---



### Step 6: Configure git HTTPS → SSH and confirm braid-ios access

When you add braid-ios in Part 2, prefer the SSH package URL. This one-time git configuration is a safety net if Xcode stores an `https://github.com/…` URL instead — Swift Package Manager still uses git to fetch packages.

In **Terminal**, run:

```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

Verify the setting:

```bash
git config --global --get-regexp url
```

You should see `url.git@github.com:.insteadof https://github.com/`.

Confirm access to braid-ios:

```bash
git ls-remote git@github.com:SEEK-Jobs/braid-ios.git HEAD
```

If this fails, check that your **Xcode disk key** is added to GitHub with **SEEK-Jobs SSO** authorised (Steps 3–4), and that Terminal SSH can reach GitHub (1Password agent or your disk key).

---



### Step 7: Install [SEEK AI Toolkit](https://backstage.myseek.xyz/docs/default/component/seek-ai-toolkit/)

This step requires a GitHub licence and access to the SEEK-Jobs organisation. If you don't yet have access, skip to Step 8.

In **Terminal**, run:

```bash
# First time: add the tap
brew tap SEEK-Jobs/homebrew-tools git@github.com:SEEK-Jobs/homebrew-tools.git

# Install the CLI
brew install SEEK-Jobs/homebrew-tools/ai-toolkit

# Run the CLI
ai-toolkit
```

Once AI Toolkit is running, install the **Braid skill**:

```bash
ai-toolkit install skill Braid --catalog seek-oss/braid-context/.agents@master
```

You will be prompted to select your IDE (**Cursor**, **Claude Code**, or **Copilot**) and installation target (**Workspace** or user profile).

---



### Step 8: Install IDE extensions (optional but recommended)

Install these extensions via your IDE's **Extensions** marketplace (names are the same across VS Code–compatible editors):


| Extension | ID                |
| --------- | ----------------- |
| GitLens   | `eamodio.gitlens` |


If you also edit Swift in a VS Code–compatible IDE, consider the **Swift** extension (`swiftlang.swift-vscode`).

---



### Done!

> **Note panel:** You can now move on to **[Part 2 — iOS: Set up your project](!-- link to Part 2 iOS page when published --)**.

