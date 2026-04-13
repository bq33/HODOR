# Detections and Controls

This folder contains the security team's detection rules, security controls, and challenge strategies. It is the "defense layer" of HODOR, where the team documents how threats identified in `threat-intelligence/` and `threat-actors/` are actually caught and mitigated in production.

## How This Folder Is Organized

**detection-rules/** contains the team's original detection rule documents. Each rule has a defined trigger condition, the data sources it queries, tuning history, known false positive patterns, and links back to the threat actor or attack pattern it was designed to catch. When an AI agent needs to write or modify a detection rule, it should read the existing rules in this folder to understand the team's conventions and the available data sources.

**sigma-catalog/** contains curated entries from the Sigma community detection rule repository. These are not a full mirror of the 4,000+ Sigma rules. They are selected rules relevant to Prism's threat landscape, imported with their metadata, ATT&CK mappings, log source references, and status. Each entry links to the corresponding community Sigma rule and maps to HODOR threats in `intelligence-index.yaml`. The Sigma catalog represents "the community's take" on detecting a technique. The team's detection rules in `detection-rules/` represent Prism's tuned implementation. See `INGESTION.md` for the curation approach.

**atomic-validation/** contains curated entries from the Atomic Red Team test library. These are ATT&CK-mapped validation tests that prove detection coverage. If the team claims to detect T1110.004 (Credential Stuffing), the corresponding Atomic test in this folder documents how to execute the technique in a controlled environment and verify the detection fires. This connects "we think we detect this" to "we actually tested this." See `INGESTION.md` for the curation approach.

**control-cards/** contains documentation of security controls in a standardized format. Each control card describes what the control protects against, how it is configured, what triggers it, how its effectiveness is measured, and which threats and ATT&CK techniques it maps to. Control cards are the preventive complement to detection rules: controls stop attacks before detection is needed.

**controls/** contains deeper documentation of preventive and compensating security controls. Things like rate limiting, credential breach blocklists, network segmentation, and transaction risk scoring. Each control document describes what it protects against, how it is configured, and what happens when it triggers.

**challenge-strategies/** contains the team's approach to interactive challenges (CAPTCHA, step-up authentication, device verification). These sit at the intersection of security and user experience and require careful calibration.

## Key Files

| File | Description |
|---|---|
| `detection-rules/CLAUDE.md` | Index of all detection rules with authoring standards |
| `detection-rules/rule-template.md` | Standard template for new detection rules |
| `controls/CLAUDE.md` | Index of all security controls |
| `challenge-strategies/CLAUDE.md` | Challenge and friction strategy documentation |

## Connection to Intelligence Index

Every detection rule and control in this folder should be mapped in `intelligence-index.yaml` under the threats it addresses. When adding a new detection rule, always update the intelligence index and the MITRE ATT&CK technique coverage in `compliance-and-frameworks/mitre-attack/technique-coverage.yaml`.
