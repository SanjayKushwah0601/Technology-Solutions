# Statistics Theory

Core statistical ideas used in machine learning. Concepts only — no code.

## What is statistics?

Statistics is a branch of mathematics that involves collecting, analyzing, interpreting, presenting, and organizing data. It is used to make decisions or predictions based on data.

In practice, statistics answers questions like: What patterns exist in this dataset? How confident are we in an estimate? Did a change actually improve the outcome, or is the difference just noise?

### Key concepts

- Descriptive statistics — summarize what you already have
- Inferential statistics — generalize from a sample to a population
- Probability — formal language for uncertainty and chance
- Population vs sample — the full set vs what you observed
- Hypothesis testing — decide whether data contradict a default claim
- Correlation and regression — measure and model relationships
- Variance and standard deviation — quantify spread

## Branches of statistics

Statistics is commonly divided into two major branches. Most ML workflows use both: descriptive tools during EDA, and inferential ideas when judging metrics, A/B tests, or model comparisons.

### Descriptive

Descriptive statistics summarizes and describes observed data **without** trying to generalize beyond it.

- **Question it answers:** What does the data look like?
- **Typical steps:** center (mean/median), spread (range/variance/SD), shape (skew), and visuals (histogram, box plot)
- **Examples:** mean, median, mode, range, variance, standard deviation, percentile, quartile, histogram, box plot, frequency table

### Inferential

Inferential statistics uses information from a **sample** to draw conclusions about a larger **population**, while accounting for uncertainty.

- **Goal:** Drawing conclusions from data
- **Why uncertainty matters:** every sample is one of many possible samples; estimates bounce around
- **Examples:** estimation, confidence intervals, hypothesis testing, regression and relationships

| Branch | Scope | Typical output |
| --- | --- | --- |
| Descriptive | This dataset only | Summary numbers and plots |
| Inferential | Beyond this dataset | Estimates, intervals, p-values, models |

## Types of data

Based on its nature, data can be classified in three ways: structure, time dimension, and number of variables. The same dataset can sit in more than one bucket (for example, a structured multivariate time series).

```text
Data
├── Type 1 — Structure
│   ├── Structured
│   └── Unstructured
├── Type 2 — Time dimension
│   ├── Cross-sectional
│   └── Time series
└── Type 3 — Number of variables
    ├── Univariate
    └── Multivariate
```

| Classification | Type | Meaning / examples | Why it matters |
| --- | --- | --- | --- |
| Structure | Structured | Tables, spreadsheets, relational databases | Fits rows/columns; easy for classical ML |
| Structure | Unstructured | Multimedia, text, web pages | Needs parsing, embeddings, or NLP/CV pipelines |
| Time dimension | Cross-sectional | Collected at a single point in time | No order over time; treat rows as independent (often) |
| Time dimension | Time series | Collected over a sequence of time intervals | Order and lag matter; leakage risk if shuffled |
| Number of variables | Univariate | Single variable | Simple distributions and summaries |
| Number of variables | Multivariate | Two or more variables | Relationships, multicollinearity, joint models |

## Types of variables

Variable type decides how you encode features, which plots make sense, and which models or metrics are valid.

```text
Variables
├── Categorical (labels or groups)
│   ├── Nominal — no natural order
│   └── Ordinal — natural order
└── Numerical (quantities or measurements)
    ├── Interval — no true zero
    └── Ratio — true zero
```

### Categorical variables

Categorical variables represent groups, classes, or labels rather than numerical quantities. Arithmetic like “average city” is usually meaningless until you encode the categories for a model.

#### Nominal variables

Nominal variables have categories with **no ranking or order**.

| Variable | Possible values |
| --- | --- |
| City | Indore, Mumbai, Delhi |
| Color | Red, Blue, Green |
| Programming language | Python, Java, Go |

You cannot say Mumbai is “greater than” Delhi, or that Python ranks above Java.

**In ML:** Predicting a customer’s city category, or encoding product types as model features. A common technique is **one-hot encoding** — each category becomes its own 0/1 column so the model does not invent a false order.

One-hot encoding example (color):

| Color | R | G | B |
| --- | --- | --- | --- |
| R | 1 | 0 | 0 |
| G | 0 | 1 | 0 |
| B | 0 | 0 | 1 |

With many categories, one-hot tables get wide. Alternatives include target encoding, hashing, or embeddings — still with care for leakage.

#### Ordinal variables

Ordinal variables have categories with a **natural order** (for example: low / medium / high, or rating 1–5), but the gaps between levels are not necessarily equal. “High” is above “medium,” yet the step from low→medium may not match medium→high.

**In ML:** Sometimes map to integers (1, 2, 3) when order matters; avoid treating them as continuous without checking that the spacing assumption is reasonable.

### Numerical variables

Numerical variables represent quantities or measurements. You can compare magnitudes and (with care) compute differences and averages.

| Type | Meaning | Example | Allowed operations |
| --- | --- | --- | --- |
| Interval | Ordered values with equal gaps, but **no true zero** | Temperature in °C | Differences make sense; ratios often do not (20°C is not “twice as hot” as 10°C) |
| Ratio | Ordered values with equal gaps and a **true zero** | Height, weight, income, counts | Differences and ratios both make sense |

**Discrete vs continuous:** counts are discrete (0, 1, 2, …); measurements like height are continuous (any value in a range, given precision).

## Population and sample

- A **population** is the full set of observations you care about (all users, all invoices this year, all possible clicks).
- A **sample** is the subset you actually observe (logged users last week, a random 10k rows).
- A **parameter** describes the population (true mean μ). A **statistic** describes the sample (sample mean x̄).
- Statistics estimates population properties from samples.
- A good sample is **representative**; a biased sample systematically misses or overweights parts of the population.
- In ML, the “population” is often future data under the same process. Train/validation/test splits are samples meant to stand in for that future.

## Descriptive statistics (measures)

Summarize a sample without making claims about a larger population. Use several measures together — mean alone hides skew and outliers.

### Measures of center

| Measure | What it describes | When it helps |
| --- | --- | --- |
| Mean | Average value | Symmetric data without extreme outliers |
| Median | Middle value | Skewed data or outliers |
| Mode | Most frequent value | Categories or multimodal distributions |

### Measures of spread

| Measure | What it describes | Notes |
| --- | --- | --- |
| Variance | Average squared distance from the mean | Units are squared; sensitive to outliers |
| Standard deviation (SD) | Square root of variance | Same units as the data; common scale for spread |
| Range | Max − min | Simple but fragile to extremes |
| IQR | Q3 − Q1 (middle 50%) | Robust spread for box plots |
| Percentile / quartile | Position within ordered data | Q1 = 25th, Q2 = median, Q3 = 75th |

### Shape

| Measure | What it describes |
| --- | --- |
| Skewness | Asymmetry — right-skewed means a long right tail (mean often > median) |
| Kurtosis | How heavy the tails are relative to a normal distribution |

**Rule of thumb:** if mean and median differ a lot, check skew and outliers before trusting the mean.

## Distributions

A **probability distribution** assigns probabilities to outcomes. It is the theoretical shape you assume or estimate for a random variable.

- **Discrete:** countable outcomes (Bernoulli, Binomial, Poisson). Use a **PMF** (probability mass function).
- **Continuous:** outcomes on a continuum (Normal, Uniform, Exponential). Use a **PDF** (probability density function); probability over an interval is the area under the curve.
- **CDF:** cumulative distribution function — P(X ≤ x).
- The **Normal (Gaussian)** distribution is central because many averages concentrate around a mean (**central limit theorem**): sample means of i.i.d. data tend toward a normal shape as n grows.
- Other useful shapes: Bernoulli (binary outcomes), Binomial (count of successes), Poisson (counts of rare events), Exponential (waiting times).

Knowing the approximate distribution guides which tests, intervals, and loss functions are reasonable.

## Sampling

How you draw the sample affects every later conclusion. Bad sampling cannot be fixed by a fancier model.

| Idea | Meaning |
| --- | --- |
| Simple random sample | Every subset of a given size is equally likely |
| Stratified sample | Sample within known subgroups (e.g. by region) so each group is represented |
| Cluster sample | Sample whole groups (e.g. schools), then observe everyone inside |
| Sampling bias | Systematic error from how data was collected (survivors only, volunteers only) |
| Sampling variability | Different samples give different estimates — expected, not a bug |
| Sample size | Larger samples usually reduce variance of estimates; they do not remove bias |

**ML link:** random splits assume rows are exchangeable. Time series, users with multiple rows, or leakage across splits break that assumption — use time-based or group-based splits instead.

## Estimation

- A **point estimate** is a single number for a parameter (e.g. sample mean for population mean).
- An **estimator** is the rule that produces the estimate (the formula or algorithm).
- **Bias:** expected difference between estimator and true value. Unbiased ≈ correct on average across samples.
- **Variance:** how much the estimator jumps across samples.
- **Bias–variance tradeoff:** lower bias can raise variance and vice versa; both contribute to error.
- **Consistency:** as sample size grows, the estimate tends to get closer to the true parameter (under conditions).
- **MSE (mean squared error)** ≈ bias² + variance — a single score for estimator quality.

## Confidence intervals

A **confidence interval** is a range that, under repeated sampling, covers the true parameter with a stated long-run frequency (e.g. 95%).

- Wider intervals = more uncertainty (or higher confidence level, e.g. 99% vs 95%).
- Narrower intervals = more precision, often from larger samples or lower variance.
- A 95% interval does **not** mean “95% probability the parameter is in this one interval” in the frequentist sense; it means the **method** covers the truth about 95% of the time across repeated samples.
- Overlapping intervals do not always settle “no difference”; use a proper comparison when decisions matter.

## Hypothesis testing

Formal way to decide whether data contradict a default claim. It does not prove the alternative is true — it asks whether the null is still plausible.

| Term | Meaning |
| --- | --- |
| Null hypothesis (H₀) | Default claim (often “no effect / no difference”) |
| Alternative (H₁) | Claim you are testing for |
| Test statistic | Summary of the data used for the decision |
| p-value | Probability of data at least as extreme as observed, **assuming H₀ is true** |
| Significance level (α) | Threshold for rejecting H₀ (e.g. 0.05) |
| Type I error | Reject H₀ when it is true (false positive) |
| Type II error | Fail to reject H₀ when H₁ is true (false negative) |
| Power | Probability of correctly rejecting H₀ when H₁ is true |

**How to read a p-value:** small p-value → data are surprising under H₀ → evidence against H₀. It is **not** “probability that H₀ is true,” and not “probability the result replicates.”

Common tests: t-tests (means), z-tests (large-sample means/proportions), chi-square (categorical association), ANOVA (several group means) — choice depends on data type and assumptions (independence, normality, equal variance, etc.).

## Correlation and regression (brief)

- **Correlation** measures how two variables move together (often Pearson for linear association). Range typically −1 to +1. Correlation ≠ slope magnitude in a useful units sense, and ≠ causation.
- **Regression** models how an outcome changes with predictors (e.g. linear regression: predict y from x). Coefficients, residuals, and R² describe fit — still subject to assumptions and confounding.

## Bias and variance (ML view)

In predictive models the same words show up with a modeling twist:

- **Bias:** error from wrong assumptions — model too simple (**underfitting**).
- **Variance:** sensitivity to the particular training sample — model too flexible (**overfitting**).
- **Irreducible error:** noise that no model can remove.
- Total expected prediction error ≈ bias² + variance + irreducible error.

**Practical levers:** more data and regularization often cut variance; richer features and more flexible models can cut bias (until they overfit). Validation curves and cross-validation help see the tradeoff.

## Correlation vs causation

- **Correlation:** two variables move together.
- **Causation:** changing one variable produces a change in the other.
- Correlation alone does not prove causation. **Confounders** (a third factor drives both), **reverse causality**, and **selection bias** can create associations without a causal link.
- Classic pattern: ice cream sales and drowning rates rise together in summer — temperature confounds both.
- Causal claims need design (randomized experiments, natural experiments) or careful assumptions, not just pairwise correlations or high feature importance.

## Why this matters for ML

- Sampling and splits decide whether metrics generalize.
- Bias/variance guide model complexity and regularization.
- Hypothesis tests and intervals quantify uncertainty in comparisons (e.g. A/B tests, model bake-offs).
- Confusing correlation with causation leads to wrong product and science decisions.
- Variable types decide encoding (one-hot, ordinal maps, scaling) and which models or metrics make sense.
- Descriptive EDA finds leaks, skew, and bad labels before you train.
