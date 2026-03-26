# Case Study 02 — Thermal Cooling Design for NVIDIA Jetson Nano (UAV Gimbal)

**Company:** Yottec Systems LLP, Bangalore  
**Role:** Lead Aero Analyst  
**Type:** Electronics thermal management | Conjugate Heat Transfer CFD | Passive cooling design

---

## Result

Resolved persistent overheating of NVIDIA Jetson Nano OBC during continuous UAV flight operations. Passive cooling solution maintained junction temperatures within safe operating limits without adding active cooling components (fans, TEC modules) that would increase weight and power draw.

---

## Problem

The NVIDIA Jetson Nano OBC (onboard computer) was installed inside a sealed gimbal enclosure on the UAV. During continuous operation — particularly in image processing and inference workloads — the Jetson Nano consistently exceeded safe junction temperature, causing thermal throttling and in some cases system shutdown mid-flight.

Constraints:
- No active cooling (fans) permitted — vibration and weight budget
- Enclosure geometry could not be significantly enlarged
- Solution had to be manufacturable without CNC machining (sheet metal + thermal interface materials)

---

## Approach

### 1. Baseline Thermal Simulation
- Modelled the Jetson Nano module as a heat source (nominal TDP: ~10W, peak load: ~15W)
- Built conjugate heat transfer (CHT) model of the gimbal enclosure interior in ANSYS Fluent
- Included PCB substrate, module housing, and enclosure walls as conduction domains
- Applied natural convection boundary conditions on external enclosure surfaces
- Identified thermal hotspots: the SoC die and the LPDDR4 memory stack were the primary heat sources, with heat accumulating at the top of the enclosure due to buoyancy-driven stratification

### 2. Passive Cooling Solution Design
- **Heat sink:** Designed aluminium fin array attached directly to Jetson Nano module lid via thermal interface material (TIM). Fin geometry optimised for available clearance inside enclosure.
- **Conductive path:** Added copper thermal strap connecting Jetson module to the gimbal structural wall (higher thermal mass, better external convection)
- **Airflow channels:** Introduced guided internal baffles to redirect buoyancy-driven natural convection away from the hotspot region and toward the cooler base of the enclosure

### 3. Validation Simulations
- Re-ran CHT simulation with cooling solution in place
- Compared temperature distributions at peak load condition (15W TDP)
- Swept across ambient temperatures: 25°C, 35°C, 45°C (representing ground idle to desert flight conditions)

---

## Key Findings

- Baseline: SoC junction temperature reached critical limit under sustained 15W load at 35°C ambient
- With passive cooling solution: junction temperature reduced to within safe operating range across all ambient conditions tested
- The copper thermal strap to the gimbal wall contributed the largest single improvement — effectively spreading heat into a much larger thermal mass
- Natural convection inside the sealed enclosure was largely ineffective without baffling; hot air recirculated back over the module

---

## Tools Used

| Tool | Purpose |
|------|---------|
| ANSYS Fluent | Conjugate heat transfer CFD, natural convection modelling |
| ANSYS Mechanical | Conduction path analysis, thermal interface material modelling |
| SolidWorks | Heat sink and baffle geometry design |

---

## Simulation Images

> *Screenshots to be added: baseline temperature contour, post-solution temperature contour, airflow path vectors, junction temperature vs ambient comparison chart*

<!-- Add images below as: ![description](./images/filename.png) -->

---

## Lessons Learned

- For sealed electronics enclosures, conductive cooling paths to external structure are far more effective than relying on internal natural convection
- CHT simulations are essential — simple conduction-only models significantly underestimate temperatures in configurations with air gaps
- Thermal interface material (TIM) resistance has a disproportionate effect on junction temperature; even moderate improvements in TIM conductivity yielded measurable gains

