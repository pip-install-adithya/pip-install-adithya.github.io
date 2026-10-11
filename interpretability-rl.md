---
layout: default
title: Mechanistic Interpretability & Reinforcement Learning
---

[Home](./) · [Scientific ML](./scientific-ml) · [Fluids](./fluid-dynamics) · [AI Systems](./ai-systems) · [Control](./controls-robotics)

# Mechanistic Interpretability & Reinforcement Learning

Modern neural networks are usually trained by optimising an external objective.

We can measure whether the model produces the correct answer.

That does not tell us **how the model produced it**.

Mechanistic interpretability attempts to move from statements such as

> this activation correlates with this behaviour

toward stronger questions such as

> this computational pathway is causally necessary for this behaviour.

---

# Representation Is Not Computation

Suppose a probe can recover some quantity $z$ from a hidden representation $\mathbf{h}$:

$$
z
\approx
g(\mathbf{h}).
$$

This demonstrates that information about $z$ exists in the representation.

It does not necessarily prove that the model actually **uses** that information when computing its output.

This motivates causal intervention.

Instead of asking only

$$
\text{What information exists here?}
$$

we can ask

$$
\text{What changes if this information is replaced or removed?}
$$

---

# Activation Patching

Consider:

- a clean input that produces the desired behaviour,
- a corrupted input for which that behaviour fails.

Let

$$
a_{\mathrm{clean}}^{(l)}
$$

represent an activation from layer $l$ in the clean run and

$$
a_{\mathrm{corrupt}}^{(l)}
$$

the corresponding activation from the corrupted run.

Activation patching replaces

$$
a_{\mathrm{corrupt}}^{(l)}
\leftarrow
a_{\mathrm{clean}}^{(l)}
$$

and evaluates whether the behaviour is restored.

If restoration occurs, that activation contains information causally relevant to the behavioural difference.

Repeated systematically, this can localise important:

- layers,
- tokens,
- attention heads,
- MLPs,
- residual-stream components.

---

# Path-Level Analysis

Neural networks contain many overlapping computational pathways.

Information represented at one location may travel through several downstream components before affecting the final output.

Methods including:

- path patching,
- Edge Attribution Patching,
- Direct Logit Attribution,

attempt to identify which components and connections contribute to the final behaviour.

---

# Direct Logit Attribution

The final logits can often be written schematically as

$$
\mathbf{z}
=
W_U\mathbf{r},
$$

where:

- $\mathbf{r}$ is the final residual-stream representation,
- $W_U$ is the unembedding matrix.

If the residual stream is decomposed as

$$
\mathbf{r}
=
\sum_i \mathbf{r}_i,
$$

then linearity gives

$$
\mathbf{z}
=
\sum_i W_U\mathbf{r}_i.
$$

This makes it possible to estimate how strongly individual residual components align with a particular output direction.

It is useful, but it should not automatically be interpreted as proving that each component performs an independent computation.

---

# Representation Geometry

Another perspective is to examine the geometry of hidden states.

Methods such as:

- PCA,
- CKA,
- representation similarity,
- residual-stream norm analysis,

allow us to compare internal representations across:

- layers,
- prompts,
- models,
- training checkpoints,
- reasoning stages.

These methods become considerably more informative when combined with causal interventions.

---

# My Interpretability Work

I have developed an interpretability framework in PyTorch and TransformerLens for sub-4B models including:

- Phi-3-Mini,
- Llama-3.2-3B.

The framework includes:

- activation patching,
- path patching,
- Edge Attribution Patching,
- Direct Logit Attribution,
- CKA,
- PCA trajectory analysis,
- counterfactual prompt interventions.

A central focus has been mathematical reasoning failures.

An incorrect answer does not necessarily mean that a model never represented the required intermediate information.

A second possibility is that the information existed internally but failed to propagate through the later computation required to affect the output.

This distinction between **representation failure** and **routing failure** is particularly interesting.

---

# Reinforcement Learning

Interpretability becomes even more interesting when the model itself changes during optimisation.

In policy-gradient methods, a policy

$$
\pi_\theta(a|s)
$$

assigns probabilities to actions conditioned on a state.

The policy is updated according to a reward-derived objective.

---

# PPO

A simplified PPO clipped-surrogate objective is

$$
L(\theta)
=
\mathbb{E}_t
\left[
\min
\left(
r_t(\theta)A_t,
\operatorname{clip}
\left(
r_t(\theta),
1-\epsilon,
1+\epsilon
\right)
A_t
\right)
\right],
$$

where

$$
r_t(\theta)
=
\frac{
\pi_\theta(a_t|s_t)
}{
\pi_{\theta_{\mathrm{old}}}(a_t|s_t)
}.
$$

Here:

- $A_t$ is an advantage estimate,
- $r_t$ measures the change in policy probability,
- $\epsilon$ limits excessively large updates.

The clipping operation keeps the policy from moving too far in one optimisation step.

---

# Group-Relative Optimisation

GRPO-style methods estimate relative advantage using a group of generated responses rather than requiring a conventional learned value function.

For rewards

$$
r_1,r_2,\ldots,r_G,
$$

a simple group-normalised signal has the form

$$
A_i
=
\frac{
r_i-\bar r
}{
\sigma_r+\varepsilon
}.
$$

This works only if the group contains meaningful reward variation.

If

$$
r_1=r_2=\cdots=r_G,
$$

then

$$
\sigma_r=0,
$$

and the group provides essentially no relative learning signal.

This creates an important failure mode for small models whose sampled responses may repeatedly receive identical rewards.

---

# My RL Work

I implemented a custom clipped-surrogate **GRPO/HGRPO** training framework incorporating a low-variance KL estimator.

The work focused heavily on diagnosing optimisation failure modes rather than only tracking reward.

This included studying:

- zero-variance reward collapse,
- residual-stream norm dynamics,
- CKA representation similarity,
- PCA state trajectories,
- behaviour under counterfactual prompts.

The broader question is not only:

> Did reinforcement learning improve the score?

but also:

> What changed internally when the model's behaviour changed?

---

# Questions I Find Interesting

## Reasoning

Does a model fail because:

1. it never computed the necessary information, or
2. it computed the information but failed to route or use it correctly?

## Circuits

Can complicated reasoning behaviour be decomposed into smaller interacting computational circuits?

## Reinforcement Learning

When optimisation improves behaviour, does it create a new internal computation or change the use of existing representations?

## Scale

Which mechanisms identified in small models continue to exist as models become larger?

---

# Tools

`PyTorch` · `TransformerLens` · `Hugging Face` · `Activation Patching` · `EAP` · `DLA` · `CKA` · `PPO` · `GRPO`

---

[Home](./) · [AI Systems](./ai-systems) · [Blog](./blog/)
