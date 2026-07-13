# Statistics by Intuition

Intuition-first statistics lessons, published as a [Quarto](https://quarto.org)
website. Each lesson pairs a structured lesson plan with a background primer
and worked modern examples.

## Repository layout

```text
├── _quarto.yml            # Quarto website configuration
├── index.qmd              # Site homepage / lesson catalog
├── styles.css             # Site-wide styling
├── pixi.toml              # Pixi environment (Quarto + future deps)
├── lessons/
│   └── 01-bayesian-statistics/
│       ├── index.qmd          # Lesson plan
│       ├── background.qmd     # Background primer
│       └── bayes-in-action.qmd  # Worked examples + exercises
└── docs/                  # Project/progress notes (not site output)
```

Each lesson lives in its own numbered directory under `lessons/` and is added
to the sidebar in `_quarto.yml`. Site output goes to `_site/` (gitignored).

## Environment

Dependencies are managed with [pixi](https://pixi.sh). The environment
currently provides Quarto.

```bash
pixi install
```

## Build the site

```bash
pixi run render    # render to _site/
pixi run preview   # live-reload preview while editing
```

## Adding a lesson

1. Create `lessons/<nn>-<topic>/` with at least an `index.qmd` (lesson plan).
2. Add the lesson's pages to the `sidebar` section of `_quarto.yml`.
3. Add a row to the lesson table in the root `index.qmd`.
4. `pixi run render` and check the output before opening a PR.

## Lessons

| # | Lesson | Status |
|---|--------|--------|
| 1 | Bayesian Statistics: Updating Beliefs with Evidence | Draft ([#2](https://github.com/nfmathieu94/remote_connection_test/issues/2)) |
