---
layout: default
title: Notes
---

[Home](../) · [Scientific ML](../scientific-ml) · [Fluids](../fluid-dynamics) · [Interpretability](../interpretability-rl) · [AI Systems](../ai-systems) · [Control](../controls-robotics)

# Notes

Technical writing on things I have had to understand while researching, simulating, implementing, or debugging systems.

Most posts follow roughly the same pattern:

> **What is the problem? Why is it difficult? What does the mathematics say? What happens in an actual implementation?**

I use this section less as a conventional blog and more as a **technical notebook**.

---

# Featured

## [Electro-osmosis Beyond the Single RC Pole](./decoupled-capacitive-gate-electroosmosis)

### Phase-Controlled Flow in High-Conductivity Electrolytes

A detailed walkthrough of our **Journal of Applied Physics** paper on decoupled capacitive-gate electro-osmosis.

The article develops the problem from first principles:

- electric double layers,
- electro-osmotic slip,
- RC charging limits,
- Faradaic current,
- finite-ion-size effects,
- modified Poisson–Boltzmann theory,
- multiphysics simulation,
- phase-controlled flow reversal,
- electrochemical and thermal operating constraints.

It also explains why separating **surface-charge control** from **tangential-field generation** changes the operating characteristics of the system.

**Topics:** Electro-osmosis · Microfluidics · Poisson–Boltzmann · Stokes Flow · Electrochemistry · COMSOL

**Related publication:** *Journal of Applied Physics*, 140, 124703 (2026)

---

# Scientific Machine Learning

## Fourier Neural Operators from the Ground Up

Why learning an **operator** differs from ordinary finite-dimensional regression, how spectral convolution arises, and what an FNO layer is actually doing.

**Topics:** Neural Operators · Fourier Analysis · PDEs · Scientific ML

---

## Neural Operators vs Conventional Neural Networks

A conceptual comparison between learning

$$
f:\mathbb{R}^n\rightarrow\mathbb{R}^m
$$

and learning mappings between function spaces.

**Topics:** Operator Learning · Function Spaces · Scientific ML

---

## Physics-Informed Learning

Where physical structure can enter machine learning:

- governing equations,
- conservation laws,
- differentiable forward models,
- boundary conditions,
- symmetry.

And why adding physics does not automatically make a model better.

**Topics:** Physics-Informed ML · Differentiable Simulation · PDEs

---

# Dynamical Systems & Turbulence

## POD vs DMD: What Are We Actually Decomposing?

POD and DMD often appear next to each other because both start from snapshot matrices.

They answer very different questions.

- POD asks where the dominant variance or energy lies.
- DMD asks which structures exhibit coherent temporal evolution.

**Topics:** POD · DMD · SVD · Koopman Theory

---

## Predictability in Turbulent Systems

Why deterministic governing equations can still produce severe limits on useful prediction.

Topics include:

- perturbation growth,
- finite-time instability,
- Lyapunov behaviour,
- predictability horizons,
- coherent structures.

**Topics:** Turbulence · Chaos · Dynamical Systems

---

## Building a Pseudo-Spectral Navier–Stokes Solver

A numerical view of:

- Fourier differentiation,
- nonlinear advection,
- pressure projection,
- incompressibility,
- dealiasing,
- timestep integration.

**Topics:** CFD · Spectral Methods · Navier–Stokes

---

## What Is a Vortex, Mathematically?

A vortex is more subtle than “fluid rotating around a point.”

This note looks at:

- vorticity,
- circulation,
- velocity fields,
- pressure structure,
- coherent rotation.

**Topics:** Fluid Mechanics · Vorticity · Vector Calculus

---

# Fluid Mechanics & Numerical Modelling

## Boundary Layers from First Principles

Why viscosity can be negligible throughout most of a high-Reynolds-number flow while completely determining what happens near a wall.

**Topics:** Boundary Layers · Aerodynamics · Viscosity

---

## What XFOIL Is Actually Solving

Potential flow, panel methods, integral boundary-layer equations, viscous-inviscid coupling, and Newton iteration.

**Topics:** XFOIL · Aerodynamics · Fortran · Numerical Methods

---

## Why CFD Eventually Becomes Linear Algebra

How continuous governing equations become finite algebraic systems through discretisation.

**Topics:** CFD · PDEs · Linear Algebra · Numerical Methods

---

## What the Reynolds Number Really Means

Beyond “laminar vs turbulent”:

how nondimensionalisation reveals the competition between inertial and viscous effects.

**Topics:** Fluid Mechanics · Dimensional Analysis

---

# Mechanistic Interpretability

## Activation Patching Without the Magic

What activation patching actually changes, what causal statement it supports, and what it does **not** prove.

**Topics:** Transformers · Causal Intervention · Mechanistic Interpretability

---

## Direct Logit Attribution

How residual-stream components can be projected onto output directions and why logit contribution should not automatically be interpreted as a complete computational explanation.

**Topics:** DLA · Residual Stream · Transformers

---

## Edge Attribution Patching

Why exhaustive intervention over every computational path is expensive and how attribution-based approximations can identify candidate circuits.

**Topics:** EAP · Circuits · Causal Analysis

---

## Representation Similarity and CKA

How representations can be compared across:

- layers,
- models,
- training checkpoints,
- reasoning stages.

And why representational similarity alone does not establish functional equivalence.

**Topics:** CKA · Representation Learning · Interpretability

---

# Reinforcement Learning

## PPO from the Objective Function Up

A derivation-oriented explanation of:

- policy ratios,
- advantage estimation,
- clipping,
- KL control,
- why PPO is structured the way it is.

**Topics:** PPO · Policy Gradients · Reinforcement Learning

---

## GRPO vs PPO

How group-relative advantage estimation changes the optimisation problem, why a separate critic can be removed, and what new failure modes appear.

**Topics:** GRPO · PPO · Reasoning Models

---

## Reward Collapse in Small Reasoning Models

Why group-based optimisation can become ineffective when every sampled response receives essentially the same reward.

**Topics:** Reward Variance · RL · Reasoning Models

---

# Control & Robotics

## Experimental PID Tuning on a 3-DOF Flight-Control Testbed

Using a constrained multirotor rig to tune and validate PID gains experimentally.

Topics include:

- ultimate gain $K_u$,
- ultimate period $T_u$,
- Ziegler–Nichols initialization,
- axis-by-axis tuning,
- cross-axis coupling,
- overshoot and damping,
- why textbook gains still need manual refinement.

**Topics:** PID · Ziegler–Nichols · Flight Control · Experimental Control

---

## Why Cascaded PID Works

Why many physical systems become easier to control when fast inner-loop dynamics are separated from slower outer-loop dynamics.

**Topics:** PID · Feedback Control · Flight Control

---

## State Estimation from an IMU

Why:

- gyroscopes drift,
- accelerometers become unreliable during motion,
- combining both can produce a better orientation estimate.

**Topics:** State Estimation · IMU · Sensor Fusion

---

## MPC vs PID

When explicitly predicting future system behaviour is worth the computational cost, and when conventional feedback remains the better engineering solution.

**Topics:** MPC · PID · Optimal Control

---

## Processor-in-the-Loop Simulation

Why running the **real embedded controller** against a simulated plant catches problems that pure desktop simulation may miss.

**Topics:** Embedded Control · Simulation · Verification

---

# AI Systems

## Why LLM Agents Need Deterministic Tools

Why probabilistic language models are useful for interpreting engineering intent but should not directly replace deterministic numerical software.

**Topics:** AI Agents · Engineering AI · Tool Use

---

## How CAD Geometry Is Represented

B-Reps, faces, edges, loops, topology, geometry, and why CAD understanding naturally becomes graph-structured.

**Topics:** CAD · B-Rep · Computational Geometry

---

## Sparse, Dense, and Hybrid Retrieval

Why:

- BM25,
- embedding search,
- fuzzy matching

solve different retrieval problems, and why practical RAG systems often combine them.

**Topics:** RAG · BM25 · Embeddings · Search

---

## Why LLM Inference Becomes a Systems Problem

Prefill, decoding, KV caches, batching, quantisation, and why serving a model efficiently is very different from simply running one locally.

**Topics:** vLLM · SGLang · GPU Inference · LLM Systems

---

# Writing Status

Some posts above are already written.

Others are notes I plan to turn into full articles once I have either:

1. implemented the idea myself,
2. had to derive it carefully,
3. encountered a failure mode worth documenting,
4. or developed enough intuition to explain it without hiding behind notation.

The goal is not to publish frequently.

The goal is for each article to contain something I would have found genuinely useful while learning the topic.

---

[← Home](../)
