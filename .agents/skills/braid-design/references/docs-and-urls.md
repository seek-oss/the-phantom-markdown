# Braid docs and URLs

**Ownership and team** are not duplicated here — read them from the **Braid** system and related catalog entities in Backstage via `get-catalog-entity` below (and linked TechDocs).

## Canonical resources (fallbacks)

| Resource                      | URL                                                                     |
| ----------------------------- | ----------------------------------------------------------------------- |
| **Braid web (open source)**   | https://github.com/seek-oss/braid-design-system                         |
| **Published docs & Playroom** | https://seek-oss.github.io/braid-design-system (Playroom: `/playroom/`) |
| **Braid Native iOS docs**     | https://braid-native.skinfra.xyz/documentation/ios/documentation/braid  |
| **Braid Native Android docs** | https://braid-android.skinfra.xyz/                                      |
| **Braid Email UI docs**       | https://braid-email.skinfra.xyz/                                        |
| **Braid Email UI Playroom**   | https://braid-email.skinfra.xyz/playroom                                |
| **Phantom markdown (design)** | https://github.com/seek-oss/the-phantom-markdown                        |

If Backstage entity metadata or TechDocs disagree with this table, **trust Backstage**.

## Backstage MCP queries

Prefer entity-targeted queries so results stay on Braid web, Native, email, or governance docs as needed:

```
get-catalog-entity({ name: "braid", kind: "system", namespace: "default" })
get-catalog-entity({ name: "braid-ios", kind: "component", namespace: "default" })
get-catalog-entity({ name: "braid-email-ui", kind: "component", namespace: "default" })
backstage-search({ query: "Braid Design System", types: ["techdocs"], entityKinds: ["System"] })
backstage-search({ query: "Braid layout Stack Columns tones", types: ["techdocs"] })
backstage-search({ query: "Braid development workflow testing guide", types: ["techdocs"] })
backstage-search({ query: "Braid Native iOS UIKit", types: ["techdocs"] })
backstage-search({ query: "Braid Native Android Material components", types: ["techdocs"] })
backstage-search({ query: "Braid Email UI", types: ["techdocs"] })
backstage-search({ query: "Braid checklist compliance adoption", types: ["techdocs"] })
```

For **Android**, if there is a dedicated catalog entity (e.g. a `braid-android` component), call `get-catalog-entity` for it the same way as `braid-ios` once you confirm the name in the catalog.

Generic searches (e.g. "design system" alone) will return noise across many repos — narrow with the queries above or entity filters.

If the **Backstage MCP** is unavailable, use this skill's **references/**, **GitHub** and other URLs in this file, the **RFC** plugin or RFC skill for formal SEEK standards, and **Backstage in the browser** (https://backstage.myseek.xyz) when live catalog content is required.
