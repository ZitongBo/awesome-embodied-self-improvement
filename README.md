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

**45** embodied self-improvement works (L1 · 8 ｜ L1–L2 · 1 ｜ L2 · 13 ｜ L3 · 17 ｜ L4 · 1 at the lower bound + 5 nascent)  ·  **3** benchmarks  ·  **4** surveys  ·  2 software-domain references

[Grading criterion](#grading-criterion-one-line-decision) · [Index by improvement target](#index-by-improvement-target-orthogonal-view) · [L1](#l1--in-episode-feedback-recovery-improvement-reset-to-zero) · [L2](#l2--retained-experience-persistent-but-the-executable-action-set-is-unchanged) · [L3](#l3--agent-driven-capability-expansion-a-new-previously-infeasible-executable-action) · [L4](#l4--rsi-improving-the-improvement-mechanism-itself) · [Benchmarks](#-benchmarks--datasets) · [Surveys](#-surveys) · [Grading methodology](./GRADING.md) · [Per-paper table](./PAPERS.md) · [Contributing](./CONTRIBUTING.md)

</div>

|  |  |  |  |
|:--:|:--:|:--:|:--:|
| 🧭 **[Grading criterion](#grading-criterion-one-line-decision)**<br/>one-line decision | 🗂️ **[By level](#the-list)**<br/>L1 · L2 · L3 · L4 | 🎯 **[By target](#index-by-improvement-target-orthogonal-view)**<br/>which layer to change | 🆕 **[Recently added](#-recently-added)**<br/>latest entries |
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

**Tag legend:** `🤖real` real-robot experiments ｜ `🧪sim` simulation ｜ `🧊frozen` base model weights frozen ｜ `⚙️weights` updates policy/world-model weights ｜ `📂open` code available. Each entry also shows its **venue + year**.

</details>

**Current state of the field:** the frontier concentrates at **L3**; **L4 is no longer entirely empty** — PhysEvo touches the lower bound in its weakest form (a meta-agent that improves and reuses its own diagnostic tools), but a complete physical-AI L4 that recursively improves the selection logic itself remains open.

---

## Index by improvement target (orthogonal view)

The main list is organized by **capability level L1–L4** ("how strong"). Many practitioners instead ask "**which layer do I want to change**". The orthogonal index below groups works by **improvement target**. A work may span several targets; it is listed under its **primary** one.

| Improvement target | What it changes | Representative works (level) |
|---|---|---|
| **Model & Policy** | Policy / world-model **weights** or decision rules | Self-Improving EFM `L2` · RECAP (π*0.6) `L2` · RoboCat `L2` · VLAW `L2` · MEDAL++ `L2` · LiReN `L2` · SEES `L3` · RoboClaw `L3` |
| **Memory & Knowledge** | Memory content / retrieval / consolidation | ABot-AgentOS `L2` · ME-Brain `L2` · SafeMem `L2` · BATON `L2` · Harness VLA's memory `L2` |
| **Skills & Behaviors** | Executable skill library (add / reuse / compose) | ASPIRE `L3` · RATs `L3` · RoboSkill `L3` · LRLL `L3` · Voyager `L3` · Skill-Space Shooting `L3` · EmbodiSkill (text skills) `L2` |
| **Harness & System** | Runtime middleware / tools / orchestration / routing / graph | Zetta `L3` · SHAPER `L3` · RoboHarness `L3` · GaP `L3` · RoboFoundry `L3` · HarnessPAI `L3` · AdaHVLA `L3` · CaP-X `L3` · ETA `L3` |
| **Control Interface** | The action / observation interface itself | PhysEvo (joint-level control + observation tools) `L3`+`L4 lower bound` |
| **Diagnostic / Meta** | The diagnosis / validation / promotion mechanism itself | **PhysEvo** `L4 lower bound` · ENPIRE / AgenticRobotics / RegenHarness / EmbodiedRSI / RPG (`L3→L4 nascent`) |
| **Embodiment** | Morphology / sensors / actuators / body coupling | *(very few public works; real-robot morphology adaptation is usually folded into Control Interface or Model & Policy)* |
| **Safety & Governance** | Constraints / auditing / rollback / upgrade safety | SafeMem `L2` (risk prediction triggers conservative replanning) · see EmbodiedGovBench |

### Level × improvement-target quick-reference matrix

Rows = improvement target, columns = capability level; cells list representative works. **An empty cell = that intersection currently has few public physical-AI works** (a potential research gap).

| Target \ Level | L1 | L2 | L3 | L3→L4 (nascent) | L4 (lower bound) |
|---|---|---|---|---|---|
| **Model & Policy** | — | Self-Improving EFM, RECAP, RoboCat, VLAW, MEDAL++, LiReN | SEES, RoboClaw | — | — |
| **Memory & Knowledge** | — | ABot-AgentOS, ME-Brain, SafeMem, BATON | — | — | — |
| **Skills & Behaviors** | — | EmbodiSkill, Harness VLA | ASPIRE, RATs, RoboSkill, LRLL, Voyager, Skill-Space Shooting | — | — |
| **Harness & System** | EmbodiedSkills | — | Zetta, SHAPER, RoboHarness, GaP, RoboFoundry, HarnessPAI, AdaHVLA, CaP-X, ETA | ENPIRE, AgenticRobotics, RegenHarness, EmbodiedRSI, RPG | — |
| **Control Interface / Observation** | Inner Monologue, DoReMi, COME-robot, CAPE, REFLECT, CycleVLA, AgentChord, Intrinsic Reward | — | PhysEvo | — | — |
| **Diagnostic / Meta mechanism** | — | — | — | — | **PhysEvo (weakest)** |
| **Embodiment (morphology / hardware)** | — | — | — | — | — |

> Note on the two rightmost columns: **L3→L4 (nascent)** works are still L3 — they reach *toward* the meta-level but keep the improvement protocol fixed (threshold not crossed). **L4 (lower bound)** is only PhysEvo, the single work whose meta-agent improves its own diagnostic machinery (threshold just crossed). The five nascent works are **not** in L4.

> **Two visible gaps:** ① **Embodiment (self-modification of the body) is nearly empty across all levels** — post-deployment adaptation of real-robot morphology/sensors is still open; ② the **Diagnostic/Meta layer is touched only by PhysEvo in its weakest form** — a complete physical-AI L4 that recursively improves the selection logic itself remains open.

---

## 🆕 Recently added

Most recent entries by arXiv date (newest first):

- **PhysEvo** · `arXiv 2026-10` · `L3`+`L4 lower bound` — first physical work to touch the L4 lower bound. → [L4](#l4--rsi-improving-the-improvement-mechanism-itself)
- **EmbodiedRSI** · `arXiv 2026-10` · `L3→L4 nascent` — value-of-information experiment selection for code/skill co-evolution. → [L4](#l4--rsi-improving-the-improvement-mechanism-itself)
- **RPG** · `arXiv 2026-10` · `L3→L4 nascent` — weight-free self-improvement that also revises its own system prompt. → [L4](#l4--rsi-improving-the-improvement-mechanism-itself)
- **Skill-Space Shooting** · `arXiv 2026-09` · `L3` — corrective actions distilled into reusable short skills. → [L3](#l3--agent-driven-capability-expansion-a-new-previously-infeasible-executable-action)
- **RoboSkill** · `arXiv 2026-09` · `L3` — Explore-Execute-Evolve skill acquisition/reuse loop. → [L3](#l3--agent-driven-capability-expansion-a-new-previously-infeasible-executable-action)

---

## The list

## L1 — In-episode feedback recovery (improvement reset to zero)

> Uses vision, tool errors, or execution feedback to change the current prompt/plan/constraints and retry; **after a reset it returns to the starting point, with no accumulation and no capability expansion**. This is closed-loop correction, not retained evolution.

- **Inner Monologue: Embodied Reasoning through Planning with Language Models** · [arXiv:2207.05608](https://arxiv.org/abs/2207.05608) · `CoRL 2022` · `L1` `🤖real` — feeds success detection / scene description / human interaction back into the LLM to form an "inner monologue" closed-loop replanner.
- **CAPE: Corrective Actions from Precondition Errors using LLMs** · [arXiv:2211.09935](https://arxiv.org/abs/2211.09935) · `arXiv 2022` · `L1` `🧪sim` — on a precondition error, re-prompts the LLM to extract an executable corrective action.
- **DoReMi: Grounding LM by Detecting and Recovering from Plan-Execution Misalignment** · [arXiv:2307.00329](https://arxiv.org/abs/2307.00329) · `arXiv 2023` · `L1` `🤖real` — a VQA model periodically detects plan–execution misalignment and recovers immediately.
- **REFLECT: Summarizing Robot Experiences for Failure Explanation and Correction** · [arXiv:2306.15724](https://arxiv.org/abs/2306.15724) · `CoRL 2023` · `L1` `🤖real` — multimodal failure summary → LLM locates the cause → corrective plan; ships the RoboFail dataset.
- **COME-robot: Closed-Loop Open-Vocabulary Mobile Manipulation with GPT-4V** · [arXiv:2404.10220](https://arxiv.org/abs/2404.10220) · `arXiv 2024` · `L1` `🤖real` — a closed-loop GPT-4V framework for open-vocabulary mobile manipulation; iteratively updates the plan / recovers from failure, ~+35% success over prior SOTA.
- **CycleVLA: Proactive Self-Correcting VLA via Subtask Backtracking & MBR Decoding** · [arXiv:2601.02295](https://arxiv.org/abs/2601.02295) · `arXiv 2026` · `L1` `🤖real` `📂open` — predicts incipient failure at subtask boundaries, backtracks, and retries with MBR decoding (inference-time self-correction).
- **AgentChord: Proactive Failure Recovery through an Agentic Task Graph** · [arXiv:2605.11951](https://arxiv.org/abs/2605.11951) · `RSS 2026` · `L1` `🤖real` `📂open` — builds a task graph with anticipated recovery branches so low-latency monitors trigger corrections.
- **Intrinsic Robot Rewarding: Reusing VLA Representations for Autonomous Evaluation** · [arXiv:2609.17115](https://arxiv.org/abs/2609.17115) · `arXiv 2026` · `L1` `🤖real` — reuses a frozen VLA encoder for autonomous outcome scoring to reduce human labeling; not yet connected to persistent policy improvement.
- **EmbodiedSkills: A Unified Framework for Orchestrating/Training/Deploying VLA Agents** · [arXiv:2609.01281](https://arxiv.org/abs/2609.01281) · `arXiv 2026` · `L1~L2` `🧪sim` — a fixed skill interface with prerequisite preflight / outcome verification; records trajectories for optional online adaptation.

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
- **BATON: Long-Horizon Manipulation via Agentic Subtask Exploration & Transition-aware Memory** · [arXiv:2608.16889](https://arxiv.org/abs/2608.16889) · `arXiv 2026` · `L2` `🧪sim` — freezes the VLA and stores reusable subtask solutions in language memory; no parameter updates.

### Weight-type L2 (changes weights, but adds no nameable new executable action)

- **Self-Improving Embodied Foundation Models** · [arXiv:2509.15155](https://arxiv.org/abs/2509.15155) · `arXiv 2025` · `L2` `🤖real` `⚙️weights` — a two-stage recipe derives rewards (Steps-to-Go) and success detection; robot fleets practice autonomously and update policy weights.
- **π*0.6 (RECAP): a VLA That Learns From Experience** · [arXiv:2511.14759](https://arxiv.org/abs/2511.14759) · `arXiv 2025` · `L2` `🤖real` `⚙️weights` — advantage-conditioned learning from real deployment experience plus corrections, updating VLA weights.
- **RoboCat: A Self-Improving Generalist Agent for Robotic Manipulation** · [arXiv:2306.11706](https://arxiv.org/abs/2306.11706) · `TMLR 2024` · `L2` `🤖real` `⚙️weights` — generates self-practice trajectories folded into the next round of generalist training.
- **VLAW: Iterative Co-Improvement of VLA Policy and World Model** · [arXiv:2602.12063](https://arxiv.org/abs/2602.12063) · `arXiv 2026` · `L2` `🤖real` `⚙️weights` — alternates improving the world model and the policy (both at the weight level).
- **MEDAL++: Self-Improving Robots via End-to-End Autonomous Visuomotor RL** · [arXiv:2303.01488](https://arxiv.org/abs/2303.01488) · `CoRL 2023` · `L2` `🤖real` `⚙️weights` — learns task and reset behaviors to practice autonomously via weight-level RL.
- **LiReN: Lifelong Autonomous Improvement of Navigation Foundation Models in the Wild** · [OpenReview](https://openreview.net/forum?id=vBj5oC60Lk) · `CoRL 2024` · `L2` `🤖real` `⚙️weights` `📂open` — a navigation foundation model fine-tunes from online experience after deployment.

---

## L3 — Agent-driven capability expansion (a new, previously infeasible executable action)

> The self-improvement **adds at least one previously infeasible executable unit** (new skill / grasp synthesis / placement / motion primitive / computation-graph node / symbolic predicate). The base policy is usually kept frozen. **This is the real frontier for physical AI.**

- **ASPIRE: Agentic Skills Discovery for Robotics** (NVIDIA GEAR) · [arXiv:2607.00272](https://arxiv.org/abs/2607.00272) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — diagnoses from per-primitive traces → writes/repairs code-as-policy → distills **new reusable skills** into a library (e.g., Multi-Angle Approach); LIBERO-90 → LIBERO-Pro Long **zero-shot 31% vs 4%**.
- **Zetta: Closed-Loop Embodied Harness for Self-Evolving Physical Intelligence** · [arXiv:2608.16590](https://arxiv.org/abs/2608.16590) · `arXiv 2026` · `L3` (with L2 scheduling) `🧪sim` `🧊frozen` `📂open` — evolves code critics/recovery/tools online; synthesizes **GraspGen re-grasp / CAP stable placement / impedance control** ("beyond the base VLA's capabilities"); LIBERO-Pro 34.5%→90.8%, 11.1× speedup.
- **SHAPER: Self-Evolving Embodied Agents via Skill-Harness Evolution** · [arXiv:2608.11350](https://arxiv.org/abs/2608.11350) · `arXiv 2026` · `L3` `🧪sim` `🧊frozen` — train-free evolution of reusable skills and a context-code harness.
- **RoboHarness: Memory-Driven Orchestration of Heterogeneous Robot Policies** (Huawei Noah's Ark) · [arXiv:2607.18060](https://arxiv.org/abs/2607.18060) · `arXiv 2026` · `L3` (variant) `🤖real` `⚙️partial weights` — PDDLLM learns **new symbolic predicates** + Memory-Bridge synthesizes **handoff actions**; SIMPACT additionally tunes low-level grasp poses. LIBERO-Plus 91.9%.
- **GaP: Graph-as-Policy Multi-Agent Self-Learning Harness** · [arXiv:2607.05369](https://arxiv.org/abs/2607.05369) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — generates **new directed computation graphs** (perception/planning/control nodes) from a modular skill library; after self-improvement in sim, runs the graph on real robots.
- **RoboFoundry: System-as-Policy Evolution for Self-Learning Embodied Agents** · [arXiv:2609.32862](https://arxiv.org/abs/2609.32862) · `arXiv 2026` · `L3` (with L2) `🤖real` `🧊frozen` — the hierarchical skill surface adds atomic skills/compositions (`pick_and_place_sim_object`); capability-conditioned held-out promotion. Improves GPT-5.5 by 27.8% on EmbodiedBench.
- **RATs: Playful Agentic Robot Learning** · [arXiv:2606.19419](https://arxiv.org/abs/2606.19419) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — self-directed play proposes tasks → executes/diagnoses code policies → distills a **persistent skill library** transferable to downstream real-robot tasks.
- **RoboSkill: A Skill Acquisition and Reuse Loop for Embodied Agents** · [arXiv:2609.37810](https://arxiv.org/abs/2609.37810) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` — an Explore-Execute-Evolve loop **evolves the skill library**; +12.5–25 pp first-episode success on LIBERO-10.
- **CaP-X: Benchmarking and Improving Coding Agents for Robot Manipulation** · [arXiv:2603.22435](https://arxiv.org/abs/2603.22435) · `arXiv 2026` · `L3` (CaP-RL variant updates weights) `🤖real` `📂open` — CaP-Agent0 **synthesizes new skills** from execution feedback; CaP-RL adds weight-level updates.
- **HarnessPAI: An Evolving Harness for Physical AI** · [arXiv:2609.29166](https://arxiv.org/abs/2609.29166) · `arXiv 2026` · `L3` `🧪sim` `🧊frozen` — revises an **executable task program** from execution feedback and retains failure-repair knowledge; LIBERO-PRO +61.6 pp over pi0.5.
- **AdaHVLA: Adaptive Harnesses for Long-Horizon VLA Execution** · [arXiv:2609.29204](https://arxiv.org/abs/2609.29204) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` — multiple agents perform **code-level harness revision**, keeping a hypothesis-revision-effect graph.
- **ETA / OpenETA: A New Agentic Paradigm for Embodied Tasks** · [arXiv:2608.03924](https://arxiv.org/abs/2608.03924) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — a Planner-Interface-World loop turns interactions into **reusable skills/experience**.
- **Skill-Space Shooting for Autonomous Robot Policy Improvement** · [arXiv:2609.38178](https://arxiv.org/abs/2609.38178) · `arXiv 2026` · `L3` `🤖real` — explores corrective actions as **reusable short skills** and turns them into policy training signals, shared across tasks.
- **SEES: Self-Evolving Embodied System via Failure-Guided VLA Policy Adaptation** · [arXiv:2609.32698](https://arxiv.org/abs/2609.32698) · `arXiv 2026` · `L3` (weight-leaning) `🧪sim` `⚙️weights` — reconstructs repeatedly failing atomic skills in simulation and updates shared VLA adapters via online RL.
- **RoboClaw: Agentic Framework for Scalable Long-Horizon Robotic Tasks** · [arXiv:2603.11558](https://arxiv.org/abs/2603.11558) · `arXiv 2026` · `L3` (weight-leaning) `🤖real` `📂open` — paired forward/inverse behaviors for self-resetting collection plus iterative policy refinement on real robots.
- **LRLL: Lifelong Robot Library Learning** · [arXiv:2406.18746](https://arxiv.org/abs/2406.18746) · `ICRA 2024` · `L3` `🤖real` `🧊frozen` — proposes tasks → stores experience → distills **reusable policies/skills** (no gradient updates; new skills generated via LLM coding).
- **Voyager: An Open-Ended Embodied Agent with LLMs** (Minecraft) · [arXiv:2305.16291](https://arxiv.org/abs/2305.16291) · `TMLR 2024` · `L3` `🧪sim` `🧊frozen` `📂open` — automatic curriculum + an ever-growing executable code skill library + iterative self-verification (foundational for embodied digital worlds).

---

## L4 — RSI (improving the improvement mechanism itself)

> The system improves not only its own capabilities but **the diagnosis / validation / promotion mechanism that produces those improvements**. **Physical AI is touched only in its weakest form; there is no mature instance yet.**

- **PhysEvo: Astra Can Act, Let It** · [arXiv:2610.08995](https://arxiv.org/abs/2610.08995) · `arXiv 2026` · **`L3` + first to touch the `L4` lower bound (physical)** · `🤖real` `🧊frozen` — a single frozen model plays both task-agent and meta-agent roles. L3: joint-level control / active + retrospective observation tools / reusable skills. **L4 crux:** the meta-agent **improves and reuses its own diagnostic tools** ("inherits a way to improve, not only a way to act"). **Still the weakest instance:** the Revise→Test→Select meta-loop skeleton is fixed, so it edits diagnostic tools rather than the selection logic. RoboDojo 62% SR; real robot 84% SR.

### Nascent L4 (self-described "toward RSI"; mechanically still enhanced L3)

- **ENPIRE: Agentic Robot Policy Self-Improvement in the Real World** · [arXiv:2606.19980](https://arxiv.org/abs/2606.19980) · `CoRL 2026` · `L3→L4 nascent` `🤖real` — automatic reset/verify/rollout plus evolution of training infrastructure and algorithm code across a fleet.
- **You Don't Need To Stay in The Loop (AgenticRobotics)** · [arXiv:2608.07555](https://arxiv.org/abs/2608.07555) · `arXiv 2026` · `L3→L4 nascent` `🧪sim` — makes train-evaluate-improve into evidence-gated transactions with auditable promotion.
- **RegenHarness: Robot Agent Harness with Evidence-Gated Recursive Self-Improvement** · [arXiv:2609.27612](https://arxiv.org/abs/2609.27612) · `arXiv 2026` · `L3→L4 nascent` `🤖real` — revises task-template/routing/recovery code; self-described as recursive but does not establish improving the improvement step.
- **EmbodiedRSI: Active Continual Robot Learning via Hypothesis-Guided Co-Evolution** · [arXiv:2610.10498](https://arxiv.org/abs/2610.10498) · `arXiv 2026` · `L3→L4 nascent` `🤖real` — autonomously decides where to explore next and turns physical interaction into better code/skills.
- **RPG: Reconstruct, Practice, Go Real — Guided Self-Improvement** · [arXiv:2610.02204](https://arxiv.org/abs/2610.02204) · `arXiv 2026` · `L3→L4 nascent` `🤖real` — weight-free self-improvement; develops new symbolic skills + refines + revises the system prompt; 22 tasks 28.6%→95.0%.

### Software-domain L4 references (not physical AI, for comparison)

- **Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents** · [arXiv:2505.22954](https://arxiv.org/abs/2505.22954) · `arXiv 2025` · `L4 (software/coding)` `📂open` — rewrites its own code and improves its ability to rewrite code; SWE-bench 20%→50%.
- **Hyperagents** · [arXiv:2603.19461](https://arxiv.org/abs/2603.19461) · `arXiv 2026` · `L4 (sim/software)` `🧪sim` `📂open` — a task agent plus an **editable meta agent** so the mechanism producing future modifications can itself evolve; its robotics evidence is simulated reward design only.

---

## 🧪 Benchmarks & Datasets

- **EmbodiedMemory-Bench** · [arXiv:2609.28236](https://arxiv.org/abs/2609.28236) `📂open` — tests whether memory built from earlier observations/interactions supports later embodied actions (2,554 episodes).
- **EmbodiedGovBench** · [arXiv:2604.11174](https://arxiv.org/abs/2604.11174) — governance-oriented evaluation: capability boundaries, runtime drift, recovery, upgrade safety, human override, audit completeness.
- **RoboDojo / LIBERO-Pro / RoboCasa / EmbodiedBench / RMBench** — evaluation suites used by many works above (see each entry).

## 📚 Surveys

- **Self-Evolving AI for Humanoids: Mechanisms, Safety, and Evaluation of Post-Deployment Self-Improvement** · [arXiv:2609.13236](https://arxiv.org/abs/2609.13236) — post-deployment self-evolution over policy/perception/memory/workflow/body, with four mechanisms (self-learning → self-adaptation → self-optimization → self-generation).
- **The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement** · [arXiv:2609.11873](https://arxiv.org/abs/2609.11873) — a roadmap for RSI across science / embodied / software, emphasizing evaluation and human control.
- **Self-evolving Embodied AI** · [arXiv:2602.04411](https://arxiv.org/abs/2602.04411) — memory updating / task switching / environment prediction / embodiment adaptation / model evolution.
- **A Comprehensive Survey of Self-Evolving AI Agents** · [arXiv:2508.07407](https://arxiv.org/abs/2508.07407) — a broad view of software-side self-evolution (for comparison).

## 🔗 Related lists

- [`cocacola-lab/awesome-embodied-rsi`](https://github.com/cocacola-lab/awesome-embodied-rsi) — a curated list organized by L0–L4 and by improvement target.

---

## Repository contents

- [`CLASSIFICATION.md`](./CLASSIFICATION.md) — the L1–L4 grade of every work **derived from a close reading of each paper**, with boundary / weight-leaning / nascent cases reasoned explicitly.
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
