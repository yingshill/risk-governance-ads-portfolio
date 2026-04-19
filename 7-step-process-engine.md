# 7-Step Process Engine
**The Operational Sequence — Detection through Postmortem**

> This engine fires every time a risk event hits, regardless of lifecycle stage.  
> It is a **reusable mechanism**, not a one-time checklist.

---

## Why a Process Engine, Not a Checklist

A checklist closes when the task is done. A process engine generates data that improves the next cycle.

The difference is the **postmortem → feedback loop**:

```
Each postmortem produces one or more of:
  · Policy update       → changes what counts as a violation or evidence
  · SOP revision        → changes how ops executes the decision
  · Model retrain signal → changes what the ML classifier catches next time
  · Training case       → calibrates reviewer judgment going forward
```

This is why governance improves over time instead of stagnating.

---

## The 7 Steps — Detail

### Step 1 — Detection 检测

**What happens:** A risk signal surfaces from one or more sources.

**Sources:**
- ML classifier score (primary for scale)
- Heuristic rules (spend velocity, login pattern, payment failure rate)
- Cross-account linkage engine (device fingerprint, payment hash, email hash)
- Payment system (chargeback alerts, credit limit breach)
- Internal referral (Ops team observation, Sales flag)
- External report (advertiser complaint, brand partner flag)

**Output:** Signal record with: source, type, confidence score, timestamp, raw data pointer

**Design note:** Detection quality determines everything downstream. A signal that doesn't surface = zero enforcement. This step deserves the most model investment.

---

### Step 2 — Triage 分诊

**What happens:** Signal is classified, prioritized, and routed.

**Classification dimensions:**
1. Risk type: ATO / Impersonation / Bad Debt / Circumvention / Fraudulent Content
2. Severity: P0 (active harm) / P1 (pattern risk) / P2 (low severity)
3. Account tier: LTV bracket, account age, managed vs. self-serve

**Routing output:**
- Correct queue assignment
- Correct reviewer tier (L1 / L2 / specialist)
- SLA clock started

**Common triage failures:**
- Misclassification between risk types → wrong evidence standard applied
- Severity underestimation → P0 treated as P1, harm continues
- Queue overflow → SLA breach → harm window extends

---

### Step 3 — Evidence Chain Assembly 证据链

**What happens:** All available signals are pulled, classified by tier, and assembled into a case file.

**Evidence tier framework:**
See [Actor Suspension Policy §2](../frameworks/actor-suspension-policy.md) for full tier definitions.

**Assembly protocol:**
1. Pull all Tier 1 signals first
2. If Tier 1 present → proceed to Decision
3. If no Tier 1 → pull Tier 2 signals; assess whether combination is sufficient
4. If only Tier 3 → flag for monitoring; do not escalate to enforcement without Tier 2 corroboration

**Linkage mapping:**
- Cross-account connections are the most common evidence for circumvention cases
- Linkage map must be reconstructable by an independent reviewer from raw data alone
- Do not rely on "reviewer memory" — all linkages must be documented

---

### Step 4 — Decision 研判

**What happens:** Evidence is weighed against policy; enforcement level is selected.

**Decision tree structure:**
```
Is Tier 1 evidence present?
  YES → Is this a first violation?
          YES → Level 3 (Restriction) minimum
          NO → Level 4 (Suspension) minimum
  NO  → Is Tier 2 evidence present with corroboration?
          YES → Is there prior violation history?
                  YES → Level 2 (Spend Cap)
                  NO → Level 1 (Warning)
          NO  → Level 0 (Monitor)
```

**Human override triggers:**
- Account LTV >$50K: mandatory L2 sign-off regardless of confidence
- Novel edge case: mandatory Policy team consultation before action
- Prior overturn on same account: mandatory L2 review

**Documentation requirement:** Decision rationale must be written in plain language sufficient for an appeal reviewer with zero prior context.

---

### Step 5 — Action 处置

**What happens:** Enforcement action is executed and advertiser is notified.

**Execution checklist:**
- [ ] Enforcement level matches decision (no silent downgrades)
- [ ] Advertiser notification sent (in-product + email) within 1 hour
- [ ] Notification includes: action taken, policy basis, appeal rights, SLA
- [ ] Case file locked (read-only until appeal trigger or postmortem)
- [ ] Action logged in enforcement system with case ID

**Common execution failures:**
- Notification not sent → advertiser discovers suspension via failed ad delivery
- Wrong enforcement level executed (system config error)
- Case file left editable → integrity risk for appeal review

---

### Step 6 — Appeal 申诉

**What happens:** Advertiser challenges the enforcement action; independent reviewer conducts fresh review.

**Independence requirement:** Appeal reviewer must not have access to original reviewer's rationale until after they have reached their own conclusion.

**Appeal outcomes and downstream routing:**

| Outcome | What It Means | Downstream Action |
|---|---|---|
| **Overturn** | Original evidence chain was insufficient | Restore account; log as false action; mandatory postmortem |
| **Modify** | Evidence supports lower level | Downgrade action; log as partial false action |
| **Uphold** | Evidence chain is valid | Confirm; close; no postmortem unless P0 |
| **Escalate** | Policy gap or novel edge case | Route to Policy team; hold action pending clarification |

**Appeal data is the most valuable governance signal.** Overturn rate by risk type, reviewer, and region tells you exactly where your policy, training, or model has gaps.

---

### Step 7 — Postmortem 复盘

**What happens:** Outcomes are analyzed and turned into durable governance upgrades.

**Triggers:**
- All P0 incidents (mandatory, within 72 hours)
- All false actions (mandatory, weekly batch)
- Any appeal overturn rate spike >2% in a 7-day window
- Novel edge case escalated from appeal

**Postmortem structure:**
```
1. What happened (timeline of events)
2. What the evidence chain contained (and what it was missing)
3. Root cause classification:
     · Policy gap — the policy didn't cover this case
     · Evidence gap — the signals existed but weren't collected/used
     · Model error — the classifier scored incorrectly
     · Reviewer error — evidence existed, policy was clear, reviewer misjudged
     · SOP gap — process didn't surface the right information at the right step
4. Durable fix (specific, owned, time-bound)
5. Verification metric — how will we know the fix worked?
```

**Durable fix routing:**
- Policy gap → Policy update (XFN review if threshold change)
- Evidence gap → SOP revision + ML feature request
- Model error → Retrain signal package to R&D
- Reviewer error → Calibration case added to training library
- SOP gap → SOP revision + reviewer communication

---

## The Feedback Loop — Why This Closes

```
Postmortem finding
      ↓
Root cause classified
      ↓
Durable fix issued
   ├── Policy update → tightens evidence standards or consequence tiers
   ├── SOP revision → improves how ops executes the decision
   ├── Model retrain → improves what the classifier catches next time
   └── Training case → improves reviewer calibration
      ↓
Next detection cycle runs against improved system
      ↓
Metrics tracked to verify fix worked
      ↓
Next postmortem reviews whether the fix held
```

**The loop is the product. Every incident is an investment in the next cycle.**

---

## Framework Mapping

| Industry Framework | How It Maps |
|---|---|
| **ITIL Incident Management** | Steps 1–7 are nearly 1:1. Key additions: explicit evidence chain step (Step 3) and feedback loop postmortem (Step 7) |
| **NIST CSF** | Detect (Step 1) → Respond (Steps 2–5) → Recover (Step 6) → Improve (Step 7) |
| **PDCA** | Plan (policy/SOP) → Do (Steps 1–5) → Check (Step 6 appeal data) → Act (Step 7 postmortem) |
| **Six Sigma DMAIC** | Postmortem IS a DMAIC cycle: Define (root cause) → Measure (metrics) → Analyze (slice) → Improve (fix) → Control (verify) |
