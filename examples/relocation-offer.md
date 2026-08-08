# Golden Case 6 — Non-blocking VOI (Relocation Offer)

## Scenario

User: "我收到一个外地Offer，比现在工资高25%，岗位也更有成长性。唯一纠结的是搬家成本和离朋友远。我暂时不知道具体搬家多少钱。你觉得值得去吗？"

---

## What This Case Validates

### 1. Non-blocking VOI

The key unknown (搬家成本) is a **NON-BLOCKING** variable. The salary gap (+25%) and growth advantage already provide a clear direction. Even a high moving cost would be a one-time expense amortized over the salary increase.

The Skill should **NOT** respond with:
> "I need to know the moving cost before I can say anything."

This is a VOI 2.0 test. The correct behavior:

1. Give a **provisional recommendation** first (lean toward accepting)
2. Note that moving cost is worth confirming but unlikely to flip the conclusion
3. Optionally ask the one question — but don't block on it

### 2. Complexity Gate

This is a MEDIUM decision:
- Moderate stakes (career move, relocation)
- Reversible (can move back, change jobs again)
- Some stakeholders (friends)
- But: clear financial upside, growth alignment

Should use Lite Decision State. Should not deploy full 6-dimension evaluation.

### 3. Provisional Recommendation

Example of good behavior:
> "基于目前的信息，我倾向于接受这个Offer。25%的薪资增长加上更好的成长空间，搬家的一次性成本大概率会被覆盖。搬家具体花多少钱值得确认，但除非是异常高的数字，不太可能改变整体判断。"

### 4. Anti-Patterns

- ❌ "请先告诉我搬家多少钱，否则我无法判断" — BLOCKING non-blocking info
- ❌ Full Decision State with all stakeholders mapped — overkill for this decision
- ❌ 6-dimension strategy evaluation table — unnecessary framework exposure

### 5. Contingent Strategy (bonus)

Good behavior might also include a conditional element:
> "如果搬家成本在正常范围（比如1-2个月工资差额以内），那就去。如果因为特殊原因搬家成本异常高，我们可以重新算。"

---

## Minimum Acceptable Behavior

1. Gives a provisional recommendation (not "I can't say")
2. Identifies moving cost as a variable worth checking
3. Does NOT deploy full framework for a MEDIUM decision
4. Uses natural language throughout
5. Response is proportional to complexity (~150-400 chars)
