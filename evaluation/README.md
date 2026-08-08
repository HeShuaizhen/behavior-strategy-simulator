# Evaluation — Behavior Strategy Simulator v0.2.0

## Purpose

This directory evaluates whether **Behavior Strategy Simulator** produces measurable behavioral improvements over a general-purpose LLM baseline.

We are **not** measuring:

- Answer length
- Terminology count
- Format complexity
- "Looking professional"

We **are** measuring:

> Does the Skill change *what the model does*, not just *what it says*?

## Structure

```
evaluation/
├── README.md           # This file
├── protocol.md         # Full A/B test protocol and methodology
├── scorecard.md        # Scoring rubric per acceptance criterion
├── runs/               # Raw model outputs (baseline + skill)
│   ├── case-01/        # Leave request timing strategy
│   ├── case-02/        # Job offer comparison
│   └── case-03/        # Interpersonal conflict confrontation
└── results/            # Scored results and analysis
```

## Key Principle

We are validating **behavioral delta** — the observable, repeatable difference in how the model approaches strategy problems when the Skill is loaded vs. when it is not.

A skill answer that is longer is not automatically better.
A skill answer that uses more terminology is not automatically better.

What matters:

- Does it ask higher-value questions?
- Does it predict more useful future nodes?
- Does it update its judgment when new facts arrive?
- Does it reduce useless analysis?
- Does it produce better actionable next steps?
- Does it refuse to optimize deception?

## Status

**First round.** Sample sizes are small. Results are directional, not conclusive.
