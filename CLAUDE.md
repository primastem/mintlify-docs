# CLAUDE.md

This file gives Claude (or any AI assistant) the context needed to work in this repository.

## ⚠️ First — read `team-notes/`

Before any non-trivial work in this repo, **read `team-notes/`** — it contains project knowledge that isn't visible from the public docs:
- `team-notes/architecture/` — device internals (NFC↔audio mapping, planned BLE protocol)
- `team-notes/workflow/` — how we do things (tooling quirks, content philosophy)
- `team-notes/open-questions.md` — what still needs clarification from the team

These notes are intentionally **not** part of the public Mintlify site (not registered in `docs.json`). They exist in git so the whole team and any AI session can rely on the same source of truth.

## Project Overview

Multilingual documentation site for **PrimaSTEM** — a screen-free coding and math educational kit for children ages 4–10+. Built with [Mintlify](https://mintlify.com). Deployed at <https://docs.primastem.com> via Mintlify's GitHub App (auto-deploys on push to `main`).

## Development Commands

Requires Node.js v19+. Mintlify CLI is installed globally as the package `mintlify` but its binary is now `mint` (renamed in 2026 — see `team-notes/workflow/mintlify-cli.md`):

```bash
npm i -g mintlify          # install once (or update)
mint dev                   # local dev server at http://localhost:3000
mint dev --port 3333       # custom port if 3000 is busy
mint broken-links          # validate all internal links
mint install               # reinstall deps if dev server fails
```

## Architecture

### Configuration

`docs.json` is the sole config file (not `mint.json`). It controls:
- Theme (`maple`), brand colours (`#5aa02c`), favicon
- Navigation structure per language — all 10 languages declared under `navigation.languages`
- Navbar links, footer socials, GA4 (`G-QGPVQ44DNN`)

When adding a page, register it in `docs.json` under the correct language group. Pages not listed there won't appear in the sidebar.

### Language structure

10 languages at root level: `en/` `ru/` `de/` `fr/` `es/` `it/` `nl/` `no/` `sv/` `jp/`

Each folder has the same pages (frontmatter `icon:` shown in parentheses):

| File | Icon | Purpose |
| --- | --- | --- |
| `quickstart.mdx` | `rocket` | Operational quick start — how the device works in 2 minutes |
| `intro.mdx` | `lightbulb` | Product introduction (rationale, audience) |
| `usermanual.mdx` | `book-open` | Tech specs, pairing, calibration, safety |
| `teachersguide.mdx` | `graduation-cap` | Pedagogy and classroom use |
| `book-1/book-1.mdx` | `book` | Main workbook; `book-1/attachment-{1-4}.mdx` — supplementary sheets |
| `mathdrawings.mdx` | `pen-line` | Geometric drawing examples |
| `nfc.mdx` | `puzzle` | NFC token reference |
| `sounds_reference.mdx` | `volume-2` | Audio dictionary (vocabulary, alphabets, notes) |
| `cognitive.mdx` | `brain` | Use case for elderly cognitive rehab |
| `contacts.mdx` | `map` | Contact info with embedded Google Map |

`index.mdx` at root is the multilingual landing/selector — language cards link to `/<lang>/quickstart`.

**When editing content, apply changes to all 10 language folders to keep them in sync.**

### Page frontmatter

```yaml
---
title: "..."
description: "..."
icon: "..."        # lucide icon name (see lucide.dev/icons)
mode: "wide"       # most pages use wide mode
---
```

### Content components

Files use `.mdx`. Common Mintlify components: `<Card>`, `<CardGroup>`, `<Steps>`, `<Step>`, `<Accordion>`, `<AccordionGroup>`, `<Info>`, `<Tip>`, `<Note>`, `<Warning>`, `<Frame>`, `<CodeGroup>`.

### Assets

Images in `images/` with subfolders per section (`images/intro/`, `images/book-1/`, etc.). Reference from `.mdx` as `../images/<folder>/<file>` (relative path). **Images are shared across all languages — do not duplicate them per language.**

Diagrams use Excalidraw; library file at `excalidraw/primastem.library.excalidrawlib`. Source `.excalidraw.svg` files are kept alongside their PNG/JPG counterparts.

### Adding a new language

1. Create language folder (e.g. `pt/`)
2. Copy and translate all pages from `en/`
3. Add navigation block in `docs.json` under `navigation.languages` — put `pt/quickstart` first
4. Add language card in root `index.mdx` linking to `/pt/quickstart`

## Project rules (from `team-notes/workflow/`)

- **Quick Start is operational, not marketing.** Don't add pricing, partner logos, certifications, or "trusted by" lines. Those belong on primastem.com pages.
- **Don't auto-generate REST API docs from `api-reference/`** — that folder was removed because it was leftover Mintlify boilerplate. The upcoming BLE protocol will be documented from scratch in MDX, not OpenAPI (see `team-notes/architecture/ble-protocol-plan.md`).
- **Voice and tone:** simple imperative sentences, present tense, no marketing flourish. We have a humanizer skill — use it on any non-trivial Russian/English content.
