# Investigations

This folder contains active and closed investigation case files. Investigations are distinct from incident response: they are proactive, deeper-dig efforts to understand patterns, attribute activity, or assess exposure, rather than reactive responses to active incidents.

## Types of Investigations

**Fraud ring analysis** identifies and maps coordinated networks of accounts involved in organized fraud. These investigations often start with a single suspicious account and expand to reveal a network connected by shared devices, payment methods, behavioral patterns, or communication channels.

**Threat actor attribution** links observed activity to known threat actors or identifies new actors. These investigations draw on intelligence from `threat-intelligence/` and actor profiles from `threat-actors/`.

**Vulnerability impact assessment** determines the scope of exposure from a newly disclosed or discovered vulnerability. These investigations assess whether the vulnerability was exploited before it was patched and what data or systems may have been affected.

**Policy violation patterns** analyze trends in policy violations to identify systemic issues, repeat offenders, or emerging abuse vectors that current rules don't adequately address.

## Folders

**active/** contains investigations currently in progress. These files are living documents and may contain sensitive information about ongoing cases.

**closed/** contains completed investigations with findings, conclusions, and recommended actions. These serve as reference material for future investigations and training material for new analysts.

## Starting a New Investigation

Use the template from `templates/investigation-template.md`. Every investigation should have a clearly stated hypothesis, defined scope, evidence log, and timeline. When an investigation concludes, document the findings, any enforcement actions taken, and recommendations for systemic improvements.
