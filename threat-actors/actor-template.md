# [Actor Name]

> Last updated: YYYY-MM-DD
> Confidence level: [high | moderate | low]
> Status: [active | dormant | disbanded | unknown]

## Overview

Brief description of the threat actor, their motivations, and their relevance to Prism.

## Classification

| Attribute | Value |
|---|---|
| Type | [nation-state / organized-crime / hacktivism / insider / tooling-provider / gray-market] |
| Motivation | [financial / espionage / disruption / ideological / competitive] |
| Sophistication | [high / moderate / low] |
| Targeting | [opportunistic / targeted / sector-specific] |
| Active since | YYYY |
| Known aliases | [list of alternative names used by vendors] |

## Relevance to Prism

How this actor specifically threatens Prism's platform, users, or operations. Include any known or suspected past activity against Prism or similar platforms.

## Tactics, Techniques, and Procedures (TTPs)

### MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name | How They Use It |
|---|---|---|---|
| Initial Access | T1078 | Valid Accounts | Description of how the actor uses this technique |
| ... | ... | ... | ... |

### Kill Chain Summary

Step-by-step description of the actor's typical attack lifecycle, from initial reconnaissance through achieving their objectives.

## Known Indicators of Compromise (IOCs)

| Type | Value | First Seen | Last Seen | Confidence |
|---|---|---|---|---|
| IP | x.x.x.x | YYYY-MM-DD | YYYY-MM-DD | [high/moderate/low] |
| Domain | example.com | YYYY-MM-DD | YYYY-MM-DD | [high/moderate/low] |
| Hash | sha256:abc... | YYYY-MM-DD | YYYY-MM-DD | [high/moderate/low] |
| Email | actor@example.com | YYYY-MM-DD | YYYY-MM-DD | [high/moderate/low] |

## Our Detection Coverage

Links to detection rules in this repo that cover this actor's known techniques.

| Technique | Detection Rule | Coverage Level |
|---|---|---|
| T1078 | [detection-rules/credential-stuffing-velocity.md](../detections-and-controls/detection-rules/credential-stuffing-velocity.md) | [full / partial / gap] |

## Our Response

Links to playbooks and response procedures for this actor.

| Scenario | Playbook |
|---|---|
| Suspected activity | [playbook-name.md](../incident-response/playbooks/playbook-name.md) |

## Intelligence Sources

Which sources have documented this actor, with links to key reports.

| Source | Report/Advisory | Date | Trust Tier |
|---|---|---|---|
| [source-name] | [report-title] | YYYY-MM-DD | [authoritative/high/moderate/requires-validation] |

## Historical Campaigns

Links to campaigns in this repo attributed to this actor.

| Campaign | Timeframe | Impact |
|---|---|---|
| [campaign-name](../campaigns-and-incidents/archive/campaign-file.md) | YYYY-MM | Summary of impact |

## Notes

Additional context, open questions, or areas for further investigation.
