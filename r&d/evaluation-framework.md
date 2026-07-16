# Evaluation framework for LCA

This document addresses what is, at present, the single largest gap in the project: **how to measure progress toward non-linguistic cognition without smuggling language back in as the yardstick.**

The paper (`paper.md`, §10) lists "evaluation without linguistic traces" as one open problem among several. That framing understates it. Evaluation is *load-bearing*: if the quality of latent cognition can only be judged by decoding it into language and reading the text, then the central thesis is untestable, and the whole project reduces to a story. Everything else in the roadmap depends on getting this right.

This is a first attempt, not a finished protocol. It will be wrong in places. The goal is to make the claims falsifiable enough to be *worth* being wrong about.

---

## 1. Guiding principle: measure function, not verbalization

A representation earns the label "cognitive" here only to the extent that it **does cognitive work** — prediction, control, planning, reuse — measurable by its downstream effect, not by how good its decoded description sounds.

Concretely, this rules out three tempting-but-invalid signals:

- **Decoding quality as the primary metric.** "The model can describe its plan in fluent language" is *not* evidence of latent cognition; it is evidence of a good decoder. Language decoding is allowed only as a *probe* (Section 4), never as the target.
- **Retrieval / similarity scores alone.** Good nearest-neighbor structure (CLIP-style) shows the space is organized, not that it is dynamic, predictive, or goal-sensitive.
- **Anthropomorphic reading of latent statistics.** Interesting clusters or trajectories are not concepts. This is the failure mode named in `00-foundational-units.md` — mistaking a useful representation for cognition — and it is the one this framework exists to prevent.

**Operational rule:** every metric below must be computable with the language decoder switched *off*. If a metric needs the decoder to produce its number, it belongs in Section 4 (probes), not in the core evaluation.

---

## 2. CLCV-level evaluation (engineering unit)

The CLCV is the initial engineering primitive. Its metrics are concrete and near-term. Each is stated as: **protocol → metric → falsifiable prediction → null result** (what outcome would count as *against* the hypothesis).

### 2.1 Predictive sufficiency
- **Protocol.** Train a latent forward model that predicts CLCV(t+k) from CLCV(t) and action/context. Hold out trajectories.
- **Metric.** Prediction error in latent space; and, downstream, task performance of a controller that uses only the predicted latent vs. one that uses the true future.
- **Falsifiable prediction.** CLCVs trained under LCA objectives are more forward-predictable than representations trained for retrieval/classification alone.
- **Null result.** If retrieval-optimized embeddings (CLIP/ImageBind features) are just as predictable, the CLCV construction adds nothing at this stage.

### 2.2 Cross-modal alignment *by transfer*, not by matching
- **Protocol.** Learn a skill/predictor in one modality (e.g. from world-state encodings); apply it to a CLCV produced from a different modality (e.g. image) of the *same* situation.
- **Metric.** Zero-/few-shot transfer performance across modalities.
- **Falsifiable prediction.** A single shared latent supports better cross-modal transfer of *dynamics and control*, not merely of labels.
- **Null result.** Alignment that scores high on caption↔image retrieval but does not transfer a predictor or controller is a **Stage-1 failure by this framework**, even though it is a CLIP success.

### 2.3 Goal-sensitivity
- **Protocol.** Fix the initial CLCV; vary only the goal/constraint conditioning; roll the dynamics forward.
- **Metric.** Divergence of resulting latent trajectories and of resulting behavior, as a function of goal. Crucially: does goal conditioning *reshape the trajectory*, or does it act as inert metadata concatenated to the state?
- **Falsifiable prediction.** Same start + different goal ⇒ measurably different, task-appropriate trajectories.
- **Null result.** If ablating the goal channel barely changes behavior, goal-conditioning is superficial (the risk flagged in roadmap Stage 3).

### 2.4 Stability / non-collapse
- **Protocol.** Monitor representation statistics during training (rank, variance across dimensions, mutual information between input and CLCV).
- **Metric.** Effective dimensionality; absence of representation collapse (the failure JEPA-style objectives are specifically engineered to avoid).
- **Falsifiable prediction.** The latent retains high effective rank while remaining predictable.
- **Null result.** Collapse to a low-rank or constant solution ⇒ the objective is degenerate.

---

## 3. DCC-level evaluation (cognitive target)

DCCs are the long-term target: dynamic, reactivatable, compositional latent configurations. These metrics are harder, later, and more likely to be revised. The danger here is over-interpretation, so each metric is paired with a **control** that a non-cognitive system would fail.

### 3.1 Reactivation / persistence across contexts
- **Question.** Does a structure that formed in context A reactivate, recognizably, in a later, different context B?
- **Metric.** Identify candidate DCC signatures (recurring coordinated latent patterns); measure their recurrence and their invariance across contexts and modalities.
- **Control.** The signature must be *specific*: it should reactivate for the relevant situation and **not** for a matched distractor. A pattern that "reactivates" everywhere is noise, not a concept.

### 3.2 Compositionality
- **Question.** Can DCC-like structures combine to represent a situation neither was trained on?
- **Metric.** Systematic generalization test — hold out combinations of factors, measure performance on novel combinations vs. novel instances of seen combinations.
- **Control.** Beat a representation that has the parts but no compositional dynamics. If a bag-of-features baseline generalizes equally, no compositional structure has emerged.

### 3.3 Planning usefulness
- **Question.** Do latent rollouts of these structures actually improve planning?
- **Metric.** Control/task performance of a planner that imagines futures in latent space vs. a reactive (no-imagination) baseline, on tasks requiring look-ahead and backtracking.
- **Control.** DreamerV3 and V-JEPA-2-AC are the reference points: LCA must show that its *goal-conditioned, memory-linked* structure adds something over a plain world model, not just that planning-in-latent works (that is already established).

### 3.4 Interface vs substrate — a double dissociation (the decisive test)
The central claim — cognition is latent, language is interface — is most cleanly tested not by one ablation but by **two opposite ones**:

- **Remove the read-out decoder** (the language interface). *Prediction:* prediction, planning, and control are unchanged; only the ability to *observe* the internal thought is lost. *If instead performance drops,* language was doing cognitive work and was not merely an interface — the thesis is falsified for this system.
- **Ablate the latent metacognition** (the in-loop self-model that forms intermediate goals; `paper.md` §6.1). *Prediction:* cognition measurably degrades, because this is substrate. *If instead nothing changes,* the metacognition was decorative and the architecture is overspecified.

**Why the pair matters.** One component you can remove with no effect (proves it is *interface*) together with one you cannot (proves it is *substrate*) demonstrates that the interface/substrate boundary is real and correctly located — far stronger than asserting it. Each half can fail, and each failure falsifies a specific named commitment.

**Caveat — faithfulness.** Passing the first test shows the decoder is *removable*, not that it was *truthful* while present. A read-out decoder can confabulate a plausible narrative unrelated to the actual latent process (cf. unfaithful chain-of-thought in current LLMs). Faithfulness of the read-out must be evaluated separately and is not implied by removability.

---

## 4. The role of language decoding: probe, never target

Language is still useful for evaluation — but only as an *interpretability probe*, applied *after* the functional metrics, and never as the score that training optimizes.

- **Allowed:** train a *frozen-encoder* linear/light probe to decode latent states into descriptions, to inspect what a DCC "means." Use it to generate hypotheses about structure.
- **Not allowed:** letting decoding quality drive training, or reporting "it can explain itself" as evidence of cognition. The decoder-removal test (3.4) is precisely the guard against the decoder quietly becoming the substrate — the dominant risk flagged in roadmap Stage 6.

---

## 5. Baselines any positive result must beat

A result is evidence *for LCA* only if it beats the honest baseline for that claim. Without this, every metric above can be passed by a system that has nothing to do with the thesis.

| Claim | Baseline that must be beaten |
|---|---|
| Shared multimodal latent is cognitive | CLIP / ImageBind features fed to the same downstream head |
| Latent prediction is useful | DreamerV3-style world model |
| Latent planning is useful | V-JEPA-2-AC (MPC in latent space) |
| Latent reasoning beats verbal reasoning | a chain-of-thought LLM, and Coconut (latent CoT) |
| Goal-conditioning genuinely reshapes cognition | the same model with the goal channel ablated |

If LCA cannot beat the relevant baseline, the correct conclusion is not "the metric is unfair" — it is "no distinct effect has been demonstrated yet."

---

## 6. A minimal first falsifiable experiment (toy)

To connect this to something buildable (see `r&d/study-plan.md`), the smallest experiment that tests the *core* claim:

- **Environment.** A tiny controllable world (gridworld or simple continuous-control), fully observable, cheap to run.
- **Setup.** Encode observations into CLCVs; learn a latent forward model (Stage 2); condition it on a goal (Stage 3).
- **The test.** Plan by rolling the latent dynamics forward under the goal — **without ever decoding to language** — and measure task success.
- **Baselines.** (a) reactive policy, no imagination; (b) a DreamerV3-style world model without the LCA-specific goal/memory structure.
- **What would confirm the direction.** Latent planning succeeds, goal-ablation measurably hurts (2.3), and performance survives with no decoder (3.4).
- **What would falsify it here.** Latent planning matches the reactive baseline, or goal-conditioning is inert, or the whole thing only works when a language head is attached.

This is deliberately in the spirit of the smallest possible JEPA-style illustration: one visual, controllable task where the claim either shows up in the numbers or does not. A clean negative result here is worth more than another page of architecture.

---

## 7. Status

This framework is itself untested and will need revision once the first toy experiment runs. Its purpose right now is narrower but essential: to make the project's central claim the kind of thing that *can* be wrong — and to specify, in advance, what being wrong would look like.
