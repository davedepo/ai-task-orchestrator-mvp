# Sequence Diagram (MVP)

This sequence diagram illustrates the **conceptual runtime flow** of the
AI Task Orchestrator MVP for a single user instruction.

The diagram focuses on **intent routing, tool execution, and trace generation**,
not on implementation details.

```mermaid
sequenceDiagram
    autonumber
    actor U as User
    participant FE as Frontend UI
    participant OR as Backend Orchestrator
    participant RT as Intent Router
    participant TL as Tool Layer
    participant TR as Trace Builder

    U->>FE: Provide single instruction
    FE->>OR: Submit instruction for orchestration

    OR->>RT: Interpret intent
    RT-->>OR: Tool selection decision

    OR->>TL: Execute selected tool
    TL-->>OR: Tool output

    OR->>TR: Build Result Summary + Trace
    TR-->>OR: Response payload

    OR-->>FE: Result Summary + Trace
    FE-->>U: Render output and trace
```

Notes:

- The MVP executes a single primary tool per orchestration run.
- Multi-step workflows, external context providers, and domain-specific logic are intentional future extensions and not part of the current scope.