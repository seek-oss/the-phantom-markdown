# Confluence draft pages — iOS, Android, Email

Draft setup guides for the DPRAC space. Copy each file into Confluence as a new page. Match formatting from the existing web guides:

- [Part 1 (Do once)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364383759/Part+1+Do+once)
- [Part 2 (Every project)](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5364350996/Part+2+Every+project)

## Preferred Part 1 (combined)

Use **`part-1-all-platforms-do-once.md`** as the single Part 1 page covering Web, iOS, Android, and Email. Steps are labelled **All platforms** or with a platform-specific note (e.g. **Web only**, **iOS only**).

The per-platform Part 1 drafts (`part-1-ios-do-once.md`, `part-1-android-do-once.md`, `part-1-email-do-once.md`) are kept as **reference only** while reviewing the combined page — do not publish those as separate Confluence pages unless you deliberately want platform-specific Part 1s.

## Suggested page hierarchy

```
Setting up an IDE for AI prototyping (parent — existing)
├── Part 1 (Do once) — all platforms   ← part-1-all-platforms-do-once.md  (replaces separate Part 1s)
├── Part 2 (Every project) — Web (existing)
├── Part 2 — iOS (Every project)       ← part-2-ios-every-project.md
├── Part 2 — Android (Every project)   ← part-2-android-every-project.md
└── Part 2 — Email (Every project)     ← part-2-email-every-project.md

Reference only (not for publish by default):
├── part-1-ios-do-once.md
├── part-1-android-do-once.md
└── part-1-email-do-once.md
```

## Confluence formatting notes

When pasting into Confluence:

1. Add the **Table of Contents** macro (exclude the page title), as on the web pages.
2. Convert blockquotes to **Note** / **Info** panels where indicated (`> **Note panel:**`, `> **Info panel:**`).
3. Replace `<!-- link -->` placeholders with actual page links after publishing.
4. Add screenshots where the template READMEs reference GitHub-hosted images (optional for v1).
5. Update the existing web Part 2 **Info panel** (“Native and Email will be added soon”) with links to these pages when published.

## Placeholder links to resolve

Each draft contains `<!-- link to Part X ... -->` comments — replace after creating sibling pages in Confluence.
