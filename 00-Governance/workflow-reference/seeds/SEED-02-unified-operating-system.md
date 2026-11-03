---
id: SEED-02
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "unified_product_engineering_marketing_growth_sales_operating_system.md"
---

# Unified Product, Engineering, Marketing, Growth & Sales Operating System

## 1. Executive Summary

This operating model integrates Product, Engineering, Security, Reliability, Operations, Marketing, Growth, Sales, Finance, Legal/Compliance, Analytics, Customer Success, and Portfolio Management into one governed **idea-to-product-to-revenue-to-production-learning** lifecycle.

The model is built on six principles:

1. **Engineering begins before investment approval.** Preliminary feasibility, architecture exploration, engineering effort, build duration, infrastructure cost, dependency risk, security burden, reliability expectations, and maintenance cost influence Commercial Analysis, Forecasting, Composite Scoring, and the Investment Decision.
2. **Technical depth increases as the opportunity earns investment.** The lifecycle distinguishes Preliminary Technical Feasibility, Execution-Grade Technical Feasibility, and continuous Implementation Feasibility / Delivery-Risk Validation.
3. **Product and Engineering remain distinct but tightly coupled.** Product owns the customer problem, desired outcome, product scope, priority, and product acceptance criteria. Engineering owns technical decomposition, architecture, implementation, technical quality, release safety, operability, and technical evidence.
4. **Implementation is iterative.** Defects return to the earliest stage capable of correcting the underlying cause rather than automatically returning to code.
5. **Launch requires three readiness views:** Engineering Release Readiness, Business/GTM/Revenue Readiness, and Integrated Launch Readiness.
6. **Launch does not end Engineering.** Observability, incidents, performance, reliability, security, cost, technical debt, architecture health, customer behavior, and commercial results all feed optimization and strategic re-evaluation.

The default path is forward. Re-entry is targeted: a material change invalidates only the affected evidence and downstream stages unless the change is systemic enough to require broader re-validation.

---

# 2. Unified Visual Text Decision Tree

```text
[PHASE 1 — SIGNAL & OPPORTUNITY DISCOVERY]

Signal Collection / Idea Submission
├─ Market / customer / sales / product signal
├─ Engineering / reliability / incident signal
├─ Infrastructure / cost signal
└─ Human-submitted idea
↓
Signal Classification
├─ Duplicate → Merge with existing opportunity/product evidence
├─ Weak but plausible → Watchlist
│  → [TRIGGER] New evidence / threshold crossed → Re-enter classification
├─ Irrelevant / prohibited → [STOP] Reject / archive
└─ Valid opportunity → Problem Discovery
↓
Exploratory Market Research
↓
Exploratory Consumer Insights
↓
Audience Discovery
↓
[DECISION GATE — Problem Validation]
├─ Proceed → Problem Validation
├─ Gather more evidence → Research / Validation Experiment
├─ Pivot problem → Problem Discovery
├─ Pivot audience → Audience Discovery
├─ Defer → Watchlist
└─ Reject → [STOP]


[PHASE 2 — PROBLEM / MARKET VALIDATION]

Problem Validation
↓
Market Analysis
↓
Competitive Analysis
↓
Early Audience Segmentation
↓
[DECISION GATE — Opportunity / Commercial Viability]
├─ Proceed → Solution Discovery
├─ Rework market scope → Market Analysis
├─ Reframe problem → Problem Discovery
├─ Pivot audience → Audience Discovery / Segmentation
├─ Gather evidence → Research / Consumer Insights
├─ Defer / Watchlist
└─ Reject → [STOP]


[PHASE 3 — SOLUTION & COMMERCIAL VALIDATION]

Solution Discovery
↓
Preliminary Product Marketing
↓
Commercial Analysis
├─ Monetization
├─ Pricing / packaging hypotheses
├─ Revenue / margin model
├─ Preliminary CAC / LTV
└─ Commercial constraints
↓
Preliminary Sales-System Design
├─ Candidate sales motions
├─ Buyer journey
├─ Qualification / routing assumptions
├─ Checkout / contract model
└─ Provisioning / onboarding assumptions

[PARALLEL — EARLY ENGINEERING]
├─ Product Requirement Framing
├─ Preliminary Technical Feasibility
│  ├─ Technical plausibility
│  ├─ Engineering effort range
│  ├─ Build-duration range
│  ├─ Infrastructure needs / cost
│  ├─ Dependency risk
│  ├─ Data availability
│  ├─ Security / privacy burden
│  ├─ Reliability / scalability limits
│  └─ Long-term maintenance burden
└─ Architecture Exploration
   ├─ Candidate system shape
   ├─ Build vs. buy
   ├─ Platform / hosting
   ├─ Data / integration approach
   └─ Feasibility spike where uncertainty is material
↓
[DECISION GATE — Preliminary Technical Feasibility]
├─ Feasible → Continue
├─ Feasible with constraints → Record constraints → Continue
├─ Prototype / spike → Run spike → Re-evaluate
├─ Re-scope product → Solution Discovery
├─ Change technology / dependency → Architecture Exploration
├─ Resolve dependency → Dependency owner → Re-evaluate
├─ [ESCALATION] Technical / security / governance review
└─ Infeasible → Solution Discovery or [STOP]
↓
Technical evidence updates Commercial Analysis + Forecasting
→ effort / duration / infrastructure cost / risk / maintenance / confidence


[PHASE 4 — PRELIMINARY TECHNICAL / RISK VALIDATION]

Risk / Legal / Security / Compliance
↓
GTM Feasibility
↓
Preliminary Forecasting
├─ Demand / revenue / margin
├─ CAC / LTV
├─ Engineering build and operating cost
├─ Infrastructure cost
├─ Sales conversion assumptions
├─ Build / release timing
└─ Delivery confidence
↓
Cross-Domain Validation
↓
[DECISION GATE — Investment Readiness]
├─ Proceed
├─ Commercial remediation → Commercial Analysis
├─ Technical remediation → Preliminary Technical Feasibility
├─ Risk remediation → Risk / Legal / Security / Compliance
├─ GTM remediation → GTM Feasibility
├─ Gather evidence → Relevant validation stage
├─ Defer / Watchlist
└─ Reject → [STOP]


[PHASE 5 — PORTFOLIO & INVESTMENT DECISION]

Composite Scoring
├─ Market / customer / commercial
├─ Technical feasibility / complexity
├─ Delivery confidence / build duration
├─ Infrastructure and maintenance cost
├─ Security / compliance burden
└─ Strategic fit
↓
Portfolio Comparison
↓
[DECISION GATE — Investment Decision]
├─ Approve
├─ Approve conditionally → Resolve conditions → Re-check
├─ Return for remediation → Earliest invalidated stage → Re-score → Re-compare
├─ Limited prototype / validation → Test → Re-score / Re-compare
├─ Defer
├─ Watchlist
├─ [ESCALATION] Policy / risk / exception review
└─ Reject → [STOP]


[PHASE 6 — PRODUCT DEFINITION]

Execution-Grade Market Research
↓
Execution-Grade Consumer Insights
↓
Execution-Grade Audience Segmentation
↓
Product Marketing
↓
Brand / Positioning
↓
Detailed Product Definition
├─ Product goals / outcomes
├─ Product scope
├─ User journeys
├─ Functional requirements
├─ UX requirements
├─ Product acceptance criteria
├─ Data requirements
├─ Accessibility requirements
├─ Compliance constraints
└─ Product analytics requirements
↓
Detailed GTM Strategy + Launch Timing
↓
Execution-Grade Forecasting


[PHASE 7 — ENGINEERING REQUIREMENTS & ARCHITECTURE]

Engineering Intake
↓
Requirements Decomposition
├─ Functional engineering requirements
├─ Non-functional requirements
│  ├─ Performance
│  ├─ Reliability
│  ├─ Scalability
│  ├─ Availability
│  ├─ Security
│  ├─ Privacy
│  ├─ Maintainability
│  ├─ Accessibility
│  ├─ Compatibility
│  ├─ Data integrity
│  ├─ Recoverability
│  ├─ Observability
│  ├─ Operability
│  ├─ Deployment safety
│  └─ Cost efficiency
├─ Integration / API / contract requirements
├─ Infrastructure requirements
├─ Data requirements
├─ Operational requirements
└─ Release requirements
↓
Requirements Version + Traceability Baseline
↓
[DECISION GATE — Requirements Readiness]
├─ Ready
├─ Ready with conditions
├─ Ambiguous → Product Definition / Requirements
├─ Missing NFR → Requirements Decomposition
├─ Conflicting → Product + Engineering resolution
└─ Material scope contradiction → Product / Commercial / GTM review
↓
Execution-Grade Technical Feasibility
↓
[PARALLEL — ARCHITECTURE]
├─ System / Application Architecture
├─ Data Architecture
├─ Integration Architecture
├─ API / Contract Design
├─ Infrastructure / Hosting Architecture
├─ Security / Privacy Architecture
├─ Reliability Architecture
├─ Observability Architecture
├─ Deployment Architecture
└─ Disaster-Recovery Design
↓
[DECISION GATE — Architecture / Technical Design]
├─ Approve
├─ Approve with conditions
├─ Simplify / redesign
├─ Technical spike
├─ Resolve dependency
├─ Change technology
├─ Revise product scope
└─ [ESCALATION] Architecture / Security / Portfolio review


[PHASE 8 — INTEGRATED PRODUCT / ENGINEERING / GTM PLANNING]

[PARALLEL]
├─ Engineering Planning
│  ├─ Work decomposition / sequence
│  ├─ Dependencies
│  ├─ Estimates / milestones
│  ├─ Staffing / resources
│  ├─ Test strategy
│  ├─ Environment strategy
│  ├─ Release strategy
│  ├─ Rollback strategy
│  └─ Contingency planning
├─ Security / Privacy / Reliability Design
├─ Revenue / Sales-System Design
├─ Campaign Strategy / Media Planning
├─ Sales Enablement Planning
├─ Provisioning / Onboarding Design
└─ Analytics / Attribution Design
↓
Engineering plan → updates Execution-Grade Forecasting + GTM launch timing
GTM timing → updates engineering milestones + release strategy
↓
[DECISION GATE — Engineering Plan / Delivery Confidence]
├─ Proceed
├─ Proceed conditionally
├─ Re-sequence → Engineering Planning
├─ Add capacity → Planning / Portfolio
├─ Reduce scope → Product Definition
├─ Change launch timing → GTM Strategy
├─ Change architecture → Architecture
├─ Resolve dependency → Planning / Architecture
└─ [ESCALATION] Confidence below threshold
↓
[DECISION GATE — Security / Privacy / Reliability Design]
├─ Approve
├─ Approve with controls
├─ Rework design
├─ Change architecture
├─ Reduce scope
└─ [ESCALATION] High / critical unresolved risk


[PHASE 9 — IMPLEMENTATION & CONTINUOUS VERIFICATION]

Environment Readiness
├─ Local / Development
├─ Test
├─ Integration
├─ Staging / Pre-Production
├─ Production-like Validation
├─ Controlled Release
└─ Production
↓
[PARALLEL]
├─ Application / Service Implementation
├─ Infrastructure Automation
├─ Data / Integration Implementation
├─ Test Automation Development
├─ Security Controls
├─ Observability Instrumentation
└─ Product Analytics Instrumentation
↓
Implementation
↓
Code Review
↓
Automated Validation
├─ Static analysis
├─ Linting
├─ Type checking
├─ Unit tests
└─ Component tests
↓
Integration Validation
├─ Integration tests
└─ API / contract tests
↓
[DECISION GATE — Implementation / Integration Quality]
├─ Healthy → Continue
└─ Issue found
   ├─ Requirement defect → Requirements
   ├─ Architecture defect → Architecture
   ├─ Security design defect → Security Design / Architecture
   ├─ Reliability design defect → Reliability Design / Architecture
   ├─ Dependency defect → Planning / Architecture
   ├─ Code defect → Implementation
   ├─ Test defect → Test Strategy / Automation
   └─ Product mismatch → Product Definition / Requirements
      → Re-validate affected downstream stages
↓
Repeat until exit criteria satisfied


[PHASE 10 — SYSTEM / SECURITY / RELIABILITY VALIDATION]

System Testing
↓
End-to-End Testing
↓
Regression Testing
↓
[PARALLEL]
├─ Performance Testing
├─ Load / Scalability Testing
├─ Reliability / Resilience Testing
├─ Security Testing
├─ Privacy Validation
├─ Accessibility Validation
└─ Compliance Validation
↓
User / Business Acceptance, where appropriate
↓
[DECISION GATE — System / NFR Validation]
├─ Pass
├─ Functional defect → Implementation / Requirements
├─ Performance issue → Architecture / Infrastructure / Implementation
├─ Scalability limit → Architecture / Capacity / Forecasting
├─ Reliability issue → Reliability Design / Architecture
├─ Security finding → Security Design / Architecture / Implementation
├─ Privacy issue → Privacy Design / Product Requirements
├─ Accessibility issue → Product / UX / Implementation
└─ Compliance issue → Compliance / Requirements / Product


[PHASE 11 — PRE-PRODUCTION VALIDATION]

Production-Like Pre-Production Validation
├─ Complete customer journeys
├─ Permissions / roles
├─ Payments / contracts
├─ Integrations / migrations
├─ Analytics / observability
├─ Runbooks
├─ Failure / recovery / rollback
├─ Device / browser compatibility
└─ Representative performance
↓
[DECISION GATE — Pre-Production Validation]
├─ Pass
├─ Controlled exception
├─ Functional remediation → Implementation
├─ Technical remediation → Architecture / Implementation
├─ Operational remediation → Operations / Runbooks
├─ Measurement remediation → Analytics / Observability
└─ Fail → Hold release


[PHASE 12 — RELEASE & GTM READINESS]

Engineering Release Readiness
├─ Functional + test evidence
├─ NFR thresholds
├─ Security / privacy / reliability evidence
├─ Environment / migration readiness
├─ Observability / runbooks
├─ Rollback evidence
└─ Release evidence package
↓
[DECISION GATE — Engineering Release Readiness]
├─ Ready
├─ Ready with controlled exceptions
├─ Limited release only
├─ Remediation required
├─ Delay
└─ Reject release

[PARALLEL]
Business / GTM / Revenue Readiness
├─ Product acceptance
├─ Campaign / sales readiness
├─ Pricing / packaging
├─ Contract / checkout / payment
├─ Support / success
├─ Provisioning / onboarding
├─ Analytics / attribution
└─ Launch timing
↓
[DECISION GATE — GTM / Revenue Readiness]
├─ Ready
├─ Limited launch
├─ Remediation required
├─ Change timing
└─ Delay

Engineering Release Readiness
+
GTM / Revenue Readiness
+
Product / Security / Reliability / Legal / Ops / Analytics readiness
↓
[DECISION GATE — Integrated Launch Readiness]
├─ Ready → Progressive Deployment
├─ Ready with controlled exceptions → Approved exception → Deployment
├─ Limited / staged launch → Controlled cohort
├─ Remediation required → Failed readiness domain
├─ Delay → GTM / Engineering Planning
├─ Roll back to earlier stage → Earliest invalidated stage
└─ Stop / reject release → [STOP]


[PHASE 13 — PROGRESSIVE DEPLOYMENT]

Build Artifact
↓
Controlled Environment
↓
Verification
↓
Canary / Pilot / Limited Cohort
↓
Observe
↓
[DECISION GATE — Deployment Expansion]
├─ Healthy → Expand deployment
├─ Degraded → Pause → Remediate → Re-verify
└─ Critical → Rollback / disable feature / failover → Incident path
↓
Feature flags + rollout + rollback controls remain active


[PHASE 14 — PRODUCTION VERIFICATION]

Production Verification
├─ App / API / auth / payment health
├─ Data correctness
├─ Customer journeys
├─ Latency / errors / resources
├─ Security telemetry
├─ Analytics / attribution
└─ Deployment health
↓
[DECISION GATE — Production Health]
├─ Healthy → Continue / expand
├─ Degraded → Hold / remediate
├─ Critical → Rollback / failover / incident
└─ Strategic defect → Product / Architecture / Commercial review


[PHASE 15 — DEMAND / SALES / ACTIVATION]

Demand Generation
↓
Demand / Lead Entry
↓
Visitor / Lead Identification
↓
Qualification
↓
Sales Motion Routing
├─ Self-Service
├─ Product-Led
├─ Sales-Assisted
├─ Outbound
└─ Hybrid
↓
Need / Solution Matching
↓
Buyer Education / Value Development
↓
Offer / Pricing / Commercial Terms
↓
Proposal / Negotiation, if required
↓
Checkout / Contract
↓
Payment / Conversion
↓
Account Provisioning
↓
Onboarding
↓
Activation / First Value
↓
Usage / Customer Health


[PHASE 16 — PRODUCTION OPERATIONS & OBSERVABILITY]

Observability / Monitoring
├─ Logs / metrics / traces
├─ Uptime / latency / error rates
├─ Resource / infrastructure / service health
├─ Security telemetry
├─ User-experience telemetry
├─ Business KPIs
├─ Deployment health
└─ SLO / SLA indicators
↓
Production Signal
↓
Severity / Impact Classification
↓
[DECISION GATE — Incident / Defect / Performance Response]
├─ Minor defect → Backlog / planned remediation
├─ Major defect → Prioritized fix → Implementation / Tests
├─ Critical incident → Incident response / mitigation / rollback
├─ Security incident → Security incident process → Security / Architecture / Implementation
├─ Reliability failure → Rollback / failover → Reliability / Architecture / Ops
└─ Architectural systemic issue → Architecture Review → Strategic impact analysis
↓
Post-Incident / Defect Analysis
→ Engineering response
→ Product response
→ Business response
as appropriate


[PHASE 17 — RETENTION / EXPANSION / REVENUE OPERATIONS]

Retention
↓
Lifecycle / Retention Marketing
↓
Customer Health Monitoring
↓
Expansion
↓
Renewal / Repeat Purchase
↓
Customer / support / sales evidence → Common Evidence Layer


[PHASE 18 — PRODUCT + ENGINEERING + BUSINESS ANALYTICS]

[PARALLEL EVIDENCE LAYER]
├─ Product Analytics
├─ Engineering Analytics
├─ Reliability Analytics
├─ Operational Analytics
├─ Commercial Analytics
├─ Marketing Analytics
├─ Sales Analytics
└─ Financial Analytics
↓
Common Evidence Layer
↓
ROI / LTV / CAC / Margin Analysis
↓
Actual vs. Forecast
↓
Technical Cost / Reliability / Delivery Analysis
↓
[DECISION GATE — Product / Commercial Optimization]
├─ Local product issue → Product Optimization
├─ Local engineering issue → Engineering Optimization
├─ Acquisition issue → Marketing / Sales Motion
├─ Pricing / margin issue → Commercial Analysis
├─ Reliability issue → Reliability / Architecture
├─ Cost issue → Architecture / Infrastructure / Commercial
├─ Material technical risk → Strategic Re-Scoring
└─ Healthy → Maintain / Scale


[PHASE 19 — CONTINUOUS OPTIMIZATION]

[PARALLEL]
├─ Product Optimization
├─ Creative / Media Optimization
├─ Conversion Optimization
├─ Sales Optimization
├─ Lifecycle Optimization
├─ Performance Optimization
├─ Reliability Improvement
├─ Security Remediation
├─ Infrastructure / Cost Optimization
└─ Engineering Process Improvement
↓
Change Impact Analysis
├─ Requirements?
├─ Market / audience?
├─ Pricing?
├─ Architecture / dependency?
├─ Compliance / security?
├─ Launch timing?
├─ Infrastructure?
├─ Sales motion?
└─ Commercial assumptions?
↓
[TRIGGER] If material:
→ identify affected stages
→ invalidate affected evidence
→ increment requirements/design version
→ re-run only affected stages
→ re-approve affected gates


[PHASE 20 — ARCHITECTURE / TECHNICAL DEBT / PRODUCT HEALTH]

Technical Debt / Architecture Health Review
├─ Maintainability / complexity
├─ Deprecated components
├─ Reliability / security risk
├─ Performance / scalability
├─ Testability / dependency health
├─ Infrastructure cost
├─ Developer productivity
├─ Observability gaps
├─ Data architecture health
└─ Operational burden
↓
[DECISION GATE — Architecture / Technical Health]
├─ Accept debt
├─ Schedule remediation
├─ Refactor
├─ Re-platform
├─ Replace component
├─ Re-architect
├─ Accelerate migration
├─ Reduce feature investment
└─ [ESCALATION] Strategic technical risk


[PHASE 21 — STRATEGIC RE-SCORING / PORTFOLIO RE-EVALUATION]

[TRIGGER] Material change in market, PMF, engineering effort/duration,
delivery confidence, architecture complexity, infrastructure cost,
security/compliance burden, reliability, scalability, maintenance,
unit economics, revenue/retention, or strategic fit
↓
Return to earliest invalidated strategic stage
↓
Re-run affected downstream validation
↓
Cross-Domain Validation
↓
Composite Re-Scoring
↓
Portfolio Re-Comparison
↓
[DECISION GATE — Strategic Re-Scoring / Portfolio Re-Evaluation]
├─ Scale
├─ Maintain
├─ Optimize
├─ Rebuild / Re-platform
├─ Reposition
├─ Reprice
├─ Reduce investment
├─ Pivot
├─ Pause
└─ Sunset


[PHASE 22 — PORTFOLIO ACTION]

Scale / Maintain / Optimize / Rebuild / Re-platform / Reposition /
Reprice / Reduce / Pivot / Pause / Sunset
↓
[FEEDBACK LOOP]
Product + Engineering + Customer + Revenue + Market learning
→ Signal Collection
→ Product evolution / future opportunity discovery
```

---

# 3. Lifecycle Phase Model

| Phase | Entry Criteria | Required Inputs | Primary Activities | Expected Outputs / Evidence | Exit Criteria | Gate / Outcomes | Re-entry Triggers |
|---|---|---|---|---|---|---|---|
| 1. Signal & Opportunity Discovery | A credible signal exists | Source evidence | Classify, deduplicate, frame problem | Opportunity record | Valid problem candidate | Proceed / watchlist / reject | New evidence |
| 2. Problem / Market Validation | Problem hypothesis | Exploratory research | Validate problem, market, competition, audience | Validated opportunity | Viability understood | Proceed / pivot / defer / reject | Market/PMF contradiction |
| 3. Solution & Commercial Validation | Valid opportunity | Market/customer evidence | Solution, PMM, commercial, sales design, early engineering | Candidate product + business + technical hypothesis | Plausible product/business/technical path | Proceed / spike / re-scope / reject | Technical/commercial contradiction |
| 4. Preliminary Technical / Risk Validation | Candidate solution | Feasibility, risk, GTM inputs | Risk, GTM, forecasting, cross-domain validation | Investment case | Investment-ready evidence | Proceed / remediate / defer / reject | Dependency/risk change |
| 5. Portfolio & Investment Decision | Cross-domain evidence | Score + resource data | Score, compare, govern investment | Formal decision | Approved/conditional/deferred/rejected | Investment Decision | Material assumption change |
| 6. Product Definition | Investment approved | Execution research | Detailed product scope, PMM, GTM, forecast | Versioned product definition | Build intent precise | Proceed / re-scope | Market/audience/price change |
| 7. Engineering Requirements & Architecture | Product baseline | Product/risk/business requirements | Decompose requirements, NFRs, feasibility, architecture | Requirements + architecture baseline | Design ready for planning | Requirements + Architecture gates | Requirement/dependency/architecture change |
| 8. Integrated Product / Engineering / GTM Planning | Architecture sufficiently stable | Scope, timing, resources | Engineering plan, NFR design, GTM/revenue planning | Integrated delivery plan | Delivery confidence acceptable | Proceed / reduce scope / delay / redesign | Capacity/timing/risk change |
| 9. Implementation & Continuous Verification | Plan + environments ready | Requirements + architecture | Implement, review, automate, integrate | Validated increments | Integrated candidate ready | Pass / root-cause rework | Any defect |
| 10. System / Security / Reliability Validation | Integrated candidate | Functional + NFR requirements | System/E2E/regression/NFR tests | Validation evidence | Required thresholds met | Pass / remediate / redesign | Test failure |
| 11. Pre-Production Validation | Candidate passed lower layers | Production-like environment | Full workflow, migration, ops, rollback validation | Pre-prod evidence | Production-like criteria met | Pass / exception / hold | Environment/ops mismatch |
| 12. Release & GTM Readiness | Technical/business prep mature | Release + GTM evidence | Engineering, GTM, integrated readiness | Launch decision | Approved launch mode | Ready / staged / remediate / delay / stop | New risk or readiness failure |
| 13. Progressive Deployment | Launch approved | Release artifact + controls | Canary, observe, expand | Deployment evidence | Target rollout achieved | Expand / hold / rollback | Degradation |
| 14. Production Verification | Production exposure | Telemetry + customer paths | Validate real health | Production health evidence | Stable or rolled back | Continue / hold / incident | Health failure |
| 15. Demand / Sales / Activation | Commercial availability | GTM + live product | Demand, sales, conversion, onboarding, activation | Active customers | First value achieved | Existing revenue gates | Low activation / sales/product evidence |
| 16. Production Operations & Observability | Production exists | Telemetry | Monitor, classify, respond | Incidents/defects/operational evidence | Continuous | Minor/major/critical/security/reliability/architecture | Any anomaly |
| 17. Retention / Expansion / Revenue Ops | Activated customers | Usage + customer/revenue data | Retain, expand, renew | Retention/LTV evidence | Continuous | Maintain / intervene / expand / churn | Churn/support/sales signals |
| 18. Product + Engineering + Business Analytics | Live data exists | Multi-domain analytics | Converge evidence | Common evidence layer | Actionable insight | Local optimize / strategic review | Trend deterioration |
| 19. Continuous Optimization | Improvement opportunity | Common evidence | Product/engineering/commercial optimization | Validated improvements | Adopted or escalated | Adopt / iterate / strategic trigger | Material change |
| 20. Architecture / Technical Debt / Product Health | Scheduled or trigger | Technical-health evidence | Review debt/architecture/cost/operability | Health decision | Disposition assigned | Accept / remediate / refactor / re-platform / re-architect | Risk/cost/velocity deterioration |
| 21. Strategic Re-Scoring / Portfolio Re-Evaluation | Material trigger | Updated strategic + technical evidence | Revalidate, score, compare | New portfolio decision | Resource action selected | Scale / maintain / rebuild / reduce / pivot / sunset | Future material evidence |
| 22. Portfolio Action | Strategic decision | Portfolio decision | Reallocate resources | New operating state | Action executed | Multiple actions | New signal |

---

# 4. Stage-by-Stage Operating Specification

The table below covers the major unified stages; sub-tests and sub-workstreams inherit the same traceability and re-entry rules.

| Stage | Purpose | Phase | Primary Inputs | Core Activities | Primary Outputs | Entry Criteria | Exit Criteria | Decision Gate | Options | Sequential Dependencies | Parallel Dependencies | Downstream Consumers | Re-entry Triggers | Evidence Generated | Classification |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Signal Collection / Classification | Capture and route opportunities | 1 | Market/customer/product/engineering signals | Normalize, source, dedupe, classify | Opportunity record | Signal exists | Candidate routed | Signal classification | Proceed/merge/watchlist/reject | None | None | Problem Discovery | New evidence | Provenance/confidence | Continuous |
| Problem Discovery | Define unmet need | 1 | Classified signal | Problem framing/JTBD | Problem hypothesis | Candidate exists | Coherent problem | Problem Validation | Proceed/reframe/reject | Classification | Research | Validation | PMF contradiction | Problem evidence | Pre-investment |
| Exploratory Market / Consumer Research | Test early evidence | 1–2 | Problem | Market/category/customer research | Demand + customer evidence | Problem framed | Sufficient evidence | Opportunity viability | Proceed/more evidence/defer | Problem Discovery | Audience Discovery | Market Analysis | Market shift | Research confidence | Pre-investment |
| Audience Discovery / Early Segmentation | Identify who has problem | 2 | Research | Discover/segment/prioritize | Candidate segments | Customer evidence | Actionable audience | Opportunity viability | Proceed/pivot/refine | Research | Market/Competition | Commercial/GTM | Lead quality/churn | Segment evidence | Repeated |
| Problem / Market / Competitive Validation | Establish opportunity attractiveness | 2 | Research + audience | Validate need, size, timing, competition | Validated opportunity | Evidence sufficient | Viability known | Opportunity / Commercial Viability | Proceed/pivot/defer/reject | Research | — | Solution Discovery | Market/competitor shift | Validation evidence | Pre-investment |
| Solution Discovery | Define product solution | 3 | Validated problem | Concepts/scope/tradeoffs | Candidate solution | Opportunity viable | Plausible solution | Solution viability | Proceed/prototype/pivot | Validation | Early Engineering | PMM/Commercial | Low activation/infeasibility | Solution rationale | Pre-investment |
| Preliminary Product Marketing | Test sellability | 3 | Solution + competition | Value prop/differentiation | Positioning hypothesis | Candidate solution | Communicable differentiation | Commercial Viability | Proceed/reposition/test | Solution | Commercial | GTM/Sales | Objections | Message evidence | Pre-investment |
| Commercial Analysis | Test economics | 3 | Solution/market/price evidence | Monetization/pricing/packaging/margin | Commercial model | Candidate solution | Viable economics | Commercial Viability | Proceed/reprice/repackage/reject | Solution | Preliminary Engineering | Forecast/Portfolio | Cost/discount/LTV changes | Unit-economics model | Repeated |
| Preliminary Sales-System Design | Test buyer-to-revenue path | 3 | Audience/product/commercial | Motion/journey/routing assumptions | Sales feasibility | Commercial model | Credible revenue path | Commercial Viability | Proceed/redesign/test | Commercial | Preliminary Engineering | GTM | High sales cost/low win | Sales feasibility | Pre-investment |
| Preliminary Technical Feasibility | Test plausibility before investment | 3–4 | Product concept | Architecture exploration, effort/duration, dependency/cost/risk analysis | Feasibility evidence | Candidate solution | Technical burden understood | Preliminary Technical Feasibility | Feasible/conditional/spike/re-scope/reject | Solution | Commercial/Risk | Forecast/Scoring | Scope/dependency/cost change | Effort/duration/risk/cost/confidence | Pre-investment |
| Risk / Legal / Security / Compliance | Establish constraints | 4 | Product/technical/commercial context | Risk/compliance assessment | Controls/blockers | Context sufficient | Risk disposition known | Investment Readiness | Proceed/remediate/reject/escalate | Feasibility | GTM | Investment/Architecture | Regulatory/scope change | Risk register | Repeated |
| GTM Feasibility | Test market-entry plausibility | 4 | Audience/PMM/sales/technical | Channel/timing/acquisition/sales analysis | GTM assessment | Product path credible | Route to market credible | Investment Readiness | Proceed/pivot/experiment | Commercial/Sales | Risk | Forecasting | CAC/channel changes | GTM evidence | Pre-investment |
| Preliminary Forecasting | Quantify investment case | 4 | Commercial/GTM/engineering/risk | Revenue/cost/timing scenarios | Forecast | Inputs mature enough | Forecast usable | Investment Readiness | Proceed/revise/defer | Feasibility | Cross-domain | Scoring | Forecast error | Scenario model | Pre-investment |
| Cross-Domain Validation | Detect contradictions | 4/21 | Domain evidence | Challenge consistency | Readiness result | Domain analyses available | Conflicts resolved/accepted | Investment Readiness | Proceed/remediate/escalate | Forecast | None | Scoring | Any material change | Conflict register | Repeated |
| Composite Scoring / Portfolio Comparison | Allocate priority | 5/21 | Validated evidence/resources | Score/rank/opportunity cost | Portfolio rank | Comparable evidence | Rank established | Investment Decision | Approve/defer/watchlist/reject | Cross-domain | Capacity planning | Investment | Material evidence | Score/rank | Repeated |
| Investment Decision | Commit resources | 5 | Rank/readiness/forecast | Governance | Formal decision | Evidence threshold met | Decision recorded | Investment Decision | Approve/conditional/remediate/defer/reject | Portfolio | Governance | Product Definition | Assumption change | Decision record | Pre-investment |
| Detailed Product Definition | Convert concept to buildable intent | 6 | Approved opportunity/research | Scope/journeys/functional/UX/data/accessibility/acceptance | Versioned product requirements | Investment approved | Ready for engineering intake | Product Definition Readiness | Proceed/refine/re-scope | Investment | GTM/PMM | Engineering Intake | Market/audience/pricing changes | PRD/acceptance criteria | Pre-launch |
| Engineering Intake / Requirements Decomposition | Translate product intent to technical requirements | 7 | Product/business/regulatory requirements | Functional/NFR/integration/data/infra/ops/release decomposition | Versioned engineering requirements | Product baseline exists | Requirements testable/traceable | Requirements Readiness | Ready/conditional/clarify/return/escalate | Product Definition | Early Architecture | Design/Planning/Test | Ambiguity/change | Requirements baseline | Pre-launch |
| Execution-Grade Technical Feasibility | Validate detailed delivery feasibility | 7 | Detailed requirements | Refine estimates/dependencies/platform/env/ops | Delivery feasibility | Requirements sufficiently clear | Confidence acceptable | Architecture/Plan gates | Proceed/spike/re-scope/resolve dependency | Requirements | Architecture | Planning/Forecasting | Dependency/architecture change | Refined estimates/confidence | Pre-launch |
| Architecture & System Design | Define governed technical solution | 7 | Requirements/feasibility | System/app/data/integration/API/infra/security/reliability/observability/deployment/DR design | Architecture baseline | Requirements ready | Architecture approved | Architecture / Technical Design | Approve/conditional/simplify/redesign/spike/re-scope | Requirements | Product refinement | Planning/Implementation/Test | Performance/security/integration failure | Architecture decisions | Repeated |
| Security / Privacy / Reliability Design | Define NFR controls | 8 | Architecture/risk/NFRs | Controls/SLOs/resilience/privacy/recovery | Control design | Architecture sufficiently formed | Controls actionable | NFR Design Gate | Approve/control/rework/change architecture/escalate | Architecture | Planning | Implementation/Validation | Security/reliability finding | Control evidence | Pre-launch/continuous |
| Engineering Planning | Make delivery executable | 8 | Scope/architecture/timing/resources | Work breakdown/sequence/estimate/milestones/env/test/release/rollback | Delivery plan | Architecture adequate | Confidence threshold met | Engineering Plan / Delivery Confidence | Proceed/conditional/resequence/add resources/reduce scope/delay | Architecture | GTM/Forecasting | Implementation | Velocity/dependency/timing change | Plan/confidence | Repeated |
| Environment Strategy / Readiness | Provide fit environments | 8–13 | Architecture/test/release plan | Provision/isolate/configure environments | Ready environments | Specs approved | Required environment usable | Environment readiness | Ready/remediate/block | Planning | Infrastructure automation | Build/Test/Release | Drift/failure | Environment evidence | Continuous |
| Implementation / Code Review | Build and review increments | 9 | Requirements/architecture/plan | Code/config/data/infra changes + peer review | Reviewed increments | Work item ready | Review/test-ready | Implementation Quality | Continue/rework/escalate | Planning | Test automation/infra/instrumentation | Automated Validation | Code/design finding | Build/review artifacts | Continuous |
| Automated / Integration / Contract Validation | Fast quality and interface validation | 9 | Reviewed increments | Static/lint/type/unit/component/integration/API/contract tests | CI/integration evidence | Build available | Checks pass | Implementation / Integration Quality | Pass/return to root-cause stage | Implementation | Continued feature work | System Testing | Requirement/architecture/code/test defect | Test evidence | Continuous |
| System / E2E / Regression Testing | Validate complete behavior | 10 | Integrated candidate | Full-system/user/business-path/regression tests | Functional evidence | Integration stable | Acceptance met | System / NFR Validation | Pass/remediate | Integration | NFR validation | Pre-Production | Product mismatch | System evidence | Pre-launch |
| Performance / Scalability / Reliability Validation | Validate operating limits/failure behavior | 10 | Candidate + NFRs | Performance/load/capacity/resilience/failure testing | NFR evidence | Candidate stable | Thresholds met | System / NFR Validation | Pass/architecture/infra/code remediation | System build | Security/privacy/accessibility | Release | Latency/saturation/failure | Benchmarks/resilience | Repeated |
| Security / Privacy / Accessibility / Compliance Validation | Verify controls | 10 | Candidate + control requirements | Security/privacy/accessibility/compliance testing | Assurance evidence | Controls implemented | Required findings resolved/accepted | System / NFR Validation | Pass/remediate/escalate | NFR design | Performance/reliability | Release | Findings/incidents | Assurance evidence | Repeated |
| Pre-Production Validation | Validate production-like release | 11 | Candidate/staging | Full workflows/migrations/ops/observability/rollback | Pre-prod package | Lower layers passed | Production-like criteria met | Pre-Production Validation | Pass/exception/remediate/hold | Validation | GTM prep | Release Readiness | Env/ops mismatch | Validation package | Pre-launch |
| Engineering Release Readiness | Decide technical releasability | 12 | Full technical evidence | Release review | Technical go/no-go | Pre-prod evidence exists | Ready/limited/hold | Engineering Release Readiness | Ready/exception/limited/remediate/delay/reject | Pre-Prod | GTM readiness | Integrated Gate | New defect/risk | Release evidence package | Pre-launch |
| GTM / Revenue Readiness | Decide business launch readiness | 12 | Product/marketing/sales/support/revenue evidence | GTM review | Business go/no-go | Launch workstreams mature | Ready/limited/hold | GTM Readiness | Ready/limited/remediate/timing/delay | GTM work | Engineering readiness | Integrated Gate | Product/market change | GTM evidence | Pre-launch |
| Integrated Launch Readiness | Decide system launch | 12 | Technical + business + risk + ops evidence | Cross-functional challenge | Launch mode | Both readiness streams available | Approved launch mode | Integrated Launch Readiness | Ready/exception/staged/remediate/delay/stop | Both readiness gates | None | Deployment | Cross-functional blocker | Integrated evidence | Launch |
| Progressive Deployment | Release safely in stages | 13 | Approved artifact | Controlled deployment/canary/observe/expand | Deployment evidence | Launch approved | Target rollout reached | Deployment Expansion | Expand/hold/remediate/rollback | Integrated Gate | Monitoring | Production Verification | Degradation | Deployment health | Launch |
| Production Verification | Verify real behavior | 14 | Deployed system | App/API/data/payment/security/analytics health checks | Production result | Exposure exists | Stable or rolled back | Production Health | Continue/hold/rollback/incident | Deployment | Observability | Ops/Demand | Health failure | Production evidence | Launch/post-launch |
| Demand / Sales / Activation | Create and activate customers | 15 | Live product + GTM | Demand/sales/conversion/provision/onboard/activate | Active customers | Commercial launch | First value | Existing revenue gates | Motion-specific outcomes | Launch | Production Ops | Low activation/sales feedback | Customer/revenue evidence | Post-launch |
| Observability / Monitoring | Make production knowable | 16 | Live systems | Logs/metrics/traces/SLO/business/UX monitoring | Telemetry/alerts | Production exists | Continuous | Production Health | Healthy/investigate | Deployment | Revenue monitoring | Incident/Analytics | Anomaly | Telemetry | Continuous |
| Incident / Defect / Performance Analysis | Correct production issues | 16 | Alerts/support/telemetry | Severity/RCA/containment/prevention | Remediation plan | Signal detected | Impact controlled/root cause addressed | Incident Response | backlog/fix/incident/security/architecture review | Monitoring | Product/Business response | Implementation/Architecture/Portfolio | Repeat/systemic issue | RCA evidence | Continuous |
| Product & Engineering Analytics | Measure product + technical behavior | 18 | Usage/delivery/quality data | Adoption/journey/defect/velocity/change-failure analysis | Common evidence | Data exists | Actionable insight | Optimization Gate | Optimize/strategic review | Production | Commercial/Reliability analytics | Product/Planning | Trend deterioration | Analytics evidence | Continuous |
| Technical Debt / Architecture Health Review | Govern long-term technical health | 20 | Architecture/incidents/delivery/cost | Review complexity/dependencies/cost/operability | Health decision | Scheduled/triggered | Disposition assigned | Architecture / Technical Health | Accept/remediate/refactor/re-platform/re-architect/escalate | Analytics | Product roadmap | Planning/Portfolio | Cost/risk/velocity deterioration | Health score/risk | Continuous |
| Continuous Improvement | Improve whole system | 19 | Common evidence | Product/technical/reliability/process/cost optimization | Validated improvements | Opportunity exists | Improvement adopted/escalated | Product / Commercial Optimization | Adopt/iterate/escalate | Analytics | Parallel optimization | Planning/Product/Portfolio | Material assumption change | Experiment evidence | Continuous |
| Strategic Re-Scoring / Portfolio Re-Evaluation | Reassess investment | 21 | Updated strategic/technical evidence | Revalidate/re-score/re-compare | New portfolio decision | Material trigger | Resource decision | Strategic Re-Scoring | Scale/maintain/rebuild/reposition/reduce/pivot/pause/sunset | Cross-domain revalidation | Technical health | Portfolio Action | Future material evidence | Revised score/decision | Governance |

---

# 5. Engineering Lifecycle Detail

## Three Levels of Technical Feasibility

### Preliminary Technical Feasibility — Pre-Investment
Determines whether the product is technically plausible and whether likely engineering effort, build duration, dependency risk, infrastructure cost, security burden, scalability limits, reliability burden, and maintenance cost materially alter the business case.

### Execution-Grade Technical Feasibility — Post-Investment
Validates feasibility against detailed, versioned requirements and refines architecture choices, estimates, dependencies, platform/infrastructure needs, environment strategy, operational model, NFR feasibility, release strategy, and delivery confidence.

### Implementation Feasibility / Delivery-Risk Validation — During Execution
Uses real integration, test, performance, security, reliability, environment, migration, and velocity evidence to update delivery risk continuously.

## Requirements Chain

```text
Product Strategy
→ Product Requirements
→ Non-Functional Requirements
→ Engineering Requirements
→ Architecture
→ Implementation
→ Validation
```

Every material requirement should have a unique identifier, version, source, owner, rationale, verification method, upstream dependency, and downstream affected artifacts.

## Architecture Governance

Architecture is governed across system, application, data, integration, API/schema, infrastructure/hosting, security/privacy, reliability, observability, deployment, and disaster recovery. Material decisions should be traceable through architecture decision records or equivalent evidence.

## Engineering Planning

Engineering Planning consumes product scope, launch timing, architecture, dependencies, staffing, infrastructure, technical risk, security requirements, regulatory constraints, and commercial priorities. It outputs decomposition, sequencing, estimates, milestones, resources, test strategy, environment strategy, release strategy, rollback strategy, contingency plans, and delivery confidence.

## Iterative Development Rule

```text
Implementation
↓
Code Review
↓
Automated Validation
↓
Integration / Contract Validation
↓
Defect?
├─ No → Continue
└─ Yes
   ├─ Requirement defect → Requirements
   ├─ Architecture defect → Architecture
   ├─ Security defect → Security Design
   ├─ Reliability defect → Reliability Design
   ├─ Dependency defect → Planning / Architecture
   ├─ Code defect → Implementation
   ├─ Test defect → Test Strategy
   └─ Product mismatch → Product Definition
```

## Testing Layers

1. Static analysis
2. Linting
3. Type checking
4. Unit testing
5. Automated component testing
6. Integration testing
7. API / contract testing
8. System testing
9. End-to-end testing
10. Regression testing
11. Performance testing
12. Load / scalability testing
13. Reliability / resilience testing
14. Security testing
15. Privacy validation
16. Accessibility validation
17. Compliance validation
18. Production-like pre-production validation
19. User/business acceptance where appropriate

## Environment Strategy

```text
Local / Development
→ Test
→ Integration
→ Staging / Pre-Production
→ Production-Like Validation
→ Controlled Release / Canary
→ Production
```

Environment readiness is a blocking dependency for the corresponding validation layer.

---

# 6. Product–Engineering Interaction Model

| Product Responsibility | Engineering Responsibility | Shared Interaction |
|---|---|---|
| Define customer problem | Assess technical implications | Problem/feasibility challenge |
| Define customer outcome | Define technical realization | Solution shaping |
| Define product scope | Define engineering scope | Scope tradeoffs |
| Define product requirements | Decompose into engineering requirements | Requirements traceability |
| Define product acceptance criteria | Define technical verification criteria | Acceptance mapping |
| Prioritize roadmap | Sequence engineering plan | Integrated planning |
| Own product-value decisions | Own technical-design decisions | Cross-domain tradeoffs |
| Interpret customer behavior | Interpret technical behavior | Common evidence layer |
| Optimize product experience | Optimize performance/reliability/cost | Joint impact analysis |
| Define product evolution | Evolve architecture | Product–architecture co-evolution |
| Change pricing/GTM | Assess implementation/operational impact | Revalidation |
| Define launch objective | Define release safety | Integrated Launch Readiness |

---

# 7. Release / Deployment / Production Model

## Engineering Release Readiness
Requires functional acceptance, automated/integration/system/NFR results, security/privacy/compliance evidence, environment and migration readiness, observability, runbooks, rollback/failover evidence, known-issue disposition, and reproducible release artifacts.

## Business / GTM Readiness
Requires product acceptance, valid launch timing, campaign/sales readiness, pricing/packaging, contracts/checkout/payment, provisioning/onboarding, support/customer success, analytics/attribution.

## Integrated Launch Readiness
Consumes both readiness streams plus Product, Security, Reliability, Legal/Compliance, Operations, Analytics, and Support evidence.

Possible outcomes: Ready; Ready with controlled exceptions; Limited/staged launch; Remediation required; Delay; Return to earlier stage; Stop/reject release.

## Progressive Delivery

```text
Approved Build
↓
Controlled Environment
↓
Verification
↓
Canary / Pilot
↓
Observe
↓
[Deployment Expansion Gate]
├─ Healthy → Expand
├─ Degraded → Pause / Remediate
└─ Critical → Rollback / Failover
↓
Production Verification
↓
Controlled expansion / Full rollout
```

Release safety mechanisms include feature flags, canaries, percentage rollouts, blue/green where appropriate, rollback, failover, health checks, and reproducible artifacts.

---

# 8. Decision-Gate Matrix

| Decision Gate | Required Evidence | Decision Options | Default Path | Rework Destination | Escalation Conditions |
|---|---|---|---|---|---|
| Problem Validation | Problem/customer evidence | Proceed / evidence / pivot / defer / reject | Proceed | Problem/Research/Audience | Conflicting high-impact evidence |
| Opportunity / Commercial Viability | Market/competition/audience/economics | Proceed / rework / pivot / defer / reject | Proceed | Market/Product/Commercial | Major uncertainty |
| Preliminary Technical Feasibility | Plausibility/effort/duration/dependencies/cost/risk | Feasible / conditional / spike / re-scope / change tech / reject | Feasible | Solution/Architecture Exploration | Critical unknown |
| Investment Readiness | Cross-domain evidence | Proceed / remediate / evidence / defer / reject | Proceed | Failed domain | Cross-domain conflict |
| Investment Decision | Score/rank/risk/forecast | Approve / conditional / remediate / prototype / defer / watchlist / reject | Approve if thresholds met | Earliest invalidated stage | Policy exception / large commitment |
| Requirements Readiness | Product + engineering requirements/NFRs | Ready / conditional / clarify / return / escalate | Ready | Product Definition / Requirements | Material conflict |
| Architecture / Technical Design | Architecture/dependency/NFR/cost/risk evidence | Approve / conditional / simplify / redesign / spike / re-scope | Approve | Architecture / Product | High-risk disagreement |
| Engineering Plan / Delivery Confidence | Scope/estimates/resources/timing/dependencies | Proceed / conditional / resequence / add resources / reduce scope / delay | Proceed | Planning/Product/GTM | Confidence below threshold |
| Security / Privacy / Reliability Design | Controls/threat/privacy/SLO evidence | Approve / controls / rework / architecture change / reduce scope | Approve | NFR Design | High/critical unresolved risk |
| Implementation / Integration Quality | Review/automation/integration/contract evidence | Pass / root-cause rework | Pass | Earliest failed stage | Repeated systemic failure |
| System / NFR Validation | System/E2E/regression/performance/security/etc. | Pass / remediate / redesign / re-scope | Pass | Earliest failed stage | Critical NFR failure |
| Pre-Production Validation | Production-like workflow/migration/obs/rollback | Pass / exception / remediate / hold | Pass | Failed technical/ops domain | Uncontrolled release risk |
| Engineering Release Readiness | Release evidence package | Ready / exception / limited / remediate / delay / reject | Ready | Engineering stage | Critical known issue |
| GTM / Revenue Readiness | Product/campaign/sales/support/revenue evidence | Ready / limited / remediate / timing / delay | Ready | GTM domain | Major business gap |
| Integrated Launch Readiness | Engineering + GTM + Product + risk + ops | Ready / exception / staged / remediate / delay / stop | Ready | Earliest failed domain | Cross-functional high risk |
| Deployment Expansion | Canary/SLO/error/business signals | Expand / hold / remediate / rollback | Expand | Release/Implementation/Incident | Critical degradation |
| Production Health | Production telemetry/customer verification | Continue / hold / remediate / rollback / incident | Continue | Incident/Architecture/Product | Critical impact |
| Product / Commercial Optimization | Product/technical/customer/revenue evidence | Maintain / optimize / local rework / strategic review | Optimize locally | Relevant domain | Material strategic impact |
| Architecture / Technical Health | Debt/maintainability/cost/risk/velocity | Accept / remediate / refactor / re-platform / re-architect / escalate | Risk-based | Architecture/Planning | Strategic technical risk |
| Strategic Re-Scoring / Portfolio | Updated product/commercial/technical evidence | Scale / maintain / optimize / rebuild / reposition / reduce / pivot / pause / sunset | Maintain/scale viable products | Earliest strategic stage | Sunset / major capital shift |

---

# 9. Source-Stage Integration Matrix

| Original Workflow | Original Stage | Unified Stage | Lifecycle Phase | Sequential / Parallel / Conditional | Repeated? | Pre- or Post-Investment | Reason for Placement |
|---|---|---|---|---|---|---|---|
| Product/Marketing/Growth/Sales | Signal Collection / Idea Submission | Signal Collection | 1 | Sequential | Yes | Both | Common signal entry |
| Product/Marketing/Growth/Sales | Signal Classification | Signal Classification | 1 | Sequential | Yes | Both | Routes signals |
| Product/Marketing/Growth/Sales | Problem Discovery | Problem Discovery | 1 | Sequential | Yes | Both | Defines need |
| Product/Marketing/Growth/Sales | Exploratory Market Research | Exploratory Market Research | 1–2 | Parallel | Yes | Pre | Early evidence |
| Product/Marketing/Growth/Sales | Consumer Insights | Consumer Insights | 1–2 / 6 | Repeated depth | Yes | Both | Validation and execution |
| Product/Marketing/Growth/Sales | Audience Discovery | Audience Discovery / Segmentation | 2 | Sequential | Yes | Both | Identifies customers |
| Product/Marketing/Growth/Sales | Problem Validation | Problem Validation | 2 | Sequential | Yes | Pre | Proves importance |
| Product/Marketing/Growth/Sales | Market Analysis | Market Analysis | 2 | Sequential | Yes | Both | Determines attractiveness |
| Product/Marketing/Growth/Sales | Competitive Analysis | Competitive Analysis | 2 | Parallel | Yes | Both | Defines alternatives/whitespace |
| Product/Marketing/Growth/Sales | Solution Discovery | Solution Discovery | 3 | Sequential | Yes | Both | Defines product concept |
| Product/Marketing/Growth/Sales | Preliminary Product Marketing | Preliminary PMM | 3 | Parallel | Yes | Pre | Tests sellability |
| Product/Marketing/Growth/Sales | Commercial Analysis | Commercial Analysis | 3 | Parallel | Yes | Both | Tests economics |
| Product/Marketing/Growth/Sales | Preliminary Sales-System Design | Preliminary Sales-System Design | 3 | Parallel | Yes | Pre | Tests revenue path |
| Product/Marketing/Growth/Sales | Technical Feasibility | Multi-level Technical Feasibility | 3–9 | Repeated at depth | Yes | Both | Progressive technical evidence |
| Product/Marketing/Growth/Sales | Risk / Legal / Security / Compliance | Risk / Legal / Security / Compliance | 4 | Parallel | Yes | Both | Governing constraints |
| Product/Marketing/Growth/Sales | GTM Feasibility | GTM Feasibility | 4 | Sequential | Yes | Pre | Route-to-market |
| Product/Marketing/Growth/Sales | Preliminary Forecasting | Preliminary Forecasting | 4 | Sequential | Yes | Pre | Investment economics |
| Product/Marketing/Growth/Sales | Cross-Domain Validation | Cross-Domain Validation | 4/21 | Sequential | Yes | Both | Contradiction detection |
| Product/Marketing/Growth/Sales | Composite Scoring | Composite Scoring | 5/21 | Sequential | Yes | Both | Comparable score |
| Product/Marketing/Growth/Sales | Portfolio Comparison | Portfolio Comparison | 5/21 | Sequential | Yes | Both | Resource allocation |
| Product/Marketing/Growth/Sales | Investment Decision | Investment Decision | 5 | Sequential | Yes | Pre | Authorizes execution |
| Product/Marketing/Growth/Sales | Execution-Grade Market Research | Execution-Grade Market Research | 6 | Parallel | Yes | Post | Refines execution |
| Product/Marketing/Growth/Sales | Execution-Grade Consumer Insights | Execution-Grade Consumer Insights | 6 | Parallel | Yes | Post | Deep buyer evidence |
| Product/Marketing/Growth/Sales | Audience Segmentation | Execution-Grade Segmentation | 6 | Iterative | Yes | Post | Targeting/routing |
| Product/Marketing/Growth/Sales | Product Marketing | Product Marketing | 6 | Parallel | Yes | Post | Final value/messaging |
| Product/Marketing/Growth/Sales | Brand / Positioning | Brand / Positioning | 6 | Parallel | Yes | Post | Final positioning |
| Product/Marketing/Growth/Sales | Detailed GTM Strategy + Launch Timing | Detailed GTM + Launch Timing | 6/8 | Parallel with planning | Yes | Post | Integrates business and delivery |
| Product/Marketing/Growth/Sales | Execution-Grade Forecasting | Execution-Grade Forecasting | 6/8 | Iterative | Yes | Post | Updated by engineering |
| Product/Marketing/Growth/Sales | Revenue / Sales-System Design | Revenue / Sales-System Design | 8 | Parallel | Yes | Post | Built with engineering/GTM |
| Product/Marketing/Growth/Sales | Campaign Strategy | Campaign Strategy | 8 | Parallel | Yes | Post | Demand planning |
| Product/Marketing/Growth/Sales | Media Planning | Media Planning | 8 | Parallel | Yes | Post | Media execution |
| Product/Marketing/Growth/Sales | Creative Production + Sales Enablement + Revenue-System Configuration | Launch Readiness Workstreams | 8–12 | Parallel | Yes | Post | Runs beside implementation |
| Product/Marketing/Growth/Sales | GTM / Revenue Readiness | GTM / Revenue Readiness | 12 | Parallel | Yes | Post | Business go/no-go |
| Product/Marketing/Growth/Sales | Launch | Integrated Launch + Progressive Deployment | 12–14 | Conditional | Yes | Post | Technical + business governed |
| Product/Marketing/Growth/Sales | Demand Generation | Demand Generation | 15 | Continuous | Yes | Post | Creates opportunities |
| Product/Marketing/Growth/Sales | Demand / Lead Entry | Demand / Lead Entry | 15 | Sequential | Yes | Post | Live revenue entry |
| Product/Marketing/Growth/Sales | Visitor / Lead Identification | Identification | 15 | Sequential | Yes | Post | Supports routing |
| Product/Marketing/Growth/Sales | Qualification | Qualification | 15 | Conditional | Yes | Post | Decides path |
| Product/Marketing/Growth/Sales | Sales Motion Routing | Sales Motion Routing | 15 | Conditional | Yes | Post | Chooses buying motion |
| Product/Marketing/Growth/Sales | Self-Service | Self-Service branch | 15 | Conditional | Yes | Post | Automated purchase |
| Product/Marketing/Growth/Sales | Product-Led | Product-Led branch | 15 | Conditional | Yes | Post | Usage-led conversion |
| Product/Marketing/Growth/Sales | Sales-Assisted | Sales-Assisted branch | 15 | Conditional | Yes | Post | Complex/high-value sales |
| Product/Marketing/Growth/Sales | Outbound | Outbound branch | 15 | Conditional | Yes | Post | Proactive acquisition |
| Product/Marketing/Growth/Sales | Hybrid | Hybrid branch | 15 | Conditional | Yes | Post | Mixed motion |
| Product/Marketing/Growth/Sales | Need / Solution Matching | Need / Solution Matching | 15 | Sequential | Yes | Post | Confirms fit |
| Product/Marketing/Growth/Sales | Buyer Education / Value Development | Buyer Education | 15 | Conditional | Yes | Post | Builds confidence |
| Product/Marketing/Growth/Sales | Offer / Pricing / Commercial Terms | Commercial Execution | 15 | Conditional | Yes | Post | Applies pricing |
| Product/Marketing/Growth/Sales | Proposal / Negotiation | Proposal / Negotiation | 15 | Conditional | Yes | Post | Complex deals |
| Product/Marketing/Growth/Sales | Checkout / Contract | Checkout / Contract | 15 | Sequential | Yes | Post | Formalizes purchase |
| Product/Marketing/Growth/Sales | Payment / Conversion | Payment / Conversion | 15 | Sequential | Yes | Post | Realizes revenue |
| Product/Marketing/Growth/Sales | Account Provisioning | Account Provisioning | 15 | Sequential | Yes | Post | Enables service |
| Product/Marketing/Growth/Sales | Onboarding | Onboarding | 15 | Parallel | Yes | Post | Moves to value |
| Product/Marketing/Growth/Sales | Activation / First Value | Activation | 15 | Sequential | Yes | Post | Confirms value |
| Product/Marketing/Growth/Sales | Usage / Customer Health | Usage / Customer Health | 15–17 | Continuous | Yes | Post | Feeds evidence |
| Product/Marketing/Growth/Sales | Retention | Retention | 17 | Continuous | Yes | Post | Preserves value |
| Product/Marketing/Growth/Sales | Expansion | Expansion | 17 | Conditional | Yes | Post | Grows value |
| Product/Marketing/Growth/Sales | Renewal / Repeat Purchase | Renewal | 17 | Recurring | Yes | Post | Preserves revenue |
| Product/Marketing/Growth/Sales | Sales + Marketing + Product + Revenue Analytics | Common Evidence Layer | 18 | Parallel | Yes | Post | Converges with engineering/reliability |
| Product/Marketing/Growth/Sales | ROI / LTV / CAC / Margin Analysis | Commercial / Financial Analytics | 18 | Sequential | Yes | Post | Realized economics |
| Product/Marketing/Growth/Sales | Continuous Optimization | Continuous Optimization | 19 | Parallel | Yes | Post | Local improvements |
| Product/Marketing/Growth/Sales | Strategic Re-Scoring / Portfolio Re-Evaluation | Strategic Re-Scoring | 21 | Conditional | Yes | Post | Strategic governance |
| Product/Marketing/Growth/Sales | Scale / Maintain / Optimize / Expand / Reduce / Reposition / Reprice / Pivot / Pause / Sunset | Portfolio Action | 22 | Conditional | Yes | Post | Resource decision |
| Product/Marketing/Growth/Sales | Learning feeds back to earliest affected stage | Earliest Invalidated Assumption Rule | All | Conditional | Yes | Both | Precise re-entry |
| Engineering | Product Requirement / Engineering Signal | Signal Collection + Product Definition Input | 1/6 | Conditional | Yes | Both | Engineering signals may initiate work |
| Engineering | Engineering Intake | Engineering Intake | 7 | Sequential | Yes | Post | Formal technical intake |
| Engineering | Requirements Decomposition | Requirements Decomposition | 7 | Sequential | Yes | Post | Technical translation |
| Engineering | Technical Feasibility | Three-Level Technical Feasibility | 3–9 | Repeated | Yes | Both | Progressive confidence |
| Engineering | Architecture & System Design | Architecture & System Design | 7 | Parallel | Yes | Post | Governs technical solution |
| Engineering | Security / Privacy / Reliability Design | NFR Design | 8 | Parallel | Yes | Post | Controls before build/release |
| Engineering | Engineering Planning | Engineering Planning | 8 | Parallel with GTM | Yes | Post | Integrated delivery planning |
| Engineering | Implementation | Implementation | 9 | Iterative | Yes | Post | Builds increments |
| Engineering | Code Review | Code Review | 9 | Iterative | Yes | Post | Quality control |
| Engineering | Automated Testing | Automated Validation | 9 | Iterative | Yes | Post | Fast feedback |
| Engineering | Integration / Contract Testing | Integration / Contract Validation | 9 | Iterative | Yes | Post | Interface validation |
| Engineering | System / End-to-End Testing | System / E2E | 10 | Sequential | Yes | Post | Full behavior |
| Engineering | Performance / Reliability / Security Testing | Distinct NFR Workstreams | 10 | Parallel | Yes | Post | Preserves separate evidence |
| Engineering | Pre-Production Validation | Pre-Production Validation | 11 | Sequential | Yes | Post | Production-like evidence |
| Engineering | Release Readiness | Engineering Release Readiness | 12 | Parallel with GTM | Yes | Post | Technical go/no-go |
| Engineering | Progressive Deployment | Progressive Deployment | 13 | Conditional | Yes | Post | Controlled rollout |
| Engineering | Production Verification | Production Verification | 14 | Sequential | Yes | Post | Confirms live behavior |
| Engineering | Observability / Monitoring | Observability / Monitoring | 16 | Continuous | Yes | Post | Production telemetry |
| Engineering | Incident / Defect / Performance Analysis | Incident / Defect / Performance Analysis | 16 | Conditional | Yes | Post | Production response |
| Engineering | Product & Engineering Analytics | Product & Engineering Analytics | 18 | Parallel | Yes | Post | Common evidence |
| Engineering | Technical Debt / Architecture Health Review | Technical Debt / Architecture Health | 20 | Recurring | Yes | Post | Technical governance |
| Engineering | Continuous Improvement | Continuous Optimization | 19 | Continuous | Yes | Post | Improvement loop |
| Engineering | Feedback to Product Strategy / Architecture / Engineering Planning | Precise Engineering Re-Entry | All | Conditional | Yes | Both | Correct root cause |

---

# 10. Engineering Feedback Matrix

| Observed Engineering Signal | Likely Cause | Immediate Response | Earliest Stage Revisited | Business Impact Review Required? | Strategic Re-Scoring Required? |
|---|---|---|---|---|---|
| Requirement ambiguity | Incomplete requirement | Stop affected work, clarify | Requirements / Product Definition | If scope/timing changes | If material |
| Frequent code rework | Weak requirements/architecture/planning | Root-cause review | Requirements / Architecture / Planning | Yes if cost/timing affected | Maybe |
| Integration failure | Contract/schema/dependency design | Stabilize interface | API/Contract Design / Architecture | If external impact | Maybe |
| Repeated API breakage | Weak compatibility governance | Freeze/change contract policy | API/Contract Design | Yes | Maybe |
| Performance failure | Architecture/query/cache/capacity | Profile/contain | Architecture / Infrastructure / Implementation | Yes if UX/cost/scale | Yes if structural |
| Scalability limit | Capacity/architecture constraint | Limit rollout/model capacity | Architecture / Capacity / Forecasting | Yes | Yes if growth constrained |
| Security finding | Design/implementation weakness | Remediate/control | Security Design / Architecture / Implementation | High severity: yes | Material: yes |
| Privacy finding | Data design/requirement issue | Stop affected processing | Privacy Design / Product Requirements | Yes | If model affected |
| Reliability failure | Resilience/dependency/ops gap | Rollback/failover/remediate | Reliability / Architecture / Operations | Yes | If systemic |
| Deployment failure | Pipeline/env/migration/config issue | Pause/rollback | Release Engineering / Environment / Testing | Usually | If recurring |
| Production defect | Code/test/requirement gap | Contain/fix/regression | Implementation / Tests / Requirements | Depends | If systemic |
| High defect escape rate | Test/architecture/process weakness | Tighten controls | Test Strategy / Architecture / Planning | Yes | Maybe |
| Critical incident | System failure | Incident response | Root-cause stage | Yes | Often |
| Repeated incidents | Systemic architecture/operability issue | Architecture review | Architecture / Reliability | Yes | Yes |
| High latency | Performance/infra/code issue | Optimize/capacity action | Architecture / Infrastructure / Implementation | If conversion/retention impacted | Maybe |
| High infrastructure cost | Inefficient architecture/usage/vendor | Cost analysis | Architecture / Infrastructure / Commercial Analysis | Yes | If margin material |
| Dependency instability | Vendor/API instability | Mitigate/fallback | Architecture / Vendor Strategy / Planning | Yes | Maybe/Yes |
| Environment drift | Weak IaC/config governance | Reconcile | Environment Strategy / Release Engineering | Usually no | No |
| Slow engineering velocity | Debt/complexity/requirements/staffing | Delivery-health review | Technical Debt / Architecture / Planning | Yes | Maybe |
| High change failure rate | Weak testing/release strategy | Improve CI/CD validation | Test / Release / Planning | Yes if customer impact | Maybe |
| Long recovery time | Poor observability/runbooks/architecture | Improve detection/recovery | Observability / Reliability / Operations | Yes | Maybe |
| Low testability | Coupling/architecture | Refactor/redesign | Architecture / Technical Debt | If delivery affected | Maybe |
| Deprecated component | Lifecycle/dependency debt | Plan replacement | Technical Debt / Architecture | If risk/cost | Maybe |
| Security patch burden | Dependency choices | Dependency strategy review | Architecture / Technical Debt | Yes | Maybe |
| Observability gap | Missing telemetry design | Add instrumentation | Observability Architecture / Requirements | Usually no | No |
| Data integrity defect | Data architecture/transaction issue | Contain/repair | Data Architecture / Requirements | Yes | If material |
| Recovery failure | DR/recoverability design | Fix before rollout | Reliability / DR Design | Yes | Severe: yes |
| Churn tied to performance | Technical UX/reliability | Priority remediation | Architecture / Performance / Product | Yes | If material |
| High support volume from defects | Quality/usability/reliability | Root-cause backlog | Product / Implementation / Reliability | Yes | Maybe |
| Engineering cost above forecast | Underestimated complexity/scope | Reforecast/replan | Planning / Architecture / Commercial | Yes | Yes if economics change |
| Build duration above forecast | Scope/dependency/velocity | Replan timing/scope | Planning / Requirements / Architecture | Yes | Yes if launch/economics change |
| Technical risk rises materially | New evidence | Hold affected commitment | Relevant technical stage | Yes | Yes |
| Debt threatens roadmap | Architecture health deterioration | Rebalance roadmap | Technical Debt / Architecture / Portfolio | Yes | Yes |
| Re-platforming required | Architecture no longer fit | Build migration case | Architecture / Commercial / Portfolio | Yes | Yes |

---

# 11. Cross-Functional Dependency Matrix

| Stage | Depends On | Produces Inputs For | Can Run In Parallel With | Blocking Conditions |
|---|---|---|---|---|
| Problem Discovery | Signal Classification | Research / Validation | Initial technical reconnaissance | No coherent problem |
| Exploratory Research | Problem hypothesis | Market/Customer Analysis | Consumer/Audience research | Evidence unavailable |
| Solution Discovery | Validated problem/market | PMM/Commercial/Technical | Architecture exploration | Problem not validated |
| Commercial Analysis | Solution/audience | Forecast/Pricing/Portfolio | Preliminary Technical Feasibility | No viable monetization assumptions |
| Preliminary Technical Feasibility | Solution/early requirements | Forecast/Commercial/Scoring | Commercial/Risk/Sales Design | Missing critical dependency/data |
| Risk / Legal / Security / Compliance | Product/technical context | Investment/Architecture constraints | GTM/Forecasting | Unacceptable risk |
| Preliminary Forecasting | Commercial/technical/GTM | Scoring/Investment | Cross-domain challenge | Key estimates unavailable |
| Investment Decision | Scoring/Portfolio | Product Definition/Engineering | None | Readiness below threshold |
| Detailed Product Definition | Investment + research | Engineering Requirements | GTM/PMM | Strategic ambiguity |
| Requirements Decomposition | Product Definition | Architecture/Tests/Planning | Early Architecture | Ambiguous/conflicting requirements |
| Execution-Grade Technical Feasibility | Requirements | Architecture/Planning/Forecast | Architecture exploration | Critical unknown unresolved |
| Architecture | Requirements + feasibility | Planning/Implementation/NFR Design | Product refinement | Foundational dependency unresolved |
| Security/Privacy/Reliability Design | Architecture + NFRs | Implementation/Validation/Release | Engineering Planning | Critical control impossible |
| Engineering Planning | Scope/architecture/resources/timing | Implementation/Forecast/GTM timing | GTM/Revenue planning | Delivery confidence too low |
| Environment Strategy | Architecture + test/release plan | Build/Test/Release | Infrastructure automation | Environment unavailable |
| Implementation | Approved plan + environment | Tests/Integration | Test automation/infra/instrumentation | Missing dependency/requirement |
| Integration / Contract Testing | Components/contracts | System Testing | Continued implementation | Dependency unavailable |
| System / E2E Testing | Integrated build | Pre-Prod Validation | NFR testing | Integration unstable |
| NFR Validation | Candidate + NFRs | Release Readiness | Security/performance/reliability parallel | Unrepresentative environment |
| Pre-Production Validation | Candidate + staging | Engineering Readiness | Final GTM prep | Staging/ops/rollback incomplete |
| Engineering Release Readiness | Technical evidence | Integrated Launch Gate | GTM Readiness | Critical defect/risk |
| GTM / Revenue Readiness | Business readiness evidence | Integrated Launch Gate | Engineering Readiness | Revenue/support system incomplete |
| Integrated Launch Readiness | Both readiness streams | Deployment | None | Cross-functional blocker |
| Progressive Deployment | Approved release | Production Verification | Approved soft-launch demand | Canary unhealthy |
| Production Verification | Deployment | Full Rollout/Ops | Observability | Critical health failure |
| Observability | Production + instrumentation | Incident/Analytics | Revenue monitoring | Telemetry gaps |
| Demand / Sales / Activation | Live product + GTM | Customer/revenue evidence | Production Ops | Product/revenue path unavailable |
| Product & Engineering Analytics | Telemetry + product events | Optimization/Portfolio | Commercial analytics | Poor data quality |
| Technical Debt / Architecture Review | Technical evidence | Roadmap/Planning/Portfolio | Product roadmap review | None; recurring |
| Strategic Re-Scoring | Material evidence | Portfolio Action | Cross-domain revalidation | Insufficient evidence |

---

# 12. Continuous Learning / Re-Entry Model

The system uses five governing rules.

## Rule 1 — Earliest Corrective Stage
Route every issue to the earliest stage capable of correcting root cause.

```text
Requirement ambiguity → Requirements Decomposition
Product behavior mismatch → Product Definition
Architecture defect → Architecture
Integration contract failure → API / Contract Design
Security design failure → Security Design / Architecture
Performance architecture failure → Architecture / Infrastructure
Code defect → Implementation
Test defect → Test Strategy
Deployment failure → Release Engineering / Environment Strategy
Reliability failure → Reliability Design / Architecture / Operations
Infrastructure cost problem → Architecture / Commercial Analysis / Pricing
Material technical risk → Strategic Re-Scoring
```

## Rule 2 — Impact-Based Re-Validation
When requirements, market assumptions, audience, pricing, architecture, dependencies, compliance, launch timing, infrastructure, security, sales motion, or commercial assumptions change:

1. create a new version,
2. map affected downstream artifacts,
3. invalidate only affected evidence,
4. re-run only affected stages,
5. re-approve only affected gates,
6. escalate to portfolio review only if strategic thresholds are crossed.

## Rule 3 — Common Evidence Layer
Product, engineering, reliability, operations, marketing, sales, commercial, and finance analytics converge before strategic decisions.

## Rule 4 — Tactical vs. Strategic Technical Change
Local defects, small performance tuning, or isolated test gaps remain in Continuous Optimization. Architecture no longer scaling, infrastructure cost damaging margin, security burden changing viability, major duration overruns, dependency continuity risk, or chronic reliability affecting retention trigger strategic review.

## Rule 5 — Production Evidence Is First-Class
Real production evidence can invalidate pre-launch assumptions and therefore has authority to reopen Product, Architecture, Engineering Planning, Commercial Analysis, Pricing, GTM, or Portfolio decisions.

---

# 13. Final Simplified End-to-End Operating Loop

```text
Signal Collection / Idea Submission
↓
Problem Discovery
↓
Exploratory Market + Customer Validation
↓
Market / Competitive / Audience Analysis
↓
Solution Discovery
↓
Preliminary Product Marketing
↓
Commercial Analysis
↓
Preliminary Sales-System Design
↓
Preliminary Technical Feasibility + Architecture Exploration
↓
Risk / Legal / Security / Compliance
↓
GTM Feasibility
↓
Preliminary Forecasting
↓
Cross-Domain Validation
↓
Composite Scoring
↓
Portfolio Comparison
↓
[INVESTMENT DECISION]
↓
Execution-Grade Market / Customer Research
↓
Detailed Product Definition
↓
Product Marketing + Brand / Positioning
↓
Detailed GTM Strategy + Launch Timing
↓
Engineering Intake
↓
Requirements Decomposition + First-Class NFRs
↓
Execution-Grade Technical Feasibility
↓
Architecture & System Design
↓
[ARCHITECTURE / TECHNICAL DESIGN GATE]
↓
[PARALLEL]
Engineering Planning
+
Security / Privacy / Reliability Design
+
Execution-Grade Forecasting
+
Revenue / Sales-System Design
+
Campaign / Media / Sales Enablement Planning
↓
[ENGINEERING PLAN / DELIVERY CONFIDENCE GATE]
↓
Implementation
↔ Code Review
↔ Automated Testing
↔ Integration / Contract Testing
↔ Earliest-Affected-Stage Rework
↓
System / E2E / Regression Testing
↓
[PARALLEL]
Performance / Scalability
+
Reliability / Resilience
+
Security / Privacy / Compliance
+
Accessibility
↓
Pre-Production Validation
↓
[ENGINEERING RELEASE READINESS]
+
[GTM / REVENUE READINESS]
↓
[INTEGRATED LAUNCH READINESS]
↓
Progressive Deployment
↓
[DEPLOYMENT EXPANSION GATE]
↓
Production Verification
↓
[PRODUCTION HEALTH GATE]
↓
Demand Generation
↓
Sales / Conversion
↓
Provisioning / Onboarding
↓
Activation / Customer Usage
↓
Retention / Expansion / Renewal
↓
[PARALLEL]
Production Observability
+
Product Analytics
+
Engineering / Reliability Analytics
+
Marketing / Sales / Revenue / Financial Analytics
↓
Common Evidence Layer
↓
Continuous Product + Engineering + Commercial Optimization
↓
Technical Debt / Architecture Health Review
↓
[TRIGGER: MATERIAL CHANGE]
Strategic Re-Scoring / Portfolio Re-Evaluation
↓
Scale / Maintain / Optimize / Rebuild / Re-platform /
Reposition / Reprice / Reduce / Pivot / Pause / Sunset
↓
Learning returns to the earliest affected stage
↓
New learning creates new signals and future product evolution
```

---

## Final Operating Principle

The mature online company should not operate separate Product, Engineering, Marketing, Sales, and Operations funnels. It should operate one evidence-driven system.

- **Product** determines what customer outcome should exist.
- **Engineering** determines how that outcome can be delivered safely, reliably, scalably, maintainably, and economically.
- **Commercial and Finance** determine whether it can produce attractive economics.
- **Marketing and Product Marketing** create and shape demand.
- **Sales and Revenue Operations** convert appropriate demand.
- **Customer Success and Lifecycle** help customers realize and retain value.
- **Reliability and Operations** keep the product healthy in production.
- **Analytics** creates a common evidence layer.
- **Portfolio Management** continuously reallocates capital, engineering capacity, marketing spend, and operational attention based on evidence.

Engineering evidence is therefore both a **delivery input** and a **business-decision input**. A material change in engineering effort, delivery confidence, infrastructure cost, architecture risk, security burden, scalability, reliability, or maintenance cost can legitimately change pricing, launch timing, commercial forecasts, investment priority, or whether the product should continue to exist.
