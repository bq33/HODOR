# Account Quality Scoring Model

> **Owner:** Maya Chen (PM), Kenji Tanaka (Data Science)
> **Last updated:** 2025-04-01
> **Version:** 1.4
> **Status:** Active in production
> **RFC for v2:** [rfc-001-account-quality-v2.md](../../engineering/RFCs/rfc-001-account-quality-v2.md)

## Overview

The Account Quality Model (AQM) assigns every Prism account a quality tier that reflects the platform's confidence in the account's legitimacy and trustworthiness. The model ingests signals from registration behavior, authentication patterns, transaction history, and platform activity to produce a composite quality score. That score determines the tier, and the tier determines what level of friction or privilege the account receives across the platform.

The model's purpose is to create a system where legitimate users earn trust over time and that trust translates into a smoother experience, while adversarial actors face escalating friction that makes abuse economically unviable. The key design principle is proportional friction: the platform should feel seamless for users who have demonstrated trustworthy behavior and progressively more challenging for users who haven't.

## Language Convention

When communicating externally (to users, partners, executives, or in any customer-facing context), the team uses "higher quality" and "lower quality" to describe account tiers. We avoid "high risk" and "low risk" terminology because risk framing creates confusion about whose risk is being assessed: the risk the user poses to the platform is different from the risk the platform poses to the user, and conflating the two leads to misunderstanding. Internally, the team may use shorthand tier names (T1 through T5) for efficiency.

## Tier Definitions

### Tier 1: Highest Quality

These accounts have demonstrated sustained trustworthy behavior over an extended period. They have verified identities, strong authentication (passkeys or authenticator-based MFA), clean transaction histories, and consistent platform engagement patterns. T1 accounts represent approximately 8% of the active user base and are Prism's most valuable users.

**Experience:** Minimal friction. Expedited checkout. Higher transaction limits. Priority customer support. Trusted seller badges (for sellers). Skip most interactive challenges.

**Qualifying signals:** Account age >12 months with consistent activity. Identity verified through IDV. Passkey or authenticator MFA enrolled. Zero confirmed fraud incidents. Transaction history with <0.1% dispute rate. Behavioral consistency score >0.9.

### Tier 2: High Quality

Established accounts with good track records but without the full verification depth of T1. They have meaningful transaction history, active authentication beyond password-only, and no fraud flags. T2 accounts represent approximately 22% of the active user base.

**Experience:** Low friction. Standard transaction limits. Normal checkout flow. Occasional step-up verification for high-value transactions.

**Qualifying signals:** Account age >6 months with activity in at least 3 of the last 6 months. SMS MFA or better enrolled. Transaction history with <0.5% dispute rate. No account security incidents in the last 12 months. Behavioral consistency score >0.7.

### Tier 3: Standard Quality

The default tier for accounts that have some history but haven't yet accumulated enough positive signals to move higher, or that have mixed signals. This is the largest segment, representing approximately 45% of the active user base.

**Experience:** Standard friction. Normal transaction limits with step-up verification for high-value actions. Standard challenge frequency. Standard seller verification requirements.

**Qualifying signals:** Account age >30 days. At least one completed transaction. Email verified. No active fraud flags. Behavioral consistency score >0.4.

### Tier 4: Elevated Review

Accounts that exhibit signals requiring additional scrutiny but have not been confirmed as fraudulent. These may be new accounts, accounts with inconsistent behavior, accounts that triggered detection rules but were not confirmed as threats, or accounts recovering from a security incident. T4 represents approximately 18% of the active user base.

**Experience:** Increased friction. Lower transaction limits. More frequent challenges. Step-up verification required for all high-value actions. Seller listing review required before publication. Payment hold periods for new sellers.

**Qualifying signals:** Account age <30 days, or triggered one or more detection rules without confirmation, or account recently recovered from compromise, or behavioral consistency score <0.4, or email domain flagged as high-risk.

### Tier 5: Lowest Quality

Accounts with strong indicators of inauthenticity or abuse but not yet confirmed and actioned by the T&S team. These accounts are under active review or restricted pending investigation. T5 represents approximately 7% of active accounts at any given time, though the population turns over rapidly as accounts are either cleared or suspended.

**Experience:** Maximum friction. Severely restricted transaction capabilities. All actions require challenge completion. Seller privileges suspended pending review. Payment processing suspended for new transactions.

**Qualifying signals:** Multiple detection rules triggered, or flagged by fraud analyst, or linked to known fraud ring infrastructure, or identity verification failed, or behavioral pattern consistent with automation.

## Signal Catalog

The model ingests signals across four categories. Each signal has a weight that reflects its predictive power for distinguishing legitimate from adversarial accounts. Weights are tuned quarterly by the data science team based on model performance analysis.

### Registration Signals

| Signal | Weight | Description |
|---|---|---|
| Registration velocity from source | 0.15 | How many accounts were created from the same IP/device/email domain in the surrounding time window |
| Email domain reputation | 0.10 | Whether the email domain is a known disposable service, a custom domain with no web presence, or a major provider |
| Registration completeness | 0.05 | Whether the user completed optional profile fields during registration (name, phone, profile photo) |
| Device fingerprint novelty | 0.10 | Whether the device fingerprint has been seen before in association with other accounts |
| Geographic consistency | 0.05 | Whether the registration IP location is consistent with the provided address information |

### Authentication Signals

| Signal | Weight | Description |
|---|---|---|
| MFA enrollment type | 0.15 | Passkey (highest weight), authenticator app (high), SMS (moderate), none (lowest) |
| Login pattern consistency | 0.10 | Whether the user logs in from consistent devices, locations, and times |
| Failed login frequency | 0.05 | Rate of failed login attempts on this account (may indicate targeting by attackers) |
| Session behavior | 0.05 | Whether sessions show normal human browsing patterns or anomalous navigation |

### Transaction Signals

| Signal | Weight | Description |
|---|---|---|
| Transaction history depth | 0.10 | Number and value of completed transactions over time |
| Dispute and chargeback rate | 0.15 | Percentage of transactions resulting in disputes or chargebacks |
| Payment method stability | 0.05 | Whether the user maintains consistent payment methods or frequently adds and removes cards |
| Shipping address consistency | 0.05 | Whether orders ship to consistent addresses or frequently change destinations |

### Behavioral Signals

| Signal | Weight | Description |
|---|---|---|
| Behavioral consistency score | 0.15 | Composite score measuring how consistent the user's platform behavior is over time (browsing patterns, search behavior, interaction timing) |
| Account change velocity | 0.10 | Rate of changes to account details (email, phone, password, payment methods) in a given window |
| Platform engagement depth | 0.05 | Whether the user engages with multiple platform features or only transactional features |
| Peer network quality | 0.05 | Quality tiers of accounts the user interacts with (buys from, sells to, messages) |

## Tier Transitions

Accounts move between tiers based on signal accumulation over time. Upward movement (toward higher quality) is gradual and requires sustained positive signals. Downward movement (toward lower quality) can be rapid when strong negative signals appear.

**Upward transition rules:** An account can move up one tier per evaluation period (monthly). Moving from T3 to T2 requires 6 months of consistent positive signals. Moving from T2 to T1 requires identity verification and phishing-resistant MFA enrollment in addition to sustained positive signals. Upward movement is blocked while any active investigation or detection flag exists on the account.

**Downward transition rules:** An account can drop multiple tiers in a single evaluation if strong negative signals appear. A confirmed account takeover immediately drops the account to T4 pending recovery. A confirmed fraud flag immediately drops the account to T5. A detection rule trigger drops the account by one tier pending review.

**Recovery:** Accounts that were compromised and recovered can rebuild quality, but the recovery path is slower than initial quality building. A recovered account must demonstrate 3 months of clean behavior at T4 before returning to T3, and 6 months of clean behavior to return to its pre-compromise tier.

## Model Performance

| Metric | Current Value | Target | Measurement Period |
|---|---|---|---|
| Fraud rate in T1 accounts | 0.02% | <0.05% | Q1 2025 |
| Fraud rate in T2 accounts | 0.08% | <0.1% | Q1 2025 |
| Fraud rate in T3 accounts | 0.4% | <0.5% | Q1 2025 |
| Fraud rate in T4 accounts | 2.1% | <3% | Q1 2025 |
| Fraud rate in T5 accounts | 12.8% | N/A (expected to be high) | Q1 2025 |
| False positive rate (legitimate users in T4/T5) | 4.2% | <5% | Q1 2025 |
| Tier distribution stability | Low churn | Stable month-over-month | Q1 2025 |

## v2 Roadmap

The v2 model (documented in [RFC-001](../../engineering/RFCs/rfc-001-account-quality-v2.md)) introduces three major improvements. First, session-level behavioral analysis that evaluates quality signals within individual sessions rather than only at the account level, enabling faster detection of compromised accounts being operated by an attacker. Second, graph-based peer network analysis that considers the quality of accounts in a user's transaction and interaction network, which is particularly effective at identifying fraud ring participants. Third, real-time score updates that adjust quality in near-real-time as signals arrive rather than in batch evaluation cycles, reducing the window between a negative signal appearing and the account being downgraded.
