---
id: PM01-PRODUCT-BRIEF
version: 2
status: complete
owner: PM01
based_on: [SEED-01, STD-NE-01]
requirements: [PM01-REQ-01, PM01-REQ-02, PM01-REQ-03, PM01-REQ-04, PM01-REQ-05, PM01-REQ-06, ASM-PM01-01]
---
# Domain Product Brief

## 0. Domain context (OUT-PM01-DOMAIN-PRODUCT-BRIEF-01)
PM01 owns end-to-end intent-to-software experience: requirements, planning, agent workflows, code creation, debugging, refactoring and human oversight. This is platform capability, not hypothetical app requirements. Completion means authoring, not build/release authorization. (SEED-01 §§1,25,26; STD-NE-01 §11.)

## 1. Executive summary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-02)
The initial single, potentially nontechnical VP/operator needs intended outcomes translated into maintainable software without manually coordinating implementation. PM01 preserves intent across development and makes consequential decisions understandable; independent evidence, not code generation alone, establishes readiness. (SEED-01 §§1–3,8–9,21.)

## 2. Users and stakeholders (OUT-PM01-DOMAIN-PRODUCT-BRIEF-03)
The VP expresses goals and oversees consequential decisions. Long-term product/business users change constraints; technical users inspect, debug and refactor; operators initiate evidence-backed repairs; independent validators challenge acceptance. These are seed-defined roles, not research-validated personas. UX01 owns user evidence. (SEED-01 §§2.1,18,32.11.)

## 3. Outcomes and value (OUT-PM01-DOMAIN-PRODUCT-BRIEF-04)
Measure intent fidelity, valid autonomous completion, intervention time, corrections, unnecessary escalations, first-pass validation, escaped defects and forecast calibration. No numerical autonomy/fidelity target is supplied. Shared throughput objective: “Approximately 5–10 newly deployed applications per week for the initial VP operator, plus ongoing updates to existing products.” Upper-bound objective: “≤7 days when requirements, access, credentials, accounts and external dependencies are available and the product remains within supported MVP scope.” Neither overrides quality gates. (SEED-01 §§27.2,29.)

## 4. Scope boundary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-05)
PM01 owns continuity and oversight across development. PM02 owns model capability; PM03 authority; PM06 creation interfaces; PM07 workspace; PM08 builds/promotion; PM09 infrastructure; PM10 data; PM11 integration/export; PM12 security; PM13 validation; PM14 operations; PM15 lifecycle; PM16 ecosystem; PM17 orchestration. PM04/PM05 own product-type creation across web apps, mobile apps, browser games and mobile games; APIs/backends are components, not a fifth MVP category. (SEED-01 §§2.2,24,26.)

STD-NE-01's 25-gap overlay assigns suggested-concept handoff to SP18, audience intelligence to SP19, forecasts/calibration to SP20, market-validation assurance to SP21 and commercial resilience/portfolio brand to SP22. PM01 presents their conclusions without replacing them. NT06 pricing, NT13 privacy, NT18 accessibility, NT19 individual brand and UX01 evidence remain external authorities (standard respective domain sections).

BND-PM01-DOMAIN-PRODUCT-BRIEF-01: not_applicable—detailed requirements belong to Domain PRD (STD-NE-01 §13).
BND-PM01-DOMAIN-PRODUCT-BRIEF-02: not_applicable—implementation and technology choices belong to Engineering (SEED-01 §26.5).
BND-PM01-DOMAIN-PRODUCT-BRIEF-03: not_applicable—schedule detail belongs to Domain Roadmap/Project plan (STD-NE-01 §§19,386).

## 5. Capabilities (OUT-PM01-DOMAIN-PRODUCT-BRIEF-06)
PM01 owns the following outcome requirements; detailed elaboration belongs to the Domain PRD, STD-NE-01 §13, whose output is unavailable.

| ID | Priority | Outcome / rationale | Acceptance outcome and source |
|---|---|---|---|
| PM01-REQ-01 | Critical | Preserve intent and visible assumptions; prevent wrong outcomes | Intent-to-behavior evidence; consequential ambiguity resolved before irreversible work; seed §§3,21.1 |
| PM01-REQ-02 | Critical | Gate manual/suggested Build requests on readiness | No silent prerequisite bypass; authorized force-start records incompleteness/rationale/controls; §§32.3,46 |
| PM01-REQ-03 | Critical | Preserve context through agents, creation, debugging/refactoring | Changes trace to objectives and affected revalidation; §§9.3,15.2,32.4 |
| PM01-REQ-04 | Critical | Understandable, auditable consequential oversight | Operator comprehension and authority evidence; maximum modes deliberately authorized; §21 |
| PM01-REQ-05 | Critical | Evidence-aware completion, not preview self-certification | Independent/non-production evidence across four output types; critical defects block release; §§4,8–9,23–24 |
| PM01-REQ-06 | High | Honest launch forecasting | Before authorization expose construction, validation/testing, deployment and total duration, likely date/range, confidence/dependencies; update with actuals/history/calibration after first completed app; §27.4 |

## 6. Assumptions, constraints and dependencies (OUT-PM01-DOMAIN-PRODUCT-BRIEF-07)
ASM-PM01-01: absent output baselines cannot be assumed approved. PM01 uses direct seed/standard references and baselines unspecified metrics with SP05/UX01 before improvement claims. Applicability.json/workflow appendices are unavailable; conservative subject-matched interfaces below do not substitute for SP13's formal decision.

| Input authority / STD-NE-01 artifact | PM01 interface and revalidation |
|---|---|
| SP18 Suggested-App Detail & One-Click Build Requirements (§557), VP Edit Revalidation Rules | Consume idea/version, qualification and lineage; return edits/Build disposition; material edits invalidate affected readiness |
| SP19 Primary/Secondary/Adjacent Audience Model (§559), Sensitive-Audience Classification & Governance (§561) | Consume audience/confidence/sensitivity; audience changes/drift return to audience, safety/privacy, commercial and UX owners |
| SP20 Build/Deployment Duration Forecast Standard (§572), Historical Estimate Learning Policy (§573), Forecast Calibration & Backtesting Report (§569) | Consume versioned forecasts, assumptions/confidence/calibration; return scope changes and PM08/Engineering actuals. PM01 owns presentation, SP20 methodology/calibration, PJL committed schedules |
| SP21 Market Validation Results & Qualification Decision (§583), Business-Model Red-Team Protocol (§578) | Consume challenged qualification evidence/limitations; scope, audience or monetization changes trigger revalidation; NT08/PL retain final commercial authority |
| SP22 Distribution Concentration Risk Assessment (§584), Channel/Provider Fallback Strategy (§586), Portfolio Brand Architecture (§587) | Consume resilience and portfolio-brand constraints alongside PM11/NT17/NT19; changed channel/provider/brand relationships trigger revalidation |
| PL Pre-Build Readiness Package (§597) | Consume current applicable contributions; missing/stale evidence cannot silently pass |
| SP13, SP14, SP17, SP05 (standard domain sections) | Return context changes, readiness claims, decisions and metrics respectively for applicability, independent assurance, authority/audit and measurement validation |

Material specialist contradictions block affected readiness until workflow reconciliation (seed §§33–36). Commercial thresholds/exemptions remain seed §28 and business-owner policy. Non-production/quality/authority gates cannot be traded for speed. Hardware strategy/BOM remains in seed §§38–45/Appendix G; SE11 owns physical realization, never copied here.

| Missing source/dependency | Disposition |
|---|---|
| PL-REQ-ID-REGISTER | not_applicable: path/file unavailable in snapshot |
| PL-PRODUCT-VISION-BRIEF | not_applicable: file unavailable |
| PL-PRODUCT-STRATEGY | not_applicable: file unavailable |
| PL-MASTER-PRODUCT-REQUIREM | not_applicable: file unavailable |
| PL-MVP-SCOPE-DEFINITI | not_applicable: file unavailable |
| PL-MASTER-PRODUCT-ROADMAP | not_applicable: file unavailable |
| PL-PRODUCT-PRIORITY-FRAMEWOR | not_applicable: file unavailable |
| PL-PRODUCT-KPIS-SUCCESS | not_applicable: file unavailable |
| PL-PRODUCT-CONSTRAI-GUARDRAI | not_applicable: file unavailable |
| PL-PRODUCT-DECISION-LOG | not_applicable: file unavailable |
| PL-GREENFIE-BASELINE-EXTERNAL | not_applicable: file unavailable |

These ten PL dependencies are recorded from review F2; current context names no required dependencies. No absent content is claimed read/approved. Remaining product questions are dispositioned: clarification is risk-based (seed §21.1), Build is readiness-gated (§32.3), unspecified metric thresholds require evidence, and design/schedule are excluded. No unresolved brief-level decision remains.

### Conflicts
No substantive conflict identified with available seed/standard. No agreement with absent outputs asserted. Stage labels removed rather than inventing workflow-stage or delivery-acceptance status.

## 7. Success and KPI links (OUT-PM01-DOMAIN-PRODUCT-BRIEF-08)
Success is understandable creation/change preserving intent, authority and independently evidenced quality. North star remains “the percentage of lifecycle work completed autonomously while still meeting intended outcomes and all applicable production-quality requirements” (seed §29.1). Domain KPIs / Success Metrics (STD-NE-01 §24; output unavailable) owns formulas, windows, baselines and targets. PM01 accepts the §5 outcomes with UX01 comprehension, PM13/SP14 quality, PM08 delivery, SP17 authority and SP20 forecast-method evidence. Forecast presentation must match SP20's current version, assumptions and calibration; committed PJL dates stay separately identified. Missing/failed evidence is not success; improved averages cannot offset hard-gate failure.

## Self-review and revision closure
F1: §§4/6/7 restore readable STD-NE-01 and SP18–SP22 canonical interfaces, particularly SP20 forecast authority. F2: §6 individually dispositions all ten absent PL dependencies. F3: stage labels removed. This revision replaces the current target, not a release attestation.

QC-PM01-DOMAIN-PRODUCT-BRIEF-01 covered: claims trace to approved SEED-01 v1.0, readable STD-NE-01 v1.0 or explicit assumption; seed folder contains only SEED-01, read in full. Sources are normative, not empirical proof; external policy currency remains applicability-time work.
QC-PM01-DOMAIN-PRODUCT-BRIEF-02 covered: external authorities and comparison limits explicit; no substantive contradiction identified.
QC-PM01-DOMAIN-PRODUCT-BRIEF-03 covered: requested unified header and stable requirement IDs retained; no fabricated approved output links.
QC-PM01-DOMAIN-PRODUCT-BRIEF-04 covered: scope, owners, measurable outcomes and evidence limits enable independent brief consumption, not implementation or schedule authorization.
