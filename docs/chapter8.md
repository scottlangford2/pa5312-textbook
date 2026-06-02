---
layout: page
title: "Chapter 8"
permalink: /docs/chapter8/
---

# Quasi-Experimental Designs and Difference-in-Differences

## Epigraphs

> "The most credible and influential research designs use random assignment."
> — Joshua Angrist and Jörn-Steffen Pischke, *Mostly Harmless Econometrics* (2009)

> "A comparison group is the heart of any impact evaluation."
> — Paul Gertler and colleagues, *Impact Evaluation in Practice* (2016)

## Opening Case: A Local Sales-Tax Change in Central Texas

In 2019, a cluster of Central Texas cities adopted a dedicated quarter-cent sales tax to fund street maintenance and economic development. Neighboring cities of similar size, served by the same regional economy along the I-35 corridor, did not. Three years later, the regional council of governments asks a simple-sounding question: did the new tax actually raise the adopting cities' total sales-tax revenue, or did it merely shift the timing of purchases or push shoppers across municipal lines?

A first instinct is to look at the adopting cities before and after 2019. Revenue did rise — but so did revenue almost everywhere, because the entire Central Texas economy was booming. A before-and-after comparison would credit the tax change with growth that would have happened anyway. A second instinct is to compare adopting cities to non-adopting cities in 2022 alone. But the cities that chose to adopt may have been growing faster (or slower) to begin with; a single post-period snapshot confounds the policy with pre-existing differences.

The way out is to combine both comparisons. If you measure how revenue changed over time in the adopting cities, and subtract off how revenue changed over the same period in comparable non-adopting cities, you difference away both the economy-wide trend and the fixed differences between the two groups. What remains is the part of the change unique to the cities that adopted the tax. This is the logic of difference-in-differences, and it is the most widely used quasi-experimental design in applied public policy.

**Guiding Questions**

- When randomization is impossible, what makes a comparison group credible?
- How does difference-in-differences remove both time trends and fixed group differences at once?
- What exactly is the parallel-trends assumption, and how would a violation fool us?

## Why This Chapter Matters

Public programs are almost never assigned by lottery. Legislatures phase policies in by region, agencies target services to needy populations, and cities opt into local-option taxes. In each case, the people or places that get the program differ from those that do not. Quasi-experimental designs are a family of strategies for squeezing a credible causal estimate out of these messy roll-outs by choosing comparison groups and time windows thoughtfully. Done well, they approximate an experiment. Done badly, they repackage selection bias as a finding. This chapter teaches the most useful of these designs and, just as important, the assumption you must defend to use it.

## Weak Designs and Their Threats

### The Single-Group Pre/Post Design

The simplest quasi-experiment measures one group before and after the program: $\hat{\tau} = \bar{Y}_{\text{post}} - \bar{Y}_{\text{pre}}$. Its fatal weakness is that anything else that changed over the same window — the economy, a season, a co-occurring policy — is mistaken for the program's effect. Shadish, Cook, and Campbell (2002) catalog these as threats to internal validity: **history** (other events), **maturation** (natural trends), **testing**, and **regression to the mean**. A pre/post design cannot rule any of them out.

### The Nonequivalent Comparison-Group Design

Adding an untreated comparison group helps but does not save us. Comparing treated and comparison groups in the post-period only ($\bar{Y}^{T}_{\text{post}} - \bar{Y}^{C}_{\text{post}}$) is contaminated by **selection bias**: the groups may have differed before the program ever started. The two weak designs fail for opposite reasons — pre/post ignores the comparison group, post-only ignores the baseline.

> **Briefing:** Pre/post controls for fixed differences between groups but not for time trends. Post-only controls for time but not for fixed group differences. Difference-in-differences controls for both.

## The Difference-in-Differences Logic

Difference-in-differences (DiD) combines the two comparisons. Define a treated group ($T$) and a comparison group ($C$), each observed in a pre-period and a post-period. The estimator is the difference of two differences:

$$ \hat{\tau}_{DiD} = \left( \bar{Y}^{T}_{\text{post}} - \bar{Y}^{T}_{\text{pre}} \right) - \left( \bar{Y}^{C}_{\text{post}} - \bar{Y}^{C}_{\text{pre}} \right) $$

The first parenthesis is the change in the treated group; the second is the change in the comparison group over the same window. Subtracting the second from the first removes any change common to both groups — the regional economy, statewide policy, inflation — leaving only the change unique to the treated group. The canonical application is Card and Krueger's (1994) study of a New Jersey minimum-wage increase, using neighboring Pennsylvania as the comparison.

### The 2×2 DiD Table

For a single treated group, a single comparison group, and two periods, DiD is just arithmetic on four cell means:

| | Pre-period | Post-period | Difference (Post − Pre) |
|---|---|---|---|
| **Treated cities** | 92.0 | 104.0 | +12.0 |
| **Comparison cities** | 90.0 | 98.0 | +8.0 |
| **Difference (T − C)** | +2.0 | +6.0 | **+4.0** |

The bottom-right cell, **+4.0**, is the DiD estimate. Read it two equivalent ways: the treated group grew by 12.0 while the comparison grew by 8.0, so the policy added $12.0 - 8.0 = 4.0$; or the gap between groups widened from +2.0 to +6.0, again +4.0. The +2.0 pre-period gap is exactly the fixed difference that a post-only comparison would have wrongly attributed to the policy.

> **Briefing:** In the 2×2 table, the four means tell the whole story. The pre-period row difference is the baseline gap you must not blame on the program; DiD is the change in that gap.

## DiD as a Regression with an Interaction Term

The table is intuitive but limited to one treated and one comparison group with no controls. The regression form generalizes it. Define $\text{Treat}_i = 1$ for units in the treated group, $\text{Post}_t = 1$ for the post-period, and their product $\text{Treat}_i \times \text{Post}_t$. Then

$$ Y_{it} = \beta_0 + \beta_1 \text{Treat}_i + \beta_2 \text{Post}_t + \beta_3 \left( \text{Treat}_i \times \text{Post}_t \right) + \varepsilon_{it} $$

Each coefficient maps onto a piece of the table. $\beta_0$ is the comparison group's pre-period mean; $\beta_1$ is the baseline treated-comparison gap; $\beta_2$ is the common time trend experienced by both groups; and the interaction coefficient $\beta_3$ **is the DiD estimate** — the extra change in the treated group beyond the common trend. You can confirm that $\beta_3$ equals the +4.0 from the 2×2 table exactly. The regression form earns its keep by letting you add control variables, use many cities and many years, and read off a standard error for $\beta_3$ directly.

> **Briefing:** In a DiD regression, the coefficient on the interaction term $\text{Treat}\times\text{Post}$ is your effect estimate. The two main effects are bookkeeping; the interaction is the finding.

## Worked Example: The Sales-Tax Change in the City Finance Panel

We test the Central Texas tax change using the **Texas City Finance Panel**. Restrict the data to two years — say 2018 (pre) and 2021 (post) — and to the adopting and comparison cities. Build four columns: `revenue` (per-capita sales-tax revenue, the outcome $Y$), `treat` (1 for adopting cities, 0 otherwise), `post` (1 for 2021, 0 for 2018), and an interaction `treat_post`.

First, create the interaction column with a formula. If `treat` is in column B and `post` in column C, then in column D enter `=B2*C2` and fill down. This yields the product that is 1 only for treated cities in the post-period.

Next, build the 2×2 table with `AVERAGEIFS`. For the treated post-period mean, use `=AVERAGEIFS(revenue_range, treat_range, 1, post_range, 1)`; change the criteria to fill in all four cells. Subtract to get the DiD estimate by hand.

Then run the regression. Open **Data → Data Analysis → Regression**. Set *Input Y Range* to `revenue`. The *Input X Range* must be the three contiguous columns `treat`, `post`, `treat_post` (rearrange columns so they are adjacent). Check *Labels* and *Confidence Level 95%*. The coefficient table will resemble:

| Term | Coefficient | Std. Error | t Stat | P-value |
|---|---|---|---|---|
| Intercept ($\beta_0$) | 90.0 | 2.1 | 42.9 | 0.000 |
| treat ($\beta_1$) | 2.0 | 2.9 | 0.69 | 0.491 |
| post ($\beta_2$) | 8.0 | 2.9 | 2.76 | 0.006 |
| treat_post ($\beta_3$) | 4.0 | 4.1 | 0.98 | 0.329 |

The `treat_post` coefficient, 4.0, matches the table's bottom-right cell. Its P-value tells you whether the estimated \$4-per-capita effect is distinguishable from zero given the noise — here it is not, a useful reminder that a point estimate without a standard error can mislead.

> **Returning to the Case:** Report to the council of governments that adopting cities' per-capita revenue rose about \$4 more than comparable non-adopting cities over 2018–2021 — but that this difference is not statistically distinguishable from zero in this sample, and the whole estimate rests on the assumption examined next.

## The Parallel-Trends Assumption and Its Limits

DiD does not assume the two groups are identical. It assumes something weaker but crucial: that *in the absence of the program*, the treated and comparison groups would have followed **parallel trends** — their outcomes would have moved up or down together by the same amount. The baseline gap can be any size; what must hold is that the gap would have stayed constant without the intervention.

This assumption is untestable directly, because we never observe the treated group's counterfactual path. But we can build confidence in it. The standard check is to examine **pre-treatment trends**: if the two groups moved in parallel in the years *before* the policy, parallel trends in the post-period is more plausible. With several pre-periods in the city panel, plot per-capita revenue for both groups from 2013 to 2018 and look for parallel lines. Divergence before treatment is a red flag.

> **Briefing:** Parallel trends is an assumption about a path you cannot see. Defend it with pre-trend evidence and institutional knowledge; never assert it just because you ran the regression.

The assumption fails when something *other* than the program differentially affected one group at the same time. If a new highway interchange opened in the adopting cities in 2020, or a major employer relocated to the comparison cities, the trends would have diverged regardless of the tax, and DiD would attribute that divergence to the policy. Other limits: DiD with a single treated and comparison unit has no real statistical uncertainty; staggered adoption (cities adopting in different years) requires more careful methods than the simple 2×2; and DiD estimates the effect for the treated group, which may not generalize to others.

## Common Pitfalls

- **Forgetting the comparison group.** A before-and-after table with no comparison is a pre/post design wearing a DiD costume; it controls for nothing about the trend.
- **Choosing a comparison group with different pre-trends.** If the groups were already diverging before treatment, the design is broken no matter how clean the regression looks. Always plot pre-trends.
- **Reading the main effects as the answer.** $\beta_1$ and $\beta_2$ are not the program effect; only the interaction $\beta_3$ is.
- **Non-contiguous X columns in the ToolPak.** `treat`, `post`, and `treat_post` must sit in adjacent columns or Excel will read the wrong data.
- **Ignoring uncertainty.** A DiD point estimate with a wide confidence interval, as in the worked example, does not support a confident causal claim.

## Practice and Application

1. **Build the 2×2 by hand.** Using the city finance panel for 2018 and 2021, compute the four `AVERAGEIFS` means for adopting vs. comparison cities and report the DiD estimate.
2. **Confirm via regression.** Run the interaction regression and verify that $\beta_3$ equals your hand-computed DiD. Report the P-value and interpret it.
3. **Pre-trends check.** Plot per-capita revenue for both groups across 2013–2018. In two sentences, state whether the parallel-trends assumption looks defensible.
4. **A threat to validity.** Name one plausible event other than the tax change that could have differentially affected the adopting cities around 2019, and explain how it would bias $\hat{\tau}_{DiD}$.
5. **County application.** Using the county panel, define a "treated" set of counties (e.g., those adopting some policy you can identify or simulate) and a pre/post pair of elections, and estimate a DiD effect on turnout. State your comparison group and why it is credible.

## Transition to Chapter 9

Difference-in-differences leans on a comparison group to stand in for the counterfactual. But sometimes the cleanest leverage comes not from another group but from a sharp moment in time, or from a sharp threshold in a rule. Chapter 9 develops two such designs. Interrupted time series asks whether an outcome's level and slope changed at the exact moment an intervention took effect, using the program's own history as the comparison. Regression discontinuity exploits an arbitrary cutoff — an eligibility score, a population threshold, a vote share — to compare units that landed just above and just below the line. Both can be implemented in Excel, and both, like DiD, live or die by an assumption you must state out loud.
