# Agent instructions: new Braid email prototype

You are helping create a new Braid **email** prototype: a standalone TypeScript project with [`@seek/braid-email-ui`](https://braid-email.skinfra.xyz/?path=/docs/braid-email-ui-getting-started--docs). Work step by step.

> **Prerequisite:** `common.md` and `email.md` complete — especially Cloudsmith npm auth for `@seek` packages.

---

## Step 1: Choose a project name

Ask for (or confirm) a single folder-safe name under `~/Code/` (e.g. `job-alert-email` or `welcome-email-proto`). Prefer lowercase with hyphens.

Validate:

```bash
test ! -e ~/Code/<project-folder> && echo "OK" || echo "Folder already exists"
```

---

## Step 2: Scaffold a standalone project

Create `~/Code/<project-folder>` with a minimal Yarn + TypeScript + React setup (agent may write these files):

**`package.json`** (use the confirmed project name):

```json
{
  "name": "<project-folder>",
  "version": "1.0.0",
  "private": true,
  "license": "UNLICENSED",
  "scripts": {
    "render": "tsx src/render.tsx"
  },
  "dependencies": {},
  "devDependencies": {}
}
```

**`tsconfig.json`:**

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "outDir": "dist",
    "rootDir": "src"
  },
  "include": ["src"]
}
```

**`.gitignore`:** include at least `node_modules/`, `out/`, `dist/`.

Then install dependencies:

```bash
cd ~/Code/<project-folder>
yarn add @seek/braid-email-ui @faire/mjml-react mjml react@^18 react-dom@^18
yarn add -D typescript tsx @types/react @types/react-dom @types/mjml
```

**Verify:** install succeeds and `@seek/braid-email-ui` resolves from Cloudsmith (no `E401` / missing package).

**If install fails on auth:** send the user back to `email.md` Step 3 (Cloudsmith npm). Do **not** fall back to cloning the monorepo or hosted Playroom as a substitute for fixing auth.

---

## Step 3: Smoke-test Braid email shell

Add a minimal layout, sample template, and render script. Keep `themeName="seekJobs"`.

**`src/EmailLayout.tsx`:**

```tsx
import { Mjml, MjmlBody, MjmlHead, MjmlPreview } from '@faire/mjml-react';
import { BraidHead, BraidProvider } from '@seek/braid-email-ui';
import type { FC, PropsWithChildren } from 'react';

type EmailLayoutProps = PropsWithChildren<{
  previewText?: string;
}>;

export const EmailLayout: FC<EmailLayoutProps> = ({
  children,
  previewText,
}) => (
  <BraidProvider themeName="seekJobs">
    <Mjml>
      <MjmlHead>
        <BraidHead />
        {previewText ? <MjmlPreview>{previewText}</MjmlPreview> : null}
      </MjmlHead>
      <MjmlBody>{children}</MjmlBody>
    </Mjml>
  </BraidProvider>
);
```

**`src/WelcomeEmail.tsx`:**

```tsx
import { Button, Heading, PageBlock, Text } from '@seek/braid-email-ui';
import type { FC } from 'react';

import { EmailLayout } from './EmailLayout';

export const WelcomeEmail: FC = () => (
  <EmailLayout previewText="Welcome to your Braid email prototype">
    <PageBlock>
      <Heading level="1" paddingBottom="small">
        Welcome
      </Heading>
      <Text paddingBottom="medium">
        Braid email is connected. You can start prototyping.
      </Text>
      <Button href="https://www.seek.com.au">Go to SEEK</Button>
    </PageBlock>
  </EmailLayout>
);
```

**`src/render.tsx`:**

```tsx
import { render } from '@faire/mjml-react/utils/render';
import { mkdir, writeFile } from 'node:fs/promises';
import path from 'node:path';

import { WelcomeEmail } from './WelcomeEmail';

async function main() {
  const outDir = path.join(process.cwd(), 'out');
  const outFile = path.join(outDir, 'welcome.html');

  const { html } = await render(<WelcomeEmail />);

  await mkdir(outDir, { recursive: true });
  await writeFile(outFile, html, 'utf8');

  console.log(`Wrote ${outFile}`);
}

main().catch((error) => {
  console.error(error);
  process.exit(1);
});
```

Docs: https://braid-email.skinfra.xyz/?path=/docs/braid-email-ui-getting-started--docs

---

## Step 4: Render and preview

```bash
cd ~/Code/<project-folder>
yarn render
open out/welcome.html
```

**Verify:** `out/welcome.html` is written and opens in a browser with the Welcome heading / button. There is no live reload — after edits, run `yarn render` again and refresh the browser.

Do **not** mark setup complete until render + preview succeed.

---

## Step 5: Open the project in the AI IDE

Open `~/Code/<project-folder>` in Cursor / Copilot / Claude Code.

> Edit templates in the IDE; preview with `yarn render` + open the HTML.

Do **not** mark setup complete until the project is open in the AI IDE.

---

## Done

| Goal | Action |
| --- | --- |
| Preview | `yarn render` then open `out/welcome.html` |
| Edit | Change `src/WelcomeEmail.tsx` (or add templates) + re-render |
| Docs | https://braid-email.skinfra.xyz/ |

Optional: [hosted Playroom](https://braid-email.skinfra.xyz/playroom/) is fine for quick visual experiments, but the prototype source of truth is this local project.
