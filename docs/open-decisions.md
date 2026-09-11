# Open product decisions

These decisions must be made explicitly. The temporary recommendation is included to prevent accidental product rules from emerging in code.

| ID | Decision | Recommended default | Needed by |
| --- | --- | --- | --- |
| PD-01 | House membership cardinality | One active House per user | Schema approval |
| PD-02 | Concurrent House applications | Allow several applications; close others only after invitation acceptance | Membership build |
| PD-03 | Recruiter powers | Review and recommend; Owner makes final acceptance/removal in v1 | Permission approval |
| PD-04 | Invitation seat reservation | Do not reserve; recheck capacity on acceptance | Invitation build |
| PD-05 | Invitation expiry | Seven days, Admin configurable within bounded limits | Invitation build |
| PD-06 | Waitlist order | Chronological presentation with manual candidate review | Waitlist build |
| PD-07 | Multiple House roles | One current functional role per House; category reputation remains unrestricted | Schema approval |
| PD-08 | Owner succession | Suspend management and require audited Admin reassignment | Admin build |
| PD-09 | Contribution verification | Category-specific reviewer policies with conflict-of-interest signals | Reputation build |
| PD-10 | Scoring changes mid-season | Prohibit after season start except audited emergency correction | Season build |
| PD-11 | Rank-50 ties | Pre-published ordered tie-breaker based on verified outcomes and consistency | Season start |
| PD-12 | Eliminated Houses | Preserve public track record; disable active-season operations pending next-season rule | Season end |
| PD-13 | Gmail requirement | Transactional email to any address, not Google-account connection | Email build |
| PD-14 | Evidence uploads | URLs at MVP launch; object uploads only if moderation/storage budget is approved | Contribution build |
| PD-15 | Reputation endorsements | No open peer point awards; use structured review/outcome signals | Reputation build |

## Decision record template

For each resolved item record:

- Decision and date
- Approver
- Context and alternatives
- User-visible consequences
- Data/schema consequences
- Security/abuse consequences
- Migration or rollout requirements
