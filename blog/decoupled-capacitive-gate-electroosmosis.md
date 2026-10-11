---
layout: default
title: "Electro-osmosis Beyond the Single RC Pole"
description: "Why conventional AC electro-osmosis struggles in physiological electrolytes, and what changes when surface-charge control is separated from propulsion."
---

[Home](../) · [Fluids](../fluid-dynamics) · [Publications](../publications) · [Notes](./)

# Electro-osmosis Beyond the Single RC Pole

### Phase-controlled flow in high-conductivity electrolytes

In September 2026, our paper

**“Decoupled capacitive-gate electro-osmosis: Phase-controlled bidirectional flow in high-conductivity electrolytes via a modified Poisson–Boltzmann–Stokes framework”**

was published in the **Journal of Applied Physics**.

**Shriram Srihari and Adithya Lakshminarayanan**  
*Journal of Applied Physics* **140**, 124703 (2026)  
DOI: `10.1063/5.0345688`

This post is less a summary of the paper than an attempt to explain the physical problem that led to it.

The starting point is deceptively simple: if you want to move fluid through a microscopic channel, why use a mechanical pump at all?

At the microscale, moving parts are expensive. They introduce fabrication complexity, wear, sealing problems, extra volume, and usually an awkward mismatch between the size of the actuator and the size of the channel. Electrokinetic propulsion offers a much cleaner possibility: use an electric field to act on the ions already present in the fluid, and let their interaction with the liquid generate motion.

That works very well in some electrolytes.

Physiological fluids are where things get difficult.

Cerebrospinal fluid, for example, has conductivity around

$$
\sigma \approx 1.68\ \mathrm{S\,m^{-1}}.
$$

That is high enough that several assumptions behind conventional AC electro-osmosis begin to become uncomfortable at exactly the voltages needed to obtain useful flow.

The question we were interested in was therefore not simply whether electro-osmosis can move CSF. It was more specific:

> Can one obtain useful, reversible electro-osmotic transport in a highly conductive physiological electrolyte without pushing the electrode-electrolyte interface into an electrochemically destructive regime?

The answer turns out to depend on separating two physical jobs that conventional ACEO usually assigns to the same electrode.

---

## The thin charged layer that moves the fluid

Electro-osmosis begins with a surface in contact with an electrolyte.

Once the interface acquires charge, oppositely charged ions in the liquid are attracted toward it. The resulting charge distribution is not confined to a perfectly sharp sheet. Instead, one obtains an **electric double layer**, or EDL: a compact interfacial region near the wall and a diffuse ionic region extending into the liquid.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/edl-primer.svg' | relative_url }}"
    alt="Schematic of an electrical double layer showing the charged surface, compact layer and diffuse ionic layer."
    style="max-width:720px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Schematic of an electrical double layer. Credit: Guillaume Paumier,
    CC BY-SA 3.0, Wikimedia Commons.
  </figcaption>
</figure>

A useful length scale for this structure is the Debye length,

$$
\lambda_D
=
\sqrt{
\frac{\epsilon k_B T}
{2N_A z_0^2 e^2 C_0}
}.
$$

For the cerebrospinal-fluid conditions in our model,

$$
\lambda_D \approx 0.834\ \mathrm{nm}.
$$

So the electrically active region near the wall is sub-nanometre in scale, even though the channel itself is several micrometres wide.

That disparity of scales is one of the recurring difficulties in electrokinetic modelling.

Now apply an electric field along the wall. The net charge inside the EDL experiences an electrical body force,

$$
\mathbf{f}_e = \rho_e\mathbf{E}.
$$

The charged fluid near the surface moves, and viscous stresses transmit that motion into the bulk.

For a thin double layer, the result is often summarized by a Helmholtz–Smoluchowski-type slip relation,

$$
u_{\mathrm{EO}}
\sim
-\frac{\epsilon\zeta}{\eta}E_t,
$$

where $\zeta$ represents the wall electrokinetic potential and $E_t$ is the tangential electric field.

The most important part is the product:

$$
\boxed{
u_{\mathrm{EO}} \propto \zeta E_t
}
$$

Electro-osmotic propulsion needs two things:

**charge at the wall**, and **a tangential field acting on that charge**.

That sounds obvious, but conventional ACEO usually entangles them.

---

## Why the usual ACEO picture becomes restrictive

Alternating-current electro-osmosis avoids some of the problems of simply applying a large DC potential across an electrolyte.

Under AC forcing, the double layer repeatedly charges and discharges. With an asymmetric electrode geometry, these oscillatory processes can rectify into a non-zero mean flow.

The difficulty is that the EDL does not charge instantaneously.

A useful first approximation is an RC circuit: the conductive electrolyte supplies a resistance and the interface contributes a double-layer capacitance. The characteristic charging time is therefore

$$
\tau_{\mathrm{RC}}
=
RC_{\mathrm{EDL}},
$$

with characteristic frequency

$$
f_{\mathrm{RC}}
=
\frac{1}{2\pi\tau_{\mathrm{RC}}}.
$$

For our annular geometry, the radial Ohmic resistance is

$$
R
=
\frac{\ln(b/a)}
{2\pi\sigma L},
$$

and the resulting charging timescale becomes

$$
\tau_{\mathrm{RC}}
=
\frac{
\epsilon ab\ln(b/a)
}{
\sigma\lambda_D(a+b)
}.
$$

With

$$
a=6\ \mu\mathrm{m},
\qquad
b=20\ \mu\mathrm{m},
$$

the model gives

$$
\tau_{\mathrm{RC}}
\approx
2.81\ \mu\mathrm{s},
$$

or

$$
f_{\mathrm{RC}}
\approx
56.6\ \mathrm{kHz}.
$$

This creates the familiar ACEO trade-off.

At sufficiently low frequency, each half-cycle lasts long enough for undesirable electrochemical charge transfer to develop.

At sufficiently high frequency, the EDL cannot charge strongly enough during the cycle.

Useful flow is therefore tied to an electrical operating window.

In dilute electrolytes this can be manageable. In a highly conductive physiological medium, the available window becomes much less forgiving.

One might imagine compensating by simply increasing the applied voltage.

Unfortunately, the electrode-electrolyte interface is nonlinear.

---

## The price of increasing voltage

An ideally blocking interface stores charge capacitively,

$$
i_{\mathrm{dl}}
=
C_{\mathrm{dl}}
\frac{d\eta}{dt},
$$

where $\eta$ is the interfacial overpotential.

A real exposed electrode can also transfer charge chemically. The Faradaic contribution is described by Butler–Volmer kinetics,

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

The important feature is the exponential growth.

Near equilibrium, Faradaic current can remain small. Increase the overpotential sufficiently, and charge-transfer reactions rise rapidly.

The interface therefore carries

$$
i_{\mathrm{total}}
=
i_{\mathrm{dl}}
+
i_{\mathrm{F}}.
$$

For a biomedical actuator, we would like the first contribution to dominate.

The usual engineering instinct—raise the voltage until the flow becomes useful—therefore runs directly into the chemistry of the interface.

This was the point where the architecture itself seemed worth reconsidering.

---

## One electrode is being asked to do two jobs

Recall the thin-EDL scaling

$$
u_{\mathrm{EO}}
\propto
\zeta E_t.
$$

A conventional ACEO electrode participates in both sides of this expression.

It influences the wall charge that establishes $\zeta$, while also participating in the electric field that produces $E_t$.

The two processes therefore inherit strongly coupled electrical dynamics.

Our architecture separates them.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig05-architecture.png' | relative_url }}"
    alt="Planar and cylindrical representations of the decoupled capacitive gate electro-osmotic architecture."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    Decoupled capacitive-gate architecture. A buried gate controls the
    wall state while exposed propulsion electrodes generate the axial
    tangential field. Source: Fig. 5 of the paper.
  </figcaption>
</figure>

A **buried gate electrode** lies beneath a thin Al$_2$O$_3$ dielectric.

Because the gate does not directly contact the electrolyte, it can modulate the interfacial potential capacitively without itself acting as a Faradaic electrode.

Conceptually,

$$
V_{\mathrm{gate}}
\longrightarrow
\zeta_{\mathrm{ind}}.
$$

A separate pair of exposed propulsion electrodes controls the bulk electric field,

$$
V_{\mathrm{prop}}
\longrightarrow
E_t.
$$

The resulting flow is produced by their interaction,

$$
U
\sim
\zeta_{\mathrm{ind}}E_t.
$$

This is the main architectural idea.

Not “a better electrode shape,” and not simply “more voltage,” but a separation of **surface-charge control** from **field generation**.

Each branch can then be limited and tuned according to the physics relevant to it.

---

## The geometry we modelled

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig01-geometry.png' | relative_url }}"
    alt="Axisymmetric cylindrical channel geometry with buried gate and propulsion electrodes."
    style="max-width:720px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Representative cylindrical geometry used in the mathematical model.
    Source: Fig. 1 of the paper.
  </figcaption>
</figure>

The representative device is an annular cylindrical channel with dimensions of approximately

$$
a=6\ \mu\mathrm{m},
\qquad
b=20\ \mu\mathrm{m},
\qquad
L\approx120\ \mu\mathrm{m}.
$$

The buried gate modifies the wall state through the dielectric. Asymmetric exposed propulsion electrodes establish the tangential field along the channel.

The geometry is axisymmetric, which also makes a 2D axisymmetric multiphysics formulation possible without discarding the essential cylindrical structure.

---

## Classical Poisson–Boltzmann theory predicts something impossible

Once the architecture was separated electrically, another problem became impossible to ignore.

At low potential and low concentration, the electric double layer is often described by classical Poisson–Boltzmann theory. For a symmetric electrolyte, the ion concentrations have the exponential form

$$
C_{\pm}
\propto
\exp
\left(
\mp\frac{z_0e\psi}{k_BT}
\right).
$$

This treats ions as point particles.

At small potential, that is often a useful approximation.

At large wall potential, it becomes pathological.

The model permits counterion concentration to grow exponentially without any excluded-volume limit. Real hydrated ions obviously cannot pack infinitely densely.

For our operating regime,

$$
\psi_{\mathrm{gate}}
\approx
0.15\ \mathrm{V},
$$

whereas the thermal voltage at room temperature is only

$$
V_T
=
\frac{k_BT}{e}
\approx
25.7\ \mathrm{mV}.
$$

This is far outside the small-potential Debye–Hückel regime.

If the effective hydrated-ion diameter is taken as roughly

$$
a_s
\approx
0.4\ \mathrm{nm},
$$

then the corresponding packing ceiling is

$$
C_{\max}
=
\frac{1}{N_Aa_s^3}
\approx
26\ \mathrm{M}.
$$

The classical model eventually predicts concentrations beyond this physical limit.

That is not merely an aesthetic problem with the mathematics. It means the model can overestimate the charge stored near the wall, and therefore overestimate electro-osmotic slip.

---

## Steric saturation and the modified Poisson–Boltzmann model

We therefore used a lattice-gas, Bikerman-type modified Poisson–Boltzmann model.

The steric crowding parameter is

$$
\nu
=
2N_Aa_s^3C_0.
$$

For the CSF composition in the model,

$$
\nu\approx0.011.
$$

The potential scale beyond which finite-size effects become important is approximately

$$
\psi_c
=
\frac{k_BT}{z_0e}
\ln\left(\frac{2}{\nu}\right)
\approx
130\ \mathrm{mV}.
$$

Our representative gate-induced wall potential,

$$
150\ \mathrm{mV},
$$

already lies beyond this scale.

So steric saturation is not a small perturbative correction. It is part of the dominant physics of the operating regime.

The modified concentrations become

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

The denominator is the essential difference.

At low potential, the correction disappears and classical Poisson–Boltzmann behaviour is recovered.

At high potential, the finite packing term suppresses the unbounded exponential accumulation of counterions.

The corresponding modified Poisson equation is

$$
\nabla^2\psi
=
\frac{
2N_Az_0eC_0
}{
\epsilon
}
\frac{
\sinh(z_0e\psi/k_BT)
}{
1+
2\nu
\sinh^2
\left(
\frac{z_0e\psi}{2k_BT}
\right)
}.
$$

The effect is easiest to see graphically.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig06-steric-crowding.png' | relative_url }}"
    alt="Comparison of classical Poisson Boltzmann concentration with Bikerman modified Poisson Boltzmann saturation."
    style="max-width:700px;width:80%;display:block;margin:auto;"
  >
  <figcaption>
    Classical Poisson–Boltzmann theory eventually exceeds the physical
    ion-packing limit, while the Bikerman-modified model saturates.
    Source: Fig. 6 of the paper.
  </figcaption>
</figure>

This plot is one of the most useful sanity checks in the paper.

A physical model should not predict that more hydrated ions occupy a volume than can geometrically fit inside it.

---

## From the double layer back to the flow

Once the charge distribution is known, it enters the fluid mechanics through the electrokinetic body force.

At the Reynolds numbers relevant here, inertial effects are negligible. The momentum equation therefore reduces to the Stokes regime.

For the axisymmetric axial velocity,

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

Using Poisson's equation and the wall conditions gives a Helmholtz–Smoluchowski-like result,

$$
u_z(r,t)
=
-\frac{\epsilon E_t(t)}{\eta}
\left[
\zeta_{\mathrm{ind}}(t)
-
\psi\left(r;\zeta_{\mathrm{ind}}(t)\right)
\right].
$$

The area-averaged velocity is then

$$
\bar U(t)
=
-\frac{\epsilon E_t(t)}{\eta}
\left[
\zeta_{\mathrm{ind}}(t)
-
\frac{2}{a^2}
\int_0^a
\psi\left(r;\zeta_{\mathrm{ind}}(t)\right)r\,dr
\right].
$$

This is a more complete statement than the elementary slip formula, but structurally the same idea remains visible:

$$
U
\propto
E_t\zeta_{\mathrm{ind}}.
$$

That bilinear structure is what later makes phase useful as a control variable.

---

## Why the reduced model can treat the double layer as quasi-static

There are three relevant timescales.

The Debye-layer relaxation time is

$$
\tau_d
=
\frac{\lambda_D^2}{D}.
$$

For the parameters in the paper,

$$
\tau_d
\approx
4\times10^{-10}\ \mathrm{s}.
$$

The electrical charging timescale is

$$
\tau_{\mathrm{RC}}
\approx
2.81\ \mu\mathrm{s},
$$

while the representative actuation frequency

$$
f=2.5\ \mathrm{kHz}
$$

corresponds to a period

$$
\frac{1}{f}
=
400\ \mu\mathrm{s}.
$$

The ordering is therefore

$$
\boxed{
\tau_d
\ll
\tau_{\mathrm{RC}}
\ll
\frac{1}{f}
}
$$

by a considerable margin.

That gives the reduced model a useful simplification: the radial EDL can be treated as essentially equilibrated with the instantaneous wall potential while the external waveform evolves much more slowly.

But we did not want the conclusions to depend entirely on that approximation.

---

## Two models, deliberately built differently

The paper therefore uses two independent modelling routes.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig02-modeling-workflow.png' | relative_url }}"
    alt="Flowchart showing the independent one-dimensional analytical and two-dimensional numerical modelling paths."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    The two modelling routes used for cross-verification. Source: Fig. 2
    of the paper.
  </figcaption>
</figure>

The first is a reduced analytical path.

It combines the capacitive gate model with a one-dimensional radial Bikerman-MPB solution and then integrates the resulting electro-osmotic velocity profile.

The second is a 2D axisymmetric COMSOL model coupling:

**Electric Currents**, **Transport of Diluted Species**, and **Creeping Flow**.

The ionic transport model includes six major CSF species:

Na$^+$, Cl$^-$, K$^+$, Ca$^{2+}$, Mg$^{2+}$, and HCO$_3^-$.

The two approaches are intentionally not identical.

One asks whether the mechanism can be represented compactly.

The other asks whether the same behaviour survives when bulk ionic transport, realistic geometry, electrical conduction and Stokes flow are solved together.

That makes agreement between them substantially more informative than simply refining one numerical model.

Before using the 2D model for parameter studies, we also checked mesh convergence. The final fine discretisation contained approximately

$$
182\,450
$$

elements, with velocity, electric-field, current-density and ionic-concentration quantities stabilizing under further refinement.

---

## Phase is where the decoupling becomes interesting

Separating wall charging from tangential-field generation does something more useful than merely widening a design space.

It creates a new independent variable: the **relative phase** between the two signals.

Let

$$
\psi_{\mathrm{gate}}(t)
=
\psi_{\mathrm{gate}}
\sin(\omega t+\theta),
$$

while the propulsion signal is

$$
V_{\mathrm{prop}}(t)
=
V_{\mathrm{prop}}
\sin(\omega t).
$$

In the quasi-static regime,

$$
\zeta_{\mathrm{ind}}(t)
\propto
\psi_{\mathrm{gate}}(t),
$$

and

$$
E_t(t)
\propto
V_{\mathrm{prop}}(t).
$$

Therefore

$$
U(t)
\propto
\sin(\omega t+\theta)\sin(\omega t).
$$

Averaging over one cycle gives

$$
\left\langle U\right\rangle
\propto
\frac{\omega}{2\pi}
\int_0^{2\pi/\omega}
\sin(\omega t+\theta)
\sin(\omega t)\,dt,
$$

and therefore

$$
\boxed{
\left\langle U\right\rangle
\propto
\frac{1}{2}\cos\theta
}
$$

This simple result is probably my favourite part of the model.

At

$$
\theta=0,
$$

the two drives reinforce each other and the time-averaged flow is maximally forward.

At

$$
\theta=\frac{\pi}{2},
$$

the cycle average vanishes.

At

$$
\theta=\pi,
$$

the sign reverses.

Nothing about the geometry changes.

Neither voltage amplitude needs to change.

The driving frequency does not need to change.

Flow direction is controlled by phase.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig07-parametric-results.png' | relative_url }}"
    alt="Four-panel parametric result showing ionic concentrations, phase-dependent velocity, voltage scaling and frequency response."
    style="max-width:950px;width:98%;display:block;margin:auto;"
  >
  <figcaption>
    The main parametric results. Panel (b) shows the phase-controlled
    reversal, while panel (d) shows the broad response in the
    non-dimensional driving variable. Source: Fig. 7 of the paper.
  </figcaption>
</figure>

The resulting phase curve is approximately cosine-like, exactly as the reduced derivation suggests.

This turns phase into a software-controlled propulsion variable.

A single structure can move continuously through forward flow, zero mean flow, and reverse flow simply by changing the delay between two electrical signals.

---

## The voltage dependence is almost embarrassingly simple

The same bilinear structure predicts

$$
\langle U\rangle
\propto
\psi_{\mathrm{gate}}V_{\mathrm{prop}}.
$$

The gate controls the strength of the wall state.

The propulsion electrode controls the field acting on it.

To expose this scaling, we defined

$$
\tilde w
=
\frac{
\langle U\rangle_t\eta L
}{
\epsilon\psi_{\mathrm{gate}}V_{\mathrm{prop}}
}.
$$

Across the investigated range, the full 2D model gives approximately

$$
\tilde w\approx0.4,
$$

while the independent 1D model gives a similar value.

This collapse matters more than the numerical value itself.

It says that once the obvious voltage product is divided out, both modelling approaches see essentially the same transport efficiency.

At the representative operating point

$$
\psi_{\mathrm{gate}}=0.15\ \mathrm{V},
$$

$$
V_{\mathrm{prop}}=1.2\ \mathrm{V},
$$

$$
f=2.5\ \mathrm{kHz},
$$

and

$$
\theta=0,
$$

the calculated mean velocity is approximately

$$
\boxed{
\langle U\rangle
\approx
600\ \mu\mathrm{m\,s^{-1}}
}
$$

in the CSF model.

That is the attractive number.

It is not, however, the design criterion.

A biomedical electrokinetic actuator that achieves high velocity while disturbing ionic balance or generating excessive heat is not useful.

---

## The operating window is set by more than flow rate

To combine the effects of frequency and voltage, the analysis uses the dimensionless driving number

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

with

$$
V_T
=
\frac{k_BT}{e}.
$$

The velocity response exhibits a comparatively broad plateau in this variable instead of being confined to one narrow single-pole peak.

But the practical window is narrower than the velocity plateau.

The useful region is approximately

$$
2\times10^{-4}
\lesssim
\Pi_f
\lesssim
10^{-3}.
$$

The lower side is constrained mainly by electrochemical and ionic effects. If the field reverses too slowly, Faradaic processes have more time to proceed during each half-cycle, producing local concentration polarisation.

As frequency increases, each half-cycle becomes shorter. Charge-transfer reactions have less time to alter the surrounding electrolyte before the field reverses.

This creates an important distinction:

> The best operating frequency is not necessarily the frequency that maximizes velocity.

It is the frequency that gives enough transport while keeping the electrolyte chemically and thermally inside an acceptable regime.

---

## Ionic transport reveals something voltage magnitude alone cannot

The simulations make this particularly clear when looking at ion-flux streamlines.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig10-ion-flux-balance.png' | relative_url }}"
    alt="Ion concentration fields and flux streamlines for different gate voltages."
    style="max-width:900px;width:95%;display:block;margin:auto;"
  >
  <figcaption>
    Representative concentration fields and ion-flux streamlines. Near
    the balanced condition, transport remains comparatively axial;
    imbalance bends the flux toward the propulsion electrode. Source:
    Fig. 10 of the paper.
  </figcaption>
</figure>

When the gate-induced and propulsion-induced potentials are appropriately balanced, the ionic flux remains comparatively axial.

Move away from that balance and the electric field develops a stronger transverse component.

The flux curves toward the propulsion electrode, producing stronger local accumulation or depletion.

This is a useful reminder that there is no single scalar called “safe voltage.”

The same nominal voltage magnitude can produce very different local behaviour depending on how the fields interact geometrically.

---

## Each branch fails for a different reason

The decoupled architecture is useful partly because its two branches encounter different physical limits.

The buried gate is insulated from the electrolyte by a thin Al$_2$O$_3$ dielectric.

That suppresses direct Faradaic exchange, but it introduces a dielectric-reliability limit instead.

For the representative

$$
d=30\ \mathrm{nm}
$$

oxide layer and a conservative breakdown field of roughly

$$
E_{\mathrm{bd}}
\approx
5\ \mathrm{MV\,cm^{-1}},
$$

the corresponding wall-potential ceiling is around

$$
\psi_{\mathrm{gate,max}}
\approx
0.15\ \mathrm{V}.
$$

The exposed propulsion electrodes face the complementary problem.

They are in direct contact with the electrolyte and are therefore constrained by Faradaic charge transfer.

We tracked the ratio

$$
\mathcal R(t)
=
\frac{|i_{\mathrm{F}}(t)|}
{|i_{\mathrm{dl}}(t)|}.
$$

The Faradaic fraction remains relatively small at modest voltage and then rises very rapidly.

Under the assumptions of the model, the resulting approximate surface-averaged upper limit is

$$
V_{\mathrm{prop}}
\lesssim
2.0\ \mathrm{V}.
$$

Putting the two constraints together gives the approximate operating envelope

$$
\boxed{
\psi_{\mathrm{gate}}
\lesssim
0.15\ \mathrm{V},
\qquad
V_{\mathrm{prop}}
\lesssim
2.0\ \mathrm{V}.
}
$$

The gate is limited mainly by dielectric reliability.

The propulsion electrode is limited mainly by electrochemistry.

This is precisely the sort of separation we wanted from the architecture: each function can be designed around its own failure mechanism instead of inheriting one combined compromise.

---

## Heating turns out not to be the dominant constraint

Electrical actuation also produces Joule heating,

$$
Q_e
=
\mathbf{J}\cdot\mathbf{E}
\approx
\sigma|\mathbf{E}|^2.
$$

The temperature field obeys

$$
\rho_fC_p
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

The quadratic dependence on field strength means that increasing voltage becomes thermally expensive much faster than it becomes hydrodynamically useful.

At practical propulsion voltages,

$$
V_{\mathrm{prop}}
\leq
1.2\ \mathrm{V},
$$

the predicted temperature rise remained below roughly

$$
0.01\ \mathrm{K}.
$$

Even at the deliberately aggressive condition

$$
V_{\mathrm{prop}}=4\ \mathrm{V},
$$

the reported maximum rise was only about

$$
0.16\ \mathrm{K}.
$$

In the representative regime, thermal limits were therefore less restrictive than electrochemical and ionic constraints.

That was useful, because it told us where the actual design pressure lies.

---

## The reduced model and the full simulation nearly agree

The strongest internal check was to compare the compact 1D model against the 2D multiphysics solution over complete AC cycles.

<figure>
  <img
    src="{{ '/assets/images/electroosmosis/paper-fig12-model-cross-validation.png' | relative_url }}"
    alt="Comparison of one-dimensional analytical and two-dimensional numerical exit velocity over two AC cycles."
    style="max-width:720px;width:82%;display:block;margin:auto;"
  >
  <figcaption>
    Instantaneous exit velocity predicted independently by the reduced
    model and the full 2D simulation. Source: Fig. 12 of the paper.
  </figcaption>
</figure>

At

$$
\psi_{\mathrm{gate}}=0.15\ \mathrm{V},
\qquad
V_{\mathrm{prop}}=1.2\ \mathrm{V},
\qquad
f=2.5\ \mathrm{kHz},
$$

the two predictions remain within approximately

$$
5\%-8\%
$$

of each other over complete cycles.

That agreement supports two things at once.

First, the timescale ordering behind the quasi-static EDL approximation is reasonable in the regime we care about.

Second, the sterically corrected double-layer model appears to retain the dominant nonlinear physics without requiring the reduced model to resolve full radial time-dependent ion transport.

There is also a simpler sanity check.

If the nonlinear electrochemical physics is deliberately disabled, classical induced-charge electro-osmosis should recover approximately quadratic voltage scaling,

$$
\langle U\rangle
\propto
V_{\mathrm{prop}}^n.
$$

The fitted exponent was

$$
n=2.001.
$$

That is almost exactly the expected classical result.

Recovering the known limit is important: complicated models should become simple when the physics is made simple.

---

## What decoupling actually changes

It is tempting to summarize the paper as “a design that produces higher electro-osmotic flow.”

I think that misses the more interesting point.

The real change is in the **control structure** of the electrokinetic system.

A conventional ACEO electrode effectively participates in both

$$
\text{EDL charging}
$$

and

$$
\text{tangential-field generation}.
$$

Those mechanisms are therefore tied together by the same electrical architecture.

The decoupled device instead gives

$$
\text{gate}
\rightarrow
\zeta_{\mathrm{ind}},
$$

while independently

$$
\text{propulsion electrodes}
\rightarrow
E_t.
$$

Since

$$
U
\propto
\zeta_{\mathrm{ind}}E_t,
$$

the system acquires several independent control variables:

the gate amplitude, propulsion amplitude, actuation frequency, and relative phase.

The phase is the most interesting because it directly changes the **sign** of the mean flow.

A single device can therefore move continuously through

$$
\text{forward}
\rightarrow
\text{zero}
\rightarrow
\text{reverse}
$$

without mechanically changing anything.

That is much closer to a steerable actuator than to a conventional fixed-direction micropump.

---

## Where the model stops

There are several things this paper does not establish.

The results are computational, not an experimental demonstration.

The primary model is axisymmetric and assumes continuous ring-like electrodes. A fabricated device with segmented or imperfect electrodes would introduce 3D edge fields, azimuthal concentration gradients, secondary vortices and potentially stronger local heating.

The reduced model assumes

$$
\tau_d
\ll
\tau_{\mathrm{RC}}
\ll
\frac{1}{f}.
$$

Move far enough outside that ordering and the quasi-static treatment of the radial EDL will fail.

The effective capacitance model is also deliberately coarse at the molecular scale. It does not resolve specific ion adsorption, detailed Stern-layer restructuring, or every possible surface-charge-regulation mechanism.

Most importantly, the predicted velocity and phase reversal have not yet been directly measured in CSF.

The computational framework was instead checked through mesh convergence, agreement between independent models, recovery of the classical voltage-scaling limit, and comparison with earlier electrokinetic benchmarks.

The clean next experiment is therefore fairly obvious.

Hold

$$
f,
\qquad
V_{\mathrm{prop}},
\qquad
V_{\mathrm{gate}}
$$

fixed and sweep only

$$
\theta.
$$

Then measure the resulting flow using something like micro-PIV or micro-laser-Doppler velocimetry in a high-conductivity physiological analogue.

The key prediction is not a delicate one:

$$
\theta=0
\quad\Rightarrow\quad
\text{forward flow},
$$

$$
\theta=\frac{\pi}{2}
\quad\Rightarrow\quad
\text{approximately zero mean flow},
$$

$$
\theta=\pi
\quad\Rightarrow\quad
\text{reverse flow}.
$$

If that cosine-like reversal survives experimentally, it would be a particularly direct validation of the proposed mechanism.

---

## The part I would keep in one equation

If I had to compress the entire paper into one expression, it would still be

$$
U
\propto
\zeta_{\mathrm{ind}}E_t.
$$

Conventional architectures largely tie those two quantities together.

The decoupled architecture gives them separate physical controls.

Everything else—the broader frequency response, the independent voltage constraints, and especially phase-controlled reversal—follows from taking that separation seriously.

That was the core idea.

---

### Paper

**Shriram Srihari and Adithya Lakshminarayanan**

*Decoupled capacitive-gate electro-osmosis: Phase-controlled bidirectional flow in high-conductivity electrolytes via a modified Poisson–Boltzmann–Stokes framework.*

**Journal of Applied Physics 140, 124703 (2026)**

DOI: `10.1063/5.0345688`

---

[← All notes](./) · [Fluid Dynamics](../fluid-dynamics) · [Publications](../publications)
