# Design — "Statistics by Intuition" as a teaching + interview-prep platform

**Date:** 2026-07-13
**Branch:** lesson-01-bayesian-statistics

## Framing

Rosalind (rosalind.info) meets a graduate seminar. The site teaches the
statistical and machine-learning intuition a **biologist / bioinformatician**
needs, then makes it stick with **Rosalind-style practice problems** and the
**conceptual questions a technical interviewer actually asks**. Guiding lens
for every lesson: *"What would the Anthropic Science team ask in a technical
interview?"* — i.e. reason about statistics rigor, ML fundamentals, model
selection, metrics, diagnostic plots, experimental design, and (building toward
the end) how LLMs find patterns in scientific data.

Two audiences, one site:
1. **Learner** — builds intuition first, formalism second.
2. **Returning reference user** (the site owner) — a durable database to refresh
   p-values, t-tests, CIs, normalization, ML workflow, before an interview.

## Voice

Graduate-level teacher: warm, precise, a little opinionated. Uses "we/you,"
poses the question before answering it, cites primary literature inline, and is
honest about controversy and failure modes. Never lectures *at* — thinks *with*
the reader.

## Visual identity — "Field Notebook"

Custom SCSS theme (`theme.scss` light, `theme-dark.scss` dark) replacing stock
flatly/darkly. Self-contained (no external font/CDN calls) so GitHub Pages works
under a strict environment.

- **Palette:** paper `#f4efe4`, ink `#20232a`, oxide red `#b0472e`,
  moss green `#5a6f3f`, faded blue `#3d5a6c`. Dark "night-desk": slate paper
  `#1c1f26`, warm-white ink `#e8e2d4`, same accents lightened.
- **Type:** serif display stack (Iowan/Charter/Palatino/Georgia) for headings;
  humanist sans (system-ui/Segoe/Helvetica) for body; monospace for math/code.
- **Signature components** (SCSS + Quarto callout restyles):
  - **Specimen-label callouts** — herbarium-tag look with a corner "stamp," used
    for key concepts / definitions.
  - **Margin notes** — Tufte-style asides and inline citations.
  - **Field Notes header band** on each lesson (lesson number, tags, time).
  - Ruled section dividers; understated grid/dot-paper texture via CSS gradient.
  - **Interview-question blocks** — a distinct callout ("At the whiteboard")
    posing a question, with a collapsible model answer.
  - **Anthropic-Science-lens asides** — a recurring "How this shows up in a
    Science interview" note.

## Interactivity — Observable JS (OJS)

Client-side, kernel-free, GitHub-Pages-safe. A small reusable pattern
(`_ojs/` helpers where useful) so any lesson can drop in sliders cheaply.
Flagship figure: **Bayes posterior explorer** — sliders for prevalence,
sensitivity, specificity driving a live posterior bar + 10,000-person icon grid,
wired to the Module 2 counting method. Future lessons reuse the pattern
(t-distribution vs. normal, p-value under the null, bias–variance, ROC curve,
regularization path, etc.).

## Literature / citations

Shared `references.bib` + Quarto citation system → a genuine, growable
bibliography. Inline margin citations plus a per-lesson **References** section
with primary sources (papers where possible, books where appropriate). This is
part of the "database I return to" goal.

## Content architecture

Each lesson directory gains a consistent set of pages:
- `index.qmd` — lesson plan (objectives, modules, time, prerequisites).
- `background.qmd` — just-enough primer.
- `<topic>-in-action.qmd` — worked examples.
- `interview.qmd` — **Rosalind-style problems + interviewer questions**, with
  collapsible solutions; the interview-prep core.

Site-level additions:
- `roadmap.qmd` — the full curriculum as tracks, showing where each lesson sits
  and what it builds toward.
- Restyled `index.qmd` homepage with a real landing hero, track cards, and a
  "how to use this" for both learner and reference-user.

## Lesson roadmap (outlines built now; deepened over time)

Ordered by owner priority. Tracks build toward LLMs-in-science.

**Track A — Inference foundations**
1. Bayesian statistics *(exists; being deepened)*
2. p-values & hypothesis testing (null, type I/II, what a p-value is *not*)
3. t-tests & the t-distribution (one/two-sample, paired, assumptions)
4. Confidence intervals & the bootstrap (interpretation traps)
5. Multiple comparisons & FDR (Bonferroni, Benjamini–Hochberg; genomics-heavy)
6. Statistical power & experimental design (effect size, sample size)

**Track B — Data transformation / normalization**
7. Normalization & standardization (z-score, min–max, log/rlog/VST, quantile) —
   when each is right, what each distorts; RNA-seq framing.

**Track C — Regression & models**
8. Linear regression (assumptions, diagnostics, residual plots)
9. Logistic regression & GLMs (odds, link functions, calibration)
10. Regularization & the bias–variance tradeoff (ridge/lasso, CV)

**Track D — Machine learning fundamentals** *(the interview core)*
11. The ML workflow — **decision flowcharts**: framing a problem, choosing a
    model, splitting data, what stats to capture, which plots to generate.
12. Model evaluation & selection (train/val/test, CV, ROC/PR, confusion matrix,
    leakage, class imbalance) — hands-on "train a small model" problems.
13. Unsupervised learning (PCA/UMAP/clustering; interpretation and pitfalls).

**Track E — Toward LLMs in science** *(the destination)*
14. Embeddings & similarity (what a vector "means," cosine similarity).
15. What a language model actually learns (tokens, attention at intuition level,
    next-token objective) — for broad scientists, not mathematicians.
16. Using LLMs to find patterns in scientific data/text (retrieval, clustering
    embeddings, evals, hallucination & calibration, when *not* to trust them).

Each roadmap entry ships now as a stub `index.qmd` with objectives + module
skeleton + "interview questions this unlocks," so the structure is visible and
fillable.

## ML flowcharts

Mermaid diagrams (Quarto-native) for decision trees like "which model?",
"which metric?", "is my model overfitting?". Kept in the ML lessons and the
roadmap so the *process* is teachable, not just the concepts.

## Build order (scope discipline)

1. **Foundation:** SCSS theme + signature components, homepage + roadmap,
   citation infra, one flagship OJS figure. (Reusable — do first.)
2. **Re-skin + re-voice Lesson 1** on the new foundation; add a science example
   (FDR / base rates in significance testing) and the `interview.qmd` page.
3. **Roadmap stubs** for lessons 2–16 with objectives + interview-question lists.
4. Deepen Bayesian modules with fuller worked prose + the OJS explorer.

No Python/Shinylive — OJS covers the interactivity described. Add compute
engines to pixi only when a specific lesson needs them.

## Non-goals (YAGNI)

- No user accounts / auto-graded submissions (Rosalind's server side). Solutions
  are collapsible; honor system.
- No external fonts or JS CDNs (self-contained requirement).
- No Python/R execution until a lesson genuinely needs it.
