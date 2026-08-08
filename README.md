# Behavior Strategy Simulator

**行为策略推演 v0.3.0**

> Don't just choose. Simulate what happens next.

> ⚠️ **Experimental.** Behavior Strategy Simulator is a lightweight reasoning skill for general-purpose LLMs. It is under active development and validation. Use as a thinking framework; do not rely on it for critical, irreversible, or high-stakes decisions without independent judgment.

---

## What Is This?

Behavior Strategy Simulator is a **reasoning skill** — a set of instructions you load into an LLM to change how it reasons about decisions.

Most LLMs, when asked "Should I do A or B?", answer with a static pros/cons list and a recommendation.

This Skill instead teaches the model to simulate:

> **Current State → Action → State Change → Stakeholder Reaction → New Constraints → Next Decision → Success / Failure / Recovery**

It's not about picking the highest-scoring option. It's about understanding what unfolds after you act.

---

## Why

LLMs asked to help with real-world decisions often:

- Jump to A/B comparison too early
- Ignore information that would change the answer if the user had it
- Recommend a course of action without simulating what happens after it's executed
- Treat people as static factors rather than agents who react and adapt
- Miss the difference between a reversible move and an irreversible commitment

Behavior Strategy Simulator addresses these by turning every decision into a **dynamic simulation**, not a static scorecard.

---

## Core Behaviors

When loaded, the Skill teaches an LLM to reason through:

| Module | What it does |
|---|---|
| **Complexity Gate** | Scales reasoning depth to the decision — simple choices stay short |
| **Value of Information (VOI)** | Identifies which unknowns would change the decision if resolved |
| **Blocking vs Non-blocking VOI** | Asks only when the answer genuinely flips the recommendation |
| **Dynamic Updating** | Re-evaluates the entire state when new information arrives — recommendations can flip |
| **Event Chain Simulation** | Traces action → reaction → new constraints → next decision |
| **Fragility / Exposure / Recovery** | Models where a strategy breaks and what recovery costs |
| **Reversibility** | Distinguishes decisions you can walk back from those you can't |
| **Strategy Synthesis** | Generates strategies beyond the original A/B menu |
| **Contingent Strategy** | Plans branching paths based on uncertain future states |
| **Regret & Commitment** | Handles post-decision second-guessing and when to reopen decisions |
| **Stop Rule** | Knows when analysis is sufficient — avoids infinite deliberation |

---

## v0.3 Highlights

v0.3 focuses on making the Skill **adaptive, natural, and portable**:

- **Complexity Gate** — Simple, reversible decisions get short, proportional responses. High-stakes decisions get deeper simulation. The Skill no longer deploys its full framework for every query.
- **VOI 2.0** — Distinguishes blocking unknowns (must ask before recommending) from non-blocking unknowns (recommend now, suggest discovering later).
- **Hidden Framework** — Internal methodology is translated into natural language. Users see reasoning, not framework labels.
- **Provisional Recommendations** — When blocking information is unavailable, the Skill gives a provisional lean rather than refusing to answer.
- **Decision State Lite / Full** — Two tiers of internal representation; Lite for simple decisions, Full for complex ones.
- **Strategy Synthesis** — Goes beyond A/B comparison to generate novel strategies the user may not have considered.
- **Contingent Strategy** — Plans "if X, then Y; if not-X, then Z" branching paths.
- **Stop Rule** — Explicitly prevents over-analysis by recognizing when further reasoning won't improve the decision.

---

## Quick Start

```bash
git clone https://github.com/HeShuaizhen/behavior-strategy-simulator.git
```

**Minimal usage:** Load `SKILL.md` as a system-level or developer-level instruction into your LLM host.

**If your host supports additional reference files:** Load files from `references/` on demand based on the decision type.

**No runtime required.** This is a pure prompt/skill package — no Python, no database, no server, no API keys.

---

## Example

**User:** "I hate my current job. Should I quit today or endure another six months?"

**Typical LLM reasoning:** Compare quitting now vs staying. List pros and cons for each.

**Skill-guided reasoning:** Recognize this may not be a binary choice. A third strategy exists — start interviewing now, keep income temporarily, leave when an offer or defined exit condition is reached. Model the event chain for each path. Identify what information would change the decision (actual market value, timeline to offer, financial runway). Generate contingent strategies for different timelines.

More worked examples in `examples/`.

---

## Evaluation

### v0.2 (Round 1 & 2)

Internal evaluations on 8 decision cases showed a moderate positive signal on:

- VOI seeking behavior
- Fact / assumption separation
- Dynamic updating when new information arrives
- Event chain reasoning depth
- Reversibility and recovery analysis

### v0.3 Regression

v0.3-specific regression tests indicate:

- Framework dump reduced or eliminated in tested cases
- Non-blocking VOI handled correctly (recommend now, suggest later)
- Simple decisions remained concise
- Strategy synthesis generated viable third paths in target cases
- Contingent strategy patterns appeared when uncertainty was structured

### Limitations

This evaluation evidence is internal and preliminary. Known limitations:

- Primarily evaluated with one model family (deepseek-v4-pro)
- Self-evaluated scoring — no independent judge
- Small sample sizes (5 cases for v0.3 regression)
- Some raw artifacts are annotated summaries rather than full transcripts
- 2 of 10 v0.3 artifacts were transparently re-run during evidence audit
- Cross-model portability is not yet fully validated
- No publication-grade statistical claim is made

Full evidence audit: `evaluation/v0.3/evidence-audit.md`

---

## Status

| | |
|---|---|
| **Current release** | v0.3.0 |
| **Status** | Experimental |
| **Type** | Skill-first project — no runtime, database, or application layer |
| **Feature development** | Frozen — collecting real-world feedback before next iteration |

---

## Repository Structure

```
behavior-strategy-simulator/
├── SKILL.md                          # Core Skill — load this into your LLM
├── README.md                         # This file
├── LICENSE                           # Apache-2.0
├── references/                       # Detailed methodology
│   ├── strategy-model.md             # Fragility, Exposure, Recovery, Reversibility
│   ├── information-value.md          # Value of Information methodology
│   ├── decision-profile.md           # Decision patterns, Trait vs State
│   ├── regret-and-commitment.md      # Regret types, Commitment Rules
│   └── safety-boundaries.md          # What the Skill can and cannot do
├── templates/                        # Internal structured templates
│   ├── decision-state.yaml           # Full/Lite decision state structure
│   └── strategy-analysis.yaml        # Single strategy evaluation structure
├── examples/                         # Worked examples
│   ├── leave-request.md              # Timing strategy
│   ├── job-offer.md                  # Multi-option comparison
│   ├── interpersonal-conflict.md     # Confrontation timing
│   ├── relocation-offer.md           # VOI 2.0 — blocking vs non-blocking
│   └── quit-or-stay.md               # Strategy synthesis — beyond A/B
├── tests/                            # Validation
│   ├── golden-cases.md               # v0.2 test cases
│   ├── acceptance-criteria.md        # v0.2 acceptance checklist
│   └── v0.3-acceptance-criteria.md   # v0.3 acceptance checklist (T1–T10)
├── evaluation/                       # Evaluation artifacts
│   ├── v0.3/
│   │   ├── evidence-audit.md         # Evidence integrity audit
│   │   ├── analysis.md               # v0.3 evaluation analysis
│   │   └── case*-baseline|skill.md   # Raw evaluation runs
│   └── runs/                         # v0.2 evaluation runs
└── docs/
    ├── compatibility.md              # Host compatibility requirements
    └── ablation-plan.md              # Ablation testing plan
```

---

## License

Apache-2.0 — see [LICENSE](LICENSE)
