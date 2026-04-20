# Methodology & Contribution Guide

**How this repo is built, how to read it, and how to contribute**

---

## Tone & Voice

All documents in this repo follow these principles:

- **Straightforward** — say what it is, no inflation
- **Humble** — this is a demonstration of thinking and approach, not a production system
- **Accurate** — every threshold, formula, and claim should be defensible
- **Curious** — show the reasoning behind decisions, not just the decisions
- **Practical** — favor possible approaches over theoretical ideals

When reviewing or contributing any document, use these as the editorial standard. If a sentence overclaims, simplify it. If a threshold is illustrative, say so.

---

## The Central Claim

**All documents start as structured drafts.** Each file is scaffolded from governance principles and domain research, then refined and reviewed for:

- Accuracy of thresholds and targets against real operational experience
- Mandarin language quality — native speaker review required for glossary and communication templates
- CN-side advertiser nuances not captured in the initial draft
- Clarity and credibility — if a claim feels inflated, it gets simplified

---

## Document Types and How to Read Them

### 1. Policy Framework (`/frameworks/actor-suspension-policy.md`)

**What it is:** The rulebook. Defines what counts as a violation, what evidence is required, what consequences apply, and what rights the actor has to appeal.

**How to read it:** Top-down. The evidence tier structure (§2) is the anchor — every enforcement action in every case playbook traces back to whether Tier 1, 2, or 3 evidence was present. If you skip §2, the rest of the repo won't make sense.

**Why it's written this way:** Policy documents at the second line of defense need to be _operationally executable_, not just conceptually correct. Every section is written so that a reviewer with no prior context could make the right decision. The test: could a third-line auditor reconstruct every enforcement action from the policy alone? If no → the policy has a gap.

**What makes a policy enforceable:**

- Precise evidence standards (not "sufficient evidence" but "Tier 1 signal OR two independent Tier 2 signals")
- Tiered consequences that scale with evidence strength
- Documented appeal rights that are genuine, not performative
- Version control with a change protocol — policy changes that don't have a rollout mechanism create inconsistency overnight

---

### 2. SOP (`/frameworks/tiered-enforcement-sop.md`)

**What it is:** The policy translated into repeatable operational steps. If the policy is the law, the SOP is the officer's procedure manual.

**How to read it:** The confidence-based routing table at the top is the most important single element — it tells you who decides under what conditions. Read that, then the 7-step sequence, then the rollout gates.

**Why it's written this way:** SOPs fail in two predictable ways: they're too abstract to follow (reviewer has to interpret too much), or too rigid to handle edge cases (reviewer has no discretion when they need it). This SOP is designed to be prescriptive where the evidence is clear (HOOL at ≥0.98) and to preserve human judgment where it isn't (HITL below 0.75).

**The canary rollout gates** exist because policy changes that ship to 100% of traffic immediately are how governance systems break. Every threshold change is a hypothesis. Canary deployment is how you test the hypothesis before it affects every advertiser.

---

### 3. 7-Step Process Engine (`/frameworks/7-step-process-engine.md`)

**What it is:** The operational sequence that fires every time a risk event hits — from detection through postmortem. Not a one-time checklist; a reusable engine.

**How to read it:** Step 7 (postmortem) is as important as Step 1 (detection). Most governance documents treat postmortems as optional or backward-looking. This one treats postmortem as the mechanism that improves every future run of Steps 1–6.

**Why it's called an engine, not a process:** A process stops when the task is done. An engine generates output that feeds the next cycle. The distinction matters because it changes how you treat failure — not as a closed case, but as an investment in the next detection cycle.

---

### 4. Case Playbooks (`/cases/`)

**What they are:** Applied policy — how the frameworks in `/frameworks` play out against a specific risk type. Each playbook is a complete, end-to-end governance document for one actor risk.

**How to read them:** Every playbook follows the same structure deliberately:

```
1. Risk definition          — what exactly is this?
2. Why it's distinct        — how does it differ from adjacent risk types?
3. Signal taxonomy          — Tier 1 / Tier 2 / Tier 3 signals
4. Evidence chain standard  — minimum for action
5. Decision framework       — explicit decision tree
6. Advertiser communication — what the actor receives (bilingual where relevant)
7. Appeal standard          — what overturns the decision
8. Postmortem questions     — what to investigate after every case
9. Metrics                  — how this risk type is measured specifically
```

**Why the same structure for every case:** Reviewers who work across risk types need consistent mental models. If ATO playbooks are structured differently from impersonation playbooks, reviewers carry higher cognitive load and make more errors at the boundaries. Structural consistency is itself a governance design choice.

**The "Why It's Distinct" section** exists because the most common reviewer error is applying the wrong playbook to an edge case. Understanding why ATO is different from circumvention — even when they look similar — prevents misclassification before it happens.

---

### 5. Metrics (`/metrics/`)

**What they are:** The measurement layer for everything above. If the policy and SOPs are the design, metrics are how you know whether the design is working.

**How to read them:** Start with `kpi-definitions.md` to understand what each metric means precisely. Then `quality-audit-system.md` to understand how the measurements are taken. Then `system-health-report.md` as the synthesis.

**Why blind audits, not just system metrics:** System metrics (action count, catch rate from the system's own logs) tell you what the system did. They don't tell you whether it was right. A system can maintain a stable aggregate catch rate while accumulating false actions in specific slices — if those slices are small enough, aggregate metrics won't surface them.

The 500-case blind audit exists to find what aggregate metrics hide. The stratified sample (overweighted toward overturns and edge cases) is designed to stress-test the system, not flatter it.

**Why every KPI has an alert threshold:** A metric without an action trigger is just a dashboard decoration. Every KPI definition includes the threshold at which someone is required to investigate — not recommended to, required to.

---

### 6. Reference Docs (`/docs/`)

**`governance-frameworks-map.md`** — Maps industry frameworks (Three Lines, NIST AI RMF, PDCA, DMAIC, ITIL) to the specific work in this repo. Exists so that a reader familiar with any of these frameworks immediately understands where this work sits within the broader governance landscape.

**`mandarin-glossary.md`** — Bilingual EN/中文 terminology. Exists because governance documentation that crosses language boundaries fails at translation. "False positive" and "误报" are not interchangeable in all contexts — the glossary locks the mapping so that CN-side advertiser communications, internal policy documents, and reviewer calibration materials all use the same terms.

---

## The Three-Layer Framework — Why Everything Connects

Every document in this repo belongs to one or more of three layers:

```
Layer A — Actor Lifecycle (WHAT)     → what stage of the advertiser's journey?
Layer B — Ops Stack (HOW)            → what governance capability is being deployed?
Layer C — 7-Step Process (WHEN)      → which step of the operational sequence?
```

When you pick up any document, ask: which layer does this primarily address?

- `actor-suspension-policy.md` → Layer B (Policy, the core ops capability)
- `tiered-enforcement-sop.md` → Layer B (SOP Design) + Layer C (the operational sequence)
- `7-step-process-engine.md` → Layer C (the full sequence)
- Case playbooks → Layer A (lifecycle stage: Enforcement) + Layer C (specific steps for this risk type)
- `quality-audit-system.md` → Layer B (Process Health Metrics)
- `kpi-definitions.md` → Layer B (Process Health Metrics — the measurement definitions)

The feedback loop — postmortem findings → policy update → SOP revision → model retrain — is what connects all three layers into a system that improves rather than stagnates.

---

## What "Durable Fix" Means

This phrase appears throughout the repo. It deserves a precise definition.

A **durable fix** is a governance improvement that prevents the same class of failure from recurring — not just resolving the immediate case.

| What it's not        | What it is                                                |
| -------------------- | --------------------------------------------------------- |
| Closing the ticket   | Policy update that changes the evidence standard          |
| Warning the reviewer | Calibration case added to the training library            |
| Flagging the model   | Labeled training data package sent to R&D for retrain     |
| Noting the edge case | Decision tree published and communicated to all reviewers |

The test: if the same failure pattern occurs again in 90 days, did the fix prevent it or just delay it? If it recurs, the fix was not durable.

---

_April 2026 · [ROADMAP](ROADMAP.md)_
