---
name: audit-diff-coverage
description: Use when reviewing a pull request or code change for test adequacy — measure test coverage specifically on the lines changed in that diff, not whole-file or whole-codebase coverage, since a codebase can have high aggregate coverage while the specific lines just added or modified are completely untested.
source: diff-cover (Python, widely used in CI pipelines to gate PRs on patch coverage); Codecov and Coveralls "patch coverage" / diff-coverage gating features, adopted broadly across GitHub- and GitLab-integrated CI at organizations using either service; distinct metric from whole-file coverage as documented in Martin Fowler's "TestCoverage" analysis of what coverage percentages do and don't tell you
tags: [diff-coverage, patch-coverage, code-review, testing, ci, pull-request]
related: [audit-test-coverage, apply-test-driven-development]
---

# Audit Diff Coverage

Measure test coverage specifically on the lines changed in a given diff or pull request, rather than relying on whole-file or whole-codebase coverage, since aggregate coverage can stay high while newly added or modified lines are completely untested.

## Why This Is Best Practice

**Adopted by:** `diff-cover` is a widely used Python tool integrated into CI pipelines specifically to gate pull requests on patch/diff coverage rather than aggregate coverage. Codecov and Coveralls — two of the most widely adopted coverage-reporting services integrated into GitHub and GitLab CI — both offer "patch coverage" or diff-coverage gating as a distinct, commonly-enabled check separate from overall repository coverage.

**Impact:** A codebase with 85% aggregate test coverage can still merge a pull request whose new or changed lines are 0% covered — the aggregate number is diluted by the large, already-tested body of existing code, hiding the fact that the actual change under review has no test verification at all. Diff coverage surfaces exactly this gap by scoping the coverage measurement to only the lines that changed, which is the part of the codebase the current review actually needs to verify.

**Why best:** `audit-test-coverage` measures and improves coverage at the whole-file or whole-module level — a genuinely different, complementary metric. Diff coverage answers a different, narrower question: "is the change I'm reviewing right now adequately tested?" — which whole-codebase coverage percentages cannot answer on their own, since a large well-tested codebase can absorb a completely untested new change without moving the aggregate number enough to notice.

Sources: `diff-cover` documentation; Codecov and Coveralls patch-coverage features; Fowler, "TestCoverage" (martinfowler.com).

## Steps

### 1. Identify the diff scope

Determine exactly which lines were added or modified in the change under review — this is the scope diff coverage measures against, distinct from the file's or module's full line count.

### 2. Run coverage measurement scoped to the diff

Use a diff-coverage tool (`diff-cover`, or a CI service's patch-coverage feature) to compute what percentage of the changed lines are exercised by the test suite, rather than reading the aggregate coverage report and assuming it reflects the new change.

### 3. Set a diff-coverage threshold distinct from the aggregate coverage threshold

Enforce a minimum diff-coverage percentage (often higher than the aggregate threshold — many teams require 80-100% coverage on new/changed lines specifically) as a required CI check on pull requests, independent of what the aggregate coverage threshold is set to.

### 4. Investigate any uncovered changed lines before merging

For any changed line not covered by the test suite, determine whether it needs a test (most cases) or is legitimately untestable/trivial (e.g., a logging statement) — don't treat every red diff-coverage line as automatically requiring a test, but don't wave all of them through either.

### 5. Don't let high aggregate coverage substitute for diff-coverage review

Treat diff coverage as a required, separate signal on every pull request — a codebase's already-high aggregate coverage says nothing about whether today's specific change is tested.

## Rules

- Measure coverage on the diff, not just the whole file or module — a file's overall coverage percentage can mask an untested new addition to that same file.
- Set the diff-coverage threshold independently from the aggregate coverage threshold — many teams intentionally require a higher bar on new/changed code than the codebase's historical aggregate.
- Investigate, don't automatically dismiss or automatically require tests for, every uncovered changed line — some are legitimately trivial, but most represent a real gap.

## Examples

**Trigger:** A pull request adds a new function to a file that already has 90% test coverage overall.
→ Run diff coverage on the PR specifically. If the new function's lines show 0% diff coverage despite the file's 90% aggregate, the aggregate number was masking a genuinely untested addition — require tests for the new function before merging, regardless of the file's historical coverage.

**Trigger:** A team's CI pipeline currently only reports whole-repository coverage percentage.
→ Add a diff-coverage gate (via `diff-cover` or the CI-integrated coverage service's patch-coverage feature) as a required check on pull requests, with its own threshold — this catches untested new code that the aggregate repository-wide number would never flag on its own.

## Common Mistakes

- **Relying only on aggregate coverage and assuming it reflects new changes.** A large, well-tested codebase can absorb an untested new change without the aggregate percentage moving enough to notice.
- **Setting the diff-coverage threshold equal to or lower than the aggregate threshold.** Many teams intentionally set diff coverage higher, since new code should meet a higher bar than the historical average the aggregate reflects.
- **Treating every uncovered changed line as automatically requiring a test, with no judgment.** Some changed lines are legitimately trivial (a log line, a comment) — audit for that distinction rather than mechanically demanding 100% on every diff.
- **Only running diff coverage locally/manually instead of enforcing it as a required CI check.** A voluntary, unenforced check is easy to skip under time pressure — gate merges on it in CI.

## When NOT to Use

- For assessing the overall health of a codebase's test suite over time — use `audit-test-coverage` for that; diff coverage is scoped to individual changes, not the codebase as a whole.
- For a codebase or team not yet using any automated coverage measurement at all — establish basic aggregate coverage tracking first before adding a diff-scoped gate on top of it.
- For trivial, non-functional changes (formatting-only diffs, comment updates) where no test coverage is meaningfully applicable to the changed lines.
