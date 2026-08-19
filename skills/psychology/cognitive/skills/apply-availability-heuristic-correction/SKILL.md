---
name: apply-availability-heuristic-correction
description: Use when judging how frequent, common, or risky something is based on how easily examples come to mind — recent news coverage, a vivid personal anecdote, a memorable failure — before treating that ease-of-recall as an accurate frequency estimate, because memorability and actual frequency are driven by different, only loosely related factors.
source: 'Tversky & Kahneman, "Availability: A Heuristic for Judging Frequency and Probability", Cognitive Psychology (1973); Lichtenstein, Slovic, Fischhoff, Layman & Combs, "Judged Frequency of Lethal Events", Journal of Experimental Psychology (1978); Combs & Slovic, "Newspaper Coverage of Causes of Death", Journalism Quarterly (1979)'
tags: [cognitive-bias, risk-assessment, decision-making, availability-heuristic, judgment, statistics]
related: [apply-reference-class-forecasting, apply-small-sample-skepticism]
---

# Apply Availability Heuristic Correction

Before estimating how frequent or risky something is from how easily examples come to mind, check the estimate against actual base-rate data — because ease of recall is driven by vividness, recency, and media exposure, not by real frequency, and the two diverge in predictable, measurable directions.

## Why This Is Best Practice

**Why best:** The availability heuristic is not simply "recent events feel more important" — it is a specific substitution: people answer the hard question ("how frequent is X, really?") by unconsciously answering an easier one ("how easily can I recall an example of X?"), and treating the answer to the easy question as if it answered the hard one. Because vividness, recency, and media coverage systematically inflate the recall-ease of dramatic, unusual, and heavily reported events relative to their actual frequency, judgments formed this way are predictably and directionally biased — not merely noisy — which makes them correctable with an explicit base-rate check.

**Tversky & Kahneman (1973):** The foundational studies showed people judge a category as more frequent when instances are easier to retrieve from memory, independent of the category's actual size — for example, subjects judged words starting with "K" to be more common than words with "K" as the third letter, because retrieval by first letter is structurally easier than retrieval by third letter, even though third-letter-K words are more frequent in English. This established that ease of retrieval, not actual frequency, is what drives the judgment.

**Lichtenstein, Slovic, Fischhoff, Layman & Combs (1978):** Asked subjects to judge the relative frequency of various causes of death and found systematic, large overestimation of dramatic, vivid causes (homicide, tornadoes, botulism) and systematic underestimation of common but undramatic causes (diabetes, stroke, asthma) relative to actual mortality statistics — subjects' rank-orderings correlated far more closely with how memorable or reported a cause of death was than with its actual death toll.

**Combs & Slovic (1979):** Directly linked the distortion to media coverage, finding that newspaper reporting frequency for various causes of death was itself highly skewed relative to actual death rates (dramatic causes overreported, common causes underreported), and that this reporting skew closely tracked the same pattern of public risk-frequency misjudgment found in Lichtenstein et al. — establishing the specific causal channel (disproportionate coverage of vivid events) that inflates their availability independent of their real frequency.

**Adopted by:** Risk-communication and public-health messaging guidance (e.g., WHO and CDC risk-communication frameworks) explicitly account for availability-driven risk misperception when designing public messaging about genuinely high-frequency but low-drama risks (e.g., promoting seatbelt use and diet/exercise over less statistically significant but more vivid dangers); actuarial and insurance underwriting relies on base-rate mortality and incidence tables specifically because individual and even expert intuitive frequency judgment is known to diverge from them in the availability-heuristic direction.
**Impact:** Lichtenstein et al.'s subjects' risk rank-orderings deviated from actual mortality data by orders of magnitude for some causes (some rare, dramatic causes of death were judged more frequent than causes that kill many times more people annually), and Combs & Slovic's finding that newspaper coverage frequency — not actual incidence — predicted these misjudgments demonstrates the distortion is driven by a measurable, external input (media exposure) rather than by any intrinsic property of the risks themselves.

## Steps

1. **Notice when a frequency, risk, or probability judgment is based on how easily an example comes to mind.** The trigger phrase is internal: "I can think of a case where..." or "this happens all the time" based on recalled instances rather than counted or looked-up data.

2. **Ask what is driving the ease of recall, separately from the actual question.** Recent exposure, personal involvement, emotional intensity, and media coverage all inflate recall-ease independent of true frequency — name which of these is likely operating before trusting the intuitive estimate.

3. **Look up the actual base rate before finalizing the judgment.** For any decision with real stakes, find the actual incidence, frequency, or statistical data for the category in question rather than relying on recalled examples — actuarial tables, incident logs, published statistics, or internal historical data, depending on the domain.

4. **Compare the base-rate figure to your recall-based intuition, and treat a large gap as informative about the bias, not about the data being wrong.** If your intuitive sense of "how often this happens" diverges sharply from the looked-up base rate, the more likely explanation is availability-driven distortion in your intuition, not an error in the base-rate data — investigate the data's validity, but don't discard it by default in favor of intuition.

5. **In group or organizational risk discussions, ask explicitly what data (not anecdotes) supports a stated frequency or risk claim.** When a decision is being justified by "we've seen this happen" or "this is a common failure," require the actual count or rate before it drives a decision — a single vivid incident can dominate a discussion despite reflecting a rare event, and a common but undramatic failure mode can be underweighted because no one has a memorable story about it.

6. **Deliberately seek out undramatic, high-frequency risks that lack a memorable narrative.** Because availability inflates dramatic risks and deflates boring ones, an explicit search for "what commonly goes wrong that nobody talks about" corrects for the blind spot the heuristic creates, rather than only correcting overestimates of dramatic risks.

## Rules

- Never finalize a real-stakes frequency or risk judgment based only on recalled examples — look up the actual base rate before deciding, even when the recalled examples feel conclusive.
- Treat a large gap between intuitive frequency judgment and looked-up base-rate data as a signal that availability bias is operating, not as grounds to distrust the data by default.
- In group settings, require a specific count or rate — not an anecdote — before a stated frequency claim is allowed to drive a decision.
- Actively look for common, undramatic risks that lack a memorable story, since the availability heuristic systematically underweights exactly this category.

## Examples

**Risk management:** A safety team is preparing to invest in preventing a rare, dramatic failure mode that was recently and vividly discussed after a single incident. Looking up the actual incident log shows this failure mode occurs far less often than a mundane, undramatic failure mode that has never generated a memorable story but occurs at a much higher rate — the team redirects investment to the higher-frequency, lower-drama risk based on the base-rate data rather than the vivid recent memory.

**Personal health decision:** Someone becomes highly concerned about a rare, widely reported illness after seeing extensive news coverage of a cluster of cases, while continuing to under-prioritize a much more common, statistically significant health risk (e.g., cardiovascular disease) that receives comparatively little dramatic coverage. Checking actual incidence and mortality statistics rebalances attention toward the higher-frequency, lower-coverage risk.

**Hiring/quality decisions:** A manager becomes convinced that a certain type of hiring mistake is "very common" after two memorable, recent bad hires, and proposes an expensive new screening process. Checking the actual historical hiring-outcome data shows the mistake rate is much lower than two vivid recent examples suggested — the availability-driven proposal is scaled back to match the actual base rate.

## Common Mistakes

- **Treating a vivid personal or organizational anecdote as representative data.** A memorable example is evidence that the event is possible, not evidence about how frequently it occurs relative to alternatives.
- **Confusing heavy media or internal-discussion coverage of an event with its actual frequency.** Coverage volume is driven by drama and novelty, not incidence rate — the two are only loosely correlated at best.
- **Discarding looked-up base-rate data because it conflicts with strong intuition.** The size of the intuition-versus-data gap is itself informative about the strength of the bias operating, not a reason to trust the intuition over the data.
- **Only correcting for overestimated dramatic risks while continuing to ignore underestimated undramatic ones.** The heuristic distorts in both directions simultaneously; a full correction requires actively surfacing the boring, high-frequency risks too.

## When NOT to Use

- For low-stakes judgments where the cost of an availability-driven misjudgment is trivial relative to the time cost of looking up base-rate data.
- When no reliable base-rate data exists for the category in question — in that case, flag the estimate as unusually uncertain rather than substituting a false precision from either the anecdote or a poorly-matched external rate.
- When the "example that comes to mind" is itself the direct, individually relevant case being assessed (e.g., a specific known defect in a specific known system) rather than a general frequency judgment being generalized from a memorable instance.

> For mental health concerns, consult a qualified mental health professional.
