# Case Playbook — Policy Circumvention

**政策规避 · Risk Type 04 of 05**

> **Risk definition:** An actor intentionally evades enforcement — by creating new accounts after suspension, using referral chains or agency proxies to re-enter, cloaking ad content from reviewers, or structuring spend to stay below detection thresholds.

> ⚠️ **Note:** Thresholds, timing windows, and metric targets in this document are proposed values — need verified against production standards before use.

---

## Why Circumvention Is the Hardest Case

Circumvention is adversarial by definition. The actor **knows your detection logic and is designing around it**. This means:

1. Signal-based detection has a ceiling — a sophisticated actor will avoid every individual signal
2. The evidence must be **relational** (linkage-based), not just behavioral
3. Every policy clarification you publish also tells bad actors what to avoid
4. Edge cases are the primary attack surface — if policy is ambiguous, bad actors exploit the ambiguity

**Governance implication:** Circumvention cases are the most important input to policy hardening. Every successful circumvention is a policy gap that must be closed.

---

## Circumvention Pattern Taxonomy

### Pattern A — New Account Creation (最常见)

Suspended actor creates a new account using different registration details. Common evasion techniques:

- New email domain (but same email naming convention)
- New payment method (but same billing address)
- New device (but same IP range or ISP)
- New business name (but same landing page, phone number, or creative assets)

**Detection approach:** Cross-entity linkage engine — hash-match on device fingerprint, payment BIN, phone, address, creative asset

### Pattern B — Agency / Proxy Re-entry

Suspended actor routes ads through a compliant agency account. The agency may be witting or unwitting.

**Detection approach:** Campaign-level creative analysis + landing page fingerprint + spend pattern matching to prior suspended account

### Pattern C — Cloaking

Ad content shown to reviewers differs from content shown to users. Techniques:

- IP-based cloaking: show compliant content to reviewer IPs; show prohibited content to users
- Time-based cloaking: compliant content during review window; switched after approval
- User-agent cloaking: detect automated review crawlers; serve clean content

**Detection approach:** Dynamic content sampling from user-side IPs + post-serve review cadence + landing page snapshot comparison

### Pattern D — Threshold Structuring

Actor stays below detection thresholds on every individual signal — spend just below velocity flag, creates new campaigns before any single campaign accumulates violations.

**Detection approach:** Pattern-level analysis across campaigns, not just individual campaign metrics. Requires ML features that capture cross-campaign behavior.

---

## The Edge Case Problem — Policy Ambiguity as Attack Surface

**Illustrative example:**

> An advertiser's ad claims: _"Our app helped 10,000 users earn an extra $500/month."_
>
> Is this fraudulent ad content?

This is a genuine edge case. The policy says "misleading claims," but:

- The claim may be statistically true (10,000 users out of 1M who downloaded the app)
- "Helped earn" is ambiguous — does this mean guaranteed income?
- $500/month is not an extreme claim by gig economy standards

**Edge case resolution protocol:**

```
Step 1: Map the claim against existing policy language exactly as written
Step 2: Identify the specific ambiguity — what does the policy NOT say?
Step 3: Apply the "reasonable reviewer" test:
         Would a strong majority of trained reviewers agree this is a violation?
         If NO → it's a policy gap, not a reviewer error
Step 4: Escalate to Policy team for edge case review
Step 5: Policy team codifies the outcome:
         · If violation → add to prohibited examples with the specific reasoning
         · If not violation → add to permitted examples with guard rails
         · If context-dependent → create a decision tree for the condition
Step 6: Add the case to calibration library
Step 7: Publish policy clarification (internal + external if materially affects advertisers)
```

> The "reasonable reviewer" agreement threshold is a proposed value — need verified against calibration data.

**Key principle:** Never resolve an edge case without codifying the outcome. A decision that lives only in one reviewer's head is not governance — it's tribal knowledge.

---

## Evidence Chain Standard — Circumvention

Circumvention evidence must demonstrate **intentionality**, not just similarity. Similarity alone is not sufficient.

**Intentionality indicators:**

- Prior suspension on linked entity (establishes actor knew they were banned)
- Timing: new account created shortly after suspension
- Active evasion: deliberately changed linkage signals that were present in original account
- Pattern replication: campaign structure, creative approach, landing page are substantially identical

> Timing window for "shortly after suspension" is a proposed value — need verified against operational standards.

**Linkage evidence requirements:**

- At least TWO independent linkage signals (e.g., same device + same creative asset)
- OR one direct linkage signal + prior suspension on linked entity
- Linkage map must be reconstructable from raw data (no "reviewer recognized the style" without documentation)

---

## Decision Framework

```
Is there confirmed linkage to a previously suspended entity?
  YES → Is there evidence of intentional evasion (new details added post-suspension)?
          YES → Level 4 (Suspension) + entity block on linked accounts
          NO  → May be unwitting proxy — Level 3 (Restriction) + investigation
                 of the agency/referral chain
  NO  → Is there a strong pattern match without direct linkage?
          YES → Level 2 (Spend Cap) + enhanced monitoring + linkage investigation
          NO  → Level 0 (Monitor) with expanded linkage data collection
```

**Entity block protocol:** When circumvention is confirmed, all accounts sharing linkage signals are blocked simultaneously. Piecemeal enforcement allows the actor to shift operations to unblocked accounts.

---

## Policy Hardening — Turning Cases into Standards

Every confirmed circumvention case should generate at least one of:

1. **New linkage signal** added to the cross-entity detection model
2. **New prohibited pattern** added to the policy (with reasoning)
3. **New detection rule** added to the heuristic engine
4. **New calibration case** for reviewers handling similar patterns

**Tracking template:**

| Case ID | Circumvention Pattern                | Policy Gap Identified                     | Fix Type             | Status |
| ------- | ------------------------------------ | ----------------------------------------- | -------------------- | ------ |
| —       | New account via same creative assets | Creative fingerprint not in linkage scope | ML feature addition  | —      |
| —       | Agency proxy (unwitting)             | No policy on proxy liability              | Policy update needed | —      |

---

## Metrics — Circumvention Specific

| Metric                          | Definition                                                                   | Target                        |
| ------------------------------- | ---------------------------------------------------------------------------- | ----------------------------- |
| **Re-entry catch rate**         | % of suspended actors caught when attempting re-entry                        | Proposed: >90% within 30 days |
| **Time to re-detection**        | Days from suspension to catching re-entry attempt                            | Trending ↓ QoQ                |
| **Edge case codification rate** | % of escalated edge cases that result in policy update within defined window | Proposed: >95%                |
| **Cloaking detection rate**     | % of cloaking attempts caught via post-serve review                          | Tracked                       |

> Metric targets above are proposed values — need verified against operational benchmarks.

---

_See also: [ATO Playbook](ato-account-takeover.md) · [Fraudulent Ad Content Playbook](fraudulent-ad-content.md) · [Actor Suspension Policy §3](../frameworks/actor-suspension-policy.md)_
