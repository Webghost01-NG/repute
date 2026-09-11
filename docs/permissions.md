# Permissions model

Every permission is evaluated server-side. `Own House` means the actor has an active authorized role in the resource's House; it never means a House ID supplied by the browser is trusted.

| Capability | Visitor | Analyst | Soldier | Shitposter | Recruiter | Owner | Admin |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Browse public profiles/Houses/rankings | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Submit public feedback | No | Yes | Yes | Yes | Yes | Yes | Yes |
| Apply for House ownership | No | Yes | Yes | Yes | Yes | Yes* | Yes* |
| Submit House pledge | No | Yes | Yes* | Yes* | Yes* | No | Yes* |
| Join House waitlist | No | Yes | Yes* | Yes* | Yes* | No | Yes* |
| Submit own contribution | No | Yes | Yes | Yes | Yes | Yes | Yes |
| Participate in eligible mission | No | Yes | Yes | Yes | Yes | Yes | Yes |
| View private own-House workspace | No | No | Yes | Yes | Yes | Yes | Yes |
| Review membership applications | No | No | No | No | Own House | Own House | Yes |
| Accept/reject applicants | No | No | No | No | TBD | Own House | Yes |
| Remove House members | No | No | No | No | TBD | Own House | Yes |
| Record proactive recruitment | No | No | No | No | Own House | Own House | Yes |
| Nominate capped House roles | No | No | No | No | No | Own House | Yes |
| Create House mission | No | No | No | No | TBD | Own House | Yes |
| Customize permitted House profile | No | No | No | No | No | Own House | Yes |
| Approve House Owner application | No | No | No | No | No | No | Yes |
| Assign/suspend House | No | No | No | No | No | No | Yes |
| Suspend user or change platform role | No | No | No | No | No | No | Yes |
| Publish admin mission/project | No | No | No | No | No | No | Yes |
| Configure scoring drafts | No | No | No | No | No | No | Yes |
| Publish scoring version | No | No | No | No | No | No | Yes |
| Start/lock/end season | No | No | No | No | No | No | Yes |
| Make audited score adjustment | No | No | No | No | No | No | Yes |

`*` Subject to the final single-House and repeated-application rules. `TBD` is intentionally blocked by product decisions rather than silently granting power.

## Enforcement rules

- Platform Admin is a platform-scoped grant, not a self-selectable profile field.
- House roles derive from active membership records; clients cannot submit their own role.
- Owner operations are restricted to the assigned House.
- Recruiter permissions must be finalized before implementation and should use named capabilities, not an all-purpose manager role.
- Role, suspension, scoring, and moderation changes require a reason and audit record.
- Admin UI routes require authorization, but the same policy is repeated in every underlying command/API.
- Read permissions distinguish public projections from private applications, email addresses, evidence, moderation notes, and OAuth credentials.
