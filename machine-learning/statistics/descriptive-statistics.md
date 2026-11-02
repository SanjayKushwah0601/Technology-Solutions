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

## Measures of center

| Measure | What it describes | When it helps |
| --- | --- | --- |
| Mean | Average value | Symmetric data without extreme outliers |
| Median | Middle value when sorted | Skewed data or outliers |
| Mode | Most frequent value | Categories or multimodal distributions |

Example: incomes `{30k, 32k, 35k, 40k, 500k}` — the mean is pulled up by 500k; the median better reflects a “typical” person.

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