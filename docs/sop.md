# Greenfield Engineering SOP

## Purpose

This SOP defines how I take a software project from an unstructured idea to a reviewed architecture, implementation contract, tested code, and reconciled documentation.

The process is tool-agnostic. Architecture and implementation may be performed by different model families or tools, but accepted project state must live in the repository.

---

## Phase 1 — Capture the Brain Dump

Start with an intentionally unstructured description of the project.

Capture:

- what I want to build
- why it should exist
- expected users
- example user workflows
- constraints I already know
- technologies I am considering
- assumptions
- concerns
- unresolved questions

Do not optimize the brain dump for architecture. Its job is to preserve intent before structure is imposed on it.

### Output

`brain-dump.md`

---

## Phase 2 — Define the North Star

Convert the brain dump into the stable project intent.

The North Star should answer:

- What problem are we solving?
- Who is the system for?
- What are the core capabilities?
- What are representative user flows?
- What constraints materially shape the system?
- What is explicitly out of scope?
- What does a successful first version look like?

The North Star is not an architecture document. It defines what the architecture must serve.

### Output

`northstar.md`

---

## Phase 3 — Decompose the System

Identify the major architectural stages or workstreams implied by the North Star.

A stage should represent a coherent design problem with understandable boundaries, inputs, outputs, and dependencies.

Examples might include ingestion, storage, retrieval, orchestration, APIs, evaluation, observability, or deployment, but stage names must come from the project rather than from a fixed checklist.

For every stage capture:

- goal
- why it exists
- upstream dependencies
- downstream consumers
- expected output artifact
- current status

### Output

`stages.md`

---

## Phase 4 — Establish the Orchestrator

Maintain one logical architecture orchestrator responsible for global consistency.

The orchestrator owns:

- the North Star
- stage decomposition
- cross-stage contracts
- architecture boundaries
- important assumptions
- ADR consistency
- project-wide trade-offs
- architecture drift

The orchestrator should not replace detailed stage exploration. It exists to ensure locally reasonable decisions still compose into one coherent system.

---

## Phase 5 — Draft a Stage

Before grilling a stage, create an initial design hypothesis.

Read:

- `northstar.md`
- `architecture.md`
- `stages.md`
- relevant ADRs
- upstream stage specifications

Draft:

- goal
- requirements
- inputs and outputs
- proposed architecture
- components
- data flow
- interfaces
- assumptions
- known trade-offs
- unresolved questions

This is a draft, not an implementation contract.

---

## Phase 6 — Grill the Stage

The grill phase exists to expose architectural ambiguity before it becomes code.

Challenge the stage across these dimensions:

### Requirements

- What behavior is actually required?
- Which requirements are assumptions rather than facts?
- Which requirements conflict?

### Boundaries

- What belongs inside this stage?
- What must remain someone else's responsibility?
- Are boundaries clean enough that downstream stages can rely on them?

### Inputs and Outputs

- What exactly enters the stage?
- What guarantees does the stage make?
- Which fields, states, formats, or ordering guarantees matter?

### Data and State

- What is canonical?
- What is derived or rebuildable?
- What state is persisted?
- What state is transient?
- Who owns mutations?

### Failure Handling

- What can fail?
- What is retried?
- What is idempotent?
- What is recoverable?
- What becomes a permanent failure?

### Performance and Scale

- expected latency
- expected throughput
- concurrency
- memory and storage behavior
- bottlenecks
- 10x, 100x, and 1000x implications when relevant

### Alternatives and Trade-offs

- What other designs are credible?
- Why was this design preferred?
- What are we deliberately giving up?
- Which decisions are reversible?

### Operability

- How is the stage observed?
- What metrics and logs matter?
- How would I know it is degraded?
- How is it debugged in production?

### Security and Trust Boundaries

- What input is trusted?
- What crosses service or privilege boundaries?
- What sensitive state exists?

### Open Questions

Unresolved questions should remain explicit. Do not manufacture certainty to make the document look complete.

---

## Phase 7 — Orchestrator Review

After a grill pass, return to the project-level view.

The orchestrator checks:

- Does the proposed stage still satisfy the North Star?
- Does it contradict another stage?
- Did it introduce a new cross-stage dependency?
- Did it change a global data or API contract?
- Does the architecture document need to change?
- Is an ADR required?
- Did the stage solve a local problem by pushing unreasonable complexity elsewhere?

The review may produce new questions.

If material questions remain, return to the grill phase.

---

## Phase 8 — Repeat Grill ↔ Review

The core architecture loop is iterative:

```text
Stage Draft
    ↓
Grill
    ↓
Revise
    ↓
Orchestrator Review
    ↓
New Cross-Stage Questions?
    ├── Yes → Grill Again
    └── No  → Finalize Stage
```

A stage is ready to finalize when:

- requirements are sufficiently clear
- major assumptions are explicit
- inputs and outputs are defined
- important failure modes are handled
- meaningful alternatives were considered
- cross-stage impacts are resolved
- important decisions are documented
- acceptance criteria can be written

The goal is not to eliminate every unknown. It is to remove unknowns that would make implementation directionally unstable.

---

## Phase 9 — Finalize the Stage Specification

Convert the accepted design into a concise implementation contract.

The final stage document should contain:

- Goal
- Requirements
- Inputs
- Outputs
- Proposed Architecture
- Components
- Data Flow
- Interfaces
- Failure Handling
- Scalability
- Performance Considerations
- Observability
- Security Considerations
- Alternatives Considered
- Decisions
- Assumptions
- Dependencies
- Out of Scope
- Open Questions
- Acceptance Criteria
- Architecture Impact

The final specification should represent accepted decisions, not the full conversation history.

### Output

`docs/stages/stage-XX-<name>.md`

---

## Phase 10 — Record Architectural Decisions

Create an ADR when a decision:

- materially changes system architecture
- affects multiple stages
- is expensive to reverse
- chooses between credible alternatives
- establishes a contract future work must understand

An ADR should contain:

- Context
- Decision
- Alternatives Considered
- Consequences

### Output

`docs/adrs/ADR-XXX-<title>.md`

---

## Phase 11 — Freeze the Implementation Contract

Before implementation begins:

1. finalize the stage specification
2. update architecture documentation if needed
3. create or update ADRs
4. check downstream impacts
5. commit the accepted documentation

The committed repository state becomes the handoff contract for the implementation agent.

---

## Phase 12 — Implement

The implementation agent should begin from repository state, not from architecture chat history.

It should:

1. read the North Star
2. read the global architecture
3. read the relevant stage specification
4. read applicable ADRs and engineering conventions
5. create an implementation plan
6. implement in small logical units
7. test continuously
8. validate the stage acceptance criteria

The implementation agent may challenge the specification when codebase reality exposes a bad assumption, but it must not silently redefine architecture.

---

## Phase 13 — Reconcile Architecture and Implementation

After implementation, compare reality with the accepted design.

Ask:

- Did implementation require a design change?
- Did an assumption prove false?
- Did a dependency change?
- Did an interface change?
- Did operational behavior differ from the design?
- Is any documentation now misleading?

If yes, update the appropriate stage document, ADR, or architecture document.

Documentation should describe the system that exists, not the system that once looked elegant in a chat window.

---

## Phase 14 — Move to the Next Stage

Repeat:

```text
Explore
  ↓
Draft
  ↓
Grill
  ↓
Orchestrator Review
  ↓
Finalize
  ↓
Implement
  ↓
Verify
  ↓
Reconcile
```

until the project reaches its intended milestone.

---

## Scaling the SOP

### Small Project

Use lightweight versions of:

- North Star
- architecture
- 2–4 stages
- implementation contract
- tests

### Medium Project

Use:

- explicit orchestrator
- 5–10 stages
- ADRs
- stage specifications
- architecture reconciliation

### Large Project

Introduce domains or subsystems above stages while keeping the same local loop.

Do not increase ceremony merely because the repository has grown. Add structure only when coordination cost justifies it.
