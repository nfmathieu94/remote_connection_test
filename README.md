# Statistics by Intuition

A **field notebook for scientists**: intuition-first lessons in statistics and
machine learning, paired with Rosalind-style practice problems and the
conceptual questions a technical interviewer actually asks. Published as a
[Quarto](https://quarto.org) website.

The guiding lens for every lesson: *what would a research science team probe in
a technical interview?* — the reasoning behind a method, its assumptions, how
you'd know if it broke, and what you'd plot to find out. The curriculum builds
across five tracks toward using LLMs to find patterns in scientific data.

## The lesson anatomy

Each lesson lives in `lessons/<nn>-<topic>/` with four pages:

| Page | Purpose |
|------|---------|
| `index.qmd` | Lesson plan — objectives, modules, interview questions unlocked |
| `background.qmd` | Just-enough prerequisites, with self-checks |
| `<topic>-in-action.qmd` | Worked examples + interactive OJS figures |
| `interview.qmd` | Rosalind-style problems + interviewer questions, model answers |

## Repository layout

```text
├── _quarto.yml            # Website config, navbar/sidebar, theme wiring
├── index.qmd              # Landing page (hero + track cards)
├── roadmap.qmd            # Full curriculum: every lesson + interview questions
├── references.bib         # Shared, growing bibliography (primary sources)
├── styles.css             # Small CSS utilities on top of the SCSS theme
├── theme/
│   ├── field-notebook.scss       # "Field Notebook" theme — light ("day desk")
│   ├── field-notebook-dark.scss  # dark override ("night desk")
│   └── favicon.svg
├── lessons/
│   └── 01-bayesian-statistics/   # index · background · bayes-in-action · interview
└── docs/                  # Project/progress notes and design docs (not site output)
```

Site output goes to `_site/` (gitignored).

## The theme

A custom **"Field Notebook"** SCSS theme (warm paper, serif display type, oxide
red + moss accents) with a dark "night desk" mode. It is self-contained — no
external fonts or CDN calls — so it works under a strict GitHub Pages / offline
environment. Signature components, used via fenced divs:

- `::: {.specimen}` — herbarium-label callout for key concepts.
- `::: {.whiteboard}` — dark "at the whiteboard" block for interview problems.
- `::: {.lens}` — "interview lens" aside.
- `::: {.interactive-figure}` — framed wrapper for OJS figures.
- `.field-notes-band`, `.track-grid` / `.track-card` — page headers and cards.

## Interactivity

Interactive figures use **Observable JS (OJS)** — client-side, no kernel, safe
for static hosting. See the Bayes posterior explorer in
`lessons/01-bayesian-statistics/bayes-in-action.qmd` for the reusable pattern.

## Environment

Dependencies are managed with [pixi](https://pixi.sh) (Quarto ≥ 1.9.38).

```bash
pixi install         # one-time environment setup
pixi run render      # build site to _site/
pixi run preview     # live-reload preview while editing
```

## Adding a lesson

1. Create `lessons/<nn>-<topic>/` with the four pages above (or a subset).
2. Add its pages to the `sidebar` in `_quarto.yml` under the right track.
3. Add/promote its entry in `roadmap.qmd`; add a track card in `index.qmd`.
4. Add any new citations to `references.bib`.
5. `pixi run render` and check the output before opening a PR.

## Curriculum

See [`roadmap.qmd`](roadmap.qmd) for the full plan. Tracks:

- **A · Inference foundations** — Bayes *(live)*, *p*-values, *t*-tests, CIs,
  multiple testing/FDR, power.
- **B · Data transformation** — z-scores, log/rlog/VST, quantile, min–max.
- **C · Regression & models** — linear, logistic/GLMs, regularization.
- **D · ML fundamentals** — the ML workflow (flowcharts), evaluation & selection,
  unsupervised learning.
- **E · Toward LLMs in science** — embeddings, what an LM learns, LLMs for
  pattern-finding in data.
