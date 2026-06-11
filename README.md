# The Phantom Markdown

A repository of SEEK design systems context, built to give AI tooling accurate grounding in our design language. Portable and tool-agnostic, works with any AI tool that can read a URL.

## How it works

A single entry point, `seek-design.md`, links to all other context files in the repo. This means the repo can grow, evolve, and be updated without requiring changes to the consumers set up. Additional files are loaded conditionally, so the AI only pulls in what's relevant to the task at hand.

## Getting started

See the [setup guides in Confluence](https://myseek.atlassian.net/wiki/spaces/DPRAC/pages/5374705714/Braid+context+for+AI+-+How+to+guides) to get up and running.

_Please note: This is an ongoing experiment that is likely to change and evolve._
