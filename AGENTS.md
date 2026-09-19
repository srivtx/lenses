# AGENTS.md

## Project

Lenses is the umbrella showcase site for a suite of five offline tools: booklens (EPUB), officelens (DOCX, PPTX), odflens (ODT, ODS, ODP), iconlens (SVG), and waxseal (WACZ). It is plain static HTML and links out to each tool's own site and repository. The five tools themselves live in their own repositories. The MCP server for the suite lives in its own repo, `srivtx/lenses-mcp`.

## Commands

- `bun install` — install the dev dependency for the umbrella site.
- `node scripts/check-site.mjs` — the only check: validates every `site/*.html`.
- `bun run check:site` — the same check via the package script.

## Layout

- `site/` — the single static page, `site/assets/` (styles, self-hosted fonts), and `site/llms.txt`.
- `scripts/` — `check-site.mjs`.
- No `src/`, no `tests/`, no `mcp/`, and no generated playground bundle at the repo root. The MCP server is at https://github.com/srivtx/lenses-mcp.

## Conventions and hard rules

- The site is fully static and offline: no external scripts or stylesheets, no network `src`, no telemetry.
- `site/assets/lens.css` is a shared design system copied byte-identical across the Lenses suite. Do not diverge it; per-tool changes go in `site/assets/theme.css`.
- `site/assets/fonts/*.woff2` are self-hosted Geist (SIL Open Font License 1.1). Do not swap them for a CDN.
- Every `site/*.html` must pass `node scripts/check-site.mjs`: exactly one `<h1>` and one `<main>`, a skip link whose `#fragment` matches an element id, and only classes defined in `lens.css` or `theme.css`.
- Each tool's CLI contract is stable: documented `--json` output and exit codes `0` (clean), `1` (findings), `2` (usage or parse error), `3` (I/O error).
