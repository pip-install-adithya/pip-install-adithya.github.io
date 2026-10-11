[Home](./) · [Scientific ML](./scientific-ml) · [Interpretability](./interpretability-rl) · [Fluids](./fluid-dynamics) · [Control](./controls-robotics)

# AI Systems

A useful AI system requires considerably more than a capable language model.

Once a model interacts with external software, the problem becomes one of **systems engineering**.

A reliable architecture may need to handle:

- structured outputs,
- tool execution,
- retrieval,
- validation,
- asynchronous computation,
- state,
- caching,
- inference serving,
- error recovery.

I have worked mainly on AI systems for **engineering workflows** and **large document collections**.

---

# AI for Engineering

Engineering software typically expects exact structures:

- geometry,
- numerical parameters,
- meshes,
- boundary conditions,
- solver inputs.

Language models operate in a fundamentally different regime: they produce probabilistic sequences of tokens.

Connecting the two safely therefore requires an intermediate layer that translates uncertain natural-language intent into deterministic machine operations.

---

## DaVinci — Enginuity Labs

During my AI Software Engineering internship at Enginuity Labs, I worked on **DaVinci**, an agentic pipeline for automated CAD topology inspection and engineering simulation.

The system translated natural-language engineering requests into structured computational workflows.

---

## Structured Orchestration

I developed an asynchronous multi-turn orchestration layer using Python, the OpenAI Responses API, and Pydantic.

Rather than allowing generated text to directly control simulation software, model outputs were converted into strictly typed JSON execution graphs.

Conceptually,

```text
User requirement
      ↓
LLM interpretation
      ↓
Typed execution graph
      ↓
Validated tool calls
      ↓
Deterministic engineering software
```

This separation helps make the stochastic language model an interface to deterministic computation rather than the final authority.

---

## Geometry Understanding

CAD models are commonly represented using **boundary representations**, or B-Reps.

A B-Rep describes a solid through entities such as:

- vertices,
- edges,
- loops,
- faces,
- shells.

Understanding engineering geometry therefore requires reasoning over both geometric quantities and topological relationships.

I developed a **17-tool deterministic topology engine** and integrated BRepNet-style graph representations for tasks including:

- adjacency traversal,
- face classification,
- semantic surface identification.

---

## Automated Simulation

The pipeline connected geometry processing to:

- **Gmsh** for automated tetrahedral meshing,
- **CalculiX** for finite-element analysis.

This allowed a high-level request to progress toward an actual numerical simulation rather than ending with a textual recommendation.

I also developed a real-time visualisation layer using Flutter and Python HTTP services to stream `.vtu` post-processing data.

---

# Retrieval-Augmented Generation

Language models have limited context and static internal knowledge.

Retrieval-Augmented Generation addresses this by retrieving relevant external information before or during generation.

The simplest version is

```text
query
  ↓
retrieval
  ↓
context
  ↓
language model
```

Real systems become considerably more complicated when documents are noisy, retrieval modes disagree, and context becomes large.

---

## Project Deep Recall

Project Deep Recall developed a retrieval system for the **IIT Madras Historical Archive**.

Historical documents create several problems:

- degraded scans,
- OCR errors,
- irregular layouts,
- uncommon names,
- sparse metadata,
- long documents.

The pipeline therefore required both document understanding and retrieval engineering.

---

## Document Processing

I worked on OCR denoising and layout restoration pipelines using **LayoutLMv3** for structured information extraction from degraded records.

Layout-aware modelling is useful because document meaning is carried not only by text but also by spatial arrangement.

---

## Hybrid Retrieval

The OpenSearch backend combined:

- fuzzy matching,
- BM25,
- dense approximate nearest-neighbour retrieval.

Each solves a different problem.

### BM25

Strong for exact lexical overlap.

### Dense retrieval

Strong for semantic similarity.

### Fuzzy retrieval

Useful for spelling variation and OCR errors.

Combining them is often more robust than relying on any single representation.

---

# Active Retrieval

I implemented **FLARE — Forward-Looking Active Retrieval-Augmented Generation**.

Instead of retrieving context only once before generation, the model monitors generation confidence and can request additional information when uncertainty becomes high.

The conceptual loop becomes

```text
generate
   ↓
confidence sufficient? ── yes ─→ continue
   │
   no
   ↓
retrieve additional context
   ↓
resume generation
```

This makes retrieval part of the generation process itself.

---

# Inference Infrastructure

Serving modern language models introduces another set of constraints:

- GPU memory,
- prefill latency,
- KV-cache growth,
- batching,
- quantisation.

I benchmarked locally hosted models using:

- vLLM
- SGLang
- FlashInfer
- FlexAttention
- INT8 quantisation

on dedicated CUDA systems.

I also worked on:

- semantic caching,
- cascading KV caches,
- attention sinks,
- EMA-based eviction,

for improving long-context multi-turn behaviour.

---

# What Interests Me Here

The most interesting AI-system problems are rarely about prompting.

They are about deciding:

- what the model should be responsible for,
- what deterministic software should handle,
- how outputs should be validated,
- when external information should be retrieved,
- how computation should be cached,
- and how failures should be contained.

In engineering applications, these distinctions become especially important because the final output may eventually drive numerical solvers or physical decisions.

---

# Tools

`Python` · `Pydantic` · `OpenAI API` · `BRepNet` · `OpenCASCADE` · `Gmsh` · `CalculiX` · `OpenSearch` · `vLLM` · `SGLang` · `Docker`

---

[Home](./) · [Interpretability](./interpretability-rl) · [Blog](./blog/)
