# Risk Governance Portfolio — Yingshi

> **Applying for:** Risk Governance Policy Specialist, TikTok Ads (Mandarin Speaking)  
> **Team:** Business Integrity → Governance → Actor Strategy  
> **Focus:** Advertiser/actor risk — ATO, impersonation, bad debt, policy circumvention

---

## What This Repo Is

A working portfolio that maps my governance experience directly to the four pillars of this role. Each folder contains frameworks, case playbooks, and decision standards I've designed and operated — adapted to TikTok's advertiser risk surface.

**This is not a resume supplement. It's a demonstration of how I think and work.**

---

## Role ↔ Experience Mapping

| JD Responsibility | My Experience | Folder |
|---|---|---|
| Own Actor Suspension policy framework | Designed Safety OS Unified Policy at Moody's — evidence chain standards across 100% of sanctions decisions | [`/frameworks`](/frameworks) |
| Build operationally actionable standards | Wrote tiered enforcement SOP at Flip — canary rollout gates, incident response, escalation paths | [`/frameworks`](/frameworks) |
| Edge case reviews → policy clarification | Found 15% of false positives traced to a single viral challenge via confusion matrix slice analysis | [`/cases`](/cases) |
| Calibration and enablement across reviewers | Built Safety Index System — 500-case blind audits tracking Precision/Recall/F1 by reviewer and region | [`/metrics`](/metrics) |

---

## Three-Layer Governance Model

Everything in this repo operates within this framework:

```
A — Actor Lifecycle        WHAT you govern
   Onboarding → Monitoring → Enforcement → Appeal

B — Ops Stack              HOW you govern  
   Policy · SOP Design · Process Health Metrics · Feedback Loops

C — 7-Step Process Engine  WHEN you govern
   Detection → Triage → Evidence Chain → Decision → Action → Appeal → Postmortem
```

> The feedback loop ties all three: every postmortem improves the policy → tightens the SOP → raises the bar for the next detection cycle.

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

> *"I don't just manage the process — I am the process. I write the standards, run the audits, investigate the failures, and turn every finding into a durable governance upgrade."*
>
> *我不只是管流程的人——我就是写标准、跑审计、查根因、把每个发现变成持久治理升级的那个人。*

---

*Portfolio maintained by Yingshi · April 2026*
