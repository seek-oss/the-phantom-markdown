# Agent instructions: machine setup for Braid prototyping (Part 1)

You are helping set up a designer's machine to run, build, and preview Braid projects locally. Work through each step below **in order**. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do manually.

> **Before starting:** Ensure the user has installed their IDE of choice via **SEEK Self Service**. This guide assumes **Cursor** on macOS.

> **Note:** Some steps require the user to act — do not attempt to skip or simulate them.

---

## Step 1: Install Node.js

Open **Terminal** (press **Cmd+Space** and search for Terminal on Mac, or **Cmd+J** in Cursor). Run the following commands one at a time and wait for each to complete:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

```bash
\. "$HOME/.nvm/nvm.sh"
```

```bash
nvm install --lts
```

Verify:

```bash
node --version
```

You should see a version starting with `v22` or higher. If not, stop and report the error.

---

## Step 2: Install Homebrew

> **User action required:** Homebrew's installer requires a password and may prompt interactively. Ask the user to run the command below in their terminal themselves, follow any on-screen instructions, then tell you when it's done.

In **Terminal**, run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When it finishes, follow the printed instructions to add Homebrew to your PATH. They'll look something like this — run both lines:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify it worked:

```bash
brew --version
```

You should see a version number printed (e.g. `4.1.8`). If not, stop and report the error.

---

## Step 3: Install Git

In **Terminal**, run:

```bash
brew install git
```

Verify it worked:

```bash
git --version
```

You should see a version starting with `git version 2` or higher. If not, stop and report the error.

---

## Step 4: Install pnpm

In **Terminal**, run:

```bash
brew install pnpm
```

Ensure the shell config file exists:

```bash
touch ~/.zshrc
```

Append the pnpm PATH configuration to `~/.zshrc` **only if it isn't already there**:

```bash
cat >> ~/.zshrc << 'EOF'

export PNPM_HOME="$HOME/Library/pnpm"
case ":$PATH:" in
  *":$PNPM_HOME:"*) ;;
  *) export PATH="$PNPM_HOME:$PATH" ;;
esac
EOF
```

Apply the changes:

```bash
source ~/.zshrc
```

Verify:

```bash
pnpm --version
```

You should see a version starting with `10` or higher. If not, stop and report the error.

---

## Step 5: Install SEEK AI Toolkit

This step requires a GitHub license and access to the SEEK-Jobs organisation. If the user doesn't yet have access, **skip to Step 6** and let them know Part 2 includes a conditional workaround for Braid guidelines.

> **SSH keys:** The user will need SSH keys in 1Password to authenticate. See [setup details](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) and [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

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

The user will be prompted to select their IDE (Cursor, Claude Code, Copilot) and installation target (Workspace or user profile).

**Verify:** the user confirms the Braid skill installed successfully, or they explicitly skipped this step due to missing GitHub access.

---

## Step 6: Install IDE extensions (optional but recommended)

In **Terminal**, run:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
cursor --install-extension eamodio.gitlens
```

This installs:

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |
| GitLens | `eamodio.gitlens` |

If any extension fails to install, note it but do not block completion — this step is optional.

---

## Done

All Part 1 steps are complete. Tell the user their machine is ready for Part 2.

Point them to [Part 2: Setting up your project](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996) if they want to continue manually.

Ask whether they want to set up a new Braid web prototype now. If yes, follow the **new-braid-web-prototype** skill (`../new-braid-web-prototype/SKILL.md` from `.agents/skills/machine-setup/SKILL.md`, or `SEEK-new-braid-web-prototype` when installed via AI Toolkit).
