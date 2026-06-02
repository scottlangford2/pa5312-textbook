---
layout: page
title: "Chapter 12"
permalink: /docs/chapter12/
---

# Communicating Findings, Ethics, and the Evaluation Report

## Epigraphs

> "The aim of evaluation is to provide useful information to those who have a legitimate interest in the program."
> — Peter H. Rossi, Mark W. Lipsey, and Gary T. Henry, *Evaluation: A Systematic Approach* (2019)

## Opening Case: Reporting to the San Marcos City Council

You have spent a semester evaluating a City of San Marcos workforce-development program that places unemployed residents into paid apprenticeships with local employers. Your analysis is sound: a defensible comparison group, a clear estimated effect on twelve-month employment, and a cost-benefit analysis showing the program roughly pays for itself within four years. You are proud of the work.

Now you have twenty minutes on the council's agenda and a five-page memo limit. The council members are a retired schoolteacher, a small-business owner, two attorneys, and a software engineer — none of them statisticians. The mayor has already told a reporter she expects the evaluation to "prove the program is a success." One council member, skeptical of the whole effort, is looking for any reason to cut its funding. Your beautifully specified regression means nothing to this audience until you can explain what it found, how confident they should be, and what they should do about it.

The hardest part is not the analysis you already finished. It is deciding how to present a result that is *positive but uncertain* — and resisting the pull, from the mayor's office and from your own pride, to overstate it.

**Guiding Questions**

- How should an evaluation report be structured so a busy, non-technical decision-maker can act on it?
- How do you report uncertainty and threats to validity honestly without burying or overselling your findings?
- What ethical standards govern the evaluator, and how do those standards apply to new tools like AI?

## Why This Chapter Matters

An evaluation that no one understands, trusts, or uses is a failed evaluation, however rigorous its methods. The skills in this final chapter — clear structure, honest reporting, effective visualization, and ethical conduct — are what convert analysis into influence. They are also where the profession's integrity lives. The technical chapters taught you to *find* a credible answer; this one teaches you to *deliver* it without distorting it, and to recognize that the most important number in a report is sometimes the one that admits what you do not know.

## Structuring the Report for Decision-Makers

Decision-makers read top-down and stop early. Structure the report so the most important content comes first and the technical justification follows for those who want it.

- **Executive summary (one page).** The single most-read section. State the question, the headline finding, the degree of confidence, and the recommendation — in plain language, with no jargon and no equations. Assume some readers read nothing else.
- **Background and questions.** What program, what problem, what the evaluation set out to answer.
- **Methods.** Design, data, and analysis — enough for a knowledgeable reader to judge credibility, written so a layperson can follow the logic.
- **Findings.** The results, led by the main effect, supported by tables and figures. Report magnitude *and* uncertainty.
- **Limitations.** An honest accounting of threats to validity. This section builds trust rather than undermining it.
- **Recommendations.** Concrete, actionable, and tied to the findings — and proportionate to how strong those findings actually are.

> **Briefing:** Write the executive summary as if it is the only page that will be read, because for most of your audience it is.

### Reporting Uncertainty and Threats to Validity Honestly

Every estimate carries uncertainty, and every design carries threats to validity. Reporting them is not a confession of weakness; it is the core of professional honesty. State confidence intervals or margins of error in words a layperson grasps: "Our best estimate is that the program raised twelve-month employment by 9 percentage points, and we are reasonably confident the true effect lies between 3 and 15 points." Distinguish *statistical* uncertainty (sampling noise) from *design* threats (selection bias, attrition, spillovers from earlier chapters) — a tight confidence interval around a biased estimate is precise *and* wrong.

> **Briefing:** A confidence interval describes sampling noise only; it says nothing about whether your design has eliminated selection bias. Report both kinds of uncertainty, and never let a small p-value substitute for a credible design.

Resist three temptations: overstating a marginal result to please a sponsor, hiding a limitation that a critic might exploit, and implying causation that the design cannot support. If the San Marcos comparison group is imperfect, say so, and say what it means for the conclusion. A report that names its own weaknesses is far harder to attack than one that pretends to have none.

## Data Visualization for Non-Technical Audiences

A figure should make one point, instantly. For a council audience, prefer a clean bar chart of group means over a scatterplot of residuals; show the *effect*, not the machinery. A few durable principles:

- **One message per chart.** If you cannot state the chart's point in a sentence, it is doing too much.
- **Label directly.** Put numbers on bars and labels on lines; make the reader's eye do no work.
- **Show uncertainty when you can.** Error bars on a bar chart visually communicate "we are not certain of the exact height," reinforcing honest reporting.
- **Avoid distortion.** A bar chart's vertical axis should start at zero; truncating it exaggerates differences and is a classic way to mislead.
- **Strip the clutter.** Drop 3-D effects, heavy gridlines, and decorative color. Ink that does not carry information distracts from the point.

> **Briefing:** The most ethical chart and the clearest chart are usually the same chart — honesty and clarity rarely conflict.

### Worked Example: An Honest Council Figure in Excel

You want one chart comparing twelve-month employment rates for the program and comparison groups, with the uncertainty visible. Your data: program-group rate 0.62, comparison-group rate 0.53, and a margin of error of 0.06 on the program estimate.

**Step 1 — Lay out the data.** Two rows (Program, Comparison) with the rate in column B and the margin of error in column C.

**Step 2 — Build the chart.** Select the rates and Insert ▸ Column Chart (Clustered). Right-click the axis, set the minimum to 0, and delete the chart's gridlines and title clutter.

**Step 3 — Add error bars.** With the series selected, Chart Design ▸ Add Chart Element ▸ Error Bars ▸ More Options, choose **Custom**, and point both the plus and minus values to the margin-of-error column (C). Now the program bar visibly carries its uncertainty.

**Step 4 — Label directly.** Add data labels so each bar shows its percentage, and replace the legend with a one-line, plain-language title: "Program participants were employed at higher rates one year later."

| Group | 12-month employment | Margin of error |
|---|---|---|
| Program | 0.62 | $\pm 0.06$ |
| Comparison | 0.53 | — |

The chart makes the 9-point gap obvious while the error bar quietly reminds the council that the exact size is uncertain — clarity and honesty in a single image.

> **Returning to the Case:** You open your council presentation with this one chart and a one-sentence headline, then give the magnitude with its range in plain words. When the mayor presses you to call the program "a proven success," you hold the line professionally: the evidence is *positive and reasonably strong*, the comparison group is good but not a randomized control, and the honest recommendation is to *continue and expand modestly while strengthening data collection* — not to declare victory. That measured framing is exactly what makes your report credible to the skeptical council member, and it is what professional standards require.

## Evaluation Ethics and Professional Standards

The evaluation field has codified its obligations. The Joint Committee on Standards for Educational Evaluation organizes them into categories that translate cleanly to public administration:

- **Utility.** The evaluation should serve the information needs of its users — the right questions, answered usefully and on time.
- **Feasibility.** Methods should be practical and proportionate to the resources and stakes.
- **Propriety.** The evaluation should be legal, ethical, and respectful of the rights and welfare of those involved — protecting confidentiality, avoiding harm, and disclosing conflicts of interest.
- **Accuracy.** Findings should be technically sound and conclusions justified by the evidence.

> **Briefing:** When a sponsor's wish and the evidence conflict, accuracy and propriety outrank utility — an evaluator's first loyalty is to the truth of the findings, not to the client's preferred story.

Protecting stakeholders is a concrete duty, not an abstraction: de-identify individual records, never report cells so small that a person could be re-identified, and disclose who funded the work and any stake you hold in the result. In the San Marcos case, that means apprentices' names and exact wages never appear in a public memo.

### The Responsible Use of AI Tools in Evaluation

AI tools can now draft a methods section, suggest an Excel formula, or summarize a literature in seconds. Used well, they speed the *drafting* of an evaluation. Used carelessly, they manufacture confident falsehoods — invented statistics, fabricated citations, plausible-but-wrong reasoning — that an unwary analyst will sign their name to.

The professional standard is simple and strict: **AI assists drafting; it never substitutes for judgment.** Concretely:

- **Verify every number.** If an AI tool reports a figure, recompute it yourself in Excel. Never paste a statistic you have not personally checked.
- **Verify every citation.** AI tools fabricate references that look real. Confirm each source exists and says what you claim before it enters a report.
- **Verify every claim.** Treat AI-generated reasoning as a draft from an unvetted intern — useful, occasionally wrong, always to be checked against the data and the design.
- **Own the output.** Your name on the report means *you* vouch for it. Responsibility is not delegable to a tool.
- **Protect confidential data.** Do not paste identifiable stakeholder records into external AI systems.

> **Briefing:** AI changes how fast you can draft, not what you are accountable for. Every number, citation, and claim that reaches a decision-maker must be one you have personally verified.

## Common Pitfalls

- **Burying the headline.** Forcing a council member to read to page four for the main finding wastes your one chance to be heard.
- **Overstating to please a sponsor.** Letting the mayor's preferred conclusion outrun the evidence destroys your credibility the first time a critic checks your work.
- **Hiding limitations.** A weakness you disclose builds trust; one a critic discovers destroys it.
- **Misleading charts.** Truncated axes and 3-D effects exaggerate differences and erode the honesty the whole report depends on.
- **Trusting AI output unchecked.** A fabricated statistic or citation under your name is your error, not the tool's.
- **Confusing precision with validity.** A tight confidence interval around a biased estimate is confidently wrong.

## Practice and Application

1. **Executive summary.** Write a one-page executive summary of the San Marcos workforce evaluation for the council: question, headline finding with its uncertainty, and a recommendation, in plain language with no equations.
2. **Honest chart.** Using the worked-example data, build the clustered bar chart in Excel with a zero-based axis, custom error bars, and direct data labels. Then build a deliberately *misleading* version (truncated axis, no error bars) and write two sentences explaining how each choice changes the reader's impression.
3. **Limitations section.** For a quasi-experimental evaluation of your own final-project program, draft a limitations paragraph that names two specific threats to validity and states honestly what each means for the conclusion.
4. **Standards application.** Take a realistic dilemma — a sponsor asks you to drop an unflattering subgroup result — and explain which Joint Committee standards are in tension and how you would resolve it.
5. **AI verification log.** Suppose an AI tool drafts a methods paragraph that cites a study and reports a benefit-cost ratio. Write the checklist of verification steps you would perform before either could appear in your report.

## Conclusion: Becoming a Critical Producer and Consumer of Evidence

Over thirteen weeks you have built a complete evaluator's toolkit. You learned to specify what a program is supposed to do and how to measure whether it does it. You learned the difference between a correlation and a cause, and the family of designs — from randomized controlled trials through difference-in-differences and matching to careful regression — that let you defend a causal claim or, just as importantly, admit when you cannot. You learned to ask not only whether a program works but whether it is worth its cost, discounting future dollars and confronting your own assumptions through sensitivity analysis. And in this final chapter you learned to carry all of that into a room full of decision-makers and deliver it clearly, honestly, and ethically.

Throughout, your tool was Microsoft Excel — `AVERAGEIF` and the Regression dialog, the `NPV` function and What-If Data Tables, clustered bar charts with honest error bars. The tool was deliberately humble, because the point was never the software. The point was *judgment*: knowing which question a method can answer, how much to trust a number, and when to say "the evidence does not support that claim."

That judgment makes you two things at once. As a *producer* of evidence, you can design and report an evaluation that a city council can act on without being misled. As a *consumer* of evidence — which you will be far more often — you can read someone else's evaluation, or an AI-generated summary of one, and ask the right questions: What was the comparison group? How large is the effect and how uncertain? What was left in the costs and out of the benefits? Whose interests funded this, and what does the report decline to mention?

Public administration runs on claims about what works. The graduate of this course is the person in the room who can tell a credible claim from a convincing one, produce evidence worthy of trust, and refuse to overstate what the data will bear. That discipline — equal parts technical skill and intellectual honesty — is the real subject of PA 5312, and it is yours to practice for the rest of your career.
