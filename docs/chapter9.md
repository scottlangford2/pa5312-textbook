---
layout: page
title: "Chapter 9"
permalink: /docs/chapter9/
---

# Interrupted Time Series and Regression Discontinuity

## Epigraphs

> "The regression discontinuity design has the attractive feature that the treatment assignment is known."
> — Guido Imbens and Thomas Lemieux, *Journal of Econometrics* (2008)

> "When the data have a structure, exploit the structure."
> — adapted teaching maxim

## Opening Case: A Texting-While-Driving Ban and a School-Funding Cutoff

The City of San Marcos is reviewing two very different programs in the same week. The first is a municipal distracted-driving enforcement campaign that began on a precise date in 2017. Traffic-injury crashes had been drifting downward for years; the council wants to know whether the campaign bent that trend further, or whether the post-2017 numbers simply continued a decline already underway. There is no comparison city the analysts trust, because San Marcos sits in a unique stretch of the I-35 corridor. All they have is the city's own monthly crash history — a long series interrupted at one known moment.

The second program is a state grant that flows to school districts only if their share of economically disadvantaged students exceeds 60 percent. A district at 60.1 percent receives the grant; a district at 59.9 percent does not. The two districts are, in every meaningful sense, the same — yet a sharp administrative line sorts one into the program and the other out. If the analysts compare outcomes for districts that landed just above and just below the 60 percent threshold, the cutoff itself does the work that randomization would do in an experiment.

These two situations call for two distinct designs. The crash campaign is a natural fit for **interrupted time series**, which models whether the level and slope of an outcome changed at the moment of intervention. The funding cutoff is the textbook setting for **regression discontinuity**, which compares units on either side of an arbitrary threshold. Both can be built in Excel, and both rest on assumptions as specific as their geometry.

**Guiding Questions**

- How can a single series, interrupted at a known date, support a causal claim without any comparison group?
- What does a cutoff on a running variable buy you, and why does it resemble a local experiment?
- What are the identifying assumptions of each design, and what can each genuinely show?

## Why This Chapter Matters

Many of the most consequential public interventions arrive at a known moment (a law's effective date, a campaign launch) or are assigned by a sharp rule (an eligibility score, a population threshold that triggers a mandate). When you can pin down that moment or that threshold, you gain causal leverage that ordinary regression cannot match — because the *timing* or the *rule* is plausibly unrelated to everything else driving the outcome. Interrupted time series and regression discontinuity are the two designs that exploit this structure. They are powerful precisely where difference-in-differences struggles: when there is no good comparison group, or when assignment follows a bright administrative line.

## Interrupted Time Series

### Modeling a Level and Slope Change

Interrupted time series (ITS) uses the pre-intervention trajectory of an outcome as the counterfactual for the post-intervention period. Let $T_t$ be a time counter ($1, 2, 3, \ldots$) running across all periods, let $\text{Post}_t = 1$ after the intervention and 0 before, and let $T^{*}_t$ count the periods since the intervention (0 before it, then $1, 2, 3, \ldots$ after). The model is

$$ Y_t = \beta_0 + \beta_1 T_t + \beta_2 \text{Post}_t + \beta_3 \left( T_t \times \text{Post}_t \right) + \varepsilon_t $$

where the product $T_t \times \text{Post}_t$ is more transparently written as $T^{*}_t$. Each coefficient has a distinct interpretation:

- $\beta_0$: the outcome's level at the start of the series (intercept).
- $\beta_1$: the **pre-intervention slope** — the trend that was already underway.
- $\beta_2$: the **immediate level change** at the moment of intervention (a jump or drop).
- $\beta_3$: the **change in slope** after the intervention — does the trend steepen, flatten, or reverse?

The genius of ITS is that it tests two things at once: did the outcome shift suddenly ($\beta_2$), and did its trajectory change going forward ($\beta_3$)? A program might cause a one-time drop with no change in trend, a trend change with no immediate jump, or both.

> **Briefing:** ITS separates a level change from a slope change. Always report both $\beta_2$ and $\beta_3$ — a campaign that produces a temporary dip but no lasting trend change is a very different story from one that bends the long-run path.

### Identifying Assumptions and Threats

ITS assumes that, absent the intervention, the pre-intervention trend would have continued unchanged. The central threat is a **co-occurring event** (history): anything else that happened at the same time as the intervention is indistinguishable from it. If a statewide speed-limit change took effect the same month as the San Marcos campaign, ITS cannot separate the two. Other threats include **seasonality** (monthly crash data have strong seasonal swings that can masquerade as a slope change unless modeled), **autocorrelation** (errors in adjacent periods are correlated, which understates standard errors), and too few post-intervention periods to estimate a slope reliably. ITS also cannot rule out a gradual confounding trend that merely happens to coincide with the intervention date.

> **Briefing:** ITS has no separate comparison group — the pre-period trend *is* the comparison. Its credibility rests entirely on the claim that nothing else changed at the same moment.

### Worked Example: The Crash Series in Excel

Lay the monthly crash counts in column A (`crashes`, the outcome $Y$), with the date in an adjacent column for reference. In column B, enter `time` as a simple counter `1, 2, 3, …` for every month in the series. In column C, enter `post`: 0 for every pre-2017 month and 1 from the campaign's start month onward (use `=IF(date>=DATE(2017,9,1),1,0)`). In column D, enter `time_post` as the product `=B2*C2`, which yields 0 before the campaign and a rising counter afterward.

Run **Data → Data Analysis → Regression** with *Input Y Range* = `crashes` and *Input X Range* = the three contiguous columns `time`, `post`, `time_post`. An illustrative result:

| Term | Coefficient | Std. Error | t Stat | P-value |
|---|---|---|---|---|
| Intercept ($\beta_0$) | 48.0 | 2.0 | 24.0 | 0.000 |
| time ($\beta_1$) | −0.20 | 0.05 | −4.0 | 0.000 |
| post ($\beta_2$) | −5.0 | 2.2 | −2.27 | 0.025 |
| time_post ($\beta_3$) | −0.30 | 0.09 | −3.33 | 0.001 |

Read it as a story: crashes were already declining by about 0.20 per month ($\beta_1$); at the campaign's launch they dropped by an additional 5 crashes ($\beta_2$, the level change); and afterward the monthly decline accelerated by a further 0.30 per month ($\beta_3$, the slope change). To visualize, plot `crashes` against `time` as a scatter, then add the fitted line; the line should show a downward kink at the intervention month.

> **Returning to the Case (Part 1):** Tell the council that the enforcement campaign is associated with both an immediate drop and a steeper subsequent decline in crashes — but flag that you have not ruled out other 2017 events, and that monthly seasonality should be modeled before the estimate is final.

## Regression Discontinuity

### Assignment by a Cutoff

Regression discontinuity (RDD) applies when treatment is assigned by whether a continuous **running variable** $X$ crosses a known **cutoff** $c$. Units with $X \geq c$ get the program; units with $X < c$ do not. The key insight is that units just above and just below $c$ are nearly identical — a district at 60.1 percent disadvantaged is, on every other dimension, essentially the same as one at 59.9 percent — yet one is treated and the other is not. Near the cutoff, treatment is **as good as randomly assigned** (Imbens and Lemieux, 2008). The estimated effect is the jump in the outcome exactly at the cutoff:

$$ \hat{\tau}_{RDD} = \lim_{x \downarrow c} E[Y \mid X = x] - \lim_{x \uparrow c} E[Y \mid X = x] $$

In practice we fit a regression that allows a discontinuity at $c$. Center the running variable as $\tilde{X} = X - c$ so the cutoff sits at zero, define $D = 1$ if $X \geq c$, and fit a local linear model within a window (bandwidth) around the cutoff:

$$ Y_i = \alpha_0 + \tau D_i + \gamma \tilde{X}_i + \delta \left( D_i \times \tilde{X}_i \right) + \varepsilon_i $$

Here $\tau$ is the RDD effect — the vertical gap between the two fitted lines at $\tilde{X} = 0$. The $\gamma$ term lets the outcome trend with the running variable, and the interaction $\delta$ lets the slope differ on either side of the cutoff.

> **Briefing:** RDD estimates a *local* effect — the impact for units right at the cutoff. It says nothing about districts far above 60 percent or far below it. The price of its credibility is its narrow reach.

### Identifying Assumptions and Threats

RDD's core assumption is **continuity**: absent the program, the relationship between the outcome and the running variable would be smooth (continuous) at the cutoff, so any jump must be caused by the program. This breaks down if units can **manipulate** the running variable to land on the favorable side — for example, if districts could massage their reported disadvantage share to clear 60 percent. The standard diagnostic is to check for **bunching**: plot a histogram of the running variable and look for a suspicious pile-up just above the cutoff (McCrary's test formalizes this). A second threat is choosing a **bandwidth** that is too wide (pulling in dissimilar units and biasing the estimate) or too narrow (too few observations, huge standard errors). A third is any **other rule** that changes at the same cutoff, which would be confounded with the program.

> **Briefing:** If units can choose which side of the cutoff to land on, RDD is dead. Always plot the density of the running variable and look for bunching at the threshold before trusting the estimate.

### Worked Example: A Population-Mandate Cutoff in Excel

Texas occasionally ties requirements to population thresholds. Suppose a fiscal-reporting mandate applies only to cities above 25,000 residents, and we use the **Texas City Finance Panel** to estimate its effect on per-capita sales-tax revenue. The running variable is `population`, the cutoff is $c = 25{,}000$, and we restrict to cities within a bandwidth (say 20,000–30,000).

Build the columns: `revenue` ($Y$); `pop_centered` = `=population-25000`; `D` = `=IF(population>=25000,1,0)`; and the interaction `D_x` = `=D * pop_centered`. Filter the sheet to the bandwidth window first. Then run **Data → Data Analysis → Regression** with *Input Y Range* = `revenue` and *Input X Range* = the three contiguous columns `D`, `pop_centered`, `D_x`. Illustrative output:

| Term | Coefficient | Std. Error | t Stat | P-value |
|---|---|---|---|---|
| Intercept ($\alpha_0$) | 102.0 | 3.0 | 34.0 | 0.000 |
| D ($\tau$) | 6.5 | 3.1 | 2.10 | 0.037 |
| pop_centered | 0.0004 | 0.0002 | 2.00 | 0.047 |
| D_x | −0.0002 | 0.0003 | −0.67 | 0.504 |

The `D` coefficient, 6.5, is the estimated jump in per-capita revenue at the 25,000 threshold — the RDD effect. Before trusting it, build a histogram of `population` near 25,000 (Excel: select the column, **Insert → Statistic Chart → Histogram**, set bin width) and confirm there is no bunching just above the line. Then re-estimate with a narrower bandwidth (e.g., 22,000–28,000) to check that $\tau$ is stable; a result that swings wildly with the bandwidth is fragile.

> **Returning to the Case (Part 2):** For the 60 percent school-funding cutoff, the same recipe applies: center the disadvantage share at 60, define the treatment dummy, fit the local linear model, and — critically — check for bunching at 60 percent before reporting the discontinuity as the grant's effect.

## What Each Design Can and Cannot Show

ITS can show whether an outcome's level and trend changed at a known moment, using the series' own history as the counterfactual — but it cannot, on its own, separate the intervention from anything else that happened at the same time. RDD can show a credible *local* causal effect for units right at a cutoff, rivaling an experiment in that narrow band — but it cannot tell you the effect for units far from the threshold, and it collapses if units manipulate their position. Both are sharp tools for specific structures, not all-purpose estimators.

## Common Pitfalls

- **ITS with too few post-periods.** Estimating a post-intervention slope from three or four observations gives a number with no real precision.
- **Ignoring seasonality and autocorrelation in ITS.** Monthly public-safety or fiscal series swing seasonally; an unmodeled cycle can masquerade as a slope change.
- **Confounding the intervention with a co-occurring event.** In ITS, anything else that changed on the same date is baked into the estimate.
- **Skipping the bunching check in RDD.** If you never plot the density of the running variable, you cannot claim continuity.
- **Extrapolating an RDD estimate far from the cutoff.** The effect is local; do not report it as the program's average effect for everyone.
- **Non-contiguous X columns in the ToolPak.** As always, the X variables must sit in adjacent columns.

## Practice and Application

1. **ITS setup.** Construct the `time`, `post`, and `time_post` columns for a monthly series of your choice (real or simulated) with a known intervention date, and run the ITS regression. Interpret $\beta_2$ and $\beta_3$ in plain language.
2. **ITS visualization.** Plot the series with a fitted line and mark the intervention month. In two sentences, describe whether the picture shows a level change, a slope change, both, or neither.
3. **RDD setup.** Using the city finance panel and a population cutoff of 25,000, build `pop_centered`, `D`, and `D_x`, restrict to a bandwidth, and estimate $\tau$. Report the discontinuity.
4. **Bunching check.** Make a histogram of `population` near 25,000. State whether you see evidence of manipulation and what it would imply for the design.
5. **Bandwidth sensitivity.** Re-run the RDD with a wider and a narrower bandwidth. Report how $\tau$ changes and what that tells you about the estimate's robustness.

## Transition to Chapter 10

Chapters 7 through 9 have built a ladder of evaluation designs — covariate-adjusted regression, difference-in-differences, interrupted time series, and regression discontinuity — each trading on a different assumption to approximate the experimental ideal. Chapter 10 steps back to weigh them against one another: given a particular program, a particular dataset, and a particular policy question, which design is most credible, and how do you communicate both the estimate and its limits to decision-makers who did not take this course? The methods are only as good as the honesty with which you report what they can and cannot prove.
