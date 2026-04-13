# Campaigns and Incidents

This folder tracks coordinated attack campaigns and significant security events, both those targeting Prism directly and those affecting the broader sector that may foreshadow similar activity against us.

## The Distinction Between Campaigns and Incidents

A **campaign** is a coordinated, time-bound operation conducted by a threat actor or group. It may involve multiple attack techniques, target multiple parts of the platform, and span days or weeks. A campaign may produce zero, one, or many internal incidents. The campaign file documents the adversary's operation as a whole.

An **incident** is a specific security event that triggered our detection and response process. An incident may be part of a larger campaign, or it may be an isolated event. Incidents that reach SEV-1 or SEV-2 get their own postmortem in `postmortems/`.

## Folders

**active/** contains campaigns and incidents currently in progress. Files here are living documents updated as the situation evolves. When a campaign or incident is resolved, it moves to `archive/` with a final status summary.

**archive/** contains resolved campaigns and incidents with their complete documentation. These serve as institutional memory and training material for the team and for AI agents that need to understand historical patterns.

## How to Document a New Campaign

1. Create a new file in `active/` using the campaign template from `templates/campaign-template.md`.
2. Link the campaign to the relevant threat actor(s) in `threat-actors/`.
3. Add the campaign to `intelligence-index.yaml` under the relevant threat entries.
4. Notify #threat-intel and #security-incidents in Slack.
5. When resolved, move the file to `archive/` and add a resolution summary.
