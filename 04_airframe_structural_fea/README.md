# Case Study 04 — UAV Airframe Structural Validation Under Aerodynamic Loads

**Company:** Yottec Systems LLP / Flying Wedge Defence and Aerospace Technologies  
**Role:** Lead Aero Analyst / Lead Simulation Engineer  
**Type:** Structural FEA | CFD-to-FEA load transfer | Aero-structural analysis

---

## Result

Validated structural integrity of UAV airframe critical components (wing root, main spar, fuselage-wing junction) under worst-case aerodynamic loading. CFD-derived pressure distributions were directly mapped as loads in ANSYS Mechanical, establishing a repeatable aero-structural workflow.

---

## Problem

UAV airframe structural qualification required accurate load estimation beyond simplified hand-calculation methods. The key challenge was translating realistic, non-uniform aerodynamic pressure distributions from CFD directly onto the FEA structural model — rather than using simplified point loads or uniform pressure assumptions that overestimate or miss local peak stresses.

Design-critical load cases:
- Maximum lift condition (pull-up manoeuvre, n = 3.5g)
- Gust load (sharp-edged gust, CS-23 equivalent)
- Asymmetric load (rolling manoeuvre, differential lift)

---

## Approach

### 1. Load Extraction from CFD
- Ran high-fidelity CFD in ANSYS Fluent at the critical load case AoA (maximum lift, pre-stall)
- Exported surface pressure distributions over wing upper/lower surfaces, fuselage, and control surfaces
- Converted pressure data to nodal force arrays for FEA import

### 2. FEA Model Setup (ANSYS Mechanical)
- Imported structural geometry (simplified for FEA: spar caps, skin panels, ribs, fuselage frames)
- Assigned material properties: carbon fibre composite (orthotropic) for primary structure, aluminium for fittings and joints
- Applied CFD-derived pressure loads via surface mapping — ANSYS Mechanical's External Data module used to interpolate CFD nodal pressures onto the FEA mesh
- Boundary conditions: wing root fully fixed (conservative), followed by realistic flexible joint model

### 3. Structural Analysis
- Static structural analysis for all three critical load cases
- Extracted: von Mises stress distribution, principal stresses, total deformation, and safety factors
- Identified critical regions: wing root spar cap, forward fuselage-wing attachment lug, and rib-skin bonded joints
- Ran sensitivity study: compared CFD-mapped loads vs simplified uniform pressure assumption — difference in peak stress was 23% at the wing root

---

## Key Findings

- Wing root spar cap showed highest von Mises stress under 3.5g pull-up condition — safety factor of 1.6 against ultimate load (above minimum 1.5 requirement)
- Fuselage-wing attachment lug was the most sensitivity-critical component: small changes in load distribution produced large changes in local peak stress
- Simplified uniform pressure load assumption underestimated peak wing root stress by 23% compared to CFD-mapped loads — validating the need for the integrated workflow
- No structural failure predicted under any of the three design load cases

---

## Tools Used

| Tool | Purpose |
|------|---------|
| ANSYS Fluent | CFD pressure distribution extraction at critical AoA |
| ANSYS Mechanical | Static structural FEA, CFD load mapping |
| ICEM CFD | Structural mesh refinement near high-stress regions |
| SolidWorks | Geometry preparation and simplification for FEA |
| Python | Pressure data extraction and format conversion for FEA import |

---

## Simulation Images

> *Screenshots to be added: CFD pressure distribution on wing surface, FEA mesh with boundary conditions, von Mises stress contour, deformation plot, safety factor summary*

<!-- Add images below as: ![description](./images/filename.png) -->

---

## Lessons Learned

- CFD-to-FEA load mapping is significantly more accurate than simplified load assumptions for complex geometry — worth the additional workflow step for structural-critical components
- The ANSYS Fluent + Mechanical integrated workflow (Workbench) handles this well once the geometry and mesh conventions are aligned between the two modules
- For composite structures, getting accurate ply orientation and laminate stacking sequence into the FEA model matters as much as getting the loads right

