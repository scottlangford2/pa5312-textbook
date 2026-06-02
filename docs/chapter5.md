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

## Opening Case: A Broadband Grant in the Texas Hill Country

The Texas Comptroller's office has distributed broadband infrastructure grants to a set of rural counties, and a legislative committee wants to know whether the program helped. A first-year analyst on your team, eager to impress, opens the county panel, runs a regression of an outcome on a grant indicator, and reports a coefficient before lunch. The number is statistically significant. The committee staffer is unimpressed, and asks a question the analyst cannot answer: "Did the grant counties and the comparison counties look anything alike *before* the money went out?"

They did not. The grant counties were, on average, poorer, less populated, and far more rural than the counties they were being compared to. The "effect" the analyst found was largely the pre-existing gap between two very different sets of places, not anything the grant did. No regression can rescue an analyst who never looked at the data before modeling it.

This chapter is about the step the analyst skipped. Before any program effect can be estimated, the evaluator describes the data: what the typical value is, how spread out the values are, whether outliers are distorting the picture, and — crucially for evaluation — whether the groups being compared were equivalent at baseline. This is not preliminary throat-clearing. It is where most of the honest insight in an evaluation lives, and where most of the embarrassing mistakes get caught.

**Guiding Questions**

- What does a good first description of an evaluation dataset include, and why is it the first step rather than an afterthought?
- How do central tendency, spread, and outliers each tell us something different about a program's units?
- How do we check whether a treatment group and a comparison group were equivalent before the program began — and present that check so a decision-maker trusts it?

## Why This Chapter Matters

Decision-makers do not read your regression output; they read your table and your chart. The ability to summarize a messy panel into a few honest numbers and one clear figure is, in practice, the most-used skill in this course. It is also a safeguard: exploratory data analysis (EDA) is how you catch the impossible values, the bimodal distributions, and the baseline imbalances that would otherwise quietly corrupt every later analysis (Tukey 1977). Skip it, and you risk being the analyst in the opening case.

## Exploratory Data Analysis as the First Step

EDA is the practice of looking — systematically and with suspicion — at your data before testing any hypothesis. The goal is to understand the shape of each variable and the relationships among them, and to surface anything that will break a later analysis. For an evaluation, three questions organize the first pass: What is typical? How much do units vary? And does anything look wrong or surprising?

> **Briefing:** EDA is not optional warm-up. It is the stage where you catch the data problems that would otherwise become false findings. Budget real time for it.

## Central Tendency

Three summaries of "typical" recur throughout evaluation, and choosing the wrong one misleads.

- The **mean** is the arithmetic average, $\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$. It uses every value but is pulled toward extremes.
- The **median** is the middle value when data are ordered. It ignores the size of extremes and so resists outliers.
- The **mode** is the most frequent value, useful mainly for nominal variables.

For right-skewed money variables — sales-tax revenue, taxable sales, median household income — the mean exceeds the median because a few large cities or wealthy counties pull the average up. Reporting only the mean of city sales-tax revenue would describe a city that does not exist. For skewed variables, report the median, or report both and let the gap reveal the skew.

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

The logic: if grant and non-grant counties had nearly identical pre-program income, population, turnout, and rurality, then a post-program difference is plausibly the program. If they differed sharply at baseline — as in the opening case — then a post-program difference might be nothing more than that pre-existing gap persisting. Baseline equivalence does not by itself license a causal claim, but its *absence* is often enough to sink one (Rossi, Lipsey & Henry 2019).

> **Briefing:** Always show baseline equivalence before showing program effects. A reader who sees imbalanced groups will — rightly — discount everything that follows.

### Worked Example: A Baseline Equivalence Table in Excel

Using the county panel, suppose we want to compare metro and non-metro counties on their pre-period (year 2000) characteristics — a stand-in for checking whether two groups defined by a policy were comparable at baseline. We will build the table with PivotTables.

**1. Filter to the baseline year.** Use a PivotTable or a filtered view restricted to `year = 2000` so the comparison is genuinely pre-period.

**2. Build the PivotTable.** Drag `metro_status` to Rows. Drag `turnout`, `median_hh_income`, and `pct_bachelors` to Values, each set to **Average** (Value Field Settings → Summarize Values By → Average). Add `population` set to Average and a `Count` of counties so the reader sees group sizes.

**3. Add spread.** A PivotTable will not directly give a standard deviation per group in older Excel, so compute it alongside with `AVERAGEIFS` and an array form, or use `=STDEV.S(IF(metro_range="Metro", income_range))` entered as needed. Report mean and standard deviation together.

**4. Standardize the gap.** To judge whether a difference is large, compute a standardized mean difference: the difference in group means divided by the pooled standard deviation. A common rule of thumb treats values below about 0.1 as good balance.

$$d = \frac{\bar{x}_{\text{Metro}} - \bar{x}_{\text{Non-metro}}}{s_{\text{pooled}}}$$

| Baseline characteristic (2000) | Metro (mean) | Non-metro (mean) | Std. mean diff. |
|---|---|---|---|
| Turnout (%) | 56.4 | 58.1 | 0.18 |
| Median household income ($) | 44,200 | 33,500 | 0.71 |
| % bachelor's degree | 24.1 | 13.8 | 0.86 |
| Population (count) | 312,000 | 18,400 | 1.40 |

*(Illustrative layout only — fill with values your own PivotTable returns; do not report these as findings.)*

The standardized differences for income, education, and population are far above 0.1. Metro and non-metro counties are profoundly different at baseline, so a naive comparison of their outcomes would confound the program with the urban-rural divide.

> **Returning to the Case:** The Hill Country broadband evaluation founders on exactly this table. Had the analyst built a baseline equivalence comparison first, the large standardized differences in income, population, and rurality would have been visible immediately — and the team would have known that a simple grant-versus-non-grant comparison cannot be trusted. The fix is not a fancier model run on incomparable groups; it is to find or construct a comparison group that resembles the grant counties at baseline, and to *show* that resemblance in a table before claiming any effect.

## Presenting Data to Decision-Makers

A table for an analyst and a table for a committee chair are different documents. For decision-makers: round to meaningful precision (sales-tax revenue to the nearest thousand dollars, not the cent), label every column with units, state the $n$, and give the table a sentence-long title that states the takeaway. For charts, prefer a clean column or line chart over a 3-D pie; let the data dominate the ink. In Excel, build these with **Insert → PivotChart** off your PivotTable so the figure updates when the data do, and use **Number Format** to control rounding rather than retyping values.

> **Briefing:** Round to the precision a decision-maker can act on, label everything, and title the table with its conclusion. Excess decimal places signal false precision and erode trust.

## Common Pitfalls

- **Skipping EDA and modeling first.** The opening-case error: a coefficient before a histogram.
- **Reporting the mean of a skewed variable alone.** Money variables are right-skewed; the median or both belong in the table.
- **Confusing population and sample standard deviation.** Use `STDEV.S` for evaluation data, not `STDEV.P`.
- **Deleting outliers for convenience.** Flag and investigate; deletion without justification is data manipulation.
- **Comparing groups without a baseline equivalence table.** A post-program difference between non-equivalent groups is uninterpretable.
- **False precision in presentation.** Six decimal places on a revenue figure tells a decision-maker you do not understand your own data.

## Practice and Application

1. **Center and spread.** For the county panel in 2020, compute the mean, median, standard deviation (`STDEV.S`), and IQR of turnout. Explain in two sentences what the gap between mean and median tells you about the distribution's shape.

2. **Histogram.** Build a histogram of city sales-tax revenue (one year) using the ToolPak's Histogram tool or `FREQUENCY`. Describe the shape and identify whether you see signs of two subpopulations.

3. **Outlier screen.** Apply the $1.5 \times \text{IQR}$ rule to median household income across counties in one year using `QUARTILE.INC`. List the flagged counties and, for two of them, argue whether each is an error or a genuine extreme.

4. **Baseline equivalence table.** Using the county panel, build a PivotTable comparing metro and non-metro counties at baseline (year 2000) on at least four characteristics, with means, standard deviations, and standardized mean differences. Write one paragraph on whether the groups are comparable.

5. **Decision-maker table.** Take any table you built above and rewrite it for a legislative committee: rounded, labeled, titled with its conclusion, and accompanied by one clean PivotChart. Explain each presentation choice in a sentence.

## Transition to Chapter 6

Description tells you that two groups *look* different; it does not tell you whether that difference is larger than what sampling noise alone would produce, or whether it is large enough to matter for policy. Chapter 6 takes up the formal comparison of groups — one-sample, independent-samples, and paired t-tests, and one-way ANOVA for three or more groups — along with effect size and the crucial distinction between statistical and practical significance, all run in Excel with `T.TEST` and the Data Analysis ToolPak.
