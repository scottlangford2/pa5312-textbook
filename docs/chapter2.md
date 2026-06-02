---
layout: page
title: "Chapter 2"
permalink: /docs/chapter2/
---

# Program Theory and Logic Models

## Epigraphs

> "There is nothing so practical as a good theory."
> — Kurt Lewin, *Field Theory in Social Science* (1951)

> "Programs are theories. Evaluation is the test of those theories."
> — paraphrasing Carol H. Weiss, *Evaluation* (1998), on theory-based evaluation

## Opening Case: A Summer Youth Jobs Program in San Antonio

Suppose the city of San Antonio launches a summer youth employment program. Using city funds and a federal workforce grant, it places 1,500 teenagers from low-income neighborhoods in six-week paid jobs with local employers and nonprofits, pairs each with an adult mentor, and runs a weekly two-hour "work readiness" workshop. The stated goals are ambitious: keep teens productively occupied over the summer, build job skills and work habits, raise high-school graduation rates, and — in the language of the grant — "reduce involvement with the justice system."

The program runs smoothly. Teens show up, employers are satisfied, the workshops are well attended. But when the city's budget office asks the program team to explain *how* a six-week summer job is supposed to raise graduation rates a year later or reduce justice involvement, the answers become vague. Some staff say the paycheck matters most; others point to the mentor; others to the workshops. No one can say which activities drive which outcomes, or how. And because no one wrote down the chain of reasoning in advance, the program collected attendance logs and payroll records but almost no data on the outcomes it actually promised.

This is a *program theory* problem before it is a data problem. The program has activities and hopes, but no explicit account linking them. Our task in this chapter is to make that account explicit — to build a logic model — and then to read the program's evaluation questions and indicators directly off of it.

**Guiding Questions**

- What is the implicit chain of cause and effect connecting a summer paycheck to a graduation rate?
- Which links in that chain are plausible, and which are heroic assumptions?
- What should the program have been measuring, and where in the chain does each measure belong?

## Why This Chapter Matters

Every program rests on a theory — a set of beliefs about why the planned activities should produce the desired results. Usually that theory is implicit, scattered across grant applications and staff intuition. Making it explicit is the single most valuable thing an evaluator can do early, because the theory determines *what questions to ask, what to measure, and how to interpret results.* A logic model is the standard tool for surfacing program theory. It is not paperwork; it is the blueprint that tells you where to point your instruments.

> **Briefing:** A logic model makes a program's implicit theory explicit, and that explicit theory dictates the evaluation's questions, indicators, and design.

## Program Theory and the Theory of Change

*Program theory* is the model of how and why a program is supposed to work. It has two interlocking parts. The *theory of change* (sometimes called the *impact theory*) is the causal story: the sequence of changes by which the program's activities are expected to produce its ultimate outcomes. The *theory of action* (or *process theory*) is the operational story: how the program will be organized and delivered to set that causal sequence in motion.

For the youth program, a theory of change might run: a paid summer job gives a teen income and structured time, which reduces idle hours and exposure to risk; the work experience plus mentoring builds work habits and a sense of efficacy; these in turn improve school engagement, which raises the odds of graduation; and being employed and mentored reduces opportunities and incentives for justice involvement. Every "which" and "in turn" in that sentence is a causal claim — and a place the chain could break.

> **Briefing:** State the theory of change as a sequence of explicit "if–then" links; each link is a testable claim, and the weakest link caps the whole program's plausibility.

## The Logic-Model Chain

A logic model lays the program theory out as a left-to-right chain of five linked elements.

- **Inputs** — the resources invested: funding, staff, employer partnerships, the federal grant, mentor volunteers.
- **Activities** — what the program does with those inputs: recruit teens, place them in jobs, run workshops, match mentors.
- **Outputs** — the direct, countable products of the activities: number of teens placed, job-hours worked, workshops delivered, mentor matches made.
- **Outcomes** — the changes in participants the program seeks, usually layered by time horizon. *Short-term* outcomes (work habits, efficacy, skills) plausibly occur during or just after the program; *intermediate* outcomes (school engagement, attendance) over the following year.
- **Impacts** — the long-term, often population-level changes the program ultimately aims at: graduation, reduced justice involvement, lifetime earnings.

The convention is that inputs and activities are within the program's control; outputs are largely within its control; outcomes and impacts are progressively *less* controllable because they depend on the world cooperating with the program's theory. The further right you move, the stronger the assumptions and the longer the causal distance between what the program does and what it hopes to achieve.

> **Briefing:** Inputs → activities → outputs → outcomes → impacts. Control decreases and assumption-burden increases as you move rightward.

### Assumptions and External Factors

Two elements are easy to omit and dangerous to ignore. *Assumptions* are the beliefs that must hold for one box to lead to the next — for example, that local employers will provide genuinely developmental work rather than busywork, or that six weeks is long enough to change habits. *External factors* are forces outside the program that affect outcomes regardless of program activity: the summer labor market, school district policies, neighborhood conditions. A good logic model names these in the margins, because they are exactly what an impact evaluation must rule out as alternative explanations.

## From Logic Model to Evaluation Questions and Indicators

The payoff of a logic model is that evaluation questions fall out of it almost mechanically. Each link in the chain suggests a question, and each box suggests an *indicator* — an observable, measurable signal of that box.

- The **inputs-to-activities** link asks process questions: were the resources delivered and the activities carried out as planned? Indicators: dollars spent, staff hired, partnerships signed.
- The **activities-to-outputs** link asks reach and dosage questions: did the program serve the intended people at the intended intensity? Indicators: teens placed, average job-hours, workshop attendance.
- The **outputs-to-outcomes** links ask outcome questions: did short-term changes occur? Indicators: a pre/post work-readiness assessment, attendance the following fall, a self-efficacy scale.
- The **outcomes-to-impacts** links ask impact questions: did the ultimate goals move, and *because of the program*? Indicators: graduation, justice-system contact — measured against a comparison group, since these are heavily shaped by external factors.

Notice how this exposes the San Antonio program's failure: it measured the left side of the chain (attendance, payroll = inputs, activities, outputs) and almost none of the right side (the outcomes and impacts it promised). The logic model would have flagged that gap before the program collected a single record.

> **Briefing:** Read evaluation questions off the *links* and indicators off the *boxes*; a box with no planned indicator is a promise you cannot keep.

## Common Logic-Model Errors

Building the model surfaces predictable mistakes. A *missing link* leaps from an early box to a distant impact with no intermediate mechanism — a six-week job that supposedly causes graduation with nothing in between. An *implausible link* connects boxes that cannot reasonably be connected at the stated dosage. *Outputs masquerading as outcomes* list "1,500 teens placed" in the outcomes column, confusing what the program did with the change it caused. An *over-stuffed model* claims every good thing in the world as an outcome, diluting focus and inviting failure on impossible promises. And an *unstated-assumption* error leaves the load-bearing beliefs invisible, so no one tests them.

### Worked Example: Building and Critiquing the Logic Model in Excel

We can build a readable logic model directly in Excel — no special software needed. Open a blank workbook and:

- In row 1, type the five column headers across **A1:E1**: *Inputs, Activities, Outputs, Short/Intermediate Outcomes, Impacts.*
- Widen the columns (**Home → Format → Column Width**) and turn on text wrapping for the data range via **Home → Alignment → Wrap Text** so long phrases stay readable.
- Enter the program elements down each column (one item per cell).
- Select **A1:E1** and apply bold and a fill color; then select the whole block **A1:E8** and add **Home → Borders → All Borders** so it reads as a grid.
- Use a separate sheet tab named *Assumptions & External Factors* to list, for each left-to-right arrow, the belief that must hold and the outside force that could interfere.
- Optionally, draw arrows between columns with **Insert → Shapes → Arrow** to emphasize the causal flow.

The resulting model, in compact form:

| Inputs | Activities | Outputs | Short/Intermediate Outcomes | Impacts |
|--------|-----------|---------|------------------------------|---------|
| Grant + city funds | Recruit & place teens | 1,500 teens placed | Improved work habits & efficacy | Higher graduation rate |
| Program staff | Run weekly workshops | ~12,000 workshop-hours | Better fall school attendance | Reduced justice-system contact |
| Employer partners | Match mentors | 1,500 mentor matches | Demonstrated job skills | Higher young-adult earnings |

Now *critique* it. The jump from a six-week summer job (an output) to a graduation rate a year later (an impact) crosses two whole columns of unmeasured outcomes — a likely missing-link problem. The promised reduction in justice involvement depends on external factors (policing, neighborhood) the program does not touch, so any impact claim there will require a strong comparison group. And "1,500 teens placed" correctly sits in *outputs*, not outcomes — a placement is something the program did, not a change it caused.

> **Returning to the Case:** Once the San Antonio team lays out this grid, the budget office's question answers itself: the program can defend its *outputs* and possibly its *short-term outcomes* (with a pre/post work-readiness measure), but its claims about graduation and justice involvement are long, assumption-heavy links it never instrumented. The fix is not to abandon those goals but to add the missing indicators and design a comparison before next summer.

## Common Pitfalls

- **Confusing the logic model with the program's org chart or budget.** It is a causal map, not an administrative diagram.
- **Listing activities in the outcomes column.** Verbs that the program performs are activities; nouns describing changes in participants are outcomes.
- **Leaving assumptions unstated.** The unexamined assumption is where programs quietly fail.
- **Promising impacts you will never measure.** If a box has no indicator and no plan to collect it, do not claim it.
- **Drawing one arrow from far-left to far-right.** Long jumps hide the mechanism; insist on the intermediate boxes.

## Practice and Application

1. **Build a logic model (Excel).** Choose a real Texas program you know — a county workforce voucher, a city summer-meals program, a library literacy initiative — and build a five-column logic model using the Excel steps above. Add a second sheet listing two assumptions and two external factors.
2. **Critique a chain.** For your model, identify the single weakest link and explain, in a paragraph, why the program's overall plausibility is capped by it.
3. **Indicators (Excel).** Add a sixth column to your model. For each outcome and impact box, write one concrete indicator and the data source you would use to measure it. Flag any box for which no data currently exist.
4. **From boxes to questions.** Translate three links in your model into three evaluation questions, and label each as process, outcome, or impact (drawing on Chapter 1).
5. **County panel application (Excel).** Suppose a county adopted a voter-engagement program in 2016. Open the Texas County Panel and use a PivotTable (**Insert → PivotTable**) to summarize turnout before and after 2016 for that county. Then explain which boxes of a plausible logic model the turnout variable could serve as an indicator for — and which it cannot.

## Transition to Chapter 3

A logic model tells you *what* to ask and *what* to measure, but it does not, by itself, tell you whether the program *caused* the changes you observe. The summer program's graduation claim hinges on a comparison the program never built: what would these teens' outcomes have been *without* the program? Chapter 3 makes that question precise. We introduce the counterfactual and the potential-outcomes framework, define a treatment effect formally, confront selection bias, distinguish internal from external validity, catalog the classic threats to a study's credibility, and lay out the menu of designs — from descriptive to experimental — and the conditions under which each can support a believable causal claim.
