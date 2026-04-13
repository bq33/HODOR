# Metrics and Reporting

This folder contains the KPI definitions, dashboard specifications, and experiment frameworks that the Prism security and T&S team uses to measure effectiveness and make data-driven decisions.

## Folders

**kpis/** contains the canonical definitions of all security and trust & safety key performance indicators. Each KPI has a precise definition, data source, calculation methodology, target value, and escalation threshold. When leadership asks "what's our ATO rate?" the answer comes from the definition in this folder, ensuring consistency across reports and conversations.

**dashboards/** contains the specifications for operational and executive dashboards. Each dashboard spec documents what it shows, why it matters, where the data comes from, and how to interpret the visualizations. Dashboard specs are used by the data engineering team to build and maintain actual dashboards, and by the AI agent to understand what metrics are available.

**experiments/** contains documentation of A/B tests and controlled experiments run by the security and T&S team. Experiments include hypothesis, methodology, results, and conclusions. These are particularly important for changes to challenge strategies, friction flows, and detection thresholds where the team needs to balance security effectiveness with user experience impact.

## Key Files

| File | Description |
|---|---|
| `kpis/security-kpis.md` | All cybersecurity KPIs: ATO rate, credential stuffing block rate, mean time to detect, mean time to contain, phishing click rate |
| `kpis/trust-safety-kpis.md` | All T&S KPIs: fake account detection rate, content removal rate, time to action, appeal overturn rate, bot detection rate |
| `dashboards/fraud-ops-dashboard.md` | Operational dashboard for the fraud and abuse team |
| `dashboards/incident-metrics.md` | Dashboard tracking incident volume, severity, and response times |
| `experiments/experiment-template.md` | Template for documenting new experiments |
