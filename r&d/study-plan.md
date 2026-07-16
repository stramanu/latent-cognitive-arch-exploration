# Study plan: from reading to a first toy experiment

Purpose: a structured path to the background needed before designing an LCA toy experiment, in the spirit of a minimal JEPA-style illustration — one small, controllable task where the core claim either shows up in the numbers or does not.

The rule for this phase: **read to build, not to admire.** For each source, the goal is to extract the one mechanism LCA needs, and to be able to run *something*. Reading without running leaves the hardest parts (non-collapse, goal-conditioning, planning cost) as words instead of experience.

Order is deliberate: **world model → latent prediction → latent reasoning.** Dreamer gives the most complete, runnable picture of "cognition as latent dynamics that plan." JEPA sharpens *why* prediction happens in latent (not pixel/token) space and how to avoid collapse. Coconut connects all of this to the abstract-reasoning / concept side, which is where LCA's own contribution (CLCV→DCC) lives.

---

## 1. DreamerV3 — the runnable world model

**Read**
- Hafner, Pasukonis, Ba, Lillicrap (2025), *Mastering diverse control tasks through world models*, Nature (arXiv:2301.04104).
- The open-source implementation (danijar/dreamerv3) — clean and the fastest way to *see* the loop.

**Run**
- Train on one cheap environment. Watch the loop: encode observation → latent state → **imagine** future latent states → plan/act on the imagined rollout.

**Guiding questions**
- Where exactly is the "planning by imagination"? What is rolled forward — latent states or reconstructions?
- What is the cost of planning (how many latent rollouts per decision)? This is the direct reality-check on the paper's §8 efficiency claims.
- How is the latent kept stable and informative during training?

**Extract for LCA**
- The concrete shape of the encode → latent-dynamics → plan loop. This *is* the skeleton of LCA Stages 2–3.
- A felt sense of planning cost — so §8 stays honest.

---

## 2. JEPA / V-JEPA — prediction in latent space, without collapse

**Read**
- LeCun (2022), *A path towards autonomous machine intelligence* — the "why," and the closest published statement of the intuition this project shares.
- Meta AI (2025), *V-JEPA 2* (arXiv:2506.09985) — the current "how": masked prediction in latent space, no pixel reconstruction; and V-JEPA-2-AC for zero-shot planning via MPC.

**Run (lighter)**
- If feasible, a small JEPA-style setup, or at minimum trace how the reference code prevents representation collapse (stop-gradient / target-encoder / variance-covariance regularization).

**Guiding questions**
- Why predict in latent space instead of reconstructing the input? What does this buy?
- What *specifically* stops the latent from collapsing to a trivial solution? (This is the mechanism the paper hand-waves with "the ball settles into an attractor.")
- What does V-JEPA-2-AC's MPC planning share with, and lack compared to, LCA's goal-conditioned dynamics?

**Extract for LCA**
- The non-collapse toolkit — the missing "how" behind §5.3/§5.4.
- Clarity on what LCA adds *beyond* JEPA (goal-conditioning, memory, DCC-level structure), so §9 is a real distinction and not a rebrand.

---

## 3. Coconut & latent reasoning — the concept/abstract side

**Read**
- Hao et al. (2024), *Training LLMs to Reason in a Continuous Latent Space* (Coconut, arXiv:2412.06769).
- Geiping et al. (2025), *Recurrent-depth latent reasoning* (arXiv:2502.05171).
- Zhu et al. (2025), *A Survey on Latent Reasoning* (arXiv:2507.06203) — for the map of the subfield.

**Run (optional/later)**
- Reproduce the smallest Coconut-style demo: feed the last hidden state back as the next input embedding instead of decoding a token.

**Guiding questions**
- What is the minimum needed to make reasoning happen in latent space and get a usable answer out?
- Coconut still sits on an autoregressive backbone with no persistent world model — where exactly is that limit, and is it the gap §2.2/§2.4 claims?
- How does a "continuous thought" relate to a CLCV? To a DCC?

**Extract for LCA**
- The concrete link between latent-reasoning-in-LLMs and the CLCV→DCC framing — the part of LCA that is genuinely its own.

---

## 4. Converging to the experiment

After the three, the minimal experiment in `r&d/evaluation-framework.md` §6 should feel almost pre-designed:

- **From Dreamer:** the encode → latent-dynamics → plan loop, and honest planning cost.
- **From JEPA:** predict in latent (not reconstruction), and how to avoid collapse.
- **From Coconut:** how far latent-only processing can carry a task, and where it stops.

The first build is then: a tiny controllable environment, CLCVs, a goal-conditioned latent forward model, planning by latent rollout **with no language decoding**, measured against a reactive baseline and a plain world model — with goal-ablation and decoder-removal as the two tests that can falsify the thesis (evaluation-framework §2.3, §3.4).

---

## 5. Working note

Depth over breadth. Three sources understood well enough to *reimplement a piece of each* is worth more than twenty skimmed. The point of this phase is to convert the paper's metaphors ("the ball rolls to an attractor," "goals are vector fields") into mechanisms you have actually seen work — and, where they don't, to find that out now rather than after committing to an architecture.
