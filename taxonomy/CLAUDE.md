# Taxonomy

This folder defines the shared vocabulary the entire Prism security and trust & safety team operates on. Every classification system, severity scale, and category definition lives here so that the team (and any AI agent working in this repo) speaks the same language.

Consistent taxonomy matters because ambiguity kills speed. When an analyst says "this is a high-severity fraud case" and an engineer hears "high-severity security incident," they may have very different response expectations. The definitions here eliminate that gap.

## Classification Systems

| File | Description |
|---|---|
| `abuse-types.md` | Master taxonomy of all abuse types on the Prism platform (fraud, spam, harassment, counterfeiting, manipulation, etc.) |
| `severity-levels.md` | Severity scale used across security incidents, T&S cases, and vulnerability management with response SLAs for each level |
| `enforcement-actions.md` | All available enforcement actions (warning, restriction, suspension, permanent ban, law enforcement referral) with criteria for each |
| `account-quality-tiers.md` | Definitions of account quality tiers (from highest quality to lowest quality) and the signals that determine placement |
| `content-categories.md` | Content moderation taxonomy defining prohibited, restricted, and allowed content categories |
| `threat-severity.md` | Threat actor and campaign severity ratings used in intelligence assessments |
| `investigation-status.md` | Lifecycle stages for investigations (open, active, awaiting-response, escalated, closed-confirmed, closed-false-positive) |

## ATT&CK Taxonomy (Canonical Feed)

The `attack/` sub-folder contains ingested MITRE ATT&CK data in STIX 2.1 format. This is HODOR's canonical taxonomy for adversary tactics, techniques, software, and groups. ATT&CK technique IDs (e.g., T1110.004) are the primary keys used throughout the repo: in `intelligence-index.yaml`, in threat actor profiles, in detection rules, and in the MITRE coverage map. The STIX data is updated quarterly when MITRE publishes new ATT&CK versions.

This data is ingested, not authored. See `INGESTION.md` for the full ingestion model.

## Design Principles

These taxonomies follow a few principles. Every category must be mutually exclusive — a case should not reasonably belong in two categories at the same level. Every severity level must have a clear, measurable action SLA so there is no ambiguity about expected response time. Every enforcement action must have both criteria for when to apply it and an appeal path. Language should use "higher quality" and "lower quality" rather than "low risk" and "high risk" when describing account tiers to external stakeholders, since risk framing can create confusion about whose risk is being assessed.
