---
layout: page
title: "Datasets"
permalink: /docs/datasets/
---

# Datasets for Evaluation Practice

The course follows **four real running cases**, and every worked example in this book uses real data. Two are Texas panels we built; two are landmark public-use evaluation datasets. All analysis is done in Microsoft Excel (enable the **Data Analysis ToolPak**).

## Case A — Texas City Finance Panel (2013–2024)
One row per city per year — **1,180 Texas cities**: sales-tax allocation, taxable sales, business outlets, local rate. Used for the **economic-development sales tax** case (Type A/B EDC adoption) — descriptive analysis, regression, difference-in-differences, cost-benefit. *(Real; shared with the PA 3311 course. To run the DiD, each city's tax-adoption year is added from the Texas Comptroller's local sales-tax-rate history.)*

## Case B — Texas County Political Panel (2000–2024)
One row per county per presidential election — **254 counties × 7 elections**: turnout, two-party vote share, income, poverty, education, race, metro status. Used for the **countywide vote-center** case — group comparisons, regression, difference-in-differences, interrupted time series. See its [codebook](https://github.com/scottlangford2/pa3311-textbook/blob/main/data/CODEBOOK_county_panel.md). *(Real; vote-center adoption year by county comes from the Texas Secretary of State.)*

## Case C — National Supported Work (NSW) Demonstration
The classic **randomized job-training experiment** (mid-1970s): disadvantaged workers randomly assigned to subsidized employment or control, with earnings before and after. We use it for the **workforce-training** case — the experiment, the famous selection-bias contrast, regression/matching, and cost-benefit.

- **Download (in this repo):** [`NSW_experimental.xlsx`]({{ '/data/NSW_experimental.xlsx' | relative_url }}) (445 rows — the randomized sample) · [CSV]({{ '/data/NSW_experimental.csv' | relative_url }}) · [`NSW_observational_cps.csv`]({{ '/data/NSW_observational_cps.csv' | relative_url }}) (program group + a non-experimental CPS comparison, for the selection-bias exercise) · [codebook]({{ '/data/NSW_codebook.md' | relative_url }}). Source: the Dehejia–Wahba public extract — [users.nber.org/~rdehejia/data](https://users.nber.org/~rdehejia/data/nswdata2.html).
- **Key real numbers:** experimental effect **+$1,794** (treated $6,349 vs. control $4,555); the naive observational comparison gives **−$8,498** (LaLonde 1986; Dehejia & Wahba 1999).

## Case D — Moving to Opportunity (MTO)
A real **HUD housing-voucher lottery** (1994–): public-housing families randomly assigned to a low-poverty-restricted voucher + counseling, a standard voucher, or control. We use it for the **housing-assistance / RCT** case — random assignment, intention-to-treat vs. treatment-on-the-treated, and cost-effectiveness.

- **Data (free public-use):** ICPSR Study **34563** (general-public access; ~3,300 adults) — [icpsr.umich.edu](https://www.icpsr.umich.edu/web/ICPSR/studies/34563). Export to CSV for Excel.
- **Key real findings:** children who moved young earned ~$3,477 (31%) more as adults vs. a $11,270 control mean (Chetty, Hendren & Katz 2016); adult mental-health gains (Kling, Liebman & Katz 2007).

## Bring-Your-Own Program Data
For the final project you may evaluate a program of your choosing using one of the datasets above or a public agency's data; we discuss sourcing and feasibility at the proposal stage.

> **A note on causal claims.** Cases A and B are observational panels; Cases C and D are randomized experiments. A central skill of this course is judging *how credibly* a given design and dataset support a causal claim — and stating the limits honestly. The NSW case makes the stakes vivid: the same data give +$1,794 with the experiment and −$8,498 without it.
