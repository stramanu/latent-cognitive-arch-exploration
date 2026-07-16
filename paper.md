# Latent Cognitive Architecture (LCA): Toward Post-Language-Centric Artificial Intelligence

> **Disclaimer**
>
> This document is speculative and exploratory. It is not peer-reviewed, not validated, and not a formal research proposal. It represents an attempt to organize some personal intuitions about AI architectures — nothing more.
>
> The writing was heavily assisted by AI tools. Please read it as a thinking exercise, not as a claim of novelty or correctness.

---

## Abstract

Current large language models (LLMs) achieve remarkable results by framing intelligence as large-scale autoregressive next-token prediction. While effective for linguistic coherence and knowledge retrieval, this paradigm implicitly equates language with thought, leading to systems that lack persistent internal state, intrinsic goals, long-horizon planning, and energetic efficiency. Neuroscience and cognitive science suggest a different picture: human reasoning primarily unfolds in non-linguistic representational spaces, while language operates as a secondary mechanism for reflection, control, and communication.

In this paper, we propose a **Latent Cognitive Architecture (LCA)**, a post-language-centric framework in which reasoning is implemented as the continuous evolution of internal latent states under goals, constraints, and predictive pressures. Language is repositioned as an optional decoding, introspection, and regulation layer, rather than the substrate of cognition itself. We formalize the core components of LCA, connect them to contemporary theories such as predictive processing, active inference, and Joint-Embedding Predictive Architectures (JEPA), and outline a research roadmap toward scalable, goal-directed, and energy-efficient artificial intelligence. We further suggest that linguistic data may be distilled into a deeper latent semantic substrate, where concepts are represented not as words but as grounded internal structures. We argue that surpassing the limits of language-centric AI requires an architectural shift from token-based reasoning to latent cognitive dynamics.

---

## 1. Introduction

The recent success of large language models has revived an old philosophical and scientific question: *is language the medium of thought?* Current systems do not literally reason in words — their computation unfolds in a continuous internal space (Section 2) — but they are still built with the token sequence at the center: the training objective, the interface, and the reasoning trace are all organized around it. This organization has proven powerful but brittle.

Humans, by contrast, do not reason primarily in words. Planning, intuition, spatial reasoning, motor control, and even abstract problem solving rely on internal representations that are continuous, multimodal, and largely inaccessible to conscious verbalization. Language enters later, as a tool for self-monitoring, explanation, and social coordination.

This mismatch suggests that current LLMs approximate *the appearance of reasoning* rather than its underlying mechanism. The Latent Cognitive Architecture is motivated by the hypothesis that true general intelligence requires internal cognitive processes that are **prior to, and independent from, language**.

A modest extension of this hypothesis is that language may still provide useful semantic supervision, provided that its content is transformed into deeper latent conceptual structures rather than treated as the native format of cognition.

### Positioning: reformist in method, revisionist in framing

It is worth being explicit about how radical this proposal is meant to be, because the document otherwise risks sounding more revolutionary than it is. LCA is deliberately **reformist in method**: it builds on components that already work — world models (DreamerV3), latent prediction (JEPA), latent reasoning (Coconut, recurrent-depth models) — rather than proposing to discard them. What it revises is the **framing of what the substrate of cognition is**: not the token sequence with everything else attached, but a persistent, goal-conditioned latent dynamics onto which language is a read/write interface. The bet is not that current techniques are wrong, but that they are being assembled around the wrong center of gravity.

---

## 2. Limits of Language-Centric AI

> **A note on framing.** A few years ago the critique in this section would have been "LLMs think in words." That is no longer accurate, and repeating it would attack a system that no longer exists. Internally, a transformer's computation already unfolds in a continuous, high-dimensional space — the residual stream; tokens are the *interface* at the boundaries, not the medium of the internal computation. The honest critique is therefore not *that* language sits at the center, but *where* language-shaped constraints still bind: the training objective, the input/output interface, and the coupling between reasoning depth and token count. This section restates the limitations in those terms — and notes that parts of the research community are already moving in the direction this paper argues for.

### 2.1 The Token Interface as a Training and Inference Bottleneck

Autoregressive models are trained by teacher-forced next-token prediction and deployed by autoregressive generation. These two regimes are not equivalent, and their mismatch has concrete, mechanism-level failure modes. Bachmann & Nagarajan (2024) show that teacher forcing can fail to learn an accurate predictor *at all* on simple planning tasks — not merely accumulate errors at inference — and that both Transformer and Mamba architectures fail on a minimal, easy-to-state planning problem. The failure is in the objective, not in a lack of scale.

The point that matters for LCA is that the binding constraint lives at the *token boundary*. Even when the internal computation is continuous, forcing every reasoning step to be serialized into, and recovered from, a discrete token stream imposes a low-bandwidth, strictly sequential bottleneck on an otherwise parallel, high-dimensional process. Natural language, at this interface, acts as a lossy compression of the underlying state.

### 2.2 Reasoning Depth Coupled to Token Count — and the Field's Own Move Away From It

In the dominant paradigm, "thinking more" means "emitting more tokens": chain-of-thought spends test-time compute by producing longer visible traces, tying the amount of internal computation to the length of the linguistic output. A growing body of work decouples the two by letting reasoning happen in latent space directly:

- **Coconut** (Hao et al., 2024) feeds the model's last hidden state back as the next input embedding instead of decoding it to a token, so reasoning proceeds as a sequence of "continuous thoughts." The authors report that a continuous state can hold several candidate next steps at once, supporting breadth-first-style search on tasks that require backtracking.
- **Recurrent-depth latent reasoning** (Geiping et al., 2025) scales test-time compute by iterating a recurrent block to arbitrary depth, without generating intermediate tokens and without chain-of-thought supervision, explicitly targeting "reasoning not easily represented in words."
- A 2025 survey (Zhu et al., 2025) already organizes this into a recognizable subfield — activation-based recurrence, hidden-state propagation, and internalization of explicit reasoning traces.

This cuts two ways for the present paper. First, it is **corroboration**: independent groups are converging on the idea that reasoning need not be linguistic. Second, it marks the **current limit**: these methods still bolt latent reasoning onto an autoregressive language backbone, with no persistent world model, no goal-conditioned dynamics, and no long-lived internal state. They move computation off the token axis; they do not yet make cognition the substrate. That remaining gap is where LCA is aimed.

### 2.3 No Persistent State and No Planning-by-Imagination

A standard LLM carries no internal state across an interaction beyond its context window; each step re-reads the entire visible history rather than updating a compact, persistent representation of the situation. It also lacks a first-class mechanism for planning by simulating consequences.

Both capabilities already exist — but outside the language stack, in world-model research:

- **DreamerV3** (Hafner et al., 2025, *Nature*) learns a latent world model and improves behavior by "imagining" future latent states, mastering 150+ tasks with a single fixed configuration, including collecting diamonds in Minecraft from scratch without human data.
- **V-JEPA 2** (Meta AI, 2025) learns a self-supervised video world model by predicting in latent space and uses it for zero-shot robot planning via model-predictive control, without task-specific reward or data.

These systems plan in a latent space and maintain a predictive model of dynamics — but over perception and action, not over abstract or linguistic reasoning. The two families are complementary and, so far, largely disjoint.

### 2.4 The Actual Gap: An Unmet Unification

Stated precisely: latent-reasoning LLMs give us abstract reasoning off the token axis but no persistent world model; world models give us persistent, plan-capable latent dynamics but no abstract or linguistic reasoning. Neither yet offers goal-conditioned, memory-linked latent cognition that spans perception, action, and abstract reasoning under a single dynamics, with language demoted to an interface.

LCA is a bet on that unification. The remainder of this document specifies what such a system would have to contain — with the explicit caveat (Section 10) that the hardest parts, especially evaluation and non-collapsing goal-conditioned dynamics, remain open.

---

## 3. Cognitive Motivation and Theoretical Grounding

LCA draws inspiration from converging lines of research:

- **Predictive Processing**: cognition as prediction error minimization
- **Active Inference**: behavior as inference under goals
- **World Models**: latent state representations of environment dynamics
- **JEPA (LeCun)**: learning by predicting in latent space without generative decoding
- **Neuroscience**: distributed, non-symbolic representations and attractor dynamics

Together, these perspectives converge on a key idea: **intelligence is best modeled as latent state dynamics, not symbol manipulation**.

---

## 4. Core Hypothesis

> **Reasoning is the controlled evolution of internal latent states under goals and constraints. Language is a regulatory and communicative interface layered on top of this process.**

This hypothesis explicitly decouples cognition from linguistic generation and reframes language as an auxiliary mechanism rather than a computational substrate.

---

## 5. Latent Cognitive Architecture (LCA)

### 5.1 High-Level Overview

LCA consists of five tightly coupled subsystems:

1. Latent World Model
2. Goal and Value System
3. Cognitive Dynamics Engine
4. Selective Working Memory
5. Language-Based Introspection and Output Layer

---

### 5.2 Latent World Model

The system maintains a continuous internal state — a kind of "mental snapshot" that encodes what it knows about the world, the current context, and itself.

This state is not made of words or symbols. It's a high-dimensional, continuous representation — think of it as a point in a vast space where nearby points represent similar situations.

This internal state is:
- **Multimodal**: it can integrate information from different sources (text, images, sensors, memory)
- **Non-symbolic**: it doesn't rely on discrete categories or labels
- **Continuously updated**: it evolves over time as new information comes in

---

### 5.3 Cognitive Dynamics Engine

Reasoning, in this framework, is modeled as the evolution of the internal state over time.

At each step, the system updates its state based on:
- **Goals**: what it's trying to achieve
- **Constraints**: physical, logical, or ethical boundaries it must respect
- **Working memory**: what it's currently paying attention to

The system doesn't "search for an answer" in the traditional sense. Instead, it lets its internal state evolve — like a ball rolling through a landscape — until it settles into a stable configuration that represents a solution, a plan, or a decision.

This process is closer to how we "mull things over" than to how a calculator computes.

---

### 5.4 Goals, Values, and Intentionality

Goals are not textual instructions but **latent attractors** in state space. Competing goals generate vector fields that bias cognitive trajectories. Intentionality emerges from the interaction between goal gradients and prediction error minimization.

This framing allows:
- Multi-goal coexistence
- Long-horizon planning
- Intrinsic motivation without language

---

### 5.5 Working Memory and Attention

A selective working memory subsystem stabilizes relevant subspaces of $W(t)$, enabling:
- Temporal coherence
- Focused reasoning
- Re-entrant cognitive loops

Attention is implemented as dynamic gating over latent dimensions, not token selection.

---

### 5.6 Latent Semantic Substrate (Speculative Extension)

A natural extension of LCA is the possibility that semantic regularities extracted from language, perception, and interaction may converge into a shared latent conceptual space.

Under this view, words are not the primitive units of thought, but surface anchors for deeper internal structures. A concept would therefore not be identified with a token or a static embedding, but with a multimodal latent configuration that can be reactivated, transformed, and integrated into ongoing cognition.

This idea remains speculative, but it suggests a possible path for using language as supervision without making language itself the cognitive substrate.

---

## 6. Internal Language and Metacognitive Control

Humans frequently experience thought as *inner speech*, yet this speech is not the generator of thought but its monitor.

In LCA, a **private internal verbalization module** periodically decodes latent states into language-like representations. This serves:

- Self-consistency checking
- Error detection and correction
- Cognitive stabilization
- Alignment with external communication norms

Crucially, this internal language:
- Does not drive the core dynamics
- Can be disabled without collapsing cognition
- Is not fully exposed externally

---

## 7. Learning Paradigm

### 7.1 Latent Predictive Learning

The system learns not by predicting the next word, but by predicting its own future internal states.

The idea is simple: if you can accurately anticipate how your internal representation will change, you've understood something about the structure of the world.

This approach:
- Avoids the need to generate explicit outputs during training
- Focuses learning on internal coherence rather than surface-level patterns
- Aligns with architectures like JEPA, which learn by comparing latent representations rather than reconstructing raw inputs

---

### 7.2 Surprise, Free Energy, and Stability

Prediction error corresponds to cognitive surprise. The system minimizes an internal energy functional, yielding stable, efficient representations consistent with the free energy principle.

---

### 7.3 Language as Supervision, Not Substrate

When language data is available, it supervises only the **decoder**, preventing linguistic structure from distorting latent cognition.

In a stronger future version of the architecture, language could also serve as weak supervision for stabilizing latent conceptual structures, without becoming the primary medium of reasoning.

---

## 8. Efficiency, Scalability, and Hardware Alignment

Efficiency is often cited as a motivation for latent-first architectures, but the honest position is that it is a *hypothesis*, not a demonstrated property — and the naive version of the claim is false. It is worth stating carefully.

**What can be argued:**
- **Decoupling compute from output length.** In autoregressive generation, producing a longer answer (or a longer chain-of-thought) costs proportionally more compute, even when the underlying problem is simple. If reasoning is latent dynamics, the amount of internal computation can in principle track the difficulty of the problem rather than the length of the verbalized trace. Recurrent-depth latent reasoning (Geiping et al., 2025) is an existence proof that compute can be spent without emitting tokens.
- **Avoiding decoder cost in the inner loop.** Systems that predict in latent space rather than reconstructing raw outputs (JEPA-style) avoid running a generative decoder at every reasoning step.

**What must *not* be claimed:**
- **That latent cognition is inherently cheaper.** It need not be. A world model that plans by imagining trajectories (e.g. DreamerV3-style model-predictive control) can be *more* expensive per decision than a single forward pass, because it runs many latent rollouts. Iterating dynamics to convergence has its own, potentially large, cost.
- **That reasoning becomes automatically parallelizable.** Latent dynamics that are recurrent in time are sequential by construction. Parallelism is available along some axes (across latent dimensions, or across imagined futures) but is not a free consequence of leaving language behind.

The defensible summary is narrower: LCA changes *what* compute is spent on — internal state evolution rather than token serialization — and this *may* enable more favorable efficiency and hardware-alignment trade-offs (including neuromorphic and low-power substrates), but only if the latent dynamics are engineered to converge cheaply. Whether this holds is an empirical question for the roadmap, not a property that can be assumed.

---

## 9. Relationship to JEPA and Contemporary AI

LCA is **convergent but not identical** to JEPA:

- JEPA focuses on representation learning
- LCA extends this to goal-driven cognition, working memory, and metacognition

In this sense, LCA can be viewed as a **cognitive-level generalization of JEPA**.

The speculative notion of a latent semantic substrate is also compatible with this comparison: where JEPA emphasizes prediction in latent space, LCA may additionally require concept stabilization, value orientation, and internal regulation.

> **An honest note on lineage.** The core intuition here — that language is an interface onto a deeper, non-linguistic cognition — predates my exposure to JEPA. Encountering LeCun's work did not seed the idea; it gave it a rigorous vocabulary and the reassurance that the direction was serious. I mention this not to claim priority — the convergence with existing research is, if anything, the encouraging part — but simply to be transparent about where the thinking came from.

---

## 10. Open Problems and Research Directions

Key challenges include:
- Interpretability of latent reasoning
- Alignment and value encoding
- Evaluation without linguistic traces
- Safety under autonomous goal pursuit
- Grounding and stabilizing latent conceptual structures

These are architectural problems, not merely training issues.

Of these, **evaluation is the load-bearing one**. If the quality of non-linguistic cognition cannot be measured without first decoding it into language, then the central claim of this paper cannot be tested — only asserted. A first attempt to make this concrete, with falsifiable metrics at the CLCV and DCC levels and the baselines any such result must beat, is developed separately in `r&d/evaluation-framework.md`.

---

## 11. Conclusion

Language-centric AI has reached impressive but fragile heights. To progress toward robust, autonomous, and efficient intelligence, we must abandon the assumption that thought is made of words. The Latent Cognitive Architecture proposes a principled alternative: cognition as latent, goal-directed dynamics, with language as a reflective interface rather than a foundation. This shift mirrors biological intelligence and may define the next paradigm of artificial cognition.

A conservative extension of this proposal is that language remains useful, not as the substance of thought, but as a partial guide toward deeper latent semantic organization.

---

## References (Indicative)

**Foundational / cognitive**
- Friston, K. (2010). *The free-energy principle: a unified brain theory.*
- LeCun, Y. (2022). *A path towards autonomous machine intelligence.*
- Ha, D., & Schmidhuber, J. (2018). *World Models.*
- Clark, A. (2013). *Whatever next? Predictive brains, situated agents.*
- Kahneman, D. (2011). *Thinking, Fast and Slow.*

**Current landscape (2024–2025)**
- Bachmann, G., & Nagarajan, V. (2024). *The Pitfalls of Next-Token Prediction.* ICML 2024. arXiv:2403.06963.
- Hao, S., Sukhbaatar, S., Su, D., Li, X., Hu, Z., Weston, J., & Tian, Y. (2024). *Training Large Language Models to Reason in a Continuous Latent Space* (Coconut). arXiv:2412.06769 (ICLR 2025).
- Geiping, J., et al. (2025). *Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach.* arXiv:2502.05171.
- Zhu, R.-J., et al. (2025). *A Survey on Latent Reasoning.* arXiv:2507.06203.
- Hafner, D., Pasukonis, J., Ba, J., & Lillicrap, T. (2025). *Mastering diverse control tasks through world models* (DreamerV3). *Nature.* arXiv:2301.04104.
- Meta AI (2025). *V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning.* arXiv:2506.09985.