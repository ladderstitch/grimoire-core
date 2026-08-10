---
name: apply-ladder-of-causation
description: Use when deciding what kind of evidence a question actually requires — before running an experiment, trusting an observational correlation, or reasoning about "what would have happened if" — by classifying the question as associational (what is?), interventional (what if I do X?), or counterfactual (what if I had done X instead?), since each rung requires a different type of evidence or model and no amount of data at a lower rung can answer a question posed at a higher one.
source: 'Pearl & Mackenzie "The Book of Why" (2018); Pearl "Causality: Models, Reasoning, and Inference" 2nd ed. (2009); Pearl awarded the Turing Award (2011) for foundational contributions to probabilistic and causal reasoning; documented adoption in econometrics'' instrumental-variables/natural-experiment methodology and in industry causal-inference practice (Microsoft''s DoWhy library, Uber''s CausalML, Netflix and LinkedIn causal-inference teams) using causal graphs to determine what evidence a business question actually requires'
tags: [causal-inference, correlation-vs-causation, counterfactual-reasoning, mathematics, judea-pearl, causal-diagrams]
related: [apply-bayesian-reasoning, apply-bayesian-network-inference, design-controlled-experiment, run-ab-test]
---

# Apply Ladder of Causation

Before trusting a correlation, running an experiment, or reasoning about what would have happened, classify the question by which rung of causal reasoning it actually sits on — association, intervention, or counterfactual — because each rung has a different evidence requirement, and no amount of data at a lower rung answers a question posed at a higher one.

## Why This Is Best Practice

**Adopted by:** Judea Pearl's causal hierarchy, most accessibly presented in *The Book of Why* (with Dana Mackenzie, 2018) and formalized in *Causality* (2009), underlies modern causal-inference practice across industry and academia — Microsoft's DoWhy library, Uber's CausalML, and causal-inference teams at Netflix and LinkedIn are built explicitly around this three-level distinction to determine what evidence a product or business question actually requires before running an analysis. Econometrics' instrumental-variables and natural-experiment methodology exists specifically to answer Rung-2 (interventional) questions when a true randomized experiment isn't possible — an approach that only makes sense once the question has been correctly classified as interventional in the first place. Pearl received the 2011 Turing Award for these foundational contributions to probabilistic and causal reasoning.

**Impact:** The hierarchy's central, falsifiable claim is that pure statistical/correlational methods — including most machine learning trained on observational data — are structurally limited to Rung 1 and cannot answer Rung 2 or Rung 3 questions without additional causal assumptions, no matter how much observational data is available. This is a testable claim about what evidence can and cannot establish: a business analysis that answers "will raising the price cause more churn?" (Rung 2) using only observational correlation between historical prices and churn (Rung 1) is answering the wrong kind of question with the wrong kind of evidence, regardless of the analysis's statistical sophistication.

**Why best:** This is not a restatement of "correlation isn't causation" as a general warning — several existing techniques already state that conclusion as justification for their own method (`design-controlled-experiment`'s and `run-ab-test`'s randomization requirement, `audit-model-fairness`'s bias-checklist warning), but none of them provide the general diagnostic step itself: given any question, identify which rung it's actually asking, and identify what evidence or model type that rung actually requires. `apply-bayesian-reasoning` updates a single belief from evidence — that is Rung 1, associational updating — and doesn't itself distinguish whether the underlying question needed to be Rung 1 in the first place. This skill is the classification step that determines, before any statistical method is chosen, whether observational data suffices, whether an intervention/experiment is required, or whether a full causal model supporting counterfactual queries is needed.

Sources: Pearl & Mackenzie, *The Book of Why* (2018); Pearl, *Causality: Models, Reasoning, and Inference* (2009).

## Steps

### 1. State the question precisely

Write the actual question being asked, in the specific form the answer needs to take — not "does X relate to Y?" but the precise version: "does seeing X change my belief about Y?" versus "if I do X, what happens to Y?" versus "if I had done X instead of what I actually did, what would Y have been?" The exact phrasing determines which rung the question sits on.

### 2. Classify the question by rung

| Rung | Question form | What it asks |
|---|---|---|
| 1 — Association | "What is?" / "How would seeing X change my belief about Y?" | Pattern/correlation in observed data — no claim about what would happen if anything were changed |
| 2 — Intervention | "What if I do X?" | The effect of deliberately changing X, holding everything else as it would naturally respond — requires causal, not just correlational, knowledge |
| 3 — Counterfactual | "What if I had done X instead of what I actually did?" | Reasoning about an alternate past given what actually happened — requires a full causal model, the hardest rung |

### 3. Identify what evidence or model type the rung actually requires

- **Rung 1** — observational data is sufficient; correlation, joint/conditional distributions, and standard statistical inference directly answer the question.
- **Rung 2** — observational data alone is not sufficient regardless of volume; requires either a randomized experiment (`design-controlled-experiment`, `run-ab-test`) or, when randomization isn't possible, a valid causal diagram plus intervention calculus (do-calculus) or a natural-experiment/instrumental-variable design that approximates the missing randomization.
- **Rung 3** — requires a fully specified structural causal model capable of representing a counterfactual world that never occurred; observational data and even a completed randomized experiment on the real world don't by themselves answer a counterfactual "what if it had been different" question without that model.

### 4. Check whether the available or planned evidence actually matches the rung

If the question is Rung 2 or 3 but the only available or planned evidence is observational (Rung 1), stop and flag the mismatch explicitly — this is the single most common analysis error the hierarchy is designed to catch. No amount of additional observational data resolves the mismatch; only interventional or counterfactual-capable evidence does.

### 5. Escalate the evidence-gathering plan to match the rung, not the convenient data

If a true randomized intervention is required but infeasible, use the appropriate Rung-2 substitute (instrumental variables, a natural experiment, a validated causal diagram with do-calculus) rather than defaulting back to observational correlation because it's what's already available.

## Rules

- Never answer a Rung 2 or Rung 3 question using only Rung 1 (observational) evidence — classify the question's rung before choosing the analysis method, not after.
- More observational data does not resolve a rung mismatch — the volume of correlational data is irrelevant to whether it can answer an interventional or counterfactual question.
- When a true experiment is infeasible for a Rung-2 question, use a recognized substitute (instrumental variables, natural experiment, validated causal diagram) rather than silently downgrading the question to Rung 1 and answering that instead.
- State the question's rung explicitly in any analysis that touches causal language ("causes," "leads to," "if we changed") — implicit rung-mismatches are the most common way correlational analysis gets mistaken for causal justification.

## Examples

**Trigger:** A product team observes that users who enable a certain feature have higher retention, and wants to decide whether to promote the feature to drive retention.
→ The business question ("will promoting this feature increase retention?") is Rung 2 — an intervention question. The available evidence (observed correlation between feature use and retention) is Rung 1. Flag the mismatch: users who enabled the feature may differ systematically from those who didn't (self-selection), so the observed correlation doesn't establish what would happen if usage were driven up by promotion. Resolve by running a randomized experiment (`run-ab-test`) that actually intervenes on feature exposure, rather than trusting the observational correlation.

**Trigger:** A team wants to know whether a specific engineer's code change caused a production outage that already occurred, to inform a postmortem.
→ This is a Rung 3 counterfactual question — "what would have happened if this specific change had not been made, given everything else that actually happened?" Observational logs and even a controlled reproduction test (Rung 2) don't fully answer this without a causal model of the system capable of representing the specific counterfactual scenario. Be explicit that the postmortem conclusion is a counterfactual causal claim, not a directly observed fact, and support it with the best available causal model rather than treating a timeline correlation as proof.

## Common Mistakes

- **Treating a strong observational correlation as if it answers an interventional question.** A large, statistically robust Rung 1 correlation is still Rung 1 — its strength doesn't convert it into Rung 2 evidence.
- **Running more observational analysis when the actual gap is a missing intervention.** No amount of additional correlational data substitutes for a randomized experiment or valid causal-diagram-based intervention calculus once the question is genuinely Rung 2.
- **Using causal language ("caused," "led to," "resulted in") while only having Rung 1 evidence.** This misrepresents what the analysis actually supports and invites decisions based on a claim the evidence doesn't establish.
- **Assuming a completed experiment on the real world automatically answers a counterfactual question about a specific past instance.** A randomized experiment establishes an average causal effect (Rung 2); a specific-instance counterfactual ("what would have happened to this particular case") is Rung 3 and needs a structural model, not just the experiment's aggregate result.

## When NOT to Use

- When the question is genuinely and only associational (predicting Y from observed X for forecasting purposes, with no causal or interventional claim being made) — classifying it is a quick confirmation step, not an obstacle; proceed directly with standard statistical methods.
- When a full, validated causal model already exists and has been vetted for the domain — repeatedly re-deriving the rung classification for routine, already-answered questions within that model adds no value.
- For purely mathematical or logical questions with no empirical causal content — the hierarchy applies to questions about real-world cause and effect, not to formal proofs or definitional claims.
