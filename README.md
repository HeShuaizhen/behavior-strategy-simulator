# Behavior Strategy Simulator

**行为策略推演 v0.2.0**

> Don't just choose. Simulate what happens next.
>
> 不只是选择。推演接下来会发生什么。

> ⚠️ **Experimental / early-stage.** This is a Skill methodology package, not a production decision engine. It is under active development and validation. Use as a thinking framework; do not rely on it for critical, irreversible, or high-stakes decisions without independent judgment.

---

## What Is This?

Behavior Strategy Simulator is a **Skill** for AI agents (Claude Code, ChatGPT, Codex, etc.) that transforms real-world decision-making from static option-scoring into **dynamic strategy simulation**.

Most AI decision assistants answer:

> "Which option is better?"

This Skill answers:

> **"If I do this, what happens next?"**

It models the chain reaction: your action → state change → stakeholder reaction → new constraints → next decision → success, failure, or recovery.

---

## How Is This Different?

| | Traditional AI Decision Assistant | Behavior Strategy Simulator |
|---|---|---|
| **Core question** | Which option is better? | What happens next if I act? |
| **Method** | List A pros/cons, B pros/cons, score | Simulate action → reaction → new state |
| **Output** | Recommendation with scores | Event chain, fragility map, recovery paths |
| **Risk model** | "Risk: High / Medium / Low" | Fragility, Exposure Surface, Recovery Cost, Reversibility |
| **People** | Treated as static factors | Modeled as stakeholders with incentives and triggers |
| **New information** | Appended to existing analysis | Re-evaluates entire state; recommendation can flip |
| **Numeric scores** | Common ("73.6%") | Explicitly avoided |
| **Deception** | May optimize it if asked | Analyzes fragility of deception; refuses to optimize it |

---

## What Problems Is It Best For?

- **Strategies involving other people** — when someone else's reaction determines the outcome
- **Timing decisions** — when *when* you act matters as much as *what* you do
- **Information-asymmetry situations** — when different people know different things
- **High-uncertainty choices** — when you can't know key facts before deciding
- **Irreversible commitments** — when you can't easily undo the choice
- **Post-decision regret** — when you've already chosen and are second-guessing
- **Communication strategy** — when *how* you say something affects the outcome

## What Problems Is It NOT For?

- Simple factual questions ("What's the best restaurant?")
- Purely technical decisions ("Which database should I use?")
- Decisions with no interpersonal or strategic dimension
- Emergency situations requiring immediate action without analysis
- Situations where the user needs therapy, not strategy

---

## Directory Structure

```
behavior-strategy-simulator/
├── SKILL.md                       # Core entry point — load this into your agent
├── README.md                      # This file
├── references/                    # Detailed methodology (loaded on demand)
│   ├── strategy-model.md          # Fragility, Exposure, Recovery, Reversibility, Asymmetry, Narrative Debt
│   ├── information-value.md       # How to decide which questions to ask
│   ├── decision-profile.md        # User decision patterns, Trait vs State
│   ├── regret-and-commitment.md   # Handling regret, Commitment Rules
│   └── safety-boundaries.md       # What the Skill can and cannot do
├── templates/                     # Structured internal templates
│   ├── decision-state.yaml        # Full decision state structure
│   └── strategy-analysis.yaml     # Single strategy evaluation structure
├── examples/                      # Worked examples (Golden Cases)
│   ├── leave-request.md           # Case 1: Leave timing strategy
│   ├── job-offer.md               # Case 2: Job offer comparison
│   └── interpersonal-conflict.md  # Case 3: Confrontation timing
└── tests/                         # Validation
    ├── golden-cases.md            # Test specifications for each case
    └── acceptance-criteria.md     # v0.2 acceptance checklist
```

---

## How to Use

### In Claude Code

Add to your CLAUDE.md or load as a Skill:

```markdown
## Skills
- behavior-strategy-simulator/SKILL.md
```

Or copy the entire directory into your project and reference SKILL.md.

### In Other Agents (ChatGPT, Codex, etc.)

Copy SKILL.md content into your custom instructions / system prompt. Reference files can be loaded as needed or inlined.

### As a Thinking Framework

You can also use the methodology directly — the concepts (Fragility, Exposure Surface, Narrative Debt, VOI, etc.) work as a mental model even without tool integration.

---

## How to Verify It Works

Run through the three Golden Cases in `examples/` and check behavior against `tests/golden-cases.md`.

Key verification: `tests/acceptance-criteria.md` defines 15 acceptance criteria (A through O) that must all be met.

---

## Current Version Boundaries (v0.2)

**This is a Skill, not an application.** It has:

- ✅ Core strategy simulation methodology
- ✅ Modular reference files
- ✅ Structured internal templates
- ✅ Three Golden Cases with test specifications
- ✅ Explicit acceptance criteria
- ✅ Safety boundaries

**It does NOT have (by design):**

- ❌ Runtime code (Python, JS, etc.)
- ❌ Database or persistence
- ❌ Web UI or API
- ❌ Multi-agent system
- ❌ User authentication
- ❌ Decision history tracking across sessions
- ❌ Automated testing harness

---

## Roadmap

### v0.2 (current)
- Modular Skill package
- Core methodology documented
- Three Golden Cases
- Acceptance criteria defined

### v0.3 (planned)
- Additional examples covering more decision domains
- Refined templates based on usage feedback
- Decision Profile accumulation method refinement
- More detailed anti-pattern documentation

### v1.0 (future)
- Host-specific integration guides (Claude Code, ChatGPT, Codex)
- Empirical validation against real decision outcomes
- Optional lightweight memory mechanism for cross-session Decision Profile

### Out of Scope (explicitly)
- Becoming a SaaS product
- Adding a database
- Building a web dashboard
- Turning into a full "Decision Runtime"
- Adding multi-agent orchestration
