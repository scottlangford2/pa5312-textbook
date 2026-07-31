---
layout: page
title: "Datasets"
nav_label: "Data"
permalink: /docs/datasets/
---

# Datasets for Evaluation Practice

The course follows **five real running cases**, and every worked example in this book uses real data. Two are Texas panels we built; two are landmark public-use evaluation datasets; the fifth is a landmark small-N nonprofit program whose real published outcomes drive the exercises. All analysis is done in Microsoft Excel (enable the **Data Analysis ToolPak**).

> **Get the data and code — all public.** The two Texas panels (Cases A and B), with codebooks and sources, live in the public companion repository **[github.com/scottlangford2/pa3311-textbook/data](https://github.com/scottlangford2/pa3311-textbook/tree/main/data)**. This book's own source and the NSW files are in **[github.com/scottlangford2/pa5312-textbook](https://github.com/scottlangford2/pa5312-textbook)**. Cases C and D also link to their original public archives (NBER, ICPSR) below.

## Case A — Texas City Finance Panel (2013–2024)
One row per city per year — **1,180 Texas cities**: sales-tax allocation, taxable sales, business outlets, local rate. Used for the **economic-development sales tax** case (Type A/B EDC adoption) — descriptive analysis, regression, difference-in-differences, cost-benefit. *(Real; shared with the PA 3311 course. To run the DiD, each city's tax-adoption year is added from the Texas Comptroller's local sales-tax-rate history.)*

- **Download (public):** [`TX_City_Sales_Panel_2013_2024.xlsx`](https://github.com/scottlangford2/pa3311-textbook/raw/main/data/TX_City_Sales_Panel_2013_2024.xlsx) · [CSV](https://github.com/scottlangford2/pa3311-textbook/raw/main/data/TX_City_Sales_Panel_2013_2024.csv) · [codebook](https://github.com/scottlangford2/pa3311-textbook/blob/main/data/CODEBOOK.md) · [data sources](https://github.com/scottlangford2/pa3311-textbook/blob/main/data/DATA_SOURCES.md).

## Case B — Texas County Political Panel (2000–2024)
One row per county per presidential election — **254 counties × 7 elections**: turnout, two-party vote share, income, poverty, education, race, metro status. Used for the **countywide vote-center** case — group comparisons, regression, difference-in-differences, interrupted time series. **Download (public):** [`TX_County_Political_Panel_2000_2024.csv`](https://github.com/scottlangford2/pa3311-textbook/raw/main/data/TX_County_Political_Panel_2000_2024.csv) · [codebook](https://github.com/scottlangford2/pa3311-textbook/blob/main/data/CODEBOOK_county_panel.md) · [vote-center adoption](https://github.com/scottlangford2/pa3311-textbook/raw/main/data/vote_center_adoption.csv). *(Real. The panel now includes `vote_center_adopt_year` and a staggered, time-varying `vote_center` treatment indicator — the year each county joined the Texas Secretary of State's Countywide Polling Place Program, chained from the SoS §43.007(j) biennial reports — so the DiD and interrupted-time-series designs run on real adoption timing. 100 of 254 counties had adopted as of 2024.)*

## Case C — National Supported Work (NSW) Demonstration
The classic **randomized job-training experiment** (mid-1970s): disadvantaged workers randomly assigned to subsidized employment or control, with earnings before and after. We use it for the **workforce-training** case — the experiment, the famous selection-bias contrast, regression/matching, and cost-benefit.

- **Download (in this repo):** [`NSW_experimental.xlsx`]({{ '/data/NSW_experimental.xlsx' | relative_url }}) (445 rows — the randomized sample) · [CSV]({{ '/data/NSW_experimental.csv' | relative_url }}) · [`NSW_observational_cps.csv`]({{ '/data/NSW_observational_cps.csv' | relative_url }}) (program group + a non-experimental CPS comparison, for the selection-bias exercise) · [codebook]({{ '/data/NSW_codebook.md' | relative_url }}). Source: the Dehejia–Wahba public extract — [users.nber.org/~rdehejia/data](https://users.nber.org/~rdehejia/data/nswdata2.html).
- **Key real numbers:** experimental effect **+\$1,794** (treated \$6,349 vs. control \$4,555); the naive observational comparison gives **−\$8,498** (LaLonde 1986; Dehejia & Wahba 1999).

## Case D — Moving to Opportunity (MTO)
A real **HUD housing-voucher lottery** (1994–): public-housing families randomly assigned to a low-poverty-restricted voucher + counseling, a standard voucher, or control. We use it for the **housing-assistance / RCT** case — random assignment, intention-to-treat vs. treatment-on-the-treated, and cost-effectiveness.

- **Data (free public-use):** ICPSR Study **34563** (general-public access; ~3,300 adults) — [icpsr.umich.edu](https://www.icpsr.umich.edu/web/ICPSR/studies/34563). Export to CSV for Excel.
- **Key real findings:** children who moved young earned ~\$3,477 (31%) more as adults vs. a \$11,270 control mean (Chetty, Hendren & Katz 2016); adult mental-health gains (Kling, Liebman & Katz 2007).

## Case E — Perry Preschool (small nonprofit program)
A landmark **small-N nonprofit program evaluation**. From 1962 to 1967 the **HighScope Educational Research Foundation** — a nonprofit — ran a preschool in Ypsilanti, Michigan, for **123 low-income children** at high risk of school failure, **randomly assigning** them to a program group (n = 58) or a no-program comparison group (n = 65) and following them for decades. We use it for the **small-organization / grant-funded** case — needs assessment, process monitoring on a shoestring, small-sample impact inference, and the most famous cost-benefit result in the field. Its lesson is that rigor does not require a big budget or a big sample: with 123 children and mostly yes/no outcomes, two-proportion tests and a transparent cost-benefit calculation carried the day.

- **Data (real, published aggregates):** [`Perry_Preschool_outcomes.csv`]({{ '/data/Perry_Preschool_outcomes.csv' | relative_url }}) · [codebook]({{ '/data/Perry_Preschool_codebook.md' | relative_url }}). These are the real published outcome percentages (with the whole-child counts they imply for n = 58 and n = 65), taken from the official age-40 report. Participant-level records are restricted, so the file is aggregate, not microdata — the Excel exercises compute directly from the published cell values.
- **Key real numbers:** high-school graduation **65% vs. 45%**; earned \$20,000+ at age 40 **60% vs. 40%**; arrested five or more times **36% vs. 55%** (Schweinhart et al. 2005). Cost-benefit: about **\$16 returned per \$1 invested** to society (\$12.90 to the public), most of it from reduced crime; an independent reanalysis estimates a **7–10% annual social rate of return** (Heckman et al. 2010).
- **Want real downloadable microdata?** Use the **Carolina Abecedarian Project** — ICPSR / Child and Family Data Archive **Study 4091** ([icpsr.umich.edu](https://www.icpsr.umich.edu/web/ICPSR/studies/4091); free account, public-use files, n ≈ 111), a comparable small-N early-childhood experiment with a citable benefit-cost ratio of about 7.3 (García et al. 2020). It is the "download and clean a real archived file yourself" companion to Perry.

## Bring-Your-Own Program Data
For the final project you may evaluate a program of your choosing using one of the datasets above or a public agency's data; we discuss sourcing and feasibility at the proposal stage.

> **A note on causal claims.** Cases A and B are observational panels; Cases C, D, and E are randomized experiments (E on a very small sample). A central skill of this course is judging *how credibly* a given design and dataset support a causal claim — and stating the limits honestly. The NSW case makes the stakes vivid: the same data give +\$1,794 with the experiment and −\$8,498 without it. Case E makes a different point — a randomized design with only 123 children still produced credible, policy-moving evidence.
