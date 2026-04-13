# Detection Rule: Credential Stuffing Velocity

> **Rule ID:** DR-001
> **Author:** Aisha Williams
> **Created:** 2024-06-15
> **Last tuned:** 2025-03-18
> **Status:** Active
> **Severity on trigger:** High

## Purpose

This rule detects automated credential stuffing attacks by identifying patterns of rapid failed authentication attempts that are characteristic of attackers testing stolen username/password pairs from breached credential databases against Prism accounts. Credential stuffing is the most common initial access vector for account takeover on the platform and the primary technique used by marketplace fraud rings and credential-trading networks.

**Threat addressed:** [credential-stuffing](../intelligence-index.yaml) (see intelligence index)
**MITRE ATT&CK technique(s):** T1110.004 (Brute Force: Credential Stuffing)
**Threat actor(s):** [Marketplace Fraud Rings](../threat-actors/marketplace-fraud-rings.md), [Scattered Spider](../threat-actors/scattered-spider.md)

## Detection Logic

**Plain language:** When the authentication service observes a high volume of failed login attempts from a single source (IP address, IP subnet, or device fingerprint) within a sliding time window, and the failures are spread across many distinct usernames (not a single user mistyping their password), trigger an alert. The rule distinguishes between a user who forgot their password (repeated failures on one account) and an attacker testing credentials across many accounts (failures spread across many accounts from one source).

**Technical implementation:**

```sql
-- Credential Stuffing Velocity Detection
-- Runs every 5 minutes against the auth_events stream
-- Looks for sources generating failed logins across many distinct accounts

SELECT
    source_identifier,          -- IP address or device fingerprint
    source_type,                -- 'ip' or 'device_fingerprint'
    COUNT(*) AS total_failures,
    COUNT(DISTINCT username) AS distinct_usernames,
    MIN(event_timestamp) AS window_start,
    MAX(event_timestamp) AS window_end,
    ARRAY_AGG(DISTINCT geo_country) AS countries,
    ARRAY_AGG(DISTINCT user_agent_family) AS user_agents
FROM auth_events
WHERE
    event_type = 'login_failed'
    AND event_timestamp >= NOW() - INTERVAL '10 minutes'
    AND failure_reason IN ('invalid_password', 'account_not_found')
    -- Exclude known good sources (internal monitoring, load testing)
    AND source_identifier NOT IN (SELECT identifier FROM allowlist_sources)
GROUP BY source_identifier, source_type
HAVING
    COUNT(*) >= 50                      -- Minimum failure volume threshold
    AND COUNT(DISTINCT username) >= 20   -- Minimum distinct username spread
    AND COUNT(DISTINCT username)::float / COUNT(*)::float >= 0.4  -- Username diversity ratio
ORDER BY total_failures DESC;
```

**Secondary signal (corroborating):**

```sql
-- Check if any of the targeted usernames appear in known breach databases
-- This is run as enrichment after the primary rule fires

SELECT
    b.breach_source,
    COUNT(*) AS matched_credentials
FROM auth_events a
JOIN breach_credential_index b ON a.username = b.username
WHERE
    a.source_identifier = :flagged_source
    AND a.event_timestamp >= :window_start
    AND a.event_type = 'login_failed'
GROUP BY b.breach_source;
```

## Data Sources

| Source | Field(s) Used | Latency | Reliability |
|---|---|---|---|
| Authentication event stream | event_type, username, source_ip, device_fingerprint, failure_reason, event_timestamp, geo_country, user_agent | <30 seconds | High — all auth events are captured |
| IP geolocation service | geo_country, geo_city, geo_asn | <100ms | Moderate — geolocation accuracy varies by IP type |
| Breach credential index | username, breach_source, breach_date | Daily sync | Moderate — coverage depends on breach database subscriptions |
| Allowlist sources table | identifier, reason, expiration | Real-time | High — manually maintained |

## Thresholds and Tuning

| Parameter | Current Value | Last Changed | Rationale |
|---|---|---|---|
| Time window | 10 minutes | 2024-06-15 | Balances detection speed against false positives from bursty legitimate traffic |
| Minimum failure count | 50 | 2025-03-18 | Raised from 30 after March 2025 credential stuffing campaign revealed that sophisticated attacks throttle to ~50-80 attempts per 10 min per IP |
| Minimum distinct usernames | 20 | 2025-01-10 | Raised from 10 to reduce false positives from corporate networks where multiple users share an egress IP |
| Username diversity ratio | 0.4 | 2024-09-22 | Added to filter out brute-force attacks against single accounts (low diversity) from credential stuffing (high diversity) |
| Evaluation frequency | 5 minutes | 2024-06-15 | Provides near-real-time detection without excessive query load |

### Tuning History

| Date | Parameter | Old Value | New Value | Reason |
|---|---|---|---|---|
| 2024-06-15 | Initial deployment | N/A | N/A | Rule created based on threat model for T1110.004 |
| 2024-08-03 | Min failure count | 20 | 30 | Excessive alerts from corporate VPN egress points during business hours |
| 2024-09-22 | Username diversity ratio | N/A | 0.4 | Added to distinguish credential stuffing from brute force against individual accounts |
| 2025-01-10 | Min distinct usernames | 10 | 20 | Corporate networks with 500+ employees behind single NAT were triggering the rule during Monday morning login surges |
| 2025-03-18 | Min failure count | 30 | 50 | March 2025 credential stuffing campaign (see [postmortem](../postmortems/2025-03-credential-stuffing-wave.md)) used distributed infrastructure throttled to ~60 attempts per IP per 10 min. Raised threshold to match the new attacker baseline while adding the subnet correlation rule (DR-001b) to catch distributed attacks |

## Known False Positive Patterns

| Pattern | Frequency | Mitigation |
|---|---|---|
| Corporate VPN/NAT egress — large organizations with hundreds of employees behind a single public IP generate high failure volumes during business hours (password resets, expired sessions) | 2-3 per week | Allowlist for known corporate egress IPs with regular review. Username diversity ratio filter catches most remaining cases since corporate failures are concentrated on a smaller set of usernames |
| Password manager sync failures — users with password managers that auto-fill incorrect saved credentials across multiple services | Rare | Filtered by the distinct username threshold (these failures are all against one username) |
| Automated integration testing — partner API integrations with misconfigured credentials | Monthly | Allowlisted by source IP with expiration dates |

## Response Procedure

1. **Triage (5 minutes):** Verify the alert is not a known false positive pattern. Check the source IP/fingerprint against the allowlist and the corporate egress IP list. Check the username diversity ratio to confirm the pattern is credential stuffing rather than brute force.

2. **Investigate (15 minutes):** Run the breach correlation query to determine if the targeted usernames appear in known breach databases. If there is a strong breach correlation, the confidence of the alert increases significantly. Check if any of the targeted accounts had successful logins from the same source (indicating some credentials were valid). Check for related activity from the same IP subnet or ASN.

3. **Contain (immediate if confirmed):** If credential stuffing is confirmed, block the source IP/subnet at the WAF level. If successful logins from the source are detected, flag those accounts for forced password reset and session revocation. If the attack is distributed across many IPs, escalate to the incident commander for broader containment (ASN-level blocking, emergency rate limit reduction).

4. **Escalate if:** The attack volume exceeds 10,000 attempts per hour across all sources, successful login rate from attacking sources exceeds 1% (indicating high-quality credential list), or the attack correlates with a newly published breach of a major service (suggesting a fresh credential dump in circulation).

5. **Playbook:** [ato-response.md](../incident-response/playbooks/ato-response.md) for confirmed account compromise. [mass-ato-response.md](../incident-response/playbooks/mass-ato-response.md) if the scale warrants a coordinated response.

## Performance Metrics

| Metric | Current Value | Target | Measurement Period |
|---|---|---|---|
| True positive rate | 94% | >90% | Q1 2025 |
| False positive rate | 6% | <10% | Q1 2025 |
| Mean time to triage | 8 minutes | <15 minutes | Q1 2025 |
| Alert volume (daily avg) | 3.2 alerts/day | <10/day | Q1 2025 |
| Attacks blocked before account compromise | 87% | >85% | Q1 2025 |

## Related Artifacts

| Type | Link |
|---|---|
| Intelligence index entry | [credential-stuffing](../intelligence-index.yaml) |
| Companion rule | DR-001b: Subnet-correlated credential stuffing (detects distributed attacks across an IP subnet) |
| Companion rule | DR-002: Breached credential match (proactive block of known-breached passwords at login) |
| Companion rule | DR-003: Impossible travel login (detects successful logins from geographically improbable locations) |
| Controls | [rate-limiting.md](../detections-and-controls/controls/rate-limiting.md), [credential-breach-blocklist.md](../detections-and-controls/controls/credential-breach-blocklist.md) |
| Postmortem | [2025-03-credential-stuffing-wave.md](../postmortems/2025-03-credential-stuffing-wave.md) |
| MITRE coverage | T1110.004 in [technique-coverage.yaml](../compliance-and-frameworks/mitre-attack/technique-coverage.yaml) |
