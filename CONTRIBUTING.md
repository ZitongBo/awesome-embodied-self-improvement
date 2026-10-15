# Contributing

Contributions of embodied self-improvement works are welcome. To keep the list trustworthy and consistent, each new entry must meet the following.

## Scope

- **Embodied intelligence / robotics / physical AI only:** real-robot or physical/embodied-simulation experiments. Pure software LLM agents are out of scope (a few may appear only as "software-domain references").
- **Must exhibit post-deployment self-improvement:** the system changes itself (policy / memory / skills / harness / diagnostic mechanism) from its own interaction experience. Plain offline training, or VLA/world-model work without self-improvement, is out of scope.

## Grading criterion (single decision)

> After this self-improvement, does the system's set of executable actions/skills gain one action it could not perform before?

- In-episode only, resets to zero → **L1**
- Persistent but **no new executable action** (memory / text / routing / monitoring critic / re-ordering existing primitives / weights with no new action) → **L2**
- Persistent and adds **a previously infeasible executable action/skill** → **L3**
- Changes the **diagnosis / validation / promotion mechanism itself** → **L4**

**Principles:** mechanism over self-description; split mixed L2+L3 systems and grade L3 if any genuine new executable unit appears; mark unverifiable works ⚠️ and do not fabricate.

## Entry format

One line per work, placed under the matching level section, ordered by date or impact:

```
- **<Title>** (<affiliation, optional>) · [arXiv:XXXX.XXXXX](https://arxiv.org/abs/XXXX.XXXXX) · `L?` `🤖real|🧪sim` `🧊frozen|⚙️weights` `📂open` — <one line: what it changes; the new executable unit, or "none">.
```

**Tag legend:** `🤖real` ｜ `🧪sim` ｜ `🧊frozen` ｜ `⚙️weights` ｜ `📂open`.

For finer evidence (input / what evolves / new executable unit / validation strictness / weights touched / grading reason), also add to the table and mechanism cards in [`PAPERS.md`](./PAPERS.md), and add the BibTeX to [`references.bib`](./references.bib).

## Submitting

- Fork → edit `README.md` (required) / `PAPERS.md` / `references.bib` → open a merge request.
- In the MR description, give the grading reason (especially "what the new executable unit is") to aid review.
