<div align="center">

# Lenses

> Five small, offline tools for the files you ship.

**by svx** · MIT Licensed

[![CI](https://github.com/srivtx/lenses/actions/workflows/ci.yml/badge.svg)](https://github.com/srivtx/lenses/actions/workflows/ci.yml)
[![license](https://img.shields.io/badge/license-MIT-4f46e5)](LICENSE)

</div>

---

**Site:** [srivtx.github.io/lenses](https://srivtx.github.io/lenses)

## What this is

The showcase and entry point for a suite of offline command-line tools that read a file format directly and report what breaks accessibility, or prove an archive has not changed. Each tool lives in its own repository with its own site and playground.

| Tool | Format | What it does | Site | Source |
|---|---|---|---|---|
| **booklens** | EPUB | Audits EPUB Accessibility 1.1 / WCAG 2.x and writes a repaired book | [site](https://srivtx.github.io/booklens) | [repo](https://github.com/srivtx/booklens) |
| **officelens** | DOCX, PPTX | Audits OOXML accessibility: alt text, headings, language, tables, links | [site](https://srivtx.github.io/officelens) | [repo](https://github.com/srivtx/officelens) |
| **odflens** | ODT, ODS, ODP | Audits OpenDocument accessibility with rules gated by format | [site](https://srivtx.github.io/odflens) | [repo](https://github.com/srivtx/odflens) |
| **iconlens** | SVG | Computes the accessible name of a standalone SVG and flags what breaks it | [site](https://srivtx.github.io/iconlens) | [repo](https://github.com/srivtx/iconlens) |
| **waxseal** | WACZ | Detached Ed25519 Merkle seal for web archives, with inclusion proofs | [site](https://srivtx.github.io/waxseal) | [repo](https://github.com/srivtx/waxseal) |

## Install

Each tool installs with one script (requires [Bun](https://bun.sh)):

```bash
curl -fsSL https://raw.githubusercontent.com/srivtx/iconlens/main/install.sh | sh
```

Or run one without installing:

```bash
bunx github:srivtx/iconlens#main --help
```

## Common shape

- A CLI and a typed library that share one rule engine.
- Text, JSON, and SARIF 2.1.0 output, with a documented exit-code scheme.
- Offline: files are read locally, with no network calls and no telemetry.
- Deterministic output, so a CI diff means a real change.

## For agents

Every tool emits stable JSON with `--json` and SARIF 2.1.0, so an agent can read findings without scraping a screen. Two extras make that first-class:

- **[lenses-mcp](https://github.com/srivtx/lenses-mcp)** — a Model Context Protocol server exposing all five tools over stdio. Add it to any MCP client:

  ```json
  { "mcpServers": { "lenses": { "command": "bunx", "args": ["github:srivtx/lenses-mcp#main"] } } }
  ```

- **`llms.txt`** — each site serves one (`/llms.txt`) so an agent can read the docs index without parsing HTML.

## This repository

This repo contains only the umbrella site. It is plain static HTML, shares the `lens.css` design system with the five tool sites, and is checked by `scripts/check-site.mjs`.

```bash
bun run check:site
python3 -m http.server 4173 --directory site
```

## License

MIT.
