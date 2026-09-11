# System architecture

## Architecture decision

Use a modular monolith for the MVP. A single deployable application contains the public web UI, authenticated dashboards, server-side application services, and HTTP endpoints. PostgreSQL is the source of truth. External providers are accessed through narrow adapters, and asynchronous work is handled by a durable job queue.

This avoids premature distributed-system complexity while allowing modules to be extracted if scale later requires it.

## Proposed stack

| Concern | Baseline | Reason |
| --- | --- | --- |
| Web/application | Next.js, React, TypeScript | Cohesive application shell, server rendering, route handlers |
| Database | Managed PostgreSQL | Transactions, constraints, relational history, mature operations |
| Data access | Prisma | Typed schema, migrations, transaction support |
| Authentication | Auth.js plus application sessions | OAuth support with server-owned authorization |
| X connection | OAuth 2.0 Authorization Code with PKCE | Official user consent and minimal scopes |
| Email | Provider adapter, initially Resend or Postmark | Transactional delivery, templates, webhooks |
| Jobs | PostgreSQL-backed durable queue | Retries and scheduled work without another core datastore |
| Validation | Zod | Shared boundary schemas; server remains authoritative |
| UI | Tailwind CSS plus accessible primitives | Consistent responsive system without a heavy design dependency |
| Tests | Vitest, Testing Library, Playwright | Unit, component, integration, and browser coverage |
| Operations | Structured logs, Sentry-compatible errors, product analytics | Debugging, safety, and product learning |

Providers are provisional until account access, pricing, data location, and client ownership are confirmed.

## Logical modules

- Identity: users, emails, sessions, X accounts, consent, suspensions.
- Houses: slots, profiles, applications, assignments, membership, roles, waitlists.
- Invitations: issuance, delivery, acceptance, expiry, revocation, retries.
- Contributions: submissions, evidence, reviews, outcomes, moderation.
- Reputation: category definitions, immutable events, summaries, known-for derivation.
- Seasons: lifecycle, eligibility, rankings, survival and Founding status.
- Scoring: versioned rules, score events, projections, explanations, adjustments.
- Missions: admin templates, House missions, participation and completion.
- Projects: empty catalog, administration, House support relationships.
- Feedback: public analysis, review, accepted suggestions, quality outcomes.
- Notifications: in-app records, preferences, email dispatch.
- Administration: privileged commands, queues, analytics, moderation.
- Audit: immutable security and business-event history.

Modules communicate through application services and durable domain events, not direct UI access to database tables.

## Request path

```text
Browser
  -> Next.js route/page
  -> authentication and authorization guard
  -> input validation
  -> module application service
  -> PostgreSQL transaction
  -> domain/audit event and outbox record
  -> response

Background worker
  -> claims outbox/job
  -> email/X/internal adapter
  -> records result and schedules retry if necessary
```

## Identity strategy

`User` is the durable platform identity. Email credentials and `XAccount` are connected identities rather than the user record itself. Future wallets can therefore be added as another connection without changing House membership, contributions, or reputation ownership.

An X account is unique platform-wide and cannot be attached to multiple users. Repute stores X user ID as the stable identifier; username changes do not create a new identity.

## Authorization strategy

- Route visibility is not authorization.
- Every mutation invokes a server-side policy using authenticated user ID, platform role, House scope, active membership, and resource state.
- House-scoped queries include the authorized House ID in the database predicate.
- Admin role changes require step-up authentication and an audit reason.
- Suspended users cannot mutate state or accept invitations.
- Authorization failures reveal no private cross-House information.

## Capacity and concurrency

Membership acceptance and invitation acceptance run in a database transaction that locks the House capacity row, rechecks all invariants, creates the active membership, updates the counter, consumes the invitation, and writes audit/outbox events atomically.

Database triggers or stored functions provide a final invariant guard so alternate code paths cannot exceed:

- 50 active members total
- 1 active Owner
- 2 active Recruiters
- 10 active Shitposters

Application checks improve error messages but are never the final protection.

## Asynchronous delivery

An outbox record is written in the same transaction as important state changes. Workers deliver invitation and notification emails with idempotency keys, bounded exponential retry, and dead-letter visibility. Provider webhooks update delivery status after signature verification.

Invitation raw tokens are displayed only in outbound links. Only a cryptographic hash is stored. Acceptance verifies intended user, expiry, revocation, membership eligibility, and capacity.

## Scoring projections

Contribution, reputation, and House score events are append-only ledgers. Read-optimized summaries and leaderboards are projections that can be rebuilt. Each event records the scoring-rule version, source event, breakdown, verification state, and actor.

Scoring configuration is drafted and validated before publication. A published version is immutable. New versions define whether their effective date is prospective or whether an explicit, audited recomputation is required.

## Deployment environments

- Development: local application, isolated local/test database, X development app, email sandbox.
- Staging: production-like deployment, synthetic labeled data, test X app, non-production sending domain.
- Production: client-owned services, real data, protected main deployment, backups and alerting.

Separate credentials and callback URLs are required for each environment. Secrets live in managed environment configuration, never in Git.

## Security baseline

- Secure, HTTP-only, SameSite cookies and CSRF protection.
- OAuth state and PKCE verification; minimal X scopes.
- Verified email before sensitive workflows.
- Rate limits by user, IP, and action category.
- Server-side schema validation and normalized URLs/handles.
- Output encoding and restrictive content security policy.
- No arbitrary HTML in user content.
- Short-lived, one-time, hashed invitation and verification tokens.
- Audit logs for authentication, permissions, moderation, scoring, and membership.
- Encryption in transit and provider-managed encryption at rest.
- Scheduled backups and tested restoration.
- Dependency, secret, and migration checks in CI.
- Data export/deletion process compatible with provider policies.

## Reliability and observability

- Request correlation IDs across logs, jobs, and provider calls.
- Health and readiness endpoints that do not leak sensitive data.
- Error tracking with sensitive-field redaction.
- Metrics for authentication, OAuth failures, email delivery, job backlog, invitation conversion, and scoring recomputation.
- Admin-visible provider failure and dead-letter queues.
- Database point-in-time recovery where the selected provider supports it.

## Scaling path

The initial system should scale vertically and through stateless application replicas. Add a dedicated cache only after measurements justify it. At higher load, scoring and notifications can become separate workers while retaining the same events and contracts. The append-only ledgers support rebuilding projections without rewriting the core product.
