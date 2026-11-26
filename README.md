# Offsitedark Devblog

Live site: [offsitedark.github.io](https://offsitedark.github.io)

Public devblog and digital garden for **offsitedark**—covering ongoing engineering updates across [offsitedarklabs](https://github.com/offsitedarklabs) and [offsitedark](https://github.com/offsitedark) projects (including [offsitedark.com](https://offsitedark.com)), CVE notes, security research, and code write-ups.

## Repository Layout

- [`source/content/`](./source/content) — Obsidian vault Markdown pages published to the site:
  - `Devlogs/` — Development updates and progress logs across offsitedark projects
  - `CVE Reports/` — Vulnerability notes and analyses
  - `Code Challenges/` — Algorithm and systems notes
  - `Understanding of Security Principles/` — Security fundamentals and study notes
- [`source/raw_html/`](./source/raw_html) — Standalone HTML files copied directly into the build output
- [`source/quartz.config.ts`](./source/quartz.config.ts) & [`source/quartz.layout.ts`](./source/quartz.layout.ts) — Quartz site theme, metadata, and layout configuration

## Local Preview

```bash
cd source
npx quartz build --serve
```

## Publishing

Commits pushed to `main` automatically build the Obsidian vault with [Quartz](https://quartz.jzhao.xyz) and deploy to GitHub Pages via [`.github/workflows/ci.yaml`](./.github/workflows/ci.yaml).

---

Built with [Obsidian](https://obsidian.md) and [Quartz](https://github.com/jackyzha0/quartz).
