# Agent instructions: SSH keys in 1Password (Terminal GitHub auth)

Use this reference when Terminal GitHub SSH fails during common machine setup (`ssh -T git@github.com` fails, or private `git clone` / `brew tap` cannot authenticate).

**Goal for this skill:** authenticate to `git@github.com` from Terminal so the user can clone SEEK repos, install AI Toolkit, and use git over SSH.

**Not the goal here:** set up an existing project’s remote, or require commit signing (optional at the end).

**Xcode note:** This flow does **not** authenticate Xcode SPM. For iOS package resolve, use the disk-based key in `iOS.md`.

---

## Agent behavior

Work **step by step**. Some steps are **manual** — wait for the user to confirm before continuing. Do not skip ahead.

Do **not** ask for an org/repo name at the start (machine setup may have no project yet).

---

## Step 1 — MANUAL: Create a new SSH key in 1Password

Ask the user to do this themselves:

1. Open **1Password** on their Mac
2. **New Item** → **SSH Key**
3. Name it something like `GitHub Auth Key`
4. Click **Generate** (ed25519)
5. **Save**
6. Open the item → copy the full **Public Key** (`ssh-ed25519 AAAA…`)

When they have it, they should tell you: “I have my public key, it is: \<paste\>”

Keep the public key for later steps.

---

## Step 2 — AGENT: Configure `~/.ssh/config` for the 1Password SSH agent

Check whether `~/.ssh/config` exists and already has an `IdentityAgent` line pointing at the 1Password socket.

If missing, create or update `~/.ssh/config` so it includes:

```sshconfig
Host *
    IdentityAgent "~/Library/Group Containers/2BUA8C4S2C.com.1password/t/agent.sock"
```

Do not remove unrelated existing Host entries unless they conflict.

---

## Step 3 — MANUAL: Enable the 1Password SSH agent

Ask the user to:

1. Open **1Password → Settings (⌘,) → Developer**
2. Turn **Use the SSH agent** on
3. Tell you when done

---

## Step 4 — MANUAL: Add the SSH key to GitHub (Authentication)

Ask the user to:

1. Copy the **Public Key** from the 1Password item (Step 1)
2. Go to https://github.com/settings/keys
3. **New SSH key** → **Key type** = **Authentication Key** → paste → save
4. Click **Configure SSO** (or **Enable SSO**) and authorise access to **SEEK-Jobs**
5. Tell you when done

> **Optional (not required for this skill):** They may also add the same public key as a **Signing Key** if they want signed commits later.

---

## Step 5 — AGENT: Verify Terminal SSH auth

Run:

```bash
ssh -T git@github.com
```

Success: a message that includes their GitHub username.

If it fails, troubleshoot in order: SSH agent enabled (Step 3), `IdentityAgent` config (Step 2), Authentication key + SEEK-Jobs SSO (Step 4), 1Password unlocked.

When auth works, return to `common.md` and continue (AI Toolkit / GitLens).

---

## Optional — Git identity and commit signing

Only if the user asks for signed commits, or you need `user.name` / `user.email` unset later.

**Git identity** (if missing):

```bash
git config --global user.name "Their Name"
git config --global user.email "them@seek.com.au"
```

Ask for name and work email first.

**Commit signing with the same 1Password key** (optional):

```bash
git config --global gpg.format ssh
git config --global gpg.ssh.program /Applications/1Password.app/Contents/MacOS/op-ssh-sign
git config --global commit.gpgsign true
git config --global user.signingkey "<PUBLIC_KEY>"
```

They should also add the public key as a **Signing Key** on GitHub (Step 4 optional).

Do **not** run empty test commits or `git remote set-url` during machine setup unless you are already inside a repo and the user asked for that.
