# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

MakhanTable (brand shown in UI: "Makhan"; full name "Makhantable") — a static-site prototype for an "Airbnb for dining" marketplace where home chefs open their tables to guests. Currently a single self-contained page. Note: the brand plays on the Malay word *makan* ("to eat"); keep that word intact in the footer etymology line — do not rename it to "Makhan".

## Running

No build step, framework, or dependencies. Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000   # then visit http://localhost:8000
```

**Deployment: GitHub Pages.** Root `index.html` is the entry point; every push to the deployed branch goes live within ~1 minute. Keep everything as plain static files with relative links (no client-side-router setup). New pages are just additional `.html` files at the repo root (e.g. `/host.html`).

## Architecture

Everything lives in `index.html`: a `<style>` block, the semantic HTML sections, and a `<script>` block — no external JS/CSS beyond Google Fonts.

- **Design tokens** are CSS custom properties in `:root` (palette: `--celadon`, `--porcelain`, `--ink`, `--lacquer` red accent, `--broth`, `--scallion`; plus `--line`, `--radius`). Fonts: Young Serif (headings), Instrument Sans (body), Spline Sans Mono (labels/meta). Reuse these tokens rather than hardcoding colors.
- **Listings are data-driven.** The `LISTINGS` array in the script is the source of truth for the cards. `render()` builds the grid from it and is re-run on cuisine-chip clicks; cuisine filter chips are derived automatically from the distinct `cuisine` values.
- **Food art is inline SVG, keyed by string.** Each listing has a `plate` key that maps into the `PLATES` object; `plateSVG(kind)` wraps it in a plate. To add a cuisine, add a `PLATES` entry and reference its key from a `LISTINGS` item — do not add `<img>` assets.
- No backend, routing, or persistence yet — chips/filtering are the only interactivity. "Book", "Sign in", "Become a host" are non-functional links.

## Conventions

- Keep the single-file, dependency-free structure unless a change genuinely warrants splitting it.
- Respect the existing `prefers-reduced-motion` and `:focus-visible` accessibility handling when adding UI.
