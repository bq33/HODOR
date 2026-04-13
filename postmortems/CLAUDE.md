# Postmortems

This folder contains retrospective analyses of significant security incidents and trust & safety events. Every SEV-1 and SEV-2 incident requires a postmortem within 5 business days of resolution. SEV-3 incidents get postmortems at the discretion of the incident commander.

## Postmortem Culture

Postmortems at Prism are blameless. The goal is to understand what happened, why it happened, what the team did well, and what can be improved. The focus is on systems, processes, and tooling, not on individual mistakes. People make errors; the interesting question is always why the system allowed the error to have the impact it did.

## Template

All postmortems use the template in `templates/postmortem-template.md`. The template covers incident summary, timeline, root cause analysis, what went well, what could be improved, action items with owners and due dates, and detection/response gaps identified.

## Connection to Other Folders

Postmortems are where the repo learns. A postmortem may identify a detection gap that results in a new detection rule in `detections-and-controls/`. It may reveal a threat actor technique not previously documented, leading to an update in `threat-actors/`. It may expose a process gap that changes a playbook in `incident-response/`. Every action item from a postmortem should link to the file in the repo where the improvement will be documented.

## Postmortem Index

| File | Date | Severity | Summary |
|---|---|---|---|
| `2025-03-credential-stuffing-wave.md` | 2025-03-15 | SEV-2 | Large-scale credential stuffing campaign targeting buyer accounts over a 72-hour period |
| `2025-01-fake-seller-ring.md` | 2025-01-22 | SEV-2 | Coordinated fake seller ring discovered with 340+ fraudulent accounts |
