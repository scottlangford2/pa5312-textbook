---
layout: page
title: "Chapter 5"
permalink: /docs/chapter5/
---

# Describing and Presenting Data for Evaluation

## Epigraphs

> "The greatest value of a picture is when it forces us to notice what we never expected to see."
> — John W. Tukey, *Exploratory Data Analysis* (1977)

> "Above all else show the data."
> — Edward R. Tufte, *The Visual Display of Quantitative Information* (1983)

## Opening Case: The Texas Economic-Development Sales Tax (Case A)

Hundreds of Texas cities levy a local "Type A" or "Type B" economic-development sales tax — a fraction of a cent on every taxable sale, dedicated to attracting and growing local business. A legislative committee wants a simple thing: a one-page description of how much money this tax actually raises per resident across the state, and whether it is distributed evenly or concentrated in a few places. A first-year analyst on your team opens the Comptroller's 2024 allocation file, computes the **average** per-capita allocation across the roughly 1,141 reporting cities — about **\$395** — and reports that single number as "the typical Texas city."

It is not. When the analyst's supervisor builds a histogram, the distribution is sharply right-skewed: most cities sit far below \$395, a long tail of a few high-allocation cities pulls the average up, and the **median** is only about **\$276**. The "typical" \$395 city barely exists. A committee that budgeted around the mean would systematically overstate what an ordinary Texas city collects. The number was not wrong; it was the wrong summary for a skewed distribution.

This chapter is about describing data honestly *before* anyone draws a conclusion from it. Before any program effect can be estimated, the evaluator describes the data: what the typical value is, how spread out the values are, whether outliers are distorting the picture, and — crucially for evaluation — whether the groups being compared were equivalent at baseline. This is not preliminary throat-clearing. It is where most of the honest insight in an evaluation lives, and where most of the embarrassing mistakes get caught.

**Guiding Questions**

- What does a good first description of an evaluation dataset include, and why is it the first step rather than an afterthought?
- How do central tendency, spread, and outliers each tell us something different about a program's units — and why does a skewed money variable demand the median, not the mean?
- How do we check whether a treatment group and a comparison group were equivalent before the program began — and present that check so a decision-maker trusts it?

## Why This Chapter Matters

Decision-makers do not read your regression output; they read your table and your chart. The ability to summarize a messy panel into a few honest numbers and one clear figure is, in practice, the most-used skill in this course. It is also a safeguard: exploratory data analysis (EDA) is how you catch the impossible values, the skewed distributions, and the baseline imbalances that would otherwise quietly corrupt every later analysis (Tukey 1977). Skip it, and you risk being the analyst in the opening case — reporting a \$395 mean for a state whose typical city collects \$276.

## Exploratory Data Analysis as the First Step

EDA is the practice of looking — systematically and with suspicion — at your data before testing any hypothesis. The goal is to understand the shape of each variable and the relationships among them, and to surface anything that will break a later analysis. For an evaluation, three questions organize the first pass: What is typical? How much do units vary? And does anything look wrong or surprising?

> **Briefing:** EDA is not optional warm-up. It is the stage where you catch the data problems that would otherwise become false findings. Budget real time for it.

## Central Tendency

Three summaries of "typical" recur throughout evaluation, and choosing the wrong one misleads.

- The **mean** is the arithmetic average, $\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$. It uses every value but is pulled toward extremes.
- The **median** is the middle value when data are ordered. It ignores the size of extremes and so resists outliers.
- The **mode** is the most frequent value, useful mainly for nominal variables.

For right-skewed money variables — per-capita sales-tax allocations, taxable sales, median household income — the mean exceeds the median because a few large cities or wealthy counties pull the average up. In the Case A 2024 file the mean per-capita allocation is about **\$395** but the median is only about **\$276**; reporting only the mean would describe a city that does not exist. For skewed variables, report the median, or report both and let the gap reveal the skew.

> **Briefing:** When the mean and median diverge sharply, the distribution is skewed. Report the median for skewed money variables; report the mean when the distribution is roughly symmetric.

## Spread

A center without a spread is half a description. Two groups can share an identical mean turnout while one is tightly clustered and the other ranges from near-zero to near-universal — and those two worlds call for very different programs.

The **range** (max minus min) is simple but driven entirely by the two most extreme cases. The **interquartile range** (IQR), the distance from the 25th to the 75th percentile, describes the middle half and resists outliers. The **standard deviation** measures typical distance from the mean. The sample standard deviation is

$$s = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}\left(x_i - \bar{x}\right)^2}$$

and its square, the variance $s^2$, is the quantity that underlies every test in Chapter 6. The $n-1$ in the denominator — Bessel's correction — is why Excel's `STDEV.S` (sample) differs from `STDEV.P` (population); for evaluation data, which is almost always a sample or a stand-in for one, use `STDEV.S`.

## Distributions and Outliers

A summary statistic hides the shape of a distribution; a histogram reveals it. Bimodality — two humps — often signals that you are looking at two distinct populations mashed together, exactly the metro/non-metro split that recurs in the county panel. EDA exists to catch this before you average across it.

Outliers deserve judgment, not reflex. A turnout of 140 percent is an error and should be corrected or removed. But a genuinely tiny county with volatile turnout is real data, and deleting it because it is inconvenient is a form of fabrication. A common screening rule flags a value as an outlier if it lies more than $1.5 \times \text{IQR}$ beyond the quartiles:

$$x < Q_1 - 1.5\,(\text{IQR}) \quad \text{or} \quad x > Q_3 + 1.5\,(\text{IQR})$$

Flagging is the start of an investigation, never an automatic deletion.

> **Briefing:** Outliers are flags, not verdicts. Investigate whether each is an error or a real extreme case before deciding what to do, and disclose the decision.

## Baseline Comparisons and Equivalence

Here is where description becomes evaluation. When you compare a treatment group to a comparison group, the entire credibility of a later difference depends on whether the two groups were similar *before* the program. A **baseline equivalence table** lays the pre-program characteristics of both groups side by side so a reader can judge for themselves.

The logic: if vote-center and non-vote-center counties had nearly identical pre-program income, education, population, and rurality, then a post-program turnout difference is plausibly the program. If they differed sharply at baseline, then a post-program difference might be nothing more than that pre-existing gap persisting. Baseline equivalence does not by itself license a causal claim, but its *absence* is often enough to sink one (Rossi, Lipsey & Henry 2019). The cleanest version of this logic is randomization: in NSW (Case C) and MTO (Case D), a lottery assigned the program, so the groups were equivalent at baseline by construction — which is exactly why their simple post-program differences can be read as effects.

> **Briefing:** Always show baseline equivalence before showing program effects. A reader who sees imbalanced groups will — rightly — discount everything that follows.

When groups are *not* randomized, the equivalence check often reveals trouble. Compare metro and non-metro counties in the Case B 2020 panel. The two groups have nearly identical turnout — metro counties average **0.554** (n = 86) and non-metro counties average **0.580** (n = 168) — but they differ on the very characteristics that drive turnout. A regression of 2020 turnout on county wealth and education makes the point: across all 254 counties,

$$\text{turnout} \approx 0.425 + 0.0017 \times (\text{median HH income in \$1{,}000s}) + 0.0022 \times (\text{percent bachelor's})$$

with an $R^2$ of only about **0.08**. Income and education each nudge turnout upward, but together they explain just 8 percent of the variation across counties — a useful reminder that turnout is driven by much more than the two demographics any single program can target, and that comparing raw metro and non-metro means without accounting for those demographics confounds the urban-rural divide with everything else.

### Worked Example: Describing the 2024 Per-Capita Sales-Tax Distribution in Excel

Return to Case A. You have the 2024 file open with one row per city and a column `alloc_per_capita` (the economic-development sales-tax allocation per resident) in, say, `D2:D1142` for the roughly 1,141 reporting cities. The committee wants an honest one-page description.

**1. Center.** Compute `=AVERAGE(D2:D1142)` and `=MEDIAN(D2:D1142)`. The mean returns about **\$395** and the median about **\$276**. The mean sitting well above the median is the signature of a right-skewed distribution.

**2. Spread.** Compute `=STDEV.S(D2:D1142)` for the sample standard deviation — about **\$596** — and `=MIN`/`=MAX` for the range. A standard deviation (\$596) *larger than the mean* (\$395) is itself a red flag for strong skew and a long upper tail; for a roughly symmetric variable the SD is usually a fraction of the mean.

**3. Histogram.** Build a histogram with **Data → Data Analysis → Histogram** (or `FREQUENCY` with bins of, say, \$100 width). The shape is unmistakable: a tall bar of low-allocation cities near zero, then a long thin tail stretching far to the right — a handful of cities collecting many times the median.

**4. A description table.** Report center, spread, and shape together so the skew is undeniable.

| Statistic | Excel function | Value (2024, per capita) |
|---|---|---|
| Cities (n) | `COUNT` | ~1,141 |
| Mean | `AVERAGE` | \$395 |
| Median | `MEDIAN` | \$276 |
| Standard deviation | `STDEV.S` | \$596 |
| Mean − median | subtraction | +\$119 (right skew) |

The mean exceeds the median by \$119, and the standard deviation exceeds the mean — both diagnostic of a strongly right-skewed money variable with a long tail of high-allocation outlier cities. The honest one-line summary for the committee is: *"The typical Texas city collects about \$276 per resident from its economic-development sales tax; the average is pulled up to \$395 by a small number of high-collecting cities."*

> **Returning to the Case:** The opening-case analyst was not wrong that the mean is \$395 — that figure is real. The mistake was reporting it *alone*, as if it described a typical city, when the median of \$276 and the \$596 standard deviation reveal a distribution where most cities fall well below the average. Had the analyst built the histogram first, the right skew would have been visible immediately, and the committee would have received the median (with the mean shown alongside) rather than a single number that overstates what an ordinary city collects. Describe the shape before you summarize the center.

## Presenting Data to Decision-Makers

A table for an analyst and a table for a committee chair are different documents. For decision-makers: round to meaningful precision (a per-capita allocation to the nearest dollar, not the cent), label every column with units, state the $n$, and give the table a sentence-long title that states the takeaway. For charts, prefer a clean column or line chart over a 3-D pie; let the data dominate the ink. In Excel, build these with **Insert → PivotChart** off your PivotTable so the figure updates when the data do, and use **Number Format** to control rounding rather than retyping values.

> **Briefing:** Round to the precision a decision-maker can act on, label everything, and title the table with its conclusion. Excess decimal places signal false precision and erode trust.

## Common Pitfalls

- **Reporting the mean of a skewed variable alone.** The opening-case error: \$395 reported without the \$276 median. Money variables are right-skewed; the median, or both, belong in the table.
- **Skipping EDA and modeling first.** A coefficient before a histogram hides the shape the histogram would have revealed.
- **Confusing population and sample standard deviation.** Use `STDEV.S` for evaluation data, not `STDEV.P`.
- **Deleting outliers for convenience.** Flag and investigate; deletion without justification is data manipulation.
- **Comparing groups without a baseline equivalence table.** A post-program difference between non-equivalent groups is uninterpretable.
- **False precision in presentation.** Six decimal places on a revenue figure tells a decision-maker you do not understand your own data.

## Practice and Application

1. **Center and spread.** For the Case A 2024 file, compute the mean (`AVERAGE` ≈ \$395), median (`MEDIAN` ≈ \$276), standard deviation (`STDEV.S` ≈ \$596), and IQR of per-capita allocation. Explain in two sentences what the gap between mean and median, and the SD exceeding the mean, tell you about the distribution's shape.

2. **Histogram.** Build a histogram of the Case A 2024 per-capita allocation using the ToolPak's Histogram tool or `FREQUENCY` with \$100 bins. Describe the shape, locate the median (\$276) relative to the tall low-end bars, and explain why the long right tail pulls the mean above the median.

3. **Outlier screen.** Apply the $1.5 \times \text{IQR}$ rule to the Case A per-capita allocation using `QUARTILE.INC`. List the flagged high-allocation cities and, for two of them, argue whether each is a data error or a genuine extreme (e.g., a small city with a large retail base).

4. **County turnout descriptives.** Using the Case B 2020 panel, compute mean and standard deviation of turnout separately for metro and non-metro counties. Confirm you recover roughly 0.554 (metro, n = 86) and 0.580 (non-metro, n = 168), and write one paragraph on what the closeness of the two means suggests before any formal test.

5. **Decision-maker table.** Take any table you built above and rewrite it for a legislative committee: rounded, labeled, titled with its conclusion, and accompanied by one clean PivotChart. Explain each presentation choice in a sentence.

## Transition to Chapter 6

Description tells you that two groups *look* different — or, as with the metro (0.554) and non-metro (0.580) turnout means just computed, barely different at all. It does not tell you whether that gap is larger than what sampling noise alone would produce, or whether it is large enough to matter for policy. Chapter 6 takes up the formal comparison of groups — one-sample, independent-samples, and paired t-tests, and one-way ANOVA for three or more groups — and puts the metro/non-metro turnout comparison through a Welch t-test to see whether that 0.026 gap survives, all run in Excel with `T.TEST` and the Data Analysis ToolPak.
