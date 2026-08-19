---
name: apply-hindsight-bias-correction
description: Use when reviewing a past decision after its outcome is already known — a postmortem, an investment review, a medical case review, a historical judgment — before judging how foreseeable the outcome was, because knowing the outcome makes it feel like it was more predictable in advance than it actually was, and this distortion cannot be corrected by simply trying harder to "imagine not knowing."
source: 'Fischhoff, "Hindsight is not Equal to Foresight: The Effect of Outcome Knowledge on Judgment Under Uncertainty", Journal of Experimental Psychology: Human Perception and Performance (1975); Fischhoff & Beyth, "I Knew It Would Happen: Remembered Probabilities of Once-Future Things", Organizational Behavior and Human Performance (1975); Kahneman, "Thinking, Fast and Slow" (2011)'
tags: [cognitive-bias, decision-making, postmortem, hindsight-bias, retrospective-judgment, evaluation]
related: [apply-premortem, apply-reference-class-forecasting, apply-sunk-cost-discipline]
---

# Apply Hindsight Bias Correction

Before judging how foreseeable a past outcome was, retrieve or reconstruct the actual probability estimates and information available at the time the decision was made — because simply knowing an outcome occurred makes it feel like it was more predictable in advance than it genuinely was, and this distortion persists even when the person judging tries consciously to correct for it.

## Why This Is Best Practice

**Why best:** Hindsight bias is not the same claim as "people are unfair when judging others' past decisions" — it is a specific, measured distortion of memory and judgment: once an outcome is known, people systematically misremember or misjudge how probable that outcome seemed beforehand, converging their retrospective estimate of foreseeability toward the outcome that actually happened. Because the bias operates on the reconstruction of the past judgment itself, not on a deliberate unfairness, it cannot be reliably fixed by asking evaluators to "try to imagine not knowing the outcome" — the correction requires an actual, contemporaneous record of what was known and estimated at the time, made before the outcome was known.

**Fischhoff (1975):** The foundational demonstration — subjects read a description of a historical event with an uncertain outcome and were asked to estimate, in hindsight, the probability they would have assigned to each possible outcome before it was known. Subjects who were told which outcome actually occurred assigned that outcome a substantially higher retrospective probability than subjects given the identical information but not told the actual outcome — and subjects were largely unaware their judgment had been altered by this knowledge, often insisting they would have predicted the actual outcome all along.

**Fischhoff & Beyth (1975) — "I knew it would happen":** Extended the finding to real-world predictions, asking subjects to state probability estimates for future geopolitical events before they occurred, then asking the same subjects, after the events occurred, to recall what probability they had originally assigned. Subjects systematically misremembered their own prior estimates as having been closer to the actual outcome than the estimates they had actually recorded — demonstrating the bias distorts a person's memory of their own past judgment, not just their evaluation of someone else's.

**Kahneman, "Thinking, Fast and Slow" (2011):** Identifies hindsight bias as a major driver of unfair retrospective evaluation of decision-makers — physicians, executives, and policymakers are judged more harshly for decisions that led to bad outcomes than for equally- or more-reasonable decisions that happened to lead to good outcomes, even when the quality of the decision-making process at the time was identical or better in the harshly-judged case. Kahneman explicitly links this to systematic risk-aversion in decision-makers who anticipate being judged this way, since prudent, well-reasoned decisions that turn out badly are punished more severely in hindsight than equally risky decisions that happen to turn out well.

**Adopted by:** Aviation and clinical incident-review protocols (e.g., root-cause-analysis frameworks used in hospital morbidity-and-mortality reviews and airline safety investigations) are explicitly designed to reconstruct what was actually known and knowable at the time of a decision, rather than evaluating the decision using information only available after the fact, specifically to counter hindsight bias in blame attribution; structured pre-decision documentation (e.g., contemporaneous investment theses, documented go/no-go risk assessments before a mission or launch) is standard practice in disciplined investment and engineering organizations specifically to create the record needed for a fair later review.
**Impact:** Fischhoff's original studies found subjects' hindsight-adjusted probability estimates for a known outcome were substantially and consistently higher than blind subjects' assessments of the same pre-outcome information, with subjects largely unaware of the shift; Fischhoff & Beyth found subjects misremembered their own genuinely-recorded prior predictions as having been more accurate than they actually were, showing the distortion affects self-evaluation as well as evaluation of others, and that only a contemporaneous written record (not memory) reliably survives the bias.

## Steps

1. **Before making a consequential decision, document the actual probability estimate and the specific information available at the time.** Write down, contemporaneously, what outcomes were considered plausible, the estimated likelihood of each, and the specific evidence the estimate was based on — this record is the only reliable defense against hindsight bias later, because memory of one's own past judgment is itself distorted by the eventual outcome.

2. **When reviewing a past decision after the outcome is known, retrieve the contemporaneous record rather than asking anyone (including the original decision-maker) to recall or estimate the pre-outcome probability from memory.** Fischhoff & Beyth's findings mean even the original decision-maker's own memory of their prior estimate is unreliable once they know the outcome — only a record made before the outcome was known should be treated as ground truth for what was foreseeable.

3. **Separate the evaluation of decision quality from the evaluation of outcome quality.** Explicitly score the decision-making process (was the available information used well, was the reasoning sound, were the right questions asked) using only the documented pre-outcome record, before looking at how the outcome actually turned out — this prevents outcome knowledge from bleeding into the process evaluation.

4. **If no contemporaneous record exists, explicitly flag the review as hindsight-bias-vulnerable and reduce confidence in the judgment accordingly.** Absent a genuine pre-outcome record, any retrospective judgment about foreseeability should be treated as unreliable by default, not corrected for by asking evaluators to try harder to imagine not knowing the outcome — that correction does not work reliably.

5. **In organizational postmortems, present the case with outcome information withheld for as long as possible while reconstructing the decision timeline.** Walking through what was known at each point in time, before revealing what ultimately happened, produces a more accurate assessment of what was genuinely foreseeable at each stage than reviewing the whole story with the outcome already known throughout.

6. **Reward well-reasoned decisions that turn out badly the same way as well-reasoned decisions that turn out well, when the decision-quality evaluation (step 3) is equivalent.** Because hindsight bias otherwise systematically punishes good decisions with bad outcomes more than it should, and rewards lucky decisions with good outcomes more than the decision quality warrants, explicitly correcting evaluation and incentive systems for this asymmetry is necessary to avoid training decision-makers toward excessive caution or outcome-chasing.

## Rules

- Never rely on memory (including the original decision-maker's own memory) to reconstruct what was foreseeable before an outcome was known — only a genuine contemporaneous record survives hindsight bias reliably.
- Evaluate decision quality using only the pre-outcome record, separately from and before considering the actual outcome — blending the two lets outcome knowledge distort the process evaluation.
- Treat any hindsight judgment made without a contemporaneous pre-outcome record as unreliable by default, not as correctable through conscious effort to "imagine not knowing."
- Calibrate reward and blame to decision quality at the time, not to outcome quality alone — a good decision with a bad outcome and a bad decision with a good outcome should not receive opposite evaluations if the decision quality itself was, respectively, sound and unsound.

## Examples

**Engineering postmortem:** A production incident occurs after a team's architecture decision, made months earlier, turns out to have an edge case that caused the failure. The postmortem retrieves the team's original documented risk assessment and finds the edge case was genuinely not identifiable given the information available at the time — the review credits the original decision as reasonable given contemporaneous knowledge, rather than judging it harshly because the outcome is now known to have been bad.

**Investment review:** A fund manager's position loses money after an unforeseeable macroeconomic shock. The investment committee reviews the manager's contemporaneously-documented investment thesis and risk assessment, made before the shock, and finds the reasoning and risk sizing were sound given the information available at the time — the manager is evaluated on the quality of the original thesis, not penalized as though the loss reflected poor judgment, because the documented record shows the shock was genuinely not foreseeable from the pre-outcome evidence.

**Medical case review:** A hospital's morbidity-and-mortality review reconstructs a clinical decision by first presenting the case information exactly as it was known at each decision point, withholding the eventual outcome until the full decision timeline has been walked through — the panel judges each decision point based on what was knowable then, rather than working backward from the known outcome and judging every prior decision through that lens.

## Common Mistakes

- **Asking a decision-maker to recall what they thought would happen, after they already know what did happen.** Fischhoff & Beyth's research shows this self-report is unreliable — it should not be treated as equivalent to a genuine contemporaneous record.
- **Judging a decision's quality primarily by its outcome, rather than by the information and reasoning available at the time it was made.** This is hindsight bias applied directly to performance evaluation, and it systematically punishes good decisions that had bad luck while rewarding bad decisions that had good luck.
- **Believing that conscious effort ("let me really try to imagine not knowing this") reliably removes the bias.** Fischhoff's original studies specifically found subjects were unaware their judgment had shifted and confidently defended their hindsight-inflated estimates — conscious effort is not a demonstrated reliable fix.
- **Reviewing an incident by presenting the outcome first and then working backward through the decision timeline.** This structure maximizes exposure to hindsight bias at every step of the review; reconstructing the timeline forward, with outcome revealed last, produces a more accurate assessment.

## When NOT to Use

- When a genuine, contemporaneous pre-outcome record already unambiguously shows the outcome was clearly foreseeable and was disregarded — hindsight-bias correction protects against unfairly harsh judgment of genuinely reasonable decisions, not against fair accountability for decisions that ignored clear, documented, available warnings.
- For decisions with no realistic way to have created a contemporaneous record (e.g., very low-stakes, routine choices) — the overhead of formal pre-decision documentation isn't justified for every decision; reserve it for decisions consequential enough to warrant a future fair review.
- When evaluating a decision-making process in the abstract, independent of any specific past outcome (e.g., designing a decision framework prospectively) — hindsight bias correction specifically addresses retrospective evaluation after an outcome is already known.

> For mental health concerns, consult a qualified mental health professional.
