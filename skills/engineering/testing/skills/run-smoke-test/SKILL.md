---
name: run-smoke-test
description: Use when a build or deployment has just completed and needs verification before being declared done — actually run the built artifact in a realistic environment and check the core paths work, rather than treating a passing automated test suite as proof the real system functions, since the test harness and the real runtime environment can diverge in ways only actual execution reveals.
source: Post-deployment smoke testing as standard release-engineering practice documented at Google (Site Reliability Engineering book, release verification chapter), Amazon, and Netflix release-engineering blog posts; distinct from automated test-suite execution as a verification step specifically targeting environment/integration issues the test harness doesn't exercise
tags: [smoke-test, release-engineering, deployment-verification, testing, real-execution]
related: [apply-test-driven-development, design-load-test, apply-verification-status-reporting]
---

# Run Smoke Test

After a build or deployment completes, actually run the built artifact in a realistic environment and verify the core paths work — rather than treating a passing automated test suite alone as proof the real system functions, since the test harness and the actual runtime environment can diverge in ways only real execution reveals.

## Why This Is Best Practice

**Adopted by:** Post-deployment smoke testing is documented as standard release-engineering practice at Google (covered in the Site Reliability Engineering book's release-verification material), and is widely referenced in Amazon's and Netflix's release-engineering practices as a distinct verification step performed after a deployment, separate from the automated test suite that ran before it.

**Impact:** An automated test suite runs inside a test harness — with mocked dependencies, an isolated database, or a configuration that doesn't fully match production. A build can pass every automated test and still fail immediately in the real environment due to a missing environment variable, an unreachable external service, a misconfigured connection string, or a packaging error that never surfaces inside the test harness. Smoke testing catches exactly this category of failure by actually running the built artifact where it will really operate, immediately after deployment, before declaring the release complete.

**Why best:** This is a different verification layer than the automated test suite `apply-test-driven-development` builds and runs. A test suite verifies the code's logic against a controlled, often-mocked test environment; a smoke test verifies that the actual deployed artifact, running in its real environment with its real configuration and real dependencies, does the basic things it's supposed to do. Passing the former doesn't guarantee the latter — environment and integration issues are exactly the failure category a smoke test is designed to catch that a test suite, by construction, usually can't.

Sources: Google Site Reliability Engineering (release verification practices); Amazon and Netflix release-engineering documentation on post-deployment verification.

## Steps

### 1. Identify the core paths that must work immediately after deployment

Select a small number of critical, high-value paths through the real system — login, a core transaction, a key API endpoint responding correctly — not exhaustive coverage of every feature. Smoke testing is meant to be fast and targeted, not a replacement for the full test suite.

### 2. Run the smoke test against the actual deployed artifact, in its real environment

Execute the smoke test against the real running instance — the actual deployed build, with its real configuration, real network access, and real dependencies — not against a local build or a test-harness simulation of the environment.

### 3. Verify observable, end-to-end outcomes, not internal implementation details

Check outcomes a real user or client would observe — a successful login, a correct API response, a page that loads — rather than internal state a smoke test has no business inspecting; this keeps the smoke test fast, simple, and focused on the specific failure category it exists to catch.

### 4. Run the smoke test immediately after every deployment, not just occasionally

Make smoke testing a required, automatic step in the deployment pipeline immediately following every release — a smoke test that's run only occasionally or manually under time pressure misses exactly the deployments most likely to have gone wrong.

### 5. Fail fast and roll back or halt on smoke test failure

Treat a smoke test failure as a signal to halt the rollout or roll back immediately, before the deployment reaches more traffic or more users — the entire value of running it immediately after deployment depends on acting on its result immediately.

## Rules

- Run the smoke test against the real deployed artifact in its real environment — running it against a local build or a test-harness simulation defeats its purpose.
- Keep the smoke test small and fast, targeting only the highest-value core paths — this is not a substitute for full test-suite coverage, and trying to make it exhaustive slows down every deployment.
- Make smoke testing a required, automatic pipeline step, not an optional or manual one — a step that's skippable under time pressure will be skipped exactly when it matters most.
- Act immediately on a smoke test failure (halt or roll back) — running the check but not acting on its result provides no real protection.

## Examples

**Trigger:** A service passes its full automated test suite in CI, but a required environment variable is missing in the actual production deployment configuration.
→ The test suite, running against a test-harness configuration, never exercises the real production environment variables and doesn't catch this. A smoke test that actually starts the deployed service and checks a core endpoint responds correctly would fail immediately, catching the misconfiguration before it affects real traffic — which the test suite alone could not do.

**Trigger:** A team wants confidence that a newly deployed build actually works, beyond "the CI pipeline showed all green."
→ Add a required smoke-test step immediately after deployment that hits a small number of critical real endpoints (login, a core transaction) against the actual running instance. Gate further traffic rollout or promotion on the smoke test passing, and automatically halt/roll back if it fails.

## Common Mistakes

- **Treating a passing automated test suite as sufficient proof the deployed system works.** Test-harness execution and real-environment execution are different verification layers; passing one doesn't guarantee the other.
- **Making the smoke test exhaustive instead of fast and targeted.** An overly broad smoke test slows down every deployment and defeats the purpose of a quick, immediate post-deployment check.
- **Running the smoke test but not acting on a failure immediately.** A smoke test that's monitored only occasionally, or whose failures don't trigger an automatic halt/rollback, provides much weaker protection than one that's acted on immediately.
- **Running the smoke test against a local build or simulated environment instead of the actual deployed artifact.** This defeats the entire purpose — the failure category smoke testing exists to catch is specifically about real-environment divergence from the test harness.

## When NOT to Use

- As a substitute for a full automated test suite — smoke testing verifies a small number of critical paths in the real environment; it is not designed to catch the broad range of logic errors a comprehensive test suite catches.
- For verifying detailed business logic correctness — that's the automated test suite's job; smoke testing checks that the deployed system is basically up and functioning, not that every edge case behaves correctly.
- In environments with no meaningful distinction between the test harness and the real runtime environment — if there's genuinely no divergence risk, a separate smoke-test step adds process overhead without addressing a real failure mode.
