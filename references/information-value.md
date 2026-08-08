# Value of Information

How to decide which questions are worth asking — and which are not.

---

## Core Principle

> **Ask the question whose answer is most likely to change the recommendation.**

Every question costs the user attention and time. The skill should ask few questions, but each one should have high decision impact.

---

## VOI Ranking

Rank potential questions by how much their answer could alter the analysis:

| Priority | Question Type | Example |
|----------|--------------|---------|
| **1 (highest)** | Can invalidate a strategy entirely | "Is there a hard deadline you'd miss?" |
| **2** | Can significantly change gain/loss | "How much does rebooking cost?" |
| **3** | Can change reversibility | "Can you undo this decision later?" |
| **4** | Can change stakeholder behavior | "Will they be asked about this directly?" |
| **5 (lowest)** | Adds context but won't change recommendation | "How do you feel about this person generally?" |

---

## The 50-Yuan Test

A practical example of VOI in action:

**Scenario:** User wants to leave early without informing their advisor, gaining 3 extra free days.

**Low-VOI question:** "What's your advisor's personality like?"
- The answer adds color but is unlikely to flip the recommendation.

**High-VOI question:** "How much would it cost to reschedule to the official leave date?"
- If the answer is 50 yuan, the **entire risk-reward calculus shifts**: the switching cost is near-zero, so bearing multiple high-impact uncertainties becomes a much worse trade.

---

## How Many Questions to Ask

**Default: 1–3 per round.**

Never present the user with a list of 10+ questions. That's interrogation, not strategy assistance.

If you genuinely need more information, ask the highest-VOI questions first, then re-evaluate before asking more.

---

## When NOT to Ask

Skip further questions when:

1. **The user has already given enough to make a clear recommendation.**
2. **The remaining unknowns won't change the recommendation** — they affect details but not the core decision.
3. **The user explicitly wants to move forward** with what they have.
4. **The question itself would create risk** (e.g., asking for information the user shouldn't disclose).

---

## VOI in Dynamic Updating

After each new fact from the user, re-rank the remaining unknowns. The highest-VOI question may change as the decision state evolves.
