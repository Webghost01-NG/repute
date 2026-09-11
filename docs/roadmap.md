# Delivery roadmap

## Estimate and assumptions

Expected delivery for two experienced full-stack engineers with part-time design/QA is 12–16 weeks after the readiness gate. One engineer should plan for roughly 18–24 weeks. External X approval, client feedback, legal review, or provider setup can extend calendar time.

No phase is complete until its acceptance criteria and security checks pass in staging.

## Milestone 0 — Product decisions and readiness (1 week)

Outcome: remove product ambiguity and confirm the external services needed to build honestly.

- Approve MVP scope and change-control process.
- Resolve membership, recruiter authority, invitation reservation, waitlist, verification, scoring, ties, and season-end rules.
- Confirm client-owned domain, X access, email provider, hosting, database, policies, brand, and test accounts.
- Approve wireframes for all critical journeys.
- Review the data model, threat model, permission matrix, and scoring v1.

Exit gate: all launch-blocking decisions and provider-access checks are signed off.

## Milestone 1 — Platform foundation (2 weeks)

Outcome: deployable application foundation with real identity, environments, and security boundaries.

- Scaffold the modular application and design system.
- Provision development/staging database and migration pipeline.
- Implement email authentication, verification, sessions, and account states.
- Implement X OAuth and profile synchronization with real responses.
- Establish RBAC, audit/outbox foundations, CI, monitoring, and seed 100 neutral Houses.

Exit gate: a verified staging user can connect X; unauthorized routes fail server-side; all 100 neutral Houses exist exactly once.

## Milestone 2 — House lifecycle and membership (3 weeks)

Outcome: an approved Owner can operate a House and fill it safely through the complete invitation flow.

- Owner application, eligibility snapshot, admin review, and House assignment.
- Public House directory/profile and Owner workspace.
- Pledges, proactive prospects, role applications, and review queues.
- Secure invitations, provider email, expiry/revocation, and delivery status.
- Membership acceptance, removal, role history, waitlist, and notifications.
- Transactional enforcement of 50 total, 2 Recruiters, and 10 Shitposters.

Exit gate: end-to-end membership tests and concurrency tests pass; cross-House access is rejected.

## Milestone 3 — Contributions, reputation, and discovery (2–3 weeks)

Outcome: legitimate activity produces explainable public reputation.

- Contribution submission, evidence, review, verification, and reversal.
- Reputation categories, versioned event calculation, projections, and histories.
- Public profiles, contribution timelines, strongest-category derivation, and discovery filters.
- Public Analyst feedback, usefulness review, accepted suggestions, and moderation.

Exit gate: each score can be traced to source events and rule versions; follower count has no scoring effect.

## Milestone 4 — Seasons, scoring, missions, and projects (2–3 weeks)

Outcome: Admin can run Season 01 transparently and Houses can participate in optional structured work.

- Season lifecycle and 30-day configuration.
- Versioned House scoring, projections, breakdowns, snapshots, and rankings.
- Suspicious-activity review, score lock, survivor/elimination, and Founding status.
- Admin and House missions with moderation and participation.
- Initially empty project catalog, Admin controls, and optional House support records.

Exit gate: a complete staging season simulation produces deterministic rankings and exactly 50 survivors.

## Milestone 5 — Administration and operations (2 weeks)

Outcome: authorized operators can run the product without direct database intervention.

- Admin management for Houses, users, membership, roles, invitations, waitlists, missions, projects, reputation, and season.
- Analytics, audit inspection, moderation queues, provider-delivery visibility, and notification preferences.
- Admin step-up authentication and reasoned privileged actions.

Exit gate: every required admin action has authorization coverage and an audit record.

## Milestone 6 — Hardening and launch (2 weeks)

Outcome: production-ready private beta followed by controlled public launch.

- Complete accessibility, responsive, performance, security, and browser testing.
- Abuse testing, rate limits, restoration drill, data export/deletion, and incident runbooks.
- Production infrastructure, DNS, email authentication, X callbacks, monitoring, and alerts.
- Client acceptance testing, launch checklist, operator training, and rollback plan.

Exit gate: all critical acceptance tests pass; no unresolved critical/high security findings; client signs launch approval.

## Dependency chain

```text
Product rules and external access
  -> identity and database foundation
  -> House membership lifecycle
  -> contribution evidence
  -> reputation and score ledgers
  -> season rankings and operations
  -> hardening and launch
```

UI work can proceed in parallel with backend modules only after the relevant state machine and contract are approved.
