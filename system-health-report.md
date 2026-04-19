# System Health Report Template
**Monthly · Risk Governance Operations · Business Integrity**

> **Purpose:** Provide leadership with a single, auditable view of enforcement quality across all risk types.  
> **Owner:** Policy team  
> **Distribution:** Business Integrity VP · Ops Lead · ML Lead · Legal (as needed)  
> **Format:** This template; fill in bracketed fields monthly

---

## SYSTEM HEALTH REPORT — [MONTH YEAR]

**Reporting period:** [Start Date] – [End Date]  
**Prepared by:** [Policy Lead]  
**Distribution:** [List]

---

### SECTION 1 — EXECUTIVE SUMMARY

| Metric | This Month | Last Month | Δ | Status |
|---|---|---|---|---|
| Overall Precision | | | | 🟢 / 🟡 / 🔴 |
| Overall Recall (Catch Rate) | | | | 🟢 / 🟡 / 🔴 |
| False Action Rate | | | | 🟢 / 🟡 / 🔴 |
| Appeal Overturn Rate | | | | 🟢 / 🟡 / 🔴 |
| F1 Score | | | | 🟢 / 🟡 / 🔴 |
| P0 Incidents | | | | 🟢 / 🟡 / 🔴 |
| MTTR (P0 incidents) | | | | 🟢 / 🟡 / 🔴 |
| SLA Compliance | | | | 🟢 / 🟡 / 🔴 |

**Status key:** 🟢 On target · 🟡 Watch · 🔴 Requires action

**One-paragraph narrative:**  
*[Summarize the month's key findings in plain language. What improved? What degraded? What is the most important thing leadership should know?]*

---

### SECTION 2 — RISK TYPE BREAKDOWN

| Risk Type | Precision | Recall | FAR | Overturn Rate | Cases Reviewed |
|---|---|---|---|---|---|
| ATO | | | | | |
| Impersonation | | | | | |
| Bad Debt | | | | | |
| Policy Circumvention | | | | | |
| Fraudulent Ad Content | | | | | |
| **Total** | | | | | |

**Notable findings by risk type:**
- *[Any risk type where a metric flag was triggered — describe what slice analysis showed]*

---

### SECTION 3 — SLICE ANALYSIS FINDINGS

*List all slices where a metric exceeded 2× aggregate baseline. Each entry must include: slice dimension, metric value, root cause hypothesis, and recommended action.*

| Slice | Metric | Value | Baseline | Root Cause | Action |
|---|---|---|---|---|---|
| *e.g. Content Category: Income Claims* | *FAR* | *18%* | *3%* | *Policy ambiguity on "guaranteed" language* | *Edge case decision tree — due [date]* |
| | | | | | |

---

### SECTION 4 — AUTOMATION COVERAGE

| Routing Tier | % of Total Actions | FAR | Notes |
|---|---|---|---|
| HOOL (≥0.98 confidence) | | | |
| HOTL (0.75–0.98) | | | |
| HITL (<0.75) | | | |

**Automation trend:** [Is HOOL coverage increasing while FAR holds? Describe.]

---

### SECTION 5 — DURABLE FIXES ISSUED THIS MONTH

| Fix Type | Description | Triggered By | Status |
|---|---|---|---|
| Policy update | | | Deployed / In review |
| SOP revision | | | Deployed / In review |
| Model retrain signal | | | Sent to R&D / Pending |
| Training case added | | | Added to library |
| Calibration session held | | | Completed |

---

### SECTION 6 — OPEN ITEMS (CARRY FORWARD)

| Item | Description | Owner | Due Date | Status |
|---|---|---|---|---|
| | | | | |

---

### SECTION 7 — NOTABLE INCIDENTS

*P0 incidents this month with brief summary. Full postmortems linked separately.*

| Incident ID | Date | Risk Type | Description | Status |
|---|---|---|---|---|
| | | | | Postmortem complete / In progress |

---

### SECTION 8 — NEXT MONTH FOCUS AREAS

*Based on this month's findings, what are the 2–3 highest-priority governance improvements for next month?*

1. *[Priority 1 — specific, owned, measurable]*
2. *[Priority 2]*
3. *[Priority 3]*

---

*Report version: [v1.0] · Last template update: April 2026*
