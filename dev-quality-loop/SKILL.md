---
name: dev-quality-loop
description: Disciplined software development workflow for Codex. Use when Codex needs to implement, debug, refactor, review, or ship code changes and should gather scoped context, preserve user work, choose a low-risk implementation path, validate with suitable tests or diagnostics, and produce a concise engineering handoff.
---

# Dev Quality Loop

## Overview

Use this skill to keep code work deliberate without becoming slow. It helps Codex move from request to verified change through a repeatable loop: understand, scope, edit, validate, and hand off.

## Operating Loop

1. **Frame the request.** Restate the concrete outcome, affected surface, and any constraints. If the request is ambiguous and the wrong assumption could cause rework or data loss, ask one focused question; otherwise choose the conservative path and continue.
2. **Inspect before editing.** Check repository state, relevant files, tests, and local conventions. Prefer semantic or symbol-level tools when available. Read only the code needed to justify the change.
3. **Plan the smallest credible change.** Identify the behavior to alter, the contract to preserve, and the validation that will prove it. Avoid unrelated cleanup unless it removes real risk for this task.
4. **Make targeted edits.** Follow existing patterns for naming, errors, logging, dependencies, and tests. Preserve user changes and avoid rewriting files wholesale when a localized patch is enough.
5. **Validate proportionally.** Run the narrowest useful checks first, then broader checks when shared behavior, public APIs, migrations, security, or user-facing flows changed.
6. **Review the diff.** Look for accidental churn, stale imports, missing tests, changed semantics, and documentation drift. Re-run checks after fixes.
7. **Hand off clearly.** Summarize what changed, where it changed, what was verified, and any residual risk or follow-up.

## Context Rules

- Start with repository status so user work is visible before edits.
- Prefer project-local guidance (`AGENTS.md`, existing tests, package scripts, CI config) over generic habits.
- For unfamiliar libraries, CLIs, cloud services, or APIs, fetch current official documentation before relying on syntax.
- For large files, inspect symbols, headings, or targeted search results before reading broad chunks.
- Treat generated files, lockfiles, migrations, and snapshots as high-blast-radius unless the task explicitly needs them.

## Change Design

- Keep the public contract stable unless the user asked for a breaking change.
- Prefer adding a focused helper over duplicating logic in multiple call sites, but do not introduce abstraction for a one-off branch.
- Match the existing error model: thrown exceptions, result types, HTTP status mapping, validation errors, logging style, and retry behavior.
- Keep data shape changes explicit at boundaries: API payloads, database schemas, config files, event contracts, and serialized formats.
- When changing concurrency, caching, authentication, authorization, money, time, or deletion behavior, assume the change is high risk and expand validation.

## Validation Ladder

Choose checks from the lowest rung that proves the change:

1. Static diagnostics for touched files or symbols.
2. Unit tests covering the changed behavior.
3. Integration tests for cross-module contracts, persistence, queues, API routes, or CLI commands.
4. Build/typecheck/lint when the project has fast commands or when edits cross boundaries.
5. Browser, E2E, or manual workflow checks for visible UI and request/response behavior.

If a check cannot run, record the command attempted, the failure reason, and the residual risk.

## Review Checklist

Load `references/review-checklist.md` when the change is more than a few lines, touches shared code, alters behavior in multiple layers, or before preparing a commit/PR.

## Handoff Template

Use this shape for the final response:

```text
Implemented <outcome> in <main files>.

Validation: <commands/checks and results>.
Notes: <only blockers, residual risk, or follow-up that matters>.
```

Keep the handoff factual and short. Do not include implementation trivia that the diff already explains.
