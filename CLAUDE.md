# Style guide — Complete Machine Learning Study Material

This file is the authority on *how* chapters are written. `00_index.ipynb` §0.3–0.5 is the short version;
this is the long one. Read it before editing any notebook.

## What this material is

An exhaustive personal reference for **classical machine learning**. Not a tutorial, not a course, not a
cheat sheet — a book-length notebook set that a reader learns from the first time and looks things up in
afterwards.

**Deep learning is out of scope.** Neural networks appear once, in §1.7, to mark the boundary. Do not add
a Keras/PyTorch example anywhere, however tempting the comparison.

## The per-concept rhythm

Every concept is **explanation + runnable demo, never one alone**:

```text
Markdown  ->  explanation (table / prose / "why it matters")
Code      ->  minimal runnable demo, inline # comments on the lines that matter
Markdown  ->  (optional) a named gotcha or a second angle
Code      ->  (optional) its own small demo cell
```

Rules that follow from that:

1. **One idea per code cell.** A cell that demonstrates three things gets split into three cells with
   markdown between them. The reference failure mode is a 40-line cell doing an entire worked example; do
   not write one.
2. **No fenced ` ```python ` blocks inside markdown** where a real code cell would do. Code that is meant to
   be read *and run* is a code cell. Fenced blocks are only for shell commands, pseudocode, or code that
   deliberately cannot run (illustrative library syntax for something not installed).
3. **Explanations are real explanations.** Not a restated heading. Say why the thing exists, what it is
   contrasted with, and what breaks without it.
4. **Tables for anything enumerable.** Metrics, kernels, linkage criteria, encoders, distance metrics,
   solver options, boosting libraries — a table beats six paragraphs.
5. **Inline `#` comments carry the expected output** on lines where the value is the point:
   `print(model.coef_)   # [2.998 1.501] -> recovers the true 3.0 and 1.5`.

## Named callouts

Two recurring callout forms, both bolded at the start of a markdown cell, each followed by its *own* small
code cell when it has something to demonstrate:

* `**Common mistake** — ...` — a specific, concrete error a reader will actually make. Show the wrong thing
  running and producing a plausible-but-wrong number, then the fix. A warning with no demonstration is
  worth much less than the same warning with the inflated score printed next to it.
* `**In practice** — ...` — what real teams do, and where the textbook answer diverges from the deployed
  one. Keep it factual and specific; no motivational filler.

## The algorithm-chapter contract

Chapters 11–21 each follow the same fixed order, and none of the four steps is optional:

1. **The objective, written out.** The loss or criterion in LaTeX, with every symbol defined against §25.3's
   notation table. Derive it far enough that the gradient/update rule is not pulled out of thin air.
2. **A from-scratch NumPy implementation.** Plain NumPy, no scikit-learn. Small, readable, and written so
   the mechanism is visible — clarity beats efficiency here every time.
3. **The scikit-learn equivalent.** The same problem, the library call, the hyperparameters that matter.
4. **An assertion that the two agree.** `np.allclose(...)` or an explicit printed comparison. Claiming the
   from-scratch version is correct is not the same as showing it.

Where the from-scratch version *cannot* reasonably match sklearn (SVM's QP solver, the boosting libraries'
histogram binning), say so explicitly and compare predictions or scores instead of parameters.

## Numbering

* **Chapter numbers are frozen.** 1–24, plus 0 (conventions) and 25 (appendix) in `00_index.ipynb`.
* **New sub-sections append** to the end of a chapter, before the `x.9` bucket if one exists.
* **`x.9` is an optional overflow bucket.** Drop it when a chapter is otherwise complete rather than
  leaving an empty heading.
* **Deeper levels are free-form** — `17.3.2` can be created and reordered freely.
* **Moving or renaming a section** means fixing every pointer to it, including `00_index.ipynb` §25.1 and
  §25.2.

## Cross-references

Refer to sections by number, in prose, densely: "the scaling requirement from 5.5", "13.1's sigmoid".
Pointers are by *section number*, never by file path — the reader resolves the chapter number to the file.
Every substantive cross-reference should also appear in the Appendix cross-reference index (§25.2).

## Notebook mechanics

* **Committed with outputs.** A chapter is committed only after executing top to bottom with zero error
  outputs. `uv run jupyter nbconvert --to notebook --execute --inplace NN_*.ipynb`.
* **Seed everything.** `RANDOM_STATE = 42` at the top of each chapter that needs it, passed to every split,
  generator, resampler, initializer, optimizer and sampler that accepts a seed. Re-execution must reproduce
  the committed output.
* **Keep it fast.** No cell should take more than a few seconds; no chapter more than a minute. Use small
  `n`, few estimators, and short search grids. A slow chapter does not get read twice.
* **No downloads.** `sklearn.datasets` bundled loaders, the `make_*` generators, and `data/*.csv` only.
* **Plots**: one point per figure, labelled axes, a title that states the takeaway rather than restating the
  axes. Default matplotlib/seaborn styling — no custom themes.

## Structural template for a chapter file

```text
markdown   backlink cell -> 00_index.ipynb
markdown   ## N. Title  +  *Scope:* one sentence
markdown   ### N.1 Section
code       ...
markdown   ### N.2 Section
code       ...
...
code       # --- N. Title — scratch cell ---
```

## Tone

Plain, direct, technical. Define a term the first time it is used and then use it. No hedging, no
enthusiasm markers, no "as we can see". Assume an intelligent reader who does not yet know this material and
will notice if a claim is hand-waved.
