---
layout: default
title: Scientific Machine Learning
---

[Home](./) · [Fluids](./fluid-dynamics) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Control](./controls-robotics) · [Publications](./publications)

# Scientific Machine Learning

Scientific machine learning lies between **numerical modelling and data-driven learning**.

In conventional machine learning, the goal is often to approximate a finite-dimensional mapping:

$$
f:\mathbb{R}^n\rightarrow\mathbb{R}^m.
$$

Physical systems are often different.

Their state may instead be a continuous field

$$
u(x,t),
$$

and the mathematical object of interest may be an operator mapping one function to another:

$$
\mathcal{G}:a(x)\mapsto u(x).
$$

This distinction motivates approaches such as:

- neural operators,
- physics-informed learning,
- differentiable simulation,
- learned reduced-order models.

---

# Why Learn Physical Systems?

High-fidelity numerical simulation can be expensive.

A physical model may require:

- millions of degrees of freedom,
- very small timesteps,
- nonlinear iterative solvers,
- large parameter sweeps,
- repeated optimisation.

Yet many engineering tasks require solving nearly the same physical problem repeatedly.

Examples include:

- inverse design,
- uncertainty quantification,
- real-time control,
- optimisation,
- parameter estimation,
- digital twins,
- rapid design-space exploration.

A learned surrogate can potentially approximate some of these expensive mappings substantially faster.

The difficult part is ensuring that speed does not come at the cost of destroying important physical structure.

---

# Neural Operators

A conventional neural network typically learns between finite-dimensional vectors.

A neural operator instead attempts to learn a mapping between **function spaces**:

$$
\mathcal{G}_\theta:
\mathcal{A}\rightarrow\mathcal{U}.
$$

This is natural for PDE systems because a differential equation frequently defines a solution operator.

For example,

$$
a(x)\longmapsto u(x)
$$

may represent the mapping from a spatially varying material property to the corresponding solution field.

Neural operators attempt to approximate this mapping directly.

Important families include:

- Fourier Neural Operators,
- Wavelet Neural Operators,
- DeepONets,
- graph neural operators,
- geometry-aware neural operators.

---

# Why Fourier Representations?

Many PDE operations have natural spectral representations.

For example, differentiation becomes multiplication in Fourier space:

$$
\frac{\partial u}{\partial x}
\quad\longleftrightarrow\quad
ik\hat{u}(k).
$$

Likewise, convolution satisfies

$$
\mathcal{F}(f*g)
=
\mathcal{F}(f)\mathcal{F}(g).
$$

Fourier Neural Operators exploit this structure by learning transformations of selected Fourier modes.

This can make global spatial interactions computationally efficient.

However, Fourier bases are global.

Highly localised phenomena, complex geometries, discontinuities, or strongly multiscale behaviour may require alternative or hybrid representations.

---

# Physics-Informed Learning

Physical problems provide information beyond input-output examples.

A governing equation may be represented abstractly as

$$
\mathcal{N}[u]=0.
$$

Physical constraints may therefore enter learning through:

- PDE residuals,
- conservation laws,
- boundary conditions,
- differentiable forward models,
- symmetry,
- known invariants,
- geometric constraints.

The interesting question is not merely whether physics can be inserted into a loss function.

It is which physical constraints genuinely improve generalisation and which instead make optimisation unnecessarily difficult.

---

# Inverse Problems

Forward problems ask:

$$
\text{cause}
\rightarrow
\text{effect}.
$$

Inverse problems reverse the direction:

$$
\text{observed effect}
\rightarrow
\text{unknown cause}.
$$

Examples include estimating:

- material parameters from deformation,
- source distributions from measured fields,
- boundary conditions from observations,
- optical phase from a desired intensity field.

Inverse problems are frequently:

- non-unique,
- unstable,
- nonlinear,
- computationally expensive.

Learning becomes particularly attractive when the same family of inverse problems must be solved repeatedly.

---

# Dynamical Systems and Learned Evolution

A dynamical system evolves according to some rule such as

$$
\frac{d\mathbf{x}}{dt}
=
f(\mathbf{x},t).
$$

A learned evolution operator instead attempts to approximate mappings such as

$$
\mathcal{G}_{\Delta t}:
u(\mathbf{x},t)
\mapsto
u(\mathbf{x},t+\Delta t).
$$

Repeated application then produces

$$
u_t
\rightarrow
u_{t+\Delta t}
\rightarrow
u_{t+2\Delta t}
\rightarrow
\cdots.
$$

This provides one route toward fast surrogate models for systems whose numerical evolution is otherwise expensive.

---

# Reduced-Order Modelling

High-dimensional physical fields often contain considerable redundancy.

Instead of evolving the complete state, one can seek a lower-dimensional representation:

$$
u(\mathbf{x},t)
\approx
\sum_{i=1}^{r}
a_i(t)\phi_i(\mathbf{x}),
$$

where:

- $\phi_i$ are spatial basis functions,
- $a_i(t)$ are time-dependent coefficients,
- $r$ is much smaller than the original state dimension.

Techniques such as **Proper Orthogonal Decomposition** and **Dynamic Mode Decomposition** provide different ways of identifying useful low-dimensional structure.

The key question is whether the reduced coordinates preserve the information required for the downstream task.

---

# Turbulence and Predictability

One area I am currently interested in is learning and prediction in strongly nonlinear dynamical systems.

Suppose two initially nearby states satisfy

$$
\mathbf{u}_2(0)
=
\mathbf{u}_1(0)
+
\delta\mathbf{u}(0).
$$

Their separation at a later time is

$$
\delta\mathbf{u}(t)
=
\mathbf{u}_2(t)
-
\mathbf{u}_1(t).
$$

In a chaotic regime, sufficiently small perturbations may initially exhibit approximate exponential growth:

$$
\|\delta\mathbf{u}(t)\|
\sim
\|\delta\mathbf{u}(0)\|
e^{\lambda t},
$$

where $\lambda$ characterises finite-time instability.

The important questions are deeper than simply observing that trajectories diverge:

- Which present structures indicate future instability?
- Which scales dominate perturbation growth?
- Can a reduced representation preserve predictability information?
- How long does useful forecast information survive?

I am currently exploring this area, but detailed methodology will be added only once the work is sufficiently mature.

---

# HoloFNO

I am also involved in ongoing work applying **neural operators to inverse problems in optical trapping**.

The broader problem is to determine optical control fields capable of producing desired trapping potentials.

When such inverse problems must be solved repeatedly, iterative numerical optimisation can become computationally expensive.

Neural operators provide one framework for learning mappings directly between continuous physical fields.

The work is currently **under review**, so detailed architecture, methodology, and experimental results are intentionally omitted here.

---

# Topics I Am Interested In

### Scientific Machine Learning

- Neural operators
- Physics-informed learning
- Differentiable simulation
- Operator learning
- Inverse problems

### Dynamical Systems

- Predictability
- Reduced-order modelling
- Learned evolution operators
- Instability

### Representations

- Fourier methods
- Wavelets
- Spectral decompositions
- Geometry-aware methods

---

[Home](./) · [Fluids](./fluid-dynamics) · [Blog](./blog/)
