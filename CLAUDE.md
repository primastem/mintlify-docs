# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Install Mintlify CLI (once)
npm i -g mintlify

# Preview docs locally (run from repo root, where docs.json is)
mintlify dev

# If dev server fails, reinstall dependencies
mintlify install
```

Changes pushed to `main` deploy automatically to production via GitHub App.

## Architecture

This is a **Mintlify documentation site** for [PrimaSTEM](https://primastem.com) — a screen-free coding and math educational kit for children aged 4+.

### Configuration

`docs.json` is the central config file. It controls:
- Theme, colors, logo, favicon
- Navigation structure per language
- Navbar links, footer socials, integrations (GA4)

### Multilingual structure

All content lives in language-specific folders at the root: `en/`, `ru/`, `de/`, `fr/`, `es/`, `it/`, `nl/`, `no/`, `sv/`, `jp/`.

Each language folder contains the **same set of pages**:
- `intro.mdx` — product introduction
- `usermanual.mdx` — technical specs and usage
- `teachersguide.mdx` — guide for educators
- `book-1/book-1.mdx` — main workbook (with attachments in `book-1/`)
- `mathdrawings.mdx` — math drawing activities
- `nfc.mdx` — NFC chip usage
- `cognitive.mdx` — cognitive development context
- `contacts.mdx` — contact info

When adding or updating content, **apply changes to all language folders** to keep them in sync.

### Images

Shared across all languages — stored in `images/` with subfolders matching page names (e.g., `images/intro/`, `images/usermanual/`). Reference from `.mdx` files as `../images/<folder>/<file>`.

### Excalidraw

The `excalidraw/` folder contains a custom Excalidraw library (`primastem.library.excalidrawlib`) used for creating diagrams in the docs.

### Page frontmatter

Each `.mdx` page uses frontmatter:
```yaml
---
title: "..."
description: "..."
icon: "..."   # lucide icon name
mode: "wide"  # most pages use wide mode
---
```
