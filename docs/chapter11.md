---
layout: page
title: "Chapter 11"
permalink: /docs/chapter11/
---

# Cost-Benefit and Cost-Effectiveness Analysis

## Epigraphs

> "Cost-benefit analysis is a method of assessing the desirability of projects when it is important to take a long view and a wide view."
> — Anthony Boardman, David Greenberg, Aidan Vining, and David Weimer, *Cost-Benefit Analysis: Concepts and Practice*

## Opening Case: A Library Early-Literacy Program in McAllen

The McAllen Public Library, with support from the city council, runs a "Books from Birth" early-literacy program: every child registered before age one receives a free book each month and an invitation to weekly story-time sessions. The program has been running for three years, and an evaluation modeled on Chapter 10 found a credible, modest improvement in kindergarten-readiness scores among participating children.

The council is pleased but not satisfied. The city manager points out that demonstrating an *effect* is not the same as demonstrating *value*. The program costs real money — books, a part-time coordinator, room rental, mailing — and that money could instead extend bus routes or repair sidewalks. The council wants to know whether the dollars spent on early literacy buy more for the city than the same dollars spent elsewhere, and whether the long-run benefits (children who read sooner, do better in school, and eventually earn more) justify the up-front cost.

You are asked to prepare a cost-benefit analysis. Immediately you face two challenges. First, some benefits are easy to monetize (reduced grade-retention costs) while others are not (a parent's joy, a child's curiosity). Second, the costs land now but the benefits unfold over fifteen years — and a dollar fifteen years from now is not worth a dollar today.

**Guiding Questions**

- Which costs and benefits belong in the analysis, and how do we attach dollar values to them honestly?
- Why must we *discount* future dollars, and how do Net Present Value and the benefit-cost ratio summarize a program's worth?
- When benefits resist monetization, how does cost-effectiveness analysis still let us compare programs?

## Why This Chapter Matters

Public budgets are zero-sum in the short run: a dollar spent on early literacy is a dollar not spent on something else. Cost-benefit analysis (CBA) is the discipline of making that trade-off explicit and defensible. It forces an evaluator to inventory *all* consequences of a program, value them in common units, and confront the awkward fact that timing matters. Done well, CBA is among the most persuasive products an evaluator can hand a city council. Done carelessly — with cherry-picked benefits or a self-serving discount rate — it is among the easiest to manipulate. This chapter teaches both the mechanics and the honesty that must accompany them.

## Identifying and Valuing Costs and Benefits

The first task is an inventory. List every consequence of the program for every party with **standing** (whose welfare counts — usually the city's residents, sometimes a broader public).

**Costs** include the obvious *direct* outlays (books, salaries, rent) and the easily forgotten ones: the *opportunity cost* of resources already owned (the meeting room could have been rented out), and volunteer or participant time. A common error is to count only what shows up on an invoice.

**Benefits** are the program's valued effects. Some are *market* benefits with observable prices — fewer children held back a grade saves a measurable per-pupil cost. Others are *non-market* benefits requiring valuation techniques: willingness-to-pay surveys, or transferring values estimated elsewhere (*benefit transfer*).

> **Briefing:** Count opportunity costs, not just cash outlays — and count a benefit once. Double-counting (e.g., adding both higher test scores *and* the future earnings those scores produce, when one causes the other) inflates the case.

Avoid counting *transfers* — pure redistributions like a subsidy that takes a dollar from taxpayers and hands it to a family — as net social benefits. From the city's whole-community perspective, a transfer nets to zero; only real changes in resources count.

## The Time Value of Money: Discounting and NPV

A benefit received in year 10 is worth less than the same benefit today, because today's dollar could be invested and grow. To compare costs and benefits arriving in different years, we *discount* each future amount back to its present value using a discount rate $r$. The present value of an amount $B_t$ received in year $t$ is:

$$PV = \frac{B_t}{(1+r)^t}$$

The **Net Present Value** of a program with net benefits $NB_t = B_t - C_t$ in each year $t$ from $0$ to $T$ is:

$$NPV = \sum_{t=0}^{T} \frac{B_t - C_t}{(1+r)^t}$$

> **Briefing:** The decision rule is simple — undertake the program if $NPV > 0$, and when ranking competing programs under a fixed budget, prefer higher NPV.

A related summary is the **benefit-cost ratio (BCR)**, the present value of benefits divided by the present value of costs:

$$BCR = \frac{\sum_{t=0}^{T} B_t / (1+r)^t}{\sum_{t=0}^{T} C_t / (1+r)^t}$$

A program is worthwhile when $BCR > 1$. NPV tells you the *magnitude* of net value; BCR tells you the value *per dollar spent*. They can disagree when ranking: a large program may have a higher NPV but a lower BCR than a small, efficient one. For a fixed budget, BCR helps you squeeze the most value per dollar; for an absolute go/no-go decision, NPV is the cleaner guide.

The discount rate $r$ is the most contested input. A higher rate punishes distant benefits more harshly — bad news for programs like early literacy whose payoffs are decades out. There is no single "correct" rate, which is precisely why we test several (below).

## Cost-Effectiveness Analysis When Benefits Resist Dollars

Sometimes the central benefit cannot be credibly monetized — and forcing a dollar figure onto "kindergarten readiness" or "a life saved" can do more to discredit an analysis than to advance it. **Cost-effectiveness analysis (CEA)** sidesteps monetization. It expresses cost per unit of a *natural* outcome:

$$CER = \frac{\text{Present value of costs}}{\text{Units of effect}}$$

For Books from Birth, the cost-effectiveness ratio might be "dollars per additional child reading at grade level." CEA cannot tell you whether a program is worth doing in the abstract, but it is powerful for *comparing* programs that share an outcome: if a competing summer-reading program achieves the same readiness gain at half the cost per child, CEA makes that visible even though neither benefit was ever priced in dollars.

> **Briefing:** Use CEA when the key benefit is real but cannot be honestly monetized; it ranks programs sharing a common outcome, but it cannot declare a single program "worth it" on its own.

## Sensitivity Analysis

Every CBA rests on assumptions: the discount rate, the size of the effect, how long benefits persist, the dollar value of each benefit. Sensitivity analysis asks how the conclusion changes when those assumptions change. The simplest form varies one input at a time — recomputing NPV across a range of discount rates. A *break-even* analysis finds the assumption value at which NPV hits zero (e.g., "the program pays off as long as the discount rate stays below 9%"). Honest sensitivity analysis is what separates a persuasive CBA from a sales pitch.

> **Briefing:** A finding that survives a wide range of reasonable assumptions is credible; one that flips when the discount rate moves a point or two should be reported as fragile.

### Worked Example: Books from Birth in Excel

We model the program over six years. Costs are concentrated early (setup plus annual operations); benefits (avoided grade-retention costs and a conservative monetized readiness gain) build as the cohort ages. All figures are in thousands of dollars. We lay out one column per year in Excel.

| Year $t$ | Costs $C_t$ | Benefits $B_t$ | Net $NB_t$ |
|---|---|---|---|
| 0 | 120 | 0 | $-120$ |
| 1 | 90 | 30 | $-60$ |
| 2 | 90 | 70 | $-20$ |
| 3 | 90 | 110 | 20 |
| 4 | 90 | 150 | 60 |
| 5 | 90 | 180 | 90 |

**Step 1 — Lay out the cash flows.** Put years in row 1, costs in row 2, benefits in row 3, and net benefits in row 4 with `=B3-B2` dragged across.

**Step 2 — Compute NPV.** Excel's `NPV` function discounts a stream *beginning one period in the future*, so it must not include the year-0 value inside the function — add year 0 separately. With the rate in cell `B7` (say 5%) and net benefits in `C4:G4` for years 1–5 and year 0 in `B4`:

`=B4 + NPV(B7, C4:G4)`

**Step 3 — Compute the BCR.** Discount benefits and costs separately. Present value of benefits: `=B3 + NPV(B7, C3:G3)`; present value of costs: `=B2 + NPV(B7, C2:G2)`; then `BCR = PV_benefits / PV_costs`.

**Step 4 — Sensitivity table.** Build a one-variable **Data Table** (Data ▸ What-If Analysis ▸ Data Table) that recomputes NPV as the discount rate runs from 2% to 12%. List the rates down a column, point the table at your NPV formula, and Excel fills in the NPV at each rate in one step.

| Discount rate $r$ | NPV (\$000) |
|---|---|
| 2% | 8 |
| 5% | $-12$ |
| 8% | $-29$ |
| 12% | $-48$ |

At a low discount rate the program clears the bar; at higher rates its distant benefits are discounted too heavily to cover the early costs. The break-even rate lies near 3%.

> **Returning to the Case:** You can tell the McAllen council that Books from Birth is a *net positive investment only if the city uses a relatively low discount rate* — defensible for a public program whose beneficiaries are children. At a 5% rate the NPV is slightly negative on these conservative figures, and the BCR hovers near 1. Rather than overstate the case, you report the break-even discount rate and note that benefits you could *not* monetize (parental engagement, library foot traffic) would push the true value upward. If the council prefers to avoid pricing childhood literacy at all, you offer the cost-effectiveness number — dollars per additional kindergarten-ready child — and let them compare it against the sidewalk and bus-route alternatives directly.

## Common Pitfalls

- **Ignoring the time value of money.** Summing undiscounted costs and benefits across years overstates programs whose payoffs are far off.
- **Counting transfers as benefits.** A subsidy moving money from one resident to another is not a net social gain.
- **Double-counting.** Adding both an intermediate outcome and the final outcome it produces inflates benefits.
- **Cherry-picking the discount rate.** Choosing the rate that makes your program look best, without disclosing the sensitivity, is advocacy, not analysis.
- **Omitting opportunity costs.** "Free" donated space or volunteer time still has a value that belongs in the cost column.
- **Forcing monetization where it isn't credible.** A made-up dollar value for an intangible can discredit an otherwise sound analysis; CEA is often the more honest tool.

## Practice and Application

1. **Build the NPV model.** Recreate the Books from Birth table in Excel and compute NPV at 5% using `=B4 + NPV(B7, C4:G4)`. Confirm your number matches the worked example, then change a single benefit figure and watch the NPV update.
2. **Benefit-cost ratio.** Using the same spreadsheet, compute the BCR at 5% by discounting benefits and costs separately. Interpret in one sentence what a BCR of, say, 0.97 means for the council's decision.
3. **Sensitivity Data Table.** Build a one-variable Data Table varying the discount rate from 1% to 15%. Identify the break-even rate (where NPV crosses zero) and write two sentences on what that implies about the program's robustness.
4. **Cost-effectiveness.** Suppose Books from Birth produces 40 additional kindergarten-ready children per cohort and a rival summer program produces 25 at a lower total cost. Compute each program's cost per additional ready child and state which is more cost-effective and why CEA, not CBA, was the right tool here.
5. **City finance application.** Using the Texas city finance panel, propose a small local program (e.g., a downtown facade-improvement grant) whose benefits show up as higher future sales-tax revenue. Sketch a five-year cost-benefit table, name the discount rate you would use, and explain one benefit you would *not* attempt to monetize.

## Transition to Chapter 12

You now have a verdict for McAllen: a program that works, with a value that depends visibly on the assumptions you chose. The final task is the one that determines whether any of this analysis matters — communicating it. A correct NPV buried in a confusing memo persuades no one, and a confident claim that hides its own uncertainty is a breach of professional ethics. Chapter 12 turns to the evaluation report: how to structure findings for busy decision-makers, how to report uncertainty and threats to validity honestly, how to visualize results for non-technical audiences, and how to use new tools — including AI — responsibly without ever surrendering your own judgment.
