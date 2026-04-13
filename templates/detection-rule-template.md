# Detection Rule: [Rule Name]

> **Rule ID:** DR-[NNN]
> **Author:** [Name]
> **Created:** YYYY-MM-DD
> **Last tuned:** YYYY-MM-DD
> **Status:** [Draft / Testing / Active / Deprecated]
> **Severity on trigger:** [Critical / High / Medium / Low / Informational]

## Purpose

What does this rule detect and why does it matter? Link to the threat pattern, attack technique, or adversary behavior that motivated this rule.

**Threat addressed:** [Link to entry in `intelligence-index.yaml`]
**MITRE ATT&CK technique(s):** [T-number(s) with names]
**Threat actor(s):** [Link to actor profile(s) in `threat-actors/` if applicable]

## Detection Logic

Describe the detection logic in plain language first, then provide the technical implementation. The plain language description ensures that someone unfamiliar with the query language can understand what the rule does and evaluate whether the logic is sound.

**Plain language:** When [condition], within [time window], involving [entity type], trigger an alert if [threshold] is exceeded.

**Technical implementation:**

```
[Query or rule logic in the team's SIEM/detection language]
```

## Data Sources

| Source | Field(s) Used | Latency | Reliability |
|---|---|---|---|
| [Data source name] | [Specific fields queried] | [How fast data arrives] | [How complete/reliable the data is] |

## Thresholds and Tuning

| Parameter | Current Value | Last Changed | Rationale |
|---|---|---|---|
| [Threshold name] | [Value] | YYYY-MM-DD | [Why this value was chosen] |

### Tuning History

Document every threshold change with the date, the old value, the new value, and the reason for the change. This history is critical for understanding why the rule behaves the way it does and for AI agents assisting with future tuning.

| Date | Parameter | Old Value | New Value | Reason |
|---|---|---|---|---|
| YYYY-MM-DD | [Parameter] | [Old] | [New] | [What prompted the change] |

## Known False Positive Patterns

Document the patterns that cause this rule to fire on legitimate activity. For each pattern, describe the behavior, how frequently it occurs, and the current mitigation (suppression, allowlist, or contextual filter).

| Pattern | Frequency | Mitigation |
|---|---|---|
| [Description of benign behavior that triggers the rule] | [How often] | [How we handle it] |

## Response Procedure

What should an analyst do when this rule fires?

1. **Triage:** [Initial assessment steps]
2. **Investigate:** [What to look at next]
3. **Escalate if:** [Conditions that require escalation]
4. **Playbook:** [Link to full playbook in `incident-response/playbooks/` if applicable]

## Performance Metrics

| Metric | Current Value | Target | Measurement Period |
|---|---|---|---|
| True positive rate | | | |
| False positive rate | | | |
| Mean time to triage | | | |
| Alert volume (daily avg) | | | |

## Related Artifacts

| Type | Link |
|---|---|
| Intelligence index entry | [Link to threat in `intelligence-index.yaml`] |
| Threat model | [Link to relevant threat model] |
| Controls | [Link to complementary controls in `detections-and-controls/controls/`] |
| Postmortem(s) | [Link to postmortems where this rule was relevant] |
| MITRE coverage | [Link to technique in `compliance-and-frameworks/mitre-attack/technique-coverage.yaml`] |
