---
name: apply-property-based-testing
description: Use when a function or module has an invariant that should hold across a wide range of inputs — not just the handful of specific cases an example-based test happens to cover — such as "encoding then decoding always returns the original value" or "sorting a list never changes its length"; generate many random inputs, assert the invariant holds for all of them, and let the framework automatically shrink any failing case to a minimal reproduction.
source: 'Claessen & Hughes "QuickCheck: A Lightweight Tool for Random Testing of Haskell Programs" (ICFP, 2000); Hypothesis (Python) and fast-check (JavaScript/TypeScript) as widely adopted modern implementations; documented industry use at Jane Street (OCaml property testing as a core QA discipline) and broad adoption of fast-check/Hypothesis across JS and Python testing ecosystems'
tags: [property-based-testing, quickcheck, invariant-testing, testing, fuzzing, shrinking]
related: [apply-test-driven-development, audit-test-coverage, write-unit-test]
---

# Apply Property-Based Testing

Test an invariant that should hold across a wide range of inputs by generating many random inputs and asserting the invariant holds for all of them, rather than writing individual example-based test cases for each input you happen to think of.

## Why This Is Best Practice

**Adopted by:** QuickCheck, introduced for Haskell by Claessen & Hughes in 2000, established property-based testing as a distinct testing discipline from example-based unit testing. Modern implementations — Hypothesis for Python and fast-check for JavaScript/TypeScript — have broad adoption across their respective ecosystems' testing practices. Jane Street, an OCaml-heavy trading firm, has documented property-based testing as a core part of its QA discipline for correctness-critical financial code.

**Impact:** Property-based testing systematically explores the input space a fixed set of example-based tests never reaches — edge cases like empty collections, extreme values, or unusual character encodings that a developer wouldn't think to write examples for are found automatically by the generator. When a property-based test finds a failing case, the framework's shrinking algorithm automatically reduces it to a minimal reproduction, turning a complex random failure into a small, debuggable example rather than requiring the developer to manually isolate the cause.

**Why best:** Example-based tests (`write-unit-test`) only test the specific inputs a developer chose to write — they can't verify a claim like "this holds for all valid inputs," only "this holds for these 5 inputs I thought of." Property-based testing instead tests the actual universal claim by generating a large, varied sample of inputs and checking the invariant against each one, catching violations that specific hand-picked examples would never surface. This is a different mechanism than `apply-test-driven-development`'s red-green-refactor cycle, which is compatible with either example-based or property-based test-writing — property-based testing changes what kind of assertion is being tested, not the development cycle around it.

Sources: Claessen & Hughes, *QuickCheck* (ICFP, 2000); Hypothesis and fast-check documentation as modern reference implementations.

## Steps

### 1. Identify an invariant, not just an example

State the property that should hold across a range of inputs, not a specific input-output pair:

```
Example-based claim: encode("hello") == "aGVsbG8="
Property-based claim: for any string s, decode(encode(s)) == s
```

The property-based claim is the stronger, more general statement — it's what you actually want to be true, of which the example is just one instance.

### 2. Choose the right kind of property

| Property type | Example |
|---|---|
| Round-trip | `decode(encode(x)) == x` |
| Invariant preservation | `sort(list)` has the same length as `list` |
| Idempotence | `normalize(normalize(x)) == normalize(x)` |
| Commutativity / associativity | `add(a, b) == add(b, a)` |
| Comparison against a simpler reference implementation | A fast, complex implementation should agree with a slow, obviously-correct one on the same inputs |

Not every function has an obvious property — for pure business logic with no clean mathematical structure, example-based testing may remain more appropriate.

### 3. Define the input generator

Specify what kind of random inputs the framework should generate — a range of integers, strings matching a pattern, lists of a given element type, or a composite generator combining several of these. Constrain the generator to the actual valid input domain, or the test will spend most of its effort on inputs the function was never meant to handle.

### 4. Run the test and let the framework shrink failures automatically

When a generated input causes the property to fail, the framework doesn't just report the large, complex random input — it automatically searches for a smaller, simpler input that still triggers the same failure (shrinking), giving a minimal reproduction to debug from rather than the original complex counterexample.

### 5. Add the specific failing case as a permanent regression example

Once a property-based test finds and the code is fixed for a specific failing case, add that minimal shrunk case as a fixed example-based regression test — this guards against the same specific bug recurring even if the random generator doesn't happen to regenerate that exact input again.

## Rules

- State the property as a general claim about a class of inputs, not as a specific input-output pair — if it can only be expressed as one example, it isn't a property.
- Constrain the input generator to the function's actual valid domain — an unconstrained generator wastes test runs on inputs the function was never designed to accept.
- Always add a fixed regression test for any specific case a property-based test found failing — the random generator finding it once doesn't guarantee it will find it again.
- Don't force property-based testing onto logic with no clean invariant — business logic with many special cases and no general mathematical structure is often better served by example-based tests.

## Examples

**Trigger:** A serialization function needs to be verified against a wide range of input data, not just a handful of chosen examples.
→ Define the round-trip property: for any valid input object, `deserialize(serialize(x)) == x`. Generate a wide range of input objects (varying nested structure, string content, numeric edge cases). Run the property test; if it finds a failing input, let the framework shrink it to a minimal reproduction, fix the bug, and add that specific minimal case as a permanent regression test.

**Trigger:** A sorting function's correctness needs to be verified beyond a few example lists.
→ Define multiple properties: the output has the same length as the input, the output is in non-decreasing order, and every element in the input appears the same number of times in the output. Generate random lists of varying length and content, including edge cases like empty lists and lists with duplicate elements, and verify all three properties hold across the generated inputs.

## Common Mistakes

- **Writing a property that's actually just a restated example.** If the "property" only holds for one specific input, it isn't a property-based test — write it as an example-based test instead.
- **Leaving the input generator unconstrained relative to the function's actual valid domain.** This wastes test effort generating inputs the function was never meant to accept and produces irrelevant "failures" on invalid inputs.
- **Not adding a fixed regression test after a property-based test finds a real bug.** The random generator finding the bug once doesn't guarantee it will find the same bug again in a future run.
- **Trying to force a property-based test onto logic with no genuine invariant.** Some business logic genuinely has no clean mathematical property — forcing an artificial one produces a weak or misleading test.

## When NOT to Use

- For logic with no identifiable general invariant — many-special-case business logic is often better tested with targeted example-based tests (`write-unit-test`) than with a forced, artificial property.
- When the function's behavior is inherently tied to specific, known real-world scenarios rather than a general mathematical claim — example-based tests documenting those specific scenarios are more directly useful.
- For UI or integration-level testing where the system under test doesn't have a clean, testable functional boundary — property-based testing works best on pure or near-pure functions with a well-defined input/output relationship.
