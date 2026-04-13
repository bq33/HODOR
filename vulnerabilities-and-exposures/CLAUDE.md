# Vulnerabilities and Exposures

This folder tracks vulnerabilities relevant to Prism's technology stack, including CVEs, zero-day disclosures, and internally discovered vulnerabilities. It combines canonical structured feeds with team-authored exposure assessments.

## Folder Structure

**kev/** contains ingested data from the CISA Known Exploited Vulnerabilities catalog. This is the "actually exploited in the wild" priority layer. When a CVE appears in KEV, it drives urgency tags, remediation priority, and executive relevance. KEV entries are the highest-priority items in vulnerability management because they represent confirmed active exploitation, not theoretical risk. Updated daily. See `INGESTION.md` for the ingestion model.

**nvd/** contains ingested data from the NIST National Vulnerability Database. NVD provides normalized CVE data with CVSS severity scores, CPE product mappings, and reference links. Used to enrich vulnerability assessments with severity context and affected technology mappings. The NVD API and JSON feeds support scheduled ingestion. See `INGESTION.md` for the ingestion model.

**curated/** contains team-authored vulnerability assessments for CVEs that are relevant to Prism. Each assessment documents whether Prism is affected, what compensating controls exist, and the patching or remediation status. Not every CVE gets an assessment. Only those that affect Prism's technology stack, are flagged by CISA KEV, or are escalated through the intelligence pipeline.

## Triage Process

When a new vulnerability is disclosed, the triage process follows these steps. First, check the source trust tier in `source-registry/source-registry.yaml` to determine the action SLA. Second, assess whether the vulnerability affects any component in Prism's technology stack. Third, if affected, document the exposure and compensating controls. Fourth, coordinate remediation with the relevant engineering team. Fifth, update the MITRE ATT&CK technique coverage if the vulnerability introduces a new detection opportunity.

## Severity and SLA

Vulnerability severity follows CVSS scoring with adjustments for Prism-specific context. A critical CVSS vulnerability in a component we don't use is informational. A medium CVSS vulnerability in a component that handles authentication may be treated as high based on business impact. SLAs for remediation follow the schedule in `source-registry/source-registry.yaml` under the NIST NVD entry.

## File Naming

Vulnerability files are named by CVE identifier when available (e.g., `CVE-2025-12345.md`) or by a descriptive name for internally discovered vulnerabilities (e.g., `internal-api-auth-bypass-2025-02.md`). Each file uses the template from `templates/vulnerability-template.md`.
