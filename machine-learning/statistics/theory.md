# Statistics Theory

Core statistical ideas used in machine learning. Concepts only — no code.

## What is statistics?

Statistics is a branch of mathematics that involves collecting, analyzing, interpreting, presenting, and organizing data. It is used to make decisions or predictions based on data.

### Key concepts

- Descriptive statistics
- Inferential statistics
- Probability
- Population vs sample
- Hypothesis testing
- Correlation and regression
- Variance and standard deviation

## Branches of statistics

Statistics is commonly divided into two major branches.

### Descriptive

Descriptive statistics summarizes and describes observed data **without** trying to generalize beyond it.

- **Question it answers:** What does the data look like?
- **Examples:** mean, median, mode, range, variance, standard deviation, percentile, quartile, histogram, box plot, frequency table

### Inferential

Inferential statistics uses information from a **sample** to draw conclusions about a larger **population**, while accounting for uncertainty.

- **Goal:** Drawing conclusions from data
- **Examples:** estimation, confidence intervals, hypothesis testing, regression and relationships

## Types of data

Based on its nature, data can be classified in three ways: structure, time dimension, and number of variables.

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

| Classification | Type | Meaning / examples |
| --- | --- | --- |
| Structure | Structured | Tables, spreadsheets, relational databases |
| Structure | Unstructured | Multimedia, text, web pages |
| Time dimension | Cross-sectional | Collected at a single point in time |
| Time dimension | Time series | Collected over a sequence of time intervals |
| Number of variables | Univariate | Single variable |
| Number of variables | Multivariate | Two or more variables |

## Types of variables

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

Categorical variables represent groups, classes, or labels rather than numerical quantities.

#### Nominal variables

Nominal variables have categories with **no ranking or order**.

| Variable | Possible values |
| --- | --- |
| City | Indore, Mumbai, Delhi |
| Color | Red, Blue, Green |
| Programming language | Python, Java, Go |

You cannot say Mumbai is “greater than” Delhi, or that Python ranks above Java.

**In ML:** Predicting a customer’s city category, or encoding product types as model features. A common technique is **one-hot encoding**.

One-hot encoding example (color):

| Color | R | G | B |
| --- | --- | --- | --- |
| R | 1 | 0 | 0 |
| G | 0 | 1 | 0 |
| B | 0 | 0 | 1 |

#### Ordinal variables

Ordinal variables have categories with a **natural order** (for example: low / medium / high), but the gaps between levels are not necessarily equal.

### Numerical variables

Numerical variables represent quantities or measurements.

| Type | Meaning | Example |
| --- | --- | --- |
| Interval | Ordered values with equal gaps, but **no true zero** | Temperature in °C |
| Ratio | Ordered values with equal gaps and a **true zero** | Height, weight, income |

## Population and sample

- A **population** is the full set of observations you care about.
- A **sample** is the subset you actually observe.
- Statistics estimates population properties from samples.
- A good sample is representative; a biased sample systematically misses or overweights parts of the population.

## Descriptive statistics (measures)

Summarize a sample without making claims about a larger population.

| Measure | What it describes |
| --- | --- |
| Mean | Average value |
| Median | Middle value (robust to outliers) |
| Mode | Most frequent value |
| Variance | Average squared distance from the mean |
| Standard deviation | Square root of variance (same units as the data) |
| Range / IQR | Spread via extremes or quartiles |
| Percentile / quartile | Position of a value within the ordered data |
| Skewness | Asymmetry of the distribution |
| Kurtosis | How heavy the tails are |

## Distributions

A **probability distribution** assigns probabilities to outcomes.

- **Discrete:** countable outcomes (Bernoulli, Binomial, Poisson).
- **Continuous:** outcomes on a continuum (Normal, Uniform, Exponential).
- The **Normal (Gaussian)** distribution is central in theory and practice because many averages concentrate around a mean (central limit theorem).
- **PDF / PMF:** density or mass of outcomes.
- **CDF:** probability that a random variable is less than or equal to a value.

## Sampling

How you draw the sample affects every later conclusion.

| Idea | Meaning |
| --- | --- |
| Simple random sample | Every subset of a given size is equally likely |
| Stratified sample | Sample within known subgroups |
| Sampling bias | Systematic error from how data was collected |
| Sampling variability | Different samples give different estimates |
| Sample size | Larger samples usually reduce variance of estimates |

## Estimation

- A **point estimate** is a single number for a parameter (e.g. sample mean for population mean).
- An **estimator** is the rule that produces the estimate.
- **Bias:** expected difference between estimator and true value.
- **Variance:** how much the estimator jumps across samples.
- **Bias–variance tradeoff:** lower bias can raise variance and vice versa; both contribute to error.

## Confidence intervals

A **confidence interval** is a range that, under repeated sampling, covers the true parameter with a stated long-run frequency (e.g. 95%).

- Wider intervals = more uncertainty (or higher confidence level).
- Narrower intervals = more precision, often from larger samples or lower variance.
- A 95% interval does **not** mean “95% probability the parameter is in this one interval” in the frequentist sense; it means the method covers the truth 95% of the time across repeated samples.

## Hypothesis testing

Formal way to decide whether data contradict a default claim.

| Term | Meaning |
| --- | --- |
| Null hypothesis (H₀) | Default claim (often “no effect / no difference”) |
| Alternative (H₁) | Claim you are testing for |
| Test statistic | Summary of the data used for the decision |
| p-value | Probability of data at least as extreme as observed, assuming H₀ is true |
| Significance level (α) | Threshold for rejecting H₀ (e.g. 0.05) |
| Type I error | Reject H₀ when it is true (false positive) |
| Type II error | Fail to reject H₀ when H₁ is true (false negative) |
| Power | Probability of correctly rejecting H₀ when H₁ is true |

Common tests: t-tests, z-tests, chi-square tests, ANOVA — choice depends on data type and assumptions.

## Bias and variance (ML view)

In predictive models:

- **Bias:** error from wrong assumptions (underfitting).
- **Variance:** sensitivity to the particular training sample (overfitting).
- **Irreducible error:** noise that no model can remove.
- Total expected prediction error ≈ bias² + variance + irreducible error.

## Correlation vs causation

- **Correlation:** two variables move together.
- **Causation:** changing one variable produces a change in the other.
- Correlation alone does not prove causation. Confounders, reverse causality, and selection bias can create associations without a causal link.
- Causal claims need design (experiments, natural experiments) or careful assumptions, not just pairwise correlations.

## Why this matters for ML

- Sampling and splits decide whether metrics generalize.
- Bias/variance guide model complexity and regularization.
- Hypothesis tests and intervals quantify uncertainty in comparisons.
- Confusing correlation with causation leads to wrong product and science decisions.
- Variable types decide encoding (one-hot, ordinal maps, scaling) and which models or metrics make sense.
