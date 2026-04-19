# Quality Audit System — Safety Index
**Pillar 4 — Data-driven Risk Operations**

> **Purpose:** Provide an independent, auditable measure of enforcement quality — separate from system metrics, which can be gamed or masked by aggregate averaging.  
> **Cadence:** Monthly blind audit · Weekly false action review · Real-time dashboard  
> **Owner:** Policy team (independent from Ops team being measured)

---

## Why Blind Audits, Not Just System Metrics

System metrics (catch rate, action count) measure **what the system did**. They don't measure **whether it was right**.

A system can maintain a stable catch rate while quietly accumulating false actions — if the false actions are distributed across reviewer queues and regions, aggregate metrics won't surface them.

The Safety Index exists to find what aggregate metrics hide.

**Core principle: Measure the decision, not just the action.**

---

## 500-Case Blind Audit Protocol

### Sample Design

```
Monthly sample: 500 cases
  ├── 200 random sample (representative baseline)
  ├── 150 stratified by risk type
  │    ├── 50 ATO
  │    ├── 40 Circumvention (highest edge case density)
  │    ├── 30 Impersonation
  │    ├── 20 Bad Debt
  │    └── 10 Fraudulent Content
  ├── 100 recent overturns and appeals (where we know we were wrong)
  └── 50 edge case escalations (calibrate policy boundary decisions)
```

### Blind Review Procedure

1. Cases are stripped of original reviewer ID and rationale
2. Audit reviewer reads only: signal log, evidence chain, enforcement action taken
3. Audit reviewer records: correct action / incorrect action / policy ambiguous
4. Audit reviewer documents: what evidence was used, what evidence was missed, what should have happened
5. Discrepancies compiled by Policy team — NOT shared with Ops until analysis complete

### Output Metrics

| Metric | Formula | Calculation |
|---|---|---|
| **Precision** | True Positives / (TP + FP) | Of all enforcement actions, what % were correct? |
| **Recall** | True Positives / (TP + FN) | Of all actual violations, what % did we catch? |
| **F1 Score** | 2 × (P × R) / (P + R) | Harmonic mean — balanced quality measure |
| **False Action Rate** | FP / Total Actions | % of enforcement actions that were wrong |
| **Miss Rate** | FN / Total Violations | % of violations we failed to catch |

---

## Slice Analysis Protocol

**Aggregate metrics are not sufficient.** When a metric looks stable at the aggregate level, the problems are hiding in the slices.

**Standard slice dimensions:**

```
1. Risk Type        → ATO vs. Impersonation vs. Bad Debt vs. Circumvention vs. Ad Content
2. Reviewer         → Which reviewers have elevated false action rates?
3. Region           → CN-side vs. US-side vs. SEA advertiser accounts
4. Account Tier     → High LTV vs. mid vs. self-serve
5. Confidence Band  → HITL (<0.75) vs. HOTL (0.75–0.98) vs. HOOL (≥0.98)
6. Content Category → Which ad categories generate most false positives?
7. Time             → Day of week, time of day, post-holiday periods
```

**Investigation trigger:** Any single slice with false action rate >2× the aggregate baseline triggers an immediate investigation — do not wait for monthly report.

**Real example of what slicing finds:**

> Aggregate false action rate: 3.2% (acceptable)  
> Slice by content category → "gig economy / income claims": 18.4% false action rate  
> Root cause: policy language on income claims was ambiguous; reviewers were applying different standards  
> Fix: edge case decision tree published; calibration session held; false action rate → 4.1% within 30 days

---

## System Health Report — Monthly Template

```
SYSTEM HEALTH REPORT — [Month Year]
Risk Governance Operations · Business Integrity

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

EXECUTIVE SUMMARY
  Overall Precision:     [X]%   [↑↓ vs. last month]
  Overall Recall:        [X]%   [↑↓ vs. last month]
  False Action Rate:     [X]%   [↑↓ vs. last month]
  Appeal Overturn Rate:  [X]%   [↑↓ vs. last month]
  P0 Incidents:          [N]    [↑↓ vs. last month]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

RISK TYPE BREAKDOWN
  ┌─────────────────┬───────────┬──────────┬──────────────────┐
  │ Risk Type       │ Precision │ Recall   │ False Action Rate│
  ├─────────────────┼───────────┼──────────┼──────────────────┤
  │ ATO             │           │          │                  │
  │ Impersonation   │           │          │                  │
  │ Bad Debt        │           │          │                  │
  │ Circumvention   │           │          │                  │
  │ Ad Content      │           │          │                  │
  └─────────────────┴───────────┴──────────┴──────────────────┘

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

NOTABLE FINDINGS
  [1] [Specific gap identified + slice that surfaced it]
  [2] [Improvement from prior month's fix — did it work?]
  [3] [Emerging pattern requiring attention]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

DURABLE FIXES ISSUED THIS MONTH
  [Policy updates, SOP revisions, model retrain signals, training cases added]

OPEN ITEMS — CARRY FORWARD
  [Issues identified but not yet resolved; owner + deadline]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Calibration Session Design

**Frequency:** Weekly (30 min) — batch 20 cases  
**Participants:** Policy lead + 4–6 reviewers from Ops  
**Format:**
1. Each participant reviews case independently (10 min)
2. Record decision without discussion
3. Reveal decisions — discuss divergence only (not consensus cases)
4. If >30% disagreement on a case type → policy clarification issued within 5 business days

**Calibration health metric:** Agreement rate by case type. Target: >85% agreement on all standard case types. Sub-85% = policy gap.

---

## KPI Definitions

See [KPI Definitions](kpi-definitions.md) for full definitions and calculation methodology.

**Top 5 metrics for this role:**

| KPI | Why It Matters |
|---|---|
| **False action rate** | The cost of being wrong when we act — harms legitimate advertisers |
| **Appeal overturn rate** | Reveals where our evidence standards or policy is failing |
| **Catch rate (pre-serve)** | The cost of being wrong when we don't act — harm reaches users |
| **MTTR (incident → durable fix)** | How fast governance improves after failure |
| **Edge case codification rate** | Whether policy is keeping up with the actual risk surface |
