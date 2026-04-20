# Case Study — Platform Merchant Governance Failure

**PDD "Ghost Delivery" Enforcement Action · April 2026**

> **Purpose:** Real-world governance failure analysis — mapped to the Three-Layer Framework and 7-Step Process Engine in this repo.
> **Scope note:** This case originates in merchant/food delivery integrity. Section 7 translates findings to the advertiser/actor risk surface relevant to this repo's domain.

> ⚠️ **Note:** All facts and figures are sourced from primary regulatory documents and cited press reporting. See references at the end of each section.

---

## 1. Case Overview

**Enforcement action:** On April 17, 2026, China's State Administration
for Market Regulation (SAMR / 国家市场监督管理总局) announced administrative
penalties against 7 major e-commerce platforms for the "Ghost Delivery"
(幽灵外卖) series of cases — the largest fine in the history of China's
Food Safety Law enforcement.

**Platforms penalized:** PDD (Pinduoduo) · Meituan · JD.com · Ele.me
(Taobao Flash Purchase) · Douyin · Taobao · Tmall

**Total penalty:** ¥3.597 billion across all 7 platforms; platform legal
representatives and food safety directors fined an additional
¥19.69 million combined [^1]

**PDD-specific penalty:**

- Platform fine: ¥1.52 billion (罚没款合计)
- Co-founder & Co-CEO Zhao Jiazhen: ¥6.93 million personal fine
- Operational restriction: suspended from adding new cake shop
  merchants (excluding pre-packaged) for 9 months
- Notable: PDD employees physically obstructed investigators;
  one investigator sustained injuries during the investigation [^2]

**Douyin-specific penalty (direct TikTok analog):**

- Decision reference: 国市监处罚〔2026〕10号
- Legal entity penalized: 北京抖音科技有限公司
- 454 cake merchants allowed to operate without valid licenses:
  412 with no valid license; 24 with no license uploaded;
  17 with falsified licenses; 1 with unlisted production license
- Total transaction value from non-compliant merchants: ¥378.89 million
- Platform illegal gains: ¥9.49 million
- Penalty: ¥9.49M confiscated + ¥45.4M fine (KYC failure) +
  ¥2M fine (failure to act on consumer harm) = ¥56.89M total
- Operational restriction: suspended from adding new cake merchants
  for 6 months [^3]

**Core violations (across all platforms):**

- Failed to verify food business licenses for merchants
  (KYC/onboarding failure)
- Authorized "one-click order transfer" (一键转单) via API access —
  allowing merchants to silently redirect consumer orders to
  third-party producers without consumer knowledge (platform-enabled
  circumvention)
- Platforms acted despite knowing or having reason to know that
  the transfer system harmed consumer rights [^2]

**Douyin-specific violations (direct TikTok analog):** [^3]

- **API partners named:** 转单宝 (重庆转单宝网络科技有限公司) and
  安徽梦馨信息技术有限公司 — granted order query + logistics
  dispatch API access; 379 merchants used this to silently transfer orders
- **Legal finding:** Each of the 454 KYC failures constitutes an
  independent violation — penalized at ¥100K per store
- **No objection filed:** Douyin did not submit written defense
  or request a hearing within the statutory period

**Enforcement mechanism:**

- "One store, one penalty" (一店一处罚) principle — each non-compliant
  merchant counted as an independent violation, multiplying the
  total fine by merchant count rather than treating all failures
  as a single infraction [^2]
- First-ever simultaneous personal fines on platform legal
  representatives and food safety directors in this sector [^2]

---

## 2. Governance Failure Taxonomy

### Scope Mapping

Per [`actor-suspension-policy.md`](../frameworks/actor-suspension-policy.md) §1:

| Scope                         | Definition                                                   | This Case                                                                                    |
| ----------------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| **Merchant/Seller Integrity** | Merchant onboarding, listing, fulfillment compliance         | Primary scope of PDD case — food merchant KYC, license verification, order fulfillment chain |
| **Platform Integrity**        | Systemic: tools, APIs, infrastructure that enable violations | API-enabled 转单 system; audit obstruction; accountability chain                             |
| **Advertiser Integrity**      | Ad account, creative, spend behavior compliance              | Out of scope for this case — translated in Section 7                                         |

> Key boundary: most violations in this case sit in **Merchant Integrity**, but the **Platform Integrity** failures are scope-agnostic — they apply equally to merchant and advertiser governance. Section 7 translates across this boundary.

---

### Failure Taxonomy

**Failure 1 — Onboarding KYC Gap**

- **Scope:** Merchant Integrity
- **What happened:** Platforms failed to verify food business licenses at merchant onboarding. Douyin alone allowed 454 non-compliant merchants to operate — including merchants with falsified licenses that passed surface-level review [^3]
- **Governance layer:** Layer A failure (Onboarding stage) — the first lifecycle checkpoint did not exist or was not enforced
- **Root cause:** Competitive pressure to onboard merchants faster than rivals. One platform employee stated to investigators: "If we screen too strictly, merchants will just go to other platforms." [^2]

**Failure 2 — Platform-Enabled Circumvention (API Design)**

- **Scope:** Platform Integrity
- **What happened:** Platforms signed cooperation agreements with 转单 service providers and granted them API access — order query, logistics dispatch, batch data decryption — knowing or having reason to know this enabled prohibited order transfers [^2][^3]
- **Governance layer:** Layer B failure (SOP Design) — the platform's own tooling operationalized the violation at scale
- **Root cause:** API access was a deliberate product decision, not an oversight. The 转单 system processed over 3.6 million orders across 7 platforms [^2]

**Failure 3 — Consumer Disclosure Gap**

- **Scope:** Merchant Integrity · Platform Integrity
- **What happened:** Consumers selected merchants based on brand reputation, hygiene records, and preparation style — then had their orders silently transferred to anonymous third-party producers bidding on price. No disclosure mechanism existed [^2]
- **Governance layer:** Layer C failure (Action stage) — enforcement action was never triggered because the signal (order transfer) was invisible to the detection layer
- **Root cause:** Detection design did not account for platform-authorized transfers as a risk signal

**Failure 4 — Audit Defensibility Failure (Obstruction)**

- **Scope:** Platform Integrity
- **What happened:** PDD refused to provide materials, submitted false information, and used physical resistance against investigators. One investigator sustained a fractured finger and ankle injury [^2]
- **Governance layer:** Layer B failure (Feedback Loop) — the postmortem mechanism (regulatory audit) was actively blocked
- **Root cause:** No internal audit trail existed that could survive external scrutiny; obstruction was the only available response

**Failure 5 — Accountability Chain Failure**

- **Scope:** Platform Integrity
- **What happened:** Governance failures persisted across multiple years without internal correction. No escalation to executive level occurred until external regulatory pressure forced it [^2]
- **Governance layer:** Layer B failure (Policy) — no internal policy existed that would have flagged API-enabled 转单 as a governance risk requiring executive sign-off
- **Root cause:** "Platform Integrity" was treated as a compliance checkbox, not a governance function with teeth

---

### Cross-Scope Insight

Platform Integrity failures (Failures 2, 4, 5) are **scope-agnostic** — the same failure patterns appear in advertiser governance:

- Granting API access that enables policy circumvention → **Advertiser: agency proxy re-entry**
- No audit trail surviving external review → **Advertiser: evidence chain gaps**
- No executive accountability mechanism → **Advertiser: governance without enforcement**

Section 7 maps each failure to its TikTok Ads analog explicitly.

---

## 3. How the 7-Step Process Engine Should Have Caught This

This section walks the case through the 7-step process engine defined in
[`7-step-process-engine.md`](../frameworks/7-step-process-engine.md) —
identifying where each step failed or did not exist.

---

**Step 1 — Detection 检测 · FAILED**

The 转单 system operated through platform-authorized API access. Because
the platform itself granted the access, the behavior was invisible to any
detection layer that treated platform-authorized actions as trusted. No
signal was ever generated.

- What should have existed: a detection rule flagging API access grants
  to third-party service providers that touch order fulfillment data —
  treated as a high-risk permission requiring governance review
- What existed instead: nothing — the API grant was a product decision
  with no risk review gate

---

**Step 2 — Triage 分诊 · NOT REACHED**

No signal surfaced from Step 1, so triage never fired. The case was
eventually opened not from internal detection but from a single consumer
complaint filed with a local regulator in July 2025 — over a cake with
fresh flowers [^2].

- What should have existed: a triage escalation path for consumer
  complaints that cross-references platform API access grants
- What existed instead: the complaint was handled locally until
  investigators discovered the systemic pattern

---

**Step 3 — Evidence Chain Assembly 证据链 · FAILED WHEN ATTEMPTED**

When regulators attempted to assemble an evidence chain, platforms
actively obstructed access. PDD refused to provide materials, submitted
false information, and physically resisted investigators. Investigators
had to build custom data models to penetrate platform data architecture
and extract order flow records [^2].

- What should have existed: an internal audit trail reconstructable
  by any independent reviewer from raw data — the standard defined
  in [`actor-suspension-policy.md`](../frameworks/actor-suspension-policy.md) §2
- What existed instead: encrypted, fragmented, and in some cases
  falsified records

---

**Step 4 — Decision 研判 · NOT REACHED INTERNALLY**

No internal decision was ever made to investigate or act on the 转单
system. The decision to act came entirely from external regulators,
not from any internal governance process.

- What should have existed: a policy that classified API access
  grants to fulfillment-touching third parties as a governance
  decision requiring evidence review and sign-off
- What existed instead: the API grant was treated as a routine
  product integration

---

**Step 5 — Action 处置 · NOT REACHED INTERNALLY**

No internal enforcement action was taken. Platforms only acted after
receiving formal administrative penalty decisions in April 2026 —
approximately 9 months after the initial consumer complaint [^2].

- What should have existed: a self-correction mechanism triggered
  by detection of unauthorized fulfillment transfers
- What existed instead: public statements of acceptance after
  the penalty was issued

---

**Step 6 — Appeal 申诉 · PARTIALLY USED**

Douyin did not file a written defense or request a hearing within
the statutory period [^3]. PDD accepted the penalty publicly.
No platforms successfully challenged the core findings.

- What this signals: the evidence assembled by regulators — despite
  obstruction — was sufficient to withstand challenge
- Governance implication: had platforms maintained audit-defensible
  internal records, they may have had grounds to dispute findings;
  instead obstruction foreclosed that option

---

**Step 7 — Postmortem 复盘 · EXTERNALLY FORCED**

The postmortem in this case was conducted by regulators, not by
the platforms. The durable fix — policy clarification, enforcement
standard, personal liability precedent — was imposed externally
rather than generated internally [^2].

- What should have existed: an internal postmortem cycle that
  identified the 转单 API risk before regulators did
- What existed instead: a reactive public statement after the
  penalty landed

---

### Summary — Where the Engine Broke

| Step               | Status                 | Root Failure                                                 |
| ------------------ | ---------------------- | ------------------------------------------------------------ |
| 1 — Detection      | Failed                 | No risk signal for platform-authorized API grants            |
| 2 — Triage         | Not reached            | Detection never fired                                        |
| 3 — Evidence Chain | Failed when attempted  | No audit-defensible internal records                         |
| 4 — Decision       | Not reached internally | No internal policy classifying API grants as governance risk |
| 5 — Action         | Not reached internally | No self-correction mechanism                                 |
| 6 — Appeal         | Partially used         | Obstruction foreclosed challenge options                     |
| 7 — Postmortem     | Externally forced      | No internal feedback loop existed                            |

> The engine did not fail at one step — it was never installed.
> Detection, triage, and decision all required a policy foundation
> that did not exist. This is a Layer B (Ops Stack) failure that
> cascaded into every Layer C (Process) step.

---

## 4. Policy Gaps Identified

<!-- PENDING -->

---

## 5. Durable Fix Recommendations

<!-- PENDING -->

---

## 6. Regulatory & Accountability Dimension

<!-- PENDING -->

## 7. Relevance to TikTok Ads Context

<!-- PENDING -->

---

_See also: [Policy Circumvention Playbook](policy-circumvention.md) · [Actor Suspension Policy](../frameworks/actor-suspension-policy.md) · [7-Step Process Engine](../frameworks/7-step-process-engine.md)_
