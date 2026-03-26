# Case Study 03 — MALE UAV Flight Envelope Analysis (150–400 kg)

**Company:** Flying Wedge Defence and Aerospace Technologies, Bangalore  
**Role:** Lead Simulation Engineer  
**Type:** Aerodynamic performance | Low-to-high fidelity validation | Mission analysis

---

## Result

Delivered validated aerodynamic performance databases and flight envelope limits for three fixed-wing UAV platforms in the MALE (Medium-Altitude Long-Endurance) category: 150 kg, 230 kg, and 400 kg gross weight. Results used directly for mission planning, flight control law development, and endurance estimation.

---

## Problem

Three fixed-wing UAV platforms required aerodynamic characterisation before flight testing. Key deliverables needed:
- Lift, drag, and pitching moment coefficients across the operational AoA and Mach range
- Stability derivatives for flight dynamics modelling
- Flight envelope limits: stall speed, maximum speed, service ceiling, and best-endurance airspeed
- Validation of low-fidelity XFLR5 models against high-fidelity CFD to establish confidence bounds

---

## Approach

### 1. XFLR5 Aerodynamic Modelling
- Built 3D panel models for each UAV configuration in XFLR5
- Imported airfoil coordinates (proprietary sections) and generated polars across Re = 0.5×10⁶ to 3×10⁶
- Performed VLM (Vortex Lattice Method) and 3D panel analysis to extract:
  - CLα, CDα curves across AoA sweep (−4° to 18°)
  - Pitching moment coefficient (Cm) and neutral point location
  - Stability derivatives: Clβ, Cnβ, Cmα, CLq
- Identified preliminary stall AoA and best L/D operating point for each platform

### 2. High-Fidelity CFD — ANSYS Fluent & SU2
- Meshed full 3D geometry (half-model with symmetry plane) using ICEM CFD
- Mesh sizing: ~8–12 million cells, structured boundary layer with y+ ≈ 1
- Turbulence model: k-ω SST with γ-Reθ transition model for low-Re sections
- AoA sweep: −4° to 18° at 2° increments, at cruise and sea-level dynamic pressure
- Additional cases: sideslip sweep (β = 0° to 10°) for lateral stability derivatives
- OpenFOAM used as independent cross-check on selected operating points

### 3. Low-to-High Fidelity Correlation
- Compared XFLR5 and CFD lift/drag polars for each platform
- Documented agreement regions and divergence zones (typically near stall and at high-lift conditions)
- Established correction factors for XFLR5 predictions to improve accuracy for future rapid design iterations

### 4. Flight Envelope Construction
- Used validated aerodynamic data with aircraft weight, thrust, and altitude model to compute:
  - Stall speed (Vs) at sea level and 3000 m
  - Best endurance airspeed (minimum drag speed)
  - Maximum level flight speed
  - Service ceiling (where climb rate = 0.5 m/s)

---

## Key Findings

- XFLR5 predicted CLmax within 8% of CFD for all three platforms — acceptable for rapid screening
- XFLR5 consistently underestimated CDmin by 15–25% due to inability to capture fuselage and nacelle parasite drag
- The 400 kg platform showed significant wing-body junction separation at AoA > 12° that XFLR5 did not predict — a critical finding for stall margin definition
- Best-endurance airspeed was 12–18% higher than the minimum drag speed predicted by XFLR5 alone, once fuselage drag correction was applied

---

## Tools Used

| Tool | Purpose |
|------|---------|
| XFLR5 | Airfoil polars, VLM analysis, stability derivatives |
| ANSYS Fluent | High-fidelity 3D CFD, AoA/sideslip sweeps |
| SU2 | Independent CFD cross-validation |
| OpenFOAM | Additional validation cases |
| ICEM CFD | Structured mesh generation |
| Python | Post-processing, polar extraction, flight envelope plotting |
| MATLAB | Flight envelope computation from aero database |

---

## Simulation Images

> *Screenshots to be added: pressure contour at cruise AoA, lift/drag polar comparison (XFLR5 vs CFD), flight envelope diagram, mesh cross-section, streamline visualisation near stall*

<!-- Add images below as: ![description](./images/filename.png) -->

---

## Lessons Learned

- Establishing low-to-high fidelity correlation upfront is worth the time investment — it allows faster iteration in subsequent design phases with known confidence bounds
- SU2's adjoint solver (not used here but available) would be a valuable addition for gradient-based drag minimisation in future work
- Transition modelling (γ-Reθ) made a measurable difference in drag prediction for the lower Reynolds number 150 kg platform; fully turbulent assumption over-predicted CDmin

