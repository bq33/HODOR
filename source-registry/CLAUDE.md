# Source Registry

This folder contains the master registry of all intelligence sources the Prism security team consumes, evaluates, and acts on. Every source is rated by reliability, update frequency, and expected action SLA.

## Source Trust Tiers

**Authoritative** — Government agencies, standards bodies, and primary CVE databases. Information from these sources is treated as ground truth and acted on within the stated SLA without additional validation. Examples: CISA KEV, NIST NVD, FBI IC3.

**High** — Established commercial threat intelligence providers and major industry research organizations. Information is reliable and actionable, though the team may cross-reference with authoritative sources for critical decisions. Examples: Mandiant, CrowdStrike, Recorded Future.

**Moderate** — Industry-specific sharing groups (ISACs), peer company disclosures, and established security researchers. Information is generally reliable but may lack the verification rigor of higher tiers. The team validates key claims before taking major action. Examples: FS-ISAC, Retail ISAC, named security researchers.

**Requires Validation** — Open-source intelligence, social media, dark web monitoring, and anonymous tips. Information from these sources must be cross-referenced with at least one higher-tier source before the team takes action. False positives are common and expected. Examples: Twitter/X security community, Telegram channels, paste sites, dark web forums.

## How to Use the Source Registry

When a new advisory, IOC, or threat report arrives, the first step is always to check the source against this registry. The trust tier determines the response tempo. An authoritative source reporting an actively exploited vulnerability triggers the action SLA immediately. A requires-validation source reporting the same vulnerability triggers a validation workflow before the clock starts.

When adding a new source, use the `source-template.yaml` format and assign a trust tier based on the criteria above. New sources default to "requires-validation" until the team has enough experience with them to upgrade.

## Files

| File | Description |
|---|---|
| `source-registry.yaml` | Master registry of all intelligence sources with trust tiers and SLAs |
| `source-template.yaml` | Template for adding new sources |
| `source-evaluation-criteria.md` | How we assess and promote sources between tiers |
