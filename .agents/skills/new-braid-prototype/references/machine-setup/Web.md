# Agent instructions: Web machine setup

Complete `common.md` first. Then work through these Web-only steps. Skip anything already installed.

**Source guide:** [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759/Part+1+Do+once)

---

## Step 1: Install Node.js

In **Terminal**, run:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

\. "$HOME/.nvm/nvm.sh"

nvm install --lts
```

Verify:

```bash
node --version
```

You should see a version number.

---

## Step 2: Install pnpm

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
grep -q 'PNPM_HOME' ~/.zshrc && echo "Already configured" || cat >> ~/.zshrc << 'EOF'

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

You should see a version number.

---

## Step 3: Install IDE extensions (optional but recommended)

Via Extensions marketplace, or for Cursor:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
```

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |

GitLens is in `common.md`.

---

## Done

Continue with `references/project-setup/Web-project.md`.
