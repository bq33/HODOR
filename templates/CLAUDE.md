# Templates

This folder contains reusable templates for all major artifact types in the HODOR repo. When creating a new document, start with the appropriate template to ensure consistency across the team and to make it easier for AI agents to parse and cross-reference artifacts.

## Available Templates

| Template | Used For |
|---|---|
| `threat-actor-template.md` | New threat actor profile in `threat-actors/` |
| `detection-rule-template.md` | New detection rule in `detections-and-controls/detection-rules/` |
| `playbook-template.md` | New incident response playbook in `incident-response/playbooks/` |
| `postmortem-template.md` | New postmortem in `postmortems/` |
| `campaign-template.md` | New campaign or incident in `campaigns-and-incidents/` |
| `vulnerability-template.md` | New vulnerability assessment in `vulnerabilities-and-exposures/` |
| `investigation-template.md` | New investigation case file in `investigations/` |
| `rfc-template.md` | New engineering RFC in `engineering/RFCs/` |
| `experiment-template.md` | New experiment in `metrics-and-reporting/experiments/` |
| `exec-quarterly-review-template.md` | Quarterly security review for leadership |
| `exec-incident-summary-template.md` | Executive incident summary |
| `exec-threat-brief-template.md` | Threat landscape brief for leadership |
| `source-template.yaml` | New intelligence source in `source-registry/` |

## Template Philosophy

Templates exist to encode the team's best thinking about what information matters for each artifact type. A detection rule template ensures every rule documents its data sources, tuning history, and false positive patterns because the team learned the hard way that rules without this context are impossible to maintain. A postmortem template ensures every retrospective captures action items with owners because action items without owners never get done.

When adapting templates for a new use case, add fields rather than removing them. If a field doesn't apply, mark it as "N/A" rather than deleting it, so the AI agent still knows the field exists in the schema.
