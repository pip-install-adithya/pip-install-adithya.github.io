[Home](./) · [Scientific ML](./scientific-ml) · [Fluids](./fluid-dynamics) · [AI Systems](./ai-systems) · [Control](./controls-robotics)

# Mechanistic Interpretability & Reinforcement Learning

Modern neural networks are usually trained by optimising an external objective.

We can measure whether the model produces the correct output.

That does not tell us **how the model produced it**.

Mechanistic interpretability attempts to move from

> "this neuron correlates with this behaviour"

toward questions such as

> "this computational pathway is causally responsible for this behaviour."

---

# Representation Is Not Computation

Suppose a probe can decode a mathematical quantity from a model's hidden state.

That establishes that the information is present.

It does not necessarily establish that the model **uses that information**.

This distinction motivates causal interventions.

Rather than asking only

\[
\text{What is represented here?}
\]

we can ask

\[
\text{What changes if this representation is replaced or removed?}
\]

---

# Activation Patching

Suppose we run a model on:

- a clean input producing the desired behaviour,
- and a corrupted input where the behaviour fails.

At a chosen location in the network, an activation from the clean run can be inserted into the corrupted run.

If the correct behaviour returns, that activation contains information causally relevant to the difference.

Repeated systematically, this can localise important:

- layers,
- tokens,
- attention heads,
- residual-stream components.

---

# Path-Level Analysis

Networks are not simple sequences of isolated components.

Information can travel through many overlapping paths.

Methods such as:

- path patching,
- Edge Attribution Patching,
- Direct Logit Attribution,

attempt to determine which components and connections actually influence the final prediction.

This matters because a representation may exist in one location while being routed elsewhere before affecting the logits.

---

# Representation Geometry

Another useful perspective is to examine the geometry of hidden states.

Methods such as:

- PCA,
- CKA,
- representation similarity,
- residual-stream norm analysis

allow us to study how internal states move or reorganise across:

- layers,
- prompts,
- training checkpoints,
- reasoning steps.

These techniques are usually most useful when combined with causal analysis rather than treated as explanations by themselves.

---

# My Work

I have developed an interpretability framework in PyTorch and TransformerLens for sub-4B models including **Phi-3-Mini and Llama-3.2-3B**.

The framework includes:

- activation patching,
- path patching,
- Edge Attribution Patching,
- Direct Logit Attribution,
- CKA,
- PCA trajectory analysis,
- counterfactual prompt interventions.

A central theme has been investigating failures in multi-step mathematical reasoning.

Rather than assuming that an incorrect answer means the model never represented the required intermediate information, the experiments examine whether the information was present but failed to propagate through later computation.

---

# Reinforcement Learning

Interpretability becomes even more interesting when the model itself is changing.

Reinforcement-learning methods optimise a policy using reward rather than direct supervised targets.

For language models, one common starting point is PPO-style optimisation.

A simplified clipped surrogate objective is

\[
L(\theta)
=
\mathbb E
\left[
\min
\left(
r_t(\theta)A_t,
\operatorname{clip}
(r_t(\theta),1-\epsilon,1+\epsilon)A_t
\right)
\right].
\]

where

\[
r_t(\theta)
=
\frac{\pi_\theta(a_t|s_t)}
{\pi_{\theta_{\mathrm{old}}}(a_t|s_t)}.
\]

The clipping term prevents excessively large policy updates.

---

# Group-Relative Optimisation

GRPO-style approaches estimate relative advantage using groups of generated outputs rather than relying on a separately trained value model.

This can simplify training, particularly for reasoning tasks where a reward can be computed over complete responses.

However, several questions become important:

- What happens when every sampled response receives the same reward?
- How stable is the KL constraint?
- Which representations change first?
- Does improved reward correspond to a better internal reasoning mechanism?
- Can optimisation collapse useful representational diversity?

---

# My RL Work

I implemented a custom clipped-surrogate **GRPO/HGRPO** training framework incorporating a low-variance KL estimator.

The work focused heavily on analysing failure modes rather than simply producing a final reward curve.

This included studying:

- zero-variance reward collapse,
- residual-stream norm changes,
- CKA representation similarity,
- PCA state trajectories,
- behaviour under counterfactual prompts.

The broader goal is to understand not only whether reinforcement learning changes behaviour, but **what computation changes inside the network when that happens**.

---

# Questions I Find Interesting

### Reasoning

Does a model fail because:

1. it never computed the necessary information, or
2. it computed it but failed to route or use it correctly?

### Circuits

Can complex reasoning behaviours be decomposed into smaller interacting computational circuits?

### RL

When reinforcement learning improves an answer, does it create a new internal algorithm or merely alter routing between existing representations?

### Scale

Which mechanisms observed in small models survive as model size increases?

---

# Tools

`PyTorch` · `TransformerLens` · `Hugging Face` · `Activation Patching` · `EAP` · `DLA` · `CKA` · `PPO` · `GRPO`

---

[Home](./) · [AI Systems](./ai-systems) · [Blog](./blog/)
