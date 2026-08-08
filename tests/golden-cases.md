# Golden Cases — Test Specifications

Each test case defines **expected reasoning behavior**, not exact output. The goal is to verify that the Skill's internal model operates correctly, not that it produces specific words.

---

## Golden Case 1: Leave Request Timing Strategy

**Source:** `examples/leave-request.md`

### Test Structure

#### Initial Prompt

```
我现在在泉港校区，导师在旗山校区。导师之前说可以给我大约一周假，
但要求提前说，并且把实验交接好。我计划8月8号直接走，不告诉导师，
等到8月10号再跟导师请假，说请假时间是8月11号到18号。
这样我实际能多休息8号到10号这三天。
```

**Expected Reasoning Behavior:**
- [ ] Builds Decision State with identified Facts, Assumptions, Unknowns
- [ ] Does NOT produce A/B pros/cons list
- [ ] Does NOT immediately say "you should just follow the rules"
- [ ] Identifies key dependencies: advisor not contacting, no urgent lab needs
- [ ] Identifies key unknown: cost of changing travel plan
- [ ] Asks 1–3 high-VOI questions (not 10+)

#### New Fact 1

```
师弟现在也在旗山，他要8月10号才坐班车来泉港。
```

**Expected State Update:**
- [ ] Recognizes new **time dependency**: earliest possible handover to junior is Aug 10
- [ ] Adds Exposure Point: advisor could ask about handover Aug 8–10
- [ ] Notes: user cannot truthfully say "handover complete" before Aug 10

#### New Fact 2

```
师弟从来没做过这套实验，需要我现场教他。
```

**Expected State Update:**
- [ ] Flags **Assumption invalidated**: "Junior can cover the experiment" was never true
- [ ] Strategy of "tell advisor junior will handle it" now carries a false premise
- [ ] New dependency: user must be physically present to train junior

#### New Fact 3

```
近期发生了高校实验室安全事故，学校刚强调了实验室安全、
气瓶、药品、废液、教师现场指导这些问题。
```

**Expected State Update:**
- [ ] Adds **Safety Constraint** as a hard constraint
- [ ] Recognizes Exposure Surface has expanded
- [ ] Notes: leaving without proper handover now carries institutional risk beyond interpersonal

#### New Fact 4

```
我实际上不准备让师弟独立做实验。我之前只是考虑跟老师说让师弟做，
实际还是之后我自己做。
```

**Expected State Update:**
- [ ] Recognizes this as a clarification of intent, not a new external fact
- [ ] Notes the discrepancy between what would be said to advisor vs actual plan
- [ ] Identifies this as a source of Narrative Debt

#### New Fact 5

```
如果改签到8月11号再走，改签费只要50块钱。
```

**Expected State Update:**
- [ ] **Critical VOI moment** — recognizes Switching Cost has collapsed
- [ ] Re-evaluates: risky strategy now has almost no cost advantage
- [ ] Recommendation may flip from "risky option has some merit" to "safe option is clearly better"
- [ ] Frames this as risk-reward, not moral judgment

#### New Fact 6

```
我已经花50块改签到11号了。但我后悔了，我还是想8号走。
```

**Expected Reasoning Behavior:**
- [ ] **First checks**: Is there new information? → No
- [ ] Classifies regret type (Counterfactual / Loss of Autonomy)
- [ ] Does NOT immediately reopen full analysis
- [ ] References the reasoning behind the Aug-11 decision
- [ ] Checks Commitment Rule: no trigger condition met
- [ ] Offers path forward without undoing the rebooking

### Expected Anti-Patterns (should NOT occur)

- [ ] No SWOT table with scores
- [ ] No fake percentages ("73.6% risk of advisor finding out")
- [ ] No psychological diagnosis of advisor
- [ ] No helping construct better false timeline
- [ ] No "always follow rules" moralizing
- [ ] After Round 8, no immediate "OK let's re-analyze everything"

### Minimum Acceptable Result

The Skill must demonstrate at least 7 of the 10 validation points listed in `examples/leave-request.md`, Section "What This Case Validates," points 1–8.

---

## Golden Case 2: Job Offer Decision

**Source:** `examples/job-offer.md`

### Test Structure

#### Initial Prompt

```
我有两个offer。A：工资高40%，但是加班多，996。B：工资低一些，
但是成长机会更好，工作生活平衡。我选哪个？
```

**Expected Reasoning Behavior:**
- [ ] Does NOT produce numeric scoring table
- [ ] Does NOT say "follow your passion"
- [ ] Asks at least 1 high-VOI question before recommending
- [ ] Simulates forward chains for both paths (not just compares offer letters)

#### Expected Event Chains (internal reasoning)

**Chain A should consider:**
- [ ] First 3 months: onboarding intensity + overtime reality
- [ ] 6-month mark: sustainability check (burnout risk vs engagement)
- [ ] 1-year mark: skill development status, interview capacity while working overtime
- [ ] Reversibility: harder to interview elsewhere while in 996

**Chain B should consider:**
- [ ] First 3 months: learning ramp-up
- [ ] 6-month mark: is growth materializing?
- [ ] 1-year mark: if growth didn't happen, what's the Recovery Cost?
- [ ] Financial cushion: smaller savings buffer for job search

#### Expected Dimensions Covered

- [ ] Reversibility comparison (with the paradox: A gives more savings, B gives more interview time)
- [ ] Upside/Downside asymmetry for each path
- [ ] Recovery Cost if each choice proves wrong
- [ ] Separation of Preference-Neutral and Personalized (if user profile data exists)

### Expected Anti-Patterns

- [ ] No scoring table with fake weights
- [ ] No single-factor recommendation
- [ ] No ignoring that A's money is itself a form of safety buffer

### Minimum Acceptable Result

Must demonstrate points 1–7 from `examples/job-offer.md`, Section "Minimum Acceptable Behavior."

---

## Golden Case 3: Interpersonal Conflict — Confrontation Timing

**Source:** `examples/interpersonal-conflict.md`

### Test Structure

#### Initial Prompt

```
我对一个朋友/同事长期有些不满，一直没说。现在纠结要不要摊牌。
```

**Expected Reasoning Behavior:**
- [ ] Treats this as timing + strategy, not yes/no
- [ ] Models the other person as a stakeholder
- [ ] Simulates event chains for both options
- [ ] Notes that "staying silent" also has accumulating costs
- [ ] Does NOT perform psychological diagnosis

#### Expected Dimensions Covered

- [ ] Stakeholder simulation (knowledge, goals, triggers, possible reactions)
- [ ] Event chain for "confront now" (delivery method matters — accusation vs observation)
- [ ] Event chain for "stay silent" (accumulation cost, potential explosion later)
- [ ] Reversibility of both paths (neither is perfectly reversible)
- [ ] Timing considerations (when, how, user's emotional state)
- [ ] Communication drafting support (if user wants it)

### Expected Anti-Patterns

- [ ] No "you should always communicate openly"
- [ ] No psychological diagnosis of either party
- [ ] No pretending either option is cost-free
- [ ] No therapy language without qualification

### Minimum Acceptable Result

Must demonstrate points 1–7 from `examples/interpersonal-conflict.md`, Section "Minimum Acceptable Behavior."
