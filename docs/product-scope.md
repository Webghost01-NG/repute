# MVP product scope

## Product objective

Repute makes demonstrated ability discoverable. It organizes people into Houses, records legitimate work and outcomes, and produces public category-specific reputation and House track records.

The activation loop is:

1. A person connects a real X identity.
2. They join a House or participate as a Public Analyst.
3. They perform and record legitimate contributions.
4. Contributions are reviewed or verified.
5. Reputation categories and House scores update transparently.
6. People and Houses become discoverable by demonstrated ability.

## Success criteria for the MVP

- A real user can authenticate and connect exactly one X account.
- X public metrics can enforce the 5,000-follower Owner eligibility threshold without making it an approval decision.
- Admin can assign approved applicants to one of exactly 100 neutral House slots.
- A user can apply, be reviewed, receive an email invitation, and join a House.
- Concurrent requests can never create a 51st active House member.
- Owner, Recruiter, member, Analyst, and Admin permissions are isolated server-side.
- Contributions produce explainable, versioned reputation and House score events.
- Admin can operate Season 01, missions, projects, moderation, and scoring without database access.
- Public profiles and House pages explain reputation and ranking from historical evidence.
- Critical flows work on mobile, tablet, and desktop and have loading, empty, error, and success states.

## MVP capabilities

### Identity and onboarding

- Email-based user account and verified email address
- X OAuth 2.0 account connection and disconnection
- Storage of consented public X profile fields
- Public user profile and onboarding state
- Account suspension and data-deletion workflow

### Houses and membership

- Exactly 100 neutral House slots for Season 01
- Owner eligibility and application workflow
- Admin review, rejection, approval, and slot assignment
- Public House directory and profile
- Pledges/applications, proactive recruitment notes, and role applications
- Secure email invitations with status and expiry
- Transaction-safe total and role capacity limits
- Membership removal, waitlist, and seat-available notifications
- Recruitment and membership history

### Contribution and reputation

- Contribution submission, evidence, moderation, verification, and reversal
- Category-specific reputation ledger and summaries
- Public contribution and reputation history
- Known-for/strongest-category discovery
- Public Analyst feedback and outcome tracking

### Competition

- Configurable 30-day season lifecycle
- Versioned, transparent House scoring rules
- Score ledger, breakdowns, rankings, and suspicious-activity review
- Admin determination of survivors, eliminated Houses, and Founding Houses

### Missions and projects

- Admin-recommended and House-created optional missions
- Mission participation and completion review
- Empty project catalog at launch
- Admin project CRUD and publication controls
- Optional House-project support records

### Operations

- In-app notification inbox and important email notifications
- Admin dashboard for users, Houses, membership, season, missions, projects, reputation, analytics, and moderation
- Append-only audit trail for security- and reputation-relevant actions
- Rate limiting, input validation, protected routes, logging, monitoring, and backups

## Explicitly out of scope

- Wallet connection
- Tokens, tokenomics, presales, NFTs, or marketplaces
- Fake influencers, fake activity, or fake projects
- Automated liking, reposting, following, replying, or direct messaging
- Engagement rings, forced actions, trend manipulation, or mass posting
- Native mobile applications
- Algorithmic machine-learning reputation models
- Multi-season historical simulations before real Season 01 data exists

## Primary personas

- Visitor: browses public Houses, rankings, profiles, and activity.
- Public Analyst: submits feedback and builds analysis reputation without joining a House.
- Soldier: contributes as a general House member.
- Shitposter: contributes creative distribution within safety rules; maximum 10 per House.
- Recruiter: discovers and reviews talent; maximum 2 per House.
- House Owner: leads one House and manages its permitted operations.
- Platform Admin: manages the platform and performs audited interventions.

## Critical end-to-end journeys

1. Sign up, verify email, connect X, and publish profile.
2. Apply for House ownership, verify follower eligibility, receive admin decision, and receive a House slot.
3. Pledge to a House, receive review, receive an exclusive email invitation, and accept it.
4. Fill a House to 50, reject concurrent over-capacity acceptance, join the waitlist, free a seat, and notify candidates.
5. Nominate or apply for a capped role, approve it, and preserve role history.
6. Submit a contribution, review evidence, verify it, and generate reputation and score events.
7. Create or join a mission, submit completion, and record its outcome.
8. Submit public feedback, mark it useful or accepted, and update Analyst reputation.
9. Start a season, publish transparent rankings, lock scoring, resolve survivors, and designate Founding Houses.

## Demo data policy

Production begins with 100 neutral records named `House #01` through `House #100`, no projects, and no fabricated users or activity. Development and staging may contain clearly labeled synthetic test fixtures that can never be promoted to production.
