# Agent instructions: Email machine setup

Complete `common.md` first. Then work through these email-only steps.

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

## Step 2: Install Yarn

```bash
brew install yarn
```

Verify:

```bash
yarn --version
```

You should see a version number (Yarn 1.x is fine).

---

## Step 3: Cloudsmith npm auth for `@seek` packages

`@seek/braid-email-ui` is hosted on SEEK’s private Cloudsmith npm registry. Docs: [Accessing Cloudsmith with NPM](https://backstage.myseek.xyz/docs/default/component/artifact-management-docs/npm/access/).

Guide the user:

1. Get access to **Cloudsmith** via **Lumos / Okta** (request **Cloudsmith → Member** if needed)
2. Sign in at [app.cloudsmith.com](https://app.cloudsmith.com) (not cloudsmith.io)
3. Copy an **API key**: click your **initials** (top right) → **API key** / [API key settings](https://app.cloudsmith.com/user/settings/api-key/) — create or copy a key
4. Note your Cloudsmith **username** (shown under your name when you click initials — **not** your email; no `@`)

In **Terminal**, run:

```bash
npm config set '@seek:registry' https://npm.cloudsmith.io/seek/npm/
npm login --auth-type=legacy --registry=https://npm.cloudsmith.io/seek/npm/
```

When prompted:

| Prompt | Value |
| --- | --- |
| **Username** | Cloudsmith username (e.g. `cheryl-paulsen`) — **not** email |
| **Password** | Cloudsmith **API key** — **not** Okta / laptop password (typing is hidden; that is normal) |
| **Email** | SEEK work email is fine |

Do **not** paste the API key into chat.

**Verify:** `npm login` succeeds with no `E401`. If login fails, re-check username vs email and that the password was the API key. Still stuck? Ask in `#support-cloudsmith`.

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

Continue with `references/project-setup/email-project.md`.
