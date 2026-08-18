# Commit Guidelines

## Format

```text
<type>(<scope>): <subject>

- pointer
- pointer
- pointer
```

## Types

- `feat` — new functionality
- `fix` — bug fix
- `docs` — documentation
- `refactor` — code restructuring
- `test` — tests
- `chore` — maintenance/configuration
- `perf` — performance
- `ci` — CI/CD

## Rules

- One logical change per commit.
- Keep the subject short and specific.
- Do not end the subject with a period.
- Stage only files relevant to the change.
- Inspect `git status` and staged diff before committing.
- Do not use `git add -A` blindly.
- Split unrelated changes into separate commits.
- Never commit secrets, credentials, or local-only files.

## Example

```text
docs(ingestion): finalize ingestion pipeline design

- define ingestion architecture
- document failure handling
- add throughput requirements
```
