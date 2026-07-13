# Redesign → teaching + interview-prep platform

**Date:** 2026-07-13

## Purpose

Reframe the site from a plain lesson collection into a Rosalind-style
teaching + **technical-interview-prep** platform for biologists/bioinformaticians,
with a custom look, a graduate-teacher voice, interactive figures, real
literature, and a curriculum that builds toward using LLMs in science. Guiding
lens: *"what would a research science team ask in a technical interview?"*

Design doc: `docs/plans/2026-07-13-site-redesign-and-interview-platform-design.md`.

## Current status — DONE this pass

- **Custom "Field Notebook" theme** (`theme/field-notebook.scss` +
  `field-notebook-dark.scss`): warm paper/ink palette, serif display type,
  dot-grid texture, oxide-red + moss accents, dark "night-desk" mode.
  Self-contained (no external fonts/CDNs) → GitHub-Pages/offline safe.
- **Signature components** (fenced divs): `.specimen` (herbarium-label callout),
  `.whiteboard` (dark interview block), `.lens` (interview-lens aside),
  `.interactive-figure`, `.field-notes-band`, `.track-grid/.track-card`.
- **Homepage** rewritten: hero band + 5 track cards + "lesson anatomy".
- **`roadmap.qmd`**: full 16-lesson curriculum across 5 tracks, each with
  core ideas + "interview questions this unlocks".
- **Lesson 1 fully built out** (4 pages): plan, background primer, bayes-in-action
  (with interactive OJS explorer), and new `interview.qmd` (conceptual Q&A +
  whiteboard problem with model answers). Re-voiced to graduate-teacher register.
- **Interactive figure**: OJS Bayes posterior explorer (prevalence/sensitivity/
  specificity sliders → live posterior, stacked bar, posterior-vs-prevalence
  curve). Client-side, no kernel.
- **Citations**: shared `references.bib` (primary sources), Quarto citation
  system, per-page References sections, margin reference-location.
- **Science example added**: reproducibility-crisis / FDR framing of base rates
  (Ioannidis 2005; Benjamini–Hochberg 1995) in Module 4 + interview Q5.

## Commands

```bash
pixi run render      # build to _site/  (renders clean, no warnings)
pixi run preview     # live preview
```

## Verification done

- `pixi run render` → clean, no unresolved links/citations.
- Compiled CSS contains all custom components (whiteboard 48 rules, etc.).
- Light + dark bootstrap theme CSS both built; dark palette present.
- OJS runtime + favicon bundled into `_site/`.
- NOT verified in a browser (no headless Chrome on cluster) — OJS interactivity
  is standard Quarto OJS (Inputs/Plot/d3), should work; confirm in `pixi run
  preview` locally.

## Next steps

- Visual pass in a real browser (`pixi run preview`) to confirm the theme +
  OJS sliders feel right; tweak spacing/contrast if needed.
- Build Lesson 2 (p-values & hypothesis testing) as the next full vertical
  slice — highest-priority Track A topic after Bayes.
- Add ML-workflow decision flowcharts (Mermaid) when Track D lessons start.
- Decide publishing (GitHub Pages via Actions vs. gh-pages branch).

## Decisions / logic

- OJS over Shinylive/Jupyter: no kernel, static-host safe, matches the
  "adjust a parameter" figures requested. No Python added to pixi yet.
- Outlines for lessons 2–16 live in `roadmap.qmd` (single source) rather than
  16 stub directories, to keep the tree clean until a lesson is written.
- Kept the (already strong) Bayesian worked-example prose; enhanced rather than
  rewrote — added band, OJS, citations, lens asides, science example.
