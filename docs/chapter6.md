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

## Opening Case: Do Metro Counties Vote at Different Rates? (Case B)

As Texas counties weigh adopting countywide vote centers, a common starting question is whether turnout even differs between the state's metropolitan and non-metropolitan counties to begin with. If urban and rural counties already turn out at sharply different rates, an evaluation of vote centers must account for that gap; if they turn out at similar rates, the comparison is simpler. So your team begins with the most basic group comparison there is: in the 2020 election, did metro counties have different turnout than non-metro counties?

The descriptive numbers from Chapter 5 are close. Metro counties (n = 86) averaged turnout of **0.554**; non-metro counties (n = 168) averaged **0.580** — non-metro counties were, if anything, *slightly higher*, which surprises most people who assume rural turnout lags. The whole question of this chapter is whether that small 0.026 gap is real or just sampling noise, and, if real, whether it is large enough to matter for policy.

The team also suspects the picture might differ if counties were split three ways — say small, mid-size, and large — rather than two. That is a three-group question, which a t-test cannot handle and which calls for analysis of variance.

These demands map onto the two halves of this chapter. *Bigger than chance* is a question of statistical significance, answered with t-tests and ANOVA. *Big enough to matter* is a question of practical significance, answered with effect size and judgment. A competent evaluator never reports one without the other.

**Guiding Questions**

- When do we use a one-sample, an independent-samples, or a paired t-test — and what does each one actually compare?
- How does one-way ANOVA extend group comparison to three or more groups, and why not just run many t-tests?
- What is an effect size, and why can a result be statistically significant yet practically trivial — or, as in this case, fail to reach significance at all?

## Why This Chapter Matters

Comparing a group that received a program to a group that did not is the most basic evaluation design there is, and the t-test is its workhorse. Almost every evaluation you read will, somewhere, compare two means and ask whether the gap is real. But the test only answers half the question. A large sample can make a meaningless difference "significant," and a small sample can hide a real one. Learning to pair every test with an effect size — and to say plainly whether a difference matters for policy — is what separates an evaluation from a p-value hunt.

## The Logic of Hypothesis Testing

Every test in this chapter shares one logic. We state a **null hypothesis** ($H_0$) of no difference, assume it is true, and ask how surprising our observed data would be under that assumption. The **p-value** is the probability of seeing a difference at least as large as ours if the null were true. A small p-value means our data are hard to reconcile with "no difference," so we reject the null. By convention many fields use $\alpha = 0.05$ as the threshold, but the threshold is a convention, not a law of nature.

> **Briefing:** A p-value is the probability of the data given no effect — not the probability that there is no effect. It never tells you the size or importance of a difference, only how compatible the data are with chance.

## The One-Sample t-Test

The one-sample t-test compares a single group's mean to a fixed benchmark — a statutory target, a statewide average, a prior-year figure treated as known. The statistic is

$$t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}$$

where $\bar{x}$ is the sample mean, $\mu_0$ the benchmark, $s$ the sample standard deviation, and $n$ the sample size. The denominator $s/\sqrt{n}$ is the standard error of the mean. Larger samples shrink the standard error, so the same gap becomes more "significant" as $n$ grows — a fact worth holding onto when we reach effect size.

For example, in Case B you might test whether average county turnout in 2020 — about 0.57 across all 254 counties — differs from a statewide benchmark of 0.60. Excel has no single one-sample function, so compute $t$ directly from `AVERAGE`, `STDEV.S`, and `COUNT`, then get the p-value with `T.DIST.2T(ABS(t), n-1)`.

## The Independent-Samples t-Test

This is the central evaluation test: two separate groups, treatment and comparison, with no natural pairing between their members. It answers the opening question — did metro counties have different turnout than non-metro counties? The statistic compares the two group means relative to the variability within the groups:

$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\dfrac{s_1^2}{n_1} + \dfrac{s_2^2}{n_2}}}$$

A decision you must make: do the two groups have equal variances? If you are unsure — and you usually are — use the **Welch** (unequal-variance) version, which is more robust and is the safer default (Agresti 2018).

> **Briefing:** When in doubt about equal variances, use the unequal-variance (Welch) t-test. It costs little when variances are equal and protects you when they are not.

Recall from Chapter 5 that this test is only as credible as the baseline equivalence behind it. Metro and non-metro counties differ on income, education, and population all at once, so even a significant turnout difference would tell you the groups differ — not why. The cleanest contrast comes from randomized programs: in NSW (Case C) the treatment group earned \$6,349 versus \$4,555 for randomized controls, an independent-samples difference of +\$1,794 that *can* be read causally precisely because the lottery made the groups equivalent at baseline (LaLonde 1986; Dehejia & Wahba 1999).

## The Paired t-Test

When each unit is measured twice — before and after — the two measurements are *not* independent, and treating them as if they were throws away the most useful information you have. The paired t-test works on the within-unit differences $d_i = x_{i,\text{post}} - x_{i,\text{pre}}$, testing whether their mean differs from zero:

$$t = \frac{\bar{d}}{s_d / \sqrt{n}}$$

In Case B this is the natural follow-up — within the counties that adopted vote centers, did turnout rise from the election before adoption to the election after? Pairing controls for everything stable about each county (its size, its political culture, its baseline civic habits), because each county serves as its own comparison. That is its strength and its limit: a paired pre/post comparison with no untreated comparison group cannot rule out that *something else* changed statewide between the two elections.

> **Briefing:** Pair your data whenever the same units are measured twice. Using an independent-samples test on paired data is a common and costly error — it discards the pairing and usually inflates the standard error.

## One-Way ANOVA for Three or More Groups

The team's suspicion — that turnout differs across small, mid-size, and large counties — is a three-group question. You might be tempted to run three separate t-tests (small vs. mid, mid vs. large, small vs. large), but each test carries its own chance of a false positive, and running several inflates the overall error rate. **One-way ANOVA** tests, in a single procedure, the null hypothesis that all group means are equal:

$$H_0: \mu_1 = \mu_2 = \mu_3$$

ANOVA works by comparing variation *between* groups to variation *within* groups, summarized in the F-statistic:

$$F = \frac{\text{MS}_{\text{between}}}{\text{MS}_{\text{within}}}$$

A large $F$ means the groups differ more from each other than members differ within their own group — evidence against the null. A significant ANOVA tells you that *some* groups differ, but not *which*; you follow up with post-hoc comparisons to locate the differences, adjusting for the multiple looks.

> **Briefing:** Do not run many pairwise t-tests across several groups. Use ANOVA to ask the overall question first, then follow up — running k(k−1)/2 separate tests inflates your false-positive rate.

## Statistical vs. Practical Significance, and Effect Size

This is the heart of the chapter. A p-value confounds the *size* of a difference with the *size* of the sample. The MTO housing experiment (Case D) makes the magnitude side vivid: children who moved young earned about **\$3,477 more** as adults than the control group's mean of **\$11,270** — a roughly **31 percent** gain that is large enough to matter for policy on its own terms (Chetty, Hendren & Katz 2016). Contrast that with the metro/non-metro turnout gap, where, as we will see, a 0.026 difference across 254 counties does not even reach significance. The p-value alone cannot tell a decision-maker whether to act; effect size and policy judgment must accompany it.

**Effect size** answers the "how big" question on a scale that does not depend on $n$. For comparing two means, **Cohen's d** expresses the difference in standard-deviation units:

$$d = \frac{\bar{x}_1 - \bar{x}_2}{s_{\text{pooled}}}$$

Conventional, rough benchmarks are $d \approx 0.2$ (small), $0.5$ (medium), and $0.8$ (large) — but these are guidelines, and what counts as "large enough to matter" is ultimately a policy judgment about cost, equity, and stakes, not a statistical one.

> **Briefing:** Always report an effect size alongside a p-value. "Significant" answers whether a difference is bigger than chance; effect size and policy judgment answer whether it is big enough to act on. Decision-makers need both.

### Worked Example: Metro vs. Non-Metro 2020 Turnout in Excel

Using the Case B county panel, we test whether 2020 turnout differs between metro and non-metro counties — the clean two-group comparison from the opening case.

**1. Arrange the data.** Put the 86 metro counties' turnout in one column and the 168 non-metro counties' turnout in another (filter on `metro_status` and copy into two ranges).

**2. Run the test two ways.** For a quick p-value, use `=T.TEST(metro_range, nonmetro_range, 2, 3)` — the `2` requests a two-tailed test and the `3` requests the unequal-variance (Welch) version. For a full report, open **Data → Data Analysis → t-Test: Two-Sample Assuming Unequal Variances**, which returns both group means, both variances, the t-statistic, degrees of freedom, and the p-value in one table.

**3. Read the result.** The ToolPak returns the means (0.554 and 0.580), a Welch t-statistic of about **−1.67**, and a two-tailed p-value of about **0.10**. Because 0.10 is *above* the conventional 0.05 threshold, you **fail to reject** the null: the metro/non-metro turnout difference is not statistically significant.

| Quantity | Excel source | Value (2020) |
|---|---|---|
| Mean turnout, metro (n = 86) | `AVERAGE` | 0.554 |
| Mean turnout, non-metro (n = 168) | `AVERAGE` | 0.580 |
| Difference (metro − non-metro) | subtraction | −0.026 |
| Welch t-statistic | ToolPak / `T.TEST` | −1.67 |
| p-value (two-tailed) | `T.TEST(...,2,3)` | ≈ 0.10 |
| Decision at α = 0.05 | compare to 0.05 | Fail to reject |

Three teaching points follow. First, the difference is **small** — about 2.6 percentage points. Second, it is **not statistically significant** at the conventional 0.05 level (p ≈ 0.10), so we cannot rule out that it is sampling noise. Third, and most surprising, the sign is **negative**: non-metro (rural) counties turned out *slightly higher* than metro counties, the opposite of the common assumption that rural turnout lags. The honest conclusion is that metro and non-metro Texas counties turned out at statistically indistinguishable rates in 2020.

> **Returning to the Case:** The team now has a defensible answer to its opening question and a template for the rest of the vote-center evaluation. The metro-versus-non-metro comparison is an independent-samples (Welch) t-test, and it returns a small, non-significant, slightly-negative gap — a reminder that "we expected rural turnout to be lower" is a hypothesis to test, not a finding to assume. The natural next steps mirror the chapter: a paired t-test of turnout before versus after vote-center adoption within adopting counties, and a one-way ANOVA across small, mid-size, and large counties to see whether county size structures turnout. In every case the evaluation reports not just "significant or not," but how large the difference is and whether it justifies the policy — and here the difference is neither significant nor large.

## Common Pitfalls

- **Reading the p-value as importance.** Significance is about chance, not magnitude. A tiny, useless difference can be "significant" in a large sample.
- **Using an independent-samples test on paired data.** Pre/post on the same units is paired; treating it as independent discards the pairing.
- **Assuming equal variances by default.** Prefer the Welch test unless you have a reason not to.
- **Running many t-tests across several groups.** Use ANOVA first; pairwise tests inflate the false-positive rate.
- **Reporting a test without an effect size.** A p-value with no Cohen's d leaves the decision-maker unable to judge whether to act.
- **Forgetting baseline equivalence.** A significant between-group difference is not a program effect if the groups were not comparable to begin with.

## Practice and Application

1. **One-sample test.** Using the Case B 2020 panel, test whether mean turnout among non-metro counties (≈ 0.580, n = 168) differs from a benchmark of 0.60. Compute $t$ from `AVERAGE`, `STDEV.S`, and `COUNT`, then get the p-value with `T.DIST.2T`. Interpret in one sentence.

2. **Independent-samples test.** Reproduce the worked example: run a Welch t-test of 2020 turnout in metro versus non-metro counties with both `T.TEST(...,2,3)` and the ToolPak. Confirm you recover means of 0.554 and 0.580, t ≈ −1.67, and p ≈ 0.10, and that the two approaches agree.

3. **Effect size.** For the comparison in Exercise 2, compute Cohen's d from the two means and the pooled SD. Classify it against the small/medium/large benchmarks and write two sentences on whether a difference this small — and non-significant — is practically meaningful.

4. **Paired test.** Using the Case B panel, run a paired t-test of county turnout in two consecutive presidential elections (e.g., 2016 and 2020) using the ToolPak's paired option. Explain why pairing is appropriate here and what it controls for.

5. **One-way ANOVA.** Classify the 254 counties into three groups by population tercile and run **Data Analysis → ANOVA: Single Factor** on 2020 turnout. Report the F-statistic and p-value, state what a significant result does and does not tell you, and describe what follow-up you would run.

## Transition to Chapter 7

t-Tests and ANOVA compare group means but cannot, on their own, account for the baseline differences that Chapter 5 warned us about. When metro counties differ from non-metro counties on income, education, and population all at once, a simple mean comparison confounds the program with everything else that distinguishes the groups. Chapter 7 introduces regression, which lets us compare groups *while holding other characteristics constant* — the first tool in this course capable of isolating one factor's contribution from the tangle of others.
