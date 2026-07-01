# Design at SEEK

## Instructions for AI tools

- **Import font** via `@import url('https://www.seek.com.au/static/shared-web/seeksans.css');`
- **After building any page or component**, ensure `<link rel="stylesheet" href="https://www.seek.com.au/static/shared-web/seeksans.css">` is present in the `<head>` in `src/render.tsx`. Add it if it isn't already there.
- **Templates and patterns:** For ready-made Braid composition examples, search your local `node_modules/braid-design-system` package for `*.snippets.tsx` files (e.g. under a `playroom/templates/` path).

---

## Getting started

Read each of the following files to get up to speed:

| File                                                                                                                                                                                              | Description                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [systems.md](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/systems.md) | Shared Braid foundations — tones, typography, layout, components, accessibility, custom UI |
| [web.md](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/web.md)         | Web platform guide — tokens, components, and implementation                                  |

## Additional context

Read the following files only when needed:

### Platform guides

| File                                                                                                                                                                                              | When to use                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [native.md](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/native.md) | When designing for iOS and Android native apps   |
| [email.md](https://raw.githubusercontent.com/seek-oss/braid-context/refs/heads/master/.agents/skills/braid/references/email.md) | When designing for Email                         |
