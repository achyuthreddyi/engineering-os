# Architecture Design Loop

## Goal

This workflow defines the repeated design cycle used after a project has been decomposed into stages.

The loop deliberately separates deep local questioning from global architecture review.

## State Machine

```text
Stage Selected
     ↓
Context Loaded
     ↓
Initial Stage Draft
     ↓
┌───────────────┐
│     GRILL     │
└───────┬───────┘
        ↓
Revise Stage Design
        ↓
┌─────────────────────┐
│ ORCHESTRATOR REVIEW │
└─────────┬───────────┘
          ↓
  Cross-stage issues?
      /          \
    yes           no
     ↓             ↓
Return to Grill   Ready to Finalize?
                      /       \
                    no         yes
                    ↓           ↓
                 Grill       Finalize
                                ↓
                        Implementation Handoff
```

## Step 1 — Select the Stage

Identify one stage as the current design focus.

Do not deep-design several stages simultaneously unless their contracts cannot be separated.

## Step 2 — Load Canonical Context

Before reasoning about the stage, load:

1. North Star
2. global architecture
3. stage map
4. relevant ADRs
5. upstream stage specifications
6. known downstream expectations

This prevents a stage discussion from becoming an isolated architecture exercise.

## Step 3 — Produce an Initial Hypothesis

Create a provisional answer for:

- responsibility
- boundaries
- data flow
- inputs
- outputs
- components
- key interfaces
- state ownership
- likely failure modes
- important assumptions

Do not spend excessive time polishing it. The grill exists to attack it.

## Step 4 — Grill

The grill should behave adversarially toward the design while remaining constructive toward the project.

It should prioritize the highest-risk unresolved dimensions instead of asking a giant questionnaire mechanically.

For every significant answer:

1. determine what assumption it introduces
2. check whether it conflicts with canonical context
3. identify downstream consequences
4. challenge weak reasoning
5. record unresolved decisions
6. continue with the next highest-value question

A useful grill question should change or validate architecture. Questions whose answers cannot affect the design are usually noise.

## Step 5 — Revise

After each meaningful grill batch, update the working design.

Track:

- decisions made
- assumptions added
- questions closed
- questions opened
- alternatives rejected
- new cross-stage impacts

Do not finalize the canonical stage document yet.

## Step 6 — Orchestrator Review

Temporarily leave the local stage perspective.

Review the proposed design against the whole system.

The orchestrator should ask:

### North Star Alignment

Does the design still serve the original problem and success criteria?

### Boundary Integrity

Is the stage solving its own problem, or quietly moving complexity into another stage?

### Contract Consistency

Do inputs, outputs, schemas, ownership rules, and guarantees align with upstream and downstream stages?

### Architectural Consistency

Does the stage introduce a pattern, dependency, technology, or state model that contradicts the wider architecture?

### Decision Scope

Did a local choice become a global architectural decision?

If yes, create or update an ADR and architecture documentation.

### Complexity

Is the proposed architecture proportionate to the requirement, or has the design become sophisticated merely because sophistication was available?

## Step 7 — Route the Result

The orchestrator produces one of three outcomes.

### A. Return to Grill

Use when there are unresolved questions or contradictions.

The next grill pass should focus specifically on the review findings rather than restarting from scratch.

### B. Request Architecture Change

Use when resolving the stage requires changing global architecture, stage boundaries, or upstream contracts.

Update the relevant canonical documents before continuing.

### C. Approve for Finalization

Use when remaining uncertainty is acceptable for implementation.

## Step 8 — Repeat as Needed

There is no fixed number of grill/review cycles.

Stop based on architectural readiness rather than iteration count.

Typical convergence criteria:

- no unresolved high-risk architectural questions
- stable stage boundaries
- stable inputs and outputs
- known failure behavior
- explicit important assumptions
- accepted major trade-offs
- cross-stage dependencies reconciled
- implementation acceptance criteria are definable

## Step 9 — Finalize

Create the canonical stage specification from accepted decisions.

Do not include abandoned conversational branches unless they are useful as documented alternatives or ADR context.

## Step 10 — Handoff

The implementation agent receives repository artifacts, not the raw architecture conversation.

The handoff should include:

- North Star
- architecture
- stage specification
- relevant ADRs
- engineering conventions
- acceptance criteria

## Step 11 — Re-enter Architecture When Necessary

Implementation may discover constraints that invalidate the design.

When this happens:

```text
Implementation Finding
        ↓
Architecture Question
        ↓
Grill if Local
        ↓
Orchestrator Review if Cross-Stage
        ↓
Update Canonical Docs
        ↓
Resume Implementation
```

This is not process failure. It is the mechanism that keeps architecture connected to reality.
