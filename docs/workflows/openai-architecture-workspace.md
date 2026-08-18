# OpenAI Architecture Workspace

## Purpose

Use OpenAI models as the architecture and reasoning layer while keeping canonical project state in GitHub and implementation in a separate coding environment.

This workflow is designed for projects that use one orchestrator discussion plus dedicated stage discussions.

## Recommended Project Setup

Create one ChatGPT Project per software project.

Keep these canonical artifacts available to the project:

```text
brain-dump.md
northstar.md
architecture.md
stages.md
docs/stages/
docs/adrs/
```

Use separate chats for:

```text
00 — Orchestrator
01 — Stage <name>
02 — Stage <name>
03 — Stage <name>
...
```

The chat names are navigation aids only. The repository remains authoritative.

## Project-Level Command Conventions

The following are prompt conventions, not native commands.

### `/orchestrator`

Switch to project-level architecture review using `prompts/openai/orchestrator.md`.

### `/grill`

Run the current stage through `prompts/openai/grill.md`.

If previous orchestrator feedback exists, focus the grill on those findings first.

### `/review`

Return from local stage reasoning to the orchestrator perspective.

Evaluate cross-stage consistency and choose one outcome:

- `RETURN_TO_GRILL`
- `ARCHITECTURE_CHANGE_REQUIRED`
- `READY_TO_FINALIZE`

### `/finalize`

Create or update the canonical stage specification using `templates/stage.md`.

Only accepted decisions belong in the final document.

### `/reconcile`

Compare implementation discoveries with the accepted architecture and identify which canonical documents must change.

## Typical Stage Session

```text
/stage <N>
      ↓
Initial design discussion
      ↓
/grill
      ↓
Answer + challenge loop
      ↓
/review
      ↓
RETURN_TO_GRILL?
      ├── yes → /grill
      └── no
            ↓
      /finalize
```

The user should spend most of the cycle answering architecture questions and making decisions, not repeatedly re-explaining process instructions.

## Orchestrator Chat

The orchestrator chat should remain focused on:

- North Star alignment
- stage boundaries
- shared contracts
- global architecture
- ADRs
- cross-stage consistency
- architecture changes discovered during implementation

Avoid using the orchestrator as the primary place for deep component design.

## Stage Chats

Each stage chat should focus on one bounded architectural problem.

A stage chat may explore freely, but accepted changes that affect another stage must return through orchestrator review.

## Repository Sync Rule

After a design converges:

1. finalize the stage document
2. update ADRs if required
3. update `architecture.md` if required
4. update affected stage contracts
5. commit the documentation
6. hand the committed state to the implementation agent

Never rely on the implementation agent reconstructing architecture from the OpenAI conversation.

## Context Reset Benefit

Separating architecture and implementation contexts is intentional.

The implementation agent receives the distilled contract rather than:

- abandoned designs
- exploratory branches
- speculative ideas
- conversational assumptions

This reduces context contamination and gives implementation a fresh opportunity to challenge the accepted design against repository reality.

## Escalation From Implementation

When implementation discovers a design problem:

```text
Implementation Finding
      ↓
Local stage issue?
   /           \
 yes            no / unsure
  ↓                 ↓
Stage Grill      Orchestrator Review
   \                /
    ↓              ↓
   Update Canonical Architecture
              ↓
      Resume Implementation
```

Implementation feedback is evidence. It should update architecture deliberately rather than silently creating documentation drift.
