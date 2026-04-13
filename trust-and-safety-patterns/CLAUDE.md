# Trust and Safety Patterns

This folder documents the abuse patterns and platform integrity challenges specific to Prism's marketplace. While `threat-actors/` profiles the adversaries and `detections-and-controls/` documents how we catch them, this folder focuses on the patterns of abuse themselves: what the abuse looks like, how it impacts the platform and users, and how the team thinks about preventing it.

## Folders

**fraud-typologies/** documents the specific types of fraud observed on the Prism platform. Each typology describes the mechanics of the fraud, the signals that indicate it, the user impact, and the team's current mitigation approach. Typologies include account takeover, payment fraud, card testing, fake accounts, promotion abuse, and refund abuse.

**content-moderation/** documents the content moderation taxonomy, review queue design, and escalation procedures for content that violates Prism's acceptable use policy.

**bot-detection/** documents the behavioral signals and challenge strategies used to distinguish automated abuse from legitimate user activity. This includes device fingerprinting approaches, interaction pattern analysis, and progressive challenge design.

**marketplace-abuse/** documents abuse patterns specific to the marketplace model, including counterfeit listings, review manipulation, seller impersonation, and price manipulation.

## Connection to Other Folders

Trust and safety patterns inform detection rule development in `detections-and-controls/`. When a new fraud typology is identified, the next step is to design detection rules that catch it and controls that prevent it. The patterns documented here are the "what" and "why" that give detection engineers the context to build the "how."
