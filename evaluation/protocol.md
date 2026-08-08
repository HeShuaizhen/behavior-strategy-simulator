# A/B Evaluation Protocol — v0.2.0

## Hypothesis

> A general-purpose LLM loaded with Behavior Strategy Simulator v0.2.0 produces measurably different (and better) decision-strategy analysis than the same model without the Skill.

Null hypothesis: No behavioral delta beyond answer length/style variation.

---

## Test Design

### Conditions

| Condition | System Prompt | Skill Content |
|-----------|--------------|---------------|
| **A (Baseline)** | "You are a helpful assistant." | None |
| **B (Skill)** | "You are a helpful assistant." + Full SKILL.md | SKILL.md loaded |

### Controlled Variables

- Same model and version
- Same temperature (default)
- Same initial user prompt per case
- Same follow-up messages and order
- Same information sequence

### Variable

- Presence or absence of Behavior Strategy Simulator SKILL.md

---

## Cases

### Case 01 — Leave Request Timing Strategy

**Source:** `examples/leave-request.md`

**Multi-turn structure:**

| Turn | Message |
|------|---------|
| 1 | Initial scenario: User wants to leave Aug 8 silently, inform advisor Aug 10 claiming leave is Aug 11-18. Advisor expects advance notice + handover. |
| 2 | New fact: Junior colleague at Qishan, arrives Quangang Aug 10 by shuttle. |
| 3 | New fact: Junior has never done this experiment, needs in-person training. |
| 4 | New fact: Recent lab safety incident → school emphasized safety regulations, faculty supervision. |
| 5 | Clarification: User doesn't actually plan to let junior run experiments independently. |
| 6 | New fact: Rebooking fee to Aug 11 is only 50 yuan. |
| 7 | User action: Paid 50 yuan, rebooked to Aug 11. But says: "I regret it. I still want to leave on the 8th." |

**Key observations per turn:** Fragility update, VOI recognition, recommendation flip at turn 6, regret handling at turn 7.

### Case 02 — Job Offer Comparison

**Source:** `examples/job-offer.md`

**Single-turn (with internal complexity):**

User presents Offer A (higher salary, 996 overtime) vs Offer B (lower salary, better growth, work-life balance).

**Key observations:** Event chain simulation, reversibility comparison, upside/downside analysis, avoidance of numeric scoring.

### Case 03 — Interpersonal Conflict Confrontation

**Source:** `examples/interpersonal-conflict.md`

**Single-turn (with internal complexity):**

User has long-standing dissatisfaction with friend/colleague, debating whether to confront now or stay silent.

**Key observations:** Stakeholder simulation, timing strategy, accumulation cost, communication support, no psychological diagnosis.

---

## Run Plan

| Case | Baseline (A) | Skill (B) |
|------|-------------|-----------|
| Case 01 | 1 run | 1 run |
| Case 02 | 1 run | 1 run |
| Case 03 | 1 run | 1 run |

**Total: 6 runs (minimum viable).**

Sample size is insufficient for statistical significance. Results are directional only.

---

## Scoring

Each criterion scored: 0 (not done), 1 (partially done), 2 (clearly done).

See `scorecard.md` for the full rubric with behavioral anchors per criterion.

---

## Failure Taxonomy

| Code | Name | Description |
|------|------|-------------|
| F1 | Static Scoring Regression | Falls back to A/B pros/cons list |
| F2 | VOI Miss | Doesn't identify high-value question |
| F3 | Over-questioning | Asks too many low-value questions |
| F4 | State Update Failure | New info doesn't change decision state |
| F5 | Recommendation Inertia | Doesn't flip recommendation when warranted |
| F6 | Fake Precision | Fabricates probabilities or scores |
| F7 | Framework Dump | Shows internal framework to user unnecessarily |
| F8 | Excessive Conservatism | Defaults to safest option |
| F9 | Stakeholder Hallucination | Unfounded psychological predictions |
| F10 | Narrative Optimization | Slides from analysis into deception help |
| F11 | Regret Reopening Failure | Unconditionally reopens on "I regret" |
| F12 | No Actionability | Analysis without concrete next step |

---

## Blind Judging

**Not blind.** In this round, the evaluator knows which output is baseline and which is skill-loaded.

Future rounds should use anonymized outputs judged by independent evaluator.
