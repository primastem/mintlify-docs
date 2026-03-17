# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Multilingual documentation site for **PrimaSTEM** — an educational robotics product for children ages 4+. Built with [Mintlify](https://mintlify.com). Deployed at https://docs.primastem.com via Mintlify's GitHub App (auto-deploys on push to `main`).

## Development Commands

Requires Node.js v19+ and Mintlify CLI installed globally:

```bash
npm i -g mintlify
```

| Command | Purpose |
|---------|---------|
| `mintlify dev` | Start local dev server at http://localhost:3000 |
| `mintlify dev --port 3333` | Custom port |
| `mintlify broken-links` | Validate all internal links |
| `mintlify install` | Reinstall dependencies |
| `npm i -g mintlify@latest` | Update CLI |

## Architecture

### Configuration

`docs.json` is the main Mintlify config (not `mint.json`). It defines:
- Theme (`maple`), brand colors, favicon
- Navigation structure per language (10 languages)
- Navbar links, footer socials
- GA4 integration (`G-QGPVQ44DNN`)

### Language Structure

Content is organized by language code at the root level. Each language folder has an identical section structure:

```
en/  fr/  de/  es/  it/  jp/  nl/  no/  ru/  sv/
└── intro.mdx, usermanual.mdx, teachersguide.mdx,
    mathdrawings.mdx, nfc.mdx, cognitive.mdx,
    contacts.mdx, book-1/
```

`index.mdx` is the landing page (multilingual selector). Navigation for all languages is declared in `docs.json` under `navigation.languages`.

### Content Format

Files use `.mdx` (Markdown + React components). Common Mintlify components used throughout:
`<Card>`, `<CardGroup>`, `<Accordion>`, `<AccordionGroup>`, `<Info>`, `<Tip>`, `<Note>`, `<Frame>`, `<CodeGroup>`

### Assets

Images live in `images/` organized by section (e.g. `images/intro/`, `images/book-1/`). Diagrams use Excalidraw — the library file is at `excalidraw/primastem.library.excalidrawlib`.

### Adding Content in a New Language

1. Create the language folder (e.g. `pt/`)
2. Mirror the structure from `en/`
3. Add the language navigation block in `docs.json` under `navigation.languages`
