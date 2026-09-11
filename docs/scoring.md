# Reputation and House scoring

## Principles

- Follower count is an Owner-application eligibility signal only; it awards zero reputation and zero House score.
- Scores are consequences of recorded activity, verification, quality, outcomes, and consistency.
- Every displayed total must be explainable from its events and rule version.
- Corrections are additive reversals, not silent history edits.
- Published rules are immutable and visible to participants.
- Admin discretion is possible only through reasoned, audited adjustments.

## Reputation categories

Initial configurable categories:

- Talent Discovery
- Research
- Distribution
- Content and Creativity
- Feedback and Analysis
- Community Building
- Execution
- Project Support

Roles do not lock categories. A Soldier can build Talent Discovery reputation; an Owner can build Feedback reputation. “Known for” is derived from sufficient evidence, recency, consistency, and relative category strength.

## Reputation event model

A verified activity produces one or more category events:

```text
event value = base value
            × verification multiplier
            × quality multiplier
            × outcome multiplier
            × diminishing-repeat factor
```

Initial bounded dimensions should use small, understandable ranges. For example, verification may be unverified/pending/verified, quality may be 0–3, and outcome may be 0–3. Exact values remain a product decision and must be tested against abuse scenarios before publication.

Consistency should be calculated as a separate rolling signal, not an endlessly compounding multiplier. Repeated identical low-value activity should receive diminishing or zero incremental value.

## Recruiter signals

- Recruitment rationale recorded
- Invitation accepted
- Recruit retained for a configured period
- Recruit produces verified contributions
- Recruit develops strong category reputation

Recruiters do not receive full credit merely for sending invitations.

## Feedback signals

- Feedback submitted
- Feedback passes moderation and specificity checks
- Subject marks observation useful
- Recommendation is accepted
- Documented improvement or outcome occurs

Subjects cannot repeatedly inflate a collaborator without detection and review.

## House score categories

- Verified contribution
- Mission outcomes
- Recruitment quality
- Legitimate distribution
- Consistency
- Project support
- Community activity
- Verified outcomes
- House performance adjustments

The House total is a weighted sum of category subtotals under a published rule version. The public breakdown shows raw signal, weight, resulting value, and source events.

## Configuration lifecycle

```text
draft -> validated -> scheduled -> active -> retired
```

- Drafts are editable by authorized Admins.
- Validation runs schema, bounds, and abuse-scenario checks.
- Scheduled versions have an effective time and visible change summary.
- Active versions are immutable.
- Retired versions remain available for historical explanations.

Changing an active season's weights should be prohibited by default. If the client allows it, the platform must announce the version, preserve the previous rankings, and execute an audited deterministic recomputation.

## Ranking lifecycle

- Rebuild score projections from ledger events.
- Generate periodic immutable ranking snapshots.
- Display last-calculated time and category breakdown.
- Flag suspicious activity without automatically accusing users.
- Lock scoring at season close.
- Resolve ties using a pre-published deterministic rule.
- Have Admin confirm the top 50 before final statuses are written.

## Anti-abuse baseline

- Idempotency and duplicate-evidence detection
- Per-activity/category rate limits
- Diminishing value for repetitive activity
- Conflict-of-interest signals for reciprocal reviews
- Manual review queue for anomalous velocity or concentration
- Reversible events and moderation cases
- No score from forced likes, reposts, replies, or other prohibited engagement
