# Testing strategy

## Test layers

- Unit: policies, validation, scoring functions, state transitions, token helpers.
- Database integration: constraints, transactions, migrations, ledgers, idempotency.
- Service integration: OAuth adapter, email adapter, outbox retries, webhook signatures.
- Component: forms, permissions-driven controls, empty/error/loading states, accessibility.
- End-to-end: browser journeys across roles and viewport sizes.
- Security: authorization matrix, CSRF, rate limiting, token replay, privilege escalation, IDOR.

External services use documented sandbox/test modes where available. Tests may use interface fakes locally, but release verification must include real staging X OAuth and email delivery; no fake response may be reported as production validation.

## Required acceptance coverage

1. Authentication: verification, session renewal/revocation, suspension, logout.
2. X connection: OAuth success, denial, state mismatch, duplicate account, refresh, disconnect.
3. Owner application: below threshold, eligible submission, validation, repeated application.
4. Admin approval: authorized review, rejection, slot assignment, audit history.
5. Membership: pledge, review, invitation, intended-user acceptance, join history.
6. Capacity: 49-to-50 success and simultaneous attempts that cannot create member 51.
7. Recruiter permissions: permitted own-House actions and denied cross-House/admin actions.
8. Shitposter permissions: contribution participation without management escalation.
9. Removal: authorization, reason, capacity update, history, notifications.
10. Waitlist: full-House entry, uniqueness, seat opening, candidate notification.
11. Invitations: secure token, expiry, revocation, replay rejection, delivery statuses.
12. Email: real staging delivery, link correctness, provider retry/webhook behavior.
13. Reputation: category events, verification, reversal, rebuild, no follower-count points.
14. House scoring: versioned formula, transparent breakdown, deterministic recomputation.
15. Missions: lifecycle, authorization, participation, completion, pause/archive.
16. Feedback: submission, moderation, usefulness/acceptance outcome, Analyst reputation.
17. Project controls: empty production seed, CRUD authorization, publish/unpublish.
18. Admin dashboard: all required operations, step-up controls, and audit records.
19. Responsiveness: representative mobile, tablet, desktop viewports and keyboard use.
20. Unauthorized access: anonymous, suspended, wrong-House, stale role, forged ID, direct API calls.

## Release quality gates

- Typecheck, lint, unit, integration, and end-to-end suites pass.
- Migration applies cleanly to an empty and previous-version staging database.
- Database restore drill succeeds.
- No open critical/high security defects.
- Core Web Vitals and accessibility thresholds are agreed and met on critical pages.
- Email authentication and delivery are verified.
- X data fields and billing behavior are verified against real staging calls.
- Product owner signs the acceptance checklist.
