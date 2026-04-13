# HODOR Ingestion Model

> HODOR is a curated security and trust-and-safety knowledge layer that turns open-source intelligence into mapped controls, response context, and AI-ready operations.

HODOR is not a feed mirror. This document defines how external data enters the Defensive Knowledge Base, how it is organized, and how it connects to the team's original work product.

## The Three-Tier Model

### Tier 1: Canonical Structured Feeds

These are authoritative, machine-readable data sources that serve as HODOR's foundation. They are not documents the team writes. They are data the team ingests, references, and builds on top of.

| Feed | What It Provides | Location in HODOR | Update Frequency |
|---|---|---|---|
| MITRE ATT&CK (STIX 2.1) | Canonical taxonomy of adversary tactics, techniques, software, and groups | `taxonomy/attack/` | Quarterly |
| CISA KEV | Authoritative catalog of vulnerabilities known to be actively exploited in the wild | `vulnerabilities-and-exposures/kev/` | Daily |
| NVD CVE/CPE | Normalized vulnerability data with severity scores, affected products, and references | `vulnerabilities-and-exposures/nvd/` | Continuous |

**Why these three first:** ATT&CK gives you the shared language for threats. CISA KEV narrows the vulnerability firehose to what is actually being exploited. NVD provides the enrichment layer for everything else. Together, they form a defensible foundation that any security leader or auditor would recognize as authoritative.

**How they connect to HODOR:** ATT&CK technique IDs are the primary keys in `intelligence-index.yaml`, `compliance-and-frameworks/mitre-attack/technique-coverage.yaml`, and every threat actor profile. CISA KEV entries drive urgency tags and remediation priority in `vulnerabilities-and-exposures/`. NVD data enriches vulnerability assessments with CVSS scores, affected product mappings, and reference links.

### Tier 2: Curated Operational Knowledge

These are large, community-maintained open-source repositories where the team selectively imports the pieces relevant to Prism's threat landscape. The keyword is "curated." Do not mirror the full Sigma repo (4,000+ rules) or the full Atomic Red Team library. Pull metadata, ATT&CK mappings, and references for the techniques that matter to your environment, then create HODOR entries that connect them to your threats and controls.

| Source | What It Provides | Location in HODOR | Approach |
|---|---|---|---|
| Sigma Rules | Community detection rules with ATT&CK mappings and log source references | `detections-and-controls/sigma-catalog/` | Curated selection mapped to HODOR threats |
| Atomic Red Team | ATT&CK-mapped validation tests that prove detection coverage | `detections-and-controls/atomic-validation/` | Selected tests for techniques we claim to detect |
| MISP / OpenCTI exports | Structured threat intel events and indicators | `threat-intelligence/intel-cards/` | Selected events relevant to Prism's sector |

**Why curate instead of mirror:** Raw open-source feeds are noisy. A full Sigma mirror would include thousands of rules for Windows event logs, Active Directory attacks, and Linux process monitoring that have nothing to do with a marketplace platform's threat model. Curating means you only carry the weight of what you actually use, and every entry in HODOR connects to a real threat or control rather than sitting as dead weight.

**How Sigma and Atomic connect:** A Sigma rule in `sigma-catalog/` maps to an ATT&CK technique, which maps to a threat in `intelligence-index.yaml`, which maps to a HODOR-authored detection rule in `detection-rules/`. The Sigma rule is the community's take on detecting the technique. The HODOR detection rule is the team's implementation tuned for Prism's environment. An Atomic Red Team test in `atomic-validation/` validates that the detection actually fires when the technique is executed. This chain, from community knowledge to team implementation to validated coverage, is what closes the loop.

### Tier 3: Human-Authored HODOR Artifacts

These are the original work products of the Prism security and T&S team. They are informed by Tiers 1 and 2 but represent the team's analysis, decisions, and operational knowledge. This is where HODOR's real value lives: context that is specific to Prism, written by people who understand the platform, and structured for AI agents to consume.

| Artifact Type | Location | Examples |
|---|---|---|
| Intel cards | `threat-intelligence/intel-cards/` | Curated intelligence summaries with Prism-specific relevance assessment |
| Actor profiles | `threat-actors/` | Detailed threat actor profiles with TTPs, IOCs, and detection coverage mapping |
| Campaign summaries | `campaigns-and-incidents/` | Documentation of active and historical attack campaigns |
| Control cards | `detections-and-controls/control-cards/` | Security control documentation with configuration and effectiveness data |
| Detection rules | `detections-and-controls/detection-rules/` | Prism-specific detection logic with tuning history and performance metrics |
| Runbooks and playbooks | `incident-response/playbooks/` | Step-by-step response procedures |
| Postmortems | `postmortems/` | Incident retrospectives with lessons learned and action items |
| Exec briefs | `exec-briefings/` | Leadership-ready security communications |
| Investigation case files | `investigations/` | Proactive investigation documentation |

## What NOT to Ingest

For v1, resist the temptation to pull in everything. Specifically:

Do not mirror the full Sigma repo. Do not mirror the full Atomic Red Team repo. Do not dump all OpenCTI or MISP objects into markdown. Do not treat breaking news as equal to canonical sources. Do not ingest unverified OSINT directly into the main index.

Instead, create a `news-triage/` area in `threat-intelligence/` where lower-confidence sources can live until they are corroborated. This keeps the main HODOR structure clean and high-signal while still giving the team a place to track emerging ransomware claims, threat actor posts, breach chatter, and published incidents.

## Phased Build Order

**Phase 1 (Foundation)**
Ingest ATT&CK STIX data into `taxonomy/attack/`. Ingest CISA KEV feed into `vulnerabilities-and-exposures/kev/`. Ingest NVD feeds into `vulnerabilities-and-exposures/nvd/`. Define taxonomy and source registry.

**Phase 2 (Operational Depth)**
Add curated Sigma rule mappings to `detections-and-controls/sigma-catalog/`. Add curated Atomic Red Team test mappings to `detections-and-controls/atomic-validation/`. Generate HODOR control cards in `detections-and-controls/control-cards/`.

**Phase 3 (Intelligence Maturity)**
Add OpenCTI or MISP interoperability for structured intel import. Add news triage and actor profile workflows. Expand trust-and-safety specific abuse patterns.

## Upstream Integration: OpenCTI and MISP

OpenCTI and MISP are not content repos to mirror. They are upstream systems or integration models. OpenCTI has a connector model for bringing in external STIX data. MISP is designed for collecting, storing, distributing, and sharing structured threat intel. HODOR can borrow their schemas and workflows, or later sync with them, instead of trying to copy all of their raw data into markdown files. In a mature deployment, OpenCTI or MISP would feed curated intel cards into HODOR's `intel-cards/` folder, and HODOR's human-authored analysis would flow back as enrichment.
