---
name: apply-bayesian-network-inference
description: Use when reasoning about multiple interacting uncertain variables with a known or learnable dependency structure — medical diagnosis with several correlated symptoms and risk factors, fault diagnosis across interdependent system components, or any query about one variable given evidence on several others — by factoring the joint distribution as a directed acyclic graph and running network inference, rather than treating each variable as an independent single-hypothesis update.
source: 'Pearl "Probabilistic Reasoning in Intelligent Systems" (1988); Koller & Friedman "Probabilistic Graphical Models: Principles and Techniques" (2009); documented applications in medical diagnostic systems (QMR-DT, PathFinder), Microsoft''s spam-filtering and troubleshooting-wizard systems, and industrial fault-diagnosis and credit-risk graphical models'
tags: [bayesian-networks, graphical-models, probabilistic-inference, d-separation, mathematics, causal-diagrams]
related: [apply-bayesian-reasoning, apply-graph-theory-analysis, calculate-probability-distribution, apply-ladder-of-causation]
---

# Apply Bayesian Network Inference

Factor a joint probability distribution over many interacting variables as a directed acyclic graph of conditional probability tables, read independence directly off the graph's structure, and run network-inference algorithms to answer queries about any variable given evidence on any others.

## Why This Is Best Practice

**Adopted by:** Pearl's 1988 formulation underlies medical diagnostic systems such as QMR-DT and PathFinder, which model diseases and symptoms as a Bayesian network rather than independent single-hypothesis tests. Microsoft's spam-filtering systems and its troubleshooting-wizard diagnostics (used across Windows and Office support tooling) are built on Bayesian network inference over interacting evidence variables. Industrial fault-diagnosis systems and financial credit-risk models similarly use graphical-model structure to reason about many correlated risk factors at once.

**Impact:** Diagnostic systems built on Bayesian networks can update a probability for any variable (a disease, a fault, a risk factor) given evidence on any subset of the others — a query structure that scalar Bayesian updating cannot represent once more than one hypothesis-relevant variable interacts with the others. Because the network factors the joint distribution as a product of small conditional probability tables (one per node, conditioned only on its parents) rather than one full joint table over all variables, it makes inference over dozens of interacting variables computationally tractable where a naive full-joint representation would not be.

**Why best:** This is a genuine extension of, not a repackaging of, `apply-bayesian-reasoning`. That skill updates a single hypothesis H from one or more evidence streams treated as conditionally independent given H — P(H|E) for one H. Bayesian networks instead factor a joint distribution over N variables, P(X) = ∏ P(Xᵢ | parents(Xᵢ)), and read conditional independence directly off the graph's structure via d-separation — a structural test with no counterpart in scalar updating. Answering a query then requires a network-inference algorithm (variable elimination, belief propagation) rather than the log-odds sequential update `apply-bayesian-reasoning` uses for independent evidence into one hypothesis. Use `apply-bayesian-reasoning`'s content as the atom this skill builds on for any single-node update; use this skill specifically when the variables have a real dependency structure among themselves, not just independent evidence pointing at one hypothesis.

Sources: Pearl, *Probabilistic Reasoning in Intelligent Systems* (1988); Koller & Friedman, *Probabilistic Graphical Models* (2009).

## Steps

### 1. Identify the variables and draw the dependency structure

List every random variable relevant to the query, and draw a directed edge from each variable to every other variable it directly influences. The resulting graph must be acyclic — if a proposed edge would create a cycle, the dependency is misspecified and needs re-examination.

### 2. Specify a conditional probability table for each node

For each node, define P(node | its parents) — not the node's full joint probability with every other variable, only its distribution conditioned on its direct parents in the graph. This factorization, P(X) = ∏ P(Xᵢ | parents(Xᵢ)), is what makes the network tractable: each table is small (scaling with the number of parents, not the total number of variables).

```
Example — three nodes, disease D, test result T, symptom S (T and S each depend on D):
P(D, T, S) = P(D) × P(T|D) × P(S|D)
```

### 3. Populate the tables from data or expert elicitation

Learn conditional probability table parameters from historical data when enough is available (maximum likelihood or Bayesian parameter estimation over observed cases), or elicit them from domain experts when data is sparse — document which source was used for each table, since the two carry different confidence levels.

### 4. Use d-separation to read independence directly off the graph

Two variables are conditionally independent given a third set of variables if every path between them is "blocked" under the rules of d-separation (a chain or fork blocked by conditioning on the middle node; a collider blocked by NOT conditioning on it). This lets you determine which variables are relevant to a query and which can be ignored, without recomputing probabilities — a structural shortcut with no equivalent in single-hypothesis updating.

### 5. Choose an inference algorithm matched to the network's size and structure

| Method | Use when |
|---|---|
| Variable elimination | Small to moderate networks; exact inference, eliminate variables not in the query one at a time, summing over their values |
| Belief propagation / junction tree | Larger or more complex networks; exact inference via message-passing along a restructured tree of variable clusters |
| Gibbs sampling / MCMC over the network | Networks too large or complex for exact inference; approximate the posterior by sampling |

### 6. Query the network and validate the result

Compute P(variable of interest | observed evidence on other variables) using the chosen algorithm. Validate against known cases or held-out data where available, and check that the result changes sensibly when evidence is added or removed — a query that doesn't respond to new evidence in the expected direction usually indicates a structural or table-specification error.

## Rules

- The graph must be acyclic — a cyclic dependency indicates the causal/dependency structure is misspecified, not that the network needs a special cyclic-inference method.
- Each node's conditional probability table is conditioned only on its direct parents, not on every other variable — this factorization is what keeps the network tractable; collapsing it back into one full joint table defeats the purpose.
- Use d-separation to check independence claims structurally before assuming them — don't assume two variables are independent just because there's no direct edge between them; check whether a path through other variables is actually blocked.
- Match the inference algorithm to network size — exact inference (variable elimination, junction tree) for tractable networks, sampling-based approximate inference for networks too large or densely connected for exact methods.

## Examples

**Trigger:** A diagnostic system needs to estimate the probability of a disease given a symptom, a risk factor, and a test result, where the symptom and test result are each independently influenced by the disease but not by each other directly.
→ Build a network with the disease as a parent node and the symptom, risk factor, and test result each as child nodes conditioned on the disease (and on each other where a real direct dependency exists). Populate each conditional probability table from clinical data or expert estimates. Query P(disease | symptom present, test positive, risk factor present) via variable elimination, rather than trying to force this multi-variable structure into a sequence of independent single-hypothesis updates.

**Trigger:** An industrial fault-diagnosis system needs to identify which of several interacting components most likely caused an observed failure pattern.
→ Model each component's failure state as a node, with edges representing which components' failures influence others (e.g., a shared power supply feeding multiple components). Use d-separation to identify which observed sensor readings are actually informative about a given component's failure probability once other evidence is accounted for, and run belief propagation to compute each component's posterior failure probability given the full evidence pattern.

## Common Mistakes

- **Treating multiple interacting variables as independent evidence streams into one hypothesis.** If the variables genuinely depend on each other (not just all pointing at one hypothesis), forcing them into `apply-bayesian-reasoning`'s independent-evidence framework produces a materially wrong answer — the dependency structure has to be modeled explicitly.
- **Populating a node's conditional probability table using more variables than its actual graph parents.** This either duplicates information already captured elsewhere in the network or silently reintroduces the full-joint intractability the factorization was meant to avoid.
- **Assuming independence without checking d-separation.** Two variables can appear unrelated but still be dependent through an unblocked path via a third variable — or appear related but actually be independent once conditioned on a common cause. Check the graph structure, don't assume.
- **Using exact inference on a network too large or densely connected for it to be tractable.** Variable elimination and junction-tree methods can become computationally infeasible on large, densely connected networks — switch to sampling-based approximate inference rather than forcing an intractable exact computation.

## When NOT to Use

- When there's only one hypothesis and one or more genuinely independent evidence streams pointing at it — `apply-bayesian-reasoning`'s scalar updating is simpler and sufficient; building a network adds unneeded structure.
- When the variables' dependency structure is itself unknown and can't be reliably learned from available data or elicited from experts — an incorrectly specified graph produces confidently wrong answers; structure learning or a simpler model may be needed first.
- When the question is fundamentally about causal effects of an intervention (what happens if we deliberately change one variable) rather than about updating belief from observed evidence — that requires the causal-inference extensions (do-calculus) built on top of, but distinct from, standard Bayesian network inference.
