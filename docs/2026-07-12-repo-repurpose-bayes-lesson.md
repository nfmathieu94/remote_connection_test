# Repo repurpose + Lesson 1 (Bayesian Statistics)

**Date:** 2026-07-12, evening

## Purpose

Repurpose this repo from a connection-test sandbox into a home for statistics
educational material, published as a Quarto website. Tracked in issue
[#2](https://github.com/nfmathieu94/remote_connection_test/issues/2).

## Current status

- Quarto website scaffold in place (`_quarto.yml`, `index.qmd`, `styles.css`).
- Lesson 1 (Bayesian statistics) written: lesson plan, background primer,
  worked examples + 8-problem exercise set.
- Dependencies managed with pixi (`pixi.toml`); Quarto >=1.9.38 from
  conda-forge. Cluster also has `quarto/1.7.31` module but pixi env is the
  source of truth per project decision.
- Site renders without errors: `pixi run render`.

## Commands

```bash
pixi install         # one-time environment setup
pixi run render      # build site to _site/
pixi run preview     # live preview
```

## Decisions / logic

- One directory per lesson under `lessons/<nn>-<topic>/` so the site scales.
- `docs/` kept for project notes; Quarto output goes to `_site/` (gitignored)
  to avoid the GitHub-Pages-uses-docs convention colliding with notes.
- Lesson content uses no executable code cells, so rendering needs only
  Quarto — no R/Python engine dependencies yet. Add them to pixi when a
  lesson needs computation.
- Pedagogy: natural frequencies (counting) before formulas, per
  Gigerenzer & Hoffrage (1995).

## Failures / issues

- `gh` CLI not installed on cluster; GitHub operations done via the GitHub
  MCP tools instead.
- First issue-creation attempt failed with 403 until the PAT was granted
  Issues write access (fixed same day).

## Next steps

- Decide on publishing (GitHub Pages via Actions vs. rendering locally and
  pushing `_site` to a `gh-pages` branch).
- Lesson 2 topic TBD; follow the layout in README "Adding a lesson."
- Optional: add a naive-Bayes coding exercise (would add Python/Jupyter to
  the pixi env).
