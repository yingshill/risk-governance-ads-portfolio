# Case Playbook — ATO (Account Takeover)

**账号被盗 · Risk Type 01 of 05**

> **Risk definition:** An unauthorized third party gains control of a legitimate advertiser account and uses it to run fraudulent ad spend — often draining credit lines, running prohibited content, or harvesting payment credentials.

> ⚠️ **Note:** Signal thresholds, SLAs, and metric targets in this document are proposed values — need verified against production standards before use. Mandarin communication templates require native speaker review.

---

## Why ATO Is Distinct

ATO is the only risk type where the **victim and the violator are the same account**. This creates two simultaneous obligations:

1. **Stop the harm** — pause fraudulent spend immediately
2. **Protect the legitimate advertiser** — ensure the actual account owner is not punished for the attacker's actions

Every ATO playbook must hold both obligations at once. Failing the second is a false action against a victim.

---

## Signal Taxonomy

### Tier 1 — Definitive ATO Signals

- Login from IP flagged in threat intelligence DB (known fraud infrastructure)
- Login country mismatch: account registered in US, login from high-risk jurisdiction not in account history
- New payment method added + spend surge within same session
- Chargeback filed by card issuer on recent ad spend
- MFA challenge failed repeatedly → succeeded (brute force or credential stuffing indicator)

### Tier 2 — Corroborative Signals

- Spend velocity anomaly above 30-day baseline
- New campaign created with prohibited ad content (crypto scam, fake tech support)
- Login device fingerprint not in account history
- Ad creative reused from known fraud campaign

> Specific velocity thresholds (e.g. standard deviation multiples) are proposed values — need verified against platform data distributions.

### Tier 3 — Indicative (insufficient alone)

- Single login from new location (travel is common; not actionable alone)
- Spend increase without device or payment anomaly
- Advertiser self-report without platform-side verification (triggers investigation, not action)

---

## Evidence Chain Standard

**Minimum for enforcement action:**

- At least ONE Tier 1 signal, OR
- TWO Tier 2 signals from independent sources (e.g., spend velocity + new device)

**Required case file elements:**

1. Timeline of anomalous events (login, payment change, spend spike, campaign creation)
2. IP/device fingerprint data with threat intelligence cross-reference
3. Comparison of pre-ATO vs. post-ATO campaign content
4. Payment record: when new method was added, first charge timestamp
5. ML confidence score + feature contribution breakdown where available

---

## Decision Framework

```
Confirmed Tier 1 signal present?
  YES → Is account owner contactable?
          YES → Immediate restriction (Level 3) + urgent owner notification
                 Account owner verifies identity → restore + help with recovery
                 Account owner cannot be reached within defined SLA → escalate to Level 4 hold
          NO  → Immediate Level 4 suspension (active fraud, no victim to protect)
  NO  → Two Tier 2 signals?
          YES → Level 2 (spend cap) + monitoring + owner notification
          NO  → Level 0 (monitor) + flag for follow-up watch
```

> Contact window and watch period SLAs are proposed values — need verified against operational capacity.

**Critical distinction:** If the legitimate account owner responds and cooperates, the enforcement action is protective (helping them), not punitive. Frame communication accordingly.

---

## Advertiser Communication Template

> ⚠️ Templates below are drafts. English version requires legal review. Mandarin version requires native speaker review before use.

**Initial notice:**

> We have temporarily restricted your account due to unusual activity that may indicate unauthorized access. This action is protective — we want to ensure you remain in control of your account.
>
> **Immediate steps:**
>
> 1. Verify your identity via [link]
> 2. Review recent logins and payment changes in Account Security
> 3. If you did not authorize recent activity, contact our priority support line: [link]
>
> Your account will be restored once identity is verified. Ad spend incurred during the unauthorized period is under review for waiver.

**中文版：**

> 由于检测到异常账户活动，我们已暂时限制您的账户访问。此操作旨在保护您的账户安全。
>
> **请立即采取以下步骤：**
>
> 1. 通过[链接]验证您的身份
> 2. 在账户安全中心查看近期登录记录和支付方式变更
> 3. 如有未经授权的操作，请联系优先支持渠道：[链接]

---

## Appeal Standard

**Overturn condition:** Account owner provides identity verification + demonstrates they did not authorize the flagged activity.

**If overturned:**

- Restore account immediately
- Waive fraudulent spend charges (refer to Finance)
- Issue postmortem: was the ATO preventable at detection stage?
- Package the case as a training signal for the ATO classifier

**If upheld:** The "owner" in appeal is not the legitimate owner. Maintain suspension.

---

## Postmortem Questions — ATO Cases

1. At what point did the first signal appear, and how long before detection?
2. Was the legitimate owner notified before or after enforcement action?
3. Did the attacker succeed in exfiltrating spend/data before we acted?
4. What would have shortened the detection-to-action window?
5. Is this a campaign pattern (same fraud infrastructure used across multiple accounts)?

---

## Metrics — ATO Specific

| Metric                         | Definition                                                    | Target              |
| ------------------------------ | ------------------------------------------------------------- | ------------------- |
| **ATO catch rate**             | % of confirmed ATO events detected before >$X spend           | Proposed: >95%      |
| **False action rate**          | % of ATO actions where legitimate owner was never compromised | Proposed: <1%       |
| **Detection-to-action window** | Time from first Tier 1 signal to enforcement action           | Proposed: <2hr (P0) |
| **Owner recovery SLA**         | Time from legitimate owner contact to account restoration     | Proposed: <4hr      |
| **Fraudulent spend recovered** | % of spend from ATO period successfully waived/recovered      | Tracked             |

> Metric targets above are proposed values — need verified against operational benchmarks.

---

_See also: [Impersonation Playbook](impersonation.md) · [Policy Circumvention Playbook](policy-circumvention.md)_
