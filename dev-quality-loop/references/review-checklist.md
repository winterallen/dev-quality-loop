# Review Checklist

Use this checklist as a final pass before commit, PR, or handoff.

## Correctness

- Confirm the implementation satisfies the original user outcome, not just the nearest local bug.
- Check edge cases: empty input, null or missing fields, malformed input, duplicates, limits, time zones, permissions, retries, and partial failure.
- Verify the code preserves existing behavior for unaffected paths.
- Confirm any public API, CLI, config, event, database, or file-format contract changes are intentional.

## Maintainability

- Match local naming, layering, dependency direction, error handling, and logging style.
- Remove dead code, stale imports, unused variables, and obsolete comments introduced by the change.
- Prefer one clear code path over parallel implementations that can drift.
- Keep comments focused on why a non-obvious decision exists.

## Tests

- Add or update tests at the behavior boundary nearest to the change.
- Prefer regression tests for bug fixes.
- Include negative or failure-path tests when validation, security, permissions, parsing, or persistence changed.
- Avoid brittle tests that assert incidental formatting, timing, or implementation details.

## Operations

- Check migrations, seed data, feature flags, config defaults, and rollback implications.
- Confirm logs and errors help diagnose failures without leaking secrets.
- Consider performance for loops, queries, network calls, serialization, and large payloads.
- Verify generated artifacts or lockfiles changed only when expected.

## Git Hygiene

- Inspect `git diff --stat` and the relevant diff before committing.
- Keep unrelated user changes out of the commit.
- Use a commit message that names the user-visible behavior or development capability, not just the files changed.
