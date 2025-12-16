# Architecture (MVP)

This document describes the **high-level architecture** of the AI Task Orchestrator MVP.

**Scope note**
- This is an **MVP** focused on orchestration patterns and traceability.
- The public repository is **documentation-only** and does not include source code.
- Any mentions of future integrations (APIs, MCP, RAG, knowledge bases) are **conceptual** and explicitly marked as future possibilities.

---

## Architecture Goals (MVP)

The MVP architecture is designed to prove three core ideas:

1. **Single-input orchestration**
   - One natural-language instruction triggers a complete orchestration run.

2. **Tool routing**
   - The system selects the most suitable tool (Summarize / Extractor / Code Helper) based on intent.

3. **Traceability**
   - Every run produces:
     - a **Result Summary** (user-facing)
     - a **Trace** (decision path + tool routing + scope boundaries)

---

## System Overview

At a high level, the MVP is composed of:

- **Frontend UI**
  - Captures user instruction
  - Triggers “Run Orchestrator”
  - Displays:
    - “orchestrating…” status
    - **Result Summary**
    - **Trace**

- **Backend Orchestrator**
  - Interprets user intent
  - Selects an appropriate tool
  - Executes the selected tool
  - Produces:
    - output payload for Result Summary
    - trace payload for routing transparency

- **Tool Layer (MVP)**
  - **Summarize**: decision-oriented summarization
  - **Extractor**: structured extraction from unstructured text
  - **Code Helper**: engineering reasoning and code understanding

---

## Runtime Flow (Single Instruction → Result + Trace)

**Step-by-step**

1. **User Input**
   - User enters a single instruction in the UI.

2. **Orchestrator Receives Request**
   - Backend accepts the instruction and starts an orchestration run.

3. **Intent Interpretation**
   - Orchestrator determines what the user is asking for (e.g., summarize vs extract vs code reasoning).

4. **Tool Selection**
   - Orchestrator selects one tool as the primary execution path for this MVP run.

5. **Tool Execution**
   - The selected tool produces a structured output appropriate to the request.

6. **Response Assembly**
   - The backend returns:
     - **Result Summary** (main user-facing response)
     - **Trace** (routing decision + execution notes)

7. **UI Rendering**
   - The frontend displays both Result Summary and Trace.

---

## Trace Model (Why It Matters)

The **Trace** is a core artifact of the MVP.

It is designed to communicate:
- **Which** tool was selected (single-tool execution per run in the MVP)
- **Why** it was selected
- **What path** the system followed
- **What limitations** apply in the MVP (explicit scope boundaries)

This supports:
- explainability for reviewers
- trust and governance alignment
- a clean foundation for future extensions

---

## Tool Layer Responsibilities (MVP)

### Summarize
**Purpose**
- Produce audience-aware summaries (executive, governance, signal-vs-noise)

**Typical outputs**
- short, decision-oriented summaries
- structured separation of facts/assumptions/unknowns

### Extractor
**Purpose**
- Convert narrative text into structured fields

**Typical outputs**
- incident decomposition (category, suspected cause, impacted process, confidence)
- risk and ownership mapping
- functional vs non-functional requirement extraction

### Code Helper
**Purpose**
- Provide engineering reasoning support (not “code generation”)

**Typical outputs**
- high-level code explanations for reviewers
- maintainability guidance without rewriting
- architecture evolution reasoning (MVP → future possibilities)

---

## Data, Privacy, and Public Repo Constraints

This MVP documentation uses:
- **fictional and sanitized** scenarios
- no credentials, no secrets, no proprietary datasets
- screenshots intended to demonstrate **behavior and traceability**, not production integration

The public repo intentionally excludes:
- runnable configuration
- environment variables / secrets
- internal endpoints or system identifiers

---

## Conceptual Extension Points (Future, Not Current Claims)

The architecture is intentionally modular so it can evolve.

Possible future directions (conceptual):
- adding more specialized tools (domain analyzers, validators, policy checks)
- introducing configurable routing rules (hybrid rule-based + LLM-based decisions)
- integrating external context providers (APIs, knowledge bases, retrieval systems)

**Important:** These are not implemented claims in the MVP; they are extension ideas consistent with the architecture intent.

---

## Technology Stack (MVP)

The MVP implementation uses a lightweight, modern web stack:

- **Backend:** Python with FastAPI  
- **Frontend:** Next.js  
- **AI / LLM:** OpenAI APIs  

The architectural focus of this stack is on intent routing, tool orchestration,
and traceability, rather than production hardening or deployment concerns.

Implementation details, setup instructions, and runtime configuration
are intentionally excluded from this public repository.

---

## Architecture Diagram (Conceptual)

```text
+--------------------+
|     Frontend UI    |
|  (Single Input)    |
|                    |
|  "What would you   |
|   like the system  |
|   to do?"          |
+----------+---------+
           |
           | Run Orchestrator
           v
+---------------------+
| Backend Orchestrator|
|                     |
| - Interpret intent  |
| - Select tool       |
| - Enforce scope     |
+----------+----------+
           |
           | Tool Routing (one per run)
           v
+-------------------------------+
|           Tool Layer          |
|                               |
|  +-----------+  +-----------+ |
|  | Summarize |  | Extractor | |
|  +-----------+  +-----------+ |
|                               |
|        +------------------+   |
|        |   Code Helper    |   |
|        +------------------+   |
+-------------------------------+
           |
           | Tool Output
           v
+-------------------------------+
|        Response Assembly      |
|                               |
|  - Result Summary             |
|  - Trace (decision path,      |
|    routing, scope notes)      |
+-------------------------------+
           |
           v
+--------------------+
|     Frontend UI    |
|                    |
| - Result Summary   |
| - Trace            |
+--------------------+
```

**Note:**  
- The MVP executes a single primary tool per orchestration run.
- Multi-step workflows, external context providers, and domain-specific logic are intentional future extensions and not part of the current scope.
---
