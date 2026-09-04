# Complete Machine Learning Study Material

A personal, exhaustive **classical machine learning** learning-and-reference notebook set — one Jupyter
notebook per chapter, every notebook committed with its outputs so it reads on GitHub without running
anything.

**Scope: classical ML only.** No deep learning. Neural networks appear exactly once, in §1.7, to mark where
this material deliberately stops and why.

Every algorithm chapter follows the same three-step shape:

```text
the objective, written out  ->  a from-scratch NumPy implementation  ->  the scikit-learn equivalent
                            ->  an assertion that the two agree
```

Start with **[`00_index.ipynb`](./00_index.ipynb)** — it holds the conventions, the notation table, the
chapter coverage tracker and the cross-reference index.

## Chapters

### Part I — Foundations

| # | Chapter | Covers |
|---|---|---|
| 1 | [Machine Learning Fundamentals](./01_ml_fundamentals.ipynb) | What ML is, ML vs. rule-based code, the types of learning, core vocabulary, the end-to-end workflow, where classical ML stops |
| 2 | [Mathematical Foundations](./02_math_foundations.ipynb) | Linear algebra, eigendecomposition and SVD, gradients and the chain rule, probability, statistics — each computed in NumPy |
| 3 | [The Python ML Stack](./03_python_ml_stack.ipynb) | NumPy, pandas, matplotlib/seaborn, and the scikit-learn estimator API contract |

### Part II — Data

| # | Chapter | Covers |
|---|---|---|
| 4 | [Data and Exploratory Data Analysis](./04_data_and_eda.ipynb) | Variable types, dataset sources, univariate → multivariate EDA, correlation structure, target analysis |
| 5 | [Data Preprocessing](./05_data_preprocessing.ipynb) | Missing data, outliers, structural repair, scaling, distribution transforms — and why the split comes first |
| 6 | [Feature Engineering](./06_feature_engineering.ipynb) | Categorical encoding, binning, interactions, datetime/cyclical features, text features, fit-on-train-only |
| 7 | [Feature Selection and Dimensionality Reduction](./07_feature_selection_and_dimensionality_reduction.ipynb) | Curse of dimensionality, filter/wrapper/embedded selection, PCA, LDA, t-SNE |

### Part III — The Learning Framework

| # | Chapter | Covers |
|---|---|---|
| 8 | [Model Evaluation and Validation](./08_model_evaluation_and_validation.ipynb) | Cross-validation strategies, regression and classification metrics, thresholds, calibration, baselines |
| 9 | [Bias, Variance and Regularization](./09_bias_variance_and_regularization.ipynb) | Over/underfitting, the bias–variance decomposition by simulation, learning and validation curves |
| 10 | [Optimization and Gradient Descent](./10_optimization_and_gradient_descent.ipynb) | Loss functions, convexity, gradient descent from scratch, learning rates, momentum |

### Part IV — Supervised Learning

| # | Chapter | Covers |
|---|---|---|
| 11 | [Linear Regression](./11_linear_regression.ipynb) | OLS derived, the normal equation from scratch, assumptions and residual diagnostics, VIF, polynomial regression |
| 12 | [Regularized Linear Models](./12_regularized_linear_models.ipynb) | Ridge, lasso, elastic net, why L1 zeroes coefficients, regularization paths |
| 13 | [Logistic Regression](./13_logistic_regression.ipynb) | Sigmoid, log-odds, cross-entropy derived, from-scratch gradient descent, decision boundaries, softmax |
| 14 | [k-Nearest Neighbors](./14_knn_and_distance_metrics.ipynb) | Distance metrics, kNN from scratch, choosing k, why scaling is mandatory, search structures |
| 15 | [Naive Bayes](./15_naive_bayes.ipynb) | Bayes as a classifier, the naive assumption, Gaussian NB from scratch, smoothing, text classification |
| 16 | [Support Vector Machines](./16_support_vector_machines.ipynb) | Maximum margin, soft margin and C, hinge loss, the kernel trick, SVR |
| 17 | [Decision Trees](./17_decision_trees.ipynb) | Impurity measures, CART from scratch, pruning, regression trees, importance biases |
| 18 | [Ensembles I: Bagging and Random Forests](./18_ensembles_bagging_and_random_forests.ipynb) | Why averaging works, the bootstrap, bagging from scratch, OOB scoring, random forests |
| 19 | [Ensembles II: Boosting and Stacking](./19_ensembles_boosting_and_stacking.ipynb) | AdaBoost and gradient boosting from scratch, XGBoost/LightGBM/CatBoost, stacking |

### Part V — Unsupervised Learning

| # | Chapter | Covers |
|---|---|---|
| 20 | [Clustering](./20_clustering.ipynb) | k-means from scratch, hierarchical clustering, DBSCAN, Gaussian mixtures, cluster evaluation |
| 21 | [Anomaly Detection and Association Rules](./21_anomaly_detection_and_association_rules.ipynb) | Statistical detection, Isolation Forest, LOF, One-Class SVM; support/confidence/lift, Apriori, FP-Growth |

### Part VI — Practice

| # | Chapter | Covers |
|---|---|---|
| 22 | [Imbalanced Data and Data Leakage](./22_imbalanced_data_and_leakage.ipynb) | Resampling done right, class weights, threshold tuning, and the full leakage taxonomy |
| 23 | [Pipelines and Hyperparameter Tuning](./23_pipelines_and_hyperparameter_tuning.ipynb) | Pipeline/ColumnTransformer, custom transformers, grid/random/halving/Optuna search, nested CV |
| 24 | [Interpretability and Deployment](./24_interpretability_and_deployment.ipynb) | Permutation importance, PDP/ICE, SHAP, LIME, persistence, monitoring and drift |

## Running it

Dependencies are managed with [uv](https://docs.astral.sh/uv/); `pyproject.toml` and `uv.lock` are committed,
so the environment is reproducible exactly.

```bash
uv sync              # create .venv and install the locked dependency set
uv run jupyter lab   # open the notebooks
```

Re-execute a chapter from a terminal:

```bash
uv run jupyter nbconvert --to notebook --execute --inplace 11_linear_regression.ipynb
```

## Data

No notebook downloads anything. Data comes from `sklearn.datasets` bundled loaders, the `make_*` synthetic
generators, and two small CSVs in [`data/`](./data):

| File | Rows | What it is |
|---|---|---|
| `customers.csv` | 1012 | A deliberately messy subscription table — missing values, six spellings of two genders, a numeric column stored as text with blanks, duplicate rows, impossible ages, and one genuine target-leakage column. Used by Chapters 4–6 and 22. |
| `transactions.csv` | 2622 | 800 shopping baskets in long format, with real co-occurrence structure to find. Used by Chapter 21. |

Both are generated, not scraped — no real people, nothing to anonymize.

## Conventions

Every stochastic call is seeded, so a committed output is the output the code actually produced and any
difference on re-execution is a real change rather than noise. The full style guide lives in
[`CLAUDE.md`](./CLAUDE.md); the short version is in §0.3–0.5 of the index notebook.
