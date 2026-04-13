# HODOR: Hold the Door

**An AI-ready Defensive Knowledge Base (DKB): the security context layer your team and your AI agents share from day one.**

HODOR is an open-source reference architecture for building a curated security and trust-and-safety knowledge base that turns open-source intelligence into mapped controls, response context, and AI-ready operations.

The name is a nod to the Game of Thrones character whose singular purpose was to hold the door. That's what security teams do: hold the line between your users and the threats trying to get through.

## The Problem

Security teams are drowning in context fragmentation. Threat models live in Confluence. Detection rules live in your SIEM. Incident playbooks are buried in Google Docs. Threat intelligence sits in email chains and Slack threads. Tribal knowledge about why a specific detection rule has that specific threshold exists only in one engineer's head.

When a new team member joins, they spend months assembling context. When someone spins up an AI coding agent, it starts from zero every time. When an executive asks "what's our exposure to this new threat?" it takes days to pull together an answer from six different systems.

## The Solution

HODOR is a Defensive Knowledge Base (DKB) where your entire security and T&S team checks in their work, structured so that any AI coding agent can find exactly what it needs to help any team member with the task at hand. Detection rules, threat actor profiles, incident playbooks, compliance mappings, investigation notes, and executive briefings all live in one place, cross-referenced and navigable. Open-source intelligence feeds flow in through a structured ingestion model, get mapped to your controls and response procedures, and become immediately accessible to both humans and AI agents.

The teams that set this up work together at a completely different level.

## The Example

The example organization is **Prism**, a fictional consumer marketplace platform with 60M+ accounts, processing payments, managing seller verification, and handling user-generated content. Inside, you'll find threat intelligence, detection rules, incident playbooks, MITRE ATT&CK mappings, abuse typologies, account quality models, investigation workflows, and more.

Instead of one person bottlenecking security context, everyone on the team can self-serve. The DKB becomes the shared brain of the security organization.

## Getting Started

Clone the repo, start a new Claude Code session inside it, and give Claude this prompt:

> "Read through the HODOR repo structure, the root CLAUDE.md, and INGESTION.md. Based on what you learn, help me build a Defensive Knowledge Base for my security team. Start in plan mode. Ask me about my team structure, what tools we use, what threat landscape we face, and what types of security artifacts we work with. Then design the full system: a root CLAUDE.md with a doc index and team roster, folder-level CLAUDE.md files as navigation maps for each section, and a folder architecture tailored to how my security team actually works."

## Architecture at a Glance

HODOR is organized around how security teams actually think and operate:

**Ingestion Layer** — How external intelligence enters the system. Canonical feeds (ATT&CK, CISA KEV, NVD), curated community knowledge (Sigma rules, Atomic Red Team tests), and a news-triage pipeline for unverified OSINT.

**Intelligence Layer** — Where threats come from and what we know about them. Source registry with trust tiers, threat actor profiles, intel cards, campaign tracking, vulnerability management, and OSINT integration.

**Defense Layer** — How we detect, prevent, and respond. Detection rules, security controls, incident response playbooks, and investigation workflows.

**Trust & Safety Layer** — How we protect the platform and its users. Fraud typologies, content moderation taxonomies, bot detection strategies, and policy enforcement.

**Identity & Access Layer** — How we verify users and manage account trust. Account lifecycle, quality scoring, authentication strategy, and identity verification.

**Governance Layer** — How we measure, report, and stay compliant. NIST CSF and 800-63 mappings, MITRE ATT&CK coverage, KPIs, dashboards, and executive briefings.

**Team Layer** — How we onboard, operate, and grow. Team processes, on-call rotations, career ladders, and onboarding guides.

## Key Concepts

### Three-Tier Ingestion Model

HODOR is not a feed mirror. It is a curated knowledge layer built on three tiers. Tier 1 is canonical structured feeds (MITRE ATT&CK STIX data, CISA KEV, NVD) that provide authoritative, machine-readable foundations. Tier 2 is curated operational knowledge: selected Sigma detection rules, Atomic Red Team validation tests, and structured intel from platforms like OpenCTI and MISP, imported selectively rather than mirrored wholesale. Tier 3 is the team's own work product: threat actor profiles, detection rules tuned for your environment, postmortems, executive briefings, and investigation case files. See `INGESTION.md` for the full model and phased build order.

### Intelligence Index

The `intelligence-index.yaml` file is the connective tissue of the entire repo. It maps every threat to its related artifacts: which threat actors use it, which MITRE ATT&CK techniques apply, which detection rules cover it, which playbooks to run, which compliance controls it maps to. When an AI agent encounters any security topic, it can trace the full chain from adversary to defense to compliance.

### Source Trust Tiering

Not all intelligence is created equal. The source registry rates every intel source by reliability (authoritative, high, moderate, requires-validation), update frequency, and action SLA. This means the team and AI agents can immediately assess how much weight to give a new advisory and how fast to act.

### Cross-Referencing

Every major artifact in the repo links to related artifacts in other folders. A detection rule references the threat model that motivated it, the MITRE technique it covers, and the playbook to run when it fires. A postmortem references the detection rules that did or didn't catch the incident, the playbook that was followed, and the improvements that were made.

## Contributing

Fork the repo, adapt it for your team, and share what you learn. Security is a team sport, and the more teams that operate with structured, AI-ready Defensive Knowledge Bases, the better our collective defense becomes.

## License

This work is licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). See [LICENSE](LICENSE) for details.

## About the Author

Created by [Brandon Quinn](https://brandonquinn.me), a product leader specializing in account security, trust & safety, and abuse prevention at scale.
