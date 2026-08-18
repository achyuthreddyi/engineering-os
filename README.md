# Engineering OS

A personal, reusable operating system for taking software projects from an unstructured idea to a reviewed architecture and then to implementation.

The workflow is intentionally model-independent. Different tools can take different roles, but the repository remains the source of truth.

## Core Flow

```text
Brain Dump
    ↓
North Star
    ↓
System Decomposition
    ↓
Architecture Design
    ↓
Stage Grill
    ↓
Orchestrator Review
    ↓
Stage Specification
    ↓
Implementation Handoff
    ↓
Implementation + Verification
    ↓
Architecture Reconciliation
```

The architecture loop is intentionally iterative:

```text
Stage Draft
    ↓
Grill
    ↓
Orchestrator Review
    ↓
Grill Again if Needed
    ↓
Finalize Stage
```

## Roles

### Architecture Agent

Used for discovery, system design, trade-off analysis, questioning assumptions, stage decomposition, and cross-stage review.

My default architecture environment is OpenAI models.

### Canonical Repository

GitHub stores the accepted state of the project:

- north star
- architecture
- stages
- ADRs
- implementation contracts
- engineering conventions

Chats are reasoning environments. Repository documents are authoritative.

### Implementation Agent

Used for repository-aware implementation, testing, refactoring, debugging, and validation against the accepted design.

My default implementation environment is Claude Code.

## Repository Structure

```text
engineering-os/
├── README.md
├── docs/
│   ├── sop.md
│   ├── principles.md
│   └── workflows/
│       └── architecture-design-loop.md
├── templates/
│   ├── northstar.md
│   ├── stage.md
│   └── adr.md
├── prompts/
│   └── openai/
│       ├── orchestrator.md
│       ├── grill.md
│       └── review.md
└── claude/
    └── README.md
```

## Design Principle

> Explore freely, crystallize decisions into model-independent artifacts, implement from those artifacts, and feed implementation discoveries back into architecture.

## Scope

This repository is intended for greenfield engineering work including:

- backend systems
- distributed systems
- databases
- AI and agent systems
- infrastructure
- developer tooling
- data platforms

The process should scale with project complexity. The ceremony should not.
