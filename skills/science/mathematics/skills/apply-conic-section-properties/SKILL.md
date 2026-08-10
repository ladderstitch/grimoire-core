---
name: apply-conic-section-properties
description: Use when a curve is a circle, ellipse, parabola, or hyperbola — classifying a general second-degree equation into standard form and applying its focus, directrix, and eccentricity properties to a physical problem, such as orbital mechanics, parabolic reflector/antenna design, or optical mirror focusing.
source: Apollonius of Perga, "Conics" (~200 BCE) — the classical foundation of conic-section theory; Kepler's laws of planetary motion (1609–1619), which establish that orbits are conic sections with the sun at a focus, used directly in NASA orbit-determination methods; parabolic reflector geometry underlying satellite dish, radio telescope, and headlight/mirror design
tags: [conic-sections, ellipse, parabola, hyperbola, eccentricity, mathematics, orbital-mechanics, optics]
related: [apply-analytic-geometry, apply-linear-algebra-methods]
---

# Apply Conic Section Properties

Classify a curve into its standard conic-section form and apply its focus, directrix, or eccentricity properties to solve the physical problem at hand — orbital trajectories, reflector geometry, or optical focusing — rather than treating the curve as an arbitrary algebraic equation with no exploitable structure.

## Why This Is Best Practice

**Why best:** Conic sections have specific, well-defined geometric properties — a focus and directrix relationship, a fixed eccentricity, reflective focusing properties — that a general quadratic curve does not. Recognizing a curve as a specific conic and converting it to standard form makes these properties directly usable, rather than working with an unclassified second-degree equation from which none of these properties are readily apparent.

**Adopted by:** Kepler's laws of planetary motion established that orbits are conic sections (ellipses, for bound orbits, with the central body at one focus) — a result used directly in NASA and other space agencies' orbit-determination and mission-planning methods. Parabolic reflector geometry — the property that a parabola reflects all rays parallel to its axis through a single focus — is the geometric basis of satellite dish antennas, radio telescopes, automotive headlight reflectors, and solar concentrators. Elliptical and hyperbolic mirror geometry is used in optical telescope design (Cassegrain and related configurations) for the same focusing-property reasons.

**Impact:** Antenna and telescope designers compute reflector shapes directly from parabolic (or, for multi-mirror systems, elliptical/hyperbolic) focus properties rather than through trial-and-error shaping — the focusing behavior is a direct, provable consequence of the conic's geometric definition. Orbital mechanics uses a spacecraft's or planet's conic-section orbital elements (semi-major axis, eccentricity) as the standard, compact way to fully describe and predict its trajectory, rather than tracking position numerically at every instant.

Sources: Apollonius of Perga, *Conics* (~200 BCE); Kepler's laws of planetary motion (1609–1619); parabolic reflector geometry as applied in antenna, telescope, and optical mirror design.

## Steps

### 1. Classify the conic from its general equation

For a general second-degree equation Ax² + Bxy + Cy² + Dx + Ey + F = 0, classify using the discriminant B² − 4AC:

| Discriminant | Conic type |
|---|---|
| B² − 4AC < 0, A = C, B = 0 | Circle |
| B² − 4AC < 0 (and not a circle) | Ellipse |
| B² − 4AC = 0 | Parabola |
| B² − 4AC > 0 | Hyperbola |

### 2. Convert to standard form

```
Circle:      (x−h)² + (y−k)² = r²
Ellipse:     (x−h)²/a² + (y−k)²/b² = 1        (a > b: major axis along x)
Parabola:    (y−k)² = 4p(x−h)                  (opens along x-axis; swap for y-axis opening)
Hyperbola:   (x−h)²/a² − (y−k)²/b² = 1
```

If the general equation has a nonzero Bxy term, first rotate the coordinate axes to eliminate it before completing the square to reach standard form.

### 3. Identify focus, directrix, and eccentricity

```
Ellipse:    c² = a² − b²,   e = c/a  (0 < e < 1);  foci at (h±c, k)
Parabola:   e = 1;  focus at (h+p, k), directrix x = h−p  (for the x-opening form above)
Hyperbola:  c² = a² + b²,   e = c/a  (e > 1);  foci at (h±c, k)
```

Eccentricity is the single parameter that determines shape: e = 0 is a circle, 0 < e < 1 is an ellipse, e = 1 is a parabola, e > 1 is a hyperbola — all defined by the same ratio of distance-to-focus over distance-to-directrix.

### 4. Apply the reflective/focusing property for optical or antenna problems

A parabola reflects every ray parallel to its axis through its single focus — the property that makes parabolic dishes and mirrors concentrate a distant, effectively-parallel signal (radio waves from space, sunlight) at one point. An ellipse reflects rays from one focus to the other. Use whichever property matches the physical configuration: a single distant source (parabola) versus two defined focal points (ellipse).

### 5. Apply orbital-mechanics properties for trajectory problems

A bound orbit around a central mass is an ellipse with the central mass at one focus (Kepler's first law); an unbound trajectory (e.g., an interstellar object passing through) is a hyperbola; the boundary case is a parabola. The orbit's eccentricity and semi-major axis fully characterize its shape and size — use these as the compact description rather than tracking position numerically at every point in time.

## Rules

- Classify the conic type before attempting to apply any focus/directrix/eccentricity property — these properties are specific to each conic type and don't apply uniformly to an unclassified quadratic curve.
- Rotate axes to eliminate a nonzero xy-term before completing the square — attempting to complete the square directly on a rotated conic's general equation doesn't produce a correct standard form.
- Match the reflective property to the physical source configuration: a single distant/parallel source calls for a parabola's property, two defined focal points call for an ellipse's or hyperbola's property.

## Examples

**Trigger:** Design a satellite dish that focuses incoming radio signals (effectively parallel rays, given the source's distance) onto a single receiver point.
→ Use a parabolic reflector shape. The parabola's defining property — every ray parallel to its axis reflects through the single focus — places the receiver exactly at that focus, regardless of where across the dish's surface a given ray strikes.

**Trigger:** Determine a comet's orbital path given its measured position and velocity at one point.
→ Compute the orbit's eccentricity from the measured position/velocity via the vis-viva equation and angular momentum. If e < 1, the comet is in a bound elliptical orbit and will return; if e ≥ 1, it's on a parabolic or hyperbolic trajectory and will not return — the conic classification directly answers the physical question of whether the comet is periodic.

## Common Mistakes

- **Treating a general second-degree equation's coefficients as if they already reveal focus/eccentricity properties without first converting to standard form.** These properties are only directly readable from the standard form; the general equation's raw coefficients don't expose them.
- **Forgetting to rotate axes when a nonzero xy cross-term is present.** Completing the square without first eliminating the cross-term produces an incorrect or unsimplifiable result.
- **Applying a parabola's single-focus reflective property to a problem that actually has two defined focal points (an ellipse's geometry).** The correct conic must match the physical configuration — a two-focus setup needs an ellipse or hyperbola, not a parabola.

## When NOT to Use

- For a general curve that isn't a conic section (a higher-degree polynomial curve, an arbitrary parametric curve) — conic-specific properties (focus, directrix, eccentricity) don't exist for non-conic curves.
- For general coordinate-geometry problems (distance, intersection, locus) that don't involve a conic's specific focus/directrix/reflective structure — use `apply-analytic-geometry` for those.
- For orbital mechanics problems requiring perturbation effects (atmospheric drag, multi-body gravitational influence) beyond the idealized two-body conic-orbit model — the pure conic-section description is only exact for an idealized two-body system.
