# Descriptive Statistics

Summarize the data you already have — center, spread, shape, and simple plots — **without** claiming anything about a larger population.

Back to [Theory](./theory.md) · overview in [Branches](./theory.md#branches-of-statistics) · measures also listed in [Theory → Descriptive statistics](./theory.md#descriptive-statistics-measures).

## What it is for

| Goal | Example question |
| --- | --- |
| Center | What is a typical value? |
| Spread | How much do values vary? |
| Shape | Is the distribution skewed or heavy-tailed? |
| Display | What does a histogram or box plot show? |

Use several measures together. The mean alone can hide skew and outliers.

## Measures of central tendency

Three common ways to describe a “typical” value: **mean**, **median**, and **mode**. Pick by data type and shape — not habit.

| Measure | Idea | Best with |
| --- | --- | --- |
| Mean | Arithmetic average | Symmetric numeric data, few outliers |
| Median | Middle value when sorted | Skewed numeric data or outliers |
| Mode | Most frequent value | Categories; also multimodal numeric data |

### Mean

Sum of values divided by count: **x̄ = (x₁ + x₂ + … + xₙ) / n**.

| | |
| --- | --- |
| **Use when** | Data are roughly symmetric; you care about the total/average (costs, scores, sensor readings); every point should influence the summary |
| **Avoid when** | Strong skew or extreme outliers; open-ended scales (“10+”); or the variable is categorical (no sensible average of “red” and “blue”) |

**Example — good fit:** exam scores `{72, 75, 78, 80, 85}` → mean ≈ **78**. Values cluster; mean matches a typical student.

**Example — poor fit:** incomes `{30k, 32k, 35k, 40k, 500k}` → mean = **127.4k**. One CEO pulls the average far above what most people earn. Prefer the median here.

### Median

Sort the data. For odd *n*, take the middle value; for even *n*, average the two middle values.

| | |
| --- | --- |
| **Use when** | Distribution is skewed; outliers exist; you want a “typical person” that half the sample sits below and half above (income, house prices, latency with rare spikes) |
| **Avoid when** | You need a summary that uses every value equally (e.g. total cost / n); data are unordered categories; or *n* is tiny and you still need to report an average for planning totals |

**Example — good fit:** same incomes `{30k, 32k, 35k, 40k, 500k}` → median = **35k**. Matches a typical earner; the 500k barely moves it.

**Example — poor fit:** you must budget total payroll for 5 people earning those incomes. Median 35k × 5 understates the real sum; the **mean** (or the total itself) is what finance needs.

### Mode

The value that appears most often. A set can be unimodal, bimodal, multimodal, or have no unique mode.

| | |
| --- | --- |
| **Use when** | Data are **categorical** (most common city, plan tier, error code); or numeric data have clear peaks you care about (most common shoe size, most common transaction amount) |
| **Avoid when** | Every value is unique (continuous measurements with high precision — often no useful mode); or you need a balance point / total-based average |

**Example — good fit:** support tickets tagged `{login, login, billing, login, shipping}` → mode = **login**. That is the issue to staff first.

**Example — poor fit:** heights in cm `{170.1, 171.4, 168.9, 172.0, 169.5}` — each value appears once, so mode adds nothing. Use mean or median instead.

### Quick chooser

| Situation | Prefer |
| --- | --- |
| Symmetric numeric, few outliers | Mean |
| Skewed numeric or heavy outliers | Median |
| Categories / “most common” | Mode |
| Mean and median far apart | Investigate skew/outliers; report median (and maybe both) |
| Need total ÷ n (budget, average cost) | Mean |

**Same data, three answers:** `{2, 2, 3, 5, 100}` → mode = **2**, median = **3**, mean = **22.4**. All are valid; they answer different questions.

## Measures of dispersion (spread)

Central tendency says where the data sit. **Dispersion** says how spread out they are. Same mean with tiny vs huge spread tells very different stories.

| Measure | Idea | Best with |
| --- | --- | --- |
| Range | Max − min | Quick glance; tiny clean sets |
| Variance | Average squared distance from the mean | Math / modeling; when squared units are OK |
| Standard deviation (SD) | √variance — spread in original units | Symmetric numeric data; reporting with the mean |
| Percentile | Value below which P% of data fall | Ranking, thresholds, “top/bottom X%” |
| Quartiles | 25th / 50th / 75th percentiles | Five-number summary; feed into IQR |
| IQR | Q3 − Q1 (middle 50%) | Skew or outliers; pair with the median |

Running example below: scores **A = {2, 4, 4, 4, 5, 5, 7, 9}** (*n* = 8).

### Range

**Formula:** Range = max − min.

**Easy steps:** find the largest value → find the smallest → subtract.

| | |
| --- | --- |
| **Use when** | You need a one-second sense of full span (daily high−low temperature, exam score band) |
| **Avoid when** | Outliers exist (one bad value inflates the whole range); comparing groups of different size; you need a stable summary for skewed data |

**Example — good fit:** A → max 9, min 2 → range = **7**. Clean, no wild extremes.

**Example — poor fit:** `{2, 4, 4, 4, 5, 5, 7, 90}` → range = **88**. Almost everyone is still 2–7; the range lies about one typo.

### Variance

Average of squared distances from the mean. Squaring removes negative signs and weights big gaps more.

**Formulas (sample — usual for data you collected):**

- Population: **σ² = Σ (xᵢ − μ)² / N**
- Sample: **s² = Σ (xᵢ − x̄)² / (n − 1)** ← divide by *n − 1* (Bessel’s correction)

**Easy steps (sample):**

1. Find the mean x̄.
2. For each value, compute (x − x̄), then square it.
3. Add the squared differences.
4. Divide by (**n − 1**).

| | |
| --- | --- |
| **Use when** | You need a building block for SD, ANOVA, or many ML losses; comparing relative spread in squared units is fine |
| **Avoid when** | You want a number people can read in the original units (prefer SD); data are categorical; outliers dominate the squares |

**Example — walkthrough on A:** mean x̄ = (2+4+4+4+5+5+7+9)/8 = **5**.

| x | x − 5 | (x − 5)² |
| --- | --- | --- |
| 2 | −3 | 9 |
| 4 | −1 | 1 |
| 4 | −1 | 1 |
| 4 | −1 | 1 |
| 5 | 0 | 0 |
| 5 | 0 | 0 |
| 7 | 2 | 4 |
| 9 | 4 | 16 |
| | | **Sum = 32** |

s² = 32 / (8 − 1) = **≈ 4.57**. Units are “score²” — hard to interpret alone.

### Standard deviation (SD)

**Formula:** SD = √variance → sample **s = √s²**, population **σ = √σ²**.

**Easy steps:** compute variance → take the square root. Same units as the data.

| | |
| --- | --- |
| **Use when** | Reporting spread next to the mean; roughly symmetric numeric data; rule-of-thumb bands (mean ± 1 SD, ± 2 SD) |
| **Avoid when** | Strong skew or heavy outliers (SD is pulled by extremes); you care about the middle bulk only (prefer IQR); categories |

**Rough reading (approx. normal data):** about **68%** of values within 1 SD of the mean; about **95%** within 2 SD.

**Example — good fit:** A → s = √4.57 ≈ **2.14**. “Typical score is about 5 ± 2.”

**Example — poor fit:** incomes with one billionaire — SD explodes; a “mean ± SD” band is misleading. Prefer **IQR** (and median).

### Percentile

The **P-th percentile** is a value such that about **P%** of the ordered data are at or below it (and about (100 − P)% are at or above it).

Examples of language:

- 50th percentile = median
- 90th percentile = only ~10% of values are higher
- “Scored in the 80th percentile” = did as well as or better than ~80% of the group

**Formula (nearest-rank — easy hand method):**

1. Sort the data ascending: x₁ ≤ x₂ ≤ … ≤ xₙ.
2. Compute rank **i = ceil(P / 100 × n)** (round up to the next whole number if needed).
3. The P-th percentile ≈ **xᵢ** (the value at position *i*).

If you land between two ranks, many tools average the two neighbors. For learning by hand, nearest-rank is enough.

| | |
| --- | --- |
| **Use when** | Ranking people or items; setting SLOs (“p95 latency”); cut scores (“top 10% get a discount”); describing position without assuming a normal shape |
| **Avoid when** | *n* is very small (percentiles jump between a few points); comparing percentiles from samples of very different size without care; treating a percentile as a probability from a fitted model unless you built one |

**Example — 25th, 50th, 90th on A:** sorted `{2, 4, 4, 4, 5, 5, 7, 9}`, *n* = 8.

| P | i = ceil(P/100 × 8) | Percentile value |
| --- | --- | --- |
| 25 | ceil(2) = 2 | x₂ = **4** |
| 50 | ceil(4) = 4 | x₄ = **4** |
| 90 | ceil(7.2) = 8 | x₈ = **9** |

**Example — good fit:** API latency — report **p50** (typical) and **p95** / **p99** (tail). Means hide slow spikes; high percentiles show them.

**Example — poor fit:** only 4 exam scores. The “90th percentile” is basically the max; it does not mean much until *n* is larger.

### Quartiles

**Quartiles** are named percentiles that split ordered data into four roughly equal parts:

| Name | Percentile | Meaning |
| --- | --- | --- |
| Q1 | 25th | Bottom of the middle half |
| Q2 | 50th | Median |
| Q3 | 75th | Top of the middle half |

**Easy steps (split method for small *n*):**

1. Sort ascending.
2. Q2 = median (middle; or average of two middles if *n* even).
3. Q1 = median of the **lower half** (values below Q2).
4. Q3 = median of the **upper half** (values above Q2).

*(Software percentile rules can differ slightly from nearest-rank or this split; for hand work either method is fine — stay consistent.)*

| | |
| --- | --- |
| **Use when** | Building a five-number summary (min, Q1, median, Q3, max); feeding **IQR**; box plots |
| **Avoid when** | Same limits as percentiles — tiny *n*, or when you only need one custom cut (use that percentile directly, e.g. 90th) |

**Example on A:** sorted `{2, 4, 4, 4, 5, 5, 7, 9}`.

- Q2 (median) = average of 4th and 5th = (4+5)/2 = **4.5**
- Lower half `{2, 4, 4, 4}` → Q1 = (4+4)/2 = **4**
- Upper half `{5, 5, 7, 9}` → Q3 = (5+7)/2 = **6**

### Interquartile range (IQR)

**Formula:** IQR = Q3 − Q1.

**Easy steps:** find Q1 and Q3 → subtract. Ignores the outer 25% on each side.

| | |
| --- | --- |
| **Use when** | Skewed data or outliers; pair with the **median**; box plots; robust “typical spread” of the middle half |
| **Avoid when** | You must reflect every point including extremes (risk, worst-case range); you need SD for a parametric method that assumes it |

**Example — good fit:** A → IQR = 6 − 4 = **2**. Middle half of scores spans only 2 points.

**Example — contrast with range:** add outlier → `{2, 4, 4, 4, 5, 5, 7, 90}`. Range jumps to 88; IQR often stays near **2**. IQR tells the truth about the bulk; range does not.

### Quick chooser

| Situation | Prefer |
| --- | --- |
| Fast full span, clean data | Range |
| Report spread with the mean | SD |
| Building block / squared error world | Variance |
| Skew, outliers, box plots | IQR (+ median) |
| “Top 10%” / cut scores / p95 latency | Percentiles |
| Box plot / middle-half spread | Quartiles → IQR |
| Range and IQR disagree a lot | Outliers or heavy tails — investigate |

**Same idea as center:** mean ↔ SD; median ↔ IQR. Match the pair to the shape of the data.

## Shape

| Measure | What it describes |
| --- | --- |
| Skewness | Asymmetry — right-skewed means a long right tail (mean often > median) |
| Kurtosis | How heavy the tails are relative to a normal distribution |

**Rule of thumb:** if mean and median differ a lot, check skew and outliers before trusting the mean.

## Common displays

| Plot | Use |
| --- | --- |
| Histogram | Shape, modality, rough spread |
| Box plot | Median, IQR, possible outliers |
| Frequency table | Counts for categories |
| Bar chart | Compare category frequencies |

## Descriptive vs inferential (quick)

| | Descriptive | Inferential |
| --- | --- | --- |
| Scope | This dataset only | Beyond this dataset |
| Output | Summaries and plots | Estimates, intervals, tests |
| Claim | “In this sample, mean = …” | “The population mean is likely …” |

In ML, descriptive work is most of **EDA**: catch skew, bad labels, and leaks before you train.