# Threat Actors

This folder contains profiles of threat actors that are relevant to Prism's attack surface. Each profile follows a standard template and links outward to detection rules, playbooks, campaigns, and MITRE ATT&CK mappings throughout the repo.

## How to Use Threat Actor Profiles

Threat actor profiles serve three purposes. First, they help the team understand *who* is attacking us and *how*, so that defenses can be designed around actual adversary behavior rather than theoretical risks. Second, they provide the AI agent with context to write better detection rules, because a rule designed to catch a specific actor's known techniques is more effective than a generic anomaly detector. Third, they create institutional memory so that when an actor resurfaces, the team doesn't start from scratch.

## Active Threat Actors

| Actor | Type | Primary TTPs | Relevance to Prism |
|---|---|---|---|
| [Marketplace Fraud Rings](marketplace-fraud-rings.md) | Organized crime | Credential stuffing, fake accounts, payment fraud | Direct — active against Prism |
| [Scattered Spider](scattered-spider.md) | Cybercrime group | Social engineering, SIM swapping, identity provider attacks | Indirect — targets our sector |
| [LockBit](lockbit.md) | Ransomware operator | Initial access brokering, double extortion, data encryption | Indirect — sector-wide risk |
| [Bot Operators](bot-operators.md) | Tooling providers | Automated scraping, inventory hoarding, queue manipulation | Direct — active against Prism |
| [Social Engineering Crews](social-engineering-crews.md) | Cybercrime | Phishing, vishing, pretexting, help desk manipulation | Direct — targets Prism employees |
| [Carding Networks](carding-networks.md) | Financial crime | Stolen card testing, payment fraud, refund abuse | Direct — active against Prism |
| [Counterfeit Sellers](counterfeit-sellers.md) | Marketplace abuse | Fake listings, brand impersonation, review manipulation | Direct — active against Prism |
| [Scam Operators](scam-operators.md) | Consumer fraud | Advance-fee schemes, phishing via messaging, fake support | Direct — targets Prism users |
| [Reseller Networks](reseller-networks.md) | Gray market | Bulk purchasing, inventory hoarding, price manipulation | Direct — active against Prism |
| [BlackCat/ALPHV](blackcat-alphv.md) | Ransomware operator | Data exfiltration, triple extortion, affiliate model | Indirect — sector-wide risk |

## How to Add a New Threat Actor

1. Copy `actor-template.md` to a new file named after the actor (use kebab-case).
2. Fill in all sections, especially the MITRE ATT&CK mapping and known indicators.
3. Link the new actor profile in the `intelligence-index.yaml` under all relevant threat entries.
4. Update this CLAUDE.md with the new actor in the table above.
5. Notify #threat-intel in Slack with a summary of the new profile.
