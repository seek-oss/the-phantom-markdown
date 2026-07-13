# Setting up an IDE for AI prototyping

## Part 1 — Web: Set up your machine (Do this once)

> Install Node.js, pnpm, and web IDE extensions for Braid web prototypes. Complete **[Part 1 — Shared](<!-- link to Part 1 Shared -->)** first.

<!-- Confluence: add Table of Contents macro (exclude page title) -->

> **Note panel:** Please ensure you've completed **[Part 1 — Shared: Set up your machine](<!-- link to Part 1 Shared -->)** (Homebrew, Git, GitHub access, SEEK AI Toolkit) before continuing.

---

### Step 1: Install Node.js

Open **Terminal** (press **Cmd+Space** and search for Terminal on Mac) and run:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

\. "$HOME/.nvm/nvm.sh"

nvm install --lts
```

Verify:

```bash
node --version
```

You should see a version starting with `v22` or higher.

---

### Step 2: Install pnpm

In **Terminal**, run:

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

You should see a version starting with `10` or higher.

---

### Step 3: Install IDE extensions (optional but recommended)

Install via your IDE's **Extensions** marketplace, or (for Cursor) from **Terminal**:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
```

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |

GitLens is covered in [Part 1 — Shared](<!-- link to Part 1 Shared -->).

---

### Done!

> **Note panel:** You can now move on to **[Part 2 — Web: Setting up your project](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996)**.
