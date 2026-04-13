# HODOR Example: Misprint-Style Collectibles Marketplace

> An example Defensive Knowledge Base environment for a fictional collectibles trading platform.

## What This Environment Models

This is a fictional but realistic trust and safety environment for a marketplace where users buy, sell, and trade collectible items such as trading cards, limited edition prints, and graded collectibles. The platform supports listings, auctions, direct sales, collection portfolios, seller ratings, and price indexing.

The economics of collectibles marketplaces create a specific set of abuse incentives. Items can range from $1 to $500,000+, pricing is driven by scarcity and condition grading rather than intrinsic material value, and reputation systems heavily influence buyer trust. These dynamics attract price manipulation, seller reputation farming, account takeover targeting high-value collections, counterfeit grading, and coordinated market manipulation.

This example is inspired by the general category of collectibles marketplaces. It does not represent or claim to model any specific real company.

## Risks Modeled

| Threat | Severity | Description |
|---|---|---|
| Price Manipulation via Fake Listings | Critical | Coordinated sellers creating artificial listings to inflate perceived market value of specific items |
| Seller Reputation Farming | High | Fake accounts conducting circular transactions to build fraudulent seller credibility |
| Account Takeover of High-Value Collections | Critical | Credential stuffing and targeted attacks against accounts with valuable inventories for rapid liquidation |

## Components

### Intel Cards (`intel-cards/`)

Structured intelligence documents describing each threat with affected surfaces, recommended actions, and cross-references to controls and runbooks.

| Card | Threat |
|---|---|
| `price-manipulation-fake-listings.yaml` | Coordinated fake listing schemes that distort marketplace pricing signals |
| `seller-reputation-farming.yaml` | Circular transaction networks designed to manufacture fraudulent seller trust |
| `account-takeover-high-value-collections.yaml` | Targeted credential attacks against accounts with high-value inventories |

### Controls (`controls/`)

Detection and prevention mechanisms that address the identified threats.

| Control | Purpose |
|---|---|
| `listing-integrity-scoring.yaml` | Scores listings for pricing anomalies, fake listing signals, and coordinated manipulation |
| `seller-reputation-scoring.yaml` | Evaluates seller trustworthiness across account lifecycle, transaction patterns, and behavioral signals |

### Runbooks (`runbooks/`)

Operational response procedures for when threats are detected.

| Runbook | Scenario |
|---|---|
| `marketplace-integrity-response.yaml` | End-to-end response procedure for marketplace manipulation events including price inflation, reputation fraud, and coordinated abuse |

### Intelligence Index (`intelligence-index.yaml`)

Master cross-reference file linking all intel cards, controls, and runbooks. Every artifact is connected. No orphan objects.

## How to Use This Example

**As a learning tool:** Read through the intel cards, controls, and runbooks to understand how a Defensive Knowledge Base structures security and trust & safety knowledge for a collectibles marketplace.

**As a starting point:** Fork or copy this example, then modify the threat models, detection signals, and response procedures to match your own platform's risk landscape.

**With Claude Code:** Navigate to this directory and start a Claude Code session. Ask the agent to analyze the threat landscape, identify detection gaps, or draft new intel cards and controls based on the existing patterns.

```bash
cd examples/misprint
claude
```

> "Read the intelligence-index.yaml and all intel cards. What are the biggest detection gaps in our current control coverage?"
