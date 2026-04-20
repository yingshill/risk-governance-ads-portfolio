# Case Playbook — Impersonation
**冒充欺诈 · Risk Type 02 of 05**

> **Risk definition:** An actor falsely claims to be a brand, agency, public figure, or another advertiser — to gain trust, access, or ad approval they would otherwise not receive.

---

## Impersonation Types

| Type | Description | Example |
|---|---|---|
| **Brand impersonation** | Fake account claiming to be a known brand | "Nike Official Store" run by unaffiliated seller |
| **Agency impersonation** | Claims to represent an agency to access managed accounts | Fake WPP/Dentsu affiliation to bypass KYC |
| **Advertiser impersonation** | Clones a legitimate advertiser's identity to run competing or fraudulent ads | Copy of a competitor's account with slight name variation |
| **Public figure impersonation** | Uses celebrity/influencer likeness without authorization | Fake Elon Musk crypto endorsement ad |

---

## Signal Taxonomy

**Tier 1:**
- Business registry mismatch: claimed brand name does not match registered entity
- Logo/trademark match to verified brand owner (different account)
- Verified brand owner files formal IP complaint

**Tier 2:**
- Domain mismatch: ad landing page domain ≠ official brand domain
- Account age <30 days with brand-name username
- Creative assets copied from verified brand's official account

**Tier 3:**
- User report of impersonation (triggers investigation, not action)
- High follower count inconsistent with account age

---

## Evidence Chain & Decision

**Minimum for action:** Tier 1 signal, OR Tier 2 signals from two independent sources.

**Decision:**
```
Verified brand owner has active account on platform?
  YES → Level 4 (Suspension) + notify verified owner
  NO  → Is evidence of deceptive intent present?
          YES → Level 3 (Restriction) + request identity verification
          NO  → Level 1 (Warning) + identity verification required to continue
```

**Key metric:** False action rate — impersonation is a case where legitimate new brand accounts can be incorrectly flagged. Verification-first before hard action.

---

## Metrics

| Metric | Target |
|---|---|
| Impersonation catch rate (pre-serve) | >80% caught before first ad impression |
| Time to verified owner notification | <4hr after action |
| False action rate on new brand accounts | <0.5% |

---
---

# Case Playbook — Bad Debt / Overspend
**坏账与超额消费 · Risk Type 03 of 05**

> **Risk definition:** An advertiser's ad spend exceeds their credit capacity, and payment cannot be recovered — whether through intentional fraud (spend then disappear) or operational failure (poor cash flow management).

---

## Why Bad Debt Requires a Different Lens

Unlike ATO or impersonation, bad debt often involves **no single moment of fraud**. An advertiser may legitimately ramp spend, then experience cash flow issues, then default. Or they may have always intended to defraud.

Governance must distinguish:
1. **Intentional bad debt fraud** (criminal; hard enforcement)
2. **Operational bad debt** (business failure; workout/recovery process, not suspension)

Treating type 2 as type 1 destroys legitimate advertiser relationships. Treating type 1 as type 2 creates moral hazard.

---

## Signal Taxonomy

**Tier 1 — High-confidence fraud indicators:**
- Prior bad debt on linked entity
- Spend surge immediately after credit limit increase (pattern: max credit, disappear)
- Payment method added with stolen card indicators (BIN mismatch, AVS failure)
- Account created, maximum credit consumed within 7 days, payment fails

**Tier 2 — Risk indicators:**
- Payment failure rate >2 in rolling 30 days
- Spend velocity increasing while payment reliability decreasing
- Account age <90 days + spend >$10K + first payment missed

**Tier 3 — Monitoring signals:**
- First-ever payment failure (common; not actionable alone)
- Spend growth >50% MoM (healthy growth is normal; monitor for payment follow-through)

---

## Credit Risk Scoring Model

```
Risk Score = f(
  account_age,
  payment_history_score,       # 0-1; based on on-time payment rate
  spend_velocity_z_score,      # standard deviations above 30d baseline
  credit_utilization_rate,     # current_spend / credit_limit
  linked_entity_risk_flag,     # binary; prior bad debt on linked account
  industry_risk_tier           # 0-2; based on historical bad debt rates by vertical
)

Thresholds:
  Score >0.85 → Proactive credit cap + payment verification required
  Score >0.95 → Spend pause + account review
  Score >0.98 → Immediate spend suspension; refer to Finance for recovery
```

---

## Decision Framework

```
Is this intentional fraud (Tier 1 signals present)?
  YES → Level 4 (Suspension) + Finance referral for recovery + entity block
  NO  → Is this operational failure (Tier 2, no fraud indicators)?
          Engage account team for workout:
            · Payment plan negotiation
            · Temporary spend cap until payment current
            · Credit limit reduction going forward
          If workout fails → Level 3 → Level 4 escalation
```

---

## Metrics

| Metric | Target |
|---|---|
| Bad debt $ exposure (rolling 30d) | Trending ↓ QoQ |
| Proactive catch rate (before default) | >70% of bad debt events flagged before payment failure |
| False action rate on legitimate advertisers | <1% |
| Recovery rate on referred bad debt | Tracked with Finance |

---
---

# Case Playbook — Fraudulent Ad Content
**虚假广告内容 · Risk Type 05 of 05**

> **Risk definition:** Ad creative or landing page contains false, misleading, or prohibited claims — including fake income guarantees, counterfeit products, health misinformation, and deceptive pricing.

---

## Why This Is Uniquely Complex

Fraudulent ad content sits at the intersection of:
- **Policy** (what claims are prohibited)
- **Context** (the same claim may be acceptable in one vertical, prohibited in another)
- **Intent** (is the advertiser deceiving, or just overstating?)
- **Regulation** (FTC guidelines, DSA, local consumer protection law)

The edge case density is higher than any other risk type. Policy must be specific enough to be actionable, but not so specific that bad actors simply rephrase their claims.

---

## Prohibited Content Categories

| Category | Example | Pre/Post-Serve |
|---|---|---|
| Guaranteed income claims | "Earn $1,000/day, guaranteed" | Pre-serve block |
| Health misinformation | "Cures diabetes in 30 days" | Pre-serve block |
| Counterfeit/IP infringement | Fake luxury goods | Pre-serve block |
| Phishing / credential harvest | Fake login pages | Pre-serve block |
| Prohibited financial products | Unlicensed crypto trading | Pre-serve block |
| Misleading pricing | "$5 item" with mandatory $99 subscription | Post-serve flag |
| Deceptive testimonials | Fabricated reviews/endorsements | Post-serve flag |

---

## The Edge Case Decision Tree — Income Claims

This is the most common ambiguous category:

```
Does the ad make an income claim?
  YES → Is the claim framed as guaranteed?
          YES → PROHIBITED (pre-serve block)
          NO  → Is the claim specific and verifiable?
                  YES → Is verification documentation provided?
                          YES → PERMITTED (with documentation on file)
                          NO  → WARNING (request substantiation within 5 days)
                  NO  → Is the claim a reasonable "up to" framing?
                          YES → PERMITTED (monitor for pattern abuse)
                          NO  → ESCALATE to Policy for edge case review
```

---

## Pre-Serve vs. Post-Serve Review

**Pre-serve (before ad runs):**
- Automated classifier screens creative + landing page
- High-confidence prohibited content → block immediately
- Medium confidence → human review queue (24hr SLA)
- Catch rate target: >95% of prohibited content blocked before first impression

**Post-serve (after ad is running):**
- Sampling-based review of live campaigns
- User reports trigger expedited review
- Priority: high-reach campaigns (>100K impressions) reviewed first
- Detection → pause ad within 2hr of confirmed violation

---

## Metrics

| Metric | Target |
|---|---|
| Pre-serve catch rate | >95% of prohibited content blocked before impression |
| Post-serve detection window | <2hr from confirmation to pause |
| False block rate | <1% of legitimate ads blocked pre-serve |
| Edge case codification rate | >95% of escalated cases → policy update within 14 days |

---

*See also: [Policy Circumvention Playbook](policy-circumvention.md) — cloaking often used to evade ad content review*
