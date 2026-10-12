# PP-SPEC-048: Proof of Efficacy Mapping to MITRE ATT&CK® Enterprise

| Field | Value |
|---|---|
| Status | DRAFT v0.1 |
| Author | Craig Ellrod, Nebulonium, Inc. (dba HACKERverse®) |
| Date | October 8, 2026 |
| License | CC BY 4.0 |
| Maps to | MITRE ATT&CK® Enterprise (mapped against ATT&CK v19.2) |
| Series | Proof Protocol Framework Mapping Specifications |

---

## 1. Purpose

This specification defines how MITRE ATT&CK® Enterprise tactics, techniques, sub-techniques, detection strategies, analytics, data components, mitigations, and associated threat intelligence context can be bound to Proof Protocol test cases, evidence, and efficacy results.

MITRE ATT&CK® remains authoritative for its own terminology, identifiers, content, and architecture. This document defines a **Proof Protocol mapping** and does not supersede or modify ATT&CK.

## 2. Scope

ATT&CK is a knowledge base of adversary tactics and techniques maintained by The MITRE Corporation. This mapping targets the Enterprise domain. As of October 2026 the current release is ATT&CK v19.2 (released April 28, 2026). ATT&CK v18 (October 2025) replaced technique-level detections with Detection Strategies and Analytics and deprecated Data Sources in favor of Data Components. ATT&CK v19 (April 2026) split the Enterprise Defense Evasion tactic into Stealth (TA0005) and Defense Impairment (TA0112). Mobile and ICS domains are out of scope for this version of the mapping and MAY be addressed by later specifications.

ATT&CK supplies adversary behavior context that can identify what should be exercised. Proof Protocol supplies an independent evidence model for determining what happened during a test and whether a selected defensive control performed as claimed.

Independent witnessing and evidence-capture implementation are defined elsewhere in the Proof Protocol specification family.

## 3. Core Question

Proof of efficacy asks:

> **Was there a control, and did it work?**

An ATT&CK technique can identify adversary behavior. A defensive control can claim to prevent, detect, or respond to that behavior. Proof Protocol binds the technique, test case, control, observed behavior, downstream outcome, and evidence into a result that can be independently examined.

## 4. Metric Definitions

Against a defined adversarial corpus, each case is recorded as **blocked**, **detected**, **missed**, or **INVALID**.

Relevant measurements include:

- containment rate;
- detection rate;
- miss rate;
- false-positive rate against paired benign cases;
- robustness against variants, bypass, suppression, manipulation, or evasion, including Stealth and Defense Impairment behaviors;
- version-level results; and
- INVALID status when required evidence is incomplete or broken.

Target levels are engagement- and risk-specific rather than imposed by this mapping.

## 5. Evidence Produced

Mapped tests can produce:

- **Proof records** binding ATT&CK context and version, test case, control, system/version, verdict, timestamp, and evidence references;
- **ProofStamp™** trusted timestamps bound to evidence/verdict objects;
- **ProofBundle™** packages containing proof records, metrics, corpus manifests, and environment/context;
- **ProofRegister™** records for issued proof artifacts; and
- corpus and environment manifests identifying the tested adversarial conditions.

## 6. Mapping to MITRE ATT&CK® Enterprise

ATT&CK identifiers SHOULD be recorded exactly as published in the ATT&CK version being mapped (for example TA0002 for a tactic, T1059.001 for a sub-technique, G0034 for a group, S0677 for software, C0025 for a campaign, and DET0001 for a detection strategy), together with the ATT&CK version and domain. This specification does not redefine ATT&CK objects.

| MITRE ATT&CK® context | Proof Protocol treatment | Evidence |
|---|---|---|
| Tactic (TA####) | Record the adversary objective as test context. | Corpus/test metadata |
| Technique (T####) | Bind the technique identifier to one or more reproducible test cases. | Proof record; corpus manifest |
| Sub-technique (T####.###) | Represent the specific variant exercised. | Test-case evidence |
| Procedure example, Group, Software, or Campaign | Use as threat-intelligence context for independently authored test conditions; do not replay third-party malware outside a controlled environment. | Corpus metadata |
| Detection Strategy (DET####) | Record the detection approach the control claims to implement, separately from observed effect. | Control descriptor |
| Analytic | Bind the specific analytic or rule logic under test, with its version, to the detection claim. | Control descriptor; detection result |
| Data Component | Record which telemetry the detection depends on and whether that telemetry was actually present during the test. | Telemetry/log evidence |
| Mitigation | Record the asserted preventive control separately from observed effect. | Control descriptor |
| Technique execution | Capture evidence that the adversarial condition was actually exercised. | Execution evidence |
| Detection outcome | Record whether the control identified the exercised condition. | Detection result |
| Prevention/containment outcome | Determine whether the adversarial objective reached the protected target. | Target/outcome evidence |
| Platform and system/version context | Bind ATT&CK version, domain, platform, and material control, policy, sensor, and environment versions to the result. | Environment descriptor |

## 7. Interoperability Rules

1. The ATT&CK version, domain, and applicable tactic, technique, sub-technique, detection strategy, or other identifier SHOULD be recorded when applicable.
2. ATT&CK identifiers, names, and terminology MUST NOT be silently redefined.
3. Proof Protocol verdicts are Proof Protocol results; they are not MITRE scores, certifications, or endorsements.
4. A control's presence, configuration, activation, and efficacy are distinct facts.
5. A policy decision, alert, or control trigger does not by itself establish efficacy when the claim concerns a downstream protected outcome.
6. Target, application, tool, SIEM, vendor, or equivalent evidence SHOULD complete the evidence round trip when required to establish the result.
7. Missing required evidence MUST yield **INVALID**, not PASS.
8. Material changes to the tested system, model, policy, tools, permissions, control, environment, ATT&CK mapping, or corpus SHOULD trigger retesting where they can affect the result.
9. ATT&CK coverage (the count or share of techniques for which a control claims a mitigation or detection) MUST NOT be reported as efficacy. Only exercised, evidenced test cases yield Proof Protocol results.
10. Revoked or deprecated ATT&CK objects SHOULD be recorded with their status and, where available, the replacing object.

## 8. Framework-Agnostic Architecture

> **Threat frameworks are pluggable inputs to Proof Protocol. Proof Protocol is framework-agnostic.**

External frameworks can identify **what to test**: threats, vulnerabilities, techniques, risk categories, controls, design assertions, identity claims, tool permissions, or other risk conditions. Proof Protocol independently establishes **whether the control worked and what evidence proves that result**.

No external framework is required for Proof Protocol to operate. A Proof Protocol implementation MAY use MITRE ATT&CK®, MITRE ATLAS, MITRE D3FEND™, CSA MAESTRO, OWASP, AIVSS, AAGATE, a proprietary threat model, another recognized framework, or no external framework at all when the test condition is otherwise sufficiently defined.

Adding, replacing, muting, or removing a framework mapping does not alter the Proof Protocol architecture, evidence model, Proof of Efficacy determination, ProofBundle™, ProofStamp™, ProofRegister™, or independent corroboration requirements.

A framework mapping therefore establishes **interoperability**, not architectural dependency.

## 9. Relationship to Proof Protocol

This mapping is part of the Proof Protocol specification family maintained by Nebulonium, Inc.

The relationship is intentionally asymmetric:

> **MITRE ATT&CK® supplies adversary tactic, technique, and detection context. Proof Protocol supplies the evidence model for determining whether a selected defensive control performed as claimed.**

No affiliation, endorsement, certification, or sponsorship by MITRE is implied.

## 10. Source Framework, Attribution, and License

MITRE ATT&CK® is external work maintained by The MITRE Corporation. MITRE names, ATT&CK names, identifiers, trademarks, and expressive framework content remain subject to MITRE's applicable terms.

The ATT&CK Terms of Use (https://attack.mitre.org/resources/legal-and-branding/terms-of-use/) grant a non-exclusive, royalty-free license to use ATT&CK for research, development, and commercial purposes. Any copy made for such purposes is authorized provided that MITRE's copyright designation and the license are reproduced in that copy. The Terms of Use state that MITRE does not claim ATT&CK enumerates all possible adversary behaviors and that using ATT&CK to address full categories of techniques will not guarantee full defensive coverage. ATT&CK is provided on an "as is" basis. MITRE's FAQ governs how the ATT&CK name may be used and represented.

This Proof Protocol mapping is independently authored and Licensed under the Greater Good Commercial License 1.0 (see LICENSE.md); text CC BY-ND 4.0 under its Part S. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).

### Required attribution

The ATT&CK Terms of Use (https://attack.mitre.org/resources/legal-and-branding/terms-of-use/) require the following copyright designation, quoted verbatim, on any copy of ATT&CK content:

> © 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation.

The ATT&CK website carries the following trademark statement, quoted verbatim:

> MITRE ATT&CK and ATT&CK are registered trademarks of The MITRE Corporation.

Source cited: MITRE ATT&CK® Enterprise, version 19.2, https://attack.mitre.org/.

This specification reproduces only ATT&CK identifiers, object type names, tactic names, and short factual statements about ATT&CK structure and releases. It does not reproduce ATT&CK technique descriptions, procedure examples, detection strategy or analytic content, mitigation text, or STIX data. The copyright designation and trademark statement above are nonetheless carried in this specification, the README, and the LICENSE file. Implementations that include ATT&CK content in a ProofBundle™ or corpus manifest MUST reproduce MITRE's copyright designation and license with that content as the Terms of Use require.

## 11. Versioning

This mapping is versioned independently of MITRE ATT&CK®. This version was prepared against ATT&CK v19.2. ATT&CK publishes major releases on a recurring schedule; each ProofBundle™ SHOULD record the ATT&CK version and domain used. Material upstream changes, including new, split, revoked, or deprecated objects, SHOULD trigger a mapping review and, where necessary, a new version identifying the ATT&CK release mapped.

---

*Proof Protocol · proofprotocol.io · CC BY 4.0*
