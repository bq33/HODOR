# Postmortem: [Incident Title]

> **Date of incident:** YYYY-MM-DD
> **Date of postmortem:** YYYY-MM-DD
> **Severity:** [SEV-1 / SEV-2 / SEV-3]
> **Incident commander:** [Name]
> **Author:** [Name]
> **Status:** [Draft / In Review / Final]

## Executive Summary

Two to three sentences describing what happened, the scope of impact, and the outcome. Written for someone who will read only this section.

## Impact

| Metric | Value |
|---|---|
| Duration (detection to resolution) | |
| Accounts affected | |
| Financial impact (estimated) | |
| Data exposed (if applicable) | |
| Customer communications sent | |
| Regulatory notifications required | |

## Timeline

All times in UTC unless otherwise noted.

| Time (UTC) | Event |
|---|---|
| HH:MM | First signal observed (describe the alert or report) |
| HH:MM | Incident declared, severity assigned |
| HH:MM | Incident commander engaged |
| HH:MM | Initial investigation and scoping |
| HH:MM | Containment actions taken |
| HH:MM | Root cause identified |
| HH:MM | Remediation applied |
| HH:MM | Incident resolved, monitoring period begins |
| HH:MM | All-clear declared |

## Root Cause Analysis

What was the underlying cause of the incident? Go beyond the immediate trigger to identify systemic factors. Use the "5 Whys" or similar technique to drill into the chain of causation.

**Immediate cause:**

**Contributing factors:**

**Systemic factors:**

## Detection Analysis

How was the incident detected? Was it detected by automated systems, reported by a user, or discovered through proactive investigation? How long did it take from the start of the incident to detection?

| Question | Answer |
|---|---|
| How was it detected? | [Automated alert / User report / Proactive hunt / External notification] |
| Which detection rule(s) fired? | [Link to rule(s) in `detections-and-controls/`] |
| Time from start to detection | |
| Were there earlier signals we missed? | |

## Response Analysis

How effective was the response? Did the playbook work as expected? Were there points of confusion, delay, or miscommunication?

**Playbook used:** [Link to playbook in `incident-response/playbooks/`]

**What went well:**

**What could be improved:**

## What We Learned

Key insights from this incident that should inform future decisions, detection development, or process changes.

## Action Items

Every action item must have an owner and a target date. Link to the file in the repo where the improvement will be documented.

| Action | Owner | Target Date | Status | Repo Link |
|---|---|---|---|---|
| [Describe the action] | [Name] | YYYY-MM-DD | [Open / In Progress / Complete] | [Link to relevant file] |

## Related Artifacts

| Type | Link |
|---|---|
| Campaign file | [Link to `campaigns-and-incidents/`] |
| Threat actor(s) | [Link to `threat-actors/`] |
| Detection rule(s) | [Link to `detections-and-controls/`] |
| Playbook used | [Link to `incident-response/playbooks/`] |
| Intelligence index entry | [Link to threat in `intelligence-index.yaml`] |
| Exec summary | [Link to `exec-briefings/` if applicable] |
