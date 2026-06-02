---
layout: page
title: "Chapter 6"
permalink: /docs/chapter6/
---

# Comparing Groups: t-Tests and ANOVA

## Epigraphs

> "The null hypothesis is never proved or established, but is possibly disproved, in the course of experimentation."
> — Ronald A. Fisher, *The Design of Experiments* (1935)

> "Statistical significance is not the same as practical importance."
> — a standard caution in applied statistics; treat as a maxim, not a citation

## Opening Case: Did the Outreach Campaign Move Turnout?

A coalition of county clerks in a set of Texas counties ran a nonpartisan voter-outreach campaign — mailers, text reminders, extended early-voting hours — and wants to know whether it raised turnout. They have two natural comparisons in mind. First, did the campaign counties have higher turnout than the counties that ran no campaign? Second, within the campaign counties, did turnout rise from the prior election to this one? They have read enough to know that "it went up" is not an answer; they want to know whether the difference is bigger than chance, and whether it is big enough to be worth the cost.

Your team also suspects the picture differs by county type. Maybe the campaign worked in fast-growing suburban counties but not in tiny rural ones or large urban ones. That is a three-group question, which a t-test cannot handle and which calls for analysis of variance.

The committee's two demands map onto the two halves of this chapter. *Bigger than chance* is a question of statistical significance, answered with t-tests and ANOVA. *Big enough to matter* is a question of practical significance, answered with effect size and judgment. A competent evaluator never reports one without the other.

**Guiding Questions**

- When do we use a one-sample, an independent-samples, or a paired t-test — and what does each one actually compare?
- How does one-way ANOVA extend group comparison to three or more groups, and why not just run many t-tests?
- What is an effect size, and why can a result be statistically significant yet practically trivial?

## Why This Chapter Matters

Comparing a group that received a program to a group that did not is the most basic evaluation design there is, and the t-test is its workhorse. Almost every evaluation you read will, somewhere, compare two means and ask whether the gap is real. But the test only answers half the question. A large sample can make a meaningless difference "significant," and a small sample can hide a real one. Learning to pair every test with an effect size — and to say plainly whether a difference matters for policy — is what separates an evaluation from a p-value hunt.

## The Logic of Hypothesis Testing

Every test in this chapter shares one logic. We state a **null hypothesis** ($H_0$) of no difference, assume it is true, and ask how surprising our observed data would be under that assumption. The **p-value** is the probability of seeing a difference at least as large as ours if the null were true. A small p-value means our data are hard to reconcile with "no difference," so we reject the null. By convention many fields use $\alpha = 0.05$ as the threshold, but the threshold is a convention, not a law of nature.

> **Briefing:** A p-value is the probability of the data given no effect — not the probability that there is no effect. It never tells you the size or importance of a difference, only how compatible the data are with chance.

## The One-Sample t-Test

The one-sample t-test compares a single group's mean to a fixed benchmark — a statutory target, a statewide average, a prior-year figure treated as known. The statistic is

$$t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}$$

where $\bar{x}$ is the sample mean, $\mu_0$ the benchmark, $s$ the sample standard deviation, and $n$ the sample size. The denominator $s/\sqrt{n}$ is the standard error of the mean. Larger samples shrink the standard error, so the same gap becomes more "significant" as $n$ grows — a fact worth holding onto when we reach effect size.

For example, you might test whether the average turnout among campaign counties differs from a statewide benchmark of 60 percent. Excel has no single one-sample function, so compute $t$ directly from `AVERAGE`, `STDEV.S`, and `COUNT`, then get the p-value with `T.DIST.2T(ABS(t), n-1)`.

## The Independent-Samples t-Test

This is the central evaluation test: two separate groups, treatment and comparison, with no natural pairing between their members. It answers the committee's first question — did campaign counties have higher turnout than non-campaign counties? The statistic compares the two group means relative to the variability within the groups:

$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\dfrac{s_1^2}{n_1} + \dfrac{s_2^2}{n_2}}}$$

A decision you must make: do the two groups have equal variances? If you are unsure — and you usually are — use the **Welch** (unequal-variance) version, which is more robust and is the safer default (Agresti 2018).

> **Briefing:** When in doubt about equal variances, use the unequal-variance (Welch) t-test. It costs little when variances are equal and protects you when they are not.

Recall from Chapter 5 that this test is only as credible as the baseline equivalence behind it. If the campaign and non-campaign counties differed sharply before the campaign, a significant t-test tells you the groups differ — not that the campaign caused the difference.

## The Paired t-Test

When each unit is measured twice — before and after — the two measurements are *not* independent, and treating them as if they were throws away the most useful information you have. The paired t-test works on the within-unit differences $d_i = x_{i,\text{post}} - x_{i,\text{pre}}$, testing whether their mean differs from zero:

$$t = \frac{\bar{d}}{s_d / \sqrt{n}}$$

This answers the committee's second question — within campaign counties, did turnout rise from the prior election to this one? Pairing controls for everything stable about each county (its size, its political culture, its baseline civic habits), because each county serves as its own comparison. That is its strength and its limit: a paired pre/post comparison with no untreated comparison group cannot rule out that *something else* changed statewide between the two elections.

> **Briefing:** Pair your data whenever the same units are measured twice. Using an independent-samples test on paired data is a common and costly error — it discards the pairing and usually inflates the standard error.

## One-Way ANOVA for Three or More Groups

The team's suspicion — that the campaign worked differently in rural, suburban, and urban counties — is a three-group question. You might be tempted to run three separate t-tests (rural vs. suburban, suburban vs. urban, rural vs. urban), but each test carries its own chance of a false positive, and running several inflates the overall error rate. **One-way ANOVA** tests, in a single procedure, the null hypothesis that all group means are equal:

$$H_0: \mu_1 = \mu_2 = \mu_3$$

ANOVA works by comparing variation *between* groups to variation *within* groups, summarized in the F-statistic:

$$F = \frac{\text{MS}_{\text{between}}}{\text{MS}_{\text{within}}}$$

A large $F$ means the groups differ more from each other than members differ within their own group — evidence against the null. A significant ANOVA tells you that *some* groups differ, but not *which*; you follow up with post-hoc comparisons to locate the differences, adjusting for the multiple looks.

> **Briefing:** Do not run many pairwise t-tests across several groups. Use ANOVA to ask the overall question first, then follow up — running k(k−1)/2 separate tests inflates your false-positive rate.

## Statistical vs. Practical Significance, and Effect Size

This is the heart of the chapter. A p-value confounds the *size* of a difference with the *size* of the sample. With 254 counties, a turnout gap of half a percentage point — far too small to justify a statewide campaign budget — can be highly statistically significant. With a dozen counties, a politically decisive gap might miss the 0.05 threshold. The p-value alone cannot tell a decision-maker whether to fund the program.

**Effect size** answers the "how big" question on a scale that does not depend on $n$. For comparing two means, **Cohen's d** expresses the difference in standard-deviation units:

$$d = \frac{\bar{x}_1 - \bar{x}_2}{s_{\text{pooled}}}$$

Conventional, rough benchmarks are $d \approx 0.2$ (small), $0.5$ (medium), and $0.8$ (large) — but these are guidelines, and what counts as "large enough to matter" is ultimately a policy judgment about cost, equity, and stakes, not a statistical one.

> **Briefing:** Always report an effect size alongside a p-value. "Significant" answers whether a difference is bigger than chance; effect size and policy judgment answer whether it is big enough to act on. Decision-makers need both.

### Worked Example: Metro vs. Non-Metro Turnout in Excel

Using the county panel, we test whether turnout differs between metro and non-metro counties in a single election year — a clean two-group comparison.

**1. Arrange the data.** Put metro counties' turnout in one column and non-metro counties' turnout in another (or filter and copy into two ranges).

**2. Run the test two ways.** For a quick p-value, use `=T.TEST(metro_range, nonmetro_range, 2, 3)` — the `2` requests a two-tailed test and the `3` requests the unequal-variance (Welch) version. For a full report, open **Data → Data Analysis → t-Test: Two-Sample Assuming Unequal Variances**, which returns both group means, both variances, the t-statistic, degrees of freedom, and the p-value in one table.

**3. Compute the effect size.** Get each mean with `AVERAGE`, each standard deviation with `STDEV.S`, and the pooled standard deviation, then divide the mean difference by it to obtain Cohen's d.

| Quantity | Excel source | Illustrative value |
|---|---|---|
| Mean turnout, metro | `AVERAGE` | 61.2% |
| Mean turnout, non-metro | `AVERAGE` | 58.7% |
| Difference | subtraction | 2.5 pts |
| t-statistic | ToolPak / formula | 2.10 |
| p-value (two-tailed) | `T.TEST(...,2,3)` | 0.037 |
| Cohen's d | difference / pooled SD | 0.28 |

*(Illustrative layout only — report the values your own data return.)*

Read together, this output says the metro/non-metro turnout gap is statistically significant (p < 0.05) but small in magnitude (d ≈ 0.28). Whether a 2.5-point gap warrants a targeted intervention is a policy question the statistics inform but do not settle.

> **Returning to the Case:** The county clerks now have a defensible answer structure. Their first question is an independent-samples (Welch) t-test of campaign versus non-campaign turnout — paired with Cohen's d and a reminder, from Chapter 5, that it is only trustworthy if the two sets of counties were equivalent at baseline. Their second question is a paired t-test of pre- versus post-campaign turnout within the campaign counties. Their suspicion about county type is a one-way ANOVA across rural, suburban, and urban groups, followed by post-hoc comparisons. In every case the evaluation reports not just "significant or not," but how large the difference is and whether it justifies the program's cost.

## Common Pitfalls

- **Reading the p-value as importance.** Significance is about chance, not magnitude. A tiny, useless difference can be "significant" in a large sample.
- **Using an independent-samples test on paired data.** Pre/post on the same units is paired; treating it as independent discards the pairing.
- **Assuming equal variances by default.** Prefer the Welch test unless you have a reason not to.
- **Running many t-tests across several groups.** Use ANOVA first; pairwise tests inflate the false-positive rate.
- **Reporting a test without an effect size.** A p-value with no Cohen's d leaves the decision-maker unable to judge whether to act.
- **Forgetting baseline equivalence.** A significant between-group difference is not a program effect if the groups were not comparable to begin with.

## Practice and Application

1. **One-sample test.** Test whether mean turnout among non-metro counties in 2020 differs from a benchmark of 60 percent. Compute $t$ from `AVERAGE`, `STDEV.S`, and `COUNT`, then get the p-value with `T.DIST.2T`. Interpret in one sentence.

2. **Independent-samples test.** Using the county panel, run a Welch t-test comparing median household income in metro versus non-metro counties for one year, with both `T.TEST(...,2,3)` and the ToolPak. Confirm the two approaches agree on the p-value.

3. **Effect size.** For the comparison in Exercise 2, compute Cohen's d. Classify it against the small/medium/large benchmarks and write two sentences on whether the difference is practically meaningful.

4. **Paired test.** Pick a set of counties and run a paired t-test of turnout in two consecutive presidential elections using the ToolPak's paired option. Explain why pairing is appropriate here and what it controls for.

5. **One-way ANOVA.** Classify counties into three groups (e.g., by population tercile) and run **Data Analysis → ANOVA: Single Factor** on turnout. Report the F-statistic and p-value, state what a significant result does and does not tell you, and describe what follow-up you would run.

## Transition to Chapter 7

t-Tests and ANOVA compare group means but cannot, on their own, account for the baseline differences that Chapter 5 warned us about. When metro counties differ from non-metro counties on income, education, and population all at once, a simple mean comparison confounds the program with everything else that distinguishes the groups. Chapter 7 introduces regression, which lets us compare groups *while holding other characteristics constant* — the first tool in this course capable of isolating one factor's contribution from the tangle of others.
