# Threat Intelligence

This folder is where the team consumes, assesses, and acts on external intelligence from government agencies, industry groups, commercial vendors, and open-source channels. It is the "intake" side of the intelligence pipeline, where raw intelligence enters the team's awareness and gets processed into actionable artifacts.

## How Intelligence Flows Through HODOR

External intelligence arrives from the sources documented in `source-registry/source-registry.yaml`. The trust tier of the source determines the initial response tempo. The intelligence then flows through a triage process: Is this relevant to Prism? Does it describe a threat we already track? Does it reveal a new technique, actor, or campaign? Based on the answers, the intelligence is routed to the appropriate location in the repo. A new threat actor goes to `threat-actors/`. A new campaign goes to `campaigns-and-incidents/`. A new vulnerability goes to `vulnerabilities-and-exposures/`. A new detection opportunity goes to `detections-and-controls/`.

## Folders

**intel-cards/** contains curated intelligence summaries written by the team or imported from structured sources (OpenCTI exports, MISP events). Each intel card documents a specific piece of actionable intelligence: a new threat, a campaign update, an emerging technique, or a relevant sector incident. Intel cards include a Prism-specific relevance assessment so the team can quickly determine whether action is needed. Cards imported from external platforms are Tier 2 in the ingestion model (see `INGESTION.md`). Cards authored by the team are Tier 3.

**news-triage/** is the intake area for lower-confidence intelligence that has not yet been corroborated. Breaking news, researcher threads on social media, unverified dark web chatter, and OSINT tips land here first. Items in news-triage are explicitly not treated as confirmed intelligence. They sit here until the team validates them against higher-tier sources. Once corroborated, they are promoted to an intel card, a threat actor update, or a campaign entry. This keeps the main HODOR structure clean and high-signal while still giving the team a place to track emerging threats. Items that cannot be corroborated within 30 days are archived with a note explaining why.

**actor-profiles/** contains supplementary actor intelligence that feeds into the main threat actor profiles in `threat-actors/`. This may include raw intelligence reports, vendor advisories, or OSINT analysis that is being synthesized into a formal actor profile.

**government/** contains references to government-published advisories, alerts, and mandates from CISA, FBI, NSA, and other agencies. These represent authoritative intelligence that the team acts on with the highest priority.

**frameworks/** contains reference documentation for the standards and frameworks the team uses (NIST, MITRE ATT&CK, OWASP). These are not operational intelligence but the structural knowledge that informs how the team categorizes and responds to threats.

**vendor-reports/** contains summaries and references to commercial threat intelligence reports from providers like Mandiant, CrowdStrike, and Recorded Future.

**osint/** contains the team's OSINT methodology documentation, monitoring tool configurations, and guidelines for validating information from open sources before acting on it.

**industry/** contains intelligence shared through industry groups like ISACs and peer company relationships.
