# Governance Frameworks Map
**How industry standards map to this role**

> This document exists for one reason: governance credibility requires a common language.  
> When a regulator, auditor, or senior leader asks "what framework are you operating under?" — you have an answer.

---

## Role Position — Three Lines Model

```
1st Line — OPERATIONS (Account Suspension Ops, Appeals)
  · Owns the risk day-to-day
  · Executes SOPs written by 2nd line
  · Reports quality metrics to 2nd line

2nd Line — GOVERNANCE/POLICY ← THIS ROLE
  · Defines the standards that 1st line executes against
  · Designs the measurement system that evaluates 1st line quality
  · Issues policy clarifications and SOP updates
  · Investigates failures and issues durable fixes

3rd Line — INTERNAL AUDIT
  · Independently validates that 2nd line standards are working
  · Reviews 2nd line's audit methodology for independence
  · Reports to leadership / board
```

**Interview soundbite:** *"I see this role on the second line of defense. I define the policy standards and evidence chain requirements that the first-line ops team executes against, and I make sure our governance is defensible when the third-line audit comes."*

---

## AI Governance — NIST AI RMF

**Relevance:** Governs TikTok's automated enforcement classifiers and any LLM/Agent-based investigation tools.

```
GOVERN → Define policy boundaries for what automated enforcement can and cannot do
          · HOOL threshold: ≥0.98 confidence only
          · Prohibited actions: permanent ban requires human sign-off always
          · Audit trail requirements for every automated action

MAP    → Identify the risk surface
          · Where does the ML model have lowest confidence? (→ these are your HITL zones)
          · What actor types / content categories are underrepresented in training data?
          · Where does model drift typically appear first?

MEASURE → Track quality of automated decisions
          · Precision/Recall by confidence band
          · False action rate for HOOL actions (should be lowest of all tiers)
          · Concept drift monitoring: catch rate degrading on new ad formats?

MANAGE  → Act on measurement findings
          · Rollback triggers: if FAR on HOOL actions spikes >1%, reduce threshold
          · Retrain signals: package false action cases as labeled training data
          · Policy update: if automated decisions are systematically wrong on a category,
            move that category to HOTL or HITL until model improves
```

**LLM/Agent governance additions:**
- All LLM-generated evidence drafts must be verified by human reviewer before entering case file
- LLM must have explicit fallback: if confidence on a claim is low, flag for human rather than assert
- Hallucination rate is a tracked metric; zero-hallucination tolerance for evidence that will support enforcement action

---

## Operational Excellence — PDCA

**Relevance:** The postmortem → improvement cycle.

```
PLAN  → Policy update or SOP revision issued after postmortem finding
DO    → Canary deployment (1% traffic) of the change
CHECK → Safety Index measurement: did FAR/catch rate improve?
ACT   → GA the change (if pass) or iterate (if fail)
        → Start next PLAN cycle with new postmortem findings
```

**Key insight:** This is not a one-time cycle. It fires every time there's a postmortem — which is every P0 incident and every false action batch. The system improves continuously because the cycle never stops.

---

## Incident Management — ITIL Mapping

```
ITIL Step              → Your 7-Step Process
Detection              → Step 1: Detection
Logging                → (embedded in Step 2 Triage — case created with metadata)
Categorization         → Step 2: Risk type classification
Prioritization         → Step 2: P0/P1/P2 assignment
Investigation          → Step 3: Evidence Chain Assembly
Resolution             → Step 4+5: Decision + Action
Closure                → Step 6+7: Appeal + Postmortem
```

**What you add that ITIL doesn't have:**
1. Explicit evidence chain standard (Step 3) — every resolution must be audit-defensible
2. Postmortem feeds back into the system (Step 7) — ITIL "closes the ticket"; you close the ticket AND upgrade the system

---

## Quality — Six Sigma DMAIC

**Relevance:** Investigation methodology when a metric degrades.

```
DEFINE  → "Our false action rate on income claim ads spiked +5% this month"
           → Scope: which risk type, which region, which reviewer tier

MEASURE → Run 500-case blind audit slice on income claim category
           → Measure Precision, Recall, FAR for this segment specifically
           → Establish baseline for comparison

ANALYZE → Build confusion matrix for this category
           → Slice by reviewer, confidence band, content sub-type
           → Find: "18% FAR on gig economy income claims"
           → Root cause: policy language on "guaranteed" claims was ambiguous

IMPROVE → Publish edge case decision tree for income claims
           → Hold calibration session with reviewers
           → Add 20 cases to training library

CONTROL → Track FAR on income claim category weekly for 60 days
           → If FAR returns to baseline: close
           → If FAR drifts again: DMAIC restarts (policy may need further refinement)
```

---

## Regulatory Framework Alignment

| Regulation | Relevance | Governance Implication |
|---|---|---|
| **DSA (EU Digital Services Act)** | Requires transparency in ad targeting and enforcement decisions | Appeal rights, decision rationale, audit trails must meet DSA standard |
| **FTC Guides** | Endorsement and testimonial standards; income claim substantiation | Fraudulent ad content policy must incorporate FTC substantiation requirements |
| **USDS Data Rules** | Post-Jan 2026 ownership: data handling requirements for US user data | Enforcement evidence chain must comply with USDS data access rules |
| **CCPA / State Privacy Laws** | Advertiser data used in enforcement subject to privacy requirements | Evidence retention and access controls |

---

## Framework Summary — Quick Reference

| Framework | What It Is | Your Application |
|---|---|---|
| **Three Lines Model** | Risk governance accountability structure | You = 2nd line |
| **ISO 31000** | International risk management standard | Identifies your risk lifecycle |
| **NIST AI RMF** | AI risk governance: Govern → Map → Measure → Manage | Governs your automated enforcement |
| **NIST CSF** | Cybersecurity: Detect → Respond → Recover | Maps to your 7-step process |
| **EU AI Act** | AI risk tiers | Your classifiers = High Risk tier |
| **HITL/HOTL/HOOL** | Human oversight gradient | Your confidence threshold design |
| **Three Lines** | Defense lines | 2nd line = your role |
| **PDCA** | Improvement cycle | Your postmortem → fix cycle |
| **DMAIC** | Quality investigation | Your slice analysis protocol |
| **ITIL** | Incident management | Your 7-step process |
