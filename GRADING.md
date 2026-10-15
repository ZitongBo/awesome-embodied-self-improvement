# Grading Methodology: L1–L4 for Embodied Self-Improvement

This document defines the grading criterion used by [`README.md`](./README.md): the L1–L4 levels, the single decision question, the decision procedure, a comparison with the improvement-target view, and full-text mechanism cards for selected works. The curated list itself (works organized by level and by improvement target) lives in the README.

**Scope.** Only embodied intelligence / robotics / physical AI, where each work exhibits post-deployment self-improvement. Pure software LLM agents appear only as explicit "software-domain references."

**Verification marks.** ✅ verified against a primary source (arXiv / conference), full text read where noted; ⚠️ could not be verified (kept as-is, not fabricated).

---

## 0. Summary

**Primary grading axis:** which layer of the system the self-improvement lands in. A single, decidable, gap-free question separates the levels:

| Level | Criterion | In one line |
|:--:|---|---|
| **L1** | Improvement resets to zero | Only the current episode's prompt/plan/constraints change; a scene reset returns to the start |
| **L2** | Persistent, but the executable action set is unchanged | Optimizes **how** existing capabilities are used: memory, text rules, routing, monitoring-only critics, re-ordering existing primitives, parameters |
| **L3** | Persistent, and adds a previously infeasible executable action/skill | Expands **what** the system can do: new grasp synthesis, placement, motion primitive, computation-graph node, symbolic predicate |
| **L4** | Improves the mechanism that produces improvements itself | Edits its own diagnosis / validation / promotion logic |

**The L2/L3 boundary:**

> After this self-improvement, does the system's set of executable actions/skills gain one action it could not perform before?
> If yes → **L3**; if no (only better scheduling/retrieval/ordering of existing actions) → **L2**.
> This does not depend on whether it is called a critic or a recovery, whether the artifact is text or code, or who performs the diagnosis — those are **secondary tags**.

**Two misclassifications this criterion blocks:**
1. "Added a critic" ≠ L3 — a monitoring-only critic executes no action; it is L2 in nature.
2. "Changes code" ≠ L3 — editing an existing skill's thresholds/ordering is L2; writing a new executable skill (even in a declarative DSL) is L3.

**Secondary tags (not used for grading):** validation strictness (commit-on-write / in-episode / held-out generalization gate); whether base-model weights are touched.

**State of the field:** the frontier concentrates at **L3**. **L4 is no longer entirely empty** — PhysEvo touches the lower bound in its weakest form (a meta-agent improving and reusing its own diagnostic tools) — but a complete physical-AI L4 that recursively improves the selection logic itself remains open.

---

## 1. Why "executable-action-set expansion" separates L2 from L3

A deployed embodied system can be seen as an outer system (planning / routing / critics / recovery / memory / skill library) wrapping a base policy (a VLA / controller, usually frozen). Self-improvement can land in any layer. The L2/L3 decision uses one binary question:

```
          After this self-improvement, does the system's executable
          action/skill set gain one action it could not perform before?
                    │                                 │
                    no                               yes
                    │                                 │
   ┌────────────────▼────────────────┐  ┌─────────────▼──────────────────┐
   │ L2: optimizes HOW existing       │  │ L3: expands WHICH capabilities │
   │ capabilities are used            │  │ exist                          │
   │ memory / text rules / routing /  │  │ new grasp synth / placement /  │
   │ monitoring critic / re-ordering  │  │ motion primitive / graph node /│
   │ existing primitives / parameters │  │ symbolic predicate             │
   └──────────────────────────────────┘  └────────────────────────────────┘
```

Why this test rather than "content vs code", "who is autonomous", or "is there a gate" (each of which produces grey zones):
- **Essential:** it directly answers "can the system now do something it previously could not" — the heart of "self-improvement."
- **Decidable, gap-free:** check whether a new callable executable unit was added to the system. Yes/no.
- **Form-agnostic:** a new skill written in a declarative DSL still counts as L3; a pile of code that only tweaks thresholds is still L2.
- **Blocks "pseudo-L3":** systems that only add monitoring critics, only change routing, or only re-order existing primitives stay at L2, even when self-described as a "self-evolving harness."

**Grading principles:**
1. **Mechanism over self-description:** grade by the described mechanism; "self-evolving / RSI" labels are only a hint.
2. **Split mixed systems:** many systems contain both L2 scheduling optimization and L3 new-skill addition; they are graded L3 if any genuine new executable unit appears, with the L2 part tagged separately (see `PAPERS.md`).
3. **A strong corroborating sign:** if the new unit transfers **zero-shot to new tasks**, it is almost certainly a new action/skill → L3.
4. **Unverifiable works** are marked ⚠️ and not force-fit.

---

## 2. The four levels

### L1 — In-episode feedback recovery (resets to zero)
Uses vision / tool errors / execution feedback to change the current prompt/plan/constraints and retry; capability change lasts only within the episode, and a scene reset returns to the start. Closed-loop correction, not retained evolution. *Examples: Inner Monologue, CAPE, DoReMi, COME-robot, REFLECT, CycleVLA, AgentChord.*

### L2 — Retained experience (persistent, executable action set unchanged)
Improvement persists across episodes but adds no previously infeasible executable action — it changes memory content, text rules, routing, monitoring-only critics, re-ordering of existing primitives, or parameters/weights. Two sub-kinds:
- **content-type** (memory / text skill / declarative policy): Harness VLA, EmbodiSkill, ABot-AgentOS, ME-Brain, SafeMem, BATON;
- **weight-type** (changes policy/world-model weights but adds no nameable new executable action): Self-Improving EFM, RECAP, RoboCat, VLAW, MEDAL++, LiReN. These are tagged `weights`, but remain L2 because no new executable unit appears.

> Boundary note: **ABot-AgentOS** is the most L3-like L2 — it has autonomous diagnosis and held-out gated promotion (strong secondary tags). But by the single criterion it changes a content pipeline and adds no executable action, so it is **L2**. This shows "has a gate" and "who diagnoses" are correctly demoted to secondary tags.

### L3 — Agent-driven capability expansion (adds a new executable action)
The self-improvement adds at least one previously infeasible executable unit (a new skill / grasp synthesis / placement / motion primitive / computation-graph node / symbolic predicate), usually with the base policy frozen. The real frontier for physical AI. *Examples: ASPIRE, Zetta, SHAPER, RoboHarness, GaP, RoboFoundry, RATs, RoboSkill, CaP-X, HarnessPAI, AdaHVLA, ETA, LRLL, Voyager.*

> Clarification on critics/recovery: these systems are L3 **not because they "added a critic/recovery"** — a monitoring-only critic and a recovery that merely re-orders existing primitives are L2 in nature. They are L3 because they synthesize nameable, previously infeasible new executable skills (GraspGen re-grasp, CAP placement, Multi-Angle Approach, PDDLLM predicates, new computation graphs, `pick_and_place_sim_object`, new skill-library entries). Internally L2+L3 mixed; `PAPERS.md` splits the two parts.

### L4 — RSI (improving the improvement mechanism itself)
The system improves the diagnosis / validation / promotion mechanism that produces its improvements. **PhysEvo** is the first physical-AI work to touch the lower bound: its meta-agent improves and reuses its own diagnostic tools ("inherits a way to improve, not only a way to act"). It remains the weakest instance because the Revise→Test→Select meta-loop skeleton is fixed — it edits diagnostic tools, not the selection logic. Nascent works (ENPIRE, AgenticRobotics, RegenHarness, EmbodiedRSI, RPG) are enhanced L3: they autonomously expand the system but do not recursively improve the improvement mechanism. In the software domain, the Darwin Gödel Machine is a full empirical L4 instance, and Hyperagents has an editable meta-agent — but neither is physical-AI control.

---

## 3. Applying the criterion to a new work (procedure)

1. **Persistence:** does the improvement survive an episode reset? No → **L1**.
2. **Executable action set:** does the improvement add one previously infeasible action/skill? Monitoring critic / routing rule / text memory / re-ordering existing primitives = no → **L2**; synthesized new skill / grasp / placement / motion primitive / graph node / symbolic predicate = yes → **L3** (split out any L2 scheduling part).
3. **Mechanism layer:** does it change the diagnosis / validation / promotion mechanism itself? Yes → **L4** (physical AI currently only PhysEvo, weakest form).
4. **Record secondary tags** (not used for grading): validation strictness; whether base-model weights are touched.
5. **Evidence rule:** mechanism over self-description; zero-shot transfer of a new unit to new tasks is strong evidence of a new action/skill (L3).

```
Q1 Does the improvement survive a reset? ── no → L1
                                          │ yes
Q2 Does the executable action/skill set gain a previously infeasible action?
   (monitoring critic / routing / text rule / re-ordering = no)
                                          ├ no → L2
                                          │ yes → L3 (split out any L2 part)
Q3 Does it change the diagnosis/validation/promotion mechanism itself? ── yes → L4
```

---

## 4. Comparison with the improvement-target view

[`cocacola-lab/awesome-embodied-rsi`](https://github.com/cocacola-lab/awesome-embodied-rsi) grades by L0–L4 and organizes by improvement target (Model&Policy / Memory / Skills / Harness / Embodiment / Lifelong / Safety). Its L2 ("Self-Improving") is the binary threshold of "does it make persistent self-improvement at all."

This list's axis cuts one level deeper: among persistent self-improvers, it asks whether the executable action set expands (L2 if not, L3 if so), and reserves L4 for recursively improving the mechanism itself.

- **Most common grading difference — weight-type self-improvement.** Weight-type self-improvement (Self-Improving EFM, RECAP, RoboCat, SEES, VLAW) and new-skill-type self-improvement (ASPIRE, RATs, RoboSkill, LRLL) are often placed together at the "Self-Improving" level by the target-based list. Here, the former stays L2 (no new executable unit; tagged `weights`) and the latter rises to L3 (a new executable unit).
- **A stricter L4 bar.** Works that the target-based list groups as recursive are split here into "expands the system (L3)" versus "changes the improvement mechanism itself (L4)." On this bar, ASPIRE is L3; ENPIRE/AgenticRobotics are L3→L4 nascent; Hyperagents (editable meta-agent) is closest to L4 but simulated; PhysEvo touches the physical L4 lower bound.
- **Agreement.** Both treat benchmarks and surveys separately, prefer mechanism evidence and reproducibility, and conclude there is no mature open-ended physical-AI RSI (L4) yet.

The two are complementary: the target-based list is broad and frequently updated; this list's criterion is sharper and splits more finely.

---

## 5. Full-text mechanism cards (selected works)

Each card: input / what evolves / new executable unit / why the grade / secondary tags.

### Harness VLA · 2607.08448 · L2
Frozen VLA + a fixed library of six analytic primitives (never expanded at deployment); Task-Specific Memory stores symbolized successful primitive sequences, Global Memory stores success rules / failure models. The executable action set is constant → L2.

### EmbodiSkill · 2605.10332 · L2
Frozen executor; Skill-Aware Reflection self-classifies each trajectory into four types and makes targeted edits to the **text** procedural skill (body/appendix). No new executable skill synthesized → L2.

### ABot-AgentOS · 2607.10350 · L2 (boundary case)
A failure-driven loop turns a diagnosed memory failure into a **declarative JSON-DSL** evo-asset, promoted via split-wise held-out gating. The paper states it does **not execute generated code**; it only changes the content pipeline → L2. Demonstrates that "gate" and "who diagnoses" are secondary tags that cannot lift L2 to L3.

### ASPIRE · 2607.00272 · L3
A coordinator-actor system diagnoses from per-primitive multimodal traces → synthesizes code repairs → distills **new reusable skills** into a library (e.g., Multi-Angle Approach); LIBERO-90 → LIBERO-Pro Long zero-shot 31% vs 4%.

### Zetta · 2608.16590 · L3 (with L2)
Harness H = {critic, recovery, tool}, all code. A monitoring-only critic is L2 in nature; but it synthesizes **GraspGen re-grasp / CAP stable placement / impedance control** ("beyond the base VLA's capabilities") → L3. Held-out two-stage protocol; LIBERO-Pro 34.5%→90.8%.

### RoboHarness · 2607.18060 · L3 (variant)
PDDLLM learns **new symbolic predicates**; Memory-Bridge synthesizes **handoff actions** → L3. SIMPACT additionally tunes low-level grasp poses → secondary tag "partial weights."

### RoboFoundry · 2609.32862 · L3 (with L2)
System-as-Policy; the hierarchical skill surface adds atomic skills/compositions (`pick_and_place_sim_object`) → L3; the context surface's SAVE/RETRIEVE/UTILIZE scheduling is L2. Capability-conditioned held-out promotion.

### GaP · 2607.05369 · L3
Generates **new directed computation graphs** (perception/planning/control nodes) from a modular skill library; after self-improvement in sim, runs the graph on real robots.

### PhysEvo · 2610.08995 · L3 + first to touch the L4 lower bound (physical)
A single frozen model plays both task-agent and meta-agent roles (not editable: model weights, robot dynamics, evaluator).
- **L3 evidence:** joint-level control (12-joint absolute targets; recovers from an obstructive IK-folded posture that a TCP interface cannot); active + retrospective observation tools; reusable manipulation skills.
- **L4 crux:** the meta-agent improves and reuses its own diagnostic tools; a trajectory-review tool built in one round supports a later correction ("inherits a way to improve, not only a way to act").
- **Why still the weakest L4 instance:** the Revise→Test→Select meta-loop skeleton is fixed; the meta-agent edits diagnostic *tools*, not the *selection logic* that decides how to improve.
- **Results / tags:** frozen single model, no weight updates, no separately trained action policy. RoboDojo 42-task five-dimension average 68.14/100, 62% SR; 8 Astra-hard tasks 55% vs 1.25%; AgileX PiPER real robot 90.60/100, 84% SR across 25 trials.
