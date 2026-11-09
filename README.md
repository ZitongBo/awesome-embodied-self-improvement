<div align="center">

# Awesome Embodied Self-Improvement [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

**A curated list of embodied self-improvement for practitioners.**

**English** · [中文](./README.zh-CN.md)

> Beyond recursive self-improvement (RSI): the broader notion of **self-evolution** is included too.
> Scope is strictly **embodied intelligence / robotics / physical AI**; every entry must exhibit **post-deployment self-improvement**.

![Scope](https://img.shields.io/badge/scope-embodied%20%2F%20robot%20%2F%20physical--AI-blue?style=flat-square)
![Grading](https://img.shields.io/badge/grading-L1%E2%80%93L4%20by%20executable--action%20delta-f97316?style=flat-square)
![Verified](https://img.shields.io/badge/entries-arXiv%20verified-2ea44f?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

**51** embodied self-improvement works (L1 · 8 ｜ L1–L2 · 1 ｜ L2 · 14 ｜ L3 · 27 ｜ L4 · 1 at the lower bound)  ·  **5** benchmarks  ·  **10** surveys  ·  2 software-domain references

[Grading criterion](#grading-criterion-one-line-decision) · [Index by improvement target](#index-by-improvement-target-orthogonal-view) · [L1](#l1--in-episode-feedback-recovery-improvement-reset-to-zero) · [L2](#l2--retained-experience-persistent-but-the-executable-action-set-is-unchanged) · [L3](#l3--agent-driven-capability-expansion-a-new-previously-infeasible-executable-action) · [L4](#l4--rsi-improving-the-improvement-mechanism-itself) · [Benchmarks](#-benchmarks--datasets) · [Surveys](#-surveys) · [Body & morphology](#-body--morphology-self-evolution-related-not-graded) · [Grading methodology](./GRADING.md) · [Crosswalk vs L0–L5](./CROSSWALK.md)
- **[SURVEY.md](./SURVEY.md)** — a full mechanism-graded survey article (12 sections): history, the L1–L4 criterion, system anatomy (software mechanism ⊕ embodied substrates), verification, enabling-technology gaps, and the physical-L4/L5 conclusion, with both figures. A Chinese version is at [`SURVEY.zh-CN.md`](./SURVEY.zh-CN.md).
- **[OPEN_SOURCE.md](./OPEN_SOURCE.md)** — per-work open-source status (FULL / PARTIAL / NONE), authors-only releases, with evidence.
- **[BENCHMARKS.md](./BENCHMARKS.md)** — reported benchmark results grouped by benchmark (LIBERO / RoboCasa / single-benchmark), with a loud non-comparability warning; a reading aid, not a leaderboard. · [Real-robot know-how](./REAL_ROBOT_KNOWHOW.md) · [Per-paper table](./PAPERS.md) · [Contributing](./CONTRIBUTING.md)

</div>

|  |  |  |  |
|:--:|:--:|:--:|:--:|
| 🧭 **[Grading criterion](#grading-criterion-one-line-decision)**<br/>one-line decision | 🗂️ **[By level](#the-list)**<br/>L1 · L2 · L3 · L4 | 🎯 **[By target](#index-by-improvement-target-orthogonal-view)**<br/>which layer to change | 🔎 **[Full-text findings](#what-the-full-text-reading-revealed)**<br/>what reading 45 revealed |
| 📊 **[Per-paper table](./PAPERS.md)**<br/>grade + reasoning | 📑 **[Classification](./CLASSIFICATION.md)**<br/>grades re-derived | 📚 **[Benchmarks & surveys](#-benchmarks--datasets)** | 🤝 **[Contributing](./CONTRIBUTING.md)** |

---

## What this is

A human-reviewed, capability-graded map of embodied self-improvement. Every entry is verified against a primary source (arXiv / conference) and placed into **L1–L4** by a single, decidable criterion. The goal is to let practitioners see at a glance **how strong a system's self-improvement actually is**, rather than relying on self-described labels such as "self-evolving" or "RSI".

## Grading criterion (one-line decision)

> **After this self-improvement, does the system's set of executable actions/skills gain one action it could not perform before?** — No → **L2**; Yes → **L3**. Wiped on reset → **L1**. Improves the mechanism that *produces* improvements → **L4**.

<details>
<summary><b>Full criterion, secondary tags, and tag legend</b> (click to expand)</summary>

**Primary axis:** which layer of the system the self-improvement lands in.

| Level | Criterion | In one line |
|:--:|---|---|
| **L1** | Improvement **resets to zero** | Only the current episode's prompt / plan / constraints change; a scene reset returns to the starting point |
| **L2** | Persistent, but the **executable action set is unchanged** | Optimizes **how** existing capabilities are used: memory, text rules, routing, monitoring-only critics, re-ordering of existing primitives, parameters |
| **L3** | Persistent, and adds **a previously infeasible executable action/skill** | Expands **what** the system can do: new grasp synthesis, new placement, new motion primitive, new computation-graph node, new symbolic predicate |
| **L4** | Improves the **mechanism that produces improvements** itself | Edits its own diagnosis / validation / promotion logic |

**Secondary tags (do not affect grading):** validation strictness (commit-on-write / in-episode / held-out generalization gate), and whether the base model weights are touched.
**Principles:** mechanism over self-description; when a system mixes L2 and L3 internally, it is graded L3 if any genuine new executable unit appears, and the L2 part is tagged separately; unverifiable items are marked ⚠️.

**Tag legend:** `🤖real` real-robot experiments ｜ `🧪sim` simulation ｜ `code-as-policy` the policy is executable code/skills an LLM/VLM writes or composes (no learned VLA at the control layer) ｜ `🧊frozen` core policy model frozen ｜ `🔥weights` updates the core policy model's weights — i.e. the model that produces the action/decision (a VLA, or the LLM/VLM the agent calls, depending on the architecture; note that black-box LLM APIs can only be frozen) ｜ `📂open` code available. `🧊frozen`/`🔥weights` apply only to works with a VLA / learned policy; a pure `code-as-policy` work has no such model to freeze or update. Each entry also shows its **venue + year**.

</details>

**Current state of the field:** the frontier concentrates at **L3**. The physical **L4 lower bound is touched by exactly one work** — PhysEvo, whose meta-agent improves and *reuses its own diagnostic tools* across rounds on a real robot — but its Revise→Test→Select meta-loop skeleton stays fixed, so **a complete physical-AI L4 that recursively improves the selection logic itself does not yet exist**.

## What the full-text reading revealed

Every entry below was read against its primary source; the deeper works were read in full text. Four observations fall out of that reading — the kind a human reviewer sees but an auto-scraped list cannot state:

1. **Code is displacing weights as the medium of self-improvement.** Only a minority of works update model weights (SEES, RoboClaw, ENPIRE-with-training); most L3 systems **freeze the base VLA/VLM and evolve the surrounding code / skill / harness layer** (HarnessPAI, EmbodiedRSI, AdaHVLA, RPG, RegenHarness). The shared rationale: robot data is costly, fine-tuning narrows generalization, and code is diagnosable, roll-back-able, transferable, and free of catastrophic forgetting.
2. **The one-line criterion survived full-text scrutiny.** Reading the strongest works in full changed **no** grade versus the abstract-level call — evidence the "one new executable action?" question is operable and resistant to self-promotion. Papers fond of "self-evolving / RSI" language often reveal a plainer mechanism in full text (e.g. ETA/OpenETA self-improvement yields **zero promotions** in its own experiments; the authors state the result is about control, not performance).
3. **L3 is crowded; physical L4 is almost empty.** The frontier can reliably synthesize new skills/programs, but the loop that *produces* those skills is still hand-designed and fixed. Crossing L3→L4 on a real robot — PhysEvo only touches the lower bound — is the field's next hard problem.
4. **"Honest verification" is the hidden through-line of the best work.** The strongest systems spend real engineering on *not fooling themselves* — separating "tool returned success / pose reached / agent claims done" from "task actually done" (ETA's four promotion gates, RegenHarness's evidence-gated commit, RPG's cross-task merge gate, AdaHVLA's behavioral-attribution gate). This list mirrors that: it records not just who *claims* self-improvement, but whose mechanism is verifiable and whether it actually landed in-paper.

---

## Index by improvement target (orthogonal view)

The main list is organized by **capability level L1–L4** ("how strong"). Many practitioners instead ask "**which layer do I want to change**". The orthogonal index below groups works by **improvement target**. A work may span several targets; it is listed under its **primary** one.

The matrix below groups works by **improvement target** × **capability level** — an empty cell flags an intersection with few public physical-AI works (a potential gap).

### Level × improvement-target quick-reference matrix

Rows = improvement target, columns = capability level; cells list representative works. **An empty cell = that intersection currently has few public physical-AI works** (a potential research gap).

| Target \ Level | L1 | L2 | L3 | L4 (lower bound) |
|---|---|---|---|---|
| **Model & Policy** | — | Self-Improving EFM, RECAP, RoboCat, VLAW, MEDAL++, LiReN, Axiom-0 | SEES, RoboClaw, AdaRSI, Criticality-WM | — |
| **Memory & Knowledge** | — | ABot-AgentOS, ME-Brain, SafeMem, BATON | — | — |
| **Skills & Behaviors** | — | EmbodiSkill, Harness VLA | ASPIRE, RATs, RoboSkill, LRLL, Voyager, Skill-Space Shooting, Skill-RSI, HERO | — |
| **Harness & System** | EmbodiedSkills | — | Zetta, SHAPER, RoboHarness, GaP, RoboFoundry, HarnessPAI, AdaHVLA, CaP-X, ETA, ENPIRE, AgenticRobotics, RegenHarness, EmbodiedRSI, RPG | — |
| **Control Interface / Observation** | Inner Monologue, DoReMi, COME-robot, CAPE, REFLECT, CycleVLA, AgentChord, Intrinsic Reward | — | PhysEvo | — |
| **Diagnostic / Meta mechanism** | — | — | — | **PhysEvo (weakest)** |
| **Embodiment (morphology / hardware)** | — | — | — | — |

> Note on the rightmost column: **L4 (lower bound)** is only PhysEvo — the single work whose meta-agent improves its own diagnostic machinery (threshold just crossed). The works that self-describe as "toward RSI" (ENPIRE, AgenticRobotics, RegenHarness, EmbodiedRSI, RPG) reach *toward* the meta-level but keep the improvement protocol fixed, so they are graded **L3**, not L4.

> **Two visible gaps:** ① **Embodiment (self-modification of the body) is nearly empty across all levels** — post-deployment adaptation of real-robot morphology/sensors is still open; ② the **Diagnostic/Meta layer is touched only by PhysEvo in its weakest form** — a complete physical-AI L4 that recursively improves the selection logic itself remains open.

---

## The list

## L1 — In-episode feedback recovery (improvement reset to zero)

> Uses vision, tool errors, or execution feedback to change the current prompt/plan/constraints and retry; **after a reset it returns to the starting point, with no accumulation and no capability expansion**. This is closed-loop correction, not retained evolution.

- **Inner Monologue: Embodied Reasoning through Planning with Language Models** · [arXiv:2207.05608](https://arxiv.org/abs/2207.05608) · `CoRL 2022` · `L1` `🤖real` `code-as-policy` — feeds success detection / scene description / human interaction back into the LLM to form an "inner monologue" closed-loop replanner.
- **CAPE: Corrective Actions from Precondition Errors using LLMs** · [arXiv:2211.09935](https://arxiv.org/abs/2211.09935) · `arXiv 2022` · `L1` `🧪sim` `code-as-policy` — on a precondition error, re-prompts the LLM to extract an executable corrective action.
- **DoReMi: Grounding LM by Detecting and Recovering from Plan-Execution Misalignment** · [arXiv:2307.00329](https://arxiv.org/abs/2307.00329) · `IROS 2024` · `L1` `🤖real` `code-as-policy` — a VQA model periodically detects plan–execution misalignment and recovers immediately.
- **REFLECT: Summarizing Robot Experiences for Failure Explanation and Correction** · [arXiv:2306.15724](https://arxiv.org/abs/2306.15724) · `CoRL 2023` · `L1` `🤖real` `code-as-policy` — multimodal failure summary → LLM locates the cause → corrective plan; ships the RoboFail dataset.
- **COME-robot: Closed-Loop Open-Vocabulary Mobile Manipulation with GPT-4V** · [arXiv:2404.10220](https://arxiv.org/abs/2404.10220) · `ICRA 2025` · `L1` `🤖real` `code-as-policy` — a closed-loop GPT-4V framework for open-vocabulary mobile manipulation; iteratively updates the plan / recovers from failure, ~+35% success over prior SOTA.
- **CycleVLA: Proactive Self-Correcting VLA via Subtask Backtracking & MBR Decoding** · [arXiv:2601.02295](https://arxiv.org/abs/2601.02295) · `arXiv 2026` · `L1` `🤖real` `📂open` — predicts incipient failure at subtask boundaries, backtracks, and retries with MBR decoding (inference-time self-correction).
- **AgentChord: Proactive Failure Recovery through an Agentic Task Graph** · [arXiv:2605.11951](https://arxiv.org/abs/2605.11951) · `RSS 2026` · `L1` `🤖real` `code-as-policy` `📂open` — builds a task graph with anticipated recovery branches so low-latency monitors trigger corrections.
- **Intrinsic Robot Rewarding: Reusing VLA Representations for Autonomous Evaluation** · [arXiv:2609.17115](https://arxiv.org/abs/2609.17115) · `arXiv 2026` · `L1` `🤖real` — reuses a frozen VLA encoder for autonomous outcome scoring to reduce human labeling; not yet connected to persistent policy improvement.
- **EmbodiedSkills: A Unified Framework for Orchestrating/Training/Deploying VLA Agents** · [arXiv:2609.01281](https://arxiv.org/abs/2609.01281) · `arXiv 2026` · `L1~L2` `🧪sim` `code-as-policy` — a fixed skill interface with prerequisite preflight / outcome verification; records trajectories for optional online adaptation.

---

## L2 — Retained experience (persistent, but the executable action set is unchanged)

> The system "knows more / schedules better", but "the set of actions it can perform is unchanged". Two sub-kinds: **content-type** (changes memory / text / declarative policy) and **weight-type** (changes weights but adds no nameable new executable action).

### Content-type L2

- **Harness VLA: Steering Frozen VLAs into Reliable Manipulation Primitives via Memory-Guided Agents** · [arXiv:2607.08448](https://arxiv.org/abs/2607.08448) · `arXiv 2026` · `L2` `🧊frozen` — a frozen VLA plus a fixed primitive library (never expanded at deployment); Task/Global Memory stores successful traces, success rules, and failure models. LIBERO-Pro 82.4%.
- **EmbodiSkill: Skill-Aware Reflection for Self-Evolving Embodied Agents** · [arXiv:2605.10332](https://arxiv.org/abs/2605.10332) · `arXiv 2026` · `L2` `🧪sim` `📂open` — classifies each trajectory into four types and makes targeted edits to the **text** procedural skill's body/appendix; synthesizes no new executable skill. ALFWorld 93.28%.
- **ABot-AgentOS: A General Robotic Agent OS with Lifelong Multi-modal Memory** · [arXiv:2607.10350](https://arxiv.org/abs/2607.10350) · `arXiv 2026` · `L2` (boundary case) `🤖real` — a failure-driven loop turns diagnosed memory failures into **declarative JSON-DSL** evo-assets, promoted via split-wise held-out gating; it explicitly does **not execute generated code** and only changes the memory pipeline.
- **ABot-Claw: Persistent, Cooperative, and Self-Evolving Robotic Agents** · [arXiv:2604.10096](https://arxiv.org/abs/2604.10096) · `arXiv 2026` · `L2` `🤖real` `📂open` — capability-driven multi-robot scheduling + cross-embodiment multimodal memory + critic feedback.
- **ME-Brain-1.0: Memory, Cognition and Action for Evolving Embodied Intelligence** · [arXiv:2609.24271](https://arxiv.org/abs/2609.24271) · `arXiv 2026` · `L2` `🤖real` — experience acquisition + hierarchical memory consolidation + skill abstraction without retraining.
- **SafeMem: Safe Task Planning with Long-Term Graph Memory** · [arXiv:2609.08444](https://arxiv.org/abs/2609.08444) · `CoRL 2026` · `L2` `🤖real` — an incremental semantic-graph memory plus an LLM risk predictor that triggers conservative replanning.
- **BATON: Long-Horizon Manipulation via Agentic Subtask Exploration & Transition-aware Memory** · [arXiv:2608.16889](https://arxiv.org/abs/2608.16889) · `arXiv 2026` · `L2` `code-as-policy` `🤖real｜🧪sim` — freezes the VLA and stores reusable subtask solutions in language memory; no parameter updates.

### Weight-type L2 (changes weights, but adds no nameable new executable action)

- **Self-Improving Embodied Foundation Models** · [arXiv:2509.15155](https://arxiv.org/abs/2509.15155) · `NeurIPS 2025` · `L2` `🤖real` `🔥weights` — a two-stage recipe derives rewards (Steps-to-Go) and success detection; robot fleets practice autonomously and update policy weights.
- **π*0.6 (RECAP): a VLA That Learns From Experience** · [arXiv:2511.14759](https://arxiv.org/abs/2511.14759) · `arXiv 2025` · `L2` `🤖real` `🔥weights` — advantage-conditioned learning from real deployment experience plus corrections, updating VLA weights.
- **RoboCat: A Self-Improving Generalist Agent for Robotic Manipulation** · [arXiv:2306.11706](https://arxiv.org/abs/2306.11706) · `TMLR 2024` · `L2` `🤖real` `🔥weights` — generates self-practice trajectories folded into the next round of generalist training.
- **VLAW: Iterative Co-Improvement of VLA Policy and World Model** · [arXiv:2602.12063](https://arxiv.org/abs/2602.12063) · `arXiv 2026` · `L2` `🤖real` `🔥weights` — alternates improving the world model and the policy (both at the weight level).
- **MEDAL++: Self-Improving Robots via End-to-End Autonomous Visuomotor RL** · [arXiv:2303.01488](https://arxiv.org/abs/2303.01488) · `CoRL 2023` · `L2` `🤖real` `🔥weights` — learns task and reset behaviors to practice autonomously via weight-level RL.
- **LiReN: Lifelong Autonomous Improvement of Navigation Foundation Models in the Wild** · [OpenReview](https://openreview.net/forum?id=vBj5oC60Lk) · `CoRL 2024` · `L2` `🤖real` `🔥weights` `📂open` — a navigation foundation model fine-tunes from online experience after deployment.
- **Axiom-0: Hierarchical Self-Refinement for Vision-Language-Action Policies** · [arXiv:2610.14155](https://arxiv.org/abs/2610.14155) · `arXiv 2026` · `L2` `🤖real` `🔥weights` — intra-VLM representation refinement (IVRR) + recursive VLM-action interface refinement (VAIR) sharpen an existing policy; no new nameable executable action. RoboCasa365 62.32%.

---

## L3 — Agent-driven capability expansion (a new, previously infeasible executable action)

> The self-improvement **adds at least one previously infeasible executable unit** (new skill / grasp synthesis / placement / motion primitive / computation-graph node / symbolic predicate). The base policy is usually kept frozen. **This is the real frontier for physical AI.**

- **ASPIRE: Agentic Skills Discovery for Robotics** (NVIDIA GEAR) · [arXiv:2607.00272](https://arxiv.org/abs/2607.00272) · `arXiv 2026` · `L3` `🤖real` `📂open` — diagnoses from per-primitive traces → writes/repairs code-as-policy → distills **new reusable skills** into a library (e.g., Multi-Angle Approach); LIBERO-90 → LIBERO-Pro Long **zero-shot 31% vs 4%**.
- **Zetta: Closed-Loop Embodied Harness for Self-Evolving Physical Intelligence** · [arXiv:2608.16590](https://arxiv.org/abs/2608.16590) · `arXiv 2026` · `L3` (with L2 scheduling) `🧪sim` `🧊frozen` `📂open` — evolves code critics/recovery/tools online; synthesizes **GraspGen re-grasp / CAP stable placement / impedance control** ("beyond the base VLA's capabilities"); LIBERO-Pro 34.5%→90.8%, 11.1× speedup.
- **SHAPER: Self-Evolving Embodied Agents via Skill-Harness Evolution** · [arXiv:2608.11350](https://arxiv.org/abs/2608.11350) · `arXiv 2026` · `L3` `🧪sim` `code-as-policy` — train-free evolution of reusable skills and a context-code harness.
- **RoboHarness: Memory-Driven Orchestration of Heterogeneous Robot Policies** (Huawei Noah's Ark) · [arXiv:2607.18060](https://arxiv.org/abs/2607.18060) · `arXiv 2026` · `L3` (variant) `🤖real` `🔥partial weights` — PDDLLM learns **new symbolic predicates** + Memory-Bridge synthesizes **handoff actions**; SIMPACT additionally tunes low-level grasp poses. LIBERO-Plus 91.9%.
- **GaP: Graph-as-Policy Multi-Agent Self-Learning Harness** · [arXiv:2607.05369](https://arxiv.org/abs/2607.05369) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` `📂open` — generates **new directed computation graphs** (perception/planning/control nodes) from a modular skill library; after self-improvement in sim, runs the graph on real robots.
- **RoboFoundry: System-as-Policy Evolution for Self-Learning Embodied Agents** · [arXiv:2609.32862](https://arxiv.org/abs/2609.32862) · `arXiv 2026` · `L3` (with L2) `🤖real` `code-as-policy` — the hierarchical skill surface adds atomic skills/compositions (`pick_and_place_sim_object`); capability-conditioned held-out promotion. Improves GPT-5.5 by 27.8% on EmbodiedBench.
- **RATs: Playful Agentic Robot Learning** · [arXiv:2606.19419](https://arxiv.org/abs/2606.19419) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` `📂open` — self-directed play proposes tasks → executes/diagnoses code policies → distills a **persistent skill library** transferable to downstream real-robot tasks.
- **RoboSkill: A Skill Acquisition and Reuse Loop for Embodied Agents** · [arXiv:2609.37810](https://arxiv.org/abs/2609.37810) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` — an Explore-Execute-Evolve loop **evolves the skill library**; +12.5–25 pp first-episode success on LIBERO-10.
- **CaP-X: Benchmarking and Improving Coding Agents for Robot Manipulation** · [arXiv:2603.22435](https://arxiv.org/abs/2603.22435) · `arXiv 2026` · `L3` (CaP-RL variant updates weights) `🤖real` `code-as-policy` `📂open` — CaP-Agent0 **synthesizes new skills** from execution feedback; CaP-RL adds weight-level updates.
- **HarnessPAI: An Evolving Harness for Physical AI** · [arXiv:2609.29166](https://arxiv.org/abs/2609.29166) · `arXiv 2026` · `L3` `🧪sim` `🧊frozen` — revises an **executable task program** from execution feedback and retains failure-repair knowledge; LIBERO-PRO +61.6 pp over pi0.5.
- **AdaHVLA: Adaptive Harnesses for Long-Horizon VLA Execution** · [arXiv:2609.29204](https://arxiv.org/abs/2609.29204) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` `🧊frozen` — multiple agents perform **code-level harness revision**, keeping a hypothesis-revision-effect graph.
- **ETA / OpenETA: A New Agentic Paradigm for Embodied Tasks** · [arXiv:2608.03924](https://arxiv.org/abs/2608.03924) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` `📂open` — a Planner-Interface-World loop turns interactions into **reusable skills/experience**.
- **Skill-Space Shooting for Autonomous Robot Policy Improvement** · [arXiv:2609.38178](https://arxiv.org/abs/2609.38178) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` — explores corrective actions as **reusable short skills** and turns them into policy training signals, shared across tasks.
- **SEES: Self-Evolving Embodied System via Failure-Guided VLA Policy Adaptation** · [arXiv:2609.32698](https://arxiv.org/abs/2609.32698) · `arXiv 2026` · `L3` (weight-leaning) `🧪sim` `🔥weights` — reconstructs repeatedly failing atomic skills in simulation and updates shared VLA adapters via online RL.
- **RoboClaw: Agentic Framework for Scalable Long-Horizon Robotic Tasks** · [arXiv:2603.11558](https://arxiv.org/abs/2603.11558) · `arXiv 2026` · `L3` (weight-leaning) `🤖real` `📂open` — paired forward/inverse behaviors for self-resetting collection plus iterative policy refinement on real robots.
- **LRLL: Lifelong Robot Library Learning** · [arXiv:2406.18746](https://arxiv.org/abs/2406.18746) · `ICRA 2024` · `L3` `🤖real` `code-as-policy` — proposes tasks → stores experience → distills **reusable policies/skills** (no gradient updates; new skills generated via LLM coding).
- **Voyager: An Open-Ended Embodied Agent with LLMs** (Minecraft) · [arXiv:2305.16291](https://arxiv.org/abs/2305.16291) · `TMLR 2024` · `L3` `🧪sim` `code-as-policy` `📂open` — automatic curriculum + an ever-growing executable code skill library + iterative self-verification (foundational for embodied digital worlds).
- **AdaRSI: On-Demand Recursive Self-Improvement for Embodied Agents** · [arXiv:2610.20474](https://arxiv.org/abs/2610.20474) · `arXiv 2026` · `L3` (with on-demand weights) `🤖real` `🔥partial weights` — a coding agent first improves skills/harness, then **attributes a persistent failure to "how it is called" vs "what it can do"** and fine-tunes only the still-unreliable sub-steps; adds new executable sub-steps on RoboCasa365 (unseen composite 4.6%→13.8%) at 28% of the GPU time of full fine-tuning.
- **Compile Once, Run Cheap (Skill-RSI): Frozen, Portable Skills for Embodied Agents** · [arXiv:2610.25114](https://arxiv.org/abs/2610.25114) · `arXiv 2026` · `L3` `🧪sim` `code-as-policy` `📂open` — a strong model acts as an offline author that writes/runs/diagnoses/repairs a skill until it passes an exam on **layouts drawn only after freezing**, then the frozen skill runs as code; proposes *Skill-RSI* with an audited, tamper-evident compile protocol. Frozen skills kept 148/150 successes on new layouts with no model.
- **Practice Makes Policies (HERO): Bootstrapping Robotic Capabilities from Zero Human Demonstrations** · [arXiv:2607.26809](https://arxiv.org/abs/2607.26809) · `arXiv 2026` · `L3` `🤖real` — autonomous capability evolution from **zero human demos**: bootstraps experience, accumulates reusable behaviors, and **consolidates recurring interactions into new closed-loop visuomotor policies**, coupling data collection with execution.
- **Policy-Level RSI with a Criticality World Model** · [arXiv:2607.28251](https://arxiv.org/abs/2607.28251) · `arXiv 2026` · `L3` (weight-leaning) `🤖real｜🧪sim` `🔥weights` — execution outcomes train a criticality world model whose risk scores guide scenario collection for specialist training; across five embodied domains failure rates drop 59–67% (locomotion/manipulation) and 8–25% (VLA).

---

## L4 — RSI (improving the improvement mechanism itself)

> The system improves not only its own capabilities but **the diagnosis / validation / promotion mechanism that produces those improvements**. **Physical AI is touched only in its weakest form; there is no mature instance yet.**

- **PhysEvo: Astra Can Act, Let It** · [arXiv:2610.08995](https://arxiv.org/abs/2610.08995) · `arXiv 2026` · **`L3` + first to touch the `L4` lower bound (physical)** · `🤖real` `🧊frozen` — a single frozen model plays both task-agent and meta-agent roles. L3: joint-level control / active + retrospective observation tools / reusable skills. **L4 crux:** the meta-agent **improves and reuses its own diagnostic tools** ("inherits a way to improve, not only a way to act"). **Still the weakest instance:** the Revise→Test→Select meta-loop skeleton is fixed, so it edits diagnostic tools rather than the selection logic. RoboDojo 62% SR; real robot 84% SR.

### L3 works that reach toward the meta-level (self-described "toward RSI", mechanically still L3)

- **ENPIRE: Agentic Robot Policy Self-Improvement in the Real World** · [arXiv:2606.19980](https://arxiv.org/abs/2606.19980) · `CoRL 2026` · `L3` `🤖real` `code-as-policy` — automatic reset/verify/rollout plus evolution of training infrastructure and algorithm code across a fleet.
- **You Don't Need To Stay in The Loop (AgenticRobotics)** · [arXiv:2608.07555](https://arxiv.org/abs/2608.07555) · `arXiv 2026` · `L3` `🧪sim` `code-as-policy` — ports the coding-agent loop to robot-policy improvement: an LLM controller runs evidence-gated train-evaluate-improve transactions with auditable promotion. The author is explicit it does not pick better checkpoints than a human — it makes the loop safe to leave (false-promotion 0.001/run; 6/6 tamper classes caught).
- **RegenHarness: Robot Agent Harness with Evidence-Gated Recursive Self-Improvement** · [arXiv:2609.27612](https://arxiv.org/abs/2609.27612) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` — revises task-template/routing/recovery code; self-described as recursive but does not establish improving the improvement step.
- **EmbodiedRSI: Active Continual Robot Learning via Hypothesis-Guided Co-Evolution** · [arXiv:2610.10498](https://arxiv.org/abs/2610.10498) · `arXiv 2026` · `L3` `🤖real` `code-as-policy` `🧊frozen` — autonomously decides where to explore next and turns physical interaction into better code/skills.
- **RPG: Reconstruct, Practice, Go Real — Guided Self-Improvement** · [arXiv:2610.02204](https://arxiv.org/abs/2610.02204) · `arXiv 2026` · `L3` `🤖real` — weight-free self-improvement; develops new symbolic skills + refines + revises the system prompt; 22 tasks 28.6%→95.0%.
- **EmbodiRSI: Recursive Self-Improvement for Data-Efficient Robot Adaptation** · [arXiv:2609.38905](https://arxiv.org/abs/2609.38905) · `arXiv 2026` · `L3` `🤖real｜🧪sim` — real-to-sim-to-real: builds a deployment-specific simulation and uses execution feedback to steer **corrective-trajectory generation + adaptive data collection**; reaches 83.1% real-world success with 10 real trajectories/subtask (vs 75.0% from 200 real demos). Reaches toward the meta-level by revising its own data-acquisition loop, but the loop structure stays fixed.

### Software-domain L4 references (not physical AI, for comparison)

- **Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents** · [arXiv:2505.22954](https://arxiv.org/abs/2505.22954) · `arXiv 2025` · `L4 (software/coding)` `📂open` — rewrites its own code and improves its ability to rewrite code; SWE-bench 20%→50%.
- **Hyperagents** · [arXiv:2603.19461](https://arxiv.org/abs/2603.19461) · `arXiv 2026` · `L4 (sim/software)` `🧪sim` `📂open` — a task agent plus an **editable meta agent** so the mechanism producing future modifications can itself evolve; its robotics evidence is simulated reward design only.

---

## 🧪 Benchmarks & Datasets

### Benchmarks that audit self-improvement / self-evolution itself

These evaluate the *capability of improving*, not just task success — directly aligned with this list's criterion. Their shared insight: **a saved memory or a successful final action does not by itself prove a reusable capability was acquired; evaluation must separate genuine capability change from carried-over resources, unequal source exposure, repeated attempts, privileged state, budget, and luck.**

- **MC-EvoBench: Auditing Experience-Driven Self-Improvement in Minecraft Agents** · [arXiv:2610.13829](https://arxiv.org/abs/2610.13829) · `arXiv 2026` — a controlled Minecraft benchmark with 19 registered "evolution chains"; represents each task as a task-state graph with stage-level verifiers, matched source/target roles, a reset target world, and only a **declared agent artifact** allowed to carry over — so transfer measures acquired capability rather than smuggled resources. Its auditing stance is the benchmark form of this list's "mechanism, not self-description" rule.
- **SEAR: Self-Evolving Agentic Robotics (framework + benchmark)** · [arXiv:2610.18792](https://arxiv.org/abs/2610.18792) · `arXiv 2026` — asks two questions this list also cares about: *is the agent really learning, or just trying more often?* and *does what it learns transfer to new tasks, a new simulator, and a real robot?* Adds controls separating retained experience from repeated attempts, familiar tasks, privileged simulator state, larger budgets, and luck; 7 frontier LMs, 330 simulated + 5 physical tasks. Runs agents as code-as-policy, agent-as-policy, or auto-research (VLA fine-tuning). It also classifies prior self-evolving systems (CaP-X, ASPIRE, RATs, ENPIRE, RPG, RoboRSI, …) in one table and finds that **almost none report both a budget-matched restart control and a no-library control** — a concrete measure of the comparability gap. See [GRADING §6](./GRADING.md#6-verifying-self-improvement-is-real-not-an-illusion) for the derived verification checklist.
- **EvoNav-Bench: Benchmarking Lifelong Navigation in Evolving Environments** · [arXiv:2609.08292](https://arxiv.org/abs/2609.08292) · `arXiv 2026` — extends GOAT-Bench-style lifelong navigation to **environments that change over time** (ProcTHOR-based), exposing the failure mode where an agent fuses stale prior observations with new ones — a failure stationary benchmarks cannot reveal.
- **Continual IL grounded? A Language-Perturbed Benchmark for Robotic Task Retention** · [arXiv:2610.00542](https://arxiv.org/abs/2610.00542) · `arXiv 2026` — meaning-preserving vs meaning-changing instruction variants over LIBERO suites; **separates task competence from language grounding**, testing whether retained behavior still follows language rather than memorized scene cues.
- **Benchmarking World Models for Continual Learning on Compositional Tasks** · [arXiv:2609.22055](https://arxiv.org/abs/2609.22055) · `arXiv 2026` — a compositional continual-learning benchmark that **isolates knowledge reuse from learning-new-tasks** for world models in robot manipulation.

### General evaluation suites borrowed by the works above

- **EmbodiedMemory-Bench** · [arXiv:2609.28236](https://arxiv.org/abs/2609.28236) `📂open` — tests whether memory built from earlier observations/interactions supports later embodied actions (2,554 episodes).
- **EmbodiedGovBench** · [arXiv:2604.11174](https://arxiv.org/abs/2604.11174) — governance-oriented evaluation: capability boundaries, runtime drift, recovery, upgrade safety, human override, audit completeness.
- **RoboDojo / LIBERO-Pro / RoboCasa / EmbodiedBench / RMBench** — evaluation suites used by many works above (see each entry).

## 📚 Surveys

- **Self-Evolving AI for Humanoids: Mechanisms, Safety, and Evaluation of Post-Deployment Self-Improvement** · [arXiv:2609.13236](https://arxiv.org/abs/2609.13236) — post-deployment self-evolution over policy/perception/memory/workflow/body, with four mechanisms (self-learning → self-adaptation → self-optimization → self-generation).
- **The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement** · [arXiv:2609.11873](https://arxiv.org/abs/2609.11873) — a roadmap for RSI across science / embodied / software, emphasizing evaluation and human control.
- **Self-evolving Embodied AI** · [arXiv:2602.04411](https://arxiv.org/abs/2602.04411) — memory updating / task switching / environment prediction / embodiment adaptation / model evolution.
- **Who Improves the Robot? Toward Physical Recursive Self-Improvement** · [arXiv:2610.18842](https://arxiv.org/abs/2610.18842) — a position + taxonomy survey proposing an **L0–L5 framework** that separates capability-level from meta-level updates and within-task from across-task gains, reserving **L5 for independently verified recursive gain**. A close, complementary companion to this list's L1–L4 criterion; notably it also insists on *independent verification* of the meta-level claim. See [CROSSWALK.md](./CROSSWALK.md) for a full-text mapping of its L0–L5 onto this list's L1–L4, per work.
- **Recursive Self-Improvement in Physical AI: Mechanisms, Evidence, and Evaluation** · [arXiv:2610.38266](https://arxiv.org/abs/2610.38266) — surveys physical AI through the link between *persistent capability* and *its improvement process*, distinguishing learner updates from improvers. Proposes an **L0–L3 rubric** (task-local adaptation → persistent capability gain → inherited process revision → verified improver gain) and common-data / interactive comparisons that separate the *use* of experience from its *acquisition*. A third independent physical-AI taxonomy; see [CROSSWALK.md](./CROSSWALK.md).
- **Weights or Skills? A Survey of Robot-Learning Techniques: from Action-Predicting Weights to Robots that Write their Own Skills** · [arXiv:2608.01851](https://arxiv.org/abs/2608.01851) — survey-level evidence for the first full-text finding above: the field is shifting from weight-level action prediction toward agents that author and reuse their own executable skills.
- **A Comprehensive Survey of Self-Evolving AI Agents** · [arXiv:2508.07407](https://arxiv.org/abs/2508.07407) — a broad view of software-side self-evolution (for comparison).
- **A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve** · [arXiv:2507.21046](https://arxiv.org/abs/2507.21046) · `TMLR 2026` — the most systematic software-side taxonomy, organizing self-evolution along four axes (*what* to evolve: model / memory / tools / workflow; *when*; *how*; *where*). A useful map for locating where a physical system's loop actually changes.
- **From Sliding Windows to Self-evolving Lifelong Memory: VLA Memory Paradigms for Long-Horizon Robotics** · [arXiv:2610.23319](https://arxiv.org/abs/2610.23319) · `arXiv 2026` — a VLA-specific taxonomy of memory by scope and persistence (five paradigms + one frontier), the memory-centric view of embodied self-evolution and why limited temporal context blocks experience reuse.
- **Safety in Self-Evolving Agents: A Survey** · [arXiv:2610.00093](https://arxiv.org/abs/2610.00093) · `arXiv 2026` — safety-focused: once experience becomes *reusable state* (weights, memory, tools, skills, workflows), past events become future causes, so content harmless in one context can later act with greater persistence, authority, or scope. The governance companion to the capability-focused entries here.

## 🤖 Body & morphology self-evolution (related, not graded)

A natural question is whether a robot can evolve its own **physical body**, not just its software. Work on robot **morphology** exists, but it sits outside this list's grading axis, so it is collected here without an L-level. The reason is methodological: these systems **search or co-design a body in simulation and finalize it there**; the new morphology is validated by a **simulated task score**, and any real-robot step is an offline demonstration that does **not feed back into the body search**. By this list's criterion — self-improvement that is autonomous, continual, and grounded in the system's own (physical) experience — a body produced by an offline design search is not a *self-evolved* executable unit. It is also exactly what the *Who Improves the Robot?* survey calls not **physically grounded**: only a change driven by what happened as the robot acted (real world or physics simulator, fed back into the next round) counts. No surveyed system closes that loop for the body yet.

- **GLAMDRING** · [arXiv:2609.19452](https://arxiv.org/abs/2609.19452) · `arXiv 2026` — jointly synthesizes a quadruped morphology (link geometry + actuators from a library) and a CPG gait controller under hard velocity/power/payload/actuator-envelope constraints. Everything is searched and validated **in IsaacSim**; the real-robot step runs the synthesized controller on an **off-the-shelf Unitree Go2** whose spec was deliberately chosen so the search converges to Go2 (no new body is built). Authors state it is "not intended as a full sim-to-real robustness study."
- **LACE-CRAFT** · [arXiv:2610.09283](https://arxiv.org/abs/2610.09283) · `arXiv 2026` — LLM-driven body–reward co-design that **inherits the incumbent's actor parameters** across morphology changes (so control experience is reused, not thrown away) and selects by a **fixed simulated task metric** over five Brax/MuJoCo locomotion tasks. A single 3D-printed prototype walks indoors, but the printed geometry differs from the simulated one, thin parts fractured, and the authors list "quantitative transfer from the co-design search" and "closing the sim-to-real loop" as **future work** — the physical result does not inform the design.
- **Morphogene** · [arXiv:2609.31329](https://arxiv.org/abs/2609.31329) · `arXiv 2026` — a compact latent "gene" blueprint that jointly conditions limb-level morphology and control generation; an offline joint-optimization formulation of brain–body co-design.
- **Tensegrity modular reconfigurable robots** · [arXiv:2608.27221](https://arxiv.org/abs/2608.27221) · `Nature Machine Intelligence 2026` — compliant tensegrity modules that dock and rearrange into **task-adaptive multi-robot morphologies**. The body genuinely changes in hardware, but reconfiguration is **task-driven planning/control**, not a capability evolved from the robot's own failure experience.
- **Recompositional Robotics (position)** · [arXiv:2609.37734](https://arxiv.org/abs/2609.37734) · `IROS 2026 Workshop` — argues for making not only morphology but **capability** (a joint function across kino-dynamics, perception, compute, coordination) open-set and lifelong. The closest articulation of a body-level self-evolution *vision*, but a position paper with no system or physical gain.

> Scope note: these are included because readers rightly ask about body/morphology. They are **not graded** because their improvement is an offline, simulation-validated design artifact rather than an autonomous, physically grounded, continually self-evolved capability. This is the same gap as the empty complete physical L4 above, viewed from the hardware side.

### Real2Sim2Real: the physical-grounding enabler, and why the loop stays open

The most realistic path toward *physically grounded* self-evolution is **Real2Sim2Real (R2S2R)**: reconstruct the current real scene into a digital twin (Real→Sim), run cheap large-scale trial-and-error there (Sim), then deploy back to the robot and — ideally — feed the real outcome back to correct the twin and the next round (Sim→Real). In this list's terms, R2S2R is the bridge that can make a simulated improvement count as physically grounded, and it directly attacks self-improvement's hardest bottleneck: real-robot trials are too expensive, slow, and irreversible to supply the volume a self-evolution loop needs. *Who Improves the Robot?* names HomeBody (a foundation-model agent that builds a digital twin from robot observations and SLAM geometry) as an instance; LACE-CRAFT's mesh→articulation→simulation pipeline is a Real→Sim instance.

**Key techniques it requires:** geometry reconstruction / digital twin; object 6-DoF pose and articulation (joints, contacts, physical properties); system identification (mass, friction, damping, contact stiffness — what sets the sim-to-real gap); simulation-ready asset generation (URDF/collision/inertia); high-throughput GPU-parallel simulation; domain randomization; automatic task/curriculum/data generation; sim-to-real transfer (actuator modeling, latency compensation); and — the decisive pieces — **continual feedback of the real outcome into the twin, and physical (not simulated) verification of each improvement.**

**Why today's self-evolution work does not actually use it end-to-end:** systems use the first half (reconstruct + train in sim) but not the second half (continual Sim→Real feedback + physical verification), which is exactly the half self-evolution needs. The reasons compound: (1) system identification is imprecise, so feeding a mis-estimated parameter back can make the next round evolve in a *more* wrong sim — not feeding back is safer; (2) a continual loop needs many rounds, but each round's "Real" end hits the expensive/slow/irreversible real-robot bottleneck, so the loop stalls after one pass (LACE-CRAFT lists real-to-design feedback as future work); (3) causal attribution across the sim/real seam is unsolved — a real failure could be the policy, the modeling, or the body, so you cannot tell which to correct; (4) once verification falls back to a simulated score it fails SEAR's controls and *Who Improves the Robot?*'s sealed-judge / physical-grounding requirement; (5) the engineering chain is long with no shared open substrate, so most teams close only the one or two links their paper needs. The missing second half is precisely the "grounded, continual" essence of physical self-evolution — which is the technical root of why complete physical L4/L5 is still empty.

## 🔗 Related lists

- [`cocacola-lab/awesome-embodied-rsi`](https://github.com/cocacola-lab/awesome-embodied-rsi) — a curated list organized by L0–L4 and by improvement target.

---

## Repository contents

- [`CLASSIFICATION.md`](./CLASSIFICATION.md) — the L1–L4 grade of every work **derived from a close reading of each paper**, with boundary / weight-leaning cases reasoned explicitly.
- [`GRADING.md`](./GRADING.md) — the grading methodology: full definition of the L1–L4 criterion, the decision procedure, and full-text mechanism cards for in-depth works.
- [`PAPERS.md`](./PAPERS.md) — the per-paper table: input / what evolves / new executable unit / validation strictness / weights touched / grade + reason / verification level.
- [`references.bib`](./references.bib) — BibTeX for all entries.
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) — inclusion criteria and entry format.

## Contributing

Contributions welcome. Each new entry must: cite a primary source (arXiv / conference); be graded by this list's criterion with the "new executable unit (or none)" stated; and carry the secondary tags. See [CONTRIBUTING.md](./CONTRIBUTING.md).

## Maintainer

Maintained by **Zitong Bo**.

- Homepage: [zitongbo.github.io](https://zitongbo.github.io/)
- RedNote (Xiaohongshu): [profile](https://www.xiaohongshu.com/user/profile/59dc1d56db2e601ae168a5bb)
- Zhihu: [profile](https://www.zhihu.com/people/qian-chang-22-46/posts)

## License

[MIT](./LICENSE). Papers in this list are the property of their respective authors.
