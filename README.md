# Antenna Array Synthesis & Full-Wave Validation in CST

**Design of a Dolph-Tschebyscheff linear array (4 GHz) and a beam-steered 3×4 planar array (6 GHz): analytical synthesis validated against full-wave EM simulation.**

| | |
|---|---|
| **Type** | Analytical design + full-wave simulation (CST Microwave Studio) |
| **Author** | Samuel Sánchez García (sole author) |
| **Context** | University of New Mexico (UNM), antenna engineering coursework, 2026 |
| **Status** | Complete — **all results are simulated** |

---

## Problem 1 — Dolph-Tschebyscheff broadside array (4 GHz)

**Spec:** 8 elements, −20 dB sidelobe level, λ/4 spacing, λ/2 dipole elements at 4 GHz (λ = 75 mm, d = 18.75 mm).

### Synthesis

- −20 dB SLL → voltage ratio R = 10, governed by Chebyshev polynomial T₇(x)
- Scaling factor x₀ = cosh[(1/7)·cosh⁻¹(10)] ≈ 1.0927
- Normalized excitation coefficients: **1.000 / 1.137 / 1.506 / 1.720** (symmetric)

### Simulated results (CST) vs uniform array

| Metric | Dolph-Tschebyscheff | vs Uniform (same aperture) |
|---|---|---|
| Gain | **10.4 dBi** | −0.2 dB |
| HPBW | **28.8°** | +2.4° wider |
| Max SLL | ≈ **−20 dB** (as designed) | uniform SLL substantially higher |

The trade-off is the expected one: the amplitude taper required to suppress sidelobes reduces aperture illumination efficiency, costing gain and beamwidth. The value of the exercise is that the full-wave simulation reproduces the analytically designed SLL.

## Problem 2 — Beam-steered 3×4 planar array (6 GHz)

**Spec:** uniform 3×4 array, dₓ = λ/2 = 25 mm, dᵧ = λ/4 = 12.5 mm, main beam steered to θ₀ = 30°, φ₀ = 30°, λ/2 dipole elements.

### Synthesis

- Progressive phase shifts: **αₓ = −77.94°, αᵧ = −22.5°**
- Total pattern via Pattern Multiplication: E_total = E_element × AF

### Simulated results (CST) and analysis

| Metric | Analytical | CST (full-wave) |
|---|---|---|
| Gain | 14.28 dBi (asymptotic formula) | **10.8 dB realized** |
| Main lobe, φ=30° plane | θ = 30° (AF design) | **θ = 28.0°** |
| Main lobe, φ=90° plane | θ ≈ 14.5° (AF only) | **θ = 10.0°** |

The discrepancies are physical, not numerical errors, and are analyzed in the report:

- **Gain:** the asymptotic planar-array directivity formula overestimates for electrically small arrays; the theoretical ceiling for 12 independent isotropic elements is 10·log₁₀(12) ≈ 10.79 dB, consistent with CST.
- **Beam squint:** multiplying the sloped dipole element pattern by the AF peak pulls the resulting maximum inward (30° → 28°; 14.5° → 10°) — a textbook demonstration of the Pattern Multiplication Principle.
- **Physical feasibility:** with Y-oriented λ/2 dipoles (25 mm) and dᵧ = 12.5 mm, adjacent elements would physically overlap — identified and documented as a constraint that makes Problem 2 a theoretical AF validation exercise.

## Repository contents

```
docs/       Full project report (PDF)
figures/    CAD models, 3D radiation patterns, 1D polar cuts
```

CST project files (.cst) available on request.

## Skills demonstrated

`array synthesis` `Dolph-Tschebyscheff / Chebyshev taper` `sidelobe control` `beam steering` `pattern multiplication` `CST Microwave Studio` `full-wave EM simulation` `analytical vs numerical validation`
