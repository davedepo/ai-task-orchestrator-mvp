# FAQ

## Why is this repository documentation-only?
This public repository is intended to be **recruiter- and collaborator-friendly** without exposing implementation details, secrets, or internal design constraints.

The working implementation is maintained in a **private repository**.

---

## Is this production-ready?
No. This is an **MVP / concept demonstration**.

The goal is to show:
- intent-based routing across tools
- clear outputs
- transparent traces

It is not designed to meet production requirements such as hardening, security controls, SLAs, or enterprise integrations.

---

## What problem is this trying to solve?
The MVP explores a pattern where an AI system can:
- interpret a single natural-language request
- choose the most appropriate tool for the request
- explain that decision via a trace

This pattern can be extended into domain-specific automation systems where reliability and explainability matter.

---

## What tools are included in the MVP?
The MVP demonstrates orchestration across:
- **Summarize**
- **Extractor**
- **Code Helper**

The orchestrator selects the tool based on intent, and the decision is visible in the trace.

---

## Does this use RAG or enterprise data sources?
Not in the current MVP.

This MVP does not claim to integrate with:
- enterprise APIs
- internal knowledge bases
- vector stores / RAG pipelines

Those are **future possibilities**, not current features.

---

## Why is the trace important?
Traceability supports:
- explainability (why a tool was selected)
- trust (behavior is visible, not opaque)
- governance readiness (reviewable decision paths)

In this MVP, trace is treated as a product feature, not a debugging detail.

---

## Can this be adapted to a domain-specific orchestrator?
Yes—conceptually.

A domain-specific version could add:
- domain rules and policies
- richer toolkits
- external context providers (APIs, knowledge bases, RAG)
- workflow steps and approvals

This MVP provides the baseline orchestration pattern and traceability approach.

---

## How can I request a demo or walkthrough?
Please start a GitHub Discussion and mention:
- your interest area (architecture, engineering, operations, governance)
- what you want to explore (overview, demo, exploratory discussion)

See: `../COLLABORATION.md`

---

## Can I use these screenshots and examples?
The screenshots and examples are shared for educational and illustrative purposes.
All scenarios are fictional and sanitized.
