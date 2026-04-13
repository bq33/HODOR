# Identity and Access

This folder documents Prism's approach to user identity, authentication, and account trust. It covers the full account lifecycle from registration through deactivation, the account quality scoring model, authentication strategy, and identity verification integrations.

## Philosophy

The identity layer is where security and user experience collide most directly. Every additional verification step makes the platform safer but risks losing legitimate users to friction. The team's operating principle is that friction should be proportional to risk: higher-quality accounts with established trust signals should move through the platform with minimal friction, while newer or lower-quality accounts encounter progressive verification challenges as they attempt higher-value actions.

This is not about blocking users. It is about building a system where legitimate users earn trust over time and that trust translates to a better experience, while adversarial actors face escalating challenges that make abuse economically unviable.

## Folders

**account-lifecycle/** documents the major touchpoints in a user's journey with the platform. Registration, authentication, account recovery, and deactivation each have their own document covering the current flow, known vulnerabilities, and planned improvements. These documents are the primary reference for product and engineering teams building identity features.

**account-quality/** contains the scoring model that assigns quality tiers to every Prism account. The model ingests signals from registration behavior, authentication patterns, transaction history, and platform activity to produce a quality score that determines what level of friction or privilege an account receives. The tier definitions, signal catalog, and enforcement rules are all documented here.

**authentication/** covers the technical authentication strategy including passkey implementation, MFA approach, and session management. These documents are the reference for security engineering decisions about how users prove their identity.

**identity-verification/** documents integrations with external IDV providers and the step-up authentication triggers that require users to verify their identity for high-risk actions.

## Key Files

| File | Description |
|---|---|
| `account-lifecycle/registration.md` | Registration flow, bot detection at sign-up, progressive profiling |
| `account-lifecycle/authentication.md` | Login flow, credential validation, session creation |
| `account-lifecycle/recovery.md` | Account recovery flow, security considerations, abuse vectors |
| `account-lifecycle/deactivation.md` | Account closure, data retention, reactivation policy |
| `account-quality/CLAUDE.md` | Overview of the account quality model |
| `account-quality/scoring-model.md` | Quality tier definitions, scoring algorithm, signal weights |
| `account-quality/signal-catalog.md` | All signals feeding the quality model with descriptions and data sources |
| `account-quality/tier-enforcement.md` | What each quality tier can and cannot do on the platform |
| `authentication/passkeys.md` | Passkey implementation strategy and rollout plan |
| `authentication/mfa-strategy.md` | MFA approach, supported methods, and migration plan away from SMS |
| `authentication/session-management.md` | Session creation, validation, rotation, and revocation |
| `identity-verification/idv-integrations.md` | External IDV provider integrations and evaluation criteria |
| `identity-verification/step-up-auth.md` | Triggers and flows for step-up identity verification |
