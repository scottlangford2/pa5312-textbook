---
layout: page
title: "Chapter 3"
permalink: /docs/chapter3/
---

# Evaluation Questions, Designs, and Causal Inference

## Epigraphs

> "No causation without manipulation."
> — Paul W. Holland, *Journal of the American Statistical Association* (1986)

> "The fundamental problem of causal inference is that we can observe at most one of the potential outcomes for each unit."
> — paraphrasing the framework of Donald B. Rubin and Paul W. Holland

## Opening Case: Did the Sales-Tax Holiday Help Texas Cities?

Suppose a coalition of Texas city finance directors wants to know whether a state-authorized "small-business Saturday" sales-tax incentive, adopted by some cities and not others starting in 2019, actually raised local taxable sales. A consultant presents a striking chart: in the cities that adopted the incentive, taxable sales rose 9% over the next three years. The implication offered is that the incentive *caused* a 9% increase, and other cities should adopt it.

A skeptical director raises her hand. The cities that adopted the incentive, she points out, were disproportionately the fast-growing suburbs — places where taxable sales were climbing anyway because of population growth. Maybe they adopted *because* they were booming, not boomed *because* they adopted. Another director notes that 2019–2022 spanned the pandemic, which scrambled retail sales everywhere, in different directions for different cities. A third asks the simplest and hardest question: compared to *what*? Nine percent growth relative to what those same cities *would have done* without the incentive — a number nobody observed.

The chart describes a *correlation*. The directors are demanding a *causal* claim. The gap between the two is the entire subject of this chapter: turning an evaluation question into a design that can credibly support a causal answer, and recognizing when no such answer is available.

**Guiding Questions**

- What exactly do we mean when we say the incentive "caused" a change in taxable sales?
- Why might adopters and non-adopters differ in ways that masquerade as a program effect?
- Which research designs could make the 9% claim credible, and which could not?

## Why This Chapter Matters

The decision a manager faces is almost always causal: *if we adopt (or keep, or cut) this program, what will happen?* Yet the data that arrive on a manager's desk are almost always correlational. The skill that separates a competent evaluator from a credulous one is the ability to specify the causal question precisely, to recognize the threats that make a naive comparison misleading, and to choose a design whose credibility matches the stakes of the decision. This chapter is the conceptual hinge of the course; every later method — t-tests, regression, difference-in-differences, RD, RCTs — is a tool for closing the gap between correlation and cause.

> **Briefing:** Managers ask causal questions; raw data answer correlational ones. Evaluation design is the discipline of closing that gap honestly.

## Turning Questions into Designs

A well-posed evaluation question names four things: the *program* (the treatment), the *population* (whose outcomes we care about), the *outcome* (the specific, measurable change), and the *comparison* (relative to what). The consultant's claim was missing the fourth. "Taxable sales rose 9%" has no comparison; "taxable sales in adopting cities rose 9% more than they would have absent the incentive" names a comparison — and immediately raises the question of how we could possibly know the second quantity. Design is the answer to that question.

## The Counterfactual and Potential Outcomes

The modern way to make "caused" precise is the *potential-outcomes framework*. For each unit $i$ (here, a city) consider two potential outcomes:

$$
Y_i(1) = \text{outcome if city } i \text{ adopts the incentive}, \qquad Y_i(0) = \text{outcome if it does not.}
$$

The *causal effect of the program for city $i$* is the difference between these two potential worlds:

$$
\tau_i = Y_i(1) - Y_i(0).
$$

Here is the difficulty, which Holland (1986) called the *fundamental problem of causal inference*: for any given city we observe only **one** of these. A city that adopted reveals $Y_i(1)$; its $Y_i(0)$ — what it would have done without the incentive — is forever unobserved. That missing quantity is the *counterfactual*. We can never measure an individual effect $\tau_i$ directly.

What we can hope to estimate is an *average* effect across a group, the *average treatment effect*:

$$
\text{ATE} = E[\,Y_i(1) - Y_i(0)\,] = E[\,Y_i(1)\,] - E[\,Y_i(0)\,].
$$

Estimating the ATE requires a credible stand-in for the unobserved $E[Y_i(0)]$ — a comparison group whose outcomes approximate what the treated group would have done without treatment. Every design in this chapter is, at bottom, a different strategy for constructing that stand-in.

> **Briefing:** A program's effect is the difference between two potential outcomes, one of which is never observed; the comparison group is our estimate of the missing counterfactual.

## Selection Bias

Why not simply compare adopters to non-adopters? Because the two groups may differ for reasons unrelated to the program. Decompose the naive difference in observed outcomes between treated ($D=1$) and untreated ($D=0$) groups:

$$
\underbrace{E[Y_i \mid D=1] - E[Y_i \mid D=0]}_{\text{naive comparison}} = \underbrace{E[Y_i(1) - Y_i(0) \mid D=1]}_{\text{effect on the treated}} + \underbrace{\big(E[Y_i(0) \mid D=1] - E[Y_i(0) \mid D=0]\big)}_{\text{selection bias}}.
$$

The second term is *selection bias*: the difference in the *untreated* potential outcome between the groups. If booming suburbs both adopt the incentive *and* would have had higher sales growth anyway, then $E[Y_i(0)\mid D=1] > E[Y_i(0)\mid D=0]$, the selection-bias term is positive, and the naive 9% overstates the true effect — possibly entirely. Selection bias is not a flaw in arithmetic; it is a flaw in *whom we are comparing*. The whole art of design is making the selection-bias term go to zero, or bounding it.

> **Briefing:** A naive treated-minus-untreated comparison equals the true effect *plus* selection bias; credible designs are the ones that eliminate or bound that bias term.

## Internal and External Validity

Two distinct questions govern a design's credibility. *Internal validity* asks whether the study correctly identifies the causal effect *for the units and setting studied* — is the estimated effect really the program's, free of selection bias and other confounds? *External validity* asks whether that effect *generalizes* — would the same incentive produce the same effect in rural West Texas cities, in a non-pandemic year, at a different dosage? The two often trade off. A tightly controlled experiment in a few volunteer cities may have high internal validity but uncertain external validity; a sprawling observational study of all 1,180 cities may speak to the whole state but be riddled with selection bias. An evaluator must be explicit about which kind of validity the decision requires.

> **Briefing:** Internal validity = "is the effect real *here*?"; external validity = "does it travel *there*?" Strengthening one frequently weakens the other.

## Classic Threats to Internal Validity

Shadish, Cook, and Campbell (2002) catalog the recurring ways a before-after or non-equivalent-group comparison can fool you. Five are essential.

- **History.** An external event coinciding with the program affects the outcome. The pandemic hitting between 2019 and 2022 is a textbook history threat to the sales-tax study.
- **Maturation.** Units change naturally over time regardless of the program — fast-growing suburbs keep growing. A before-after rise can be pure maturation.
- **Selection.** Treated and untreated groups differ at baseline, as in our adopters-vs-non-adopters problem; this is the threat that produces selection bias.
- **Regression to the mean.** When units are chosen *because* they had an extreme value (e.g., a city targeted for help after an unusually bad sales year), their later values tend to drift back toward average even with no program at all, mimicking an effect.
- **Attrition.** Units drop out of the study non-randomly. If struggling cities stop reporting, the surviving sample looks artificially successful.

A sixth worth naming is *testing/instrumentation* — changes in how the outcome is measured over time, such as a revised sales-tax reporting rule, which can masquerade as a real change.

## A Menu of Designs

Designs form a rough ladder of causal credibility. The right rung depends on the decision's stakes and on what is feasible.

### Experimental Designs

In a *randomized controlled trial (RCT)*, units are assigned to treatment or control *by chance*. Randomization makes the two groups equivalent in expectation on *everything* — observed and unobserved — so $E[Y_i(0)\mid D=1] = E[Y_i(0)\mid D=0]$ and the selection-bias term vanishes. This is why the RCT is the benchmark for internal validity (Gertler et al., 2016, build their entire impact-evaluation toolkit around this point). Its limits are practical and ethical: you often cannot randomize a city's tax policy.

### Quasi-Experimental Designs

When randomization is impossible, *quasi-experiments* construct a comparison group by other means and lean on assumptions to defend it. *Difference-in-differences* compares the before-after change in adopters to the before-after change in non-adopters, differencing out fixed differences and common trends (Chapter 8). *Regression discontinuity* exploits a sharp eligibility cutoff (Chapter 9). *Matching* and *regression with controls* (Chapter 7) adjust for observed differences between groups. These are credible to the extent their identifying assumptions hold — and an honest evaluator states those assumptions.

### Observational and Descriptive Designs

A plain *observational* comparison of adopters and non-adopters, or a *before-after* (pre-post) comparison with no comparison group, controls for nothing and is exposed to every threat above; it is the consultant's 9%. *Descriptive* designs make no causal claim at all — they characterize a population or trend (how many cities adopted, how taxable sales are distributed). Descriptive work is honest and useful precisely because it does not overreach.

> **Briefing:** Credibility climbs from descriptive to observational to quasi-experimental to experimental, as the comparison group's defense against selection bias gets stronger.

### Worked Example: Decomposing a Naive Comparison in Excel

Return to the directors' 9% claim. Suppose we have, for adopting and non-adopting cities, mean taxable sales in 2018 (pre) and 2022 (post). A naive before-after for adopters overstates the effect; a difference-in-differences begins to net out the common shock. In Excel, lay the four cell means in a small block:

- Place pre/post means for each group in **B2:C3**.
- Adopters' raw change in **D2**: `=C2-B2`.
- Non-adopters' raw change in **D3**: `=C3-B3`.
- The **difference-in-differences** estimate in **D4**: `=D2-D3` — the adopters' change *net of* the change non-adopters experienced over the same period.

| Group | 2018 mean (B) | 2022 mean (C) | Change (D) |
|-------|--------------:|--------------:|-----------:|
| Adopters | 100.0 | 109.0 | 9.0 |
| Non-adopters | 100.0 | 105.0 | 5.0 |
| **Diff-in-diff** | | | **4.0** |

The naive story credited the incentive with the full +9.0. Once we subtract the +5.0 that *non-adopters* also gained over the same window (capturing the common history/maturation), the difference-in-differences estimate is +4.0. That estimate is credible *only if* we believe adopters and non-adopters would have followed *parallel trends* absent the incentive — the identifying assumption we will scrutinize in Chapter 8. Even this is not proof; it is a more defensible comparison.

> **Returning to the Case:** The consultant's 9% conflated the program's effect with selection and history. Specifying the counterfactual ($Y_i(0)$ for adopting cities), naming the threats (selection toward booming suburbs; the pandemic as history), and moving from a before-after to a difference-in-differences design turns an indefensible number into a defensible — and smaller — estimate, with its assumption stated out loud.

## Common Pitfalls

- **Reporting a correlation as a cause.** "Adopters grew 9%" is not "the incentive caused 9% growth."
- **Comparing groups that selected themselves.** Volunteers, early adopters, and the worst-off differ systematically from everyone else.
- **Ignoring a coinciding shock.** A pandemic, a recession, or a state law change can drive the outcome instead of the program (history).
- **Mistaking regression to the mean for an effect.** Programs that target the worst performers will look effective even if they do nothing.
- **Overclaiming external validity.** An effect found in volunteer suburbs may not hold statewide.

## Practice and Application

1. **Define the effect.** For the sales-tax incentive, write the potential outcomes $Y_i(1)$ and $Y_i(0)$ in words for a single city, and explain in one sentence why $\tau_i$ can never be observed directly.
2. **Name the threats.** List the five classic internal-validity threats and give a concrete sales-tax-incentive example of each.
3. **Diff-in-diff (Excel).** Recreate the worked example. Then open the Texas City Finance Panel, designate any plausible "adopter" and "comparison" set of cities, and compute a difference-in-differences in sales-tax revenue between 2018 and 2022 using cell formulas. State the parallel-trends assumption your estimate relies on.
4. **County panel selection bias (Excel).** Using the Texas County Panel, compare mean turnout in high-income versus low-income counties with an `AVERAGEIF` formula. Explain why this difference is *not* the causal effect of income on turnout, identifying at least one confounder.
5. **Match design to decision.** For three real Texas decisions — keep a workforce voucher, adopt a city tax incentive, choose between two literacy curricula — name the most credible *feasible* design and justify the internal/external validity trade-off it makes.

## Transition to Chapter 4

We now know *what* we want to estimate (a treatment effect against a counterfactual) and *which designs* can credibly deliver it. But a design is only as good as the numbers fed into it: a difference-in-differences on mismeasured sales data, or a turnout comparison built on an inconsistent voter file, will mislead no matter how clean the design. Chapter 4 turns to measurement and administrative data — how to define indicators, judge their reliability and validity, and wrangle the messy real-world records that Texas agencies actually keep — so that the elegant logic of this chapter rests on data worth analyzing.
