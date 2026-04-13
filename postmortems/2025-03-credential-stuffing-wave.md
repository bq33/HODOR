# Postmortem: March 2025 Credential Stuffing Wave

> **Date of incident:** 2025-03-12 through 2025-03-14
> **Date of postmortem:** 2025-03-19
> **Severity:** SEV-2
> **Incident commander:** James Okafor
> **Author:** Aisha Williams
> **Status:** Final

## Executive Summary

Between March 12 and March 14, 2025, Prism experienced a sustained credential stuffing campaign that tested approximately 2.8 million stolen credential pairs against the platform's authentication endpoint. The attack originated from a distributed network of residential proxy IPs, throttled to stay below existing detection thresholds for the first 18 hours before the pattern was identified. Approximately 34,000 accounts were successfully accessed before containment. Of those, 8,200 showed evidence of post-compromise activity (payment method harvesting, unauthorized purchases, or account detail changes). No customer payment card data was exfiltrated from Prism's systems, though attackers used stored payment methods for approximately $142,000 in fraudulent purchases, of which $118,000 was recovered through transaction reversal.

## Impact

| Metric | Value |
|---|---|
| Duration (detection to resolution) | 54 hours (18h undetected + 36h active response) |
| Total credential pairs tested | ~2.8 million |
| Accounts successfully accessed | 34,000 (~1.2% success rate) |
| Accounts with post-compromise activity | 8,200 |
| Fraudulent purchase volume | $142,000 |
| Recovered through reversal | $118,000 |
| Net fraud loss | $24,000 |
| Forced password resets issued | 34,000 |
| Customer notification emails sent | 34,000 |
| Regulatory notifications required | None (no PII exfiltration from Prism systems) |

## Timeline

All times in UTC.

| Time (UTC) | Event |
|---|---|
| Mar 12 04:00 | Estimated start of the credential stuffing campaign based on retrospective log analysis |
| Mar 12 04:00-22:00 | Attack proceeds at low velocity (~50-70 attempts per IP per 10 minutes) across approximately 800 residential proxy IPs. Stays below DR-001 threshold of 30 failed logins per source. No alerts generated |
| Mar 13 08:15 | Darnell Brooks notices an unusual uptick in "suspicious login" tickets in the fraud ops queue during morning triage. Multiple buyers reporting unauthorized purchases they didn't make |
| Mar 13 08:45 | Darnell escalates to Aisha Williams in #detection-engineering. Initial hypothesis is account takeover but volume seems higher than normal |
| Mar 13 09:30 | Aisha runs ad-hoc query against auth_events and identifies the distributed credential stuffing pattern. The attack is spread across 800+ IPs with each IP individually below detection thresholds, but the aggregate pattern is clear. Incident declared as SEV-2 |
| Mar 13 09:45 | James Okafor assumes incident commander role. War room opened in #security-incidents |
| Mar 13 10:00 | Aisha identifies the credential source: the usernames being tested correlate strongly with a major retail platform breach disclosed in January 2025. Users who reused passwords from that platform are the primary victims |
| Mar 13 10:30 | First containment action: emergency rate limit reduction on authentication endpoint from 20 req/min to 5 req/min per IP. This slows the attack but does not stop it due to the distributed IP pool |
| Mar 13 11:00 | Second containment action: Kenji Tanaka deploys an emergency detection model that flags authentication attempts where the username appears in the January 2025 breach database. These attempts are routed to a CAPTCHA challenge |
| Mar 13 12:00 | Attack velocity drops 85% as the CAPTCHA challenge blocks automated attempts. Remaining attempts appear to be using CAPTCHA-solving services |
| Mar 13 14:00 | Third containment action: all accounts that had successful logins from the identified residential proxy IP ranges are flagged for forced password reset and session revocation. 34,000 accounts identified |
| Mar 13 15:00 | Priya Sharma begins building the ASN-level correlation to identify additional proxy IPs not yet in the block list |
| Mar 13 18:00 | Customer notification drafted and approved. 34,000 emails sent informing users of the forced reset and recommending MFA enrollment |
| Mar 14 02:00 | Attack effectively stopped. Residual attempts (<100/hour) continue from CAPTCHA-solving services but conversion rate is near zero |
| Mar 14 16:00 | All-clear declared. Monitoring period begins |
| Mar 18 09:00 | Monitoring period ends. No recurrence detected |

## Root Cause Analysis

**Immediate cause:** An attacker obtained a credential database from the January 2025 breach of a major retail platform and tested those credentials against Prism at scale. Approximately 1.2% of the tested credentials were valid on Prism, consistent with industry password reuse rates.

**Contributing factors:**

The attack succeeded in staying undetected for 18 hours because of a deliberate evasion strategy. The attacker distributed the campaign across approximately 800 residential proxy IPs and throttled each IP to 50-70 attempts per 10-minute window, which was below our detection rule threshold of 30 failed logins per source at the time. Our detection rule (DR-001) was designed to catch concentrated attacks from individual sources, not distributed attacks that stayed below per-source thresholds.

The 34,000 successfully accessed accounts all shared two characteristics: the users had reused passwords from the breached retail platform, and none of them had MFA enabled. Prism's MFA adoption rate is currently 23% across all accounts, meaning 77% of accounts are protected only by passwords.

**Systemic factors:**

The team had discussed adding a subnet-level and ASN-level correlation signal to DR-001 in Q4 2024 but deprioritized it in favor of other detection work. Had this correlation been in place, the distributed pattern would have been detectable within the first 1-2 hours rather than 18 hours. The broader systemic issue is that password-only authentication is fundamentally vulnerable to credential stuffing when users reuse passwords across services. Until MFA adoption increases significantly or passkey adoption provides a stronger default, credential stuffing will remain a viable attack vector.

## Detection Analysis

| Question | Answer |
|---|---|
| How was it detected? | Fraud analyst noticed uptick in unauthorized purchase reports during manual queue triage |
| Which detection rule(s) fired? | DR-001 did not fire because individual source IPs stayed below thresholds. Detection was manual |
| Time from start to detection | ~28 hours |
| Were there earlier signals we missed? | Yes. Retrospective analysis showed a 340% increase in aggregate failed login volume starting at 04:00 UTC on March 12. An aggregate volume-based alert (not tied to individual sources) would have caught this within the first hour |

## Response Analysis

**Playbook used:** [ato-response.md](../incident-response/playbooks/ato-response.md)

**What went well:**

Once the incident was declared, the response moved quickly. The team went from declaration to first containment action in 45 minutes. Kenji's emergency detection model using the breach database correlation was deployed within 90 minutes and immediately reduced attack effectiveness by 85%. The cross-functional coordination between detection engineering, fraud ops, and security engineering was smooth, with clear ownership at each stage. Customer communication was drafted, approved, and sent within 6 hours of incident declaration.

**What could be improved:**

The 18-hour detection gap is the primary issue. The attack was detected by a human analyst noticing downstream symptoms (fraud reports) rather than by automated detection of the attack itself. The detection rule was designed for a previous generation of attack technique (concentrated, high-velocity) and had not been updated for the distributed, throttled pattern that is now standard among sophisticated operators.

The forced password reset for 34,000 accounts generated significant customer support volume (~2,400 support tickets over 48 hours). The team should develop a smoother account recovery flow for mass-reset scenarios that reduces the need for human support intervention.

## What We Learned

Sophisticated credential stuffing operations have evolved beyond high-velocity attacks from concentrated sources. The current standard is distributed infrastructure with per-source throttling designed to evade velocity-based detection. Our detection strategy must evolve to match, with aggregate volume monitoring, subnet/ASN correlation, and breach database correlation as standard signals rather than post-incident emergency measures.

The 1.2% credential match rate reinforces that password reuse is the fundamental enabler of credential stuffing. Every percentage point increase in MFA adoption directly reduces the attack surface. The passkey rollout planned for Q3 2025 should be accelerated if possible.

## Action Items

| Action | Owner | Target Date | Status | Repo Link |
|---|---|---|---|---|
| Add aggregate login failure volume alert (not per-source) to detect distributed attacks | Aisha Williams | 2025-04-01 | Complete | `detections-and-controls/detection-rules/aggregate-auth-failure-volume.md` |
| Build subnet/ASN correlation signal into DR-001 as companion rule DR-001b | Aisha Williams | 2025-04-15 | Complete | `detections-and-controls/detection-rules/subnet-credential-correlation.md` |
| Raise DR-001 minimum failure threshold from 30 to 50 to reduce FP rate given new companion rules | Aisha Williams | 2025-03-18 | Complete | `detections-and-controls/detection-rules/credential-stuffing-velocity.md` |
| Integrate January 2025 retail breach database into proactive credential blocklist | Kenji Tanaka | 2025-04-01 | Complete | `detections-and-controls/controls/credential-breach-blocklist.md` |
| Develop mass password reset recovery flow that reduces support ticket volume | Maya Chen | 2025-05-01 | In Progress | `identity-and-access/account-lifecycle/recovery.md` |
| Evaluate acceleration of passkey rollout from Q3 to Q2 2025 | Maya Chen | 2025-04-15 | In Progress | `identity-and-access/authentication/passkeys.md` |
| Add breach credential check at login time (proactive block of known-breached passwords) | Liam Fitzgerald | 2025-05-15 | Open | `detections-and-controls/controls/credential-breach-blocklist.md` |
| Write exec briefing summarizing incident and MFA investment case | Maya Chen | 2025-03-25 | Complete | `exec-briefings/2025-03-credential-stuffing-exec-summary.md` |

## Related Artifacts

| Type | Link |
|---|---|
| Campaign file | `campaigns-and-incidents/archive/2025-q1-credential-stuffing-wave.md` |
| Threat actor(s) | [Marketplace Fraud Rings](../threat-actors/marketplace-fraud-rings.md) |
| Detection rule(s) | [credential-stuffing-velocity.md](../detections-and-controls/detection-rules/credential-stuffing-velocity.md), DR-001b (subnet correlation) |
| Playbook used | [ato-response.md](../incident-response/playbooks/ato-response.md) |
| Intelligence index entry | [credential-stuffing](../intelligence-index.yaml), [account-takeover](../intelligence-index.yaml) |
| Exec summary | [2025-03-credential-stuffing-exec-summary.md](../exec-briefings/2025-03-credential-stuffing-exec-summary.md) |
