# Engineering OS Principles

These principles govern the workflow regardless of which model or tool is used.

## 1. Repository over memory

Chats are temporary reasoning environments. Accepted project state must be written into the repository.

If repository documentation and chat memory disagree, the repository wins until explicitly changed.

## 2. Separate exploration from commitment

Architecture discussion should be free to explore alternatives, contradict earlier ideas, and expose bad assumptions.

A decision becomes authoritative only after it is deliberately written into the canonical project documents.

## 3. Design before implementation, but only to the required depth

Resolve architectural uncertainty that can cause expensive rework before implementation.

Do not attempt to design every future detail upfront. Deeply design the stage currently approaching implementation and keep later stages at the appropriate level of abstraction.

## 4. Local reasoning must preserve global consistency

A stage can make local decisions only within its boundaries.

Changes that affect shared contracts, global architecture, upstream assumptions, or downstream responsibilities must return to orchestrator review.

## 5. Grill assumptions, not just diagrams

The purpose of architectural review is not to make the design look complete. It is to find where the design is wrong, underspecified, internally inconsistent, or unnecessarily complex.

## 6. Make important decisions explicit

Use ADRs when future work needs to understand why a meaningful architectural choice exists.

The absence of an ADR should not force someone to reconstruct a decision from chat history.

## 7. Implementation can challenge architecture

Specifications are contracts, not sacred text.

If implementation exposes a false assumption or impractical design, stop treating the document as correct merely because it was written first. Reconcile the design deliberately.

## 8. Acceptance criteria define done

A stage is complete when its observable acceptance criteria are satisfied, not when code has merely been produced.

## 9. Prefer independent reasoning contexts

Architecture and implementation may intentionally use different model families or tools.

The goal is not to assume disagreement guarantees correctness. The benefit is fresh context, role specialization, and reduced dependence on one model's conversational history.

## 10. Keep artifacts model-independent

Project documentation should describe the system, decisions, and constraints without depending on a particular model vendor.

Tool-specific prompts and skills belong in adapters around the SOP, not inside the canonical architecture.

## 11. Preserve traceability

A future reader should be able to answer:

- what was decided
- why it was decided
- where the decision applies
- how implementation satisfies it
- when the decision changed

Commit history, ADRs, stage specifications, and architecture documents should make this possible.

## 12. Complexity determines ceremony

Small projects should remain lightweight.

Large projects should not rely on memory and informal chats.

Add process only when it reduces coordination, ambiguity, or rework more than it costs.
