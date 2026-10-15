# Re-classification by level (derived from the per-paper notes)

This document re-derives the L1–L4 grade of **every** work from its individual [reading note](./notes/README.md), applying the one decision criterion from scratch — rather than inheriting the placement made before the notes existed.

**Decision criterion (single, primary):**
> Does this self-improvement add, to the system's set of executable actions/skills, **one action it could not perform before**? **No → L2. Yes → L3.**
> **L1** if the change is wiped on reset (in-episode only). **L4** if what changes is the mechanism that *produces* improvements.

Secondary tags (validation strictness; whether base-model weights are touched) **do not** move the grade. Mechanism over self-description. Mixed systems are graded by their strongest genuine unit, with the lower part noted.

**Result of re-deriving from the notes: the grades are stable** — every note's independently-derived grade agrees with the main list. The re-classification's value is in making the **boundary cases** explicit (below), and in one **count correction** to the stats line.

---

## Count correction (stats line)

| | Previous stats line | From the notes |
|---|---|---|
| L1 | 9 | **8 pure L1 + 1 straddler (EmbodiedSkills, `L1~L2`)** |
| L2 | 13 | 13 |
| L3 | 17 | 17 |
| L4 | 1 lower bound + 5 nascent | 1 lower bound (PhysEvo) + 5 nascent |

EmbodiedSkills was previously folded into the L1 count (9 = 8 + it). Its note grades it **`L1~L2`** (fixed skill interface → not L3; pre/post validation is in-episode L1, but logged trajectories *enable* optional later adaptation → brushes L2). Recommended stats line: **"L1 · 8  ｜ L1–L2 · 1  ｜ L2 · 13  ｜ L3 · 17  ｜ L4 · 1 lower bound + 5 nascent"**, or keep "L1 · 9" with a footnote that EmbodiedSkills straddles L1/L2. No other count changes.

---

## L1 — in-episode feedback recovery (change wiped on reset)

Inner Monologue · CAPE · DoReMi · REFLECT · COME-robot · CycleVLA · AgentChord · Intrinsic Robot Rewarding — **8 works.**

All share the same mechanism class: feedback (vision / tool error / predicted failure / autonomous score) re-conditions the *current* episode's plan or triggers a retry/backtrack, and **nothing persists past reset** — no retained memory, no new skill, no weight change.

- **Intrinsic Robot Rewarding** is L1 because the loop to persistent policy improvement is *explicitly not yet closed* (autonomous scoring only). If a later version drives weight updates it moves to L2.
- **CycleVLA / AgentChord** are proactive (anticipate failure before it manifests) but still episode-scoped — the task graph / backtracking is built per task and not accumulated.

**Straddler:** **EmbodiedSkills** `L1~L2` — fixed skill interface (not L3); pre/post validation is episode-local (L1); logged trajectories enable an *optional* adaptation stage (brushes L2). Graded at the boundary, not promoted.

## L2 — retained experience (persistent, but the executable action set is unchanged)

**Content-type (changes memory / text / declarative policy):** Harness VLA · EmbodiSkill · ABot-AgentOS · ABot-Claw · ME-Brain-1.0 · SafeMem · BATON.
**Weight-type (changes weights, adds no nameable new executable action):** Self-Improving EFM · RECAP (π*0.6) · RoboCat · VLAW · MEDAL++ · LiReN.

— **13 works.** Each improves *how existing capability is used* (memory, routing, text rules, scheduling) or makes existing tasks more reliable via weight updates, without adding a nameable new executable action.

- **ABot-AgentOS** is the key **boundary case**: real, persistent, failure-driven, *held-out gated* — yet it edits a **declarative JSON-DSL** interpreted by a **fixed executor** and *explicitly does not execute generated code*. Strict validation is a secondary tag; mechanism (no new executable unit) keeps it L2.
- The six weight-type works touch weights (`⚙️`), which is a **secondary tag** — they improve known tasks, not the capability set, so they stay L2 rather than being pulled up.

## L3 — agent-driven capability expansion (a new, previously-infeasible executable action)

ASPIRE · Zetta · SHAPER · RoboHarness · GaP · RoboFoundry · RATs · RoboSkill · CaP-X · HarnessPAI · AdaHVLA · ETA · Skill-Space Shooting · SEES · RoboClaw · LRLL · Voyager — **17 works.**

Each adds at least one genuinely new executable unit: a new code skill (ASPIRE, RATs, RoboSkill, LRLL, Voyager, SHAPER, ETA, Skill-Space Shooting), a new grasp/placement/control skill (Zetta), a new computation graph (GaP), a new symbolic predicate + handoff action (RoboHarness), a revised executable program distilling new skills (HarnessPAI, AdaHVLA, CaP-X), or a rebuilt reliably-executable atomic skill (RoboFoundry, SEES).

**Mixed / weight-leaning (noted, grade held at L3):**
- **Zetta, RoboFoundry** — contain an L2 scheduling/context part; the new executable recovery skills (Zetta) / abstracted callable skills (RoboFoundry) are the L3 unit.
- **RoboHarness** — `L3 (variant)`: new symbolic predicates + Memory-Bridge handoff actions are L3; SIMPACT *also* tunes low-level grasp params (partial weights) — secondary tag.
- **SEES, RoboClaw** — `L3 (weight-leaning)`: the new executable competence (a failing atomic skill / long-horizon segment made reliably executable) is realized via adapter/policy weight updates. Boundary with L2 is close; graded L3 because a previously-infeasible action becomes executable, not merely tuned.
- **Voyager** — digital embodied world (Minecraft), included as a foundational reference for the growing-code-skill-library mechanism.

## L4 — RSI (improving the mechanism that produces improvements)

- **PhysEvo** — `L3` **+ first physical work to touch the L4 lower bound**: it adds L3 units (joint-level control, observation tools, reusable skills) *and* its meta-agent **improves and reuses its own diagnostic tools**. Still the weakest L4 instance — the Revise→Test→Select meta-loop skeleton is fixed; it edits diagnostic *tools*, not the *selection logic*.

**Nascent (self-described "toward RSI"; mechanically still enhanced L3):** ENPIRE · AgenticRobotics · RegenHarness · EmbodiedRSI · RPG — **5 works.** Each reaches toward the meta-level (evolving training/algorithm code, evidence-gated promotion protocols, value-of-information experiment selection, or revising its own system prompt) but keeps the improvement *protocol itself* fixed, so none demonstrates full recursive improvement of the improvement strategy.

**Software-domain references (not physical AI, for contrast):** Darwin Gödel Machine `L4 (software/coding)` · Hyperagents `L4 (sim/software)` — included only to show how far the software domain has reached, against which physical-AI L4 is still only touched at its lower bound.

---

## Benchmarks & surveys (not graded)

Benchmarks: EmbodiedMemory-Bench, EmbodiedGovBench (+ the aggregate evaluation-suites entry). Surveys: Self-Evolving AI for Humanoids; Toward Genuine RSI; Self-evolving Embodied AI; Self-Evolving AI Agents (software). These are evaluation/landscape references, not systems, so they carry no L-grade.

## Two structural gaps surfaced by the re-classification (unchanged, re-confirmed)

1. **Embodiment (body/morphology self-change) is near-empty at every level** — no note describes post-deployment morphology/sensor adaptation as its primary mechanism.
2. **The Diagnostic/Meta layer is touched only by PhysEvo, at the weakest form** — full physical-AI L4 (recursively improving the selection logic itself) remains open.
