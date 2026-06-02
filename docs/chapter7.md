---
layout: page
title: "Chapter 7"
permalink: /docs/chapter7/
---

# Regression for Evaluation

## Epigraphs

> "All models are wrong, but some are useful."
> — George E. P. Box

> "Empirical work in economics is like detective work."
> — Joshua Angrist and Jörn-Steffen Pischke, *Mostly Harmless Econometrics* (2009)

## Opening Case: A Workforce Training Program in the Rio Grande Valley

The Lower Rio Grande Valley Workforce Development Board has spent three years offering a short-term credential program for adults in the manufacturing and logistics trades. The program is voluntary: residents hear about it through community colleges, public libraries, and word of mouth, then enroll if they choose. The board's executive director wants to report to its funders whether the program "works" — specifically, whether completing it raises a participant's annual earnings.

A first-year analyst pulls the records and computes a simple comparison. The average earnings of people who completed the program is about \$8,200 higher than the average earnings of people in the same counties who did not enroll. The director is delighted and drafts a press release claiming the program "boosts earnings by more than eight thousand dollars a year." You are asked to review the draft before it goes out.

You hesitate. The people who enrolled were not chosen at random. They tended to be younger, more likely to already hold a high-school diploma, and more motivated to seek out new work — exactly the kinds of people who might earn more *regardless* of the program. The eight-thousand-dollar gap mixes the effect of the program together with the effect of who chose to enroll. Before you can say anything credible about the program's effect, you need a way to compare participants and non-participants *as if* they were similar on these background characteristics. Regression is the workhorse tool for doing exactly that.

**Guiding Questions**

- What does it mean to "control for" a variable, and how does covariate adjustment change an estimated program effect?
- How do we use a dummy variable for treatment inside a regression to estimate an adjusted effect?
- Why is regression adjustment *not* the same thing as a randomized experiment, and what is omitted-variable bias?

## Why This Chapter Matters

Most program data you will ever encounter come from the world as it is, not from a controlled experiment. People select into programs; agencies target services to the neediest or the most promising; policies roll out where the politics allow. In all of these situations, the groups you are comparing differ in ways that have nothing to do with the program itself. Regression is the most common, most flexible, and most misunderstood tool for handling that problem. Used carefully, it lets you estimate a program effect that is adjusted for measured differences between groups. Used carelessly, it produces confident numbers that are simply wrong. This chapter builds the tool from the ground up and is equally clear about where it stops.

## From the Regression Line to Multiple Regression

### The Simple Regression Line

Start with one outcome and one predictor. Suppose $Y$ is a county's voter turnout rate and $X$ is its median household income. The simple linear regression model is

$$ Y_i = \beta_0 + \beta_1 X_i + \varepsilon_i $$

where $i$ indexes counties, $\beta_0$ is the **intercept**, $\beta_1$ is the **slope**, and $\varepsilon_i$ is the error term capturing everything about turnout that income does not explain. Ordinary least squares (OLS) chooses the line that minimizes the sum of squared vertical distances between each point and the line:

$$ \min_{\beta_0,\beta_1} \sum_{i=1}^{n} \left( Y_i - \beta_0 - \beta_1 X_i \right)^2 $$

The **slope** $\beta_1$ is the heart of the interpretation: a one-unit increase in $X$ is associated with a $\beta_1$-unit change in $Y$, on average. The **intercept** $\beta_0$ is the predicted value of $Y$ when $X = 0$ — sometimes meaningful, often just a mathematical anchor.

> **Briefing:** A regression slope is a comparison of conditional means. "For counties that differ by \$10,000 in median income, predicted turnout differs by $10{,}000 \times \beta_1$" is the honest way to read it — an association, not yet a cause.

### Goodness of Fit: R-squared

How much of the variation in $Y$ does the line capture? The coefficient of determination is

$$ R^2 = 1 - \frac{\sum_i (Y_i - \hat{Y}_i)^2}{\sum_i (Y_i - \bar{Y})^2} $$

where $\hat{Y}_i$ is the predicted value and $\bar{Y}$ is the sample mean. $R^2$ ranges from 0 to 1 and reports the share of the variance in the outcome explained by the model. A high $R^2$ does not mean you have found a causal effect, and a low $R^2$ does not mean your estimated effect is wrong. For evaluation, the slope on the treatment variable matters far more than the overall fit.

### Multiple Regression and "Controlling For"

Now add more predictors. With $k$ regressors,

$$ Y_i = \beta_0 + \beta_1 X_{1i} + \beta_2 X_{2i} + \cdots + \beta_k X_{ki} + \varepsilon_i $$

The interpretation of each slope changes in a crucial way. Each $\beta_j$ now measures the association between $X_j$ and $Y$ **holding the other variables fixed**. This is what "controlling for" means: $\beta_1$ describes how $Y$ differs across units that have the same values of $X_2, \ldots, X_k$ but differ in $X_1$. Algebraically, multiple regression first strips out the part of $X_1$ that the other regressors can explain, and relates only the leftover variation to $Y$. That is why we say the effect is "net of" or "adjusted for" the controls.

> **Briefing:** "Controlling for" a variable means comparing units that look the same on that variable. It removes the part of the group difference that is explained by the measured controls — and only the part that is measured.

## Estimating a Program Effect with a Treatment Dummy

To turn regression into an evaluation tool, define a **treatment indicator** (dummy variable) $D_i$ that equals 1 if unit $i$ received the program and 0 otherwise. The model becomes

$$ Y_i = \beta_0 + \tau D_i + \beta_1 X_{1i} + \cdots + \beta_k X_{ki} + \varepsilon_i $$

The coefficient $\tau$ on the treatment dummy is the **adjusted program effect**: the average difference in the outcome between treated and untreated units that have the same values of the control variables $X_1, \ldots, X_k$. Without controls, $\tau$ would simply reproduce the raw difference in means. With controls, $\tau$ answers a sharper question: among units that look alike on the things we measured, how much higher is the outcome for the treated group?

> **Briefing:** The treatment dummy's coefficient $\tau$ is your headline number. Report it with its standard error, and always say which covariates it is adjusted for — the adjustment set defines what the estimate means.

## Worked Example: Adjusted Program Effect in the County Panel

Suppose the state piloted a county-level civic-engagement grant in a subset of Texas counties, and we want its association with voter turnout in the 2020 election, adjusting for income and education. We use the **Texas County Panel**, filtered to the 2020 cross-section. Lay the data out in columns: column A `turnout` (the outcome $Y$), column B `grant` (the treatment dummy $D$, 1/0), column C `median_income` (in \$1,000s), column D `pct_ba` (percent with a bachelor's degree).

Enable the **Analysis ToolPak** (File → Options → Add-ins → Manage Excel Add-ins → Go → check *Analysis ToolPak*). Then choose **Data → Data Analysis → Regression**. Set the *Input Y Range* to the `turnout` column (including the header) and the *Input X Range* to the three columns B:D together (the X variables must be contiguous). Check *Labels*, check *Confidence Level 95%*, and choose an output cell. Excel returns a regression table. The key portion looks like this (illustrative layout, not real estimates):

| Term | Coefficient | Std. Error | t Stat | P-value |
|---|---|---|---|---|
| Intercept | 41.2 | 3.10 | 13.3 | 0.000 |
| grant ($\tau$) | 2.8 | 1.05 | 2.67 | 0.008 |
| median_income | 0.31 | 0.07 | 4.43 | 0.000 |
| pct_ba | 0.45 | 0.12 | 3.75 | 0.000 |

Read the `grant` row: the coefficient $\tau$ is the estimated turnout difference between grant and non-grant counties *after* adjusting for income and education. The *P-value* tests whether that coefficient differs from zero. The *Regression Statistics* block at the top reports `R Square`; the *Significance F* in the ANOVA block tests the whole model. You would describe the result as: "Holding median income and education constant, grant counties had turnout about 2.8 percentage points higher, an estimate distinguishable from zero at conventional levels."

To verify Excel's slope by hand for a single regressor, recall that $\hat{\beta}_1 = \text{SLOPE}(Y\text{-range}, X\text{-range})$ and $\hat{\beta}_0 = \text{INTERCEPT}(Y\text{-range}, X\text{-range})$ reproduce the ToolPak's simple-regression coefficients exactly. `=RSQ(Y,X)` returns the simple $R^2$.

> **Returning to the Case:** Re-run the workforce analysis as a regression of earnings on the enrollment dummy plus age, prior education, and prior-year earnings. The eight-thousand-dollar raw gap will almost certainly shrink once you adjust for who enrolled. The adjusted coefficient is a far more defensible headline — but, as the next section warns, it is still not proof.

## Omitted-Variable Bias: Why Adjustment Is Not an Experiment

Regression controls only for variables you actually include. Anything that (a) affects the outcome and (b) differs systematically between treated and untreated units, but is left out of the model, contaminates the treatment coefficient. This is **omitted-variable bias (OVB)**. Formally, if the true model includes an omitted variable $W$ with coefficient $\gamma$, and you leave it out, the expected value of your treatment estimate is

$$ E[\hat{\tau}] = \tau + \gamma \, \delta $$

where $\delta$ is the slope from regressing the omitted $W$ on the treatment $D$ (and the included controls). The bias term $\gamma\,\delta$ vanishes only if the omitted variable does not affect the outcome ($\gamma = 0$) or is unrelated to treatment given the controls ($\delta = 0$). In the workforce case, *motivation* is the classic culprit: it raises earnings ($\gamma > 0$) and is higher among those who enroll ($\delta > 0$), so leaving it out pushes the estimated effect upward.

> **Briefing:** The sign of omitted-variable bias is the sign of $\gamma \times \delta$. Ask of any leftover variable: does it raise the outcome, and is it more common in the treated group? If both point the same way, your estimate is biased upward.

This is the deep reason regression adjustment is not equivalent to a randomized experiment. Randomization makes the treated and untreated groups statistically identical on *everything* — measured and unmeasured — so there are no systematically omitted variables. Regression can only balance the variables you can name and measure. Motivation, latent health, local economic shocks, and unrecorded eligibility rules all remain potential confounders. Shadish, Cook, and Campbell (2002) call this the central trade-off of observational work: you can adjust for what you observe, but you must argue, not assume, that nothing important is left out.

## Common Pitfalls

- **Treating $R^2$ as a measure of causal success.** A model can have a high $R^2$ and a hopelessly biased treatment coefficient. Judge the design, not the fit.
- **Controlling for a post-treatment variable.** If a control is itself affected by the program (a "bad control"), adjusting for it can absorb part of the very effect you are trying to measure. Use only covariates measured *before* treatment.
- **Reading the intercept as meaningful when $X=0$ is impossible.** A predicted turnout "at zero income" is a mathematical artifact, not a real county.
- **Putting non-contiguous X columns into the ToolPak.** Excel requires the X variables to sit in adjacent columns; rearrange your sheet first or the regression will silently use the wrong data.
- **Claiming causation from adjustment alone.** "Controlling for" is not "holding constant in an experiment." State explicitly which confounders you could *not* address.

## Practice and Application

1. **Simple regression by hand and by ToolPak.** In the county panel's 2020 cross-section, regress `turnout` on `median_income` using both `=SLOPE()`/`=INTERCEPT()` and the Data Analysis ToolPak. Confirm the coefficients match, and interpret the slope in one sentence.
2. **Adding a control.** Add `pct_ba` to the model from Exercise 1. Report how the income slope changes and explain, in terms of "controlling for," why it moved.
3. **Treatment dummy.** Create a dummy equal to 1 for counties above the median in `pct_ba` and 0 otherwise (a stand-in "treatment"). Regress turnout on the dummy alone, then add income and population as controls. Report the adjusted coefficient and its P-value.
4. **OVB reasoning.** For the workforce case, name two plausible omitted variables. For each, state the likely sign of $\gamma$ and of $\delta$, and therefore the direction of the bias.
5. **Writing it up.** In 150 words, write the methods note you would attach to the executive director's revised press release, stating the adjusted estimate and the limits of the design honestly.

## Transition to Chapter 8

Regression with controls is the best you can do when your only leverage is the variables you happened to measure. But there is a more powerful idea: if you can find a comparison group that, by the structure of how a policy rolled out, plausibly stands in for what the treated group *would have done* in the absence of the program, you can defend a causal claim far more credibly. Chapter 8 turns to quasi-experimental designs — pre/post comparisons, nonequivalent comparison groups, and the difference-in-differences strategy — that exploit the timing and geography of real Texas policy changes to get closer to the experimental ideal without a randomized trial.
