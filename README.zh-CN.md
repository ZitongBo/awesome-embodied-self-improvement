<div align="center">

# Awesome Embodied Self-Improvement [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

**面向从业者的具身自我改进（Embodied Self-Improvement）精选清单。**

[English](./README.md) · **中文**

> 不只递归自我改进（RSI），更广义的**自进化（self-evolution）**也纳入。
> 范围严格限定 **具身智能 / 机器人 / physical AI**；每项工作必须体现**部署后的自我改进**。

![Scope](https://img.shields.io/badge/scope-embodied%20%2F%20robot%20%2F%20physical--AI-blue?style=flat-square)
![Grading](https://img.shields.io/badge/grading-L1%E2%80%93L4%20by%20executable--action%20delta-f97316?style=flat-square)
![Verified](https://img.shields.io/badge/entries-arXiv%20verified-2ea44f?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

**45** 项具身自我改进工作（L1 · 8 ｜ L1–L2 · 1 ｜ L2 · 13 ｜ L3 · 17 ｜ L4 · 1 触及下沿 + 5 苗头）  ·  **3** 个 benchmark  ·  **4** 篇 survey  ·  2 项软件域对照

[判级口径](#判级口径一句话决策) · [按改进对象索引](#按改进对象索引正交视图) · [L1](#l1--episode-内反馈恢复改进-reset-后清零) · [L2](#l2--经验留存改进持久但可执行动作集合不变) · [L3](#l3--agent-主导的能力扩张新增一个之前做不出的可执行动作) · [L4](#l4--rsi改进产生改进的机制本身) · [Benchmarks](#-benchmarks--datasets) · [Surveys](#-surveys) · [判级方法论](./GRADING.md) · [逐篇详表](./PAPERS.md) · [贡献](./CONTRIBUTING.md)

</div>

|  |  |  |  |
|:--:|:--:|:--:|:--:|
| 🧭 **[判级口径](#判级口径一句话决策)**<br/>一句话决策 | 🗂️ **[按级别](#清单)**<br/>L1 · L2 · L3 · L4 | 🎯 **[按改进对象](#按改进对象索引正交视图)**<br/>想改哪一层 | 🆕 **[最近新增](#-最近新增)**<br/>最新条目 |
| 📊 **[逐篇详表](./PAPERS.md)**<br/>判级+理由 | 📑 **[分级说明](./CLASSIFICATION.md)**<br/>判级重新推导 | 📚 **[Benchmarks & Surveys](#-benchmarks--datasets)** | 🤝 **[贡献](./CONTRIBUTING.md)** |

---

## 这是什么

一张**人工审核、按能力分级**的具身自我改进工作地图。每一项都已核到一手出处（arXiv / 会议），并按一条单一、可判定、无灰带的判据归入 **L1–L4**。目标：让从业者一眼看清**一个系统的自我改进到底强在哪一级**，而不是被"self-evolving / RSI"这类自称干扰。

## 判级口径（一句话决策）

> **这次自我改进之后，系统能执行的「动作/技能集合」有没有多出一个它之前执行不出来的动作？** — 没有 → **L2**；有 → **L3**。reset 后清零 → **L1**。改进「产生改进」的机制本身 → **L4**。

<details>
<summary><b>完整判据、副轴标签与图例</b>（点击展开）</summary>

**主轴**：自我改进落在系统的哪一层。

| 级别 | 判据 | 一句话 |
|:--:|---|---|
| **L1** | 改进 **reset 后清零** | 只改当前 episode 的 prompt/计划/约束；场景复位即回到起点 |
| **L2** | 持久，但**可执行动作集合不变** | 优化"**怎么用**"现有能力：记忆/文本规则/路由/纯监测 critic/已有原语重排/参数 |
| **L3** | 持久，且**新增一个之前做不出的可执行动作/技能** | 扩张"**有哪些能力**"：新抓取合成/新放置/新运动原语/新计算图节点/新符号谓词 |
| **L4** | 改进的是**产生改进的那套机制**本身 | 修改自己的诊断 / 验证 / 晋升逻辑 |

**不参与判级的副轴（仅作标签）**：验证严格度（写入即用 / 当轮 / held-out 泛化闸门）、是否触及底模权重。
**原则**：机制优先于自称；同一系统内部混有 L2 与 L3 时，只要出现任一真·新增可执行单元即归 L3，并把 L2 部分单独标注；无法核验的标 ⚠️。

**标签图例**：`🤖real` 有真机实验 ｜ `🧪sim` 仿真 ｜ `🧊frozen` 冻结底模权重 ｜ `⚙️weights` 更新策略/世界模型权重 ｜ `📂open` 有代码。每条还标注**会议 + 年份**。

</details>

**当前领域状态**：前沿集中在 **L3**；**L4 不再完全为空**——PhysEvo 以最弱形态触及下沿（meta-agent 改进并复用自身诊断工具），但"递归改进选择逻辑本身"的完整 physical-AI L4 仍是空白。

---

## 按改进对象索引（正交视图）

主清单按**能力级别 L1–L4** 组织（"进化到多强"）。很多从业者更关心"**我想改系统的哪一层**"。下面给一个正交索引：按**改进对象**分组。同一工作可能跨多类，列在其**主要**改进对象下。

| 改进对象 | 它改的是什么 | 代表工作（级别） |
|---|---|---|
| **Model & Policy** | 策略/世界模型**权重**或决策规则 | Self-Improving EFM `L2` · RECAP (π*0.6) `L2` · RoboCat `L2` · VLAW `L2` · MEDAL++ `L2` · LiReN `L2` · SEES `L3` · RoboClaw `L3` |
| **Memory & Knowledge** | 记忆内容 / 检索 / 巩固 | ABot-AgentOS `L2` · ME-Brain `L2` · SafeMem `L2` · BATON `L2` · Harness VLA 的记忆 `L2` |
| **Skills & Behaviors** | 可执行技能库（新增/复用/组合） | ASPIRE `L3` · RATs `L3` · RoboSkill `L3` · LRLL `L3` · Voyager `L3` · Skill-Space Shooting `L3` · EmbodiSkill（文本技能）`L2` |
| **Harness & System** | 运行时中间件 / 工具 / 编排 / 路由 / 计算图 | Zetta `L3` · SHAPER `L3` · RoboHarness `L3` · GaP `L3` · RoboFoundry `L3` · HarnessPAI `L3` · AdaHVLA `L3` · CaP-X `L3` · ETA `L3` |
| **Control Interface** | 动作 / 观察接口本身 | PhysEvo（关节级控制 + 观察工具）`L3`+`L4 下沿` |
| **Diagnostic / Meta** | 诊断 / 验证 / 晋升机制本身 | **PhysEvo** `L4 下沿` · ENPIRE / AgenticRobotics / RegenHarness / EmbodiedRSI / RPG（`L3→L4 苗头`） |
| **Embodiment** | 形态 / 传感器 / 执行器 / 本体耦合 | *（公开工作极少；真机形态自适应多并入 Control Interface 或 Model & Policy）* |
| **Safety & Governance** | 约束 / 审计 / 回滚 / 升级安全 | SafeMem `L2`（风险预测触发保守重规划）· 评测见 EmbodiedGovBench |

### 能力级别 × 改进对象 二维速查矩阵

行=改进对象，列=能力级别；格内为代表工作。**空格 = 该交叉点目前公开 physical-AI 工作稀缺**（潜在研究空白）。

| 改进对象 \ 级别 | L1 | L2 | L3 | L3→L4（苗头） | L4（下沿） |
|---|---|---|---|---|---|
| **Model & Policy** | — | Self-Improving EFM, RECAP, RoboCat, VLAW, MEDAL++, LiReN | SEES, RoboClaw | — | — |
| **Memory & Knowledge** | — | ABot-AgentOS, ME-Brain, SafeMem, BATON | — | — | — |
| **Skills & Behaviors** | — | EmbodiSkill, Harness VLA | ASPIRE, RATs, RoboSkill, LRLL, Voyager, Skill-Space Shooting | — | — |
| **Harness & System** | EmbodiedSkills | — | Zetta, SHAPER, RoboHarness, GaP, RoboFoundry, HarnessPAI, AdaHVLA, CaP-X, ETA | ENPIRE, AgenticRobotics, RegenHarness, EmbodiedRSI, RPG | — |
| **Control Interface / Observation** | Inner Monologue, DoReMi, COME-robot, CAPE, REFLECT, CycleVLA, AgentChord, Intrinsic Reward | — | PhysEvo | — | — |
| **Diagnostic / Meta 机制** | — | — | — | — | **PhysEvo（最弱）** |
| **Embodiment（形态 / 硬件）** | — | — | — | — | — |

> 右侧两列说明：**L3→L4（苗头）**本质仍是 L3——够到 meta 层但改进协议本身固定（未跨过门槛）；**L4（下沿）**只有 PhysEvo 一个，其 meta-agent 改进自身诊断机器（刚跨过门槛）。那五篇苗头**不在** L4 内。

> **两个明显空白**：① **Embodiment（本体形态自改）在各级近乎空白**——真机形态/传感器的部署后自适应仍是开放方向；② **Diagnostic/Meta 层只有 PhysEvo 以最弱形态触及**——"递归改进选择逻辑本身"的完整 physical-AI L4 仍是空白。

---

## 🆕 最近新增

按 arXiv 日期排序（最新在前）：

- **PhysEvo** · `arXiv 2026-10` · `L3`+`L4 下沿` — 首个触及 L4 下沿的 physical 工作。 → [L4](#l4--rsi改进产生改进的机制本身)
- **EmbodiedRSI** · `arXiv 2026-10` · `L3→L4 苗头` — 用 value-of-information 选实验来 co-evolve 代码/技能。 → [L4](#l4--rsi改进产生改进的机制本身)
- **RPG** · `arXiv 2026-10` · `L3→L4 苗头` — 无权重更新自改，还改自己的 system prompt。 → [L4](#l4--rsi改进产生改进的机制本身)
- **Skill-Space Shooting** · `arXiv 2026-09` · `L3` — 把纠正动作蒸馏成可复用短技能。 → [L3](#l3--agent-主导的能力扩张新增一个之前做不出的可执行动作)
- **RoboSkill** · `arXiv 2026-09` · `L3` — Explore-Execute-Evolve 技能获取/复用循环。 → [L3](#l3--agent-主导的能力扩张新增一个之前做不出的可执行动作)

---

## 清单

## L1 — Episode 内反馈恢复（改进 reset 后清零）

> 利用视觉 / 工具报错 / 执行反馈改当前 prompt/计划/约束并重试；**reset 后回到起点，不积累、不扩能力**。是闭环纠错，不是留存式进化。

- **Inner Monologue: Embodied Reasoning through Planning with Language Models** · [arXiv:2207.05608](https://arxiv.org/abs/2207.05608) · `CoRL 2022` · `L1` `🤖real` — 把成功检测/场景描述/人类交互反馈喂回 LLM，形成"内心独白"式闭环重规划。
- **CAPE: Corrective Actions from Precondition Errors using LLMs** · [arXiv:2211.09935](https://arxiv.org/abs/2211.09935) · `arXiv 2022` · `L1` `🧪sim` — 前置条件出错时重新提示 LLM 抽取可执行的纠正动作。
- **DoReMi: Grounding LM by Detecting and Recovering from Plan-Execution Misalignment** · [arXiv:2307.00329](https://arxiv.org/abs/2307.00329) · `arXiv 2023` · `L1` `🤖real` — VQA 定期检测 plan–execution 失配并即时恢复。
- **REFLECT: Summarizing Robot Experiences for Failure Explanation and Correction** · [arXiv:2306.15724](https://arxiv.org/abs/2306.15724) · `CoRL 2023` · `L1` `🤖real` — 多模态失败摘要→LLM 定位原因→纠正计划；配套 RoboFail 数据集。
- **COME-robot: Closed-Loop Open-Vocabulary Mobile Manipulation with GPT-4V** · [arXiv:2404.10220](https://arxiv.org/abs/2404.10220) · `arXiv 2024` · `L1` `🤖real` — 用 GPT-4V 的闭环开放词汇移动操作框架；靠反馈迭代更新计划/从失败恢复，成功率较先前 SOTA ~+35%。
- **CycleVLA: Proactive Self-Correcting VLA via Subtask Backtracking & MBR Decoding** · [arXiv:2601.02295](https://arxiv.org/abs/2601.02295) · `arXiv 2026` · `L1` `🤖real` `📂open` — 在子任务边界预判失败、回溯并用 MBR 解码重试（推理时自纠）。
- **AgentChord: Proactive Failure Recovery through an Agentic Task Graph** · [arXiv:2605.11951](https://arxiv.org/abs/2605.11951) · `RSS 2026` · `L1` `🤖real` `📂open` — 预建带预设恢复分支的任务图，低延迟监测触发纠正。
- **Intrinsic Robot Rewarding: Reusing VLA Representations for Autonomous Evaluation** · [arXiv:2609.17115](https://arxiv.org/abs/2609.17115) · `arXiv 2026` · `L1` `🤖real` — 复用冻结 VLA 编码器做自主评分以减少人工标注；尚未连到持久策略改进。
- **EmbodiedSkills: A Unified Framework for Orchestrating/Training/Deploying VLA Agents** · [arXiv:2609.01281](https://arxiv.org/abs/2609.01281) · `arXiv 2026` · `L1~L2` `🧪sim` — 固定技能接口做前置校验/结果验证；记录轨迹供可选在线适应。

---

## L2 — 经验留存（改进持久，但可执行动作集合不变）

> 系统"**知道得更多 / 调度得更准**"，但"**会做的动作集合不变**"。分两小类：**内容型**（改记忆/文本/声明式策略）与**权重型**（改权重但不新增可点名的新可执行动作）。

### 内容型 L2

- **Harness VLA: Steering Frozen VLAs into Reliable Manipulation Primitives via Memory-Guided Agents** · [arXiv:2607.08448](https://arxiv.org/abs/2607.08448) · `arXiv 2026` · `L2` `🧊frozen` — 冻结 VLA + 固定原语库（部署期不扩）；Task/Global Memory 存成功轨迹、成功规则与失败模型。LIBERO-Pro 82.4%。
- **EmbodiSkill: Skill-Aware Reflection for Self-Evolving Embodied Agents** · [arXiv:2605.10332](https://arxiv.org/abs/2605.10332) · `arXiv 2026` · `L2` `🧪sim` `📂open` — 把轨迹分四类→对**文本** procedural skill 的 body/appendix 做定向编辑；不合成新可执行技能。ALFWorld 93.28%。
- **ABot-AgentOS: A General Robotic Agent OS with Lifelong Multi-modal Memory** · [arXiv:2607.10350](https://arxiv.org/abs/2607.10350) · `arXiv 2026` · `L2`（边界样本）`🤖real` — failure-driven loop 把诊断出的记忆失败转成**声明式 JSON-DSL** evo-asset，经 split-wise held-out 闸控晋升；明确**不执行生成代码**，只改内容管线。
- **ABot-Claw: Persistent, Cooperative, and Self-Evolving Robotic Agents** · [arXiv:2604.10096](https://arxiv.org/abs/2604.10096) · `arXiv 2026` · `L2` `🤖real` `📂open` — 能力驱动多机调度 + 跨本体多模态记忆 + critic 反馈。
- **ME-Brain-1.0: Memory, Cognition and Action for Evolving Embodied Intelligence** · [arXiv:2609.24271](https://arxiv.org/abs/2609.24271) · `arXiv 2026` · `L2` `🤖real` — 经验获取 + 分层记忆巩固 + 技能抽象，不重训。
- **SafeMem: Safe Task Planning with Long-Term Graph Memory** · [arXiv:2609.08444](https://arxiv.org/abs/2609.08444) · `CoRL 2026` · `L2` `🤖real` — 增量语义图记忆 + LLM 风险预测触发保守重规划。
- **BATON: Long-Horizon Manipulation via Agentic Subtask Exploration & Transition-aware Memory** · [arXiv:2608.16889](https://arxiv.org/abs/2608.16889) · `arXiv 2026` · `L2` `🧪sim` — 冻结 VLA，把可复用子任务解存入语言记忆；无参数更新。

### 权重型 L2（改权重，但不新增可点名的新可执行动作）

- **Self-Improving Embodied Foundation Models** · [arXiv:2509.15155](https://arxiv.org/abs/2509.15155) · `arXiv 2025` · `L2` `🤖real` `⚙️weights` — 两阶段自产奖励（Steps-to-Go）+ 成功检测，机群自练并更新策略权重。
- **π*0.6 (RECAP): a VLA That Learns From Experience** · [arXiv:2511.14759](https://arxiv.org/abs/2511.14759) · `arXiv 2025` · `L2` `🤖real` `⚙️weights` — 优势条件化地从真实部署经验 + 人工纠正改 VLA 权重。
- **RoboCat: A Self-Improving Generalist Agent for Robotic Manipulation** · [arXiv:2306.11706](https://arxiv.org/abs/2306.11706) · `TMLR 2024` · `L2` `🤖real` `⚙️weights` — 自产练习轨迹并入下一轮通才训练。
- **VLAW: Iterative Co-Improvement of VLA Policy and World Model** · [arXiv:2602.12063](https://arxiv.org/abs/2602.12063) · `arXiv 2026` · `L2` `🤖real` `⚙️weights` — 交替改进世界模型与策略（均权重级）。
- **MEDAL++: Self-Improving Robots via End-to-End Autonomous Visuomotor RL** · [arXiv:2303.01488](https://arxiv.org/abs/2303.01488) · `CoRL 2023` · `L2` `🤖real` `⚙️weights` — 学任务 + 重置行为，经权重级 RL 自主练习。
- **LiReN: Lifelong Autonomous Improvement of Navigation Foundation Models in the Wild** · [OpenReview](https://openreview.net/forum?id=vBj5oC60Lk) · `CoRL 2024` · `L2` `🤖real` `⚙️weights` `📂open` — 导航基模部署后从在线经验微调。

---

## L3 — Agent 主导的能力扩张（新增一个之前做不出的可执行动作）

> 自我改进**往系统里加了至少一个之前执行不出来的可执行单元**（新技能/新抓取合成/新放置/新运动原语/新计算图节点/新符号谓词）。多数保持底层策略冻结。**当前 physical AI 的真实前沿。**

- **ASPIRE: Agentic Skills Discovery for Robotics**（NVIDIA GEAR）· [arXiv:2607.00272](https://arxiv.org/abs/2607.00272) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — 从 per-primitive trace 诊断→写/修 code-as-policy→蒸馏成**新可复用技能**入库（如 Multi-Angle Approach）；LIBERO-90 → LIBERO-Pro Long **zero-shot 31% vs 4%**。
- **Zetta: Closed-Loop Embodied Harness for Self-Evolving Physical Intelligence** · [arXiv:2608.16590](https://arxiv.org/abs/2608.16590) · `arXiv 2026` · `L3`（含 L2 调度）`🧪sim` `🧊frozen` `📂open` — 在线演化 code critic/recovery/tool；合成 **GraspGen 重抓 / CAP 稳定放置 / 阻抗控制**（"beyond the base VLA's capabilities"）；LIBERO-Pro 34.5%→90.8%，11.1× 加速。
- **SHAPER: Self-Evolving Embodied Agents via Skill-Harness Evolution** · [arXiv:2608.11350](https://arxiv.org/abs/2608.11350) · `arXiv 2026` · `L3` `🧪sim` `🧊frozen` — train-free 演化可复用技能与 context-code harness。
- **RoboHarness: Memory-Driven Orchestration of Heterogeneous Robot Policies**（华为诺亚）· [arXiv:2607.18060](https://arxiv.org/abs/2607.18060) · `arXiv 2026` · `L3`（变体）`🤖real` `⚙️partial weights` — PDDLLM 学**新符号谓词** + Memory-Bridge 合成**衔接动作**；SIMPACT 另调底层 grasp 位姿。LIBERO-Plus 91.9%。
- **GaP: Graph-as-Policy Multi-Agent Self-Learning Harness** · [arXiv:2607.05369](https://arxiv.org/abs/2607.05369) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — 从模块化技能库生成**新有向计算图**（感知/规划/控制节点）；仿真自改进后上真机跑图。
- **RoboFoundry: System-as-Policy Evolution for Self-Learning Embodied Agents** · [arXiv:2609.32862](https://arxiv.org/abs/2609.32862) · `arXiv 2026` · `L3`（含 L2）`🤖real` `🧊frozen` — hierarchical skill 面新增原子技能/组合（`pick_and_place_sim_object`）；能力条件化 held-out 晋升。EmbodiedBench 把 GPT-5.5 提升 27.8%。
- **RATs: Playful Agentic Robot Learning** · [arXiv:2606.19419](https://arxiv.org/abs/2606.19419) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — 自导玩耍提任务→执行诊断 code policy→蒸馏成**持久技能库**，迁移到下游真机任务。
- **RoboSkill: A Skill Acquisition and Reuse Loop for Embodied Agents** · [arXiv:2609.37810](https://arxiv.org/abs/2609.37810) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` — Explore-Execute-Evolve 循环**演化技能库**；LIBERO-10 首回合 +12.5~25pt。
- **CaP-X: Benchmarking and Improving Coding Agents for Robot Manipulation** · [arXiv:2603.22435](https://arxiv.org/abs/2603.22435) · `arXiv 2026` · `L3`（CaP-RL 变体动权重）`🤖real` `📂open` — CaP-Agent0 用执行反馈**合成新技能**；CaP-RL 另有权重级更新。
- **HarnessPAI: An Evolving Harness for Physical AI** · [arXiv:2609.29166](https://arxiv.org/abs/2609.29166) · `arXiv 2026` · `L3` `🧪sim` `🧊frozen` — 从执行反馈修订**可执行任务程序**并留存失败修复知识；LIBERO-PRO +61.6pt（vs pi0.5）。
- **AdaHVLA: Adaptive Harnesses for Long-Horizon VLA Execution** · [arXiv:2609.29204](https://arxiv.org/abs/2609.29204) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` — 多 agent 做**代码级 harness 修订**，保留 hypothesis-revision-effect 图。
- **ETA / OpenETA: A New Agentic Paradigm for Embodied Tasks** · [arXiv:2608.03924](https://arxiv.org/abs/2608.03924) · `arXiv 2026` · `L3` `🤖real` `🧊frozen` `📂open` — Planner-Interface-World 环把交互转成**可复用技能/经验**。
- **Skill-Space Shooting for Autonomous Robot Policy Improvement** · [arXiv:2609.38178](https://arxiv.org/abs/2609.38178) · `arXiv 2026` · `L3` `🤖real` — 把纠正动作探索为**可复用短技能**并转成策略训练信号，跨任务共享。
- **SEES: Self-Evolving Embodied System via Failure-Guided VLA Policy Adaptation** · [arXiv:2609.32698](https://arxiv.org/abs/2609.32698) · `arXiv 2026` · `L3`（偏权重）`🧪sim` `⚙️weights` — 对重复失败的原子技能在仿真重建→在线 RL 更新共享 VLA adapter。
- **RoboClaw: Agentic Framework for Scalable Long-Horizon Robotic Tasks** · [arXiv:2603.11558](https://arxiv.org/abs/2603.11558) · `arXiv 2026` · `L3`（偏权重）`🤖real` `📂open` — 正逆配对自重置采集 + 真机上迭代策略精炼。
- **LRLL: Lifelong Robot Library Learning** · [arXiv:2406.18746](https://arxiv.org/abs/2406.18746) · `ICRA 2024` · `L3` `🤖real` `🧊frozen` — 提任务→存经验→蒸馏成**可复用策略/技能**（无梯度；经 LLM 编码生成新技能）。
- **Voyager: An Open-Ended Embodied Agent with LLMs**（Minecraft）· [arXiv:2305.16291](https://arxiv.org/abs/2305.16291) · `TMLR 2024` · `L3` `🧪sim` `🧊frozen` `📂open` — 自动课程 + 不断增长的可执行代码技能库 + 迭代自我验证（具身数字世界的奠基工作）。

---

## L4 — RSI（改进"产生改进的机制"本身）

> 系统不仅改进自身能力，还**改进产生这些改进的那套诊断/验证/晋升机制本身**。**physical AI 仅被最弱触及，尚无成熟实例。**

- **PhysEvo: Astra Can Act, Let It** · [arXiv:2610.08995](https://arxiv.org/abs/2610.08995) · `arXiv 2026` · **`L3` + 首个触及 `L4` 下沿（physical）** · `🤖real` `🧊frozen` — 单一冻结模型兼 task-agent 与 meta-agent 两角色。L3：关节级控制 / 主动+回溯观察工具 / 可复用技能。**L4 要害**：meta-agent **改进并复用自己的诊断工具**（"inherits a way to improve, not only a way to act"）。**仍是最弱实例**：Revise→Test→Select 元流程骨架固定，改的是诊断工具而非选择逻辑。RoboDojo 62% SR；真机 84% SR。

### 逼近 L4 的苗头（自称"迈向 RSI"，机制上仍是 L3 强化版）

- **ENPIRE: Agentic Robot Policy Self-Improvement in the Real World** · [arXiv:2606.19980](https://arxiv.org/abs/2606.19980) · `CoRL 2026` · `L3→L4 苗头` `🤖real` — 自动重置/验证/rollout + 演化训练基础设施与算法代码（跨机群）。
- **You Don't Need To Stay in The Loop (AgenticRobotics)** · [arXiv:2608.07555](https://arxiv.org/abs/2608.07555) · `arXiv 2026` · `L3→L4 苗头` `🧪sim` — 把 train-evaluate-improve 做成证据门控、可审计晋升的事务。
- **RegenHarness: Robot Agent Harness with Evidence-Gated Recursive Self-Improvement** · [arXiv:2609.27612](https://arxiv.org/abs/2609.27612) · `arXiv 2026` · `L3→L4 苗头` `🤖real` — 修订 task template/routing/recovery 代码；自称 recursive 但未证"改进改进"这一步。
- **EmbodiedRSI: Active Continual Robot Learning via Hypothesis-Guided Co-Evolution** · [arXiv:2610.10498](https://arxiv.org/abs/2610.10498) · `arXiv 2026` · `L3→L4 苗头` `🤖real` — 自主决定下一步探索，把物理交互转成更好的代码/技能。
- **RPG: Reconstruct, Practice, Go Real — Guided Self-Improvement** · [arXiv:2610.02204](https://arxiv.org/abs/2610.02204) · `arXiv 2026` · `L3→L4 苗头` `🤖real` — 无权重更新自改；develop 新 symbolic skills + refine + 改 system prompt；22 任务 28.6%→95.0%。

### 软件域 L4 对照（非 physical AI，仅供参照）

- **Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents** · [arXiv:2505.22954](https://arxiv.org/abs/2505.22954) · `arXiv 2025` · `L4（软件/编码域）` `📂open` — 自改自身代码并改进"改代码的能力"；SWE-bench 20%→50%。
- **Hyperagents** · [arXiv:2603.19461](https://arxiv.org/abs/2603.19461) · `arXiv 2026` · `L4（仿真/软件域）` `🧪sim` `📂open` — task agent + **可编辑 meta agent**，让产生未来修改的机制自身演化；机器人证据仅为仿真奖励设计。

---

## 🧪 Benchmarks & Datasets

- **EmbodiedMemory-Bench** · [arXiv:2609.28236](https://arxiv.org/abs/2609.28236) `📂open` — 测早期观测/交互构建的记忆是否支撑后续动作（2,554 episodes）。
- **EmbodiedGovBench** · [arXiv:2604.11174](https://arxiv.org/abs/2604.11174) — 治理向评测：能力边界、运行时漂移、恢复、升级安全、人工接管、审计完整性。
- **RoboDojo / LIBERO-Pro / RoboCasa / EmbodiedBench / RMBench** — 上述多篇工作的评测场（见各条目）。

## 📚 Surveys

- **Self-Evolving AI for Humanoids: Mechanisms, Safety, and Evaluation of Post-Deployment Self-Improvement** · [arXiv:2609.13236](https://arxiv.org/abs/2609.13236) — 人形部署后自进化综述：policy/perception/memory/workflow/body 五维，自学习→自适应→自优化→自生成四机制。
- **The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement** · [arXiv:2609.11873](https://arxiv.org/abs/2609.11873) — 跨科学/具身/软件的 RSI 路线图，强调评估与人类控制。
- **Self-evolving Embodied AI** · [arXiv:2602.04411](https://arxiv.org/abs/2602.04411) — 记忆更新/任务切换/环境预测/本体适应/模型演化。
- **A Comprehensive Survey of Self-Evolving AI Agents** · [arXiv:2508.07407](https://arxiv.org/abs/2508.07407) — 软件侧自进化全景（对照用）。

## 🔗 相关清单

- [`cocacola-lab/awesome-embodied-rsi`](https://github.com/cocacola-lab/awesome-embodied-rsi) — 按 L0–L4、按改进对象组织的精选清单。

---

## 本仓库内容

- [`CLASSIFICATION.md`](./CLASSIFICATION.md) — **逐篇精读每篇工作后推导**出的 L1–L4 判级，边界 / 偏权重 / 苗头样本逐一给出判定理由。
- [`GRADING.md`](./GRADING.md) — 判级方法论：L1–L4 判据的完整定义、决策流程、以及若干工作的全文精读机制卡。
- [`PAPERS.md`](./PAPERS.md) — 逐篇详表：输入 / 演化对象 / 新增可执行单元 / 验证严格度 / 是否动底模 / 判级+理由 / 核验程度。
- [`references.bib`](./references.bib) — 全部条目的 BibTeX。
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) — 收录标准与条目格式。

## 贡献

欢迎补充。每条新工作须：核到一手出处（arXiv / 会议）；按本清单判据标注级别并写明"新增的可执行单元（或无）"；附副轴标签。详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 维护者

由 **薄紫彤（Zitong Bo）** 维护。

- 个人主页：[zitongbo.github.io](https://zitongbo.github.io/)
- 小红书：[主页](https://www.xiaohongshu.com/user/profile/59dc1d56db2e601ae168a5bb)
- 知乎：[主页](https://www.zhihu.com/people/qian-chang-22-46/posts)

## License

[MIT](./LICENSE)。清单中论文版权归各自作者所有。
