---
layout: default
title: Publications & Patents
---

[Home](./) · [Scientific ML](./scientific-ml) · [Fluids](./fluid-dynamics) · [Control](./controls-robotics) · [About](./about)

# Publications & Patents

A collection of published, submitted, and patented research work.

---

# Publications

## Decoupled Capacitive-Gate Electroosmosis

### Phase-Controlled Bidirectional Flow in High-Conductivity Electrolytes via a Modified Poisson-Boltzmann-Stokes Framework

**Journal of Applied Physics — Featured Article**

**DOI:** `10.1063/5.0345688`  
**Advisor:** Prof. Srikanth Vedantam

Electroosmotic flow arises when an applied electric field interacts with charge contained in the electric double layer near a solid-electrolyte interface.

At high electrolyte concentrations, however, classical dilute-solution models become increasingly insufficient because effects such as finite ion size and interfacial polarisation become important.

This work developed a continuum electrokinetic framework combining:

- modified Poisson-Boltzmann electrostatics,
- finite ion-size steric effects,
- dynamic Stern-layer polarisation,
- Stokes momentum equations.

The device architecture introduces an independently controlled **capacitive gate electrode**.

By adjusting the phase relationship between gate actuation and the tangential AC electric field, the surface charge in the electric double layer can be dynamically modulated.

This enables control over both the magnitude and direction of electroosmotic transport.

High-fidelity 2D axisymmetric finite-element simulations in COMSOL Multiphysics were used to investigate:

- nonlinear boundary-layer charge transport,
- phase-dependent pumping,
- parasitic vortex formation,
- volumetric flow rate,
- operation at high ionic conductivity,
- avoidance of Faradaic degradation.

The work demonstrates continuously controllable bidirectional electroosmotic pumping using capacitive rather than Faradaic charge modulation.

[Read more about the fluid mechanics →](./fluid-dynamics)

---

# Under Review

## HoloFNO

### Neural Operators for Optical Trapping of Neutral Atoms

**Under review at ICLR 2027**

**RISE Lab**  
**Advisor:** Prof. Gopalakrishnan

Optical trapping often requires solving an inverse problem: determining the optical control field required to generate a desired trapping landscape.

When these inverse problems must be solved repeatedly, conventional iterative optimisation can become computationally expensive.

This work investigates the use of **neural operators** for learning mappings between continuous physical fields in this setting.

Because the work remains under review, detailed architecture, methodology, ablations, and experimental results are intentionally omitted from this website.

[Background on neural operators →](./scientific-ml)

---

# Patents

## Decoupled Capacitive-Gate Electroosmotic Pump Architecture

Patent filing associated with the electroosmotic-flow research described above.

The architecture introduces independent capacitive control over electric-double-layer charge in order to achieve phase-controlled electroosmotic transport without relying on Faradaic current.

[Related publication →](#decoupled-capacitive-gate-electroosmosis)

---

## Decoupled Tilting Architecture for Narrow-Track Vehicles

**Indian Patent Application Filed — Provisional Patent**

**Advisor:** Prof. Guruprasad K R

Narrow-track vehicles benefit from chassis tilting during cornering, but integrating tilt with conventional suspension and steering introduces several mechanical difficulties.

In particular, chassis roll should ideally remain distinct from:

- suspension compression,
- suspension extension,
- road-disturbance response,
- steering articulation.

The developed architecture uses a **non-tilting suspension subframe** together with parallelogram-based suspension geometry.

This permits the vehicle chassis to tilt relative to the suspension structure while preserving substantially independent vertical suspension motion.

A multi-degree-of-freedom steering knuckle was also developed to avoid kinematic binding during combinations of:

- large steering angle,
- large chassis tilt,
- suspension travel.

The architecture was evaluated through:

- kinematic analysis,
- MATLAB/Simulink dynamic modelling,
- finite-element structural analysis.

[Read more about the vehicle system →](./controls-robotics)

---

# Research Areas

My formal and ongoing research broadly spans:

- scientific machine learning,
- neural operators,
- electrohydrodynamics,
- fluid mechanics,
- nonlinear dynamical systems,
- mechanistic interpretability,
- mobility systems.

---

[Home](./) · [About](./about)
