---
layout: default
title: About
---

[Home](./) · [Scientific ML](./scientific-ml) · [Fluids](./fluid-dynamics) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Control](./controls-robotics) · [Publications](./publications)

# About

I'm **Adithya Lakshminarayanan**, an undergraduate studying **Engineering Design at IIT Madras**.

What interests me most is understanding complex systems well enough to either **predict them, control them, or build computational tools around them**.

That has naturally taken me across several areas:

- scientific machine learning,
- fluid mechanics,
- numerical methods,
- nonlinear dynamics,
- control,
- mechanistic interpretability,
- reinforcement learning,
- CAD/CAE,
- embedded systems.

The common thread is studying how a system transforms **information or state**.

---

# Physical Systems

For a physical system, I tend to think in terms of

$$
\text{Current State}
\rightarrow
\text{Governing Dynamics}
\rightarrow
\text{Future State}.
$$

A continuous dynamical system can be represented abstractly as

$$
\dot{\mathbf{x}}
=
f(\mathbf{x},\mathbf{u},t).
$$

Questions then become:

- What equations describe the system?
- Which approximations are justified?
- Which quantities dominate its behaviour?
- Is the system stable?
- How sensitive is it to perturbations?
- Can its dynamics be represented in fewer dimensions?
- Can it be controlled?

This is what drew me toward fluid mechanics, dynamical systems, scientific computing, and control.

---

# Learned Systems

A neural network raises surprisingly similar questions.

Given a model state and an input:

- where is information represented?
- how does that representation evolve?
- what computations are performed internally?
- which pathways actually influence the output?
- how does optimisation reshape those pathways?

A useful abstract picture is

$$
\mathbf{h}_{l+1}
=
F_l(\mathbf{h}_l),
$$

where $\mathbf{h}_l$ represents the internal state at layer $l$.

A model may contain useful information in $\mathbf{h}_l$ without necessarily routing that information correctly into the eventual output.

This is one reason I find mechanistic interpretability interesting.

---

# Computation

Between a mathematical model and a final result lies the part I enjoy most: making the system computationally tractable.

That can mean:

- discretising differential equations,
- modifying legacy Fortran solvers,
- building GPU training pipelines,
- writing embedded C++,
- connecting meshing and FEA software,
- designing real-time feedback loops,
- constructing retrieval and inference infrastructure.

I enjoy moving between theory and implementation rather than treating them as separate activities.

---

# Education

## Indian Institute of Technology Madras

**B.Tech in Engineering Design**  
2024–Present

**CGPA:** 9.00 / 10.00

My coursework has included:

- deep learning,
- linear algebra,
- control systems,
- geometric modelling,
- CAD,
- computation and visualisation.

---

# Broad Interests

## Mathematics

Linear algebra · optimisation · dynamical systems · numerical PDEs · spectral methods

## Physics

Fluid mechanics · turbulence · electrohydrodynamics · aerodynamics · hydrodynamics

## Machine Learning

Neural operators · mechanistic interpretability · reinforcement learning · representation learning

## Engineering

Control · embedded systems · robotics · CAD · FEA · simulation

## Computing

Python · C/C++ · Fortran · MATLAB · CUDA · Linux

---

# What I Use This Website For

This site is not intended to be a web version of my résumé.

Instead, I use it to organise:

1. technical areas I work in,
2. projects that taught me something useful,
3. research questions I find interesting,
4. notes explaining concepts I had to understand properly.

Most topics become considerably more interesting once the clean textbook formulation meets an actual numerical implementation.

Those details are usually what I want to write about.

---

[Home](./) · [Blog](./blog/) · [GitHub](https://github.com/pip-install-adithya)
