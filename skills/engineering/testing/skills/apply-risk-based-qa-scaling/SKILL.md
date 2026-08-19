---
name: apply-risk-based-qa-scaling
description: Use when deciding how much additional QA effort a specific code change warrants — route the decision through the change's actual risk profile (does it touch money, authentication, personal data, or concurrency?) to select which additional QA layers apply, rather than applying either a uniform minimum check to every change or an equally exhaustive review to changes with very different risk levels.
source: Risk-based test-effort allocation as documented in ISO/IEC/IEEE 29119 software testing standards and in risk-based testing practice broadly (e.g., Gerrard & Thompson "Risk-Based E-Business Testing"); the underlying principle — concentrate scarce QA effort where the cost of a defect is highest — is standard in software quality assurance and safety-critical engineering practice
tags: [risk-based-testing, qa-strategy, test-planning, code-review, engineering-process]
related: [design-test-strategy, design-load-test, design-contract-testing, run-chaos-engineering, design-security-logging, apply-property-based-testing, audit-test-coverage, apply-verification-volume-scaling]
---

# Apply Risk-Based QA Scaling

Route a code change's additional-QA decision through its actual risk profile — does it touch money, authentication, personal data, or concurrency? — to select which additional QA layers apply, rather than giving every change the same minimum check or the same exhaustive review regardless of how different their risk levels actually are.

## Why This Is Best Practice

**Why best:** QA effort is a limited resource. Applying the same shallow minimum check to every change under-scrutinizes the small number of changes where a defect would be most costly (money handling, authentication, data integrity, concurrency bugs); applying the same exhaustive review to every change wastes scarce reviewer and QA time on low-risk changes that didn't need it. Explicitly routing the decision through the change's risk profile concentrates effort where a defect's cost is actually highest.

**Adopted by:** Risk-based test-effort allocation is documented in the ISO/IEC/IEEE 29119 software testing standards and in risk-based testing methodology broadly — the practice of scaling test depth and additional QA layers to the assessed risk of a specific change, rather than a uniform standard, is a recognized discipline in software quality assurance and is especially standard practice in safety-critical and financial-systems engineering.

**Impact:** Changes that touch money, authentication, personal data, or concurrency carry a systematically higher cost when something goes wrong — a payment bug, an auth bypass, a data leak, or a race condition can have consequences far beyond a typical UI bug. Concentrating additional QA layers (load testing, contract testing, chaos/fault-injection testing, security-logging review, mutation testing) specifically on changes with these risk characteristics, rather than spreading the same fixed effort evenly across all changes, directs scrutiny to where defects are both more likely to be introduced unnoticed and more expensive when they are.

**Why best (continued):** This is a composing skill, not a new testing technique — it doesn't introduce a new QA method itself, it routes a change's assessed risk category to the existing, already-atomic QA skills in this repo (`design-load-test` for performance-critical changes, `design-contract-testing` for API-boundary changes, `run-chaos-engineering` for concurrency/fault-tolerance concerns, `design-security-logging` for auth/data-sensitive changes, `apply-property-based-testing`/`audit-test-coverage`'s mutation testing for correctness-critical logic) rather than duplicating their content.

Sources: ISO/IEC/IEEE 29119 software testing standards; Gerrard & Thompson, *Risk-Based E-Business Testing*; risk-based testing practice in safety-critical software engineering.

## Steps

### 1. Assess the change's risk category

Determine whether the change touches one or more of the higher-risk categories: money/financial transactions, authentication/authorization, personal or sensitive data, or concurrency/shared-state. A change can fall into more than one category.

### 2. Route each identified risk category to its matched QA layer

| Risk category | Additional QA layer to apply |
|---|---|
| Performance-critical / high-traffic path | `design-load-test` |
| Cross-service API boundary | `design-contract-testing` |
| Concurrency, fault tolerance, distributed failure modes | `run-chaos-engineering` |
| Authentication, authorization, sensitive-data handling | `design-security-logging` (and relevant security-review skills) |
| Correctness-critical business logic (money, calculations) | Mutation testing via `audit-test-coverage`; consider `apply-property-based-testing` for invariant-heavy logic |

### 3. Apply only the minimum baseline QA for changes with no elevated risk category

Changes that don't touch any of the higher-risk categories don't need the full menu of additional QA layers — apply the team's standard baseline (unit tests, standard code review) without adding unnecessary process overhead to low-risk changes.

### 4. Document which risk categories were identified and which QA layers were applied

Record the risk assessment and the resulting QA layers applied as part of the change's review record — this makes the scaling decision auditable and lets a later reviewer confirm the right layers were actually applied, rather than trusting an unrecorded judgment call.

### 5. Re-assess when a change's scope expands mid-review

If a change that started in a low-risk category grows to touch a higher-risk area during development, re-run the risk assessment and add the matched QA layers rather than QA-ing the change only against its original, narrower scope.

## Rules

- Assess risk category explicitly before deciding QA depth — don't default to either a uniform minimum or a uniform maximum without checking what the specific change actually touches.
- Route each identified risk category to its matched existing QA skill rather than inventing an ad hoc check each time — this keeps the additional QA layers consistent and complete.
- Document the risk assessment and applied QA layers as part of the review record, not as an unrecorded judgment call.
- Re-assess risk if a change's scope expands during development — the original risk assessment is only valid for the original scope.

## Examples

**Trigger:** A pull request adds a new field to a user-profile settings page with no financial, authentication, or concurrency implications.
→ Assess risk: no elevated risk category applies. Apply the standard baseline (unit tests, standard code review) without adding load testing, contract testing, or chaos testing — the change doesn't warrant that additional effort.

**Trigger:** A pull request modifies the payment-processing service's transaction-handling logic, which also involves concurrent access to a shared balance record.
→ Assess risk: this touches both money and concurrency. Route to mutation testing (via `audit-test-coverage`) for the transaction logic's correctness, and to `run-chaos-engineering` for the concurrent-access failure modes — applying both matched QA layers rather than treating this as a routine change warranting only the standard baseline.

## Common Mistakes

- **Applying the same fixed QA checklist to every change regardless of risk.** This either under-scrutinizes high-risk changes or wastes effort on low-risk ones — the whole point of risk-based scaling is that the two shouldn't get the same treatment.
- **Assessing risk informally and not recording the decision.** An unrecorded judgment call about QA depth can't be audited or corrected later, and different reviewers may apply the scaling inconsistently.
- **Failing to re-assess when a change's scope grows.** A change that started low-risk and expanded into a higher-risk area needs its QA scaling re-evaluated, not grandfathered into its original assessment.
- **Inventing ad hoc checks instead of routing to the existing matched QA skill.** This produces inconsistent, incomplete QA layers instead of reliably applying the full, already-defined technique for that risk category.

## When NOT to Use

- For teams or projects too small to meaningfully differentiate risk categories, or where every change already receives the same thorough review by necessity — the overhead of formal risk categorization may exceed its benefit at very small scale.
- As a substitute for the underlying QA skills themselves — this skill only routes risk categories to the right existing technique; it doesn't replace the actual execution of `design-load-test`, `run-chaos-engineering`, or the other referenced skills.
- For risk categories not covered by any existing QA layer — if a genuinely novel risk category emerges with no matched technique in this repo, that's a signal a new atomic QA skill may be needed, not that this routing skill should absorb the content itself.
