# HODOR Example: CatchBack-Style Collectibles Transaction Platform

> An example Defensive Knowledge Base environment for a fictional peer-to-peer collectibles marketplace focused on transaction risk, payouts, and financial fraud.

## What This Environment Represents

This is a fictional but realistic trust and safety environment for a marketplace where users buy, sell, and trade collectible items with integrated payment processing and instant payouts. Unlike a general marketplace integrity scenario (see the Misprint example), this environment specifically models the financial abuse patterns that emerge when a platform handles money movement: payout fraud, transaction laundering, account takeover for cash-out, and coordinated fake transaction networks.

The platform supports direct sales, offers, trades, integrated payments (credit card, debit, and stored balance), seller payouts (bank transfer, instant pay), and escrow-style holds. The combination of digital collectible assets with real money movement creates a specific set of financial abuse incentives that go beyond listing manipulation.

This example is inspired by the general category of peer-to-peer collectibles and payment platforms. It does not represent or claim to model any specific real company.

## How This Differs from Marketplace Integrity

The Misprint example focuses on listing integrity, price manipulation, and reputation gaming. Those threats damage marketplace trust but don't directly steal money from the platform or its users.

CatchBack focuses on the money layer. The threats here involve real financial loss: attackers extracting funds from compromised accounts, coordinated fake transactions designed to trigger payouts of funds that don't represent genuine commerce, and rapid asset transfers used to launder proceeds before the platform can intervene. The detection signals, controls, and response procedures are oriented around transaction velocity, payment graph analysis, and payout risk rather than listing quality and reputation scores.

## Risks Modeled

| Threat | Severity | Financial Focus |
|---|---|---|
| Account Takeover for Liquidation | Critical | Compromised accounts used to sell assets and cash out proceeds via payout system |
| Payout Fraud via Fake Transactions | Critical | Coordinated fake sales between controlled accounts to trigger payout of funds with no genuine underlying commerce |
| Rapid Transfer Laundering | High | High-frequency asset movement between linked accounts to obscure provenance and extract value |

## Components

### Intel Cards (`intel-cards/`)

| Card | Threat |
|---|---|
| `account-takeover-liquidation.yaml` | Credential stuffing and session hijacking targeting accounts with stored balance or high-value inventory for rapid cash-out |
| `payout-fraud-fake-transactions.yaml` | Coordinated fake transaction networks designed to trigger the payout system and extract funds |
| `rapid-transfer-laundering.yaml` | High-frequency asset transfers between linked accounts to launder proceeds or obscure stolen goods |

### Controls (`controls/`)

| Control | Purpose |
|---|---|
| `risk-based-authentication.yaml` | Applies adaptive friction to suspicious logins to prevent ATO and session abuse |
| `transaction-risk-scoring.yaml` | Evaluates transaction legitimacy using graph, behavioral, and velocity signals to flag suspicious payment and transfer activity |

### Runbooks (`runbooks/`)

| Runbook | Scenario |
|---|---|
| `financial-abuse-response.yaml` | End-to-end incident response for account takeover cash-out, payout fraud, and suspicious transaction patterns |

### Intelligence Index (`intelligence-index.yaml`)

Master cross-reference linking all intel cards, controls, and runbooks. Every artifact is connected.

## How to Navigate

Start with `intelligence-index.yaml` to see the full threat landscape, coverage matrix, and gaps. Drill into individual intel cards for threat detail, controls for detection logic, and the runbook for response procedures.

```bash
cd examples/catchback
claude
```

> "Read the intelligence-index.yaml. What are our detection gaps for payout fraud, and what would you recommend building next?"
