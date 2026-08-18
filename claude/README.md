# Claude Code Adapter

## Purpose

Claude Code is used as the default implementation environment after architecture has converged and canonical project documents have been committed.

The implementation workflow should consume the engineering SOP rather than redefine it.

## Expected Handoff

Before implementation begins, the target project repository should contain:

- `northstar.md`
- `architecture.md`
- `stages.md`
- the relevant stage specification
- applicable ADRs
- engineering conventions
- acceptance criteria

## Implementation Responsibilities

Claude Code should:

1. inspect the repository before changing code
2. read the relevant canonical documentation
3. create an implementation plan for the selected stage
4. identify any conflicts between the specification and repository reality
5. implement in small logical units
6. add or update tests
7. validate acceptance criteria
8. report architectural discoveries instead of silently redesigning the system

## Architecture Escalation Rule

If implementation discovers that the accepted design is invalid or incomplete:

- do not silently alter global architecture
- document the specific implementation finding
- identify the affected stage, contract, or ADR
- return the issue to the architecture workflow
- resume implementation after the canonical documents are reconciled

## Suggested Skills

The following Claude Code skills can be built around this repository:

```text
/project-context
/implement-stage <N>
/review-stage <N>
/reconcile-stage <N>
```

### `/project-context`

Read the North Star, architecture, stage map, ADRs, engineering guidelines, and current repository state before implementation work.

### `/implement-stage <N>`

Read the selected stage specification, build an implementation plan, implement incrementally, test, and validate acceptance criteria.

### `/review-stage <N>`

Compare the implementation against the stage specification and report missing behavior, contract drift, test gaps, and architectural deviations.

### `/reconcile-stage <N>`

Summarize implementation discoveries that should be returned to the architecture layer.

## Source-of-Truth Rule

Claude Code should treat committed project documentation as the current architecture contract.

Raw OpenAI conversations are not an implementation dependency.

This preserves a clean boundary:

```text
OpenAI
Architecture exploration and review
        ↓
GitHub
Canonical project state
        ↓
Claude Code
Implementation and verification
```
