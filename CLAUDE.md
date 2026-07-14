# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is a **Zenn Connect** content repository — it holds the Markdown source for articles and books published on [Zenn](https://zenn.dev), a Japanese tech-article platform. It is connected to the author's Zenn account via GitHub, so pushes to the default branch sync directly to the live Zenn site. There is no application code, build step, or test suite; the only dependency is the `zenn-cli` package used to preview content locally.

## Commands

```bash
npm install                 # installs zenn-cli (the only dependency)
npx zenn preview            # live-preview articles/books at http://localhost:8000
npx zenn new:article        # scaffold a new article with a random slug under articles/
npx zenn new:book           # scaffold a new book under books/
```

There is no lint, build, or test command — `npm test` is an unconfigured placeholder that exits with an error.

## Structure

- `articles/*.md` — one file per article. Filenames are Zenn-generated slugs (hex IDs, e.g. `021e653989089d.md`), not human-readable titles.
- `books/` — Zenn "book" content (currently empty aside from `.keep`).

## Article frontmatter conventions

Every article file starts with YAML frontmatter Zenn requires:

```yaml
---
title: "記事タイトル"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "react"]
published: true
---
```

- `type` is either `tech` (technical write-up) or `idea` (opinion/idea piece).
- `topics` is an array of tag strings (can be empty `[]`); Japanese tags (e.g. `"マネージメント"`) are used alongside English ones.
- `published: false` keeps a draft out of the live site while still being committed to the repo — check this field before assuming a change is public.
- Article body content and commit messages are written in Japanese, matching the existing corpus.

## Working conventions

- When adding a new article, prefer `npx zenn new:article` so the slug and frontmatter scaffold match Zenn's expectations, rather than hand-crafting a filename.
- Do not rename existing article files — the slug is the stable URL identifier on Zenn; renaming breaks the published link.
- Since pushes to the default branch publish directly to Zenn, treat `published: true` commits as live-deploy actions.
