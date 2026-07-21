# Agent instructions: Email machine setup (Track B)

Complete `common.md` first. These steps are for **Track B** (Playroom + AI assistant).

> **Track A:** If the user only wants hosted Playroom, skip this file and go to `email-project.md` Track A.

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

## Step 2: Confirm access to the email repository

```bash
git ls-remote git@github.com:SEEK-Jobs/mjml-react-email-templates.git HEAD
```

If this fails, fix Terminal SSH (`ssh-keys-1password.md` / SEEK-Jobs access) before continuing.

---

## Step 3: Install Yarn

The email monorepo uses **Yarn 1.x** (not pnpm).

```bash
brew install yarn
```

Verify:

```bash
yarn --version
```

You should see a version number (Yarn 1.x).

---

## Step 4: IDE extensions (optional but recommended)

Via marketplace, or for Cursor:

```bash
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
```

| Extension | ID |
| --- | --- |
| Prettier | `esbenp.prettier-vscode` |
| ESLint | `dbaeumer.vscode-eslint` |

---

## Done

Continue with `references/project-setup/email-project.md` (Track B).
