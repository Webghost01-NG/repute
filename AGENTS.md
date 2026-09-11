# Repository Guidelines

## Purpose

Repute is a production-minded MVP for contribution-based public reputation and a seasonal House competition. Reputation must come from recorded activity and outcomes, not follower count or artificial engagement.

## Structure

Planning documents live in `docs/`. Application structure will be created only after the architecture pull request is approved. The proposed application is a modular Next.js monolith with PostgreSQL.

## Required workflow

Before editing, read the README, relevant issue, architecture documents, and existing implementation. Always run `git status --short --branch`, fetch, update `main` with a fast-forward pull, and create a focused branch. Never implement directly on `main`. Never push, merge, or merge your own pull request without explicit instruction.

Ask before changing architecture, dependencies, schemas, API contracts, CI/CD, environment configuration, or security-sensitive code. Preserve unrelated work in a dirty worktree.

## Engineering expectations

- TypeScript strict mode; two-space indentation; semicolons.
- Validate all untrusted input on the server.
- Enforce authorization and House boundaries on the server.
- Enforce the 50-member total and role caps transactionally in PostgreSQL.
- Store invitation and verification tokens as hashes, with expiration and revocation.
- Record sensitive mutations in the append-only audit history.
- Keep email and X integrations behind interfaces; never invent successful provider responses.
- Use UTC in storage and explicit time zones in presentation.
- Preserve accessibility and keyboard behavior.

## Verification

Each implementation issue must include proportionate unit, integration, authorization, and end-to-end coverage. Before completion, report files changed, reasons, tests and results, and remaining risks.
