---
layout: page
title: "Chapter 10"
permalink: /docs/chapter10/
---

# Randomized Controlled Trials

## Epigraphs

> "Randomized experiments are the gold standard for estimating causal effects."
> — Donald B. Rubin

> "Random assignment is a procedure for creating treatment and control groups that are, on average, identical in every way except the treatment itself."
> — Alan S. Gerber and Donald P. Green, *Field Experiments* (2012)

## Opening Case: The Travis County Eviction-Diversion Pilot

A coalition of judges, legal-aid attorneys, and the Travis County commissioners is alarmed by the post-pandemic surge in residential evictions. Their idea is a *diversion* program: when a landlord files for eviction, the tenant is offered a 30-minute mediation session plus one-time rental assistance before the case goes before a justice of the peace. Advocates believe the program will sharply reduce the number of households that lose their housing. Skeptics on the commissioners' court worry that the families who *accept* mediation would have worked things out anyway, and that the program will simply spend public money on outcomes that would have happened regardless.

You are hired to evaluate the pilot. Your first instinct is to compare eviction rates for tenants who used mediation against those who did not. But you quickly see the problem: tenants who voluntarily show up to mediation are different from those who do not. They may be more motivated, more employed, or simply more able to take an afternoon off work. Any difference in outcomes could reflect *who chose the program* rather than *what the program did*. This is selection bias, the recurring villain of the earlier chapters.

The court has enough funding to serve only about half of eligible filings in the first year. That scarcity is, from an evaluation standpoint, an opportunity. If the county allocates the limited slots *by lottery* among eligible tenants, you can compare the lucky and unlucky groups and, for once, defend a genuine causal claim about the program's effect.

**Guiding Questions**

- Why does random assignment, and almost nothing else, let us interpret a group difference as a causal effect?
- What real-world complications — refusal of treatment, dropout, neighbors talking to neighbors — threaten an experiment even after we randomize?
- Is it ethical, and is it feasible, to assign a public benefit by chance?

## Why This Chapter Matters

Every design we have studied so far tries to *approximate* the comparison a randomized experiment makes directly. Difference-in-differences, matching, and regression with controls all ask, in effect, "what would the treated group have looked like without the program?" and then construct a plausible answer from observational data. A randomized controlled trial (RCT) does not have to construct that answer; it manufactures the counterfactual by design. Understanding the RCT is therefore the conceptual anchor for the entire course. Once you see *why* randomization works, you can judge how well any weaker design substitutes for it.

## Random Assignment and the Logic of Causal Identification

Recall the potential-outcomes framework. For each person $i$ there are two potential outcomes: $Y_i(1)$, the outcome if treated, and $Y_i(0)$, the outcome if not. The individual causal effect is $Y_i(1) - Y_i(0)$. We can never observe both — this is the *fundamental problem of causal inference*. We see a person either in the program or out of it, never both.

What we can hope to recover is the **average treatment effect** (ATE):

$$\text{ATE} = E[Y_i(1)] - E[Y_i(0)]$$

The trouble in observational data is that the people we observe as treated are not a fair stand-in for everyone's $Y_i(1)$, and the untreated are not a fair stand-in for everyone's $Y_i(0)$. Random assignment fixes exactly this. When treatment $D_i$ is assigned by a coin flip, it is statistically independent of the potential outcomes:

$$E[Y_i(0) \mid D_i = 1] = E[Y_i(0) \mid D_i = 0]$$

In words: the control group's untreated outcome is, in expectation, what the treated group's outcome *would have been* without treatment. The control group is a valid counterfactual. The simple difference in group means is then an unbiased estimate of the ATE:

$$\widehat{\text{ATE}} = \bar{Y}_{\text{treatment}} - \bar{Y}_{\text{control}}$$

> **Briefing:** Randomization does not make the two groups identical in any single sample — it makes them identical *in expectation*, balancing both the characteristics you measured and the ones you never thought to measure.

That last clause is the magic. Matching and regression can only balance variables you have data on. Randomization balances *everything*, including unobserved motivation, family support, and a tenant's relationship with the landlord — the very things that drive selection bias in the eviction case.

### Designing an RCT

A credible experiment has a few non-negotiable parts:

- **A defined population and eligibility rule.** In the case, "tenants with an eviction filed in a participating JP court."
- **A treatment and a control condition.** Treatment: offer mediation plus assistance. Control: business as usual (the existing court process).
- **A randomization mechanism** that is genuinely unpredictable and documented — a random-number generator, a sealed-envelope lottery, or a published seed.
- **Pre-specified outcomes** measured the same way for both groups (e.g., whether a writ of possession issued within 90 days).

> **Briefing:** Decide and write down your outcomes and analysis *before* you see the data. Choosing the outcome that happens to look best after the fact is a recipe for false findings.

**Blinding.** In medical trials, neither patient nor doctor knows who got the real drug, which prevents expectations from coloring outcomes. In public programs, blinding the *participant* to whether they received mediation is usually impossible. But you can often blind the *people who measure outcomes* — the coder who reads case files should not know which arm a case belongs to. That guards against measurement bias even when full blinding is infeasible.

## When Reality Intrudes: Attrition, Noncompliance, and Spillovers

Randomization at the moment of assignment is clean. What happens afterward rarely is.

### Attrition

Attrition is the loss of subjects from measurement — tenants who move and cannot be tracked, records that go missing. The danger is not the lost sample size; it is *differential* attrition. If unsuccessful treatment-group tenants are the ones who disappear (because they were evicted and left no forwarding address), the surviving treatment group looks artificially successful. Always report attrition rates by arm and check whether the dropouts differ on baseline characteristics.

### Noncompliance and ITT vs. ToT

Some tenants assigned to mediation will refuse to attend. Some assigned to control may find mediation through a nonprofit on their own. Assignment and actual treatment have come apart.

You have two honest things to estimate. The **intention-to-treat (ITT)** effect compares everyone *as randomized*, regardless of what they actually did. It answers the policy question a commissioner cares about: "If we offer this program, what happens?" The **treatment-on-the-treated (ToT)** effect tries to recover the effect on those who actually complied. Intuitively, if only 60% of the treatment group took up mediation and the program can only work through mediation, the ToT is roughly the ITT scaled up — the same total effect concentrated among the 60% who participated.

> **Briefing:** ITT preserves the randomization and is almost always the right headline number for a public decision-maker, because real programs can only *offer*, not *force*, participation.

### Spillovers

The independence that makes randomization work assumes one person's treatment does not affect another's outcome. That can fail. If mediation training changes how a landlord behaves toward *all* their tenants — including control-group tenants in the same building — the control group is contaminated and the estimated effect is understated. When spillovers are likely, evaluators sometimes randomize at the group level (e.g., by court or by apartment complex) rather than the individual level.

## Ethics and Feasibility

Is a lottery for a public benefit fair? Often it is *more* fair than the alternatives, especially when slots are genuinely scarce — a lottery treats every eligible person equally, with no favoritism. Ethical experiments rest on a few pillars: there should be genuine uncertainty about whether the program helps (*equipoise*); participants should give informed consent where practical; and the control group should not be denied anything they were already entitled to. A common humane design is the **waitlist** or **phase-in**: the control group receives the program later, so the trial only randomizes the *order* of a benefit everyone eventually gets. Some programs simply cannot be randomized — you cannot randomize which cities get hit by a hurricane — and for those we fall back on the quasi-experimental designs from earlier chapters.

### Worked Example: Analyzing the Eviction Trial in Excel

Suppose 600 eligible tenants were randomized, 300 to each arm. The outcome is a binary indicator, `evicted` (1 = a writ of possession issued within 90 days, 0 = not). Your spreadsheet has one row per tenant with columns `treat` (1/0) and `evicted` (1/0).

**Step 1 — Check balance.** Before trusting the randomization, confirm the arms look similar on baseline traits. Use `AVERAGEIF` to compare, say, baseline monthly rent by arm: `=AVERAGEIF(treat_range, 1, rent_range)` versus `=AVERAGEIF(treat_range, 0, rent_range)`. Large gaps would signal a broken randomization.

**Step 2 — Estimate the ITT effect.** Compute each arm's eviction rate with `AVERAGEIF` on the `evicted` column. The difference is the estimated treatment effect on the eviction *rate*.

**Step 3 — Test it.** Run the ToolPak's **t-Test: Two-Sample Assuming Unequal Variances** (Data ▸ Data Analysis), with the treatment group's `evicted` values as Variable 1 and the control group's as Variable 2. Equivalently — and this scales to adding controls later — run **Regression** with `evicted` as Y and `treat` as the single X. The coefficient on `treat` *is* the difference in means, and its p-value tests the same hypothesis.

| Quantity | Excel result |
|---|---|
| Control eviction rate $\bar{Y}_{C}$ | 0.42 |
| Treatment eviction rate $\bar{Y}_{T}$ | 0.30 |
| Estimated ITT effect | $-0.12$ (12 fewer evictions per 100) |
| t-test two-tail p-value | 0.003 |
| Regression coef. on `treat` | $-0.12$, p = 0.003 |

The negative coefficient says assignment to the program lowered the eviction rate by 12 percentage points, and the p-value says a gap this large is very unlikely if the program truly did nothing.

> **Returning to the Case:** Because slots were assigned by lottery, the 12-point drop is not an artifact of which tenants chose mediation — the lottery balanced motivation and circumstance across arms. You can tell the commissioners' court, with a straight face, that *offering* the program (ITT) caused fewer evictions. If only 70% of the treatment arm actually attended mediation, you would note that the effect *among attenders* (ToT) is larger still, and you would report the attrition rate in each arm so the court can judge whether tracking loss might be flattering your result.

## Common Pitfalls

- **Reporting the ToT as if it were the program's overall effect.** A commissioner authorizes an *offer*, not guaranteed participation; lead with the ITT.
- **Ignoring differential attrition.** A clean randomization can still produce a biased estimate if the groups are measured unequally afterward.
- **Analyzing only compliers as a self-contained group.** Comparing tenants who *attended* mediation to controls who *didn't* throws away the randomization and reintroduces selection bias — the original sin you used the experiment to avoid.
- **Treating a statistically significant difference as a large or important one.** Significance and magnitude are different questions; always report the effect size.
- **Forgetting that small samples can be imbalanced by chance.** Always check baseline balance even after a valid lottery.

## Practice and Application

1. **Balance check.** Using the Texas county panel, pretend you will randomize 254 counties into a "treatment" and "control" arm with Excel's `RAND()` function and a 0.5 cutoff. After assigning, use `AVERAGEIF` to compare median household income across your two random arms. Are they close? Repeat the randomization three times and comment on how much the balance varies sample to sample.
2. **ITT vs. ToT reasoning.** In the eviction trial, suppose 70% of the treatment arm attended mediation and the ITT effect is $-0.12$. Give an intuitive (back-of-envelope) estimate of the ToT effect, and explain in two sentences which number you would put in the executive summary and why.
3. **Attrition diagnosis.** You learn that 15% of the treatment arm and 30% of the control arm could not be located at follow-up. Explain how this pattern could bias the estimated effect, and state the direction of the likely bias.
4. **Spillover design.** The county worries that mediation changes landlord behavior toward *all* their tenants. Propose a randomization scheme that addresses this, and explain what you would now treat as the unit of analysis.
5. **Excel regression.** Build a 40-row mock dataset with `treat` and a continuous outcome (days housing was retained). Run the ToolPak Regression of the outcome on `treat`, and write one sentence interpreting the coefficient and its p-value for a non-technical reader.

## Transition to Chapter 11

The eviction trial answered *whether* the program works. The commissioners' next question is harder: *is it worth it?* Twelve fewer evictions per hundred filings is a real benefit, but mediation sessions, staff time, and rental assistance all cost money — and the benefits arrive over years while the costs are paid up front. Chapter 11 turns to cost-benefit and cost-effectiveness analysis, where we learn to put costs and benefits on a common footing, account for the time value of money, and decide whether a program that *works* is a program worth *funding*.
