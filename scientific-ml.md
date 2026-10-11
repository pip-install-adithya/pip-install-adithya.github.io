[Home](./) · [Fluids](./fluid-dynamics) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Control](./controls-robotics) · [Publications](./publications)

# Scientific Machine Learning

Scientific machine learning sits between **numerical modelling and data-driven learning**.

In conventional machine learning, the goal is often to approximate a relationship between finite-dimensional inputs and outputs:

\[
f:\mathbb{R}^n\rightarrow\mathbb{R}^m.
\]

Physical systems are often different.

Their state may be a continuous field

\[
u(x,t),
\]

and the mathematical object we actually care about may be an operator mapping one function to another:

\[
\mathcal G:a(x)\mapsto u(x).
\]

This distinction motivates approaches such as **neural operators, physics-informed models, differentiable simulation, and learned reduced-order models**.

---

# Why Learn Physical Systems?

High-fidelity numerical simulation can be expensive.

A physical model may require:

- millions of degrees of freedom,
- very small timesteps,
- nonlinear iterative solvers,
- large parameter sweeps,
- or repeated optimisation.

Yet many engineering tasks require solving nearly the same physical problem thousands or millions of times.

Examples include:

- inverse design,
- uncertainty quantification,
- real-time control,
- optimisation,
- parameter estimation,
- digital twins,
- and rapid exploration of design spaces.

A learned surrogate can potentially approximate some of these expensive mappings much faster.

The difficult part is ensuring that speed does not come at the cost of destroying the structure of the underlying physics.

---

# Neural Operators

A conventional network learns between vectors.

A neural operator attempts to learn between **function spaces**:

\[
\mathcal G_\theta:
\mathcal A\rightarrow\mathcal U.
\]

This is particularly natural for PDE systems, because a PDE itself often defines a solution operator.

For example,

\[
a(x)
\longrightarrow
u(x)
\]

may represent the mapping from a spatially varying material property to the solution of a boundary-value problem.

Neural operators attempt to approximate this mapping directly.

Important families include:

- Fourier Neural Operators
- Wavelet Neural Operators
- DeepONets
- graph-based neural operators
- geometry-aware operators

---

# Why Fourier Representations?

Many PDEs are naturally connected to spectral representations.

Differentiation, for example, becomes multiplication in Fourier space:

\[
\frac{\partial u}{\partial x}
\quad\longleftrightarrow\quad
ik\hat u(k).
\]

Global spatial interactions can therefore become comparatively simple operations on spectral coefficients.

Fourier Neural Operators exploit this structure by learning transformations of selected spectral modes.

This makes them attractive for many smooth field problems, but also introduces limitations.

Fourier bases are global.

Highly localised structures, discontinuities, complex geometry, and strongly multiscale phenomena may require different representations or hybrid approaches.

---

# Physics-Informed Learning

Purely data-driven models rely on examples of the correct output.

Physical problems often provide an additional source of information:

\[
\mathcal N[u]=0,
\]

where \(\mathcal N\) represents the governing equation.

Physical constraints may enter learning through:

- PDE residuals,
- conservation laws,
- boundary conditions,
- differentiable forward models,
- symmetry,
- known invariants,
- geometric structure.

The interesting question is not simply whether physics can be added to a loss function.

It is **which physical information actually improves generalisation and which merely makes optimisation harder**.

---

# Inverse Problems

Forward problems ask:

\[
\text{cause}\rightarrow\text{effect}.
\]

Inverse problems ask:

\[
\text{observed effect}\rightarrow\text{unknown cause}.
\]

Examples include estimating:

- material parameters from deformation,
- source distributions from measured fields,
- boundary conditions from observations,
- optical phase from a desired intensity field.

Inverse problems are often difficult because the mapping may be:

- non-unique,
- unstable,
- nonlinear,
- computationally expensive.

Learning becomes especially useful when the same class of inverse problem must be solved repeatedly.

---

# Ongoing Interests

One area I am currently exploring is learning and prediction in **nonlinear dynamical systems**.

Even when the governing equations are deterministic, nearby initial states can evolve into dramatically different future states.

This creates fundamental questions:

- Which structures indicate future instability?
- How much information about future divergence exists in the present state?
- When does a reduced representation discard information that matters for predictability?
- Which spatial or spectral scales control finite-time evolution?

These questions are particularly interesting in turbulent fluid systems.

I am currently investigating this direction, but will add detailed methodology and results here only once the work is sufficiently mature.

---

# HoloFNO

I am also involved in ongoing work applying **neural operators to inverse problems in optical trapping**.

The broader problem is to efficiently determine optical control fields capable of producing desired trapping potentials.

Conventional iterative optimisation can be computationally expensive when such inverse problems must be solved repeatedly.

Neural operators provide one possible framework for learning mappings directly between continuous physical fields.

The work is currently **under review**, so implementation details and results are intentionally not described here.

---

# Topics I Am Interested In

```text
Scientific Machine Learning
├── Neural Operators
│   ├── Fourier
│   ├── Wavelet
│   └── Geometry-aware methods
│
├── Physics-Informed Learning
│   ├── Differentiable physics
│   ├── Conservation constraints
│   └── PDE structure
│
├── Dynamical Systems
│   ├── Predictability
│   ├── Reduced-order models
│   └── Learned evolution operators
│
└── Inverse Problems
    ├── Field reconstruction
    ├── Parameter inference
    └── Physics-constrained optimisation
```

---

## Related Notes

- Fourier Neural Operators from the Ground Up
- POD vs DMD
- Predictability in Turbulent Systems
- Spectral Methods for PDEs

[Blog →](./blog/)


---
