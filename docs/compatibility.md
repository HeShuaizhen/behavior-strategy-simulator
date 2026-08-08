# Host Compatibility

Behavior Strategy Simulator is a **runtime-agnostic reasoning skill.** It does not depend on any specific LLM provider, runtime, or tool system.

---

## Minimum Host Requirements

The host environment MUST support:

1. **System-level instruction injection** — the ability to prepend SKILL.md content as system-level instructions (or equivalent, e.g., custom instructions, developer messages)
2. **Multi-turn context** — the ability to maintain conversation state across multiple user/assistant turns (required for Dynamic Updating, Regret Handling, and VOI follow-ups)

These are the only hard requirements. Most modern LLM interfaces support both.

---

## Optional Host Capabilities

These enhance the Skill but are NOT required:

| Capability | Benefit If Present | Fallback If Absent |
|-----------|-------------------|-------------------|
| Persistent memory (cross-session) | Decision Profile accumulation, Outcome tracking | Per-session only; profile resets each conversation |
| Tool access | Could fetch real data for VOI questions | Asks user to provide data manually |
| File access | Could read reference files on demand | References must be inlined or summarized |
| Structured output (JSON/YAML) | Could maintain Decision State formally | Maintains state in natural language internally |

---

## Platform Guidance

### Claude Code
**Status: Tested (primary development target).**
Load SKILL.md as a project skill. References are available as files in the project directory.

### ChatGPT (Custom Instructions / GPTs)
**Status: Expected to work.**
Paste SKILL.md content into custom instructions. References can be uploaded as knowledge files. Multi-turn context is natively supported.

### Codex / OpenAI API (system prompt)
**Status: Expected to work.**
Include SKILL.md content in the system message. References must be inlined or summarized in the system prompt if the model cannot access files.

### Generic LLM (any provider with system prompt)
**Status: Not tested — expected to work.**
Any LLM interface that supports system-level instructions and multi-turn conversation should be compatible. Performance depends on the base model's reasoning capability.

### Single-turn / Stateless Interfaces
**Status: Partially compatible.**
Dynamic Updating, Regret Handling, and VOI follow-ups will not function. Static strategy evaluation dimensions still apply.

---

## Loading the Skill

### Recommended: Load SKILL.md only
The 260-line SKILL.md is designed to be self-contained for runtime use. References provide depth documentation but are not required at inference time.

### Extended: Load SKILL.md + strategy-model.md
If context budget permits, loading `references/strategy-model.md` alongside SKILL.md provides richer dimension definitions.

### Full: Load all references
Only recommended for evaluation or when maximum fidelity is required. The full reference set (~500 lines) is designed for human maintainers, not runtime loading.
