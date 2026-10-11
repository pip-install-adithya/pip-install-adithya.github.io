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

A feedback-controlled physical system can be viewed broadly as

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

Narrow-track vehicles provide an interesting vehicle-dynamics problem.

Reducing vehicle width can improve manoeuvrability and road-space utilisation, but it also reduces the lateral spacing between tyre contact patches and therefore reduces passive resistance to rollover.

During cornering, lateral acceleration generates an overturning moment.

Rather than relying entirely on track width to resist this moment, a narrow-track vehicle can lean into a corner similarly to a motorcycle.

This introduces another controlled degree of freedom: **vehicle roll**.

---

## Nonlinear Vehicle Modelling

For Project Agilit-E, I developed a **four-degree-of-freedom nonlinear state-space model** coupling:

- yaw dynamics,
- roll dynamics,
- vertical motion,
- lateral tyre behaviour.

A general nonlinear state-space system may be represented as

$$
\dot{\mathbf{x}}
=
f(\mathbf{x},\mathbf{u}),
$$

where:

- $\mathbf{x}$ represents the dynamic state,
- $\mathbf{u}$ represents the control input,
- $f$ represents the nonlinear vehicle dynamics.

The model also incorporates a three-tyre force representation and the kinematic constraints associated with the reverse-trike architecture.

A nonlinear representation becomes particularly important at large tilt angles and aggressive manoeuvres, where small-angle linearisation becomes increasingly inaccurate.

---

# Vehicle Tilt Control

For an ideal steady turn, the equilibrium lean angle can be understood from the balance between gravity and lateral acceleration:

$$
\tan \phi
=
\frac{a_y}{g},
$$

where:

- $\phi$ is the lean angle,
- $a_y$ is lateral acceleration,
- $g$ is gravitational acceleration.

A real vehicle must additionally handle:

- transient steering,
- varying speed,
- actuator dynamics,
- torque saturation,
- state-estimation errors,
- disturbances,
- modelling uncertainty.

I developed a **Steer Direct Tilt Control architecture** combining:

- Nonlinear Model Predictive Control,
- cascaded PID feedback.

---

## Model Predictive Control

Model Predictive Control repeatedly predicts future system behaviour over a finite horizon and chooses control actions by solving an optimisation problem.

A representative objective is

$$
\min_{\mathbf{u}_{0:N-1}}
\sum_{k=0}^{N-1}
\left[
(\mathbf{x}_k-\mathbf{x}_{\mathrm{ref}})^T
Q
(\mathbf{x}_k-\mathbf{x}_{\mathrm{ref}})
+
\mathbf{u}_k^T R \mathbf{u}_k
\right].
$$

The optimisation is subject to:

- system dynamics,
- actuator limits,
- state constraints,
- physical operating limits.

Only the first computed control action is applied.

The optimisation is then solved again using the latest state estimate.

This receding-horizon structure allows future behaviour and actuator constraints to enter the control decision explicitly.

---

# Processor-in-the-Loop Validation

Testing aggressive control behaviour directly on a vehicle introduces unnecessary risk.

I therefore developed a **Processor-in-the-Loop simulation environment** using MATLAB/Simulink.

The vehicle dynamics remain simulated while the actual embedded processor executes the controller.

This allows evaluation of:

- controller timing,
- numerical precision,
- communication delays,
- control logic,
- actuator demands,
- embedded implementation,

before unrestricted physical testing.

---

# State Estimation

Not every state required by a controller can be measured directly.

For roll estimation, I developed a sensor-fusion pipeline using a six-axis IMU.

Gyroscopes measure angular velocity accurately over short intervals but accumulate bias after integration.

Accelerometers provide an absolute gravity reference over long timescales but become unreliable under translational acceleration.

A complementary filter combines these behaviours:

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

- $\omega_k$ is gyroscope angular velocity,
- $\phi_{\mathrm{acc}}$ is the accelerometer-derived orientation estimate,
- $\alpha$ controls the relative weighting.

Conceptually:

> trust the gyroscope over short timescales and the accelerometer over long timescales.

---

# Distributed Embedded Architecture

The vehicle electronics use multiple ESP32 controllers rather than placing every sensing and control task on a single processor.

Communication uses **ESP-NOW** for low-latency peer-to-peer exchange between distributed nodes.

The architecture supports:

- sensing,
- state communication,
- controller execution,
- actuator commands,
- telemetry.

I also developed an MQTT-based telemetry pipeline connected to Grafana for real-time monitoring of vehicle states and controller behaviour.

---

# Mechanically Decoupled Tilting Architecture

Control alone does not solve the vehicle-stability problem.

The suspension geometry must allow the chassis to tilt while avoiding undesirable coupling with vertical suspension motion and steering.

I developed a mechanically decoupled architecture based on:

- a non-tilting suspension subframe,
- parallelogram suspension geometry,
- independent chassis tilt,
- multi-degree-of-freedom steering articulation.

The objective is to distinguish

**vertical suspension displacement caused by road irregularities**

from

**chassis roll used to balance the vehicle.**

A multi-DOF steering knuckle was developed to avoid kinematic binding during simultaneous large steering and tilt motions.

Dynamic behaviour was studied in MATLAB/Simulink and structural components were evaluated using finite-element analysis.

An **Indian patent application has been filed** for this architecture.

---

# Flight Control

## Project Tessera

Multirotor flight provides a different control problem.

A multirotor has little passive attitude stability and therefore depends continuously on feedback.

The flight controller repeatedly:

1. measures vehicle motion,
2. estimates attitude,
3. computes attitude error,
4. determines corrective moments,
5. modifies individual motor thrust.

The complete feedback loop must execute substantially faster than the dominant vehicle dynamics.

---

# Embedded Flight-Control Firmware

I developed modular flight-control firmware in **C/C++ on an ESP32-WROOM-32** using FreeRTOS.

Separate real-time tasks handled:

- sensor acquisition,
- controller execution,
- communication,
- telemetry.

Sensor acquisition operated at approximately **100 Hz**, while the cascaded attitude and rate controller operated at up to **200 Hz**.

---

# Cascaded PID Flight Control

The controller separates attitude regulation from angular-rate regulation.

For one rotational axis, the outer loop computes an attitude error

$$
e_\theta
=
\theta_{\mathrm{desired}}
-
\theta_{\mathrm{measured}}.
$$

Its output specifies a desired angular velocity.

The inner loop then computes

$$
e_\omega
=
\omega_{\mathrm{desired}}
-
\omega_{\mathrm{measured}}.
$$

A conventional PID controller has the form

$$
u(t)
=
K_P e(t)
+
K_I
\int_0^t e(\tau)\,d\tau
+
K_D
\frac{de(t)}{dt}.
$$

The three terms serve different roles:

- $K_P$ responds to present error,
- $K_I$ removes persistent steady-state error,
- $K_D$ reacts to the rate at which error changes.

I also implemented:

- anti-windup handling,
- dynamic gyro notch filtering.

---

# Experimental PID Tuning on a 3-DOF Testbed

A controller tuned entirely from simulation may perform poorly once applied to physical hardware.

Real systems introduce effects that are difficult to model precisely:

- motor response delay,
- propeller aerodynamics,
- structural flexibility,
- sensor noise,
- friction,
- centre-of-mass offsets,
- actuator saturation.

For this reason, I developed a physical **3-DOF gimbal testbed** for experimental controller tuning and validation.

The testbed permits the flight stack to rotate in roll, pitch, and yaw while preventing translational motion.

This allows unstable controller settings to be investigated without risking unrestricted flight.

---

## Ziegler–Nichols Closed-Loop Method

For an initial set of vanilla PID gains, I used the classical **Ziegler–Nichols ultimate-gain approach**.

For a selected axis, the integral and derivative terms are first removed:

$$
K_I = 0,
\qquad
K_D = 0.
$$

The controller therefore becomes purely proportional:

$$
u(t)
=
K_P e(t).
$$

The proportional gain is then increased gradually.

At low gain, a displaced vehicle returns slowly toward the desired orientation.

As $K_P$ increases, the response becomes faster but progressively more oscillatory.

Eventually a gain is reached where the system exhibits approximately **sustained oscillation**: the oscillation neither grows significantly nor decays significantly.

That proportional gain is defined as the **ultimate gain**

$$
K_u.
$$

The corresponding oscillation period is measured as the **ultimate period**

$$
T_u.
$$

---

## Classical PID Initialization

For a conventional PID controller, the classical Ziegler–Nichols rules give

$$
K_P
=
0.6K_u,
$$

$$
T_I
=
\frac{T_u}{2},
$$

and

$$
T_D
=
\frac{T_u}{8}.
$$

If the implementation uses gains $K_P$, $K_I$, and $K_D$ directly rather than integral and derivative time constants, then

$$
K_I
=
\frac{K_P}{T_I}
=
\frac{1.2K_u}{T_u},
$$

and

$$
K_D
=
K_P T_D
=
0.075K_uT_u.
$$

Therefore the classical initial tuning can be written directly as

$$
\boxed{
K_P = 0.6K_u,
\qquad
K_I = \frac{1.2K_u}{T_u},
\qquad
K_D = 0.075K_uT_u
}
$$

These values are not treated as the final controller.

They provide a physically measured **starting point** for subsequent refinement.

---

## Applying the Method to a 3-DOF Platform

A multirotor testbed is not three independent SISO systems.

Roll, pitch, and yaw are coupled through:

- rigid-body dynamics,
- motor thrust,
- frame inertia,
- centre-of-mass location.

The practical tuning procedure therefore begins approximately axis-by-axis.

For each rotational axis:

1. Begin from safe, low proportional gain.
2. Disable integral and derivative action.
3. Apply a small attitude disturbance or command.
4. Increase $K_P$ incrementally.
5. Observe the transient response.
6. Identify the gain $K_u$ producing sustained oscillation.
7. Measure the oscillation period $T_u$.
8. Compute initial Ziegler–Nichols PID gains.
9. Repeat for the other axes.
10. Re-enable simultaneous three-axis motion and validate the coupled system.

The 3-DOF testbed is particularly useful at the final stage because gains that appear satisfactory on an isolated axis may excite another rotational mode once the complete rigid body is allowed to move.

---

## Why Ziegler–Nichols Is Only an Initial Estimate

Classical Ziegler–Nichols tuning is intentionally aggressive.

Its objective is not to produce the smoothest possible response.

A typical Ziegler–Nichols-tuned system may exhibit:

- noticeable overshoot,
- oscillatory settling,
- excessive derivative sensitivity,
- aggressive actuator commands.

For a flight controller, the experimental gains therefore require additional refinement.

In practice:

- excessive overshoot suggests reducing $K_P$,
- slow removal of persistent error suggests increasing $K_I$,
- excessive oscillation can often be reduced by increasing damping through $K_D$,
- noisy derivative response may require derivative filtering,
- actuator saturation may require reducing overall gain or adding anti-windup protection.

The physical testbed therefore turns the process into

$$
\text{Ziegler--Nichols estimate}
\rightarrow
\text{experimental response}
\rightarrow
\text{manual refinement}
\rightarrow
\text{coupled validation}.
$$

---

## Why Use a 3-DOF Testbed?

A one-axis rig is useful for identifying basic controller behaviour.

A three-axis rig additionally exposes:

- cross-axis coupling,
- inertial asymmetry,
- centre-of-mass errors,
- motor-mixing interactions,
- sensor-axis alignment errors.

It therefore bridges the gap between an idealised single-axis experiment and unrestricted flight.

This was particularly useful for validating the controller before transitioning from constrained laboratory testing to a complete multirotor platform.

---

# Flight-Control Hardware

I also designed and routed a **four-layer flight-stack PCB** containing:

- IMU,
- magnetometer,
- ESP32 controller,
- I²C interfaces,
- SPI interfaces,
- ESC connections,
- power distribution.

Flight-control electronics require particular attention to:

- grounding,
- signal integrity,
- power distribution,
- electrical noise,
- high-current switching.

Low-level inertial measurements must coexist with rapidly switching motor electronics without allowing noise to dominate the state estimate.

---

# Physical Test Infrastructure

I developed both:

- 1-DOF test rigs,
- 3-DOF gimbal rigs,

for:

- controller tuning,
- system identification,
- thrust characterisation,
- isolated-axis validation,
- coupled attitude-control testing.

Constrained testbeds make it possible to intentionally explore unstable controller configurations while substantially reducing the consequences of failure.

---

# Why I Find Control Interesting

Control lies at an unusual intersection of several disciplines.

A successful controller may require understanding:

- differential equations,
- optimisation,
- numerical methods,
- sensing,
- state estimation,
- embedded computation,
- electronics,
- mechanical design.

The most interesting systems are usually those where none of these can be treated independently.

---

## Related Writing

A longer note on the experimental tuning procedure, oscillation measurements, final gain refinement, and limitations of classical Ziegler–Nichols tuning will be available in the blog.

[Home](./) · [Fluids](./fluid-dynamics) · [Publications](./publications) · [Notes](./blog/)
