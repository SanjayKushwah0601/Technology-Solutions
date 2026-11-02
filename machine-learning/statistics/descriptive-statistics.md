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

## Measures of spread

| Measure | What it describes | Notes |
| --- | --- | --- |
| Variance | Average squared distance from the mean | Units are squared; sensitive to outliers |
| Standard deviation (SD) | Square root of variance | Same units as the data |
| Range | Max − min | Simple but fragile to extremes |
| IQR | Q3 − Q1 (middle 50%) | Robust; used with box plots |
| Percentile / quartile | Position in ordered data | Q1 = 25th, Q2 = median, Q3 = 75th |

Rough reading of SD (for roughly normal data): about **68%** of values fall within 1 SD of the mean, and about **95%** within 2 SD.

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