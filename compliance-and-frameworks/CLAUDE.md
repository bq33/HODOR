# Compliance and Frameworks

This folder maps Prism's security posture to industry standards and regulatory requirements. Rather than treating compliance as a checkbox exercise, the team uses these frameworks as lenses to identify coverage gaps and prioritize investments.

## Frameworks We Map To

**NIST Cybersecurity Framework (CSF)** is the primary framework for overall security posture assessment. The `nist-csf/` folder contains a control mapping that documents which Prism controls satisfy each CSF function (Identify, Protect, Detect, Respond, Recover) and where gaps exist. The gap analysis is reviewed quarterly as part of the executive security review.

**NIST SP 800-63 (Digital Identity Guidelines)** is the reference standard for identity and authentication decisions. The `nist-800-63/` folder documents Prism's identity assurance levels and how the account lifecycle, IDV integrations, and authentication strategy align (or diverge) from the 800-63 guidance. This is particularly important for the identity-and-access team when making architectural decisions about authentication strength.

**MITRE ATT&CK** is the framework for detection coverage analysis. The `mitre-attack/` folder contains a technique coverage map that explicitly documents which ATT&CK techniques the team detects, which ones have partial coverage, and which ones are gaps. Navigator layer exports provide a visual heat map of coverage. This analysis drives the detection engineering roadmap — the team prioritizes building detection rules for techniques used by threat actors tracked in `threat-actors/` that currently have gaps in coverage.

**OWASP Top 10** is the reference for application security prioritization. The `owasp/` folder documents how Prism's application security program addresses each of the OWASP Top 10 risks and where additional testing or controls are needed.

**Regulatory** requirements including privacy laws, data breach notification obligations, and sector-specific regulations are tracked in `regulatory/`. These requirements inform T&S policy decisions and data handling practices.

## Key Files

| File | Description |
|---|---|
| `nist-csf/control-mapping.yaml` | Prism controls mapped to NIST CSF functions |
| `nist-csf/gap-analysis.md` | Current gaps and remediation priorities |
| `nist-800-63/identity-assurance-levels.md` | How Prism's identity architecture maps to 800-63 |
| `mitre-attack/technique-coverage.yaml` | Detection coverage by ATT&CK technique |
| `mitre-attack/navigator-layers/` | ATT&CK Navigator exports for visual coverage maps |
| `owasp/top-10-coverage.md` | OWASP Top 10 coverage assessment |
| `regulatory/privacy-requirements.md` | Applicable privacy and data protection requirements |
