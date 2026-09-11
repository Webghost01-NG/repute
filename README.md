# Repute

Repute is a contribution-driven Web3 social reputation and House competition platform.

> Don't tell us what you're good at. Show us.

> Attention gets you noticed. Reputation tells people why you matter.

Crypto Twitter contains people with very different abilities: talent discovery, research, content, distribution, analysis, community building, and execution. Those abilities are usually collapsed into follower counts and impressions. Repute gives people a structured place to demonstrate their abilities, records what they actually contribute, and turns that evidence into category-specific public reputation.

The competition is the activation layer. The long-term product is the track record.

## Project status

**Current phase:** Product definition and architecture planning.

The application has not been scaffolded or implemented yet. This repository currently contains the approved working proposal, delivery backlog, risk analysis, and engineering workflow. Architecture and product rules must be reviewed before implementation begins.

The GitHub backlog is organized into seven milestones covering readiness through launch. Dates are tentative until the client completes the readiness gate.

## Table of contents

- [Product model](#product-model)
- [Season 01](#season-01)
- [Roles](#roles)
- [Core product journeys](#core-product-journeys)
- [MVP capabilities](#mvp-capabilities)
- [Explicit exclusions](#explicit-exclusions)
- [Architecture](#architecture)
- [System modules](#system-modules)
- [Data integrity](#data-integrity)
- [Security model](#security-model)
- [Reputation and scoring](#reputation-and-scoring)
- [Delivery roadmap](#delivery-roadmap)
- [Repository documents](#repository-documents)
- [Development workflow](#development-workflow)
- [Testing and release gates](#testing-and-release-gates)
- [External services and missing inputs](#external-services-and-missing-inputs)
- [Data and demo policy](#data-and-demo-policy)

## Product model

Repute is built around the following loop:

```text
X identity
   ↓
House membership or Public Analyst participation
   ↓
Recorded contribution and supporting evidence
   ↓
Review, verification, usefulness, and outcomes
   ↓
Category-specific reputation and House score events
   ↓
Public track records, discovery, and opportunities
```

Follower count can help determine whether somebody is eligible to apply as a House Owner. It does not award reputation or House points. A smaller account with repeated useful outcomes can build stronger reputation than a much larger account.

## Season 01

Season 01 has fixed headline rules:

| Rule | Value |
| --- | ---: |
| House slots | Exactly 100 |
| Season duration | 30 days |
| Maximum active members per House | 50 total |
| Surviving Houses | 50 |
| Eliminated Houses | 50 |
| Founding Houses | First 50 survivors |
| Maximum total participants across full Houses | 5,000 |

All 100 Houses initially have neutral identities: `House #01` through `House #100`. A House becomes associated with a real X identity only when an eligible Owner applicant is manually approved and assigned by Repute Admin.

The 50-person capacity includes every active House role. A valid full House might contain one Owner, two Recruiters, ten Shitposters, and thirty-seven Soldiers. No application, invitation, role change, or Admin action may create member 51.

## Roles

### Platform Admin

Admin operates Repute across Houses, users, applications, seasons, scoring, missions, projects, moderation, analytics, notifications, and audit history. Sensitive operations require elevated authorization, a reason, and an immutable audit event.

### House Owner

An Owner connects X, has at least 5,000 followers when eligibility is checked, submits an application, and receives a manual Admin decision. The threshold permits an application; it never guarantees approval. An approved Owner manages only their assigned House.

### Recruiter

A House can have no more than two active Recruiters. Recruiters discover and evaluate talent, preserve recruitment rationale, and build reputation from recruit outcomes—not from invitation volume. Their exact acceptance, removal, and mission-management powers remain an explicit product decision.

### Shitposter

A House can have no more than ten active Shitposters. The role turns legitimate House activity and ideas into creative attention and distribution. It must not enable spam, harassment, misinformation, artificial engagement, forced actions, copy/paste campaigns, or trend manipulation.

### Soldier

Soldiers are general contributors, not a lesser class. They can demonstrate research, content, education, memes, project discovery, support, feedback, distribution, community work, missions, and execution.

### Public Analyst / Feedbacker

People outside Houses can analyze Houses, campaigns, projects, strategies, and Repute itself. Useful observations, accepted recommendations, consistency, and outcomes can build Feedback and Analysis reputation. There is no artificial 500-person participation limit.

## Core product journeys

1. A user signs up, verifies email, connects X, and completes a public profile.
2. An eligible user submits a House Owner application; Admin reviews it and assigns a neutral House slot if approved.
3. A user pledges to a House, House staff reviews the application, and acceptance sends a secure email invitation.
4. The intended user follows the exclusive link; the server rechecks identity, expiry, eligibility, and capacity before joining.
5. A full House exposes a waitlist. When a committed removal frees capacity, relevant candidates and House staff are notified.
6. Members or Analysts record contributions and evidence. Authorized review produces quality and outcome signals.
7. Verified activity creates immutable category reputation and House score events under a published rule version.
8. Admin starts, operates, locks, and completes Season 01; deterministic rules produce 50 survivors and 50 eliminated Houses.

## MVP capabilities

### Public application

- Emotional homepage and current Season 01 progress
- Dedicated searchable/filterable House directory
- Public House track records, capacity, rankings, and score explanations
- People discovery by demonstrated reputation categories
- Public profiles and contribution histories
- Missions and optional project discovery/support records
- Public Analyst feedback

### Authenticated user experience

- Verified email account and secure sessions
- Official X OAuth 2.0 connection
- Owner, role, and House membership applications
- Invitation acceptance and waitlist management
- Contribution and evidence submission
- Mission participation and feedback
- In-app notifications and preferences

### House workspace

- Applications and recruitment prospects
- Invitation statuses and waitlist
- Member roster, capacity, role history, and permitted removals
- House activity, missions, contributions, reputation, score, and performance
- Configurable public House information within Admin-defined limits

### Admin application

- House application review and slot assignment
- Users, X snapshots, suspensions, Houses, membership, roles, removals, invitations, and waitlists
- Season lifecycle, rankings, survivors, eliminated Houses, and Founding status
- Versioned reputation and House scoring rules
- Mission and project publication controls
- Moderation, appeals, suspicious-activity review, analytics, audit, job, email, and provider operations

## Explicit exclusions

The initial MVP does not include:

- Wallet connection
- NFTs or NFT marketplace
- Tokens, tokenomics, presales, or token marketplace
- Fake influencer identities
- Fake project listings or fabricated production activity
- Automated X posting, liking, reposting, following, or replying
- Forced or coordinated fake engagement
- Native mobile applications
- Machine-learning reputation ranking

The internal identity model leaves room for a future wallet connection without exposing wallet UI or functionality today.

## Architecture

The proposed MVP uses a **modular monolith**. A single deployable application provides the responsive interface, server-rendered public content, authenticated dashboards, application services, and HTTP endpoints. PostgreSQL is the source of truth. Durable background work delivers emails and notifications through provider adapters.

| Concern | Proposed baseline |
| --- | --- |
| Application | Next.js, React, TypeScript |
| Database | Managed PostgreSQL |
| Data access | Prisma |
| Authentication | Auth.js and server-owned application authorization |
| X integration | OAuth 2.0 Authorization Code with PKCE |
| Validation | Zod at server boundaries |
| Email | Resend or Postmark behind a provider interface |
| Jobs | PostgreSQL-backed durable job/outbox worker |
| Interface | Tailwind CSS with accessible UI primitives |
| Testing | Vitest, React Testing Library, Playwright |
| Operations | Structured logs, error monitoring, analytics, alerts, backups |

This baseline remains a proposal until the architecture issue and client-owned providers are approved. Dependencies and versions will be selected during the foundation milestone rather than guessed in planning documents.

### Request and event path

```text
Browser
  -> route/page
  -> authentication and authorization guard
  -> server-side validation
  -> module application service
  -> PostgreSQL transaction
  -> domain event + audit event + outbox job
  -> response

Worker
  -> safely claims job
  -> calls email/X/internal adapter
  -> records provider result
  -> retries or exposes dead-letter state
```

## System modules

- **Identity:** users, verified emails, sessions, X accounts, consent, suspension, deletion.
- **Houses:** slots, applications, assignments, memberships, roles, pledges, prospects, waitlists.
- **Invitations:** secure issuance, delivery, intended-user acceptance, expiry, revocation, retry.
- **Contributions:** submissions, evidence, reviews, outcomes, disputes, moderation.
- **Reputation:** categories, immutable events, summaries, known-for derivation, corrections.
- **Seasons:** lifecycle, House participation, scoring lock, final status.
- **Scoring:** published rule versions, House score ledger, projections, explanations, adjustments.
- **Missions:** Admin recommendations, House missions, participation, completion review.
- **Projects:** initially empty catalog, publication, House discovery/support records.
- **Feedback:** public analysis, usefulness, accepted recommendations, outcomes.
- **Notifications:** in-app inbox, preferences, transactional email delivery.
- **Administration:** privileged workflows, analytics, moderation, provider operations.
- **Audit:** append-only security and business-event history.

Modules communicate through application services and durable domain events. Browser code never writes directly to database tables or decides authorization.

## Data integrity

The database—not only the interface—must enforce the critical business rules:

- Exactly 100 Season 01 House slots
- One active Owner per House
- No more than two active Recruiters per House
- No more than ten active Shitposters per House
- No more than fifty active members of all roles combined
- One Repute user per stable X user ID
- One-use, expiring, revocable invitation tokens bound to their intended identity
- Immutable published scoring versions
- Compensating reputation/score events instead of silent historical edits

Membership acceptance runs in one locked transaction. It rechecks House state, user eligibility, active membership, invitation validity, total capacity, and role capacity before writing membership, invitation, notification, and audit changes atomically. Concurrent attempts cannot produce member 51.

## Security model

- Authentication is not authorization; every protected command checks current server-side policy.
- House operations include the authorized House scope in database predicates.
- Clients cannot submit trusted roles or promote themselves.
- Admin privileges use least privilege, MFA expectations, step-up checks, and audit reasons.
- OAuth uses state, PKCE, exact callback URLs, minimal scopes, and protected tokens.
- Invitations store only cryptographic token hashes and reject replay.
- Untrusted text and URLs receive server validation; arbitrary HTML is not accepted.
- Authentication, application, invitation, feedback, and expensive endpoints are rate-limited.
- Logs, analytics, errors, job views, and audit records redact secrets and sensitive fields.
- Backups, restoration, data export, disconnection, and deletion are tested before launch.

Security reports should use the repository's private security-advisory link rather than a public issue.

## Reputation and scoring

Reputation is a set of category track records, not one universal popularity score. Initial configurable categories are:

- Talent Discovery
- Research
- Distribution
- Content and Creativity
- Feedback and Analysis
- Community Building
- Execution
- Project Support

A role does not lock a category. For example, a Soldier who repeatedly discovers successful contributors may build Talent Discovery reputation.

Verified activity produces an explainable event under a published scoring version:

```text
event value = base value
            × verification multiplier
            × quality multiplier
            × outcome multiplier
            × diminishing-repeat factor
```

Exact values are intentionally unresolved until the product owner approves scoring v1 and the team tests abuse scenarios. Every score event records its source, category, rule version, breakdown, verification state, timestamp, and any reversal.

## Delivery roadmap

The working estimate is **12–16 weeks for two experienced full-stack engineers with part-time design/QA**, or approximately **18–24 weeks for one engineer**, after the readiness gate. External provider approval and delayed client decisions can extend calendar time.

| Milestone | Outcome | Tentative target |
| --- | --- | --- |
| M0 — Product decisions and readiness | Resolve rules, access, UX, ownership, privacy, and threats | 18 Sep 2026 |
| M1 — Platform foundation | Identity, X, database, RBAC, audit/outbox, CI, 100 slots | 2 Oct 2026 |
| M2 — House lifecycle and membership | Owner approval, Houses, invitations, capacity, roles, removal, waitlist | 23 Oct 2026 |
| M3 — Contributions, reputation, and discovery | Evidence, verification, reputation, profiles, discovery, feedback | 6 Nov 2026 |
| M4 — Seasons, scoring, missions, and projects | Competition, rankings, finalization, missions, project infrastructure | 20 Nov 2026 |
| M5 — Administration and operations | Complete Admin, analytics, moderation, notifications, provider operations | 4 Dec 2026 |
| M6 — Hardening and launch | Security, accessibility, performance, recovery, UAT, controlled launch | 18 Dec 2026 |

These are planning targets, not a promise independent of scope approval, staffing, X access, domain/email readiness, and client response time.

## Repository documents

- [MVP product scope](docs/product-scope.md) — product outcomes, boundaries, personas, and critical journeys.
- [System architecture](docs/architecture.md) — technical baseline, modules, request flow, environments, security, and scaling.
- [Data model and invariants](docs/data-model.md) — conceptual entities, constraints, membership transaction, and history.
- [Permissions model](docs/permissions.md) — role/capability matrix and enforcement rules.
- [Reputation and House scoring](docs/scoring.md) — scoring philosophy, ledgers, configuration lifecycle, and anti-abuse controls.
- [Delivery roadmap](docs/roadmap.md) — milestone outcomes, exit gates, dependency order, and estimate.
- [Testing strategy](docs/testing.md) — test layers, all twenty required acceptance flows, and release gates.
- [Readiness checklist](docs/readiness-checklist.md) — commercial, product, account, domain, email, legal, design, operational, and test inputs still needed.
- [Open product decisions](docs/open-decisions.md) — fifteen unresolved rules with recommended defaults and decision deadlines.
- [Risk register](docs/risk-register.md) — product, provider, security, delivery, reputation, and operational risks.

## Development workflow

Implementation will follow GitHub issues and milestone order.

1. Read this README, the relevant planning documents, and the assigned issue.
2. Check the worktree and synchronize `main`:

   ```bash
   git status --short --branch
   git fetch --all --prune
   git switch main
   git pull --ff-only
   ```

3. Create one focused branch:

   ```bash
   git switch -c feat/short-description
   ```

4. Implement only the issue's approved scope.
5. Run the required format, lint, typecheck, unit, integration, build, and end-to-end checks introduced during M1.
6. Review the entire diff and confirm no credential, real private data, or fabricated external result is present.
7. Open a pull request using the repository template. Include intent, verification results, security/data effects, risks, and UI screenshots where applicable.

Never implement directly on `main`. Never merge your own pull request without explicit authorization. Architecture, dependency, schema, API-contract, CI/CD, environment, or security changes require explicit review.

## Testing and release gates

Testing includes unit, database-integration, provider-integration, component, browser end-to-end, security, accessibility, concurrency, and load coverage.

Before launch, the release candidate must pass the twenty requested product areas:

1. Authentication
2. X connection
3. House Owner application
4. Admin approval
5. House membership
6. Fifty-member capacity
7. Recruiter permissions
8. Shitposter permissions
9. Member removal
10. Waitlist
11. Invitation generation and verification
12. Real staging email flow
13. Reputation updates and corrections
14. House scoring and explanation
15. Missions
16. Public feedback
17. Project Admin controls and empty production state
18. Admin dashboard
19. Mobile/tablet/desktop responsiveness and accessibility
20. Unauthorized and cross-House access

Launch additionally requires clean migrations, a successful backup-restoration drill, verified email authentication, verified X fields and cost behavior, no unresolved critical/high security defects, and signed client acceptance.

## External services and missing inputs

The client should own production accounts and billing. Credentials must be shared through a secure vault and stored only in managed environment secrets.

Primary external requirements include:

- Production domain and DNS control
- Client-owned X Developer application with verified OAuth and `public_metrics.followers_count`
- Transactional email account and verified sending domain with SPF, DKIM, and DMARC
- Managed PostgreSQL with backups and recovery capability
- Hosting organization and deployment access
- Object storage if direct evidence uploads are approved
- Error monitoring and product analytics
- Password manager or secure access-sharing process
- Privacy policy, terms, community guidelines, moderation/appeal policy, and data-retention rules
- Brand source files, neutral House emblem direction, approved copy, application questions, and responsive wireframes
- Controlled test accounts for all roles and X eligibility cases

See the [readiness checklist](docs/readiness-checklist.md) for the complete actionable list. Do not place credentials in GitHub issues.

## Data and demo policy

Production begins with exactly 100 neutral Houses and no projects, users, applications, missions, contributions, scores, or activity fabricated for appearance.

Development and staging may use clearly labeled synthetic fixtures for testing, including Houses at 0, 47, 49, and 50 members. Fixture tooling must refuse to run against production. External integration success must be verified with authorized staging services; it must never be invented or reported from a local fake.

## License

No open-source license has been granted yet. Although the repository is public, all rights remain with the copyright holder unless and until the project owner adds an explicit license after confirming client and intellectual-property terms.
