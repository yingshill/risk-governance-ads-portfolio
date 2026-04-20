# Roadmap

**Portfolio Build Tracker — Risk Governance Portfolio**

> **Working principle:** Ship in dependency order. The README is the front door — everything else references it. Content must be locked before the HTML page. Human refinement happens in framework → case → metrics → docs order because cases cite frameworks, and metrics cite both.

---

## Build Phases

### Phase 1 — Foundation ✦ In Progress

Get the repo readable and navigable before touching content.

- [x] **README — render pass** ✅ _April 2026_
  - Philosophy quote moved to top — first thing reader sees
  - Identity-neutral — no personal names anywhere
  - Badges added: status, file count, language, updated date
  - Three-Layer model rebuilt as Mermaid diagram with feedback loop arrow
  - JD mapping table: identity-neutral columns, GitHub-compatible links
  - Flat repo tree replaced with per-folder tables with file-level descriptions
  - Build Status checklist added at the bottom

- [x] **CONTRIBUTING.md — methodology explainer** ✅ _April 2026_
  - Tone & Voice section added: straightforward, humble, accurate, curious, practical
  - Per-document-type reading guide (policy, SOP, process engine, case playbook, metrics, ref docs)
  - How the Three-Layer framework connects every file
  - Precise definition of "durable fix"
  - Build protocol: structured drafts → repo owner review in dependency order

---

### Phase 2 — Refinement ✦ Backlog

Each file reviewed, corrected, and sharpened through repo owner judgment. Drafts are starting points — accuracy and credibility come from review.

**Refinement order follows dependency chain:**

#### 2A — Frameworks (refine first — cases and metrics cite these)

- [ ] `frameworks/actor-suspension-policy.md`
  - Verify evidence tier thresholds are realistic for TikTok Ads context
  - Check consequence levels (L0–L5) against what you know of TikTok's actual enforcement tiers
  - Add any CN-side advertiser-specific nuances (e.g., how KYC works for cross-border advertisers)
  - Confirm appeal SLAs match TikTok's actual timelines if known

- [ ] `frameworks/tiered-enforcement-sop.md`
  - Validate HITL/HOTL/HOOL confidence thresholds (0.75 / 0.98) — are these defensible?
  - Refine the P0 incident response timeline based on real operational experience
  - Add anything the canary rollout section is missing from Flip experience
  - Check the calibration session design against what actually works

- [ ] `frameworks/7-step-process-engine.md`
  - This is the most conceptual file — review for any gaps vs. how you'd actually run this
  - Confirm the feedback loop description matches how Moody's postmortem → retrain actually worked
  - Add concrete examples to any step that feels abstract

#### 2B — Cases (refine after frameworks — each case references the policy)

- [ ] `cases/ato-account-takeover.md`
  - Validate signal taxonomy against real ATO patterns you've seen or researched
  - Refine the advertiser communication templates (tone, bilingual accuracy)
  - Add anything the postmortem questions section is missing

- [ ] `cases/impersonation.md`
  - Review the four impersonation types — any missing for TikTok Ads specifically?
  - Validate evidence chain minimum for action
  - Check the decision framework logic

- [ ] `cases/bad-debt-overspend.md`
  - The credit risk scoring model is illustrative — flag any variables that need adjustment
  - Validate the intentional vs. operational bad debt distinction
  - Confirm the workout process description is realistic

- [ ] `cases/policy-circumvention.md`
  - The edge case resolution protocol is the most interview-relevant section — sharpen it
  - Add any circumvention patterns specific to CN-side advertisers
  - Validate the intentionality indicators in the evidence chain standard

- [ ] `cases/fraudulent-ad-content.md`
  - The income claim decision tree is the most likely interview question area — refine carefully
  - Check pre-serve vs. post-serve catch rate targets for realism
  - Add any TikTok-specific prohibited content categories you know of

#### 2C — Metrics (refine after cases — metrics are the measurement layer for everything above)

- [ ] `metrics/quality-audit-system.md`
  - Validate the 500-case sample design stratification
  - Refine slice dimensions — anything missing for TikTok's advertiser population?
  - Check the calibration health metric (>85% agreement target)

- [ ] `metrics/kpi-definitions.md`
  - Verify every formula is precisely defined and calculable
  - Add any missing metrics that Kai's ops background would expect to see
  - Check alert thresholds for realism

- [ ] `metrics/system-health-report.md`
  - This is a template — refine the structure so you'd actually use it
  - Make sure Section 3 (slice analysis) is detailed enough to demonstrate the methodology

#### 2D — Docs (refine last — these are reference documents, not operational)

- [ ] `docs/governance-frameworks-map.md`
  - Check that every framework cited is accurate (NIST AI RMF, ITIL, PDCA, DMAIC, Three Lines)
  - Verify the "Interview soundbite" sections — would you actually say these?
  - Add any regulatory framework nuance from Moody's OFAC/sanctions experience

- [ ] `docs/mandarin-glossary.md`
  - **Critical:** Native speaker review of every Chinese term
  - Check that the "common CN-side advertiser communications" section uses natural business Mandarin, not translated English
  - Add any terms that came up in R1 or R2 conversations

---

### Phase 3 — Deployment ✦ Backlog

Repo is locked. Build the public-facing layer.

- [ ] **HTML portfolio page**
  - Single-page site that surfaces the repo's key content for non-GitHub audiences
  - Designed to be shared as a link — readable by Kai without needing to navigate GitHub
  - Sections: intro + philosophy · JD mapping · Three-layer framework visual · 5 risk cases summary · metrics methodology · quick links to repo
  - Mobile-readable (Kai may open this on a phone before the interview)
  - _Dependency: all Phase 2 refinements complete — HTML content mirrors locked repo content_

- [ ] **GitHub Pages enable**
  - Point to the HTML page as the repo's `index.html`
  - Verify all repo links work from the rendered page
  - _Dependency: HTML page complete_

---

## Status Legend

| Symbol           | Meaning                               |
| ---------------- | ------------------------------------- |
| ✦ In Progress    | Active phase                          |
| ✦ Backlog        | Queued; not started                   |
| ✅ Done          | Complete; no further changes expected |
| 🔄 Needs revisit | Done but flagged for another pass     |

---

## Decisions Log

_Record any non-obvious choices made during the build so future sessions have context._

| Date     | Decision                                                                        | Rationale                                                                                    |
| -------- | ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Apr 2026 | Build order: README → CONTRIBUTING → frameworks → cases → metrics → docs → HTML | Dependency chain — downstream files reference upstream ones                                  |
| Apr 2026 | 14 files in one initial commit                                                  | Establish full skeleton first; refine in subsequent passes rather than building file-by-file |
| Apr 2026 | Confidence thresholds: 0.75 / 0.98 for HITL/HOTL/HOOL                           | Illustrative; flagged for human validation in Phase 2                                        |
| Apr 2026 | 500-case blind audit as the quality anchor metric                               | Mirrors Moody's Safety Index methodology; scales to TikTok context                           |

---

_Last updated: April 2026 · Next action: README render pass (Phase 1)_
