---
layout: default
title: "Electro-osmosis Beyond the Single RC Pole"
description: "How decoupling surface-charge control from tangential-field generation enables phase-controlled electro-osmotic flow in high-conductivity electrolytes."
---

[Home](../) · [Fluids](../fluid-dynamics) · [Publications](../publications) · [Notes](./)

# Electro-osmosis Beyond the Single RC Pole

## Phase-Controlled Flow in High-Conductivity Electrolytes

In September 2026, our work

**“Decoupled capacitive-gate electro-osmosis: Phase-controlled bidirectional flow in high-conductivity electrolytes via a modified Poisson–Boltzmann–Stokes framework”**

was published in the **Journal of Applied Physics**, Volume 140, Article 124703.

**Authors:** Shriram Srihari and Adithya Lakshminarayanan  
**DOI:** `10.1063/5.0345688`

This post explains the physical problem behind the paper, why conventional AC electro-osmosis becomes problematic in physiological electrolytes, the modelling decisions we made, and what the results actually mean.

---

# 1. The Problem We Started With

Suppose we want to move fluid through a microscopic channel.

At macroscopic scales, the obvious solution is some kind of mechanical pump.

At micrometre scales, that becomes much less attractive.

Mechanical components introduce:

- moving parts,
- fabrication complexity,
- wear,
- sealing problems,
- additional volume,
- difficult miniaturisation.

Electrokinetic transport offers a different approach:

> Use electric fields to move the ions already present in the fluid, and let their interaction with the liquid generate flow.

This is particularly appealing for microfluidics and potentially for small biomedical devices.

But physiological liquids create an unusually difficult operating environment.

Cerebrospinal fluid, for example, has an electrical conductivity of approximately

$$
\sigma \approx 1.68\ \mathrm{S\,m^{-1}}.
$$

That is **very conductive** compared with many dilute electrolytes used in classical electrokinetic experiments.

The central question behind our work was therefore:

> **Can useful, reversible electro-osmotic transport be generated in a highly conductive physiological electrolyte without relying on large voltages that drive damaging electrochemical reactions?**

To understand why that is difficult, we first need to understand the electric double layer.

---

# 2. The Electric Double Layer

When a solid surface comes into contact with an electrolyte, the interface generally becomes electrically charged.

Counterions in the liquid are attracted toward the surface while similarly charged ions are repelled.

This creates an **electric double layer**, or EDL.

<!-- EXTERNAL IMAGE 1: OPEN-LICENSE PRIMER -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/edl-primer.svg' | relative_url }}"
    alt="Schematic of an electrical double layer showing the charged surface, compact layer and diffuse ionic layer."
    style="max-width:720px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Electrical-double-layer structure. Credit: Guillaume Paumier,
    CC BY-SA 3.0, Wikimedia Commons.
  </figcaption>
</figure>

Very close to the surface lies a compact region of strongly associated charge.

Farther away lies the **diffuse layer**, where thermal motion competes with electrostatic attraction.

The electrostatic potential therefore decays from the wall toward its bulk value.

A useful characteristic length is the **Debye length**

$$
\lambda_D
=
\sqrt{
\frac{\epsilon k_B T}
{2N_A z_0^2 e^2 C_0}
}.
$$

Here:

- $\epsilon$ is fluid permittivity,
- $k_B$ is Boltzmann's constant,
- $T$ is temperature,
- $N_A$ is Avogadro's number,
- $z_0$ is ionic valence,
- $e$ is elementary charge,
- $C_0$ is bulk ion concentration.

For the CSF conditions considered in the paper,

$$
\lambda_D \approx 0.834\ \mathrm{nm}.
$$

That is extraordinarily thin compared with a micrometre-scale channel.

---

# 3. How an Electric Double Layer Produces Fluid Motion

Now apply an electric field tangential to the wall.

The net charge inside the EDL experiences an electrical body force.

If $\rho_e$ is the local space-charge density and $\mathbf{E}$ is the electric field,

$$
\mathbf{f}_e
=
\rho_e\mathbf{E}.
$$

The charged fluid near the surface moves under this force.

Viscosity transfers that momentum into the rest of the fluid.

This produces **electro-osmotic flow**.

For a sufficiently thin EDL, this is often represented by a Helmholtz–Smoluchowski-type slip relation:

$$
u_{\mathrm{EO}}
\sim
-\frac{\epsilon\zeta}{\eta}E_t,
$$

where:

- $\zeta$ is the wall electrokinetic potential,
- $\eta$ is dynamic viscosity,
- $E_t$ is the tangential electric field.

The key relationship is therefore roughly

$$
\boxed{
u_{\mathrm{EO}}
\propto
\zeta E_t
}
$$

and this simple product becomes extremely important later.

There are effectively **two things we need**:

1. surface charge, represented through $\zeta$;
2. a tangential electric field, $E_t$.

Conventional ACEO usually couples both of these to the same electrode system.

That is where the problem begins.

---

# 4. Why AC Electro-osmosis?

If we simply place electrodes in an electrolyte and apply a sufficiently large DC voltage, electrochemical reactions occur at the electrode surface.

That can produce:

- electrolysis products,
- local pH changes,
- bubbles,
- ionic concentration disturbances,
- electrode degradation.

AC electro-osmosis instead uses alternating fields.

The electrode repeatedly charges and discharges the double layer.

With asymmetric geometry, these oscillatory processes can rectify into a non-zero time-averaged flow.

But the EDL cannot charge infinitely quickly.

It has a characteristic electrical timescale.

---

# 5. The RC Bottleneck

A simplified electrode-electrolyte system behaves partly like an RC circuit.

The conducting electrolyte supplies a resistance $R$, while the electric double layer contributes a capacitance $C_{\mathrm{EDL}}$.

The characteristic charging time is

$$
\tau_{\mathrm{RC}}
=
RC_{\mathrm{EDL}}.
$$

The corresponding characteristic frequency is

$$
f_{\mathrm{RC}}
=
\frac{1}{2\pi\tau_{\mathrm{RC}}}.
$$

For the cylindrical annular geometry used in our work, the bulk radial resistance is

$$
R
=
\frac{\ln(b/a)}
{2\pi\sigma L},
$$

while the effective double-layer capacitance leads to

$$
\tau_{\mathrm{RC}}
=
\frac{
\epsilon ab\ln(b/a)
}{
\sigma\lambda_D(a+b)
}.
$$

For

$$
a=6\ \mu\mathrm{m},
\qquad
b=20\ \mu\mathrm{m},
$$

under the CSF conditions used in the study,

$$
\tau_{\mathrm{RC}}
\approx
2.81\ \mu\mathrm{s}
$$

and therefore

$$
f_{\mathrm{RC}}
\approx
56.6\ \mathrm{kHz}.
$$

Conventional ACEO flow tends to exist inside a comparatively narrow frequency window associated with this charging dynamics.

At low frequency, electrochemical charge transfer has enough time to become important.

At sufficiently high frequency, the EDL cannot respond strongly enough during each cycle.

The result is a restricted operating window.

---

# 6. Why High Conductivity Makes This Worse

CSF does not behave like the very dilute electrolytes commonly used to demonstrate conventional electro-osmotic devices.

Its conductivity is

$$
\sigma \approx 1.68\ \mathrm{S\,m^{-1}}.
$$

The high conductivity alters the electrical charging dynamics and makes it difficult to simply increase voltage to compensate for poor electro-osmotic performance.

Why not just increase the voltage?

Because electrode reactions are strongly nonlinear.

As the electrode overpotential rises, **Faradaic current** increases rapidly.

---

# 7. Capacitive Current vs Faradaic Current

An ideal blocking interface stores charge capacitively.

Its double-layer current density is

$$
i_{\mathrm{dl}}
=
C_{\mathrm{dl}}
\frac{d\eta}{dt},
$$

where $\eta$ is the interfacial overpotential.

But a real electrode can also exchange charge electrochemically with the liquid.

The Faradaic branch is described using Butler–Volmer kinetics:

$$
i_{\mathrm{F}}
=
i_0
\left[
\exp\left(
\frac{\alpha_a F\eta}{RT}
\right)
-
\exp\left(
-\frac{\alpha_c F\eta}{RT}
\right)
\right].
$$

This exponential dependence is the dangerous part.

<!-- EXTERNAL IMAGE 2 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/butler-volmer-current.svg' | relative_url }}"
    alt="Butler Volmer current-density versus electrode overpotential."
    style="max-width:520px;width:65%;display:block;margin:auto;"
  >
  <figcaption>
    Typical Butler–Volmer current-overpotential behaviour. Credit:
    Toshiyouri, CC BY-SA 4.0, Wikimedia Commons.
  </figcaption>
</figure>

Near equilibrium, Faradaic current may remain relatively small.

Once overpotential grows, however, charge-transfer reactions increase rapidly.

The total interfacial current is therefore

$$
i_{\mathrm{total}}
=
i_{\mathrm{dl}}
+
i_{\mathrm{F}}.
$$

For biomedical operation, we would ideally like the capacitive branch to dominate.

Simply pushing conventional ACEO to higher voltage is therefore not a clean solution.

---

# 8. The Central Design Idea: Separate the Two Jobs

Recall that electro-osmotic velocity depends roughly on

$$
u_{\mathrm{EO}}
\propto
\zeta E_t.
$$

A conventional electrode system tries to create both:

- the wall charge responsible for $\zeta$,
- the tangential field $E_t$.

We instead physically separated these functions.

<!-- PAPER FIGURE: Fig. 5, PDF page 10 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig05-architecture.png' | relative_url }}"
    alt="Planar and cylindrical representations of the decoupled capacitive gate electro-osmotic architecture."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    Decoupled electrode architecture. The buried gate controls wall
    charge, while exposed propulsion electrodes generate the tangential
    field. Source: Fig. 5 of the paper. Add the publisher-required credit
    line if reuse permission is applicable.
  </figcaption>
</figure>

The architecture contains two electrically distinct subsystems.

## Gate electrode

A **buried gate electrode** lies beneath a thin Al$_2$O$_3$ dielectric.

It does not directly contact the electrolyte.

Its role is to control the wall potential and therefore the EDL.

Conceptually,

$$
V_{\mathrm{gate}}
\longrightarrow
\zeta_{\mathrm{ind}}.
$$

Because the gate is capacitively isolated, it can modulate surface charge without itself providing a direct Faradaic current path into the electrolyte.

## Propulsion electrodes

A separate set of exposed asymmetric electrodes generates the axial tangential field:

$$
V_{\mathrm{prop}}
\longrightarrow
E_t.
$$

The electro-osmotic forcing then arises from their interaction:

$$
u
\sim
\zeta_{\mathrm{ind}}E_t.
$$

This separation is the conceptual heart of the paper.

Instead of forcing one electrode system to perform both tasks through one charging dynamics, **surface-charge control and field generation become independently tunable quantities**.

---

# 9. The Actual Geometry

<!-- OPTIONAL PAPER FIGURE: Fig. 1, PDF page 3 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig01-geometry.png' | relative_url }}"
    alt="Axisymmetric cylindrical channel geometry with buried gate and propulsion electrodes."
    style="max-width:720px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Geometry used for the mathematical model. Source: Fig. 1 of the paper.
  </figcaption>
</figure>

The representative cylindrical channel has:

$$
a=6\ \mu\mathrm{m},
$$

$$
b=20\ \mu\mathrm{m},
$$

and approximately

$$
L=120\ \mu\mathrm{m}.
$$

The buried gate controls the wall potential, while asymmetric propulsion electrodes establish the axial field.

The cylindrical geometry also allows the problem to be represented using a 2D axisymmetric numerical model.

---

# 10. Why Ordinary Poisson–Boltzmann Theory Was Not Enough

At low surface potential and low ionic concentration, the electric double layer is often modelled using classical Poisson–Boltzmann theory.

For a symmetric electrolyte, the classical ionic distributions have the familiar exponential form

$$
C_{\pm}
\propto
\exp
\left(
\mp
\frac{z_0e\psi}{k_BT}
\right).
$$

This assumes ions are effectively point particles.

At sufficiently high wall potential, this causes a physical problem.

The exponential distribution allows an arbitrarily large number of counterions to accumulate near the surface.

Real ions have finite hydrated size.

They cannot occupy the same volume.

For the conditions in our system,

$$
\psi_{\mathrm{gate}}
\approx
0.15\ \mathrm{V},
$$

while the thermal voltage is only

$$
V_T
=
\frac{k_BT}{e}
\approx
25.7\ \mathrm{mV}.
$$

So the system is far outside the small-potential Debye–Hückel regime.

---

# 11. Finite Ion Packing

Taking an effective hydrated-ion diameter

$$
a_s
\approx
0.4\ \mathrm{nm},
$$

the maximum physically packable concentration is

$$
C_{\max}
=
\frac{1}{N_Aa_s^3}
\approx
26\ \mathrm{M}.
$$

This immediately gives us a useful physical sanity check:

> A double-layer model predicting concentrations far above approximately 26 M cannot be physically meaningful under this finite-size representation.

The steric crowding parameter is

$$
\nu
=
2N_Aa_s^3C_0.
$$

For the CSF concentration used in the paper,

$$
\nu
\approx
0.011.
$$

The corresponding potential at which steric effects become dominant is approximately

$$
\psi_c
=
\frac{k_BT}{z_0e}
\ln\left(\frac{2}{\nu}\right)
\approx
130\ \mathrm{mV}.
$$

Our representative wall potential,

$$
150\ \mathrm{mV},
$$

is already beyond this scale.

Steric saturation is therefore not a tiny correction.

It is essential to obtaining physically admissible near-wall concentrations.

---

# 12. The Bikerman Modified Poisson–Boltzmann Model

To include finite ion size, we used a lattice-gas or **Bikerman modified Poisson–Boltzmann model**.

The modified ionic concentrations become

$$
C_+(\psi)
=
\frac{
C_0
\exp\left(-z_0e\psi/k_BT\right)
}{
1+
2\nu
\sinh^2
\left(
\frac{z_0e\psi}{2k_BT}
\right)
},
$$

and

$$
C_-(\psi)
=
\frac{
C_0
\exp\left(+z_0e\psi/k_BT\right)
}{
1+
2\nu
\sinh^2
\left(
\frac{z_0e\psi}{2k_BT}
\right)
}.
$$

The crucial term is the denominator.

At low potential,

$$
\nu\rightarrow0,
$$

and the classical Boltzmann result is recovered.

At high potential, the denominator suppresses the otherwise unbounded exponential accumulation.

The corresponding modified Poisson equation becomes

$$
\nabla^2\psi
=
\frac{
2N_Az_0eC_0
}{
\epsilon
}
\,
\frac{
\sinh(z_0e\psi/k_BT)
}{
1+
2\nu
\sinh^2
\left(
z_0e\psi/2k_BT
\right)
}.
$$

<!-- PAPER FIGURE: Fig. 6, PDF page 10 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig06-steric-crowding.png' | relative_url }}"
    alt="Comparison of classical Poisson Boltzmann concentration with Bikerman modified Poisson Boltzmann saturation."
    style="max-width:700px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Classical PB predicts rapidly increasing near-wall concentration,
    whereas the Bikerman model saturates at the finite packing limit.
    Source: Fig. 6 of the paper.
  </figcaption>
</figure>

This figure is one of the most important physical checks in the paper.

The classical curve eventually crosses the physical packing limit.

The modified model does not.

---

# 13. From Charge Distribution to Flow

The electrokinetic force density is

$$
\mathbf{f}_e
=
\rho_e(-\nabla\psi).
$$

At the very low Reynolds numbers relevant here, inertia is negligible and the fluid is governed by the Stokes limit.

For axial velocity $u_z(r,t)$, the governing equation becomes

$$
\frac{\eta}{r}
\frac{\partial}{\partial r}
\left(
r
\frac{\partial u_z}{\partial r}
\right)
+
N_Az_0e
\left[
C_+(\psi)-C_-(\psi)
\right]
E_t(t)
=
0.
$$

Using Poisson's equation and applying the wall conditions gives a Helmholtz–Smoluchowski-like velocity profile:

$$
u_z(r,t)
=
-\frac{\epsilon E_t(t)}{\eta}
\left[
\zeta_{\mathrm{ind}}(t)
-
\psi
\left(
r;\zeta_{\mathrm{ind}}(t)
\right)
\right].
$$

The area-averaged velocity is therefore

$$
\bar U(t)
=
-\frac{\epsilon E_t(t)}{\eta}
\left[
\zeta_{\mathrm{ind}}(t)
-
\frac{2}{a^2}
\int_0^a
\psi
\left(
r;\zeta_{\mathrm{ind}}(t)
\right)
r\,dr
\right].
$$

This was the central closed-form result of the reduced quasi-steady model.

Notice what remains visible even inside the more complete expression:

$$
\boxed{
U
\propto
E_t\zeta_{\mathrm{ind}}
}
$$

which is exactly why separating the two control mechanisms becomes useful.

---

# 14. Why a Quasi-Static Double Layer Was Reasonable

The model contains several characteristic timescales.

The Debye-layer relaxation time is

$$
\tau_d
=
\frac{\lambda_D^2}{D}.
$$

For the parameters used,

$$
\tau_d
\approx
4\times10^{-10}\ \mathrm{s}.
$$

Meanwhile,

$$
\tau_{\mathrm{RC}}
\approx
2.81\ \mu\mathrm{s},
$$

and at the representative operating frequency

$$
f=2.5\ \mathrm{kHz},
$$

the forcing period is

$$
\frac{1}{f}
=
400\ \mu\mathrm{s}.
$$

Therefore

$$
\boxed{
\tau_d
\ll
\tau_{\mathrm{RC}}
\ll
\frac{1}{f}
}
$$

by a substantial margin.

This separation of timescales motivates treating the radial double layer as quasi-equilibrated relative to the applied waveform in the reduced model.

---

# 15. Two Independent Modelling Paths

We did not rely on only one model.

The work used two different modelling pathways.

<!-- PAPER FIGURE: Fig. 2, PDF page 8 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig02-modeling-workflow.png' | relative_url }}"
    alt="Flowchart showing the independent one-dimensional analytical and two-dimensional numerical modelling paths."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    Independent analytical and numerical modelling pathways used for
    cross-verification. Source: Fig. 2 of the paper.
  </figcaption>
</figure>

## Branch A — reduced analytical model

The first branch uses:

- capacitive wall-potential modelling,
- a one-dimensional radial Bikerman-MPB solution,
- quasi-static double-layer behaviour,
- analytical slip integration.

This gives a fast reduced description of the mechanism.

## Branch B — multiphysics numerical model

The second branch is a 2D axisymmetric COMSOL model coupling:

- **Electric Currents**,
- **Transport of Diluted Species**,
- **Creeping Flow**.

The ionic transport includes six major CSF species:

- Na$^+$,
- Cl$^-$,
- K$^+$,
- Ca$^{2+}$,
- Mg$^{2+}$,
- HCO$_3^-$.

This model captures the channel geometry, bulk field, ionic transport, and resulting Stokes flow.

Using both models allowed the reduced theory to be checked against a substantially more detailed numerical calculation.

---

# 16. Mesh Independence

Before using the numerical model for parametric studies, we tested its sensitivity to spatial discretisation.

The final fine model used approximately

$$
182\,450
$$

elements.

Across the refinement sequence:

- exit velocity changed only negligibly,
- peak electric field and current density converged,
- further refinement of the boundary layer produced less than approximately 0.2% change in peak ionic concentrations.

This matters because sub-micrometre and nanometre electrochemical structures can otherwise produce numerical solutions that appear physically meaningful while still being mesh dependent.

---

# 17. The Most Interesting Result: Phase Becomes a Control Variable

Once wall charging and tangential-field generation are separated, their **relative phase** becomes an independently controllable quantity.

Let the wall-control signal be

$$
\psi_{\mathrm{gate}}(t)
=
\psi_{\mathrm{gate}}
\sin(\omega t+\theta),
$$

and the propulsion signal be

$$
V_{\mathrm{prop}}(t)
=
V_{\mathrm{prop}}
\sin(\omega t).
$$

Because

$$
\zeta_{\mathrm{ind}}(t)
\propto
\psi_{\mathrm{gate}}(t)
$$

and

$$
E_t(t)
\propto
V_{\mathrm{prop}}(t),
$$

the instantaneous flow scales approximately as

$$
U(t)
\propto
\sin(\omega t+\theta)
\sin(\omega t).
$$

Now average over one period:

$$
\left\langle U\right\rangle
\propto
\frac{\omega}{2\pi}
\int_0^{2\pi/\omega}
\sin(\omega t+\theta)
\sin(\omega t)\,dt.
$$

Using the product identity gives

$$
\boxed{
\left\langle U\right\rangle
\propto
\frac{1}{2}\cos\theta
}
$$

and therefore the flow direction follows a remarkably simple rule.

### $\theta=0$

$$
\cos 0=1
$$

Maximum forward flow.

### $\theta=\pi/2$

$$
\cos\left(\frac{\pi}{2}\right)=0
$$

Zero time-averaged flow.

### $\theta=\pi$

$$
\cos\pi=-1
$$

Full flow reversal.

This means the pump can be reversed **without changing the geometry, frequency, or voltage amplitudes**.

Only the phase relationship needs to change.

---

# 18. The Parametric Results

<!-- PAPER FIGURE: Fig. 7, PDF page 11 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig07-parametric-results.png' | relative_url }}"
    alt="Four-panel parametric result showing ionic concentrations, phase-dependent velocity, voltage scaling and frequency response."
    style="max-width:950px;width:98%;display:block;margin:auto;"
  >
  <figcaption>
    Main parametric results. Panel (b) demonstrates phase-controlled flow
    reversal, while panel (d) shows the broad non-dimensional frequency
    plateau. Source: Fig. 7 of the paper.
  </figcaption>
</figure>

Panel (b) directly shows the approximately cosine-like dependence of the time-averaged flow on phase.

This is important because the phase is now effectively a **software-controlled propulsion variable**.

The same physical structure can provide:

- forward motion,
- reduced forward motion,
- zero net motion,
- reverse motion.

---

# 19. Voltage Scaling

The analytical structure predicts approximately

$$
\langle U\rangle
\propto
\psi_{\mathrm{gate}}V_{\mathrm{prop}}.
$$

Increasing the gate potential strengthens the wall charge.

Increasing the propulsion voltage strengthens the tangential field.

Their product therefore sets the leading-order electro-osmotic forcing.

To make this behaviour easier to compare across different voltage combinations, we defined a non-dimensional transport efficiency

$$
\tilde w(\theta)
=
\frac{
\langle U\rangle_t\eta L
}{
\epsilon
\psi_{\mathrm{gate}}
V_{\mathrm{prop}}
}.
$$

The 2D model gives approximately

$$
\tilde w
\approx
0.4
$$

over the investigated range.

The independently derived 1D model gives a very similar value.

That collapse is useful because it shows that the dominant voltage dependence has been correctly isolated.

---

# 20. Representative Operating Point

A central operating point in the study was

$$
\psi_{\mathrm{gate}}
=
0.15\ \mathrm{V},
$$

$$
V_{\mathrm{prop}}
=
1.2\ \mathrm{V},
$$

$$
f
=
2.5\ \mathrm{kHz},
$$

and

$$
\theta=0.
$$

At this condition, the calculated time-averaged electro-osmotic velocity is approximately

$$
\boxed{
\langle U\rangle
\approx
600\ \mu\mathrm{m\,s^{-1}}
}
$$

for the CSF model used.

But velocity by itself is not enough.

A biomedical design also has to remain electrochemically and thermally safe.

---

# 21. The Dimensionless Driving Number

To combine voltage and frequency effects, the paper introduces

$$
\Pi_f
=
\frac{
fV_T
}{
\left|
V_{\mathrm{prop}}
+
\psi_{\mathrm{gate}}\cos\theta
\right|
f_{\mathrm{RC}}
},
$$

where

$$
V_T
=
\frac{k_BT}{e}
\approx
25.7\ \mathrm{mV}.
$$

When the response is plotted against $\Pi_f$, the useful velocity region extends across a broad plateau rather than showing only the narrow single-pole response expected from conventional coupled ACEO.

The practical safe region identified in the study lies approximately within

$$
2\times10^{-4}
\lesssim
\Pi_f
\lesssim
10^{-3}.
$$

The lower side is constrained predominantly by electrochemical concentration disturbances.

The upper side eventually encounters capacitive roll-off.

---

# 22. Ionic Concentration Is a Safety Constraint

A high flow velocity is not useful if the actuator significantly changes the chemical composition of the surrounding physiological liquid.

The model therefore tracked the principal ionic constituents of CSF.

At low enough actuation frequency, each AC half-cycle is long.

Faradaic reactions have more time to proceed before the field reverses.

This can produce local concentration polarisation.

Increasing frequency shortens the duration available for those reactions during each half-cycle.

The maximum ionic excursion therefore falls as the field reverses more rapidly.

The operating point must consequently lie in a region where:

1. ionic concentration excursions remain acceptable;
2. EDL charging remains effective enough to maintain useful flow.

This is a more meaningful design criterion than simply maximizing velocity.

---

# 23. Voltage Balance and Ion-Flux Geometry

An especially useful result from the simulations is that the spatial pattern of ion transport depends strongly on voltage balance.

<!-- OPTIONAL PAPER FIGURE: Fig. 10, PDF page 16 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig10-ion-flux-balance.png' | relative_url }}"
    alt="Ion concentration fields and flux streamlines for different gate voltages."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    Representative ion concentration and flux-streamline fields. Balanced
    potentials keep the flux comparatively axial, while imbalance bends
    flux toward the propulsion-electrode geometry. Source: Fig. 10 of the
    paper.
  </figcaption>
</figure>

When the gate-induced and propulsion-induced potentials are appropriately balanced, the ion-flux streamlines remain comparatively axial.

Moving away from this balance increases transverse field components.

The streamlines curve toward the propulsion electrode and generate stronger local concentration accumulation or depletion.

This illustrates an important point:

> Safe operation cannot be inferred from voltage magnitude alone; the spatial electric-field topology matters.

---

# 24. Dielectric Breakdown Sets the Gate Limit

The gate is isolated from the electrolyte by a thin Al$_2$O$_3$ dielectric.

This prevents direct Faradaic contact, but introduces a different limit:

**dielectric breakdown.**

For the representative

$$
d=30\ \mathrm{nm}
$$

Al$_2$O$_3$ layer, the simulation gives an approximately linear relation between applied terminal gate voltage and electric field in the dielectric.

Using a conservative dielectric-strength assumption of approximately

$$
E_{\mathrm{bd}}
\approx
5\ \mathrm{MV\,cm^{-1}},
$$

the representative breakdown-limited wall potential is approximately

$$
\psi_{\mathrm{gate,max}}
\approx
0.15\ \mathrm{V}.
$$

This is why

$$
\psi_{\mathrm{gate}}=0.15\ \mathrm{V}
$$

appears repeatedly in the operating analysis.

---

# 25. Faradaic Current Sets the Propulsion-Electrode Limit

The exposed propulsion electrodes have the opposite problem.

They are in contact with the electrolyte, so Faradaic activity must remain controlled.

The simulations evaluated the ratio

$$
\mathcal{R}(t)
=
\frac{
|i_{\mathrm{F}}(t)|
}{
|i_{\mathrm{dl}}(t)|
}.
$$

The surface-averaged Faradaic contribution remains comparatively small at low propulsion voltage but rises dramatically as the applied voltage increases.

The analysis identifies approximately

$$
V_{\mathrm{prop}}
\lesssim
2.0\ \mathrm{V}
$$

as the surface-averaged upper operating bound under the model assumptions.

The representative value

$$
V_{\mathrm{prop}}=1.2\ \mathrm{V}
$$

therefore remains well inside this limit.

---

# 26. The Resulting Safe Voltage Envelope

Combining dielectric breakdown at the gate with electrochemical limits at the propulsion electrode produces the approximate design envelope

$$
\boxed{
\psi_{\mathrm{gate}}
\lesssim
0.15\ \mathrm{V},
\qquad
V_{\mathrm{prop}}
\lesssim
2.0\ \mathrm{V}
}
$$

for the modelling assumptions used.

This is an important feature of the decoupled architecture:

> each subsystem is limited by a different physical mechanism.

The gate is primarily constrained by dielectric reliability.

The propulsion stage is primarily constrained by electrochemical charge transfer.

Separating the two functions allows each to be designed around its own physical limitation.

---

# 27. Joule Heating

Electrical actuation also heats the electrolyte.

The volumetric heat-generation term is approximately

$$
Q_e
=
\mathbf{J}\cdot\mathbf{E}
\approx
\sigma|\mathbf{E}|^2.
$$

The fluid temperature obeys the transient energy equation

$$
\rho_f C_p
\left(
\frac{\partial T}{\partial t}
+
\mathbf{u}\cdot\nabla T
\right)
=
\nabla\cdot(k\nabla T)
+
Q_e.
$$

Because heating scales approximately with

$$
|\mathbf{E}|^2,
$$

raising voltage to obtain additional velocity becomes increasingly expensive thermally.

At practical operating voltages in the paper,

$$
V_{\mathrm{prop}}
\leq
1.2\ \mathrm{V},
$$

the calculated temperature rise remained below approximately

$$
0.01\ \mathrm{K}.
$$

Even at the much more aggressive

$$
V_{\mathrm{prop}}=4\ \mathrm{V},
$$

the reported maximum rise was approximately

$$
0.16\ \mathrm{K}.
$$

So thermal limits were not the dominant restriction at the representative operating point.

Electrochemical and ionic constraints were more important.

---

# 28. Independent Model Cross-Validation

A useful model should not merely produce attractive plots.

We therefore compared the reduced 1D result with the independent 2D multiphysics solution.

<!-- PAPER FIGURE: Fig. 12, PDF page 17 -->
<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig12-model-cross-validation.png' | relative_url }}"
    alt="Comparison of one-dimensional analytical and two-dimensional numerical exit velocity over two AC cycles."
    style="max-width:720px;width:82%;display:block;margin:auto;"
  >
  <figcaption>
    Instantaneous exit velocity predicted by the reduced 1D model and
    the 2D axisymmetric multiphysics simulation. Source: Fig. 12 of the
    paper.
  </figcaption>
</figure>

At

$$
\psi_{\mathrm{gate}}
=
0.15\ \mathrm{V},
$$

$$
V_{\mathrm{prop}}
=
1.2\ \mathrm{V},
$$

and

$$
f=2.5\ \mathrm{kHz},
$$

the two predictions agree within approximately

$$
5\%-8\%
$$

over complete AC cycles.

This supports two important assumptions:

1. the timescale separation used by the quasi-static EDL model is reasonable in the investigated regime;
2. the Bikerman steric correction captures the dominant high-potential double-layer nonlinearity sufficiently well for the reduced model.

---

# 29. A Linear-Limit Sanity Check

Another useful numerical check is to deliberately move the model back toward the regime where classical theory should apply.

When nonlinear electrochemical effects were disabled, the predicted velocity was fitted against propulsion voltage as

$$
\langle U\rangle
\propto
V_{\mathrm{prop}}^n.
$$

The fitted value was

$$
n=2.001.
$$

That is essentially the expected quadratic scaling of classical linear induced-charge electro-osmosis.

Recovering known limiting behaviour is important because it tests whether a complicated nonlinear implementation reduces correctly when the additional physics is removed.

---

# 30. So What Did Decoupling Actually Buy Us?

The answer is not merely "more flow."

The important change is **control structure**.

A conventional coupled ACEO device ties several physical processes together:

$$
\text{electrode}
\rightarrow
\begin{cases}
\text{EDL charging}\\
\text{tangential field}
\end{cases}
$$

and both are strongly constrained by one charging response.

The decoupled architecture instead gives

$$
\text{gate}
\rightarrow
\zeta
$$

and independently

$$
\text{propulsion electrodes}
\rightarrow
E_t.
$$

That creates several new degrees of freedom:

- gate amplitude,
- propulsion amplitude,
- operating frequency,
- relative phase.

Most importantly,

$$
\boxed{
\theta
\text{ becomes an independent flow-direction control variable}
}
$$

rather than being effectively fixed by electrode geometry and RC dynamics.

---

# 31. Why the Phase Result Matters

The relation

$$
\langle U\rangle
\propto
\cos\theta
$$

looks mathematically simple.

Its engineering implication is much larger.

A single device can theoretically transition continuously between:

$$
\text{forward}
\rightarrow
\text{slower forward}
\rightarrow
\text{zero}
\rightarrow
\text{reverse}
$$

without physically reconfiguring the channel.

For a future electrokinetically propelled microdevice, that would mean flow direction could be controlled electronically through waveform phase alone.

---

# 32. What This Work Does *Not* Prove

It is important to separate a computational design study from an experimentally demonstrated device.

This work is computational.

Several simplifying assumptions remain.

## 1. Axisymmetry

The primary numerical model assumes continuous azimuthally uniform electrode rings.

A fabricated device with segmented electrodes could introduce:

- three-dimensional edge fields,
- azimuthal concentration gradients,
- secondary vortices,
- local thermal hotspots.

## 2. Quasi-static EDL approximation in the reduced model

The reduced model assumes

$$
\tau_d
\ll
\tau_{\mathrm{RC}}
\ll
\frac{1}{f}.
$$

Outside this ordering, fully time-resolved radial ion transport would become necessary.

## 3. Lumped double-layer capacitance

The effective gate model does not explicitly resolve every possible microscopic interfacial phenomenon such as:

- specific ion adsorption,
- detailed Stern-layer restructuring,
- surface-charge regulation.

## 4. No direct experimental validation yet

The flow velocities and phase-control behaviour have not yet been demonstrated experimentally in CSF.

The numerical framework was instead checked through:

- mesh convergence,
- independent reduced/full model comparison,
- recovery of classical voltage scaling,
- comparison against earlier electro-osmotic benchmarks.

An experimental demonstration remains the next important step.

---

# 33. What Would Be a Clean Experimental Test?

One particularly attractive prediction to validate is

$$
\boxed{
\langle U\rangle
\propto
\cos\theta
}
$$

because it is largely independent of absolute calibration of electro-osmotic mobility.

A possible experimental system would require:

- a microfabricated cylindrical or equivalent channel,
- a buried dielectric-isolated gate,
- exposed propulsion electrodes,
- a high-conductivity CSF analogue such as PBS,
- phase-controlled waveform generation,
- micro-PIV or micro-laser-Doppler velocimetry.

Then one could hold

$$
f,
\qquad
V_{\mathrm{prop}},
\qquad
V_{\mathrm{gate}}
$$

fixed while sweeping only

$$
\theta.
$$

The central experimental signature would be:

$$
\theta=0
\rightarrow
\text{forward flow},
$$

$$
\theta=\frac{\pi}{2}
\rightarrow
\text{approximately zero mean flow},
$$

$$
\theta=\pi
\rightarrow
\text{reverse flow}.
$$

That would be a particularly direct test of the physical mechanism proposed in the paper.

---

# 34. The Main Takeaway

The central insight of the work is relatively simple:

> **Do not force one electrode system to simultaneously control the double-layer charge and generate the propulsion field.**

Separating those functions changes the control problem.

The gate primarily determines

$$
\zeta_{\mathrm{ind}},
$$

while the propulsion electrodes determine

$$
E_t.
$$

Since

$$
U
\propto
\zeta_{\mathrm{ind}}E_t,
$$

their relative amplitude and phase become independently useful variables.

The combination of:

- decoupled surface-charge control,
- finite-ion-size double-layer modelling,
- nonlinear electrochemical constraints,
- multiphysics simulation,
- phase-controlled actuation,

produces a computational design framework for electro-osmotic flow in a regime where conventional dilute-electrolyte assumptions are no longer adequate.

---

# Paper

**Shriram Srihari and Adithya Lakshminarayanan**

*Decoupled capacitive-gate electro-osmosis: Phase-controlled bidirectional flow in high-conductivity electrolytes via a modified Poisson–Boltzmann–Stokes framework.*

**Journal of Applied Physics 140, 124703 (2026)**

DOI: `10.1063/5.0345688`

---

[← All notes](./) · [Fluid Dynamics](../fluid-dynamics) · [Publications](../publications)
