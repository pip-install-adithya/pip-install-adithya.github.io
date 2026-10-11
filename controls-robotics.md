---
layout: default
title: Dynamics, Control & Robotics
---

[Home](./) · [Scientific ML](./scientific-ml) · [Fluids](./fluid-dynamics) · [Interpretability](./interpretability-rl) · [AI Systems](./ai-systems) · [Publications](./publications)

# Dynamics, Control & Robotics

Control becomes necessary when a physical system must do more than simply evolve according to its natural dynamics.

We may want it to:

- follow a desired trajectory,
- reject disturbances,
- remain stable,
- operate despite incomplete measurements,
- respect actuator limits,
- and remain robust to modelling errors.

A typical feedback system can be viewed as

$$
\text{Sensing}
\rightarrow
\text{State Estimation}
\rightarrow
\text{Control}
\rightarrow
\text{Actuation}
\rightarrow
\text{Physical System}.
$$

My work in this area has primarily involved **vehicle dynamics, nonlinear control, flight-control systems, state estimation, embedded electronics, and simulation-based validation**.

---

# Narrow-Track Vehicle Dynamics

## Project Agilit-E

Narrow-track vehicles offer an interesting mobility problem.

Reducing vehicle width can improve manoeuvrability and road-space utilisation, but it also reduces the lateral distance between the tyre contact patches.

During cornering, lateral acceleration generates an overturning moment about the outer wheels.

A conventional wide vehicle primarily resists this through its track width. A sufficiently narrow vehicle instead benefits from **leaning into the turn**, similar to a motorcycle.

This introduces an additional controlled degree of freedom: **vehicle roll**.

---

## Modelling the Vehicle

A controller can only be as useful as the dynamic model on which its decisions are based.

For Project Agilit-E, I derived a **four-degree-of-freedom nonlinear state-space model** capturing interactions between:

- yaw motion,
- roll motion,
- vertical dynamics,
- lateral tyre behaviour.

A generic nonlinear dynamical system can be represented as

$$
\dot{\mathbf{x}}
=
f(\mathbf{x},\mathbf{u}),
$$

where:

- $\mathbf{x}$ contains the system states,
- $\mathbf{u}$ contains control inputs,
- $f$ describes the nonlinear vehicle dynamics.

The model also incorporates a three-tyre force representation and the kinematic constraints introduced by the reverse-trike architecture.

This becomes important at large lean angles and aggressive manoeuvres, where simple small-angle linearised models are no longer sufficient.

---

# Tilt Control

For a steady turn, an intuitive equilibrium lean relationship can be obtained by balancing gravitational and lateral effects:

$$
\tan\phi
=
\frac{a_y}{g},
$$

where:

- $\phi$ is the desired lean angle,
- $a_y$ is lateral acceleration,
- $g$ is gravitational acceleration.

Real vehicle control is substantially more complicated.

The system must account for:

- transient manoeuvres,
- actuator dynamics,
- torque limits,
- steering behaviour,
- state-estimation error,
- model uncertainty.

I developed a **Steer Direct Tilt Control architecture** combining:

- Nonlinear Model Predictive Control,
- cascaded PID feedback.

---

# Model Predictive Control

Model Predictive Control repeatedly predicts the future behaviour of a system over a finite horizon.

Conceptually, the controller solves

$$
\min_{\mathbf{u}_{0:N-1}}
\sum_{k=0}^{N-1}
\left(
\|\mathbf{x}_k-\mathbf{x}_{\mathrm{ref}}\|_Q^2
+
\|\mathbf{u}_k\|_R^2
\right),
$$

subject to the system dynamics and physical constraints.

Only the first control action is applied.

The optimisation is then solved again using the latest state estimate.

This makes MPC particularly attractive when actuator constraints and nonlinear behaviour matter explicitly.

---

# Processor-in-the-Loop Validation

Testing an unstable or highly dynamic controller directly on a physical vehicle is risky.

I therefore developed a **Processor-in-the-Loop simulation environment** using MATLAB/Simulink.

The vehicle remains simulated while the actual embedded processor executes the control algorithm.

This allows evaluation of:

- controller timing,
- numerical precision,
- communication delays,
- actuator demands,
- embedded implementation,
- failure cases,

before full physical deployment.

---

# State Estimation

Many states needed by a controller cannot be measured directly.

For vehicle roll estimation, I developed a sensor-fusion pipeline using a six-axis IMU.

Gyroscopes measure angular velocity accurately over short periods but accumulate bias when integrated.

Accelerometers provide a long-term gravity reference but are corrupted by translational acceleration.

A complementary filter combines both:

$$
\hat{\phi}_k
=
\alpha
\left(
\hat{\phi}_{k-1}
+
\omega_k\Delta t
\right)
+
(1-\alpha)\phi_{\mathrm{acc}},
$$

where:

- $\omega_k$ is measured angular velocity,
- $\phi_{\mathrm{acc}}$ is the accelerometer-based estimate,
- $\alpha$ determines the relative weighting.

The basic idea is simple:

**trust the gyroscope at high frequency and the accelerometer at low frequency.**

---

# Distributed Embedded Architecture

The vehicle uses multiple ESP32 controllers rather than relying on one central microcontroller for every task.

Communication between nodes uses **ESP-NOW**, allowing low-latency peer-to-peer data exchange.

The architecture supports distributed:

- sensing,
- control,
- actuator commands,
- telemetry.

I also developed a telemetry pipeline using:

- MQTT,
- Grafana,

for real-time monitoring of dynamic states and controller behaviour.

---

# Mechanically Decoupled Tilting Architecture

Control is only one part of the vehicle-stability problem.

The suspension geometry must also permit the chassis to lean without introducing undesirable suspension motion or steering interference.

I developed a mechanically decoupled architecture based on:

- a non-tilting suspension subframe,
- parallelogram suspension geometry,
- independent chassis tilt,
- multi-degree-of-freedom steering articulation.

The objective is to separate:

**vertical wheel motion caused by road disturbances**

from

**chassis roll used for vehicle balancing.**

A multi-DOF steering knuckle was designed to avoid kinematic binding during simultaneous large steering and tilt motions.

Dynamic behaviour was studied in Simulink and structural components were evaluated using finite-element analysis.

An **Indian patent application has been filed** for the architecture.

---

# Flight Control

## Project Tessera

Multirotor vehicles present another control problem.

Unlike a conventional aircraft, a multirotor generally has little passive attitude stability.

Its controller must continuously:

1. measure motion,
2. estimate attitude,
3. determine attitude error,
4. compute corrective moments,
5. modify motor thrust.

This entire loop must execute much faster than the characteristic dynamics of the vehicle.

---

# Embedded Flight-Control Firmware

I developed modular flight-control firmware in **C/C++ on an ESP32-WROOM-32** using FreeRTOS.

Separate real-time tasks handled:

- sensor acquisition,
- control computation,
- telemetry,
- communication.

Sensor acquisition operated at approximately **100 Hz**, while the cascaded controller operated at up to **200 Hz**.

---

# Cascaded PID Control

Rather than directly converting attitude error into motor commands, the controller uses two feedback loops.

The outer loop regulates attitude:

$$
e_\theta
=
\theta_{\mathrm{desired}}
-
\theta_{\mathrm{measured}}.
$$

Its output becomes a desired angular rate.

The inner loop then regulates angular velocity:

$$
e_\omega
=
\omega_{\mathrm{desired}}
-
\omega_{\mathrm{measured}}.
$$

A PID controller uses

$$
u(t)
=
K_P e(t)
+
K_I\int e(t)\,dt
+
K_D\frac{de(t)}{dt}.
$$

This cascaded structure allows the faster rotational-rate dynamics to be controlled separately from the slower attitude dynamics.

I also implemented:

- integrator anti-windup,
- dynamic gyro notch filtering.

---

# Empirical Controller Tuning

Manual PID tuning becomes difficult when the real system differs significantly from the simulated model.

I therefore developed an automated empirical tuning module based on modified **Ziegler-Nichols relay oscillation**.

A controlled oscillation is induced on the physical test rig.

The resulting response provides information about:

- system gain,
- characteristic period,
- stability margin,

from which initial controller gains can be estimated automatically.

---

# Flight-Control Hardware

I also designed and routed a **four-layer flight-stack PCB** containing:

- IMU,
- magnetometer,
- ESP32 controller,
- I²C interfaces,
- SPI interfaces,
- ESC connections,
- onboard power distribution.

PCB design becomes especially important in flight-control hardware because low-level sensor measurements coexist with rapidly switching, high-current motor electronics.

Attention must therefore be given to:

- grounding,
- signal integrity,
- power distribution,
- noise isolation.

---

# Physical Test Rigs

Before allowing unrestricted flight, I developed:

- one-degree-of-freedom rigs,
- three-degree-of-freedom gimbal rigs.

These were used for:

- system identification,
- thrust-curve characterisation,
- isolated-axis controller testing,
- empirical tuning.

Constrained test rigs allow instability and controller failure to be studied without immediately losing the vehicle.

---

# Why I Find Control Interesting

Control lies at an unusual intersection of several disciplines.

A successful controller may require understanding:

- differential equations,
- optimisation,
- numerical methods,
- sensing,
- filtering,
- embedded computation,
- electronics,
- mechanical design.

The most interesting systems are usually those where none of these can be considered independently.

---

[Home](./) · [Fluids](./fluid-dynamics) · [Publications](./publications)
