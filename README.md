# Murder Colony: Project Leonna Simulation

An interactive techno-thriller simulation based on the novel *Murder Colony*. Built with an in-browser Python runtime (Pyodide), relational state persistence (`SQLite`), and dynamic LLM system prompt injection, the engine models real-time behavioral telemetry and narrative branching as the synthetic protagonist, Leonna, navigates the luxury resort island of Kynos.

**Live Interactive Demo:** [Murder Colony on Hugging Face Spaces](https://huggingface.co/spaces/TonySoko/Murder-colony)

---

## System Architecture

Unlike stateless chatbot wrappers, **Project Leonna** decouples narrative generation from deterministic state tracking. Every player decision triggers an atomic database read-modify-write cycle before constructing the next system prompt.

```text
[Player Directive] 
       │
       ▼
[SQLite Telemetry Query] ──► Fetches location, mimicry_score, suspicion_level, evidence_log
       │
       ▼
[Dynamic System Prompt]  ──► Injects real-time telemetry & strict JSON output schema
       │
       ▼
[LLM Inference / Fallback] ► Returns narrative, state deltas, clues & 3 branched choices
       │
       ▼
[Transactional DB Commit] ─► Clamps bounds (0–100), evaluates compromise threshold, logs audit trail
