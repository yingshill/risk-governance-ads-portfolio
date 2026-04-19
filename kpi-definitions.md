# KPI Definitions
**Risk Governance Operations — Measurement Standard**

> All metrics must have: a precise definition, a calculation method, a data source, and an owner.  
> Ambiguous metrics are not metrics — they're opinions.

---

## Enforcement Quality Metrics

### False Action Rate (FAR)
**Definition:** The percentage of enforcement actions taken against accounts that were not actually in violation — i.e., legitimate advertisers incorrectly actioned.  
**Formula:** `FAR = False Positives / Total Actions Taken`  
**Data source:** Appeal overturn outcomes + blind audit findings  
**Owner:** Policy team  
**Target:** <2% overall; <1% for Level 4 (Suspension) and above  
**Alert threshold:** Any 7-day window where FAR exceeds 2× rolling 30-day average  

---

### Catch Rate (Recall)
**Definition:** The percentage of actual violations that were detected and actioned.  
**Formula:** `Catch Rate = True Positives / (True Positives + False Negatives)`  
**Note:** False Negatives are estimated via: (a) post-hoc detection of previously missed cases, (b) appeal cases where advertiser self-reports prior undiscovered violations, (c) external reports  
**Data source:** Enforcement system + blind audit  
**Owner:** Policy team + ML team (joint)  
**Target:** >95% pre-serve for prohibited content; >90% for actor-level fraud within 30 days of first signal  

---

### Appeal Overturn Rate
**Definition:** The percentage of appealed enforcement actions that are overturned (reversed) by the appeal reviewer.  
**Formula:** `Overturn Rate = Overturned Appeals / Total Completed Appeals`  
**Interpretation:** High overturn rate = evidence chain or policy application failures. High uphold rate with low appeal volume = may indicate advertiser distrust of appeal process.  
**Data source:** Appeal management system  
**Owner:** Appeals team + Policy team (joint accountability)  
**Target:** <8% overall; any risk type >15% triggers immediate investigation  
**Segmentation required:** By risk type, reviewer, region, enforcement level  

---

### Precision
**Definition:** Of all enforcement actions taken, the percentage that were correct.  
**Formula:** `Precision = True Positives / (True Positives + False Positives)`  
**Data source:** Blind audit (ground truth determination)  
**Target:** >97%  

---

### F1 Score
**Definition:** Harmonic mean of Precision and Recall — the balanced quality measure.  
**Formula:** `F1 = 2 × (Precision × Recall) / (Precision + Recall)`  
**Use:** Primary single metric for overall enforcement quality. Penalizes imbalanced systems that sacrifice one for the other.  
**Target:** >0.95  

---

## Operational Metrics

### Mean Time to Resolution (MTTR) — Incident
**Definition:** Average time from a P0 incident detection to a durable governance fix being deployed.  
**Formula:** `MTTR = Σ(fix_deployment_time - detection_time) / P0_incident_count`  
**Durable fix defined as:** Policy update, SOP revision, or model retrain signal deployed through canary gate  
**Target:** <10 business days for P0 incidents  
**Owner:** Policy team (owns the fix; not Ops team which owns the response)  

---

### SLA Compliance Rate
**Definition:** Percentage of cases resolved within the defined SLA for their priority tier.  
**Formula:** `SLA Compliance = Cases Resolved Within SLA / Total Cases`  
**SLA definitions:**
  - P0: 2hr triage, 4hr action
  - P1: 8hr triage, 24hr action
  - P2: 24hr triage, 72hr action
  - Appeals: 5 business days standard, 2 business days Level 4+  
**Target:** >95% compliance across all tiers  

---

### Automation Coverage Rate
**Definition:** Percentage of total enforcement actions executed by the automated system (HOOL) vs. requiring human review.  
**Formula:** `Automation Rate = HOOL Actions / Total Actions`  
**Target:** Increase QoQ while false action rate holds — do not trade quality for coverage  
**Note:** Automation rate is not a quality metric. It's an efficiency metric. Never optimize automation rate at the expense of FAR.  

---

### Edge Case Codification Rate
**Definition:** Percentage of escalated edge cases that result in a published policy clarification within 14 business days.  
**Formula:** `Codification Rate = Codified Edge Cases / Total Edge Case Escalations`  
**Target:** >95%  
**Owner:** Policy team  
**Why it matters:** Uncodified edge cases become inconsistency. Inconsistency is what bad actors exploit.  

---

## Financial / Risk Exposure Metrics

### Bad Debt Exposure (Rolling 30d)
**Definition:** Total outstanding ad spend from accounts in active bad debt status or at high risk of default.  
**Owner:** Finance + Risk Governance (joint)  
**Target:** Trending ↓ QoQ as early detection improves  

### Proactive Catch Rate — Bad Debt
**Definition:** Percentage of bad debt events where the account was flagged before the first payment failure.  
**Formula:** `Proactive Rate = Accounts Flagged Pre-Default / Total Default Events`  
**Target:** >70%  

---

## Metric Governance

**Review cadence:**
- Real-time: False action rate, SLA compliance (dashboard)
- Weekly: FAR slice analysis, appeal overturn by reviewer/region
- Monthly: Full Safety Index report — all metrics, all slices

**Metric change protocol:** Any change to metric definitions, formulas, or targets requires Policy lead sign-off and must be logged in this document with effective date.

| Metric | Last Updated | Change | Owner |
|---|---|---|---|
| All definitions above | April 2026 | Initial version | Policy team |
