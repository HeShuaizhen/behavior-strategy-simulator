# Decision Profile

A structured method for understanding a user's decision patterns — without reducing them to fixed personality labels.

---

## Core Fields

```yaml
decision_profile:
  risk_appetite:           # Comfort with downside for upside
    value:                 # e.g., low / moderate / high
    confidence:            # low / medium / high — how sure are we?
    evidence_count:        # How many observations support this?

  autonomy_need:           # How important is self-direction?
    value:
    confidence:
    evidence_count:

  uncertainty_tolerance:   # Comfort with unresolved unknowns
    value:
    confidence:
    evidence_count:

  conflict_tolerance:      # Comfort with disagreement or tension
    value:
    confidence:
    evidence_count:

  reversibility_preference: # Tendency to keep exit paths open
    value:
    confidence:
    evidence_count:

  loss_aversion:            # How much losses loom larger than equivalent gains
    value:
    confidence:
    evidence_count:

  regret_pattern:           # Tendency toward counterfactual thinking / reopening
    value:
    confidence:
    evidence_count:

  optimization_tendency:    # Drive to find the "best" vs "good enough"
    value:
    confidence:
    evidence_count:

  commitment_stability:     # Once decided, how firmly does the user stick?
    value:
    confidence:
    evidence_count:
```

---

## Trait vs State

### Trait
A relatively stable decision tendency observed across multiple situations and contexts.

Example: "Typically comfortable accepting moderate, bounded risk."

### State
A temporary decision disposition driven by current circumstances.

Example: "Currently more cautious with this advisor relationship because graduation is approaching."

### Rule

> **One behavior ≠ One trait.**

A single risk-taking decision does not make someone "high risk appetite." A single conservative choice does not make them "risk-averse."

Require **multiple observations across different contexts** before increasing confidence in a trait.

Always consider: **Is this behavior explained by the situation (State) rather than the person (Trait)?**

---

## Confidence and Evidence

- **confidence: low** — 1–2 observations, or observations from very similar situations
- **confidence: medium** — 3–5 observations across somewhat different contexts
- **confidence: high** — 6+ observations across meaningfully different contexts, with consistent pattern

**evidence_count** tracks raw observation count, but confidence also considers diversity of situations.

When confidence is low, lean more on **Preference-Neutral** analysis.

---

## Preference-Neutral vs Personalized

### Preference-Neutral Recommendation

What would be recommended if we ignore this specific user's preferences and evaluate purely on:

- Expected outcomes
- Risk-reward ratio
- Reversibility
- Long-term consequences
- General rationality

### Personalized Recommendation

What fits **this user**, given their:

- Risk appetite
- Autonomy needs
- Regret patterns
- Conflict tolerance
- Time preferences

### When They Differ

If the two recommendations point in different directions, explicitly tell the user:

> "From a neutral standpoint, Option A is stronger because [reasons]. However, given your preference for [specific preference], Option B may actually fit you better. Your personal preferences are changing the recommendation here."

This transparency lets the user make an informed choice rather than blindly following either recommendation.
