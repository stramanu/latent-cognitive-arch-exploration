# Changelog

This file tracks conceptual additions, revisions, clarifications, and partial shifts in the development of the Latent Cognitive Architecture (LCA) project.

It is not a changelog of code, but of **research ideas**.

---

## Entry template

Use this structure for future updates:

### YYYY-MM-DD — Title of the conceptual change

**Type:** addition | clarification | revision | tension | open question

**Status:** tentative | conservative | exploratory | strong claim

**Summary**  
Short description of the change.

**What changed**  
- ...
- ...
- ...

**What remained unchanged**  
- ...
- ...
- ...

**Reason for the change**  
Explain why this modification was introduced.

**Open questions**  
- ...
- ...
- ...

---

## 2026-07-16 — Modernization of the LLM critique, honesty pass, and first evaluation framework

**Type:** revision + addition
**Status:** conservative

**Summary**
A cleanup pass to bring the critique of language-centric AI up to the 2024–2025 state of the art, remove overclaims, and give the project its first falsifiable evaluation framework and a concrete study path toward a toy experiment.

**What changed**
- **§2 rewritten.** The old critique ("LLMs think in words") was retired as a strawman: modern transformers compute in a continuous internal space, with tokens as the interface. The limitation is now located precisely — training objective, token interface, and the coupling of reasoning depth to token count — and grounded in current work: Bachmann & Nagarajan (2024), Coconut (Hao et al., 2024), recurrent-depth latent reasoning (Geiping et al., 2025), the latent-reasoning survey (Zhu et al., 2025), DreamerV3 (Nature 2025), V-JEPA 2 (2025). The latent-reasoning line is framed as *corroboration* of the thesis; the missing unification (§2.4) is framed as where LCA is aimed.
- **§1 positioning added:** "reformist in method, revisionist in framing" — resolving the revolutionary-vs-incremental tension honestly.
- **§8 (efficiency) rewritten** from asserted claims ("energy drops dramatically," "parallelizable") to an argued position that separates what can be claimed from what cannot; efficiency is now an open empirical question.
- **§9:** an honest lineage note added — the core intuition predates exposure to JEPA; LeCun's work confirmed and sharpened it rather than seeding it.
- **§10:** evaluation flagged as the load-bearing open problem, pointing to the new framework.
- **Roadmap Stage 1** now explicitly distinguishes itself from CLIP/ImageBind (success = downstream predictive/controllable dynamics, not retrieval).
- **New `r&d/evaluation-framework.md`:** falsifiable CLCV- and DCC-level metrics, the "measure function not verbalization" principle, mandatory baselines, and a minimal toy experiment.
- **New `r&d/study-plan.md`:** Dreamer → JEPA → Coconut study path toward that experiment.
- **`notes/open-questions.md`** populated by consolidating questions already scattered across the corpus.
- **References** updated with the six current sources (arXiv/Nature identifiers).

**What remained unchanged**
- Cognition is still modeled as latent, goal-directed dynamics; language remains an interface.
- The CLCV/DCC distinction remains the methodological backbone.
- The document stays speculative and exploratory; no claim of validation.

**Reason for the change**
The critique risked attacking an AI that no longer exists, and several claims (efficiency in particular) were asserted rather than argued. The pass makes the project current, honest about its limits, and — via the evaluation framework — for the first time *falsifiable*.

**Open questions**
- Will the toy experiment's decoder-removal test actually hold, or reveal language as the hidden substrate?
- Is the CLCV → DCC emergence hypothesis measurable with the proposed metrics, or does it need new ones?
- Does goal-conditioning reshape latent dynamics, or act as inert metadata?

---

## 2026-03-06 — Conservative semantic extension to LCA

**Type:** addition  
**Status:** conservative

**Summary**  
A new conceptual extension was introduced: language may remain useful as a weak supervisory source for stabilizing deeper latent conceptual structures, without being treated as the substrate of cognition.

**What changed**  
- The framework now allows for the possibility of a **latent semantic substrate**.
- Linguistic input is no longer viewed only as output material or decoder supervision.
- Language may also provide weak semantic traces that help organize internal conceptual structure.
- Concepts are framed less as words and more as multimodal latent configurations.

**What remained unchanged**  
- Cognition is still modeled as latent state dynamics.
- Language is still secondary to cognition.
- Reasoning is still not identified with token prediction.
- The overall project remains post-language-centric.
- The core critique of autoregressive language models remains intact.

**Reason for the change**  
The earlier formulation may have been too sharp in separating cognition from language at every level. While language should not define the structure of thought, it may still contain useful semantic regularities that can help bootstrap or stabilize deeper internal representations.

This change creates a bridge between current language-trained systems and a future cognition-first architecture, without collapsing the theory back into a language-native model.

**Open questions**  
- Can latent concept formation emerge without overfitting to linguistic priors?
- How can the system distinguish grounded concepts from compressed language statistics?
- What would count as evidence that a latent conceptual space is genuinely cognitive?
- How should latent conceptual structures interact with goals, memory, and metacognitive control?

---

## 2026-03-06 — Clarification on concepts versus embeddings

**Type:** clarification  
**Status:** conservative

**Summary**  
A conceptual distinction was made between static embeddings and genuinely cognitive latent concepts.

**What changed**  
- The project now more clearly distinguishes between:
  - word embeddings
  - semantic similarity spaces
  - deeper cognitive concept structures
- A concept is not assumed to be equivalent to a token embedding.
- Conceptual organization is treated as potentially dynamic, multimodal, and context-sensitive.

**What remained unchanged**  
- The project still values latent representation learning.
- Continuous internal spaces remain central to the architecture.
- Language still functions as a secondary interface.

**Reason for the change**  
Without this clarification, the proposal risks being interpreted as a standard embedding-based extension of current LLMs rather than a more radical shift toward cognition-first architectures.

**Open questions**  
- Are concepts best represented as regions, trajectories, attractors, or generators in latent space?
- How much stability should a concept have across contexts?
- How can compositionality arise without reverting to explicit symbolic structures?

---

## 2026-03-06 — Methodological caution preserved

**Type:** clarification  
**Status:** conservative

**Summary**  
The new semantic extension was intentionally introduced in a limited way to preserve the speculative and exploratory character of the paper.

**What changed**  
- The paper now acknowledges an additional research path involving latent conceptual organization.
- This path is explicitly framed as a possible extension, not as a settled claim.

**What remained unchanged**  
- The document is still speculative and exploratory.
- The paper still does not claim formal validation.
- The central architecture remains a conceptual proposal, not a proven implementation plan.

**Reason for the change**  
The objective is to expand the framework without overstating confidence or prematurely hardening speculative intuitions into doctrine.

**Open questions**  
- At what point should these extensions become part of the main thesis rather than side hypotheses?
- Which additions deserve inclusion in the paper, and which should remain in notes only?