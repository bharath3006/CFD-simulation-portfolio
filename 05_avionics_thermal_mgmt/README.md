# Case Study 05 — UAV Avionics Bay Thermal Management

**Company:** Flying Wedge Defence and Aerospace Technologies, Bangalore  
**Role:** Lead Simulation Engineer  
**Type:** Avionics thermal management | Conjugate Heat Transfer CFD | Fuselage ventilation analysis

---

## Result

Confirmed that onboard electronics (flight controller, OBC, payload systems) remain within safe operating temperature limits across the full UAV flight envelope. Identified the most thermally critical components and validated fuselage ventilation path effectiveness at multiple flight speeds and altitudes.

---

## Problem

Fixed-wing UAV avionics bays present a different thermal challenge from ground-based electronics enclosures: the thermal environment changes dynamically with airspeed, altitude (ambient temperature and pressure), and flight phase (ground idle, climb, cruise, descent). The avionics compartment needed thermal validation across these conditions to ensure reliable operation during missions of 4–8 hours.

Electronics installed in the avionics bay:
- Flight controller (FC) — ~5W continuous
- Onboard computer (OBC) — ~10W nominal, ~18W peak
- Payload electronics (EO/IR camera processor) — ~12W
- Power distribution board — ~3W

Total heat load: ~30W nominal, ~38W peak

---

## Approach

### 1. Conjugate Heat Transfer Model
- Built full CHT model of the avionics bay interior in ANSYS Fluent
- Heat sources modelled as volumetric heat generation in each component block
- Component mounting surfaces (PCB, chassis) modelled as conduction domains
- Fuselage skin modelled as a convective boundary (external forced convection from airflow)

### 2. External Airflow Boundary Conditions
- Derived convective heat transfer coefficients for the fuselage outer skin at:
  - Sea-level cruise: V = 28 m/s (typical MALE cruise speed)
  - 3000 m cruise: V = 32 m/s (higher TAS at altitude)
  - Ground idle: V = 0 (natural convection only — worst case for heat removal)
- Applied as spatially varying convection BCs on the fuselage walls

### 3. Ventilation Path Analysis
- Modelled inlet and outlet vent geometry in the fuselage (ram air inlet + exhaust port)
- Analysed internal airflow distribution: velocity vectors, recirculation zones, dead-flow regions
- Evaluated natural convection contribution at ground idle condition
- Identified components in low-velocity regions (poor convective cooling) and those in high-velocity zones

### 4. Parametric Study
- Swept ambient temperatures: 25°C, 35°C, 45°C
- Swept flight speeds: ground idle, 20 m/s, 28 m/s, 35 m/s
- Peak load vs nominal load heat dissipation scenarios

---

## Key Findings

- OBC (18W peak) was the most thermally critical component in all scenarios
- Ground idle at 45°C ambient was the worst-case condition — natural convection alone was insufficient; component temperatures approached limits after ~12 minutes
- At cruise speed (28 m/s), forced convection through the ventilation path maintained all components within safe operating margins with >15°C temperature headroom
- A recirculation zone downstream of the power distribution board created a hot spot — resolved by adding a small internal baffle to redirect airflow
- OBC positioned downstream of flight controller received pre-heated air — repositioning the OBC to the front of the bay reduced its steady-state temperature by ~8°C

---

## Tools Used

| Tool | Purpose |
|------|---------|
| ANSYS Fluent | Conjugate heat transfer CFD, ventilation analysis |
| ICEM CFD | Hex-dominant mesh for avionics bay interior |
| Python | Post-processing, temperature sweep data extraction |
| MATLAB | Thermal margin analysis and reporting |

---

## Simulation Images

> *Screenshots to be added: ventilation path velocity vectors, temperature contour at cruise vs ground idle, component temperature comparison bar chart, hot spot identification*

<!-- Add images below as: ![description](./images/filename.png) -->

---

## Lessons Learned

- Ground idle is the defining thermal design condition for UAV avionics — forced airflow during flight provides substantial cooling margin that disappears entirely on the ground
- Component positioning within the bay matters significantly — upstream components see cooler air; downstream ones inherit heat from upstream sources
- CHT simulation with realistic ventilation geometry is essential; simplified lumped-parameter thermal models miss the airflow distribution effects that drive component-level temperatures

