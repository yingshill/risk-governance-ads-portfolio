# Risk Governance Portfolio

> _"I don't just manage the process — I am the process. I write the standards, run the audits, investigate the failures, and turn every finding into a durable governance upgrade."_
>
> _我不只是管流程的人——我就是写标准、跑审计、查根因、把每个发现变成持久治理升级的那个人。_

![Status](https://img.shields.io/badge/status-active_build-2ea44f)
![Files](https://img.shields.io/badge/files-14_documents-0075ca)
![Updated](https://img.shields.io/badge/updated-April_2026-lightgrey)
![Language](https://img.shields.io/badge/language-EN_%7C_%E4%B8%AD%E6%96%87-red)

>

---

## What This Repo Is

A working governance portfolio — not a resume supplement. Every document in this repo demonstrates how governance work gets designed and operationalized — policy frameworks, enforcement SOPs, case playbooks, audit methodology, and KPI definitions.

The content maps directly to the four pillars of the Risk Governance Policy Specialist role at TikTok Business Integrity — translated to the advertiser risk surface: ATO, impersonation, bad debt, policy circumvention, and fraudulent ad content.

---

## JD → Experience Mapping

| JD Responsibility                                                                                         | Approach                                                                                                                     | Where                        |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| Own the Actor Suspension policy framework — scope, definitions, enforcement criteria                      | Evidence chain standards governing sanctions decisions, designed to survive regulatory audit                                 | [`/frameworks`](frameworks/) |
| Build operationally actionable standards — evidence requirements, decision guidelines, write-up standards | Tiered enforcement SOP: HITL→HOOL routing, canary-to-GA rollout gates, P0 incident response                                  | [`/frameworks`](frameworks/) |
| Edge case reviews → codify into policy clarifications and decision trees                                  | Confusion matrix slice analysis surfacing hidden false positive clusters; packaged into policy exception + retraining signal | [`/cases`](cases/)           |
| Calibration and enablement to reduce inconsistency across reviewers and regions                           | 500-case blind audits tracking Precision/Recall/F1 by reviewer, region, and content category                                 | [`/metrics`](metrics/)       |

---

## Governance Model

Everything in this repo operates within a three-layer framework. Understanding how the layers connect is prerequisite to reading any individual document.

┌─────────────────────────────────────────────────────────────────┐
│ A — ACTOR LIFECYCLE WHAT you govern │
│ Onboarding → Monitoring → Enforcement → Appeal │
├─────────────────────────────────────────────────────────────────┤
│ B — OPS STACK HOW you govern │
│ Policy · SOP Design · Process Health Metrics · Feedback │
├─────────────────────────────────────────────────────────────────┤
│ C — 7-STEP PROCESS ENGINE WHEN you govern │
│ Detection → Triage → Evidence Chain → Decision → │
│ Action → Appeal → Postmortem │
└─────────────────────────────────────────────────────────────────┘

**How they connect:**

- Layer A defines the lifecycle stages that trigger Layer C process instances
- Layer B (ops stack) powers every step of Layer C
- The **feedback loop** ties all three: every postmortem → policy update → SOP revision → raises the bar for the next detection cycle

> See [`docs/governance-frameworks-map.md`](docs/governance-frameworks-map.md) for how this maps to Three Lines Model, NIST AI RMF, PDCA, DMAIC, and ITIL.

---

## Repo Structure

```
/
├── README.md                          ← You are here
│
├── frameworks/
│   ├── actor-suspension-policy.md    ← Evidence standards, consequence tiers, appeal rights
│   ├── tiered-enforcement-sop.md     ← HITL → HOTL → HOOL confidence thresholds
│   └── 7-step-process-engine.md      ← Operational sequence: detection → postmortem
│
├── cases/
│   ├── ato-account-takeover.md       ← Account hijack: signals, evidence chain, playbook
│   ├── impersonation.md              ← Brand/identity fraud: detection, tiers, SOP
│   ├── bad-debt-overspend.md         ← Credit risk: scoring model, enforcement gates
│   ├── policy-circumvention.md       ← Evasion patterns: edge case taxonomy, decision tree
│   └── fraudulent-ad-content.md      ← Misleading ads: pre/post-serve review standards
│
├── metrics/
│   ├── quality-audit-system.md       ← Safety Index: 500-case blind audit methodology
│   ├── kpi-definitions.md            ← Catch rate, false action rate, MTTR, appeal overturn
│   └── system-health-report.md       ← Monthly reporting template + slice analysis protocol
│
└── docs/
    ├── governance-frameworks-map.md  ← Three Lines, NIST AI RMF, PDCA, ITIL — mapped to role
    └── mandarin-glossary.md          ← 广告主诚信与行为治理术语表 (bilingual)
```

---

## Quick Links

- [Actor Suspension Policy Framework](frameworks/actor-suspension-policy.md)
- [5 Risk Case Playbooks](cases/)
- [Quality Audit & Metrics System](metrics/quality-audit-system.md)
- [Governance Frameworks Map](docs/governance-frameworks-map.md)
- [Bilingual Glossary 双语术语表](docs/mandarin-glossary.md)

---

## Core Governance Philosophy

> _"I don't just manage the process — I am the process. I write the standards, run the audits, investigate the failures, and turn every finding into a durable governance upgrade."_
>
> _我不只是管流程的人——我就是写标准、跑审计、查根因、把每个发现变成持久治理升级的那个人。_

---

_April 2026 · [ROADMAP](ROADMAP.md) · [Methodology](CONTRIBUTING.md)_
