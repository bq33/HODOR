# Scattered Spider

> Last updated: 2025-04-06
> Confidence level: high
> Status: active

## Overview

Scattered Spider (also tracked as UNC3944 by Mandiant, Octo Tempest by Microsoft, and 0ktapus by Group-IB) is a financially motivated cybercrime group known for sophisticated social engineering campaigns targeting identity providers, help desks, and IT support personnel. They specialize in gaining initial access through human manipulation rather than technical exploitation, making them particularly dangerous to organizations that rely on human-operated identity verification processes.

Their relevance to Prism is both direct and indirect. They target organizations in our sector for credential theft and account takeover, and their techniques for compromising identity providers could be used to attack Prism's authentication infrastructure. Their social engineering playbook is also increasingly adopted by less sophisticated groups.

## Classification

| Attribute | Value |
|---|---|
| Type | Organized crime |
| Motivation | Financial |
| Sophistication | High |
| Targeting | Targeted, sector-specific (tech, telecom, retail, hospitality) |
| Active since | 2022 |
| Known aliases | UNC3944, Octo Tempest, 0ktapus, Scatter Swine, Star Fraud |

## Relevance to Prism

Scattered Spider poses a direct risk to Prism in two ways. First, they are known to target identity providers (Okta, Azure AD) used by organizations like Prism, which could compromise employee access to internal systems. Second, their SIM swapping and social engineering techniques can be used to take over high-value user accounts on consumer platforms. Prism's reliance on SMS-based MFA for some user segments makes those accounts vulnerable to SIM swap attacks. Their documented attacks on hospitality and retail companies in the same sector as Prism's marketplace make them a priority tracking target.

## Tactics, Techniques, and Procedures (TTPs)

### MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name | How They Use It |
|---|---|---|---|
| Reconnaissance | T1598 | Phishing for Information | Research employees via LinkedIn, build pretext for help desk calls |
| Initial Access | T1566.004 | Phishing: Spearphishing Voice | Call help desk impersonating employees to reset MFA |
| Initial Access | T1078 | Valid Accounts | Use stolen credentials from phishing or social engineering |
| Persistence | T1556.006 | Modify Authentication Process: MFA | Register new MFA devices after compromising help desk |
| Credential Access | T1111 | Multi-Factor Authentication Interception | SIM swapping to intercept SMS-based MFA codes |
| Lateral Movement | T1021.004 | Remote Services: SSH | Move through infrastructure using compromised credentials |
| Collection | T1530 | Data from Cloud Storage | Access cloud-hosted data using compromised identities |
| Impact | T1657 | Financial Theft | Monetize access through unauthorized transactions |

### Kill Chain Summary

Scattered Spider's typical attack lifecycle starts with open-source reconnaissance of target employees via LinkedIn and social media. They identify help desk phone numbers and IT support procedures. They then call the help desk impersonating an employee, using social engineering to convince the support agent to reset the employee's MFA or password. Once they have valid credentials with fresh MFA enrollment, they log in through normal channels, making detection difficult. From there, they move laterally through cloud infrastructure, targeting identity provider admin consoles, financial systems, and customer data. They monetize access through direct financial theft, data extortion, or selling access to other criminal groups.

## Known Indicators of Compromise (IOCs)

| Type | Value | First Seen | Last Seen | Confidence |
|---|---|---|---|---|
| Technique | Help desk impersonation calls | 2022-06 | 2025-03 | High |
| Technique | SIM swap requests via carrier social engineering | 2022-08 | 2025-03 | High |
| Technique | Okta admin console access from residential VPNs | 2023-01 | 2025-02 | High |
| Tool | Residential proxy services for credential access | 2023-03 | 2025-03 | Moderate |

Note: Scattered Spider deliberately avoids traditional IOCs like malware hashes and C2 domains. Their attacks rely on legitimate tools and stolen credentials, making indicator-based detection largely ineffective. Behavioral detection is essential.

## Our Detection Coverage

| Technique | Detection Rule | Coverage Level |
|---|---|---|
| T1078 (Valid Accounts) | [credential-stuffing-velocity.md](../detections-and-controls/detection-rules/credential-stuffing-velocity.md) | Partial — covers automated stuffing but not manual social engineering |
| T1078 (Valid Accounts) | [impossible-travel-login.md](../detections-and-controls/detection-rules/impossible-travel-login.md) | Partial — effective when actor uses different geolocation |
| T1556 (Modify Auth Process) | [account-change-velocity.md](../detections-and-controls/detection-rules/account-change-velocity.md) | Full — detects rapid MFA/email/phone changes |
| T1111 (MFA Interception) | Gap | Gap — no detection for SIM swap prior to account access |

### Coverage Gaps

The primary gap is detection of the social engineering phase itself. Scattered Spider's initial access method (help desk impersonation) occurs outside our digital telemetry. Mitigations focus on hardening the help desk process (identity verification procedures, callback requirements) rather than real-time detection.

## Our Response

| Scenario | Playbook |
|---|---|
| Suspected help desk social engineering | [phishing-response.md](../incident-response/playbooks/phishing-response.md) |
| Confirmed account takeover via social engineering | [ato-response.md](../incident-response/playbooks/ato-response.md) |
| Identity provider compromise | [mass-ato-response.md](../incident-response/playbooks/mass-ato-response.md) |

## Intelligence Sources

| Source | Report/Advisory | Date | Trust Tier |
|---|---|---|---|
| CISA | Advisory on Scattered Spider TTPs | 2023-11-16 | Authoritative |
| Mandiant | UNC3944 Threat Profile | 2023-09 | High |
| CrowdStrike | Scattered Spider Campaign Analysis | 2023-10 | High |
| Microsoft | Octo Tempest Threat Actor Profile | 2023-10-25 | High |
| Group-IB | 0ktapus Campaign Report | 2022-08 | High |

## Historical Campaigns

| Campaign | Timeframe | Impact |
|---|---|---|
| 0ktapus phishing campaign | 2022-Q3 | 130+ organizations compromised via Okta phishing |
| MGM Resorts attack | 2023-Q3 | Major hospitality company disrupted via help desk social engineering |
| Telecom SIM swap wave | 2023-Q4 | Multiple carrier employees socially engineered for SIM swaps |

## Notes

Scattered Spider is notable for its young membership (many members reportedly teenagers and young adults based in the US and UK). Their sophistication comes from social engineering skill rather than technical exploitation capability. This makes them a useful model for training help desk staff, because the attack vector is human rather than technical.

The group's evolution toward ransomware deployment (partnering with ALPHV/BlackCat) in late 2023 represents an escalation from their original focus on credential theft and financial fraud. This partnership model, where a social-engineering-focused group provides initial access for a ransomware operator, is increasingly common and relevant to Prism's risk assessment.
