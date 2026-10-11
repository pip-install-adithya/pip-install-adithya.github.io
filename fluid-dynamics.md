[Home](./) · [Scientific ML](./scientific-ml) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Control](./controls-robotics) · [Publications](./publications)

# Fluid Dynamics & Computational Physics

Fluid mechanics is an interesting example of how relatively compact physical laws can produce extraordinarily complicated behaviour.

For an incompressible Newtonian fluid,

\[
\frac{\partial \mathbf u}{\partial t}
+
(\mathbf u\cdot\nabla)\mathbf u
=
-\frac{1}{\rho}\nabla p
+
\nu\nabla^2\mathbf u
+
\mathbf f,
\]

with

\[
\nabla\cdot\mathbf u=0.
\]

Despite the compact form, solutions can contain:

- boundary layers,
- separation,
- vortices,
- instabilities,
- turbulence,
- multiple interacting spatial scales.

Much of my engineering and research work has involved understanding these phenomena computationally.

---

# Electrokinetic Flow

At very small scales, fluid motion can be strongly coupled to electrostatics.

Near a charged surface in an electrolyte, mobile ions form an **electric double layer**.

Applying an electric field produces a body force on this charge distribution and can drive fluid motion.

This is the basis of electroosmosis.

---

## Decoupled Capacitive-Gate Electroosmosis

I worked on a continuum model coupling modified Poisson-Boltzmann electrostatics with Stokes flow for high-conductivity electrolytes.

At high ionic concentration, classical dilute-solution approximations become insufficient.

The formulation therefore incorporated:

- finite ion-size steric effects,
- dynamic Stern-layer polarisation,
- nonlinear electric-double-layer behaviour.

The system used an asymmetric three-electrode geometry with an independently driven capacitive gate.

Controlling the relative phase between the gate actuation and tangential electric field allowed modulation of surface charge and therefore the direction and magnitude of electroosmotic forcing.

High-fidelity 2D axisymmetric finite-element simulations in COMSOL were used to study:

- parasitic vortex formation,
- phase-dependent pumping,
- volumetric flow rate,
- high-conductivity operation,
- suppression of Faradaic degradation.

The work was published as a **Featured Article in the Journal of Applied Physics**.

DOI: `10.1063/5.0345688`

---

# Aerodynamics & Active Flow Control

Aircraft performance depends strongly on the interaction between pressure distribution, viscous boundary layers, separation, and wake formation.

At high lift coefficients, preventing or delaying separation becomes especially important.

---

## Inter-IIT STOL Aircraft Optimisation

As part of the Inter-IIT Tech Meet, I worked on automated aerodynamic optimisation for a high-lift STOL aircraft concept.

Airfoil geometries were parameterised using a **12th-order Bernstein polynomial basis**.

A PPO-based optimisation framework explored this design space for high-lift configurations.

---

## FastFOIL

Part of this work required extending XFOIL to model **Co-Flow Jet active flow control**.

XFOIL couples:

1. an inviscid potential-flow solution,
2. an integral boundary-layer model,
3. viscous-inviscid interaction.

Introducing active mass injection and suction therefore requires modifying both the physical model and the numerical coupling.

I implemented:

- line-source terms,
- line-sink terms,
- wall-normal transpiration,
- modified integral boundary-layer momentum equations,
- corresponding Newton-Raphson Jacobian terms.

I also identified and corrected a station-indexing issue in the legacy `SETBL` Fortran routine that destabilised mass-flux computations during large parameter sweeps.

The resulting aircraft configuration achieved a reported takeoff lift coefficient of

\[
C_L = 9.49
\]

at approximately

\[
Re=10^6.
\]

---

# Hydrofoil Boundary Layers

## Project DOFT

Hydrofoils operate in water under many of the same aerodynamic principles governing airfoils, but the fluid properties change the relevant transport scales.

I conducted 2D CFD simulations of NACA and Eppler hydrofoil sections in ANSYS Fluent using the

\[
k-\omega\ \text{SST}
\]

turbulence model.

The project investigated boundary-layer separation and whether surface heating could be used as a flow-control mechanism.

Water has a relatively large Prandtl number,

\[
Pr\approx7,
\]

meaning momentum and thermal diffusion occur over significantly different scales.

The analysis showed that thermal transport remained concentrated close to the wall, making surface heating ineffective as a practical mechanism for manipulating the larger hydrodynamic boundary layer in the proposed configuration.

---

# Bio-Inspired Propulsion

## Project PowerKick

Biological swimmers often exploit compliant structures rather than perfectly rigid propulsors.

Their deformation interacts with vortex shedding and wake dynamics.

Project PowerKick explored a compliant monofin inspired by cetacean caudal-fin kinematics.

I developed a variable-thickness flexural rigidity distribution intended to balance:

- structural flexibility,
- thrust production,
- drag,
- wake interaction.

Coupled fluid-structure simulations in COMSOL were used to investigate how passive deformation affects the thrust-to-drag behaviour.

---

# Turbulence & Predictability

Turbulence remains one of the most interesting examples of a deterministic system with severe practical predictability limits.

Two initially nearby flow states

\[
\mathbf u_1(0)
\quad\text{and}\quad
\mathbf u_2(0)
\]

can separate rapidly under nonlinear evolution.

Define

\[
\delta\mathbf u(t)
=
\mathbf u_2(t)-\mathbf u_1(t).
\]

For sufficiently small perturbations, one may observe approximate finite-time exponential growth,

\[
\|\delta\mathbf u(t)\|
\sim
\|\delta\mathbf u(0)\|e^{\lambda t}.
\]

But real turbulent systems contain many interacting spatial and temporal scales.

The important question is not simply whether trajectories diverge.

It is whether the **present flow field contains structures that indicate how that divergence will occur**.

This connects:

- turbulence,
- chaos,
- reduced-order modelling,
- coherent structures,
- spectral analysis,
- scientific machine learning.

I am currently exploring questions in this area, but detailed methodology will be added only after the work is mature.

---

# Methods I Use

### Numerical

- Finite-element methods
- CFD
- Spectral analysis
- Reduced-order modelling
- Numerical PDEs

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
- dimensional reasoning

---

[Scientific ML](./scientific-ml) · [Publications](./publications) · [Blog](./blog/)


---

