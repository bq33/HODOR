# Incident Response

This folder contains the playbooks, runbooks, and procedures the Prism security team follows when responding to security incidents and trust & safety escalations.

## Severity Classification

Incident severity follows the definitions in `taxonomy/severity-levels.md`. The summary for quick reference during active incidents is below.

**SEV-1 (Critical)** — Active data breach, ransomware deployment, mass account takeover, or platform-wide outage caused by a security event. Response SLA: 15 minutes to assemble incident commander. All-hands war room. Executive notification required.

**SEV-2 (High)** — Confirmed targeted attack in progress, significant fraud spike, vulnerability actively being exploited against Prism, or localized service degradation from security event. Response SLA: 1 hour. Dedicated incident channel. Manager notification required.

**SEV-3 (Medium)** — Suspicious activity under investigation, fraud pattern requiring rule adjustment, or vulnerability with no evidence of active exploitation. Response SLA: 4 hours. Handled within normal on-call rotation.

**SEV-4 (Low)** — Minor policy violation, isolated abuse report, or informational security alert. Response SLA: 24 hours. Handled async during business hours.

## Playbooks

Playbooks are step-by-step response procedures for specific incident types. Each playbook defines the trigger conditions, immediate actions, investigation steps, containment measures, recovery procedures, and communication templates.

| Playbook | Triggers |
|---|---|
| `playbooks/ato-response.md` | Confirmed account takeover of individual or small batch of accounts |
| `playbooks/mass-ato-response.md` | Large-scale credential stuffing or identity provider compromise affecting many accounts |
| `playbooks/ransomware-response.md` | Ransomware indicators detected on any Prism system |
| `playbooks/data-breach.md` | Confirmed unauthorized access to customer or employee PII |
| `playbooks/payment-fraud-response.md` | Significant spike in fraudulent transactions or chargebacks |
| `playbooks/phishing-response.md` | Phishing campaign targeting Prism employees or customers |
| `playbooks/fake-account-ring-takedown.md` | Discovery of coordinated fake account network |
| `playbooks/bot-mitigation-response.md` | Automated abuse exceeding normal thresholds |
| `playbooks/content-moderation-escalation.md` | Content requiring urgent legal, safety, or PR escalation |

## On-Call Rotation

The on-call schedule and escalation procedures are documented in `team/processes/on-call-rotation.md`. The incident commander role rotates weekly among senior engineers (James, Priya, Liam) with Carlos as the T&S escalation point.

## After the Incident

Every SEV-1 and SEV-2 incident requires a postmortem within 5 business days. Postmortems are documented in `postmortems/` using the standard template. Postmortems are blameless — the goal is to improve systems and processes, not to assign fault.
