# Strategy Model

> **Runtime entry point:** `SKILL.md` §5. This file provides extended definitions and examples.

The core analytical framework for evaluating any candidate strategy. These six dimensions replace static pros/cons lists with a dynamic risk-structure analysis.

---

## 1. Strategy Fragility

**Definition:** How many external conditions must remain true for the strategy to succeed?

### Fragility Indicators

A strategy is **High Fragility** when it depends on:

- Others not asking questions
- Others not discovering a specific fact
- Multiple stakeholders simultaneously cooperating
- Exact timing with no buffer
- No unexpected events occurring
- Continuous supplementary explanations
- No easy exit path

### Rating

| Level | Meaning |
|-------|---------|
| **Low** | Strategy works under most reasonable scenarios. Few dependencies. |
| **Medium** | Some conditions must hold. A single common event could cause problems. |
| **High** | Multiple brittle conditions. One routine disruption breaks the plan. |

### Key Insight

Fragility is about **dependency count and dependency sensitivity**, not probability. A strategy with one fragile dependency that is almost certain to break may be worse than one with three dependencies that are each very stable.

Do **not** assign numeric scores (e.g., "73.6% fragile"). Explain **why** in plain language.

---

## 2. Exposure Surface

**Definition:** What real-world events could expose, interrupt, or invalidate the plan?

### Common Exposure Points

- Unexpected contact (call, message, visit)
- Ad-hoc task or requirement
- Third party being asked a question
- Schedule conflict
- Record or log mismatch
- Safety inspection or audit
- On-site requirement
- Policy change
- System notification or alert
- Accident or external incident

### Analysis Focus

Don't just count exposure points. Identify:

> **Which single exposure point, if triggered, causes the most damage?**

One high-impact exposure point can outweigh five low-impact ones.

### Interaction with Fragility

Exposure Surface × Fragility = operational risk. A strategy with wide exposure and high fragility is the most dangerous combination.

---

## 3. Recovery Cost

**Definition:** If the strategy fails mid-execution, what must the user pay to return to a normal state?

### Cost Categories

| Category | Examples |
|----------|----------|
| **Money** | Fines, fees, lost deposits, rebooking costs |
| **Time** | Rework, travel back, restarting processes |
| **Relationship** | Lost trust, damaged reputation, awkwardness |
| **Process** | Re-approval, re-application, re-scheduling |
| **Psychological** | Stress, guilt, regret, cognitive load |
| **Opportunity** | Lost alternatives, missed windows |

### Critical Insight

> A strategy can have **low failure probability** but **extremely high Recovery Cost**, making it a bad bet.

Don't only look at "how likely is failure." Also ask: "If it fails, how bad is it?"

---

## 4. Reversibility

**Definition:** Once executed, can the user undo the strategy or switch to another?

| Level | Meaning |
|-------|---------|
| **High** | Can easily undo or switch. Low switching cost. |
| **Medium** | Can undo, but with meaningful cost (money, time, awkwardness). |
| **Low** | Once done, very hard to reverse. |

### Option Value

In high-uncertainty situations, prefer strategies that **preserve future flexibility**. This is not about being conservative — it's about keeping options open until key unknowns resolve.

But do **not** mechanically always recommend the most reversible option. Sometimes the irreversible option has genuinely higher upside that justifies the commitment.

---

## 5. Upside / Downside Asymmetry

**Definition:** Are the potential gains and losses symmetric, or is one side disproportionately large?

### Red-Flag Pattern

```text
Best case:  Gain X (small, capped)
Worst case: Lose Y (large, uncapped, compounding)
```

This is a **negative asymmetry** — the strategy's risk-reward ratio may be poor even if the failure probability is low.

### Green-Flag Pattern

```text
Best case:  Gain X (large, lasting)
Worst case: Lose Y (small, contained, recoverable)
```

### Analysis Approach

Don't just say "risk is high so don't do it." Instead:

> "The extra gain from the risky option is [X]. The potential downside is [Y]. The question is whether X is worth bearing the risk of Y."

Sometimes it is. The skill's job is to make the tradeoff explicit, not to always recommend the safer path.

---

## 6. Narrative Debt

**Definition:** Does the strategy require the user to maintain increasingly complex explanations over time to keep information consistent?

### How Narrative Debt Accumulates

```text
Step 1: Conceal or misrepresent fact A
Step 2: To maintain A, must explain away situation B
Step 3: Third party inquires → need new explanation C
Step 4: Original timeline doesn't match C → need adjustment D
...
```

Each layer adds fragility. The strategy becomes harder to maintain, not easier.

### Relationship to Fragility

Narrative Debt is a **driver** of Strategy Fragility. High Narrative Debt → High Fragility.

### Safety Boundary

**CAN analyze:**
- Why a strategy based on incomplete disclosure is becoming fragile
- The real accumulated cost of maintaining inconsistency
- Truthful alternatives that reduce or eliminate Narrative Debt

**CANNOT:**
- Help design more sophisticated deception
- Optimize cover stories
- Make deception harder to detect
- Help fabricate evidence or timelines

The correct approach is always: **find a truthful strategy that reduces Narrative Debt.**
