# Tiered Enforcement SOP

> **Purpose:** Operationalize the Actor Suspension Policy into a repeatable, auditable enforcement workflow  
> **Audience:** Account Suspension Operations · Appeals · ML/Product (for system design)  
> **Human oversight model:** HITL → HOTL → HOOL gradient based on ML confidence score

> ⚠️ **Note:** Confidence thresholds, SLAs, and numerical values in this document are proposed values — need verified against production standards before use.

---

## Confidence-Based Routing

The single most important design decision in automated enforcement: **who decides, based on how certain the system is.**

```
ML Confidence Score    Routing               Human Role
─────────────────────────────────────────────────────────────
< 0.75                 HITL                  Human decides; ML provides evidence draft
                       Human-in-the-Loop     Reviewer reads all signals, makes judgment

0.75 – 0.98            HOTL                  System recommends; human approves/overrides
                       Human-on-the-Loop     5-minute SLA to review; default = approve

≥ 0.98                 HOOL                  System acts autonomously
                       Human-out-of-the-Loop Audit trail logged; human reviews in batch
```

**Design rationale:**

- Below 0.75: Model uncertainty is too high. False action cost (legitimate advertiser suspended) exceeds automation efficiency gain.
- 0.75–0.98: Model is directionally right but edge cases exist. Human checkpoint catches the long tail.
- Above 0.98: Model confidence is high enough that automation is warranted; batch audit provides assurance. Exact false action rate at this threshold requires empirical validation.

**Override protocol:** Any HOTL reviewer may override the system recommendation. Override reason must be logged and reviewed in weekly calibration.

---

## 7-Step Process Engine

```
Step 1 — DETECTION
  Source: ML classifier output · Heuristic rules · User reports · Payment system flags
  Output: Risk signal logged with confidence score, signal type, timestamp
  SLA: Real-time (automated) / 4hr (manual report triage)

Step 2 — TRIAGE
  Who: Ops team (L1 reviewer)
  Action: Classify risk type (ATO / Impersonation / Bad Debt / Circumvention / Ad Content)
          Assign severity tier (P0 / P1 / P2)
          Route to correct queue
  SLA: 2hr (P0) / 8hr (P1) / 24hr (P2)

  Priority matrix:
    P0 — Active fraud: live spend fraud, confirmed ATO, active impersonation
    P1 — Pattern risk: circumvention signals, spend anomaly without confirmation
    P2 — Low severity: single indicative signal, no active harm

Step 3 — EVIDENCE CHAIN ASSEMBLY
  Who: L1 reviewer (HITL/HOTL) or automated system (HOOL)
  Action: Pull all Tier 1/2/3 signals per evidence standard
          Build linkage map (cross-account, device, payment)
          Log confidence score + signal sources
  Output: Structured case file (see Policy Framework §2)

Step 4 — DECISION
  Who: L1 reviewer (HITL) · L1 with system recommendation (HOTL) · Automated (HOOL)
  Action: Apply consequence framework to evidence tier
          L2+ decisions require dual-reviewer sign-off for accounts >$50K LTV
  Output: Enforcement level selected + rationale documented

Step 5 — ACTION
  Who: System (automated) + Ops confirmation
  Action: Execute enforcement action (cap / restrict / suspend / ban)
          Notify advertiser via in-product + email
          Lock case file (no edits without appeal trigger)

Step 6 — APPEAL
  Who: Appeal team (independent from original reviewer)
  Action: Fresh evidence review — no reference to original rationale
          Decide: Overturn / Modify / Uphold / Escalate
          Log outcome as true positive, false positive, or edge case

Step 7 — POSTMORTEM
  Who: Policy team (weekly batch) · Incident-triggered (P0 events)
  Action: Analyze overturns and false actions
          Identify root cause (evidence gap / policy ambiguity / model error)
          Issue: Policy update · SOP revision · Model retrain signal · Training case
```

> SLAs, reviewer tiers, and LTV thresholds above are proposed values — need verified against operational capacity and team structure.

---

## Rollout Gates — Canary to GA

Any enforcement policy change or confidence threshold adjustment follows this staged deployment:

```
Stage 1 — Canary (1% traffic)
  Duration: 5 business days
  Monitor: False action rate · Appeal overturn rate · Catch rate
  Pass criteria: No metric degrades >1% vs. baseline
  Fail action: Immediate rollback; RCA before rescheduling

Stage 2 — Limited Rollout (10% traffic)
  Duration: 10 business days
  Monitor: Same as Stage 1 + queue volume impact on Ops
  Pass criteria: All metrics within ±2% of baseline
  Fail action: Rollback to Stage 1 or hold pending investigation

Stage 3 — GA (100% traffic)
  Requires: Stage 1 + Stage 2 both passed
  Monitoring: First 30 days at daily cadence; then weekly
```

> Traffic percentages, durations, and pass criteria above are proposed values — need verified against platform scale and ops capacity.

---

## Incident Response — P0 Protocol

For active fraud events (confirmed ATO, coordinated circumvention campaigns):

```
T+0     Detection signal flagged as P0
T+30m   Ops lead notified; initial triage complete
T+2hr   Contain: restrict affected accounts pending full investigation
T+4hr   Evidence chain assembled; enforcement action executed
T+24hr  Advertiser notified with appeal rights
T+72hr  Postmortem draft circulated to Policy + ML + Ops
T+5d    Durable fix identified: policy update / model retrain / SOP revision
T+10d   Fix deployed through canary gate
```

**Communication protocol:**

- Internal: Ops lead → Policy lead → Business Integrity VP (P0 only)
- External (advertiser): Standard suspension notice + dedicated appeals contact for P0 cases
- Regulatory: Legal notified within 24hr if regulatory exposure identified

> P0 timeline (T+30m through T+10d) and communication protocol above are proposed values — need verified against actual incident response capacity and legal requirements.

---

## Calibration & Reviewer Alignment

**Weekly calibration session:**

- Sample: 20 cases per session — mix of overturns, edge cases, and random sample
- Format: Blind review → compare decisions → discuss divergence
- Output: Policy clarification logged if >30% reviewer disagreement on a case type

**Monthly System Health Report inputs:**

- False action rate by risk type, reviewer, region
- Appeal overturn rate by enforcement level
- HITL/HOTL/HOOL distribution (automation coverage trend)
- P0 incident count and MTTR

> Sample size and disagreement threshold above are proposed values — need verified against team size and operational cadence.

---

## Related Documents

- [Actor Suspension Policy](actor-suspension-policy.md) — The rules this SOP executes
- [7-Step Process Engine (detail)](7-step-process-engine.md) — Deeper process documentation
- [Quality Audit System](../metrics/quality-audit-system.md) — How SOP compliance is measured
