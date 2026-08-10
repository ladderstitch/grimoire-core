---
name: apply-verification-status-reporting
description: Use when reporting the results of tests, checks, or any automated or manual verification step — explicitly label any result you have not actually observed running as unverified rather than presenting it as passing, and never weaken a test's assertion or scope just to make it pass, since a reporting discipline that silently conflates "unverified" with "passing" destroys the reliability of every report built on it.
source: Standard software-engineering release-verification and CI-reporting discipline — the principle that a check's reported status must reflect what was actually executed and observed, distinct from claiming or assuming a result; the same discipline underlies why weakening an assertion to force a passing test is treated as a serious defect in code review practice (e.g., Google's code review culture as documented in "Software Engineering at Google", Winters, Manshreck & Wright, O'Reilly 2020) rather than a legitimate way to resolve a failing check
tags: [verification, reporting-integrity, testing, ci, engineering-discipline]
related: [apply-test-driven-development, apply-beyonce-rule, run-smoke-test]
---

# Apply Verification Status Reporting

Explicitly label any result you have not actually observed running as unverified rather than presenting it as passing, and never weaken a test's assertion or scope just to force it to pass — a reporting discipline that conflates "unverified" with "passing" destroys the reliability of every report built on it.

## Why This Is Best Practice

**Why best:** A verification report — a test suite result, a code-review checklist, an automated agent's summary of what it checked — is only useful if its "passed" status means the thing was actually run and actually observed to behave correctly. The moment "unverified" and "passed" become indistinguishable in a report, every downstream decision based on that report (merge this code, ship this release, trust this check) is being made on false confidence, and the report's entire value collapses regardless of how good the underlying work actually was.

**Adopted by:** The discipline of treating a weakened or disabled assertion as a defect, not a legitimate fix, is documented in Google's engineering culture (*Software Engineering at Google*, Winters, Manshreck & Wright, 2020) — a test that's been modified to pass by loosening what it actually checks is treated the same as a genuinely failing test, because it no longer verifies what it claims to verify. The same principle underlies standard CI reporting practice broadly: a check's reported result is expected to reflect what was actually executed, not an assumption or an unverified claim presented as if it were.

**Impact:** Reports that silently present unverified or weakened results as passing produce a specific, predictable failure: problems that were never actually caught get treated as resolved, and the gap is only discovered later, at a point where it's more expensive to fix and harder to trace back to its actual cause. A reporting discipline that requires explicit "unverified" labeling and forbids assertion-weakening surfaces exactly this gap at the point it's cheapest to address — before the report is trusted and acted on.

Sources: *Software Engineering at Google* (Winters, Manshreck & Wright, 2020); standard CI/release-verification reporting practice.

## Steps

### 1. Distinguish "observed passing" from "not run" or "assumed"

Before reporting any check's status, confirm whether it was actually executed and its result actually observed, versus skipped, not run in this context, or assumed based on similar past results — these are different states and must be reported differently.

### 2. Label anything not actually observed as "unverified," not as passing

If a check wasn't run, couldn't be run, or its result wasn't actually observed, report it explicitly as unverified — never let an unverified item default into looking like a pass simply because it wasn't flagged as a failure.

### 3. Never weaken an assertion or narrow a check's scope solely to make it pass

If a test or check is failing, the correct responses are: fix the underlying issue, or explicitly and visibly change what's being verified with a documented reason — not quietly loosen the assertion so the same check reports success while verifying less than it used to.

### 4. Disclose when required approval or sign-off hasn't occurred

If a process requires a human or a specific role to review or approve something before it's considered complete, and that approval hasn't happened, state this explicitly in the report rather than presenting the item as done.

### 5. Make the unverified/weakened-check state visible, not buried

Report unverified items and any changes to a check's scope prominently, in the same report as the pass/fail summary — burying this information in a separate log or requiring someone to dig for it defeats the purpose of disclosing it at all.

## Rules

- Never present an unverified result as passing — if it wasn't actually observed running and succeeding, it's unverified, and must be labeled as such.
- Never weaken an assertion or narrow a check's scope solely to force a pass — fix the actual issue, or document an explicit, visible, justified change to what's being verified.
- Disclose missing required approvals or sign-offs explicitly — don't let an unapproved item look complete by omission.
- Make unverified/weakened-check disclosures prominent in the report itself, not buried where they're unlikely to be seen.

## Examples

**Trigger:** An automated coding agent completes a task but couldn't run one specific check due to a missing dependency in its environment.
→ Report that specific check as "unverified — could not run due to missing dependency," not as passing and not by silently omitting it from the summary. This gives whoever reviews the report accurate information to decide whether that gap matters before trusting the result.

**Trigger:** A test is failing because the code has a genuine bug, and there's pressure to get the check green quickly.
→ Fix the underlying bug the test is correctly catching, rather than loosening the test's assertion or narrowing its scope to make it pass. If the test itself is genuinely wrong (testing the wrong behavior), change it explicitly and visibly with a documented reason — don't quietly weaken it to make the failure disappear.

## Common Mistakes

- **Letting an unrun or unobserved check default to looking like a pass.** Silence isn't a report — anything not actually verified needs an explicit "unverified" label, or it will be read as "passed" by anyone consuming the report.
- **Weakening a failing assertion to make it pass instead of fixing the underlying issue.** This produces a report that says "verified" while verifying less than it used to, which is worse than an honest failure.
- **Burying disclosure of unverified items in a separate log instead of the main report.** If finding the caveat requires extra digging, most readers will never see it and will treat the item as fully verified.
- **Treating "no human approved this yet" as equivalent to "approved."** Omitting a required-but-missing approval from a report misrepresents the item's actual status.

## When NOT to Use

- For informal, low-stakes personal notes with no downstream audience relying on the report's accuracy — the discipline exists specifically to protect decisions made by others based on the report.
- When a check is genuinely optional and explicitly marked as such from the start — the concern here is about disguising unverified/weakened results as verified ones, not about making every optional item mandatory.
