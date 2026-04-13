# HODOR — Hold the Door

> An AI-ready Defensive Knowledge Base (DKB): the security context layer your team and your AI agents share from day one.

## Mission

Protect Prism's 60M+ users and the integrity of the marketplace by building layered defenses that make abuse expensive, detection fast, and response decisive — while keeping the platform experience seamless for legitimate users.

## Team

| Function | Team Member | GitHub | Jira ID | Slack ID |
|---|---|---|---|---|
| Security PM | Maya Chen | `mayachen` | `a1b2c3d4-e5f6-7890-abcd-ef1234567890` | `U0A1B2C3D4E` |
| Security EM | James Okafor | `jamesokafor` | `b2c3d4e5-f6a7-8901-bcde-f12345678901` | `U0B2C3D4E5F` |
| Security Engineer | Priya Sharma | `priyasharma` | `c3d4e5f6-a7b8-9012-cdef-123456789012` | `U0C3D4E5F6A` |
| Security Engineer | Liam Fitzgerald | `liamfitz` | `d4e5f6a7-b8c9-0123-defa-234567890123` | `U0D4E5F6A7B` |
| Detection Engineer | Aisha Williams | `aishawilliams` | `e5f6a7b8-c9d0-1234-efab-345678901234` | `U0E5F6A7B8C` |
| T&S Lead | Carlos Reyes | `carlosreyes` | `f6a7b8c9-d0e1-2345-fabc-456789012345` | `U0F6A7B8C9D` |
| T&S Analyst | Nadia Petrov | `nadiapetrov` | `a7b8c9d0-e1f2-3456-abcd-567890123456` | `U0A7B8C9D0E` |
| Fraud Analyst | Darnell Brooks | `darnellbrooks` | `b8c9d0e1-f2a3-4567-bcde-678901234567` | `U0B8C9D0E1F` |
| Security Data Science | Kenji Tanaka | `kenjitanaka` | `c9d0e1f2-a3b4-5678-cdef-789012345678` | `U0C9D0E1F2A` |
| Security Ops & Compliance | Fatima Al-Rashid | `fatimarashid` | `d0e1f2a3-b4c5-6789-defa-890123456789` | `U0D0E1F2A3B` |

## Slack Channels

| Channel | ID | Visibility | Purpose |
|---|---|---|---|
| #security-incidents | `C0A1B2C3D4E` | Public | Active incident coordination, status updates, postmortem links |
| #threat-intel | `C0B2C3D4E5F` | Private | Intelligence sharing, advisory triage, IOC distribution |
| #fraud-ops | `C0C3D4E5F6A` | Private | Fraud pattern alerts, case escalations, rule tuning discussions |
| #trust-safety | `C0D4E5F6A7B` | Private | Policy decisions, abuse trends, enforcement actions |
| #detection-engineering | `C0E5F6A7B8C` | Private | Detection rule development, tuning, false positive reviews |
| #security-engineering | `C0F6A7B8C9D` | Private | Architecture decisions, RFC reviews, code reviews |
| #security-standup | `C0A7B8C9D0E` | Private | Daily async standups and blockers |
| #vulnerability-mgmt | `C0B8C9D0E1F` | Private | CVE triage, patching status, exposure assessments |
| #exec-security-updates | `C0C9D0E1F2A` | Private | Executive briefings, board prep, risk summaries |
| #security-random | `C0D0E1F2A3B` | Private | Team culture, celebrations, off-topic |

### DM Groups

| Group | Members | ID | Purpose |
|---|---|---|---|
| Security Leads | Maya, James, Carlos, Fatima | `G0A1B2C3D4E` | Weekly leads sync, cross-functional decisions |
| Detection + Intel | Aisha, Priya, Kenji, Darnell | `G0B2C3D4E5F` | Detection rule development informed by intel and data |
| Incident Commanders | James, Priya, Liam, Carlos | `G0C3D4E5F6A` | On-call coordination and escalation decisions |
| T&S Policy | Carlos, Nadia, Maya, Fatima | `G0D4E5F6A7B` | Policy creation, enforcement calibration, appeal reviews |
| Fraud Ring | Darnell, Kenji, Aisha, Carlos | `G0E5F6A7B8C` | Active fraud investigations and pattern analysis |
| Security + Product | Maya, James, Fatima | `G0F6A7B8C9D` | Roadmap alignment, compliance requirements, exec reporting |

## Doc Index

**When looking up artifacts for a specific threat, attack pattern, or feature, check `intelligence-index.yaml` first.** It maps every threat to all related artifacts in one place — detection rules, playbooks, threat actor profiles, compliance controls, and postmortems.

**For understanding how external data feeds into HODOR, read `INGESTION.md`.** It defines the three-tier model: canonical structured feeds (ATT&CK, CISA KEV, NVD), curated operational knowledge (Sigma, Atomic Red Team), and human-authored HODOR artifacts.

| Area | File | Description |
|---|---|---|
| Intelligence index | `intelligence-index.yaml` | Master lookup — every threat mapped to its actors, detections, playbooks, controls, and compliance |
| Ingestion model | `INGESTION.md` | Three-tier model for how external data enters HODOR |
| Source registry | `source-registry/CLAUDE.md` | All intelligence sources, rated by reliability and action SLA |
| Threat intelligence | `threat-intelligence/CLAUDE.md` | Government advisories, framework references, vendor reports, OSINT |
| Threat actors | `threat-actors/CLAUDE.md` | Adversary profiles, TTPs, tracked groups and individuals |
| Campaigns & incidents | `campaigns-and-incidents/CLAUDE.md` | Active and historical attack campaigns and security events |
| Vulnerabilities | `vulnerabilities-and-exposures/CLAUDE.md` | CVE tracking, exposure assessments, patching status |
| Taxonomy | `taxonomy/CLAUDE.md` | Shared vocabulary — abuse types, severity levels, enforcement actions |
| Trust & safety patterns | `trust-and-safety-patterns/CLAUDE.md` | Fraud typologies, content moderation, bot detection, marketplace abuse |
| Detections & controls | `detections-and-controls/CLAUDE.md` | Detection rules, security controls, challenge strategies |
| Identity & access | `identity-and-access/CLAUDE.md` | Account lifecycle, quality scoring, authentication, IDV |
| Investigations | `investigations/CLAUDE.md` | Active and closed investigation case files |
| Incident response | `incident-response/CLAUDE.md` | Response playbooks, runbooks, on-call procedures |
| Postmortems | `postmortems/CLAUDE.md` | Incident retrospectives, lessons learned, improvement tracking |
| Policies & enforcement | `policies-and-enforcement/CLAUDE.md` | T&S policies, enforcement rubrics, appeal workflows |
| Metrics & reporting | `metrics-and-reporting/CLAUDE.md` | KPIs, dashboards, experiment results |
| Exec briefings | `exec-briefings/CLAUDE.md` | Board decks, quarterly reviews, risk summaries for leadership |
| Automations | `automations/CLAUDE.md` | SOAR playbooks, enrichment workflows, automated responses |
| Compliance & frameworks | `compliance-and-frameworks/CLAUDE.md` | NIST CSF, 800-63, MITRE ATT&CK, OWASP mappings |
| Engineering | `engineering/CLAUDE.md` | Security architecture, RFCs, system design |
| Templates | `templates/CLAUDE.md` | Reusable templates for all artifact types |
| Team | `team/CLAUDE.md` | Onboarding, processes, career ladders, on-call rotation |

## How to Use This Repo

1. **Starting a new task?** Check the `intelligence-index.yaml` to find all related artifacts for the threat or feature you're working on.
2. **Investigating a new threat?** Start in `threat-intelligence/` to assess the source, then check `threat-actors/` for known adversary profiles, `detections-and-controls/` for existing coverage, and `compliance-and-frameworks/mitre-attack/` for technique mapping.
3. **Building a new detection?** Start with the threat model in `trust-and-safety-patterns/` or `threat-intelligence/`, write the rule in `detections-and-controls/detection-rules/`, and update `intelligence-index.yaml` and the MITRE technique coverage.
4. **Responding to an incident?** Pull the relevant playbook from `incident-response/playbooks/`, document the response in `campaigns-and-incidents/active/`, and create a postmortem in `postmortems/` when resolved.
5. **Preparing an exec briefing?** Pull KPIs from `metrics-and-reporting/`, threat landscape updates from `threat-intelligence/`, and incident summaries from `postmortems/`. Use templates from `exec-briefings/`.
6. **Onboarding someone new?** Start with `team/onboarding/` and the taxonomy in `taxonomy/` to get them speaking the team's language.
