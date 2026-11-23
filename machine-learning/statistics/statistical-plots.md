# Statistical Plots

Visual summaries used in EDA: **histograms**, **box plots**, and **scatter plots**. Concepts only — no code.

Back to [Theory](./theory.md) · related measures in [`descriptive-statistics.md`](./descriptive-statistics.md).

## Contents

1. [Histograms](#histograms)
2. [Types of histograms based on skewness](#types-of-histograms-based-on-skewness)
3. [Types of histograms based on modes](#types-of-histograms-based-on-modes)
4. [Box plots](#box-plots)
5. [Scatter plots and their types](#scatter-plots-and-their-types)

## Histograms

A **histogram** shows how a **numeric** variable is distributed. You split the range into bins (intervals), count how many values fall in each bin (**frequency**), and draw bars whose height is that count (or relative frequency).

| Part | Role |
| --- | --- |
| X-axis | Value range (bins / class intervals) |
| Y-axis | Frequency or relative frequency |
| Bar width | Bin width |
| Bar height | How many points (or what share) land in that bin |

**Unlike a bar chart:** histogram bins are ordered numeric intervals and usually touch; bar charts compare categories and often have gaps.

**Easy steps:**

1. Choose bin width (or number of bins).
2. Count values in each bin ([frequency](./descriptive-statistics.md#frequency-relative-frequency-cumulative-frequency)).
3. Draw adjacent bars.
4. Read shape: center, spread, skew, peaks, gaps, outliers.

| | |
| --- | --- |
| **Use when** | One continuous (or finely discrete) variable; you want shape, skew, modality, rough spread |
| **Avoid when** | Pure categories (use a bar chart); binning is arbitrary and you over-read tiny bumps; *n* is tiny (shape is noise) |

**Bin tip:** too few bins → oversimplified lump; too many → spiky noise. Try a few widths before trusting a “pattern.”

**ML link:** check feature/label skew before scaling; spot multimodal mixes (e.g. two user segments) that one global model may mishandle.

## Types of histograms based on skewness

Skewness is about **asymmetry** — which side has the longer tail.

```text
Skewness shapes
├── Symmetric (approx. zero skew)
├── Right-skewed (positive skew) — long right tail
└── Left-skewed (negative skew) — long left tail
```

| Type | Look | Mean vs median (typical) | Example |
| --- | --- | --- | --- |
| **Symmetric** | Mirror-like around the center; bell-ish or flat-ish | Mean ≈ median ≈ mode | Heights in a narrow age group; measurement error |
| **Right-skewed** | Bulk on the left; long tail to the **right** | Mean > median | Income, house prices, request latency |
| **Left-skewed** | Bulk on the right; long tail to the **left** | Mean < median | Easy exam scores (most near 100); age at retirement in some samples |

**Memory aid:** the skew is named after the **tail**, not the hump. Right-skewed = tail points right.

| | |
| --- | --- |
| **Use this reading when** | Choosing mean vs median; deciding on log transforms; checking model error assumptions |
| **Don’t overclaim when** | Bins hide a weak skew; outliers alone create a fake “tail” |

## Types of histograms based on modes

A **mode** here means a **peak** (local high-frequency region), not only the single most common value.

```text
Modality
├── Unimodal — one main peak
├── Bimodal — two clear peaks
├── Multimodal — more than two peaks
└── Uniform (no clear mode) — roughly flat
```

| Type | Look | What it often means | Example |
| --- | --- | --- | --- |
| **Unimodal** | One hump | One main process or group | Adult heights in one gender/age band |
| **Bimodal** | Two humps | Mixture of two groups or regimes | Heights mixing men and women; weekday vs weekend traffic |
| **Multimodal** | Several humps | Several subgroups or settings | Multi-region latency; several product tiers mixed |
| **Uniform** | Roughly flat across the range | No preferred value; sometimes “all bins similar” | Fair die faces (discrete); random IDs in a range |

| | |
| --- | --- |
| **Use when** | Deciding whether to split data (cluster, stratify) before modeling |
| **Avoid over-reading when** | Extra “peaks” are binning artifacts; sample is small |

**ML link:** bimodal features often need separate models, a mixture approach, or an explicit segment feature — not one mean for everyone.

## Box plots

A **box plot** (box-and-whisker) summarizes a numeric variable with a **five-number summary** plus possible outliers — compact for comparing groups.

```text
        |-----[====|====]-----|   o
       min   Q1   Q2   Q3    max  outlier
                   (median)
              ←── IQR ──→
```

| Piece | Meaning |
| --- | --- |
| Box | From **Q1** to **Q3** (middle 50%) |
| Line inside box | **Median** (Q2) |
| Whiskers | Typically out to the farthest point within **1.5 × IQR** of the box (rule varies by tool) |
| Dots beyond whiskers | Candidate **outliers** |
| Box width / notches | Optional; some variants show sample size or CI for the median |

**Easy read:**

1. Median line → typical value.
2. Box height → **IQR** (robust spread).
3. Whisker length / asymmetry → skew.
4. Far dots → investigate (error vs real extreme).

| | |
| --- | --- |
| **Use when** | Comparing distributions across categories (region, model version); skewed data; outlier scan; pair with the median |
| **Avoid when** | You need full shape detail (histogram shows multimodality better); *n* is tiny; categories are the focus (bar chart) |

**Histogram vs box plot:** histogram → detailed shape; box plot → compact compare + outliers. Use both when the decision matters.

Detail on Q1/Q3/IQR: [`descriptive-statistics.md` → dispersion](./descriptive-statistics.md#measures-of-dispersion-spread).

## Scatter plots and their types

A **scatter plot** places each observation as a point with **X** = one numeric variable and **Y** = another. It shows relationship, clusters, and outliers that a single correlation number can hide.

| Part | Role |
| --- | --- |
| X-axis | Predictor / first variable |
| Y-axis | Response / second variable |
| Each point | One observation (xᵢ, yᵢ) |

### Types (by pattern)

| Type | Look | Correlation (rough) | Example |
| --- | --- | --- | --- |
| **Positive linear** | Cloud slopes up-right | Near +1 if tight | Study hours vs exam score |
| **Negative linear** | Cloud slopes down-right | Near −1 if tight | Car age vs resale price |
| **No association** | Formless blob | Near 0 | Shoe size vs coding skill |
| **Nonlinear** | Curve, U-shape, bend | Pearson near 0 possible even when related | Dose vs response; age vs income over full life |
| **Clusters / groups** | Separate blobs | Overall *r* misleading | Two customer segments mixed |
| **Outlier-driven** | One/few points pull the eye or the fit | *r* unstable | Data entry error at extreme x |
| **Homoscedastic vs fan** | Even vertical spread vs widening spread | Affects regression assumptions | Residuals growing with x |

```text
Scatter patterns
├── Linear
│   ├── Positive
│   └── Negative
├── None (random scatter)
├── Nonlinear (curve / U)
├── Clustered
└── Outlier-influenced
```

| | |
| --- | --- |
| **Use when** | Checking relationships before correlation/regression; spotting nonlinearity, clusters, heteroscedasticity, outliers |
| **Avoid when** | Both axes are unordered categories; huge *n* without transparency/hexbin (overplotting hides structure) |

**Tips:**

- Add a smooth or fit line only after you look at the raw cloud.
- Color/shape by a third variable (segment) if you suspect clusters.
- Correlation ≠ causation — see [Theory → Correlation vs causation](./theory.md#correlation-vs-causation).

**ML link:** scatter train features vs target (and residual plots) before trusting a linear model; curves and fans mean you need transforms, different models, or better features.

## Quick chooser

| Goal | Plot |
| --- | --- |
| Shape of one numeric variable | Histogram |
| Skew / modality of one variable | Histogram |
| Compare groups compactly + outliers | Box plot |
| Relationship between two numerics | Scatter plot |
| Category counts | Bar chart (see [frequency](./descriptive-statistics.md#frequency-relative-frequency-cumulative-frequency)) |

**EDA habit:** histogram (or box) per important feature → scatter vs target → then means, SDs, and models.