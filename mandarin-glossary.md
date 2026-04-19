# 广告主诚信与行为治理术语表
# Advertiser Integrity & Risk Governance Glossary

> **Scope:** Actor/advertiser risk governance — TikTok Ads context  
> **Languages:** English · 中文  
> **Use:** Policy documentation · Reviewer calibration · CN-side advertiser communications

---

## Risk Types 风险类型

| English | 中文 | Definition | 定义 |
|---|---|---|---|
| Account Takeover (ATO) | 账号被盗 / 账号劫持 | Unauthorized third-party access to a legitimate advertiser account | 未经授权的第三方获取合法广告主账号的控制权 |
| Impersonation | 冒充欺诈 / 身份伪冒 | Falsely claiming to be a brand, agency, or individual | 虚假宣称代表某品牌、代理机构或个人 |
| Bad Debt | 坏账 | Ad spend that cannot be recovered from the advertiser | 无法从广告主处追回的广告消费 |
| Overspend | 超额消费 | Ad spend exceeding the advertiser's credit capacity | 广告消费超出广告主信用额度 |
| Policy Circumvention | 政策规避 | Intentional evasion of enforcement through account re-creation, proxies, or cloaking | 通过新建账号、代理渠道或技术手段刻意规避执法 |
| Fraudulent Ad Content | 虚假广告内容 | Ad creative containing false, misleading, or prohibited claims | 包含虚假、误导性或违禁内容的广告素材 |
| Cloaking | 技术隐蔽 / 内容伪装 | Showing different content to reviewers vs. end users | 向审核人员和真实用户展示不同广告内容 |
| Coordinated Inauthentic Behavior | 协调性虚假行为 | Multiple accounts acting in concert to evade detection | 多个账号协同操作以规避检测 |

---

## Enforcement Actions 执行措施

| English | 中文 | Definition |
|---|---|---|
| Monitor | 监控 | Enhanced observation; no account restriction |
| Warning | 警告通知 | In-product notice; no spend restriction |
| Spend Cap | 消费限额 | Daily spend capped below normal credit limit |
| Account Restriction | 账号限制 | Ads paused; account read-only |
| Account Suspension | 账号暂停 | Full suspension; ad serving halted |
| Permanent Ban | 永久封禁 | Irreversible; entity block applied |
| Entity Block | 实体封禁 | Block extended to all linked accounts and entities |

---

## Evidence & Decision Standards 证据与决策标准

| English | 中文 | Definition |
|---|---|---|
| Evidence Chain | 证据链 | Complete, traceable record of all signals supporting an enforcement decision |
| Tier 1 Signal | 一级信号 | Definitive evidence; sufficient for enforcement action |
| Tier 2 Signal | 二级信号 | Corroborative evidence; sufficient with other Tier 2 signals |
| Tier 3 Signal | 三级信号 | Indicative evidence; insufficient alone |
| Linkage Map | 关联图谱 | Documentation of cross-account or cross-entity connections |
| Confidence Score | 置信度评分 | ML model's probability estimate that a risk event is genuine |
| Decision Rationale | 决策依据说明 | Plain-language explanation of why an enforcement action was taken |

---

## Human Oversight Model 人机协同模型

| English | 中文 | Definition |
|---|---|---|
| HITL — Human-in-the-Loop | 人工主导 | Human makes the decision; ML provides evidence draft |
| HOTL — Human-on-the-Loop | 人工监督 | System recommends; human approves or overrides |
| HOOL — Human-out-of-the-Loop | 系统自动 | System acts autonomously; human reviews in batch |

---

## Quality & Measurement 质量与度量

| English | 中文 | Definition |
|---|---|---|
| Precision | 精确率 | Of all enforcement actions, % that were correct |
| Recall | 召回率 | Of all actual violations, % that were detected |
| F1 Score | F1值 | Harmonic mean of Precision and Recall |
| False Positive | 误报 / 假阳性 | Enforcement action taken against a non-violating account |
| False Negative | 漏报 / 假阴性 | Actual violation that was not detected or actioned |
| False Action Rate | 误处置率 | % of enforcement actions that were false positives |
| Catch Rate | 捕获率 | % of actual violations detected — equivalent to Recall |
| Appeal Overturn Rate | 申诉推翻率 | % of appeals that result in the original action being reversed |
| Blind Audit | 盲审 | Quality review conducted without access to original reviewer's rationale |
| Calibration Session | 校准会议 | Structured session to align reviewer decisions and identify policy gaps |

---

## Process Terms 流程术语

| English | 中文 | Definition |
|---|---|---|
| Triage | 分诊 / 初步研判 | Classification and prioritization of incoming risk signals |
| Postmortem | 复盘 | Structured analysis of a failure to identify root cause and durable fix |
| Durable Fix | 长效修复 | A governance improvement that prevents recurrence — not just resolving the immediate case |
| Root Cause Analysis (RCA) | 根本原因分析 | Process to identify the underlying cause of a failure |
| Canary Rollout | 金丝雀发布 | Limited deployment (1% traffic) to test policy/system changes before full release |
| MTTR | 平均修复时间 | Mean Time to Resolution — from incident detection to durable fix deployment |
| SLA | 服务水平协议 | Service Level Agreement — the defined time window for completing a task |
| Edge Case | 边界案例 | Case where existing policy language does not clearly determine the correct outcome |

---

## Actor Lifecycle Terms 广告主生命周期术语

| English | 中文 | Definition |
|---|---|---|
| KYC (Know Your Customer) | 实名认证 / 客户身份核查 | Identity verification at account onboarding |
| Onboarding | 入驻 | The process of a new advertiser gaining access to the platform |
| Appeal | 申诉 | Formal challenge to an enforcement action |
| Advertiser | 广告主 | Entity purchasing ad placements on TikTok Ads |
| Business Center | 商业中心 | TikTok's multi-account management hub for agencies |
| Managed Account | 托管账号 | Advertiser account managed by an agency on behalf of the brand |
| Self-Serve | 自投 | Advertiser directly manages their own account without agency |
| LTV (Lifetime Value) | 生命周期价值 | Total ad spend from an advertiser account over its lifetime |

---

## Common CN-Side Advertiser Communications 常用对外沟通表达

| Situation | English | 中文 |
|---|---|---|
| Suspension notice | "Your account has been suspended due to a policy violation." | "您的账号因违反平台政策已被暂停。" |
| Appeal invitation | "You may appeal this decision within 30 days." | "您可在30天内对此决定提出申诉。" |
| Evidence request | "Please provide documentation to support your identity claim." | "请提供相关证明材料以核实您的身份。" |
| Protective restriction | "We have temporarily restricted your account due to unusual activity." | "由于账号出现异常活动，我们已暂时限制您的账号访问权限。" |
| Appeal outcome — overturn | "Upon review, we have reversed the enforcement action on your account." | "经复核，我们已撤销对您账号的处置决定。" |
| Policy clarification | "Please review our updated policy guidelines before resuming activity." | "请在恢复推广活动前仔细阅读我们更新后的政策指引。" |
