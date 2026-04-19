# Actor Suspension Policy Framework
**Pillar 1 — Risk Policy Architecture & Standards**

> **Scope:** Advertiser/actor-level enforcement on TikTok Ads  
> **Applies to:** Account Suspension Operations · Appeals · Governance Review  
> **Version control:** Major updates require XFN sign-off (Legal, Ops, ML); minor clarifications logged inline

---

## 1. Policy Scope & Actor Definition

**Covered actors:** Any entity accessing TikTok Ads Manager — self-serve advertisers, agency accounts, managed accounts, and Business Center operators.

**Out of scope:** Content-level violations (handled by Content Policy), merchant/seller violations (handled by Shop Integrity), organic creator violations (handled by Creator T&S).

**Actor risk taxonomy:**

| Risk Type | Definition | Primary Signal |
|---|---|---|
| **ATO — Account Takeover** | Unauthorized access to a legitimate advertiser account | Login anomaly + spend spike + new payment method |
| **Impersonation** | False identity claim — brand, agency, or individual | Entity mismatch vs. KYC records or public registry |
| **Bad Debt / Overspend** | Ad spend exceeds recoverable credit exposure | Payment failure + spend velocity + account age |
| **Policy Circumvention** | Intentional evasion of enforcement — new accounts, cloaking, referral chains | Multi-account linkage + prior violation history |
| **Fraudulent Ad Content** | Misleading claims, prohibited categories, deceptive landing pages | Pre/post-serve content flags + landing page mismatch |

---

## 2. Evidence Chain Standards

**Principle:** Every enforcement action must survive an independent audit. If the evidence chain cannot be reconstructed end-to-end, the action does not ship.

### Evidence Tiers

```
TIER 1 — Definitive (supports auto-action at ≥0.98 confidence)
  · Direct behavioral signal: login from known fraud IP, payment chargebacks ≥3
  · Verified identity mismatch: KYC document vs. account registration
  · Confirmed linkage to previously suspended entity (same device/payment/email hash)

TIER 2 — Corroborative (required to elevate Tier 3 to actionable)
  · Spend velocity anomaly: >3σ above 30-day baseline
  · Creative asset reuse from flagged account
  · Landing page flagged by pre-serve review

TIER 3 — Indicative (insufficient alone; requires Tier 1 or 2 corroboration)
  · Single behavioral anomaly without pattern
  · User report without platform-side verification
  · Industry-sector risk flag (high-risk vertical without account-level evidence)
```

### Evidence Documentation Requirements

For every enforcement action, the case file must contain:

1. **Signal log:** Timestamped list of all signals, tier classification, data source
2. **Linkage map:** Any cross-account or cross-entity connections identified
3. **Confidence score:** ML model output + human reviewer override (if applicable)
4. **Decision rationale:** Plain-language summary sufficient for appeal reviewer with no prior case context
5. **Reviewer ID + timestamp:** Who decided, when, under which policy version

---

## 3. Consequence Framework — Tiered Enforcement

**Design principle:** Consequences must be proportionate to evidence strength and actor history. Escalation paths are one-directional without new evidence.

```
LEVEL 0 — Monitor
  Trigger: Indicative signals only (Tier 3)
  Action: Flag for enhanced monitoring; no restriction on account
  Review cycle: 7 days

LEVEL 1 — Warning
  Trigger: First Tier 2 signal, no prior history
  Action: In-product notice; no spend restriction
  Appeal: Not required (no restriction imposed)

LEVEL 2 — Spend Cap / Creative Restriction
  Trigger: Tier 2 signal + prior Level 1, OR first Tier 1 signal (low severity)
  Action: Daily spend capped at $X; prohibited creatives paused
  Appeal window: 14 days

LEVEL 3 — Account Restriction
  Trigger: Tier 1 signal (moderate severity) OR Level 2 with continued violation
  Action: Ads paused; account read-only; payment methods frozen
  Appeal window: 30 days
  Human review: Required before action

LEVEL 4 — Account Suspension
  Trigger: Tier 1 signal (high severity) — ATO confirmed, impersonation confirmed, bad debt threshold breached
  Action: Full account suspension; ad serving halted; funds held
  Appeal window: 30 days
  Human review: Required; dual-reviewer sign-off for accounts >$50K LTV

LEVEL 5 — Permanent Ban + Entity Block
  Trigger: Level 4 + appeal upheld OR multi-account circumvention confirmed
  Action: Account + linked entities blocked; business registry flagged
  Appeal: Executive escalation only; 90-day cooling period
```

---

## 4. Appeal Rights & Standards

**Appeal eligibility:** All Level 2+ actions are appealable. Level 1 warnings are not.

**Review standard:** Appeal reviewer must assess whether the original evidence chain meets Tier 1/2 standards *without reference to the original reviewer's rationale*. Fresh review only.

**Outcome options:**

| Outcome | Condition | Action |
|---|---|---|
| **Overturn** | Evidence chain does not meet tier standard | Restore account; log as false action; feed to postmortem |
| **Modify** | Evidence supports lower-level consequence | Downgrade action; notify advertiser |
| **Uphold** | Evidence chain is valid | Confirm action; close appeal |
| **Escalate** | Novel edge case; policy ambiguity | Route to Policy team for edge case review within 5 business days |

**SLA:** Appeal decision within 5 business days (standard) / 2 business days (Level 4+).

---

## 5. Policy Version Control

| Version | Change Summary | Effective Date | Sign-off |
|---|---|---|---|
| v1.0 | Initial framework | — | — |
| — | *Updates logged here as policy evolves* | — | — |

**Change protocol:**
- **Minor clarifications** (no enforcement change): Policy owner updates inline, logs in changelog
- **Threshold changes** (enforcement behavior affected): XFN review — Legal, Ops Lead, ML — before publishing
- **New risk type added:** Full policy review cycle; pilot on 5% traffic before GA

---

## Related Documents

- [Tiered Enforcement SOP](tiered-enforcement-sop.md) — Operational execution of this policy
- [5 Risk Case Playbooks](../cases/) — Applied policy per risk type
- [Quality Audit System](../metrics/quality-audit-system.md) — How this policy is measured
