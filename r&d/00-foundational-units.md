# Foundational units for LCA R&D

Before defining an R&D roadmap, it is necessary to distinguish between the **initial engineering unit** and the **final cognitive unit** targeted by the project.

This distinction is essential. Without it, there is a constant risk of confusing a practical implementation artifact with the deeper cognitive structure that the architecture is ultimately trying to approximate.

---

## 1. Initial engineering unit: CLCV

**CLCV (Contextual Latent Cognitive Vector)**

A CLCV is a high-dimensional continuous vector representing a local, contextualized cognitive state. It is an engineering-level primitive designed to integrate perceptual, semantic, task-relevant, and memory-conditioned information into a computationally tractable form.

A CLCV is not assumed to be a concept in the full cognitive sense. It is a practical representational unit for training, prediction, control, and analysis.

### Desired properties of a CLCV

A useful CLCV should be:

- **continuous**: represented in a dense latent space
- **contextualized**: sensitive to the current situation and task
- **multimodal**: able to integrate information from text, perception, memory, and action
- **goal-conditioned**: modulated by active objectives and constraints
- **temporally usable**: suitable as input to latent dynamics models
- **computationally tractable**: easy to update, compare, compress, and decode

### Functional role of a CLCV

At the engineering level, a CLCV is intended to support:

- encoding of current latent state
- prediction of future latent states
- retrieval of relevant memory traces
- conditioning on goals and constraints
- intermediate decoding into language or action

### What a CLCV is not

A CLCV should **not** be confused with:

- a word embedding
- a fixed symbolic token
- a full concept in the cognitive sense
- a complete model of thought

It is better understood as a local representational primitive or operational snapshot.

---

## 2. Final cognitive unit: DCC

**DCC (Dynamic Cognitive Configuration)**

A DCC is a dynamic, multimodal, and goal-sensitive configuration in latent cognitive space. It is not a static point, but a structured pattern that can persist, reactivate, transform, and guide prediction, planning, control, and introspection.

A DCC is the intended long-term cognitive target of the architecture.

### Desired properties of a DCC

A mature DCC should be:

- **dynamic**: defined by structured evolution, not by a fixed position alone
- **multimodal**: shared across perception, memory, action, and language interfaces
- **partially stable**: persistent enough to be reusable, flexible enough to adapt
- **reactivatable**: capable of being recalled or reconstructed under relevant conditions
- **goal-sensitive**: shaped by active intentions, constraints, and value gradients
- **compositionally productive**: able to participate in the formation of more complex structures
- **functionally useful**: capable of supporting planning, simulation, and introspection

### Functional role of a DCC

At the cognitive level, a DCC is intended to:

- organize concept-like latent structures
- bind together perceptual, semantic, and action-relevant information
- mediate between memory and ongoing reasoning
- support internal simulation and long-horizon planning
- provide the substrate from which verbalizable reports may later be derived

### What a DCC is not

A DCC should **not** be reduced to:

- a single static vector
- a token-like representation
- a purely linguistic embedding
- a manually defined symbolic object

It is better understood as a structured latent organization with temporal, functional, and contextual coherence.

---

## 3. Relationship between the two

A DCC should not be reduced to a single vector. Instead, it may be approximated at the engineering level through sequences, assemblies, or coordinated transformations of CLCVs.

In this sense:

- **CLCVs are implementation primitives**
- **DCCs are emergent cognitive structures**

A single CLCV may capture only a local activation of a broader cognitive organization. By contrast, a DCC may require:

- multiple coordinated latent states
- temporal persistence across updates
- interaction with memory systems
- modulation by goals and constraints
- partial invariance across contexts and modalities

The engineering hypothesis is therefore:

> DCC-like cognitive structures may emerge from the controlled interaction of CLCVs under predictive, goal-conditioned, and memory-linked dynamics.

---

## 4. Why this distinction matters

This distinction protects the project from a major conceptual failure mode: mistaking a useful latent representation for cognition itself.

Without this separation, the project could easily collapse into a more sophisticated version of standard embedding-based AI. The purpose of the distinction is to keep open the possibility that:

- current engineering representations are only approximations
- cognitive organization may be fundamentally dynamic rather than static
- true concept-like units may be patterns of transformation, not isolated vectors

---

## 5. Early evaluation implications

The distinction between CLCV and DCC also implies different evaluation criteria.

### CLCV-level evaluation
At the engineering level, useful questions include:

- Does the representation align across modalities?
- Does it improve latent prediction?
- Does it support task-relevant control?
- Is it sensitive to context and goals?
- Can it be decoded or analyzed in a stable way?

### DCC-level evaluation
At the cognitive level, deeper questions include:

- Do stable concept-like structures emerge?
- Can they reactivate across contexts?
- Do they support compositional reasoning?
- Are they useful for planning and simulation?
- Do they remain functional when language decoding is removed?

---

## 6. Working principle for the R&D roadmap

For the purposes of this project:

- **the CLCV is the initial engineering unit**
- **the DCC is the final cognitive unit**
- the roadmap should be designed so that each experimental step improves the likelihood that DCC-like structures can emerge from systems built on CLCVs

This working principle should guide architecture design, data selection, training objectives, and evaluation methodology.