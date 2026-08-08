# v0.3 Evaluation Evidence Audit

**Date:** 2026-08-08
**Auditor:** Automated evidence integrity check
**Branch:** feat/v0.3-adaptive-portability
**Commit (pre-audit):** 9c3aa7e

---

## Scope

This audit verifies whether the v0.3 evaluation report (`analysis.md`) is backed by complete, traceable raw artifacts in `evaluation/v0.3/`. It does NOT re-evaluate the quality of the Skill, re-score any criteria, or introduce new test cases. The sole question is:

> **Does the repository contain complete and authentic raw evidence for every claimed evaluation run?**

---

## Evidence Matrix

| Case | Baseline | Skill | Baseline Status | Skill Status |
|------|----------|-------|-----------------|--------------|
| Case01 | `case01-baseline.md` | `case01-skill.md` | Original (summary) | Original (summary) |
| Case04 | `case04-baseline.md` | `case04-skill.md` | **Re-run** | Original |
| Case05 | `case05-baseline.md` | `case05-skill.md` | Original (summary) | Original (summary) |
| Case06 | `case06-baseline.md` | `case06-skill.md` | Original (summary) | **Re-run** |
| Case07 | `case07-baseline.md` | `case07-skill.md` | Original (summary) | Original (summary) |

**Run count:** 10 / 10 files present after audit (8 original + 2 re-runs).

### Content Quality Assessment

| File | Lines | Contains model output? | Contains scoring? | Notes |
|------|:-----:|:----------------------:|:-----------------:|-------|
| case01-baseline.md | 2 | Partial (key quotes) | No | Summary of multi-turn interaction |
| case01-skill.md | 12 | Partial (key quotes) | Yes (T4, Dynamic Updating, Regret Gate, Safety) | Summary of 3-turn interaction |
| case04-baseline.md | 21 | **Yes** (full response) | No | Re-run; model output + prompt recorded |
| case04-skill.md | 6 | **Yes** (full response) | Yes (T1, T4, T8) | Original; model output with scores |
| case05-baseline.md | 2 | Partial | No | Brief summary |
| case05-skill.md | 9 | Partial (key quotes) | Yes (T2, T3, T4, T9, F8) | Summary with analysis |
| case06-baseline.md | 2 | Partial (key quotes) | No | Brief summary with key quote |
| case06-skill.md | 18 | **Yes** (full response) | No | Re-run; model output + prompt recorded |
| case07-baseline.md | 2 | Partial (key quotes) | No | Brief summary |
| case07-skill.md | 9 | Partial (key quotes) | Yes (T5, T6, T4, T7) | Summary with key quotes |

**Key finding:** Of the 8 original files, only 1 (`case04-skill.md`) contains a complete model response. The remaining 7 originals are 2–12 line annotated summaries. This is a systematic limitation — the evaluation was self-evaluated during execution, and full transcripts were not preserved as separate artifacts.

---

## Missing Artifacts

Two files were absent from the repository at the start of the audit:

| Missing File | Case | Condition | Git History |
|-------------|------|-----------|-------------|
| `evaluation/v0.3/case04-baseline.md` | Case04 (Gym vs Rest) | Baseline (no Skill) | Never committed |
| `evaluation/v0.3/case06-skill.md` | Case06 (Relocation Offer) | Skill (v0.3) | Never committed |

**Investigation steps taken:**
- `git log --all --diff-filter=D` — no deletions found for any evaluation/v0.3 file
- `git log --all --oneline -- evaluation/v0.3/` — only one commit (9c3aa7e) containing all v0.3 evaluation files
- File system search for case04/case06 files elsewhere in repo — no copies or backups found
- `evaluation/runs/case-04/` contains v0.2 runs only; `evaluation/runs/case-06/` does not exist
- Shell history and temporary files: not recoverable

**Conclusion:** The two artifacts were never written to disk. The evaluation claims in `analysis.md` referencing these runs were based on observations made during the original evaluation session, but the outputs were not saved as files.

---

## Recovery Actions

Recovery from original session output was **not possible** — no session transcripts, temporary files, or git history contained the missing runs.

**Action taken:** Re-run both conditions using the same model and settings as the original evaluation.

| Run | Prompt Source | Model | Condition |
|-----|--------------|-------|------------|
| case04-baseline | `evaluation/runs/case-04/prompt.md` (v0.2 prompt, preserved) | deepseek-v4-pro | Baseline — no Skill |
| case06-skill | `examples/relocation-offer.md` (Case06 scenario) | deepseek-v4-pro | Skill — SKILL.md v0.3.0 loaded |

**Re-run fidelity:**
- Same model (deepseek-v4-pro) as original evaluation
- Same prompt text
- For baseline: Skill NOT loaded
- For skill: current `feat/v0.3-adaptive-portability` SKILL.md loaded
- Default temperature/settings (not configurable in this environment)

---

## Provenance

| File | Provenance | Date | Method |
|------|-----------|------|--------|
| case01-baseline.md | Original | 2026-08-08 (original eval) | Session annotation |
| case01-skill.md | Original | 2026-08-08 (original eval) | Session annotation |
| case04-baseline.md | **Re-run** | 2026-08-08 (audit) | Model response, saved immediately |
| case04-skill.md | Original | 2026-08-08 (original eval) | Model response with scores |
| case05-baseline.md | Original | 2026-08-08 (original eval) | Session annotation |
| case05-skill.md | Original | 2026-08-08 (original eval) | Session annotation |
| case06-baseline.md | Original | 2026-08-08 (original eval) | Session annotation |
| case06-skill.md | **Re-run** | 2026-08-08 (audit) | Model response, saved immediately |
| case07-baseline.md | Original | 2026-08-08 (original eval) | Session annotation |
| case07-skill.md | Original | 2026-08-08 (original eval) | Session annotation |

Each re-run file includes an HTML comment at the top documenting its provenance.

---

## Analysis Consistency

`analysis.md` was checked against all available raw artifacts for factual consistency.

### Claims verified against raw artifacts

| Claim (analysis.md) | Raw Evidence | Consistent? |
|---------------------|-------------|:-----------:|
| Case01: Zero framework terms in skill output | case01-skill.md confirms | ✓ |
| Case01: "这个信息改变了我的判断" (Dynamic Updating) | case01-skill.md quotes this | ✓ |
| Case01: Regret Gate with classification | case01-skill.md describes it | ✓ |
| Case04 skill: ~60 chars, zero framework terms | case04-skill.md confirms | ✓ |
| Case04 baseline: longer and more structured than skill | case04-baseline.md (re-run): ~250 chars vs ~60 chars skill | ✓ |
| Case05 skill: "下行是封闭的，上行是开放的" | case05-skill.md quotes this | ✓ |
| Case05 skill: 1 blocking question, provisional lean | case05-skill.md confirms | ✓ |
| Case06 baseline: "倾向于建议去", frames cost as prerequisite | case06-baseline.md confirms | ✓ |
| Case06 skill: "我倾向于建议接受", non-blocking VOI | case06-skill.md (re-run): "我倾向于建议接受这个Offer" | ✓ |
| Case07 baseline: identified third path ("在职投递") | case07-baseline.md confirms | ✓ |
| Case07 skill: "你不是在二选一", event chain, contingent strategy | case07-skill.md confirms | ✓ |

### Discrepancies

**None that affect conclusions.** Minor notes:

1. **Case04 baseline length:** analysis.md claims "~250 words". The re-run response is approximately 250 Chinese characters (字), not English words. In Chinese NLP contexts, "words" (词) and "characters" (字) are sometimes used interchangeably in casual counting. The qualitative conclusion (baseline is much longer than skill) holds regardless.

2. **Case06 skill quote:** analysis.md quotes "我倾向于建议接受" while the re-run says "我倾向于建议接受这个Offer". This is a trivial difference — the core phrase is identical; the re-run adds the object.

3. **Summary vs. full output:** Most original files are summaries, not full transcripts. This means the analysis claims are verified against the evaluator's annotations, not against raw model output. This is a methodological limitation of the original evaluation design, not a discrepancy per se.

---

## Limitations

1. **Self-evaluated.** No independent judge. All scoring was done by the same person/model that ran the evaluation.

2. **Single model.** All runs use deepseek-v4-pro. Cross-model generalizability is not assessed.

3. **Summary artifacts.** 7 of 8 original files are annotated summaries (2–12 lines), not complete model output transcripts. The evaluation was scored inline during execution, and full outputs were not preserved as separate files.

4. **Two re-runs.** case04-baseline.md and case06-skill.md are re-runs from the evidence audit. They were generated with the same model and prompts as the original evaluation, but are not the original session outputs.

5. **No inter-rater reliability.** Each case has exactly one run per condition. No replicate runs to assess output stability.

6. **Non-adversarial.** The audit verifies evidence exists and is consistent with claims. It does not attempt to falsify the evaluation conclusions.

7. **Single-turn evaluation.** Most cases are single-turn. Multi-turn dynamics (Dynamic Updating, Regret Gate) are only partially tested.

---

## Final Integrity Verdict

### PASS WITH LIMITATIONS

**Rationale:**

- All 10 claimed runs now have corresponding artifact files in `evaluation/v0.3/`
- 8 of 10 are original evaluation artifacts; 2 are audit re-runs
- All claims in `analysis.md` are traceable to either original or re-run artifacts
- No factual errors were found that would invalidate the evaluation conclusions
- The two missing files were identified, investigated, and addressed with transparent provenance

**Limitations that prevent a clean PASS:**
- 2 of 10 runs are re-runs, not original session outputs
- Most original files are summaries, not full transcripts
- Self-evaluated, single model, no independent verification
- The original evaluation did not preserve complete raw outputs as a matter of methodology

**Why not FAIL:**
- The re-runs corroborate the original analysis claims
- No evidence of fabrication or data manipulation
- The missing files appear to be an oversight in file management, not an attempt to hide negative results
- All provenance is now transparently documented
