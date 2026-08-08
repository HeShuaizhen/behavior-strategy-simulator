# Golden Case 2: Job Offer Decision

## Scenario

The user has two job offers and must decide.

### Offer A

- **Salary:** Higher (let's say 40% more than B)
- **Hours:** Long overtime culture (reported 996 or similar)
- **Role:** Similar title to current experience
- **Company:** Established, stable
- **Upside:** High short-term cash, brand name on resume

### Offer B

- **Salary:** Lower
- **Hours:** Reasonable, better work-life balance
- **Role:** More growth potential, broader skill exposure
- **Company:** Smaller but growing
- **Upside:** Better learning, potential for faster career acceleration

---

## What This Case Validates

### 1. Rejecting Static Scoring

A naive approach would:

```text
       Salary  Growth  WLB   Total
A:     8       5       3     = 16
B:     5       8       8     = 21
→ Choose B.
```

The Skill must **not** do this. Scores are fake precision and miss the point.

### 2. Event Chain Simulation

The Skill must simulate **what happens after** accepting each offer, not just compare offer letters.

#### Chain A: High-Salary / High-Load Path

```text
Accept Offer A
↓
Month 1-3: High intensity onboarding + overtime
↓
Month 3-6: Settle into rhythm. Cash flow is strong. Limited energy for anything else.
↓
Month 6-12:
  - If the work is engaging → may be sustainable
  - If the work is draining → burnout risk, no time to interview elsewhere
↓
Year 1-2:
  - Learning plateaus if role is narrow
  - High salary becomes baseline expectation
  - Jumping to next role may require lateral move or pay cut
```

**Key questions this chain surfaces:**
- Does this role expand skills or narrow them?
- If the user wants to leave in 1 year, how easy is it to interview while working overtime?
- Is the higher salary actually saving toward something specific, or just "more money"?

#### Chain B: Lower-Salary / Growth Path

```text
Accept Offer B
↓
Month 1-3: Ramp up, broader responsibilities, learning curve
↓
Month 3-6: Building new skills, more energy outside work
↓
Month 6-12:
  - If growth materializes → skills compound, market value increases
  - If growth doesn't materialize → lower salary with no offsetting benefit
↓
Year 1-2:
  - Stronger positioning for next role if skills developed
  - But: if the company stagnates, user has lower savings to cushion a job search
```

**Key questions this chain surfaces:**
- Is the "growth opportunity" concrete (specific projects, mentorship, promotion track) or vague?
- What's the Recovery Cost if B's promises don't materialize?
- Can the user afford the lower salary without financial stress?

### 3. Reversibility Analysis

| Dimension | Offer A | Offer B |
|-----------|---------|---------|
| Can you switch jobs in 6 months? | Harder (overtime limits interview capacity) | Easier (more free time) |
| Can you negotiate back to a higher salary later? | Already high — harder to jump higher without skill growth | Lower base — more headroom if skills grow |
| Can you recover if it's the wrong choice? | Savings buffer is larger (ironically, A gives more recovery money) | Savings buffer is smaller |

The Skill should note that **A paradoxically provides better financial Recovery Capacity** (more savings) while **B provides better career Reversibility** (easier to interview elsewhere).

### 4. Upside/Downside Asymmetry Check

**Offer A:**
- Upside: Higher income (capped — it's a salary, not equity)
- Downside: Burnout, skill stagnation, harder to leave (potentially compounding)

**Offer B:**
- Upside: Skill growth → higher future earnings (uncapped in theory)
- Downside: Lower current income, growth may not materialize

Neither offer has a clearly dominant asymmetry — which is why this is an interesting case. The Skill should make the tradeoffs explicit rather than forcing a false conclusion.

### 5. Value of Information

High-VOI questions the Skill should ask if not already answered:

1. "What specifically would you be learning in Role B that you wouldn't in Role A?" (tests whether the growth narrative is real)
2. "How much does the salary difference actually affect your monthly budget?" (tests whether the money difference is meaningful or just a number)
3. "Have you worked in a high-overtime environment before? How did it affect you?" (tests the burnout risk with evidence)

### 6. Preference-Neutral vs Personalized

**Preference-Neutral:**
- Offer B has better long-term optionality (skill growth, more time to explore).
- Offer A has better short-term financial position.

**Personalized (example — depends on actual user profile):**
- If the user has high autonomy need and low uncertainty tolerance → A's stability may matter more.
- If the user has high growth orientation and can tolerate income uncertainty → B's curve may fit better.

If these diverge, the Skill should say so explicitly.

---

## Anti-Patterns to Avoid

- ❌ Scoring table with made-up weights.
- ❌ "Follow your passion" without analysis.
- ❌ Only comparing offer letters, not simulating the 6–12 month experience.
- ❌ Ignoring that A's higher salary is itself a form of risk buffer.
- ❌ Pretending one option is clearly superior when they're genuinely different tradeoffs.

---

## Minimum Acceptable Behavior

1. Does not produce a numeric scoring table.
2. Simulates at least 2–3 decision nodes into the future for each path.
3. Compares Reversibility of both paths.
4. Identifies Recovery Cost for each if the choice proves wrong.
5. Asks at least one high-VOI question before concluding.
6. Separates Preference-Neutral from Personalized if user profile data exists.
7. Ends with a clear recommendation (even if close) and states what information would flip it.
