---
name: apply-statistical-prediction-preference
description: Use when a validated statistical model, checklist, or actuarial formula exists for a prediction task — hiring, credit risk, medical diagnosis, parole/recidivism, quality forecasting — and you are tempted to override it with expert intuition or "holistic" case-by-case judgment, because decades of comparison studies show simple statistical rules match or outperform expert intuitive judgment in the large majority of domains studied.
source: 'Meehl, "Clinical Versus Statistical Prediction: A Theoretical Analysis and a Review of the Evidence" (1954); Grove, Zald, Lebow, Snitz & Nelson, "Clinical Versus Mechanical Prediction: A Meta-Analysis", Psychological Assessment (2000); Dawes, Faust & Meehl, "Clinical Versus Actuarial Judgment", Science (1989)'
tags: [decision-making, cognitive-bias, prediction, forecasting, expert-judgment, statistics]
related: [apply-reference-class-forecasting, apply-small-sample-skepticism]
---

# Apply Statistical Prediction Preference

When a validated statistical rule, checklist, or actuarial formula exists for a prediction task, use it as the primary basis for the decision and treat intuitive expert override as the exception requiring justification — because comparison studies across dozens of domains find simple statistical rules match or outperform expert intuitive judgment in the large majority of cases, despite experts' confidence that their case-by-case judgment adds value.

## Why This Is Best Practice

**Why best:** The finding is not that experts are unintelligent or careless — it is that combining many weakly-predictive cues through holistic human judgment is a noisier, less consistent process than combining the same cues through a fixed statistical formula, even when the formula is simple and the expert has access to more information than the formula uses. The formula is perfectly consistent (the same inputs always produce the same output); expert judgment is not, even from the same expert evaluating the same case on different days. This inconsistency, not a lack of expertise, is the primary source of the statistical rule's advantage, which is why the advantage persists even when experts have more raw information available to them than the formula does.

**Meehl (1954):** The founding analysis, reviewing then-available studies comparing clinical psychologists' case-by-case predictions (of outcomes like treatment success, parole violation, or academic performance) against simple actuarial formulas using the same or a subset of the same input data. Meehl found the statistical formula matched or exceeded clinical judgment in the substantial majority of the studies reviewed, a finding that was controversial and resisted at the time precisely because it contradicted practitioners' confidence in their own case-specific judgment.

**Dawes, Faust & Meehl (1989):** Extended and updated the analysis across a much larger body of subsequent research spanning medicine, personnel selection, education, and parole decisions, confirming the original pattern held broadly: mechanical, formula-based combination of predictive information outperformed or matched intuitive clinical combination of the same information in the strong majority of studies, even in domains (like medical diagnosis) where practitioners had extensive specialized training.

**Grove, Zald, Lebow, Snitz & Nelson (2000):** A formal meta-analysis of 136 studies comparing mechanical/statistical prediction against clinical/intuitive prediction across a wide range of domains, finding statistical prediction outperformed clinical prediction in roughly half of studies and performed about equally in most of the remainder, with clinical judgment outperforming statistical prediction in only a small minority of studies — establishing the pattern as a robust, replicated, large-sample finding rather than an artifact of the original 1954 review.

**Adopted by:** Structured, algorithmically-weighted checklists and scoring rules are standard in actuarial underwriting (insurance risk pricing), structured behavioral hiring interviews with pre-defined scoring rubrics (see `run-behavioral-interview`), clinical risk-prediction tools in medicine (e.g., validated scoring systems for cardiac risk, sepsis risk), and criminal-justice risk-assessment instruments used in parole and sentencing decisions in many jurisdictions.
**Impact:** Grove et al.'s meta-analysis of 136 comparison studies found statistical prediction outperformed clinical judgment outright in a substantial share of studies and matched it in most of the remainder, with clinical judgment clearly superior in only a small fraction of cases — a pattern replicated across medicine, personnel selection, and criminal justice, indicating this is a general property of combining multiple weak predictors, not a domain-specific quirk.

## Steps

1. **Check whether a validated statistical model, checklist, or formula already exists for the prediction task at hand.** Many high-stakes recurring prediction tasks (credit risk, clinical risk scores, structured interview rubrics, quality-control formulas) already have a validated instrument — the first step is determining whether one exists before defaulting to intuitive judgment.

2. **If a validated instrument exists, use its output as the primary basis for the decision, not as one input to be weighed against intuition.** The research finding specifically is that *blending* statistical output with intuitive override, weighted case-by-case, tends to erode the statistical rule's advantage — treat the formula's output as the default decision, overridden only through the explicit override process below.

3. **If no validated instrument exists but the prediction is a recurring, high-volume decision, build one.** Identify the small number of factors most predictive of the outcome (from historical outcome data, not intuition about what should matter), combine them with a simple, fixed weighting scheme (equal weights on standardized inputs perform surprisingly well and are often within noise of an optimally-fitted formula), and validate the resulting rule against held-out historical outcomes before deploying it.

4. **Require an explicit, documented justification for any override of a validated statistical prediction — not a general feeling that "this case is different."** Because "this case is different" is the exact intuition Meehl and colleagues found unreliable as a general practice, an override should be based on a specific, verifiable piece of information the formula genuinely does not and cannot account for (e.g., a documented input error, a case falling fully outside the model's validated range) — not a holistic impression.

5. **Track override outcomes over time and compare them to the statistical rule's own track record on similar cases.** If overrides are, on average, performing worse than the formula would have on those same cases, that is direct local evidence to tighten the override policy, independent of the general research literature.

6. **Use structured checklists as an intermediate step when a full statistical model isn't feasible.** A fixed checklist that forces the same specific factors to be considered, in the same order, for every case captures much of the consistency advantage of a full statistical formula even without a fitted numerical model.

## Rules

- Treat a validated statistical prediction as the default decision, not as one input to be intuitively weighed against expert judgment — blending tends to erode the statistical advantage found in the comparison literature.
- Require a specific, documented, verifiable reason for any override — general confidence that "this case is different" is precisely the unreliable judgment pattern this research identifies.
- Where no validated model exists for a recurring, high-volume decision, building even a simple equal-weighted checklist from historically predictive factors is worth the effort — simple, fixed-weight rules perform close to optimally-fitted models in most studied domains.
- Track override outcomes against the baseline model's own track record to detect, with local data, whether a specific team's or individual's override pattern is actually adding value or eroding it.

## Examples

**Hiring:** A hiring team has a validated structured-interview scoring rubric with a demonstrated track record, but a hiring manager wants to override a below-threshold score because "I had a great feeling about this candidate." Applying statistical-prediction preference: the override requires documenting a specific, verifiable factor the rubric didn't capture (e.g., a scoring error, a skill genuinely outside the rubric's scope) rather than the general impression, and if approved, the outcome is tracked against the rubric's typical accuracy for similarly-scored candidates.

**Clinical risk scoring:** An emergency department uses a validated sepsis risk score to flag high-risk patients for immediate escalation. A clinician who feels a low-scoring patient "looks sicker than the number suggests" documents the specific clinical signs driving that judgment (not present in the score's inputs) before escalating outside the protocol, rather than silently overriding the score based on general impression.

**Credit underwriting:** A loan officer has access to a validated credit-scoring model but is inclined to approve a below-threshold applicant based on a favorable in-person impression. The underwriting policy requires the officer to document the specific factor the score doesn't capture (e.g., verified information the credit bureau data is missing) and tracks approved-override loan performance separately to check whether officer overrides are, in practice, outperforming or underperforming the model's own baseline default rate.

## Common Mistakes

- **Treating the statistical model's output as just one more opinion to weigh against expert intuition.** The research finding specifically concerns cases where the formula is used as the primary decision rule; ad hoc blending with intuition tends to reintroduce the inconsistency the formula was built to remove.
- **Overriding based on a general feeling that a case is unusual, without a specific, documented, verifiable reason.** This is exactly the pattern of intuitive override the comparison literature finds unreliable on average, even when any individual expert feels confident in the specific instance.
- **Assuming this preference applies even without a validated model.** An unvalidated ad hoc "statistical-sounding" formula has no demonstrated advantage over intuition — the preference is for *validated* statistical prediction specifically, not for numbers in general.
- **Never revisiting or updating the statistical model as new outcome data accumulates.** A model validated on historical data can degrade if the underlying population or conditions shift — periodic revalidation against new outcomes is necessary, not optional.

## When NOT to Use

- When no validated statistical model or checklist exists and the decision is too infrequent or too idiosyncratic to justify building one — in that case, structured expert judgment (independent multi-rater assessment, see `apply-halo-effect-mitigation`) is the best available alternative, not a reason to trust unstructured intuition instead.
- When the prediction task involves genuinely novel circumstances clearly outside the range of cases the statistical model was validated on — extrapolating a model far outside its validated domain is itself an unreliable practice; flag this explicitly rather than either blindly trusting or blindly overriding the model.
- When the decision has ethical or legal dimensions beyond pure predictive accuracy (e.g., criminal-justice risk instruments raise documented fairness and bias concerns in their input data) — predictive accuracy is one input to such decisions, not the sole criterion, and this skill addresses prediction accuracy specifically, not the full ethical evaluation of high-stakes automated decision systems.

> For mental health concerns, consult a qualified mental health professional.
