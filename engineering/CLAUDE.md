# Engineering

This folder contains the security engineering team's architecture documentation, RFCs, and technical design decisions. While other folders document what the team defends against and how it responds, this folder documents how the security infrastructure is built.

## Folders

**architecture/** contains system design documentation including data flow diagrams, service architecture, and infrastructure topology relevant to security operations. These documents help engineers and AI agents understand how Prism's security systems are connected and where data flows between services.

**RFCs/** contains technical design proposals for significant security engineering changes. RFCs go through a review process before implementation and serve as the permanent record of why architectural decisions were made. Each RFC uses the template in `templates/rfc-template.md` and documents the problem, proposed solution, alternatives considered, security implications, and rollout plan.

## Key Files

| File | Description |
|---|---|
| `architecture/system-overview.md` | High-level architecture of Prism's security infrastructure |
| `architecture/data-flow-diagrams.md` | How security-relevant data flows through the platform |
| `RFCs/CLAUDE.md` | Index of all RFCs and their status |
| `RFCs/rfc-template.md` | Standard template for new RFCs |
| `RFCs/rfc-001-account-quality-v2.md` | RFC for the next generation of the account quality scoring model |
