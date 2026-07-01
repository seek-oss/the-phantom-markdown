# Agent instructions: machine setup for Braid prototyping (Part 1)

You are helping set up a designer's machine to run, build and preview Braid projects locally. Work through each step below **in order**. After each step, verify it succeeded before continuing. If a step fails, stop and clearly explain what went wrong and what the user needs to do manually.

> **Note:** Some steps (marked below) require the user to act — do not attempt to skip or simulate them.

---

## Step 1: Install Node.js via nvm

Run the following commands one at a time and wait for each to complete:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

```bash
\. "$HOME/.nvm/nvm.sh"
```

```bash
nvm install --lts
```

Then verify:

```bash
node --version
```

If the output starts with `v22` or higher, continue. Otherwise stop and report the error.

---

## Step 2: Install Homebrew

> **User action required:** Homebrew's installer requires a password and may prompt interactively. Run the command below in your terminal yourself, follow any on-screen instructions, then tell me when it's done.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once the installer finishes, run these two lines to add Homebrew to your PATH (the installer will have printed similar instructions):

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Then verify:

```bash
brew --version
```

If a version number is printed, continue. Otherwise stop and report the error.

---

## Step 3: Install Git

```bash
brew install git
```

Verify:

```bash
git --version
```

If the output starts with `git version 2` or higher, continue. Otherwise stop and report the error.

---

## Step 4: Install pnpm and configure PATH

Install pnpm:

```bash
brew install pnpm
```

Ensure the shell config file exists:

```bash
touch ~/.zshrc
```

Append the pnpm PATH configuration to `~/.zshrc` if it isn't already there:

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

If the output starts with `v10` or higher, continue. Otherwise stop and report the error.

---

## Step 5: Create the Cursor global design rule

Create the rules directory if it doesn't exist:

```bash
mkdir -p ~/.cursor/rules
```

Write the rule file:

```bash
cat > ~/.cursor/rules/design-guidelines.mdc << 'EOF'
---
description: SEEK design guidelines for Braid projects
alwaysApply: true
---

# Design Guidelines

Read these guidelines: https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md
EOF
```

Confirm the file was created and has the correct content:

```bash
cat ~/.cursor/rules/design-guidelines.mdc
```

If the output matches the content above, continue. Otherwise stop and report the error.

---

## Step 6: Install IDE extensions

Run each of the following to install the recommended Cursor extensions:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
cursor --install-extension eamodio.gitlens
```

---

## Done

All Part 1 steps are complete. Tell the user their machine is ready for Part 2.

Ask whether they want to set up a new Braid web project now. If yes, follow the **new-braid-web-project** skill (`../new-braid-web-project/SKILL.md` from `.agents/skills/machine-setup/SKILL.md`, or `New-braid-web-project` when installed via AI Toolkit).
