# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Multilingual documentation site for **PrimaSTEM** — a screen-free coding and math educational kit for children ages 4+. Built with [Mintlify](https://mintlify.com). Deployed at https://docs.primastem.com via Mintlify's GitHub App (auto-deploys on push to `main`).

## Development Commands

Requires Node.js v19+ and Mintlify CLI installed globally:

```bash
npm i -g mintlify          # install once
mintlify dev               # local dev server at http://localhost:3000
mintlify dev --port 3333   # custom port
mintlify broken-links      # validate all internal links
mintlify install           # reinstall deps if dev server fails
npm i -g mintlify@latest   # update CLI
```

## Architecture

### Configuration

`docs.json` is the sole config file (not `mint.json`). It controls:
- Theme (`maple`), brand colors (`#5aa02c`), favicon
- Navigation structure per language — all 10 languages declared under `navigation.languages`
- Navbar links, footer socials, GA4 (`G-QGPVQ44DNN`)

When adding a page, register it in `docs.json` under the correct language group. Pages not listed there won't appear in the sidebar (e.g. `en/quickstart.mdx` currently exists but is not in navigation).

### Language Structure

10 languages at root level: `en/` `ru/` `de/` `fr/` `es/` `it/` `nl/` `no/` `sv/` `jp/`

Each folder has the same pages:
- `intro.mdx` — product introduction
- `usermanual.mdx` — technical specs and usage
- `teachersguide.mdx` — guide for educators
- `book-1/book-1.mdx` — main workbook; `book-1/attachment-{1-4}.mdx` — supplementary sheets
- `mathdrawings.mdx`, `nfc.mdx`, `cognitive.mdx`, `contacts.mdx`

`index.mdx` at root is the multilingual landing/selector page.

**When editing content, apply changes to all language folders to keep them in sync.**

### Page Frontmatter

```yaml
---
title: "..."
description: "..."
icon: "..."   # lucide icon name
mode: "wide"  # most pages use wide mode
---
```

### Content Format

Files use `.mdx`. Common Mintlify components: `<Card>`, `<CardGroup>`, `<Accordion>`, `<AccordionGroup>`, `<Info>`, `<Tip>`, `<Note>`, `<Frame>`, `<CodeGroup>`.

### Assets

Images in `images/` with subfolders per section (`images/intro/`, `images/book-1/`, etc.). Reference from `.mdx` as `../images/<folder>/<file>` (relative path). Images are shared across all languages — do not duplicate them per language.

Diagrams use Excalidraw; library file at `excalidraw/primastem.library.excalidrawlib`.

### Adding a New Language

1. Create language folder (e.g. `pt/`)
2. Copy and translate all pages from `en/`
3. Add navigation block in `docs.json` under `navigation.languages`
