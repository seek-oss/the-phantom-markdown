# Agent instructions: common machine setup

You are helping set up a macOS machine for Braid prototyping. Work through each step **in order**. After each step, verify it succeeded before continuing. Skip steps that already work. If a step fails, stop and explain what the user needs to do manually.

> **Before starting:** Ensure the user has installed their AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.

> **User action required:** Some steps need the user to act (password prompts, browser SSO). Do not skip or simulate them.

---

## Step 1: Install Homebrew

> **User action required:** Homebrew’s installer requires a password and may prompt interactively. Ask the user to run the command in their own terminal, then tell you when it’s done.

In **Terminal**, run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When it finishes, follow the printed instructions to add Homebrew to your PATH. They'll look something like this — run both lines:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify:

```bash
brew --version
```

You should see a version number.

---

## Step 2: Install Git

In **Terminal**, run:

```bash
brew install git
```

Verify:

```bash
git --version
```

You should see a version number.

---

## Step 3: Set up GitHub access (Terminal)

The user needs a GitHub licence and access to the **SEEK-Jobs** organisation. For Terminal, `git`, and AI Toolkit, SSH keys in **1Password** are recommended.

If SSH is not working yet, read and follow `ssh-keys-1password.md` in this folder (agent-assisted setup).

Verify:

```bash
ssh -T git@github.com
```

You should see a success message mentioning the user’s GitHub username.

> **Note:** Platform-specific credentials (Xcode disk key, Android Cloudsmith token) are in the platform machine-setup files — not here.

---

## Step 4: Install SEEK AI Toolkit, Braid skill, and braid-ui rule

If `ai-toolkit` is already installed (e.g. this skill was launched from AI Toolkit), skip the tap/install — go straight to installing or verifying the **Braid skill** and **braid-ui rule**.

This step requires SEEK-Jobs GitHub access. If the user doesn’t have it yet, **skip** and continue to Step 5.

In **Terminal**, run:

```bash
# First time: add the tap
brew tap SEEK-Jobs/homebrew-tools git@github.com:SEEK-Jobs/homebrew-tools.git

# Install the CLI
brew install SEEK-Jobs/homebrew-tools/ai-toolkit

# Run the CLI
ai-toolkit
```

Once AI Toolkit is running, install the **Braid skill** and the **braid-ui rule**:

```bash
ai-toolkit install skill Braid --catalog seek-oss/braid-context/.agents@master
ai-toolkit install rule braid-ui --catalog seek-oss/braid-context/.agents@master
```

The user will be prompted to select their IDE (**Cursor**, **Claude Code**, or **Copilot**) and installation target (**Workspace** or user profile) for each install.

**Verify:** user confirms the Braid skill and braid-ui rule installed, or they explicitly skipped due to missing GitHub access.

---

## Step 5: Install GitLens (optional but recommended)

Install via the IDE **Extensions** marketplace. For Cursor, you can also run:

```bash
cursor --install-extension eamodio.gitlens
```

| Extension | ID |
| --- | --- |
| GitLens | `eamodio.gitlens` |

If install fails, note it but do not block — this step is optional.

Platform-specific extensions are in `web.md`, `ios.md`, `android.md`, and `email.md`.

---

## Done

Common machine setup is complete. Continue with the **platform** machine-setup file (`web.md`, `ios.md`, `android.md`, or `email.md`), then the matching project-setup file.
