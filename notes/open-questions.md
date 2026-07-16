# Open Questions

Things I don't understand yet. Consolidated from what is already scattered across `paper.md` (§10), the roadmap risks, and the changelog — nothing new is invented here, it is just collected in one place so the hard parts stay visible.

Grouped roughly from most concrete to most speculative.

---

## Evaluation (the one that gates everything)
- What would count as evidence that a latent space is *genuinely cognitive* and not just well-organized statistics?
- How do you measure the quality of non-linguistic cognition **without** decoding it into language as the yardstick? (Full attempt in `r&d/evaluation-framework.md`.)
- What is the baseline any positive result must beat, for each claim, so a success is real and not self-flattering?

## Concepts, embeddings, and the CLCV → DCC gap
- Are concepts best represented as regions, trajectories, attractors, or generators in latent space?
- How much stability should a concept have across contexts — persistent enough to reuse, flexible enough to adapt?
- How can a concept-like structure be distinguished from a compressed language statistic?
- Can DCC-like structures actually emerge from coordinated CLCVs, or is that an assumption doing too much work?

## Goals, dynamics, and non-collapse
- How do you train goal-conditioned latent dynamics so the goal genuinely *reshapes* the trajectory instead of acting as inert metadata?
- What specifically stops the latent dynamics from collapsing to a trivial solution? (The paper's "ball settling into an attractor" is a metaphor, not a mechanism — see JEPA's actual anti-collapse tooling.)
- How can compositionality arise without reverting to explicit symbolic structure?

## Language as supervision without becoming the substrate
- Can latent concept formation emerge without overfitting to linguistic priors?
- How does the decoder stay a *probe* without quietly becoming the thing training optimizes for (the Stage-6 risk)?
- Does cognition actually survive when the language decoder is removed? (If not, the thesis is falsified.)

## Metacognition, introspection, and read-out
*(Sharpened in study sessions: the split between what is in the cognitive loop and what merely reads it. See `paper.md` §6.)*
- **The double dissociation as experimental design:** can we show that removing the read-out decoder changes *nothing but observability*, while ablating the latent metacognition *degrades cognition*? One removal that breaks nothing + one that breaks a lot is the strongest available evidence that the interface/substrate boundary is real. (See `r&d/evaluation-framework.md` §3.4.)
- **Faithfulness of the read-out decoder:** "seeing the thought" is not "seeing the true thought." A fluent decoder can confabulate. How do we measure whether the read-out faithfully reflects the latent metacognition, rather than producing a plausible post-hoc narrative (cf. unfaithful chain-of-thought)?
- Where exactly is the boundary between latent metacognition (in-loop, writes, non-linguistic) and inner-speech read-out (out-of-loop, read-only, removable)? Is it always cleanly separable, or do some systems blur it?

## Efficiency (claim, not fact)
- Is latent-first cognition actually cheaper, or can planning-by-imagination be *more* expensive per decision than a forward pass? (§8 now treats this as an open empirical question, not a given.)

## Safety and alignment
- How are values/constraints encoded in latent dynamics rather than as textual rules?
- What does safety look like under autonomous, goal-directed latent behavior that is not fully verbalizable?

## Meta / project
- At what point should a speculative extension become part of the main thesis rather than a side note?
- Which ideas belong in `paper.md` and which should stay here in notes?
