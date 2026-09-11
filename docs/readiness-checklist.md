# Readiness and missing inputs

Items marked **Launch blocker** must be resolved before their dependent implementation or production launch. Credentials must be shared through a secure vault, never an issue or chat message.

## Commercial and ownership

- [ ] **Launch blocker:** signed statement of work, MVP exclusions, acceptance criteria, payment milestones, change-request process.
- [ ] Confirm intellectual-property ownership and repository handover terms.
- [ ] Confirm who pays recurring X, email, hosting, database, storage, monitoring, and domain costs.
- [ ] Name the client product owner with authority to approve rules and launch.
- [ ] Agree support, warranty, maintenance, and incident-response expectations.

## Product decisions

- [ ] **Launch blocker:** single-House versus multi-House membership.
- [ ] **Launch blocker:** Recruiter acceptance/removal/mission permissions.
- [ ] **Launch blocker:** invitation seat reservation and expiry.
- [ ] **Launch blocker:** waitlist ordering and selection.
- [ ] **Launch blocker:** contribution evidence and verification authority.
- [ ] **Launch blocker:** scoring v1 values, anti-abuse limits, weight-change policy, and tie-breaker.
- [ ] Define role changes, Owner suspension/succession, and eliminated-House behavior.
- [ ] Define appeals, reputation corrections, and moderation service levels.

## Client-owned accounts and access

- [ ] **Launch blocker:** production domain and DNS control.
- [ ] **Launch blocker:** client-owned X account, Developer Console app, OAuth 2.0 access, billing, and confirmed `public_metrics.followers_count` response.
- [ ] **Launch blocker:** transactional email account and verified sending domain.
- [ ] Managed PostgreSQL organization/project with backups.
- [ ] Hosting organization/project and billing.
- [ ] Object storage if evidence uploads are included.
- [ ] Error monitoring and product analytics accounts.
- [ ] Password manager or secure vault for access handoff.

## X values to prepare

- [ ] Development, staging, and production callback URLs.
- [ ] OAuth Client ID and Client Secret stored only in environment secrets.
- [ ] Minimal scopes: `users.read`, `tweet.read`, and optionally `offline.access`.
- [ ] Privacy policy, terms, and website URLs required by the app configuration.
- [ ] Data deletion/disconnection procedure matching X policy.
- [ ] Spending cap and alerting; avoid uncontrolled auto-recharge during development.

## Email and domain

- [ ] Sender name and addresses such as `invite@`, `notifications@`, and `support@`.
- [ ] SPF, DKIM, and DMARC records.
- [ ] Invitation, decision, seat-available, mission, reputation, season, and security templates.
- [ ] Delivery, bounce, and complaint webhook configuration.
- [ ] Email retention and notification preference rules.

## Brand and content

- [ ] Logo/source files, color direction, typography, and usage guidance.
- [ ] Neutral emblem system for House #01 through House #100.
- [ ] Approved homepage and onboarding copy.
- [ ] Owner application, pledge, Recruiter, and Shitposter application questions.
- [ ] Empty-state, decision, removal, suspension, and safety copy.
- [ ] Responsive wireframes for all critical journeys.

## Legal, privacy, and trust

- [ ] **Launch blocker:** privacy policy and terms reviewed by appropriate counsel.
- [ ] Community guidelines and prohibited engagement rules.
- [ ] Moderation, appeal, suspension, deletion, and retention policies.
- [ ] Data inventory and subprocessor list.
- [ ] Minimum-age and geographic availability decisions.
- [ ] Public explanation of scoring and correction processes.

## Operations

- [ ] Named platform Admins with MFA.
- [ ] Separate development, staging, and production environments.
- [ ] Backup schedule, retention, point-in-time recovery, and restoration drill.
- [ ] Incident severity and response contacts.
- [ ] Support channel and response expectations.
- [ ] Launch-day moderation and X/email provider monitoring coverage.

## Test materials

- [ ] Controlled Admin, Owner, Recruiter, Shitposter, Soldier, Analyst, suspended, eligible-X, and ineligible-X accounts.
- [ ] Clearly labeled staging fixtures for Houses at 0, 47, 49, and 50 members.
- [ ] Test mailboxes across common providers.
- [ ] Supported browsers/devices and accessibility targets.
- [ ] Client acceptance-test owners and schedule.
