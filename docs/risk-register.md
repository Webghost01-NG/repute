# Risk register

| Risk | Probability | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| X access, pricing, or profile fields differ from assumptions | High | Critical | Verify real OAuth and `followers_count` before identity sprint; isolate adapter | Client + Engineering |
| Product rules change after schema implementation | High | High | Approve open decisions and state machines before migrations | Product owner |
| Concurrent joins create member 51 | Medium | Critical | Database-owned locked transaction plus concurrency integration tests | Engineering |
| House leaders manufacture reputation | High | High | Structured evidence, reviewer conflicts, rate limits, anomaly queue, reversals | Product + Trust |
| Admin abuse or account compromise | Medium | Critical | MFA, least privilege, step-up checks, reasons, immutable audit trail | Operations |
| Email invitations are leaked or replayed | Medium | High | Intended identity, hashed one-time token, short expiry, revocation, capacity recheck | Engineering |
| Public reputation causes disputes or privacy harm | High | High | Transparent evidence, correction/appeal process, moderation, deletion policy | Legal + Trust |
| Scoring changes undermine competition trust | Medium | High | Versioned public rules, immutable active versions, ranking snapshots | Product |
| Scope exceeds budget and schedule | High | High | Signed MVP, milestones, change control, explicit exclusions | Client + Delivery |
| Fake/demo data reaches production | Low | High | Environment-separated seeds and production allowlist | Engineering |
| Provider outage delays invitations or OAuth | Medium | Medium | Durable jobs, retries, status visibility, runbooks | Engineering |
| Public launch attracts spam and harassment | High | High | Rate limits, reporting, moderation queue, community rules, launch staffing | Trust + Operations |
| Client-owned accounts are not ready | High | High | Readiness gate and named account owner | Client |
| Analytics or logs expose sensitive data | Medium | High | Data minimization, redaction, access controls, retention limits | Engineering |
| Season-end job produces disputed result | Medium | Critical | Deterministic simulation, scoring lock, snapshots, Admin confirmation | Product + Engineering |
