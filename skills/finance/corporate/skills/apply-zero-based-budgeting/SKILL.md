---
name: apply-zero-based-budgeting
description: Use when restructuring a business's cost base during a turnaround, margin-improvement initiative, or annual budget cycle — building every expense line from a zero baseline and requiring explicit justification, rather than incrementally adjusting last year's budget forward.
source: Peter Pyhrr, "Zero-Base Budgeting", Harvard Business Review (1970) — originated at Texas Instruments; adopted by Jimmy Carter's Georgia state government (1971) and later the U.S. federal government under Carter's presidency; modern private-equity revival at 3G Capital (Kraft Heinz, Anheuser-Busch InBev)
tags: [cost-restructuring, budgeting, zero-based-budgeting, margin-improvement, turnaround, corporate-finance, cost-management]
related: [design-cost-allocation-system, calculate-break-even-analysis, apply-theory-of-constraints, design-cash-flow-forecast]
---

# Apply Zero-Based Budgeting

Rebuild every budget line from a zero baseline each cycle, requiring explicit justification for every expense, rather than incrementally adjusting the prior period's budget forward — surfacing costs that persist purely from institutional inertia.

## Why This Is Best Practice

**Adopted by:** Peter Pyhrr developed zero-based budgeting at Texas Instruments in the late 1960s; Jimmy Carter, then Governor of Georgia, adopted it statewide in 1971 and later brought it to U.S. federal budgeting during his presidency. It has seen a modern revival as a private-equity cost-restructuring tool, most visibly at 3G Capital's portfolio companies including Kraft Heinz and Anheuser-Busch InBev, where it was applied systematically across acquired businesses to reset cost bases.

**Impact:** ZBB's central mechanism — decision packages ranked by value rather than expenses inherited from the prior year's baseline — routinely surfaces spending that survives purely because "that's what was budgeted last year," not because it's currently justified. 3G Capital's application at Kraft Heinz and AB InBev is documented to have produced substantial, rapid margin improvement in the years immediately following acquisition, by forcing every cost center to justify its budget from zero rather than negotiating an incremental increase.

**Why best:** This is a different tool than the cost skills already in this repo. `design-cost-allocation-system` (activity-based costing) makes existing costs visible and correctly attributed — it doesn't force a rebuild of the budget itself. `calculate-break-even-analysis` and unit-economics calculators are diagnostic math, not a budget-construction process. `apply-theory-of-constraints` targets throughput bottlenecks, not the cost base. ZBB is specifically a budget-construction methodology: incremental budgeting inherits and compounds unjustified spend indefinitely; ZBB resets the justification burden to zero every cycle, which is the only one of these mechanisms that directly attacks entrenched, un-rejustified cost.

Sources: Pyhrr, "Zero-Base Budgeting," *Harvard Business Review* (1970); Pyhrr, *Zero-Base Budgeting: A Practical Management Tool for Evaluating Expenses* (1973); documented 3G Capital ZBB application at Kraft Heinz and Anheuser-Busch InBev.

## Steps

1. **Define decision units.** Break the organization into discrete cost centers or activities ("decision units") — a department, a program, a product line — each of which will build its own budget from zero rather than inheriting last year's figure.

2. **Build a decision package for each decision unit.** For every decision unit, require an explicit justification package: what the spend accomplishes, what happens if it's cut entirely, and at minimum one lower-cost alternative way to accomplish the same objective (a reduced-scope version of the same activity).

3. **Rank all decision packages by value, across the whole organization.** Rather than approving each department's budget in isolation, rank every decision package from every unit together, so the highest-value spending across the entire organization is funded first regardless of which department it sits in.

4. **Set the funding cutoff at the actual available budget, not the prior year's total.** Fund packages top-down from the ranked list until the available budget is exhausted — spend that ranks below the cutoff is cut, even if it was funded in every prior year.

5. **Require re-justification every cycle, not just once.** The discipline only works if it repeats — a single one-time ZBB exercise reverts to incremental budgeting the following year unless the zero-baseline requirement is genuinely repeated each cycle.

6. **Watch for review fatigue and rubber-stamping.** ZBB is resource-intensive to run properly; if the organization starts approving packages without genuine scrutiny to save review time, the exercise degrades back into incremental budgeting with extra paperwork.

## Rules

- Every decision package must include at least one lower-cost alternative, not just a justification for the status quo spend level — forcing an alternative is what prevents rubber-stamped justification.
- Rank packages across the whole organization, not department by department — ranking within a silo just reproduces each department's own incremental habits.
- Re-run the zero-baseline requirement every cycle — a one-time ZBB exercise doesn't compound; the value comes from repeated re-justification.

## Examples

**Trigger:** A company post-acquisition needs to reset an inherited cost structure that grew through years of incremental annual increases.
→ Break the organization into decision units (each function/department). Require each to submit a decision package justifying its spend from zero, with at least one reduced-scope alternative. Rank all packages company-wide by value. Fund top-down to the available budget — this is the mechanism 3G Capital applied at Kraft Heinz to reset an inherited, incrementally-grown cost base.

**Trigger:** An annual budget cycle has become a negotiation over percentage increases from last year's baseline, with no one revisiting whether the underlying spend is still justified.
→ Replace the incremental negotiation with zero-based decision packages — every cost center justifies its full budget from zero this cycle, not just the requested increase over last year.

## Common Mistakes

- **Treating ZBB as a one-time exercise.** The value comes from repeating the zero-baseline discipline every cycle; running it once and reverting to incremental budgeting the following year forfeits most of the ongoing benefit.
- **Ranking decision packages within department silos instead of across the whole organization.** This just reproduces each department's own defensive budgeting habits rather than surfacing genuinely low-value spend anywhere in the organization.
- **Letting review fatigue turn justification into rubber-stamping.** ZBB's rigor is expensive to sustain — without real scrutiny of each package, the process becomes incremental budgeting with extra steps.
- **Applying ZBB indiscriminately to investment that needs a longer horizon to pay off.** Cutting anything that doesn't show immediate value can gut genuine long-cycle investment (R&D, brand-building) that a single-cycle justification window can't fairly evaluate.

## When NOT to Use

- Investment areas with long payback horizons that a single annual justification cycle can't fairly evaluate — ZBB applied indiscriminately to R&D or brand-building budgets has been blamed for underinvestment in some of its documented private-equity applications.
- Organizations that can't sustain the review rigor ZBB requires — a resource-intensive process run without real scrutiny degrades into rubber-stamped incremental budgeting with extra overhead.
- Very small organizations or cost bases where the overhead of building and ranking decision packages exceeds any plausible savings from the exercise.

---

> **Finance disclaimer:** This skill encodes professional best practices for educational purposes. It is not financial advice. Consult a licensed financial advisor before making investment decisions.
