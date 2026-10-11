---
layout: default
title: Fluid Dynamics & Computational Physics
---

[Home](./) · [Scientific ML](./scientific-ml) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Control](./controls-robotics) · [Publications](./publications)

# Fluid Dynamics & Computational Physics

Fluid mechanics is a striking example of how compact physical laws can produce extraordinarily complicated behaviour.

For an incompressible Newtonian fluid,

$$
\frac{\partial \mathbf{u}}{\partial t}
+
(\mathbf{u}\cdot\nabla)\mathbf{u}
=
-\frac{1}{\rho}\nabla p
+
\nu\nabla^2\mathbf{u}
+
\mathbf{f},
$$

subject to

$$
\nabla\cdot\mathbf{u}=0.
$$

Despite this compact formulation, solutions may contain:

- boundary layers,
- separation,
- vortices,
- instabilities,
- turbulence,
- interacting spatial and temporal scales.

Much of my research and engineering work has involved understanding these behaviours computationally.

---

# Electrokinetic Flow

At microscopic scales, fluid motion can couple strongly to electrostatics.

Near a charged surface in an electrolyte, mobile ions rearrange and create an **electric double layer**.

An applied tangential electric field acts on this charge distribution and can generate fluid motion.

This is the basis of electroosmosis.

---

# Decoupled Capacitive-Gate Electroosmosis

I worked on a continuum model coupling modified Poisson-Boltzmann electrostatics with Stokes flow for high-conductivity electrolytes.

At sufficiently high ionic concentration, ideal dilute-solution approximations become inaccurate.

The formulation therefore incorporated:

- finite ion-size steric effects,
- dynamic Stern-layer polarisation,
- nonlinear electric-double-layer behaviour.

The system uses an asymmetric three-electrode configuration containing an independently driven capacitive gate.

Controlling the phase between the gate signal and tangential electric field permits dynamic modulation of electric-double-layer surface charge and therefore electroosmotic forcing.

High-fidelity 2D axisymmetric finite-element simulations in COMSOL were used to investigate:

- parasitic vortex formation,
- harmonic phase effects,
- volumetric throughput,
- operation at high conductivity,
- suppression of Faradaic degradation.

The work was published as a **Featured Article in the Journal of Applied Physics**.

**DOI:** `10.1063/5.0345688`

---

# Aerodynamics and Active Flow Control

Aircraft performance depends strongly on the interaction between:

- pressure distribution,
- viscous boundary layers,
- separation,
- wake formation.

A useful nondimensional quantity is the Reynolds number:

$$
Re
=
\frac{\rho UL}{\mu}
=
\frac{UL}{\nu}.
$$

It measures the relative influence of inertial and viscous effects.

At high Reynolds number, viscosity may have little influence throughout much of the external flow while remaining decisive inside thin boundary layers near solid surfaces.

---

# Inter-IIT STOL Aircraft Optimisation

As part of the Inter-IIT Tech Meet, I worked on automated aerodynamic optimisation for a high-lift STOL aircraft configuration.

Airfoil geometries were represented using a **12th-order Bernstein polynomial basis**.

A PPO-based optimisation framework searched this parameter space for high-lift configurations.

---

# FastFOIL

Part of the project required extending XFOIL to represent **Co-Flow Jet active flow control**.

XFOIL combines:

1. an inviscid potential-flow model,
2. an integral boundary-layer model,
3. viscous-inviscid interaction.

Active mass injection and suction therefore require modifications to both the physical model and the numerical coupling.

I implemented:

- line-source distributions,
- line-sink distributions,
- wall-normal transpiration,
- modified integral boundary-layer momentum terms,
- corresponding Newton-Raphson Jacobian terms.

I also identified and corrected a station-indexing issue in the legacy `SETBL` Fortran routine that destabilised mass-flux calculations during extreme parameter sweeps.

The final aircraft configuration achieved a reported takeoff lift coefficient of

$$
C_L = 9.49
$$

at approximately

$$
Re=10^6.
$$

---

# Boundary Layers

At sufficiently high Reynolds number, the external flow may be approximately inviscid while a thin region near the wall remains strongly affected by viscosity.

This is the boundary layer.

The characteristic no-slip condition is

$$
\mathbf{u}_{\mathrm{wall}}=0.
$$

Velocity therefore changes rapidly between the stationary surface and the outer flow.

This creates strong velocity gradients and wall shear.

Boundary-layer behaviour ultimately determines phenomena including:

- skin-friction drag,
- separation,
- stall,
- wake formation.

---

# Hydrofoil Boundary Layers

## Project DOFT

Hydrofoils obey many of the same aerodynamic principles as airfoils, but the different thermophysical properties of water change the relative transport scales.

I conducted high-resolution 2D CFD simulations of NACA and Eppler hydrofoil sections using the

$$
k-\omega\ \mathrm{SST}
$$

turbulence model in ANSYS Fluent.

The project investigated boundary-layer separation and whether local surface heating could provide useful boundary-layer control.

The Prandtl number is

$$
Pr
=
\frac{\nu}{\alpha},
$$

where:

- $\nu$ is momentum diffusivity,
- $\alpha$ is thermal diffusivity.

For water,

$$
Pr\approx7.
$$

This means thermal and momentum diffusion occur on substantially different scales.

The analysis indicated that thermal effects remained concentrated in a comparatively thin near-wall region, making the proposed heating mechanism ineffective for practical manipulation of the larger hydrodynamic boundary layer.

---

# Bio-Inspired Propulsion

## Project PowerKick

Biological swimmers frequently exploit compliant structures rather than perfectly rigid propulsors.

The deformation of a flexible fin interacts with:

- vortex shedding,
- wake structure,
- thrust production,
- energy recovery.

Project PowerKick explored a compliant monofin inspired by cetacean caudal-fin motion.

I developed a variable-thickness flexural-rigidity distribution intended to balance:

- structural flexibility,
- thrust generation,
- drag,
- wake interaction.

Coupled fluid-structure simulations in COMSOL were used to investigate the relationship between passive deformation and hydrodynamic performance.

---

# Vorticity

Velocity is not always the most useful quantity for describing rotational flow.

The vorticity field is defined by

$$
\boldsymbol{\omega}
=
\nabla\times\mathbf{u}.
$$

Vorticity measures local rotational structure and provides a natural way to analyse:

- vortices,
- shear layers,
- coherent structures,
- wake dynamics.

In two-dimensional incompressible flow, the vorticity equation can be written schematically as

$$
\frac{\partial\omega}{\partial t}
+
\mathbf{u}\cdot\nabla\omega
=
\nu\nabla^2\omega.
$$

This highlights the competition between nonlinear advection and viscous diffusion.

---

# Turbulence and Predictability

Turbulence is a deterministic system with severe practical predictability limits.

Consider two initially nearby velocity fields:

$$
\mathbf{u}_1(0),
\qquad
\mathbf{u}_2(0)
=
\mathbf{u}_1(0)
+
\delta\mathbf{u}(0).
$$

Define their difference as

$$
\delta\mathbf{u}(t)
=
\mathbf{u}_2(t)
-
\mathbf{u}_1(t).
$$

For sufficiently small perturbations over a limited interval, one may observe approximately

$$
\|\delta\mathbf{u}(t)\|
\sim
\|\delta\mathbf{u}(0)\|
e^{\lambda t},
$$

where $\lambda$ represents a finite-time instability rate.

The interesting question is not simply whether turbulent trajectories diverge.

It is whether the **present flow structure contains information about how future divergence will occur**.

This connects several areas:

- turbulence,
- nonlinear dynamics,
- chaos,
- coherent structures,
- reduced-order modelling,
- spectral analysis,
- scientific machine learning.

I am currently exploring questions in this area, but detailed methodology will be added only after the work is sufficiently mature.

---

# Methods I Use

### Numerical

- Finite-element methods
- CFD
- Numerical PDEs
- Spectral analysis
- Reduced-order modelling

### Simulation

- COMSOL Multiphysics
- ANSYS Fluent
- XFOIL
- MATLAB/Simulink

### Analysis

- POD
- DMD
- Fourier analysis
- instability analysis
- dimensional analysis

---

[Scientific ML](./scientific-ml) · [Publications](./publications) · [Blog](./blog/)
