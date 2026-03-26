# Case Study 01 — VTOL UAV Aerodynamic Redesign

**Company:** Yottec Systems LLP, Bangalore  
**Role:** Lead Aero Analyst  
**Type:** Aerodynamic optimisation | CFD | Low-to-high fidelity validation

---

## Result

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Lift-to-Drag Ratio (L/D) | 6.5 | ~10 | **+54%** |
| Total Aerodynamic Drag | Baseline | Optimised | **−35%** |

---

## Problem

The tandem-wing VTOL UAV had an aerodynamic efficiency (L/D) of 6.5, which was insufficient to meet mission endurance targets. The configuration suffered from unfavourable wing interference effects and poor lift distribution across the tandem arrangement. A full aerodynamic redesign was required to improve cruise efficiency without compromising VTOL transition stability.

---

## Approach

### 1. Low-Fidelity Screening (XFLR5)
- Built 3D panel models of the tandem-wing configuration in XFLR5
- Generated airfoil polars across the operational Reynolds number range
- Evaluated multiple wing planform variants: changes to sweep angle, aspect ratio, taper ratio, and airfoil section
- Extracted lift distribution, stability derivatives (Cm, CLα, Cmα), and preliminary drag estimates
- Screened ~12 configurations down to 3 candidates for high-fidelity CFD

### 2. High-Fidelity CFD Validation (ANSYS Fluent / OpenFOAM)
- Imported candidate geometries into ICEM CFD for structured/unstructured hybrid mesh generation
- Applied y+ < 1 wall refinement for accurate boundary layer resolution
- Turbulence model: k-ω SST (well-suited for airfoil flows with mild separation)
- Ran AoA sweeps from −4° to 16° at cruise Reynolds number
- Captured 3D effects: wing-body interaction, downwash from front wing on rear wing, propeller wake influence zones
- Compared Cl, Cd, Cm curves against XFLR5 predictions to identify low-fidelity model limitations

### 3. Optimisation Iterations
- Identified rear wing placement (vertical offset and longitudinal gap) as the dominant driver of interference drag
- Adjusted airfoil camber distribution to improve front wing pressure recovery
- Refined wing-fuselage fairing geometry to reduce junction separation

---

## Key Findings

- Tandem-wing downwash interaction was responsible for ~18% of total drag in the baseline configuration
- Increasing vertical separation between front and rear wings by 12% reduced interference drag significantly
- XFLR5 underestimated drag by ~22% in the baseline case due to inability to capture 3D separation at the wing-body junction — an important calibration point for future low-fidelity screening

---

## Tools Used

| Tool | Purpose |
|------|---------|
| XFLR5 | Airfoil polars, planform screening, stability derivatives |
| ANSYS Fluent | High-fidelity 3D viscous CFD, AoA sweeps |
| OpenFOAM | Cross-validation of Fluent results |
| ICEM CFD | Structured mesh generation, boundary layer control |
| ANSYS Mechanical | Preliminary load estimation from CFD pressure distributions |

---

## Simulation Images

> *Screenshots to be added: pressure contour plots, velocity streamlines, drag polar comparison, mesh cross-section, convergence history*

<!-- Add images below as: ![description](./images/filename.png) -->

---

## Lessons Learned

- Low-fidelity tools like XFLR5 are reliable for planform screening but require CFD calibration for tandem configurations where interference effects dominate
- Iterating geometry in XFLR5 before committing to CFD meshes reduced total simulation time by approximately 60%
- k-ω SST performed well across the AoA range tested; no RANS model switching was required

