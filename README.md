# ISO 27001 Practice Lab

A browser-based, hands-on lab that works through the core ISO/IEC 27001:2022 management cycle for a fictional managed cloud and SOC-as-a-service provider, **Harbourline Cloud Services**.

Each module presents a realistic decision, asks for an answer, then compares it with a model answer and explains the reasoning with references to the standard and to relevant regulation.

**Live demo:** `https://brown-jerry.github.io/iso27001-practice-lab/` *(available once GitHub Pages is enabled)*

---

## Contents

1. [Objectives](#objectives)
2. [Skills demonstrated](#skills-demonstrated)
3. [Scenario](#scenario)
4. [Modules](#modules)
5. [Risk methodology](#risk-methodology)
6. [Risk register summary](#risk-register-summary)
7. [Incident response model](#incident-response-model)
8. [How to use](#how-to-use)
9. [Repository structure](#repository-structure)
10. [References](#references)
11. [Assumptions and limitations](#assumptions-and-limitations)
12. [How this was built](#how-this-was-built)
13. [Author](#author)

---

## Objectives

- Apply the ISO/IEC 27001:2022 cycle (Clauses 4 to 10) to a realistic organisation, not in the abstract.
- Practise the decisions an Information Security Officer makes: scoring risk, choosing controls, justifying applicability, grading audit findings, running an incident and preparing a management review.
- Connect the ISMS to legal obligations that apply to a managed service provider in the EU: GDPR breach notification and NIS2 incident reporting.

## Skills demonstrated

| Area | What the lab covers |
|------|---------------------|
| Governance | ISMS scope definition, interested parties, management review inputs and outputs |
| Risk management | Acceptance criteria, likelihood and impact scoring, risk owners, residual risk |
| Controls | Selecting ISO 27001:2022 Annex A controls, using all four treatment options |
| Compliance | Statement of Applicability with justified inclusions and exclusions |
| Audit | Distinguishing conformity, observations, minor and major nonconformities |
| Incident response | Containment, escalation, controller and processor roles, the 72 hour clock |
| Regulation | GDPR Art. 28 and 33, NIS2 Art. 23 |

## Scenario

**Harbourline Cloud Services** (fictional) provides:

- Managed cloud hosting for about 300 SME and fintech customers
- A 24/7 SOC-as-a-service built on a shared, multi tenant logging platform
- A remote management tool and a monitoring agent on about 4,000 customer servers
- A customer self-service portal developed in house
- Customer backups in cloud object storage

**ISMS scope:** delivery of managed hosting and SOC services, including the portal, logging platform, remote management and backup services, operated from head office and the cloud. Customers' internal systems are out of scope; Harbourline's access to them and its agents running on them are in scope.

**Interested parties:** customers (some regulated), data protection authorities, the national CSIRT (managed service providers fall under NIS2), the certification body, management and investors.

## Modules

| # | Module | Task | Reference |
|---|--------|------|-----------|
| 0 | Company brief | Understand the business, scope and interested parties | Clause 4 |
| 1 | Risk assessment | Score eight risks on a 5×5 matrix | Clause 6.1.2 |
| 2 | Risk treatment | Select Annex A controls for the four highest risks, name a risk owner | Clause 6.1.3, Annex A |
| 3 | Statement of Applicability | Decide and justify applicability for ten controls | Clause 6.1.3 d) |
| 4 | Internal audit drill | Grade six pieces of audit evidence | Clause 9.2, Clause 10.2 |
| 5 | Breach drill | Order the response steps, identify controller and processor, calculate the deadline | A.5.24 to A.5.28, GDPR Art. 33, NIS2 Art. 23 |
| 6 | Management review | Select the required inputs, name the required outputs | Clause 9.3 |
| 7 | Key takeaways | One principle per module | |

## Risk methodology

**Risk score = Likelihood × Impact**, each rated 1 to 5.

| Score | Level | Treatment rule |
|-------|-------|----------------|
| 15 to 25 | High | Must be treated |
| 8 to 14 | Medium | Treat, or the risk owner formally accepts |
| 1 to 7 | Low | May be accepted |

Acceptance criteria are set **before** assessment so results are consistent, repeatable and comparable (Clause 6.1.2 a and c). Every risk has a named owner from the business, not the security team, who approves the treatment plan and accepts residual risk.

## Risk register summary

Model scores used in the lab:

| ID | Asset | Scenario | L | I | Score | Level |
|----|-------|----------|---|---|-------|-------|
| R1 | Remote management platform | Engineer account phished, attacker reaches all customers | 4 | 5 | 20 | High |
| R6 | Corporate IT | Ransomware stops SOC, support and billing | 3 | 5 | 15 | High |
| R3 | Customer portal | Credential stuffing takes over customer accounts | 4 | 3 | 12 | Medium |
| R4 | Backup storage | Misconfigured bucket exposes a customer's backups | 3 | 4 | 12 | Medium |
| R7 | Portal software | Critical vulnerability in an open source library | 3 | 4 | 12 | Medium |
| R2 | Agent update pipeline | Tampered update pushed to 4,000 servers | 2 | 5 | 10 | Medium |
| R5 | Shared logging platform | One customer sees another customer's logs | 2 | 5 | 10 | Medium |
| R8 | Source code repositories | Leaver keeps repository access | 3 | 3 | 9 | Medium |

Key treatments for the top risk (R1): phishing resistant MFA (A.8.5), just in time privileged access (A.8.2), full session logging (A.8.15), targeted awareness (A.6.3), and a contractual basis for remote access (A.5.20).

## Incident response model

The breach drill uses a leaked export of one customer's data from the shared logging platform.

1. Contain and preserve evidence
2. Open an incident and start a timeline
3. Assess scope and whether personal data is involved
4. Inform the Data Protection Officer and legal
5. Notify the customer (the **controller**) without undue delay, as the **processor** (GDPR Art. 33(2))
6. Support the customer's own 72 hour notification to its supervisory authority
7. Assess NIS2 reportability: a significant incident needs a 24 hour early warning to the CSIRT
8. Root cause analysis and corrective action (Clause 10.2), feeding lessons into the risk register

The 72 hour period runs in calendar time from awareness, including weekends.

## How to use

**In the browser:** open `index.html`. No build step, no installation. The only external resource is Google Fonts.

**Suggested approach:**
1. Read the company brief.
2. Answer each module before opening the model answer.
3. Record your answers and reasoning in [`my-answers.md`](my-answers.md), especially where you disagree with the model.

**Publish with GitHub Pages:** Settings → Pages → deploy from the `main` branch, root folder.

Progress is stored locally in the browser where permitted. No data leaves the page.

## Repository structure

```
iso27001-practice-lab/
├── index.html        The interactive lab (HTML, CSS and JavaScript in one file)
├── README.md         This documentation
└── my-answers.md     Worked answers and reasoning
```

## References

- ISO/IEC 27001:2022, Information security management systems, Requirements
- ISO/IEC 27002:2022, Information security controls
- Regulation (EU) 2016/679 (GDPR), Articles 28 and 33
- Directive (EU) 2022/2555 (NIS2), Articles 21 and 23

## Assumptions and limitations

- The company, systems, figures and scenarios are fictional and simplified for learning.
- Model answers reflect common practice. A real ISMS scores and decides against its own risk criteria, context and legal advice.
- The Statement of Applicability covers ten sample controls, not all 93 in Annex A.
- NIS2 obligations vary by member state transposition; the lab uses the directive's baseline.
- This is a study aid, not legal advice or a certification tool.

## How this was built

Built with AI assistance. I designed the learning goals, worked through every module, and recorded my own reasoning in `my-answers.md`.

## Author

**Jerry Brown**, information security professional
[LinkedIn](https://linkedin.com/in/brownjerry) · [GitHub](https://github.com/Brown-Jerry)
