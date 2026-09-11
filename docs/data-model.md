# Data model and invariants

This is the conceptual schema. Exact names and columns will be finalized in a reviewed migration design.

## Identity and access

- `users`: durable platform identity, status, public profile, onboarding state.
- `email_identities`: normalized email, verification state, primary flag.
- `x_accounts`: unique X user ID, username, public profile snapshot, metrics timestamp, OAuth metadata.
- `auth_accounts`: provider linkage managed by the authentication layer.
- `sessions`: revocable authenticated sessions.
- `platform_role_assignments`: Admin and other platform-scoped grants with issuer and reason.
- `consents`: policy version, scope, timestamp, withdrawal.

## Houses and membership

- `houses`: one of the 100 Season 01 slots, public data, operational status.
- `house_applications`: applicant, eligibility snapshot, application answers, decision and reviewer.
- `house_assignments`: approved application to slot history.
- `house_memberships`: user, House, role, active interval, join source, removal reason.
- `house_role_applications`: Recruiter or Shitposter application and decision.
- `pledges`: public-application data and review state.
- `recruitment_prospects`: proactive discovery record, rationale, creator, consent/contact state.
- `invitations`: intended user/email, House, role, token hash, expiry, status.
- `waitlist_entries`: House, user, position metadata, status, notification history.
- `membership_events`: append-only join, role, removal, and reinstatement history.

## Activity and reputation

- `contributions`: actor, House if applicable, category, narrative, evidence, state.
- `contribution_evidence`: URLs/files and verification metadata.
- `contribution_reviews`: reviewer, decision, quality/outcome dimensions, notes.
- `reputation_categories`: admin-managed category definitions.
- `reputation_events`: immutable point/evidence events with rule version and reversal link.
- `reputation_summaries`: rebuildable per-user/category projection.
- `feedback`: subject, analyst, analysis, state, outcome.
- `feedback_reviews`: usefulness and accepted-suggestion outcome.

## Competition and content

- `seasons`: duration, lifecycle state, capacity and survival configuration.
- `season_houses`: House participation and final status.
- `scoring_rule_sets`: immutable published versions and draft configuration.
- `house_score_events`: immutable breakdown events with source and reversal.
- `house_score_summaries`: rebuildable totals and category breakdowns.
- `ranking_snapshots`: periodic published ranks and explanations.
- `missions`: admin or House source, lifecycle, eligibility, moderation state.
- `mission_participations`: participant, status, submission, decision.
- `projects`: initially empty, admin publication state.
- `house_projects`: optional discovery/support relationship and history.

## Operations

- `notifications`: recipient, kind, payload reference, read state.
- `notification_preferences`: channel preferences by notification category.
- `email_deliveries`: template, provider ID, idempotency key, delivery state.
- `outbox_events`: durable work awaiting publication/delivery.
- `admin_actions`: actor, action, target, reason, before/after metadata.
- `audit_events`: append-only actor, action, target, request correlation, timestamp.
- `moderation_cases`: reports, evidence, decisions, appeals.

## Core constraints

1. Season 01 has exactly 100 House slots numbered 1 through 100.
2. An X user ID belongs to at most one Repute user.
3. A user has at most one active membership unless the product decision explicitly changes this rule before migration approval.
4. A House has at most 50 active memberships, including its Owner, Recruiters, and Shitposters.
5. A House has at most one active Owner, two active Recruiters, and ten active Shitposters.
6. Invitation tokens are unique by hash, one-use, revocable, expiring, and bound to an intended identity.
7. Only one active waitlist entry exists per user and House.
8. Published scoring rule versions cannot be mutated.
9. Reputation and score corrections use compensating events rather than destructive edits.
10. Audit records cannot be edited through the application.

## Capacity transaction

Membership creation must call one database-owned operation:

1. Begin transaction.
2. Lock the target House capacity/membership scope.
3. Verify House status and season eligibility.
4. Verify the user is allowed to join.
5. Count or read the locked active-member capacity.
6. Check total and requested-role caps.
7. Insert membership and consume invitation if present.
8. Add membership, audit, notification, and outbox events.
9. Commit.

Any conflict produces a domain error such as `HOUSE_FULL` or `ROLE_CAP_REACHED`; it never partially accepts a user.

## Deletion and history

Operational records may be anonymized or detached when required by policy, but evidence-bearing ledgers require a documented retention decision. Soft deletion is not a substitute for an explicit legal retention policy. Public projections must stop exposing data immediately after a valid suspension or deletion request while background cleanup completes.
