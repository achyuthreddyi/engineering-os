# Stage <XX> — <Name>

## Goal

What this stage must achieve.

## Requirements

- requirement
- requirement

## Inputs

- input

## Outputs

- output

## Proposed Architecture

Describe the accepted design at the level required for implementation.

## Components

### Component A

Responsibility and boundaries.

## Data Flow

```text
Input
  ↓
Component
  ↓
Output
```

## Interfaces

Document APIs, schemas, events, contracts, ordering guarantees, ownership, and compatibility expectations that matter.

## State and Data Ownership

- canonical state
- derived or rebuildable state
- transient state
- mutation ownership

## Failure Handling

| Failure | Expected Behavior | Recovery |
|---|---|---|
| failure | behavior | recovery |

## Scalability

Describe expected scale, likely bottlenecks, and how the design behaves as load grows.

## Performance Considerations

- latency
- throughput
- concurrency
- memory
- storage

## Observability

- logs
- metrics
- traces
- alerts
- debugging signals

## Security Considerations

- trust boundaries
- sensitive data
- authorization/authentication implications

## Alternatives Considered

### Alternative A

Why it was considered and why it was not selected.

## Decisions

- accepted decision

## Assumptions

- assumption

## Dependencies

### Upstream

- dependency

### Downstream

- dependent stage or consumer

## Out of Scope

- excluded responsibility

## Open Questions

- unresolved question

## Acceptance Criteria

- [ ] observable criterion
- [ ] observable criterion

## Architecture Impact

State whether this stage changes global architecture, shared contracts, stage boundaries, or requires ADRs.
