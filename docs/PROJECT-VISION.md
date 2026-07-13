# Project Vision & Roadmap — Statistics by Intuition

**Last updated:** 2026-07-13
**Read this first when resuming work on this repo.**

---

## Mission

A **Quarto website teaching statistics and machine learning for bioinformatics**,
that does three jobs at once:

1. **Teach** commonly-used statistics and ML for bioinformatics, rigorously,
   intuition-first (meaning before formalism).
2. **Prepare** readers for hard technical interviews at top companies and labs.
3. **Stay modern** — examples drawn from cutting-edge biology and AI:
   single-cell sequencing, neural networks / gradient descent, and LLMs in
   biology.

Secondary purpose: a **personal reference database** the owner (Nathan) returns
to when refreshing key concepts or prepping for interviews.

## THE core thesis (the "main message of the book")

**Real data does not tell you which method to use — recognizing the *shape* of
the problem does.** The book's job is to build the reader's reflex for
pattern-matching a messy real-world problem to the right *family* of solutions:
"this is a base-rate problem," "this is a maximum-likelihood problem," "this
sequence has memory → think Markov," "no closed form → simulate it (Monte
Carlo)." Every lesson should end with the reader able to *recognize the problem
type in the wild*. State/reinforce this thesis on the homepage, the roadmap, and
in each lesson (each roadmap lesson has a "Reach for this when:" line).

## Audience (three readers)

- **Graduate students** learning stats/bioinformatics — want durable intuition.
- **Late-stage PhDs / postdocs** prepping for demanding technical interviews.
- **Working professionals** needing fast, trustworthy refreshers on a concept
  or workflow.

## The guiding lens

Every lesson is framed by: *"What would a sharp technical interviewer press you
on?"* — reasoning over trivia. For each concept, always surface: why this
method, what it assumes, how you'd know if it broke, and what you'd plot to find
out. (Origin of the lens: "what would the Anthropic Science team ask?")

## Pedagogy & conventions

- **Voice:** graduate-level teacher — engaging, warm, a little opinionated;
  never dry or stock/AI-generic.
- **Intuition first, formalism second.** Natural-frequency / counting arguments
  before formulas.
- **Design:** custom "Field Notebook" aesthetic (see below) — must not look
  like a stock template.
- **Interactive figures:** parameter-adjustable graphs (Observable JS) that
  drive concepts home.
- **Real citations:** primary literature (incl. science papers) in
  `references.bib`.
- **Recurring worked example:** thread **single-cell RNA-seq** through the
  tracks so concepts compound.

## Lesson anatomy (per `lessons/<nn>-<topic>/`)

| Page | Purpose |
|------|---------|
| `index.qmd` | Lesson plan — objectives, modules, interview questions unlocked |
| `background.qmd` | Just-enough prerequisites, with self-checks |
| `<topic>-in-action.qmd` | Worked examples + interactive OJS figures |
| `interview.qmd` | Rosalind-style problems + interviewer questions, model answers |

## Curriculum (6 tracks, 21 lessons) — see `roadmap.qmd` for full detail

**Track A · Inference foundations**
1. Bayesian Statistics — **LIVE (complete)**
2. p-values & Hypothesis Testing — *next up*
3. t-tests & the t-distribution
4. Confidence Intervals & the Bootstrap
5. Maximum Likelihood Estimation (likelihood, log-lik, MLE=optimization;
   MLE vs MAP vs Bayesian; links fwd to gradient descent)
6. Multiple Comparisons & FDR (single-cell DE example)
7. Statistical Power & Experimental Design (cells vs. samples trap)

**Track B · Data transformation & normalization**
8. Normalization & Standardization (z-score, log1p, CPM/TPM, size factors,
   SCTransform, VST, quantile; bulk + single-cell)

**Track C · Regression & statistical models**
9. Linear Regression (diagnostics, residual plots)
10. Logistic Regression & GLMs (incl. negative-binomial for RNA-seq)
11. Regularization & the Bias–Variance Tradeoff (bridge to ML)

**Track D · Probabilistic & computational modeling**
12. Monte Carlo Methods & Simulation (permutation/randomization tests,
    simulating nulls & power, MCMC intuition; bootstrap revealed as Monte Carlo)
13. Markov Chains & Hidden Markov Models (Markov property; hidden states;
    Viterbi & forward–backward; gene finding, CpG islands, profile HMMs,
    base-calling)

**Track E · Machine learning: workflow → neural networks**
14. The ML Workflow (decision flowcharts; train a tiny model)
15. Model Evaluation & Selection (metrics, leakage, imbalance)
16. Unsupervised Learning & Dimensionality Reduction (PCA/UMAP/clustering;
    single-cell heavy)
17. Gradient Descent & Optimization (the learning engine; the *how* of MLE)
18. Neural Networks (logistic regression → deep nets; backprop intuition)

**Track F · LLMs & modern AI in biology**
19. Embeddings & Similarity (words, proteins, cells as vectors)
20. What a Language Model Actually Learns (tokens, attention, transformers —
    intuition, incl. protein sequences)
21. LLMs & Foundation Models in Biology (ESM-style protein LMs, single-cell
    foundation models, literature mining, evals, hallucination risks)

## Design system — "Field Notebook"

- Theme: `theme/field-notebook.scss` (light "day desk") +
  `theme/field-notebook-dark.scss` (dark "night desk"). Self-contained
  (no external fonts/CDNs) → GitHub-Pages/offline safe.
- Palette: warm paper `#f4efe4`, ink `#23262d`, oxide red `#b0472e`,
  moss green `#5a6f3f`, faded blue `#3d5a6c`, ochre `#c98a26`.
- Signature fenced-div components:
  - `::: {.specimen}` — herbarium-label callout for key concepts.
  - `::: {.whiteboard}` — dark "at the whiteboard" interview block.
  - `::: {.lens}` — "interview lens" aside.
  - `::: {.interactive-figure}` — framed wrapper for OJS figures.
  - `.field-notes-band` (lesson header), `.track-grid` / `.track-card`.

## Tech & workflow

- Quarto (pixi-managed, Quarto ≥ 1.9.38). `pixi run render` / `pixi run preview`.
- Interactivity: **Observable JS** (client-side, no kernel). No Python/R engine
  added yet — add to pixi only when a lesson needs real computation (e.g.,
  training a model in-page might warrant it; reconsider then).
- Publishing: GitHub Actions → GitHub Pages (`.github/workflows/publish.yml`),
  Quarto pinned to 1.9.38. Pages source must be set to "GitHub Actions" in repo
  settings (one-time, done).
- Repo is `nfmathieu94/remote_connection_test`. Git auth is NOT configured on
  the cluster — use the GitHub MCP tools for remote operations; the user
  pushes/merges manually.

## Current status (2026-07-13)

- Redesign + Lesson 1 + roadmap + theme + publish workflow: **done, committed,
  merged to main.**
- Publish workflow debugged: a "2 github-pages artifacts" deploy error was
  caused by re-running a run (transient API hiccup on first try); fix is to
  start a *fresh* run, not re-run.

## Next steps (in priority order)

1. **Build Lesson 2 — p-values & Hypothesis Testing** as the next full vertical
   slice (4 pages + an interactive figure, e.g. p-value distribution under the
   null / sampling distribution explorer). Highest priority.
2. Then continue Track A (t-tests → CIs → FDR → power).
3. Introduce Mermaid decision flowcharts when Track D lessons begin.
4. Keep threading the single-cell example; keep adding primary citations.
5. Confirm the live site renders/looks right in a browser (`pixi run preview`);
   no headless browser on the cluster for screenshots.

## Design doc

Original design rationale: `docs/plans/2026-07-13-site-redesign-and-interview-platform-design.md`.
