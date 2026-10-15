# PAPERS — Per-Paper Grading Table & Mechanism Cards

Grading criterion (see [`GRADING.md`](./GRADING.md)): the single primary axis for L1–L4 is **whether the self-improvement adds, to the system's executable action/skill set, one action it could not perform before**. Secondary tags (validation strictness; whether base-model weights are touched) do not affect grading. Mechanism over self-description; mixed L2+L3 systems are split; unverifiable works are marked ⚠️.

Verification: "✅ full text" = arXiv full text read; "✅ verified" = verified on arXiv/conference from abstract + listing.

Per-paper reading notes (one file per work) are in [`notes/`](./notes/README.md).

---

## Grading table

| Work | arXiv / venue | Grade | New executable unit (named / none) | Validation strictness | Weights | Verif. |
|---|---|:---:|---|---|---|:---:|
| Inner Monologue | 2207.05608 | **L1** | none | in-episode feedback | no | ✅ full |
| CAPE | 2211.09935 | **L1** | none | in-episode precondition | no | ✅ full |
| DoReMi | 2307.00329 | **L1** | none | in-episode VQA | no | ✅ verified |
| COME-robot | 2404.10220 | **L1** | none | in-episode feedback | no | ✅ verified |
| REFLECT | 2306.15724 | **L1** | none | in-episode failure summary | no | ✅ verified |
| Intrinsic Robot Rewarding | 2609.17115 | **L1** | none (reuses VLA reps for scoring; TRL4 demo) | internal scoring | no | ✅ verified |
| AgentChord | 2605.11951 | **L1** | none (pre-built task graph + preset recovery) | low-latency monitor | no | ✅ verified |
| CycleVLA | 2601.02295 | **L1** | none (subtask backtracking + MBR; inference-time) | inference-time | no | ✅ verified |
| EmbodiedSkills | 2609.01281 | **L1~L2** | none (fixed skill interface preflight/verify) | pre/post checks | no | ✅ verified |
| Harness VLA | 2607.08448 | **L2** | none (primitive library fixed, not expanded) | few-shot / in-episode | no | ✅ full |
| EmbodiSkill | 2605.10332 | **L2** | none (edits text skills) | in-episode reflection | no | ✅ full |
| ABot-AgentOS / ABot-Claw | 2607.10350 / 2604.10096 | **L2** | none (edits memory pipeline; no code execution) | **held-out gated** | no | ✅ full/verified |
| ME-Brain-1.0 | 2609.24271 | **L2** | none (hierarchical memory + skill abstraction) | episode-level | no | ✅ verified |
| SafeMem | 2609.08444 | **L2** | none (long-term semantic graph + risk prediction) | risk threshold | no | ✅ verified |
| BATON | 2608.16889 | **L2** | none (reusable subtask solutions in language memory) | invocation check | no | ✅ verified |
| VLAW | 2602.12063 | **L2** | none (policy ↔ world-model co-improvement, weight-level) | real rollout | yes | ✅ verified |
| Self-Improving EFM | 2509.15155 | **L2** | none (self-derived reward + success detection; weight-level) | self-reward | yes | ✅ verified |
| RECAP (π*0.6) | 2511.14759 | **L2** | none (advantage-conditioned, updates VLA weights) | sparse reward + corrections | yes | ✅ verified |
| RoboCat | 2306.11706 | **L2** | none (self-practice folded into next training round) | self-generated data | yes | ✅ verified |
| MEDAL++ | 2303.01488 | **L2** | none (task + reset behavior, weight-level RL) | autonomous practice | yes | ✅ verified |
| LiReN | OpenReview'24 | **L2** | none (navigation model online fine-tuning) | online RL | yes | ✅ verified |
| ASPIRE | 2607.00272 | **L3** | yes: new code-as-policy skills (e.g., Multi-Angle Approach) | held-out seeds | no | ✅ full |
| SHAPER | 2608.11350 | **L3** | yes: train-free evolution of new reusable skills | target-env rollout | no | ✅ verified |
| Zetta | 2608.16590 | **L3** (with L2) | yes: GraspGen re-grasp / CAP placement / impedance control | **held-out two-stage** | no | ✅ full |
| RoboHarness | 2607.18060 | **L3** (variant) | yes: PDDLLM new predicates / Memory-Bridge handoff actions | online evidence + regression | ⚠️ partial (SIMPACT) | ✅ full |
| GaP | 2607.05369 | **L3** | yes: new directed computation graph (perception/planning/control nodes) | sim self-improve → real | no | ✅ verified |
| RoboFoundry | 2609.32862 | **L3** (with L2) | yes: `place_held_sim_object` / `pick_and_place_sim_object` new skills | in-place + capability-conditioned held-out | no | ✅ full |
| RATs (Playful Agentic) | 2606.19419 | **L3** | yes: distills play into a persistent skill library | execution diagnosis | no | ✅ verified |
| RoboSkill | 2609.37810 | **L3** | yes: Explore-Execute-Evolve evolves the skill library | execution records | no | ✅ verified |
| CaP-X / CaP-Agent0 | 2603.22435 | **L3** (CaP-RL variant updates weights) | yes: CaP-Agent0 synthesizes new skills | execution feedback / RL | ⚠️ partial (CaP-RL) | ✅ verified |
| SEES | 2609.32698 | **L3** (weight-leaning) | yes/boundary: shared VLA adapters updated via online RL | task-specific success criteria | yes | ✅ verified |
| HarnessPAI | 2609.29166 | **L3** | yes: revises executable task program; retains repair knowledge | cross-rollout retention | no | ✅ verified |
| AdaHVLA | 2609.29204 | **L3** | yes: code-level harness revision | behavioral assessment | no | ✅ verified |
| ETA / OpenETA | 2608.03924 | **L3** | yes: Planner-Interface-World turns interactions into reusable skills | outcome verification | no | ✅ verified |
| RoboClaw | 2603.11558 | **L3** (weight-leaning) | yes/boundary: iterative policy refinement on real robots | real on-policy | yes | ✅ verified |
| LRLL | 2406.18746 | **L3** | yes: distills reusable policies/skills (no gradients) | experience distillation | no | ✅ verified |
| Voyager | 2305.16291 | **L3** | yes: ever-growing executable code skill library | self-verification | no | ✅ verified |
| ENPIRE | 2606.19980 | **L3→L4 nascent** | yes: evolves training infra + algorithm code | physical feedback loop | yes | ✅ verified |
| AgenticRobotics | 2608.07555 | **L3→L4 nascent** | yes: evidence-gated train-eval-improve transactions | evidence-gated promotion | — | ✅ verified |
| RegenHarness | 2609.27612 | **L3→L4 nascent** | yes: revises task template/routing/recovery code | evidence-gated | no | ✅ verified |
| EmbodiedRSI | 2610.10498 | **L3→L4 nascent** | yes: turns interaction into better code/skills | co-evolution | no | ✅ verified |
| RPG | 2610.02204 | **L3→L4 nascent** | yes: new symbolic skills + refine + system-prompt revision | cross-task test + merge | no | ✅ verified |
| **PhysEvo** | 2610.08995 | **L3 + first physical L4 lower bound** | yes: joint-level control / observation tools / reusable skills; **meta-agent improves & reuses its own diagnostic tools** | in-dev Revise→Test→Select + held-out layout | no | ✅ full |
| Hyperagents | 2603.19461 | **L4 (sim/software)** | yes: editable meta-agent evolves the modification mechanism; robotics evidence is simulated reward design | across-run accumulation | — | ✅ verified |
| Darwin Gödel Machine | 2505.22954 | **L4 (software, non-embodied)** | yes: self-rewrites code + improves its code-rewriting ability | coding-benchmark empirical | — | ✅ verified |

---

## Notes on the levels

- **L1 (~9 works):** closed-loop correction / inference-time self-correction; resets to zero. Note that Intrinsic Robot Rewarding, AgentChord, CycleVLA, and EmbodiedSkills look sophisticated but do not persist improvement into a new action across episodes → L1.
- **L2 (~13 works):** persistent improvement without a new executable action. Split into **content-type** (changes memory / text skills / declarative policy) and **weight-type** (changes weights but adds no nameable new executable action; tagged `weights`).
- **L3 (~17 works):** adds at least one previously infeasible executable unit (new skill / grasp synthesis / graph / predicate / harness program).
- **L3→L4 nascent (5 works):** self-described as "toward RSI" but with no evidence of recursively improving the improvement mechanism itself.
- **L4:** **PhysEvo** touches the physical lower bound (meta-agent improves/reuses its own diagnostic tools) but keeps a fixed meta-loop skeleton → weakest instance; Hyperagents is closest to full L4 but simulated; the Darwin Gödel Machine is a software-domain instance.

---

## Full-text mechanism cards

### Harness VLA · 2607.08448 → L2
Frozen VLA + six analytic primitives, with the primitive library explicitly not expanded at deployment; Task/Global Memory stores symbolized successful sequences and success rules / failure models. Executable action set constant → L2.

### EmbodiSkill · 2605.10332 → L2
Frozen executor; Skill-Aware Reflection self-classifies trajectories into four types → targeted edits to the **text** procedural skill's body/appendix; no new executable skill → L2.

### ABot-AgentOS · 2607.10350 → L2 (boundary)
A failure-driven loop turns memory failures into **declarative JSON-DSL** evo-assets, promoted via split-wise held-out gating. States it does **not execute generated code**; only changes the content pipeline → L2. Shows "gate" and "who diagnoses" are secondary tags that cannot lift L2 to L3.

### ASPIRE · 2607.00272 → L3
Coordinator-actor; diagnoses from per-primitive traces → synthesizes code repairs → distills **new reusable skills** into a library (e.g., Multi-Angle Approach); LIBERO-90 → LIBERO-Pro Long zero-shot 31% vs 4%.

### Zetta · 2608.16590 → L3 (with L2)
Harness {critic, recovery, tool}, all code. The monitoring-only critic is L2 in nature; it synthesizes **GraspGen re-grasp / CAP placement / impedance control** ("beyond the base VLA's capabilities") → L3. Held-out two-stage protocol; LIBERO-Pro 34.5%→90.8%.

### RoboHarness · 2607.18060 → L3 (variant)
PDDLLM learns **new symbolic predicates**; Memory-Bridge synthesizes **handoff actions** → L3. SIMPACT additionally tunes low-level grasp poses → secondary tag "partial weights."

### RoboFoundry · 2609.32862 → L3 (with L2)
System-as-Policy; the hierarchical skill surface adds atomic skills/compositions (`pick_and_place_sim_object`) → L3; the context surface's SAVE/RETRIEVE/UTILIZE scheduling is L2. Capability-conditioned held-out promotion.

### GaP · 2607.05369 → L3
Generates **new directed computation graphs** (perception/planning/control nodes) from a modular skill library; after self-improvement in sim, runs the graph on real robots.

### PhysEvo · 2610.08995 → L3 + first physical L4 lower bound
A single frozen model plays both task-agent and meta-agent roles (not editable: model weights, robot dynamics, evaluator).
- **L3 evidence:** joint-level control (recovers an obstructive IK-folded posture a TCP interface cannot); active + retrospective observation tools; reusable manipulation skills.
- **L4 crux:** the meta-agent improves and reuses its own diagnostic tools; a trajectory-review tool built in one round supports a later correction ("inherits a way to improve, not only a way to act").
- **Why still the weakest L4 instance:** the Revise→Test→Select meta-loop skeleton is fixed; the meta-agent edits diagnostic *tools*, not the *selection logic*.
- **Results:** frozen single model, no weight updates. RoboDojo 68.14/100, 62% SR; 8 Astra-hard tasks 55% vs 1.25%; AgileX PiPER real robot 90.60/100, 84% SR.
