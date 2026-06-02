---
layout: page
title: "Chapter 4"
permalink: /docs/chapter4/
---

# Measurement and Administrative Data

## Epigraphs

> "Not everything that can be counted counts, and not everything that counts can be counted."
> — William Bruce Cameron, *Informal Sociology* (1963)

> "The measure of a thing is never the thing itself."
> — paraphrase commonly used in measurement theory; treat it as a maxim, not a citation

## Opening Case: The Workforce Training "Completion Rate" in Central Texas

A workforce board serving Hays, Caldwell, and Comal counties runs a tuition-assistance program that pays for short-term credentials — commercial driver's licenses, welding certificates, certified nursing assistant coursework. The board's annual report to the state proudly lists a 91 percent "completion rate," and the executive director wants that number to anchor a request for expanded funding. Your evaluation team has been asked to verify it before the figure goes into a legislative briefing.

Within an afternoon of looking at the underlying records, the clean story dissolves. Some training providers report "completion" when a student finishes coursework; others report it only when the student passes the licensing exam; one community-college partner counts anyone who attended past the refund-deadline date. The denominator is murkier still: students who withdrew in the first two weeks were quietly dropped from the file before the rate was computed. And the field that is supposed to record credential attainment is blank for roughly a fifth of enrollees, because that information arrives from a separate state database on a lag.

The 91 percent is not a lie, exactly. It is the predictable result of stitching together administrative records that were built to run a program, not to evaluate it. Before this evaluation can say anything about whether the program *works*, it has to settle a more basic question: what, precisely, are we measuring, and how much can we trust the numbers we have?

**Guiding Questions**

- How do we move from an abstract concept ("training success") to a specific, defensible indicator we can put in a spreadsheet column?
- What makes a measure valid and reliable, and how would we know if ours is neither?
- When evaluation rides on administrative data we did not collect, what can go wrong — and how do we check for it before we trust it?

## Why This Chapter Matters

Every method in the rest of this course — group comparisons, regression, difference-in-differences — assumes you have already done the unglamorous work of this chapter well. A flawless statistical analysis of a badly measured outcome produces a precise, confident, wrong answer. In public administration this is not a hypothetical risk: most evaluations run on data that some agency generated for compliance, billing, or case management, then handed to you for a purpose it was never designed to serve. Learning to interrogate a measure before you analyze it is the difference between an evaluator and a calculator.

## From Concepts to Indicators: Operationalization

Evaluation questions arrive as concepts — *success*, *need*, *equity*, *fiscal stress*. None of these can be entered into a cell. **Operationalization** is the process of specifying the concrete, observable indicator that will stand in for the concept in your analysis. It is a series of choices, and each choice should be defended in writing.

Consider "voter engagement" in our Texas county panel. We cannot measure engagement directly, so we operationalize it as **turnout**, defined as ballots cast divided by some population base. But which base? Voting-age population, registered voters, or citizen voting-age population each yields a different denominator and a different number. A program that appears to boost turnout under one definition can appear to do nothing under another. The concept did not change; the operational definition did.

> **Briefing:** Operationalization is not a technicality you settle once. The choice of denominator, time window, and inclusion rule can move your headline number more than the program ever did.

A useful discipline is to write, for every outcome in your evaluation, a one-sentence operational definition that another analyst could follow to reproduce your column exactly. "Completion" in the opening case fails this test; "passed the state licensing exam within 180 days of course end, among enrollees who attended past the refund deadline" passes it.

## Validity and Reliability of Measures

Two properties separate a usable indicator from a misleading one.

**Construct validity** asks whether the indicator actually captures the concept it claims to. A high completion rate has poor construct validity for "workforce success" if completion is recorded before anyone gets a job. **Reliability** asks whether the indicator is consistent — whether the same case measured twice, or by two providers, yields the same value. The opening case has a reliability problem: three providers apply three different rules to the same word.

The two are distinct. A bathroom scale that always reads three pounds high is perfectly reliable and invalid. A measure can be reliable without being valid, but it cannot be valid without being reliable — noise in the indicator caps how well it can track the concept (Shadish, Cook & Campbell 2002).

> **Briefing:** Reliability is necessary but not sufficient for validity. Always check both. A consistent measure of the wrong thing is still the wrong thing.

A practical way to think about reliability is the idea that any observed score decomposes into a true value plus error:

$$X_{\text{observed}} = T_{\text{true}} + E_{\text{error}}$$

Reliability is the share of the variation in observed scores that reflects real differences rather than error:

$$\rho_{XX} = \frac{\sigma^2_T}{\sigma^2_T + \sigma^2_E}$$

When $\sigma^2_E$ is large — inconsistent reporting, sloppy data entry, definitional drift — reliability falls toward zero and the indicator becomes mostly noise.

## Levels of Measurement

The arithmetic you are allowed to do depends on the variable's level of measurement. Confusing these levels is one of the most common errors in student evaluations.

| Level | Meaning | Texas panel example | Legitimate operations |
|---|---|---|---|
| Nominal | Categories, no order | Metro status; county name | Counts, modes, proportions |
| Ordinal | Ordered categories, unequal gaps | Bond rating; survey "satisfaction" 1–5 | Median, percentiles |
| Interval | Equal gaps, no true zero | Year (2000, 2004, …) | Differences, means |
| Ratio | Equal gaps, true zero | Sales-tax revenue; population; turnout % | All arithmetic, ratios |

> **Briefing:** You can compute a mean of turnout (ratio) but not a meaningful mean of bond ratings (ordinal). Averaging "Aa1" and "Baa2" is a category error, even though Excel will happily return a number if you code them 1–10.

Most outcomes in our county and city panels are ratio-level, which is convenient — but several useful predictors (metro status, race categories) are nominal, and you will need to handle them as groups or indicator variables rather than as quantities.

## Choosing Outcome Measures for an Evaluation

A good outcome measure for an evaluation is **valid, reliable, sensitive to the program, available over the relevant period, and consistently defined across the units you compare**. The last two criteria are where administrative data most often fail.

Sensitivity matters because a program can only move an outcome that is close enough downstream to be affected within your study window. A job-training program might plausibly affect credential attainment within six months, employment within a year, and earnings within two — but lifetime earnings will not budge during a one-year evaluation, no matter how good the program is. Picking an outcome the program cannot move guarantees a null result that says nothing about the program.

## Administrative Data: Strengths and Pitfalls

Administrative data — records generated by the routine operation of a program or agency — are the workhorse of public-sector evaluation. The Comptroller's sales-tax allocations behind our city finance panel, the county vote canvasses behind the county panel, FEMA grant files, Medicaid claims: all are administrative. Their strengths are real. They cover entire populations rather than samples, they are inexpensive because the collection is already paid for, and they often span many years.

But they were collected to *run* the program, not to evaluate it, and that origin creates four recurring hazards.

**Coverage.** Who is *in* the data? The workforce file dropped early withdrawals before computing the rate; our city finance panel covers cities that levy a local sales tax and report to the Comptroller, which is not the same as "all Texas municipalities." Units missing from the file are invisible to your analysis and can bias it badly if their absence is related to the outcome.

**Definitional changes.** Administrative definitions change with statute, software, and staff. A poverty threshold is revised; a "case closure" reason gets a new code; the Census changes how it tabulates race. A jump in a time series may be a policy effect — or a redefinition. Always check whether a break in the data lines up with a known administrative change before you interpret it as a program effect.

> **Briefing:** Before treating any change over time as a finding, ask whether the *measurement* changed. Many "effects" in administrative time series are artifacts of redefinition.

**Missingness.** Records are blank for reasons that are rarely random. In the opening case, credential attainment was missing precisely for the most recent enrollees, because of reporting lag — so dropping missing rows would systematically exclude the newest cohort. Missingness that depends on the outcome is the dangerous kind.

**Error.** Free-text fields, fat-fingered entries, duplicate records, and impossible values (a city with negative sales-tax revenue, a turnout rate of 140 percent) are endemic. These are not rare edge cases; in a panel of 1,180 cities over twelve years you should *expect* them and screen for them.

## Data Quality and Cleaning

Cleaning is not a chore that precedes the "real" analysis; it is part of the analysis, and it should be documented so a skeptic can retrace it. A disciplined first pass screens every variable for range, missingness, duplicates, and definitional consistency before a single statistic is computed.

### Worked Example: Screening the City Finance Panel in Excel

Suppose you have the Texas city finance panel open, with one row per city-year and columns including `city`, `year`, and `sales_tax_rev`. You want to screen `sales_tax_rev` for quality before using it.

**1. Range and impossible values.** Find the extremes with `=MIN(D2:D14162)` and `=MAX(D2:D14162)`. A negative minimum is impossible for revenue and flags an error. Count suspicious zeros with `=COUNTIF(D2:D14162,0)` — a true zero (no sales tax) is plausible for some cities but a sudden zero in one year of an otherwise-reporting city is likely missing data miscoded.

**2. Missingness.** Count blanks with `=COUNTBLANK(D2:D14162)`, then compute the missing rate as that count divided by `=COUNTA(A2:A14162)`. Use a PivotTable with `year` in Rows and a count of blanks to check whether missingness clusters in recent years — the reporting-lag pattern from the opening case.

**3. Duplicates.** Build a key with `=A2&"_"&B2` (city and year) in a helper column, then `=COUNTIF($E$2:$E$14162,E2)`. Any value above 1 means a city-year appears twice — a duplicate to investigate, not silently sum.

**4. A cleaning log.** Record every decision in a separate sheet so the cleaning is reproducible.

| Check | Excel function | Finding | Action |
|---|---|---|---|
| Minimum value | `MIN` | −4,200 (one city, 2017) | Flag; trace to source; treat as missing |
| Missing rate | `COUNTBLANK`/`COUNTA` | 6.2% overall, 18% in 2024 | Note reporting lag; exclude 2024 or footnote |
| Duplicate keys | `COUNTIF` on city_year | 11 duplicate city-years | Investigate; keep most recent record |
| Zero values | `COUNTIF(...,0)` | 240 zeros | Verify which are true no-tax cities |

> **Returning to the Case:** The workforce board's 91 percent fails almost every screen in this chapter. Its outcome (coursework completion) has weak construct validity for "workforce success"; its reliability is undermined by three providers using three definitions; its denominator suffers a coverage problem from dropped withdrawals; and its key field has 20 percent non-random missingness. Your briefing should not report a corrected single number — it should report a defensible operational definition, the rate computed under that definition with missingness disclosed, and a recommendation that providers adopt a common reporting standard. That is a more useful deliverable than any single percentage.

## Common Pitfalls

- **Analyzing before defining.** Computing statistics on a column you cannot define in one sentence. Write the operational definition first.
- **Treating a reliable measure as valid.** Consistency is not correctness; a measure can be precisely wrong.
- **Doing arithmetic the measurement level forbids.** Averaging ordinal codes (bond ratings, Likert items treated as raw categories) as if they were ratio quantities.
- **Trusting administrative totals at face value.** Headline rates often hide denominator manipulation, coverage gaps, and definitional drift.
- **Dropping missing rows reflexively.** Listwise deletion is fine only when data are missing at random — which administrative missingness usually is not.
- **Interpreting a redefinition as a finding.** A break in a time series may be a coding change, not a program effect.

## Practice and Application

1. **Operationalize a concept.** For the county panel, write three competing operational definitions of "voter engagement" (e.g., different turnout denominators). Compute each in Excel for Travis and Hays counties in 2020 and explain in a paragraph how the choice of definition could change an evaluation's conclusion.

2. **Validity and reliability.** A school district claims its "college readiness index" measures readiness. List two threats to its construct validity and one threat to its reliability, and propose one check for each.

3. **Levels of measurement.** Classify five variables from the city finance panel by level of measurement. For each, state one statistic that is legitimate and one that is not.

4. **Screen a variable.** Using the city finance panel, screen `taxable_sales` for range, missingness, and duplicates using `MIN`, `MAX`, `COUNTBLANK`, `COUNTA`, and `COUNTIF`. Produce a four-row cleaning log like the worked example.

5. **Spot the redefinition.** Suppose median household income in the county panel jumps sharply in one year for many counties at once. Describe how you would determine whether this is a real economic shift or a measurement change, and what evidence would distinguish the two.

## Transition to Chapter 5

You now have indicators you can defend and data you have screened. The next question is what those numbers actually look like. Before any comparison or model, a competent evaluator describes the data — its center, its spread, its outliers, and whether the groups being compared even started in the same place. Chapter 5 turns to describing and presenting data for decision-makers, building the tables and charts in Excel that make an evaluation legible to the people who must act on it.
