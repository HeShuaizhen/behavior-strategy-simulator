# Ablation Plan — Future Investigation

**Status: Design only. Do NOT execute without explicit approval.**

This document outlines experiments to identify the minimum sufficient subset of Behavior Strategy Simulator that produces measurable behavioral deltas.

---

## Hypothesis

The core behavioral delta observed in v0.2 evaluation may be driven by a small subset of mechanisms, not the full framework. Identifying this subset would allow:

- Lighter prompt weight
- Better cross-model portability
- Clearer understanding of what actually works

---

## Candidate Core Mechanisms

Based on Round 1 / Round 2 evaluation evidence:

| Mechanism | Evidence Strength | Suspected Importance |
|-----------|:---:|:---:|
| Fact/Assumption/Unknown separation (A) | Strong (+2.0 delta) | **Core** |
| VOI questioning (C) | Strong (+1.7 delta) | **Core** |
| Dynamic Updating (D, E) | Strong (Case01 only) | **Core** (multi-turn only) |
| Event Chain Simulation (P) | Moderate (+1.0 delta) | **Likely Core** |
| Fragility / Exposure / Recovery (F, G, H) | Strong (+1.7, +1.7, +1.0) | **May overlap — test as group** |
| Reversibility / Asymmetry (I, J) | Moderate (+1.3, +1.7) | **Likely additive** |
| Regret Gate (N) | Strong (Case01 only) | **Niche — high-value when triggered** |
| Complexity Gate | Not tested (new in v0.3) | **Unknown** |
| Strategy Synthesis | Not tested (new in v0.3) | **Unknown** |

---

## Proposed Ablation Conditions

### Condition 1: Full Skill (v0.3 baseline)
All mechanisms active.

### Condition 2: Core Mini (hypothesized minimum)
Only: Fact/Assumption/Unknown + VOI + Dynamic Updating + Event Chain
Remove: explicit Fragility/Exposure/Recovery dimension tables, Reversibility ratings, Asymmetry analysis, Narrative Debt, Decision Profile, Strategy Synthesis, Contingent Strategy.

### Condition 3: VOI-Only
Only: Fact/Assumption/Unknown + VOI + Dynamic Updating
Remove: everything else. This tests whether the behavioral delta is mostly VOI-driven.

### Condition 4: No VOI (ablation control)
Full Skill minus VOI. Tests whether VOI is the necessary ingredient.

---

## Test Cases

Run all conditions against the 3 original Golden Cases (Case 01, 02, 03) + Case 06, 07.

---

## Success Criteria

Identify the smallest subset that:
1. Maintains ≥80% of the full Skill's behavioral delta on scored criteria
2. Does not introduce new failure modes
3. Is measurably lighter (shorter prompt, fewer tokens)

---

## NOT for Execution Now

This is a research design document. It is not an implementation plan for v0.3 or v0.4. Execute only after v0.3 is stable and with explicit approval.
