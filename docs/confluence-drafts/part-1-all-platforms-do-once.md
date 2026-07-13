# Setting up an IDE for AI prototyping

## Part 1: Set up your machine (Do this once)

> Install the tools your machine needs to run, build and preview Braid prototypes locally — for **Web**, **iOS**, **Android**, and **Email**.



> **Before starting:** Install your AI-enabled IDE (Cursor, Claude Code, or GitHub Copilot) via **SEEK Self Service**.
>
> - **iOS only:** Also install **Xcode** from SEEK Self Service.
> - **Android only:** Also install **Android Studio** from SEEK Self Service.
> - **Email — Track A (Playroom only):** No machine setup required. Open [Braid Email Playroom](https://braid-email.skinfra.xyz/playroom/) in your browser (SEEK SSO sign-in required) and skip this page. Use **Track B** below if you want an AI assistant with full project context.

> **Info panel:** You do not need every step. Follow the **All platforms** steps, then only the steps marked for the platform(s) you use. Skip anything labelled for a platform you are not setting up.



### What you need by platform


| Step                    | Web | iOS | Android | Email (Track B) |
| ----------------------- | --- | --- | ------- | --------------- |
| 1. Administrator access | ✓   | ✓   | ✓       | ✓               |
| 2. Homebrew             | ✓   | ✓   | ✓       | ✓               |
| 3. Git                  | ✓   | ✓   | ✓       | ✓               |
| 4. Node.js              | ✓   | —   | —       | ✓               |
| 5a. pnpm                | ✓   | —   | —       | —               |
| 5b. Yarn                | —   | —   | —       | ✓               |
| 6a. Xcode               | —   | ✓   | —       | —               |
| 6b. Android Studio      | —   | —   | ✓       | —               |
| 7. GitHub access        | ✓   | ✓   | ✓       | ✓               |
| 8. SEEK AI Toolkit      | ✓   | ✓   | ✓       | ✓               |
| 9. IDE extensions       | ✓   | ✓   | ✓       | ✓               |


---



### Step 1: Request administrator access

> **All platforms**

To install software you must first **Request administrator access** in the top right-hand menu of your machine (checkmark icon).



---



### Step 2: Install Homebrew

> **All platforms**

In **Terminal** (press **Cmd+Space** and search for Terminal on Mac), run:

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

You should see a version number printed (e.g. `4.1.8`).

---



### Step 3: Install Git

> **All platforms**

In **Terminal**, run:

```bash
brew install git
```

Verify:

```bash
git --version
```

You should see a version starting with `git version 2` or higher.

---



### Step 4: Install Node.js

> **Web and Email only** — skip if you are only setting up iOS or Android.

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

You should see a version starting with `v22` or higher.

---



### Step 5: Install a JavaScript package manager

> **Web and Email only** — skip if you are only setting up iOS or Android. Web uses **pnpm**; Email uses **Yarn 1.x**. Install only what you need.



#### 5a. Install pnpm (Web)

> **Web only**

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

#### 5b. Install Yarn (Email)

> **Email only** — the email monorepo uses **Yarn 1.x** (not pnpm).

In **Terminal**, run:

```bash
brew install yarn
```

Verify:

```bash
yarn --version
```

You should see version `1.x`.

---



### Step 6: Install platform SDKs

> **iOS and Android only** — skip if you are only setting up Web or Email.



#### 6a. Install Xcode (iOS)

> **iOS only**

Install **Xcode** from **SEEK Self Service**, then launch Xcode once to install the iOS SDKs and accept the licence agreement.

Verify:

```bash
xcodebuild -version
```

You should see an Xcode version printed.

#### 6b. Install Android Studio (Android)

> **Android only**

Install **Android Studio** from **SEEK Self Service**, then launch it once to complete the setup wizard and install the Android SDK.

Verify that `adb` is available (optional):

```bash
adb --version
```

---



### Step 7: Set up GitHub access

> **All platforms** need GitHub access for the SEEK AI Toolkit (Step 8). Some platforms have extra one-time checks or credentials — complete only the subsections for platforms you use.

You'll need a GitHub licence and access to the **SEEK-Jobs** organisation. SSH keys in 1Password are recommended:

- Follow the developer [setup guide](https://myseek.atlassian.net/wiki/spaces/DP/blog/2020/09/14/857116358) + [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended)
- Or use the [Agent-assisted copy and paste prompt](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5606015700) (non-engineer friendly)

Verify GitHub SSH access:

```bash
ssh -T git@github.com
```

You should see a success message mentioning your GitHub username.

#### 7a. Confirm email repository access (Email)

> **Email only**

In **Terminal**, run:

```bash
git ls-remote git@github.com:SEEK-Jobs/mjml-react-email-templates.git HEAD
```

If this fails, you do not yet have access. Request access via your team or [GitHub onboarding](https://myseek.atlassian.net/wiki/spaces/DP/pages/2169283073/GitHub+Onboarding#Optional---but-highly-recommended).

#### 7b. Disk-based SSH key for Xcode (iOS)

> **iOS only** — Braid iOS prototypes add [braid-ios](https://github.com/SEEK-Jobs/braid-ios) as a Swift package dependency in a blank Xcode app (Part 2). **Xcode does not support SSH agents** (including 1Password), so it cannot use the agent-based SSH setup from Step 7 above. Create a **disk-based** key that Xcode can select directly. Keep 1Password SSH for Terminal/`git`/AI Toolkit if you already use it.

**Create the key** (replace the email with your SEEK email):

```bash
mkdir -p ~/.ssh
ssh-keygen -t ed25519 -C "your.name@seek.com.au" -f ~/.ssh/id_ed25519_xcode
```

Use a **passphrase** when prompted. This creates:

- **Private key:** `~/.ssh/id_ed25519_xcode` (no extension) — use this in Xcode
- **Public key:** `~/.ssh/id_ed25519_xcode.pub` — add this to GitHub

**Add the public key to GitHub:**

```bash
pbcopy < ~/.ssh/id_ed25519_xcode.pub
```

1. Go to **Settings → SSH and GPG keys** → **New SSH key**
2. Set **Key type** = **Authentication Key**, paste the key, and save
3. Click **Configure SSO** and authorise access to **SEEK-Jobs**

**Select the private key in Xcode** when prompted (for example while adding or resolving a package):

1. Choose **Choose…**
2. Select `~/.ssh/id_ed25519_xcode` (**not** the `.pub` file)
3. Enter the passphrase if prompted

You'll add the `braid-ios` package itself in Part 2.

#### 7c. GitHub Packages token and confirm android-app-template (Android)

> **Android only** — the Android app template depends on private SEEK packages hosted on GitHub Packages (including Braid via [android-app-platform](https://github.com/SEEK-Jobs/android-app-platform)).

**Generate a GitHub token:**

1. Visit [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Name it `Android Studio GitHub`
4. Grant the `read:packages` permission (and `repo` if you will clone via HTTPS)
5. Generate the token and copy it — you **cannot** view it again
6. Click **Enable SSO** and authorise access to **SEEK-Jobs**

Keep your username and token handy — you'll add them to each Android project in Part 2.

Confirm access to the Android template:

```bash
git ls-remote git@github.com:SEEK-Jobs/android-app-template.git HEAD
```

If this fails, request access via your team or GitHub onboarding before continuing.

---



### Step 8: Install [SEEK AI Toolkit](https://backstage.myseek.xyz/docs/default/component/seek-ai-toolkit/)

> **All platforms**

This step requires a GitHub licence and access to the SEEK-Jobs organisation. If you don't yet have access, skip to Step 9.

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



### Step 9: Install IDE extensions (optional but recommended)

> **All platforms** share **GitLens**. Other extensions depend on what you edit.

Install via your IDE's **Extensions** marketplace, or (for Cursor) from **Terminal**:

```bash
# All platforms
cursor --install-extension eamodio.gitlens

# Web and Email only
cursor --install-extension esbenp.prettier-vscode
cursor --install-extension dbaeumer.vscode-eslint
```


| Extension | ID                       | Platforms  |
| --------- | ------------------------ | ---------- |
| GitLens   | `eamodio.gitlens`        | All        |
| Prettier  | `esbenp.prettier-vscode` | Web, Email |
| ESLint    | `dbaeumer.vscode-eslint` | Web, Email |


> **iOS only (optional):** If you also edit Swift in a VS Code–compatible IDE, consider the **Swift** extension (`swiftlang.swift-vscode`).
>
> **Android only (optional):** If you edit Kotlin in a VS Code–compatible IDE, consider the **Kotlin** extension (`fwcd.kotlin`).

---



### Done!

> **Note panel:** You can now move on to Part 2 for your platform:
>
> - **[Part 2 — Web: Setting up your project](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996)**
> - **[Part 2 — iOS: Set up your project](!-- link to Part 2 iOS page when published --)**
> - **[Part 2 — Android: Set up your project](!-- link to Part 2 Android page when published --)**
> - **[Part 2 — Email: Set up your workspace](!-- link to Part 2 Email page when published --)**

