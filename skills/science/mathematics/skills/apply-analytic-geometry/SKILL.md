---
name: apply-analytic-geometry
description: Use when a geometric problem — distance, intersection, locus, optimization, or a claim about points, lines, and curves — is better solved by assigning coordinates and manipulating algebraic equations than by classical synthetic/axiomatic proof, including distance/midpoint/slope calculations and vector-based angle, area, and plane computations.
source: 'Descartes, "La Géométrie" (1637) — the founding text unifying algebra and geometry via coordinates; Fermat''s independent contemporaneous coordinate methods; modern industrial applications: CAD/CAM systems, GPS/GIS coordinate computation, and computer-graphics intersection/collision testing all rely directly on this method'
tags: [analytic-geometry, coordinate-geometry, cartesian, vectors, mathematics, descartes]
related: [apply-linear-algebra-methods, apply-conic-section-properties, apply-graph-theory-analysis]
---

# Apply Analytic Geometry

Translate a geometric problem into coordinates and algebraic equations, solve it with algebra, and translate the result back into a geometric conclusion — rather than constructing a classical synthetic proof directly from geometric axioms.

## Why This Is Best Practice

**Why best:** Descartes' method converts geometric problems — distance, intersection, locus, optimization — into algebra, where standard equation-solving techniques apply directly. A synthetic proof must be constructed fresh for each specific configuration; an algebraic approach via coordinates generalizes immediately (the same distance formula, the same line equation, the same intersection-by-substitution method) across configurations that would each require a distinct classical construction.

**Adopted by:** Every modern CAD/CAM system computes part geometry, tool paths, and collision boundaries via coordinate equations rather than synthetic construction. GPS and GIS systems compute distances, bearings, and intersections of geographic features entirely in coordinate form. Computer graphics engines test ray-object intersection and collision detection by solving the coordinate equations of the relevant surfaces. All of this traces directly to Descartes' 1637 unification of algebra and geometry, developed independently and around the same time by Pierre de Fermat.

**Impact:** Coordinate methods made problems that resisted synthetic proof for centuries — general conic-intersection problems, optimization of geometric quantities, loci defined by algebraic conditions — solvable by routine algebraic manipulation. The same coordinate framework underlies virtually all applied geometric computation today, from engineering CAD to satellite navigation, precisely because it replaces case-by-case geometric construction with a uniform algebraic procedure.

Sources: Descartes, *La Géométrie* (1637); modern applications in CAD/CAM, GPS/GIS, and computer graphics as evidence of continued industry reliance on the method.

## Steps

### 1. Assign a coordinate system

Place an origin and axes to exploit the problem's structure — center a circle at the origin, align an axis with a given line, or place a right angle at the origin — since a well-chosen coordinate placement reduces the algebra needed in every subsequent step.

### 2. Represent each geometric object as an equation

| Object | Coordinate representation |
|---|---|
| Point | (x, y) or (x, y, z) |
| Line (2D) | y = mx + b, or ax + by = c |
| Line (3D, parametric) | (x, y, z) = (x₀, y₀, z₀) + t(a, b, c) |
| Circle | (x − h)² + (y − k)² = r² |
| Plane (3D) | ax + by + cz = d |

### 3. Apply the standard coordinate formulas

```
Distance between two points:      d = √[(x₂−x₁)² + (y₂−y₁)²]
Midpoint:                          M = ((x₁+x₂)/2, (y₁+y₂)/2)
Slope of a line:                   m = (y₂−y₁)/(x₂−x₁)
Point-slope line equation:         y − y₁ = m(x − x₁)
```

### 4. Use vectors for angle, area, and plane calculations

```
Dot product (angle between vectors):    a·b = |a||b|cos(θ)  →  θ = arccos(a·b / (|a||b|))
Cross product (area, normal to a plane): |a×b| = area of parallelogram spanned by a, b
Plane through a point with normal n:     n·(r − r₀) = 0
Distance from a point to a plane:        |n·(P − P₀)| / |n|
```

These vector operations extend the coordinate method to angle, area, and orientation questions that pure point/line-equation algebra doesn't directly answer.

### 5. Solve the resulting algebraic system

Translate the geometric question — "do these two curves intersect," "what point minimizes this distance," "what set of points satisfies this condition" — into an algebraic equation or system, and solve it with standard algebraic techniques (substitution, elimination, calculus for optimization).

### 6. Translate the algebraic result back into a geometric conclusion

Confirm what the algebraic solution means geometrically — how many intersection points, what curve the locus traces, what geometric configuration the optimum corresponds to — since the algebra alone doesn't automatically state the geometric answer the original problem asked for.

## Rules

- Choose the coordinate system to exploit the problem's symmetry — a poor origin/axis choice makes the algebra unnecessarily complex without changing the answer.
- Keep the algebraic and geometric interpretations linked throughout — translate back to a geometric statement at the end, not just an algebraic result.
- Use vector methods (dot/cross product) for angle, area, and plane/normal questions rather than trying to force them into pure point/line-equation algebra.

## Examples

**Trigger:** Determine whether three given points are collinear.
→ Assign coordinates to the three points. Compute the slope between the first two and the slope between the second two (or equivalently, check whether the vectors between the points are parallel via the cross product being zero). If the slopes match (or the cross product is zero), the points are collinear — an algebraic test replacing a synthetic argument about the points lying on one line.

**Trigger:** Find the point on a given line closest to a given external point.
→ Represent the line in coordinate form and the external point's coordinates. Set up the distance formula from the external point to a general point on the line, minimize it algebraically (or use the perpendicular-distance vector projection), and solve for the coordinates of the closest point — translating a geometric minimization into a calculus or algebra problem.

## Common Mistakes

- **Choosing an arbitrary coordinate placement instead of one that exploits the problem's symmetry.** This doesn't change the final answer but can make the algebra substantially harder than necessary.
- **Solving the algebra correctly but failing to translate the result back into a geometric statement.** An algebraic solution (a number, a set of coordinates) isn't itself the answer to "how many intersection points" or "what shape is the locus" until it's interpreted geometrically.
- **Trying to answer angle, area, or plane-orientation questions with only point/line-equation algebra instead of vector methods.** Dot and cross products exist specifically because these questions don't reduce cleanly to line/circle equation algebra alone.

## When NOT to Use

- When the problem is fundamentally about abstract vector spaces, matrix transformations, or eigenstructure rather than concrete 2D/3D geometric configurations — use `apply-linear-algebra-methods` instead.
- When the curve in question is specifically a conic section and the question concerns its focus/directrix/eccentricity properties — use `apply-conic-section-properties`, which covers that classification and application directly.
- When a classical synthetic proof is specifically required (e.g., for pedagogical reasons, or because the problem is stated in purely axiomatic terms) — coordinate methods prove the same facts but don't produce a synthetic-style proof.
