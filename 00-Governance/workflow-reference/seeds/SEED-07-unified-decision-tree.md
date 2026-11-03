---
id: SEED-07
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "latest_unified_decision_tree_visual_text_flowchart.md"
---

# Integrated Product–Engineering–Marketing–Growth–Sales Visual Text Flow Chart

A visual flow-chart conversion of **the latest unified decision tree**, preserving its original 22 phases, named gates, decision outcomes, parallel workstreams, rework destinations, triggers, and learning loop. This is a faithful visual reformat of the source, not a new operating-model revision.

**Notation:** `╔═╗` phase boundary · `╭─╮` decision gate / parallel section · `┌─┐` activity · `│ ▼` default progression · `├─ / └─` option branches · `→` handoff or re-entry · `[STOP]` terminal outcome · `[ESCALATION]` governance review.

For best alignment, view in a Markdown editor with a monospace font and horizontal scrolling if necessary.

## Complete visual text flow chart

```text
╔══════════════════════════════════════════════════════════════════════════╗
║                 PHASE 1 — SIGNAL & OPPORTUNITY DISCOVERY                 ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Signal Collection / Idea Submission                                     │
└──────────────────────────────────────────────────────────────────────────┘
├─ Market / customer / sales / product signal
├─ Engineering / reliability / incident signal
├─ Infrastructure / cost signal
└─ Human-submitted idea
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Signal Classification                                                   │
└──────────────────────────────────────────────────────────────────────────┘
├─ Duplicate → Merge with existing opportunity/product evidence
├─ Weak but plausible → Watchlist
│  → [TRIGGER] New evidence / threshold crossed → Re-enter classification
├─ Irrelevant / prohibited → [STOP] Reject / archive
└─ Valid opportunity → Problem Discovery
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Exploratory Market Research                                             │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Exploratory Consumer Insights                                           │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Audience Discovery                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                    DECISION GATE — Problem Validation                    │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Proceed → Problem Validation
├─ Gather more evidence → Research / Validation Experiment
├─ Pivot problem → Problem Discovery
├─ Pivot audience → Audience Discovery
├─ Defer → Watchlist
└─ Reject → [STOP]

╔══════════════════════════════════════════════════════════════════════════╗
║                  PHASE 2 — PROBLEM / MARKET VALIDATION                   ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Problem Validation                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Market Analysis                                                         │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Competitive Analysis                                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Early Audience Segmentation                                             │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│            DECISION GATE — Opportunity / Commercial Viability            │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Proceed → Solution Discovery
├─ Rework market scope → Market Analysis
├─ Reframe problem → Problem Discovery
├─ Pivot audience → Audience Discovery / Segmentation
├─ Gather evidence → Research / Consumer Insights
├─ Defer / Watchlist
└─ Reject → [STOP]

╔══════════════════════════════════════════════════════════════════════════╗
║                PHASE 3 — SOLUTION & COMMERCIAL VALIDATION                ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Solution Discovery                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Preliminary Product Marketing                                           │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Commercial Analysis                                                     │
└──────────────────────────────────────────────────────────────────────────┘
├─ Monetization
├─ Pricing / packaging hypotheses
├─ Revenue / margin model
├─ Preliminary CAC / LTV
└─ Commercial constraints
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Preliminary Sales-System Design                                         │
└──────────────────────────────────────────────────────────────────────────┘
├─ Candidate sales motions
├─ Buyer journey
├─ Qualification / routing assumptions
├─ Checkout / contract model
└─ Provisioning / onboarding assumptions

╭──────────────────────────────────────────────────────────────────────────╮
│                      [PARALLEL — EARLY ENGINEERING]                      │
╰──────────────────────────────────────────────────────────────────────────╯
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
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│            DECISION GATE — Preliminary Technical Feasibility             │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Feasible → Continue
├─ Feasible with constraints → Record constraints → Continue
├─ Prototype / spike → Run spike → Re-evaluate
├─ Re-scope product → Solution Discovery
├─ Change technology / dependency → Architecture Exploration
├─ Resolve dependency → Dependency owner → Re-evaluate
├─ [ESCALATION] Technical / security / governance review
└─ Infeasible → Solution Discovery or [STOP]
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Technical evidence updates Commercial Analysis + Forecasting            │
└──────────────────────────────────────────────────────────────────────────┘
→ effort / duration / infrastructure cost / risk / maintenance / confidence

╔══════════════════════════════════════════════════════════════════════════╗
║            PHASE 4 — PRELIMINARY TECHNICAL / RISK VALIDATION             ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Risk / Legal / Security / Compliance                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  GTM Feasibility                                                         │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Preliminary Forecasting                                                 │
└──────────────────────────────────────────────────────────────────────────┘
├─ Demand / revenue / margin
├─ CAC / LTV
├─ Engineering build and operating cost
├─ Infrastructure cost
├─ Sales conversion assumptions
├─ Build / release timing
└─ Delivery confidence
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Cross-Domain Validation                                                 │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                   DECISION GATE — Investment Readiness                   │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Proceed
├─ Commercial remediation → Commercial Analysis
├─ Technical remediation → Preliminary Technical Feasibility
├─ Risk remediation → Risk / Legal / Security / Compliance
├─ GTM remediation → GTM Feasibility
├─ Gather evidence → Relevant validation stage
├─ Defer / Watchlist
└─ Reject → [STOP]

╔══════════════════════════════════════════════════════════════════════════╗
║                PHASE 5 — PORTFOLIO & INVESTMENT DECISION                 ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Composite Scoring                                                       │
└──────────────────────────────────────────────────────────────────────────┘
├─ Market / customer / commercial
├─ Technical feasibility / complexity
├─ Delivery confidence / build duration
├─ Infrastructure and maintenance cost
├─ Security / compliance burden
└─ Strategic fit
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Portfolio Comparison                                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                   DECISION GATE — Investment Decision                    │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Approve
├─ Approve conditionally → Resolve conditions → Re-check
├─ Return for remediation → Earliest invalidated stage → Re-score → Re-compare
├─ Limited prototype / validation → Test → Re-score / Re-compare
├─ Defer
├─ Watchlist
├─ [ESCALATION] Policy / risk / exception review
└─ Reject → [STOP]

╔══════════════════════════════════════════════════════════════════════════╗
║                       PHASE 6 — PRODUCT DEFINITION                       ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Execution-Grade Market Research                                         │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Execution-Grade Consumer Insights                                       │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Execution-Grade Audience Segmentation                                   │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Product Marketing                                                       │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Brand / Positioning                                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Detailed Product Definition                                             │
└──────────────────────────────────────────────────────────────────────────┘
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
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Detailed GTM Strategy + Launch Timing                                   │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Execution-Grade Forecasting                                             │
└──────────────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║            PHASE 7 — ENGINEERING REQUIREMENTS & ARCHITECTURE             ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Engineering Intake                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Requirements Decomposition                                              │
└──────────────────────────────────────────────────────────────────────────┘
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
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Requirements Version + Traceability Baseline                            │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                  DECISION GATE — Requirements Readiness                  │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Ready
├─ Ready with conditions
├─ Ambiguous → Product Definition / Requirements
├─ Missing NFR → Requirements Decomposition
├─ Conflicting → Product + Engineering resolution
└─ Material scope contradiction → Product / Commercial / GTM review
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Execution-Grade Technical Feasibility                                   │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                        [PARALLEL — ARCHITECTURE]                         │
╰──────────────────────────────────────────────────────────────────────────╯
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
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│             DECISION GATE — Architecture / Technical Design              │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Approve
├─ Approve with conditions
├─ Simplify / redesign
├─ Technical spike
├─ Resolve dependency
├─ Change technology
├─ Revise product scope
└─ [ESCALATION] Architecture / Security / Portfolio review

╔══════════════════════════════════════════════════════════════════════════╗
║        PHASE 8 — INTEGRATED PRODUCT / ENGINEERING / GTM PLANNING         ║
╚══════════════════════════════════════════════════════════════════════════╝

╭──────────────────────────────────────────────────────────────────────────╮
│                                [PARALLEL]                                │
╰──────────────────────────────────────────────────────────────────────────╯
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
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Engineering plan → updates Execution-Grade Forecasting + GTM launch     │
│  timing                                                                  │
└──────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────┐
│  GTM timing → updates engineering milestones + release strategy          │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│          DECISION GATE — Engineering Plan / Delivery Confidence          │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Proceed
├─ Proceed conditionally
├─ Re-sequence → Engineering Planning
├─ Add capacity → Planning / Portfolio
├─ Reduce scope → Product Definition
├─ Change launch timing → GTM Strategy
├─ Change architecture → Architecture
├─ Resolve dependency → Planning / Architecture
└─ [ESCALATION] Confidence below threshold
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│         DECISION GATE — Security / Privacy / Reliability Design          │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Approve
├─ Approve with controls
├─ Rework design
├─ Change architecture
├─ Reduce scope
└─ [ESCALATION] High / critical unresolved risk

╔══════════════════════════════════════════════════════════════════════════╗
║            PHASE 9 — IMPLEMENTATION & CONTINUOUS VERIFICATION            ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Environment Readiness                                                   │
└──────────────────────────────────────────────────────────────────────────┘
├─ Local / Development
├─ Test
├─ Integration
├─ Staging / Pre-Production
├─ Production-like Validation
├─ Controlled Release
└─ Production
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                                [PARALLEL]                                │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Application / Service Implementation
├─ Infrastructure Automation
├─ Data / Integration Implementation
├─ Test Automation Development
├─ Security Controls
├─ Observability Instrumentation
└─ Product Analytics Instrumentation
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Implementation                                                          │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Code Review                                                             │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Automated Validation                                                    │
└──────────────────────────────────────────────────────────────────────────┘
├─ Static analysis
├─ Linting
├─ Type checking
├─ Unit tests
└─ Component tests
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Integration Validation                                                  │
└──────────────────────────────────────────────────────────────────────────┘
├─ Integration tests
└─ API / contract tests
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│           DECISION GATE — Implementation / Integration Quality           │
╰──────────────────────────────────────────────────────────────────────────╯
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
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Repeat until exit criteria satisfied                                    │
└──────────────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║          PHASE 10 — SYSTEM / SECURITY / RELIABILITY VALIDATION           ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  System Testing                                                          │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  End-to-End Testing                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Regression Testing                                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                                [PARALLEL]                                │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Performance Testing
├─ Load / Scalability Testing
├─ Reliability / Resilience Testing
├─ Security Testing
├─ Privacy Validation
├─ Accessibility Validation
└─ Compliance Validation
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  User / Business Acceptance, where appropriate                           │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                 DECISION GATE — System / NFR Validation                  │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Pass
├─ Functional defect → Implementation / Requirements
├─ Performance issue → Architecture / Infrastructure / Implementation
├─ Scalability limit → Architecture / Capacity / Forecasting
├─ Reliability issue → Reliability Design / Architecture
├─ Security finding → Security Design / Architecture / Implementation
├─ Privacy issue → Privacy Design / Product Requirements
├─ Accessibility issue → Product / UX / Implementation
└─ Compliance issue → Compliance / Requirements / Product

╔══════════════════════════════════════════════════════════════════════════╗
║                   PHASE 11 — PRE-PRODUCTION VALIDATION                   ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Production-Like Pre-Production Validation                               │
└──────────────────────────────────────────────────────────────────────────┘
├─ Complete customer journeys
├─ Permissions / roles
├─ Payments / contracts
├─ Integrations / migrations
├─ Analytics / observability
├─ Runbooks
├─ Failure / recovery / rollback
├─ Device / browser compatibility
└─ Representative performance
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                DECISION GATE — Pre-Production Validation                 │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Pass
├─ Controlled exception
├─ Functional remediation → Implementation
├─ Technical remediation → Architecture / Implementation
├─ Operational remediation → Operations / Runbooks
├─ Measurement remediation → Analytics / Observability
└─ Fail → Hold release

╔══════════════════════════════════════════════════════════════════════════╗
║                    PHASE 12 — RELEASE & GTM READINESS                    ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Engineering Release Readiness                                           │
└──────────────────────────────────────────────────────────────────────────┘
├─ Functional + test evidence
├─ NFR thresholds
├─ Security / privacy / reliability evidence
├─ Environment / migration readiness
├─ Observability / runbooks
├─ Rollback evidence
└─ Release evidence package
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│              DECISION GATE — Engineering Release Readiness               │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Ready
├─ Ready with controlled exceptions
├─ Limited release only
├─ Remediation required
├─ Delay
└─ Reject release

╭──────────────────────────────────────────────────────────────────────────╮
│                                [PARALLEL]                                │
╰──────────────────────────────────────────────────────────────────────────╯
┌──────────────────────────────────────────────────────────────────────────┐
│  Business / GTM / Revenue Readiness                                      │
└──────────────────────────────────────────────────────────────────────────┘
├─ Product acceptance
├─ Campaign / sales readiness
├─ Pricing / packaging
├─ Contract / checkout / payment
├─ Support / success
├─ Provisioning / onboarding
├─ Analytics / attribution
└─ Launch timing
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                 DECISION GATE — GTM / Revenue Readiness                  │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Ready
├─ Limited launch
├─ Remediation required
├─ Change timing
└─ Delay

┌──────────────────────────────────────────────────────────────────────────┐
│  Engineering Release Readiness                                           │
└──────────────────────────────────────────────────────────────────────────┘
+
┌──────────────────────────────────────────────────────────────────────────┐
│  GTM / Revenue Readiness                                                 │
└──────────────────────────────────────────────────────────────────────────┘
+
┌──────────────────────────────────────────────────────────────────────────┐
│  Product / Security / Reliability / Legal / Ops / Analytics readiness    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│               DECISION GATE — Integrated Launch Readiness                │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Ready → Progressive Deployment
├─ Ready with controlled exceptions → Approved exception → Deployment
├─ Limited / staged launch → Controlled cohort
├─ Remediation required → Failed readiness domain
├─ Delay → GTM / Engineering Planning
├─ Roll back to earlier stage → Earliest invalidated stage
└─ Stop / reject release → [STOP]

╔══════════════════════════════════════════════════════════════════════════╗
║                    PHASE 13 — PROGRESSIVE DEPLOYMENT                     ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Build Artifact                                                          │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Controlled Environment                                                  │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Verification                                                            │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Canary / Pilot / Limited Cohort                                         │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Observe                                                                 │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                   DECISION GATE — Deployment Expansion                   │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Healthy → Expand deployment
├─ Degraded → Pause → Remediate → Re-verify
└─ Critical → Rollback / disable feature / failover → Incident path
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Feature flags + rollout + rollback controls remain active               │
└──────────────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║                    PHASE 14 — PRODUCTION VERIFICATION                    ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Production Verification                                                 │
└──────────────────────────────────────────────────────────────────────────┘
├─ App / API / auth / payment health
├─ Data correctness
├─ Customer journeys
├─ Latency / errors / resources
├─ Security telemetry
├─ Analytics / attribution
└─ Deployment health
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│                    DECISION GATE — Production Health                     │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Healthy → Continue / expand
├─ Degraded → Hold / remediate
├─ Critical → Rollback / failover / incident
└─ Strategic defect → Product / Architecture / Commercial review

╔══════════════════════════════════════════════════════════════════════════╗
║                  PHASE 15 — DEMAND / SALES / ACTIVATION                  ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Demand Generation                                                       │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Demand / Lead Entry                                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Visitor / Lead Identification                                           │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Qualification                                                           │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Sales Motion Routing                                                    │
└──────────────────────────────────────────────────────────────────────────┘
├─ Self-Service
├─ Product-Led
├─ Sales-Assisted
├─ Outbound
└─ Hybrid
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Need / Solution Matching                                                │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Buyer Education / Value Development                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Offer / Pricing / Commercial Terms                                      │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Proposal / Negotiation, if required                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Checkout / Contract                                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Payment / Conversion                                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Account Provisioning                                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Onboarding                                                              │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Activation / First Value                                                │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Usage / Customer Health                                                 │
└──────────────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║             PHASE 16 — PRODUCTION OPERATIONS & OBSERVABILITY             ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Observability / Monitoring                                              │
└──────────────────────────────────────────────────────────────────────────┘
├─ Logs / metrics / traces
├─ Uptime / latency / error rates
├─ Resource / infrastructure / service health
├─ Security telemetry
├─ User-experience telemetry
├─ Business KPIs
├─ Deployment health
└─ SLO / SLA indicators
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Production Signal                                                       │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Severity / Impact Classification                                        │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│         DECISION GATE — Incident / Defect / Performance Response         │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Minor defect → Backlog / planned remediation
├─ Major defect → Prioritized fix → Implementation / Tests
├─ Critical incident → Incident response / mitigation / rollback
├─ Security incident → Security incident process → Security / Architecture / Implementation
├─ Reliability failure → Rollback / failover → Reliability / Architecture / Ops
└─ Architectural systemic issue → Architecture Review → Strategic impact analysis
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Post-Incident / Defect Analysis                                         │
└──────────────────────────────────────────────────────────────────────────┘
→ Engineering response
→ Product response
→ Business response
as appropriate

╔══════════════════════════════════════════════════════════════════════════╗
║          PHASE 17 — RETENTION / EXPANSION / REVENUE OPERATIONS           ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Retention                                                               │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Lifecycle / Retention Marketing                                         │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Customer Health Monitoring                                              │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Expansion                                                               │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Renewal / Repeat Purchase                                               │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Customer / support / sales evidence → Common Evidence Layer             │
└──────────────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║          PHASE 18 — PRODUCT + ENGINEERING + BUSINESS ANALYTICS           ║
╚══════════════════════════════════════════════════════════════════════════╝

╭──────────────────────────────────────────────────────────────────────────╮
│                        [PARALLEL EVIDENCE LAYER]                         │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Product Analytics
├─ Engineering Analytics
├─ Reliability Analytics
├─ Operational Analytics
├─ Commercial Analytics
├─ Marketing Analytics
├─ Sales Analytics
└─ Financial Analytics
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Common Evidence Layer                                                   │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  ROI / LTV / CAC / Margin Analysis                                       │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Actual vs. Forecast                                                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Technical Cost / Reliability / Delivery Analysis                        │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│            DECISION GATE — Product / Commercial Optimization             │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Local product issue → Product Optimization
├─ Local engineering issue → Engineering Optimization
├─ Acquisition issue → Marketing / Sales Motion
├─ Pricing / margin issue → Commercial Analysis
├─ Reliability issue → Reliability / Architecture
├─ Cost issue → Architecture / Infrastructure / Commercial
├─ Material technical risk → Strategic Re-Scoring
└─ Healthy → Maintain / Scale

╔══════════════════════════════════════════════════════════════════════════╗
║                    PHASE 19 — CONTINUOUS OPTIMIZATION                    ║
╚══════════════════════════════════════════════════════════════════════════╝

╭──────────────────────────────────────────────────────────────────────────╮
│                                [PARALLEL]                                │
╰──────────────────────────────────────────────────────────────────────────╯
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
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Change Impact Analysis                                                  │
└──────────────────────────────────────────────────────────────────────────┘
├─ Requirements?
├─ Market / audience?
├─ Pricing?
├─ Architecture / dependency?
├─ Compliance / security?
├─ Launch timing?
├─ Infrastructure?
├─ Sales motion?
└─ Commercial assumptions?
                                      │
                                      ▼
[TRIGGER] If material:
→ identify affected stages
→ invalidate affected evidence
→ increment requirements/design version
→ re-run only affected stages
→ re-approve affected gates

╔══════════════════════════════════════════════════════════════════════════╗
║        PHASE 20 — ARCHITECTURE / TECHNICAL DEBT / PRODUCT HEALTH         ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Technical Debt / Architecture Health Review                             │
└──────────────────────────────────────────────────────────────────────────┘
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
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│             DECISION GATE — Architecture / Technical Health              │
╰──────────────────────────────────────────────────────────────────────────╯
├─ Accept debt
├─ Schedule remediation
├─ Refactor
├─ Re-platform
├─ Replace component
├─ Re-architect
├─ Accelerate migration
├─ Reduce feature investment
└─ [ESCALATION] Strategic technical risk

╔══════════════════════════════════════════════════════════════════════════╗
║        PHASE 21 — STRATEGIC RE-SCORING / PORTFOLIO RE-EVALUATION         ║
╚══════════════════════════════════════════════════════════════════════════╝

[TRIGGER] Material change in market, PMF, engineering effort/duration,
┌──────────────────────────────────────────────────────────────────────────┐
│  delivery confidence, architecture complexity, infrastructure cost,      │
└──────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────┐
│  security/compliance burden, reliability, scalability, maintenance,      │
└──────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────┐
│  unit economics, revenue/retention, or strategic fit                     │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Return to earliest invalidated strategic stage                          │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Re-run affected downstream validation                                   │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Cross-Domain Validation                                                 │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Composite Re-Scoring                                                    │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  Portfolio Re-Comparison                                                 │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
╭──────────────────────────────────────────────────────────────────────────╮
│      DECISION GATE — Strategic Re-Scoring / Portfolio Re-Evaluation      │
╰──────────────────────────────────────────────────────────────────────────╯
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

╔══════════════════════════════════════════════════════════════════════════╗
║                       PHASE 22 — PORTFOLIO ACTION                        ║
╚══════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────┐
│  Scale / Maintain / Optimize / Rebuild / Re-platform / Reposition /      │
└──────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────┐
│  Reprice / Reduce / Pivot / Pause / Sunset                               │
└──────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  [FEEDBACK LOOP]                                                         │
└──────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────┐
│  Product + Engineering + Customer + Revenue + Market learning            │
└──────────────────────────────────────────────────────────────────────────┘
→ Signal Collection
→ Product evolution / future opportunity discovery
```

## Navigation

The **22 numbered phase banners** follow the source tree from signal discovery through portfolio action. Side branches represent conditional outcomes and may return to an earlier phase. Parallel activity branches are concurrent *when prerequisites permit*. The operating loop is continuous: production, customer, revenue, and engineering evidence can re-open the earliest stage capable of correcting an invalidated assumption.
