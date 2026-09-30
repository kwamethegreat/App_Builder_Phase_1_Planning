---
id: PM01-PRODUCT-BRIEF
version: 3
status: complete
owner: PM01
based_on: [SEED-01]
requirements: [PM01-REQ-01, PM01-REQ-02, PM01-REQ-03, PM01-REQ-04, PM01-REQ-05, PM01-REQ-06, ASM-PM01-01]
---
# Domain Product Brief

## 0. Domain context (OUT-PM01-DOMAIN-PRODUCT-BRIEF-01)
PM01 owns the end-to-end intent-to-software experience: requirements, planning, agent workflows, code creation, debugging, refactoring and human oversight. This brief defines platform outcomes, not requirements for a hypothetical generated application. Cross-domain concerns enter as constraints, evidence or handoffs, not transferred ownership. Completion of this document is not build or release authorization. (SEED-01 §§1,25,26.)

## 1. Executive summary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-02)
The initial single, potentially nontechnical VP/operator needs intended outcomes translated into maintainable software without manually coordinating implementation. PM01 preserves intent through autonomous development and makes consequential decisions understandable. Its value is reduced coordination and intervention without losing intent, authority or independently demonstrated quality—not merely faster code generation. (SEED-01 §§1–3,8–9,21,29.)

## 2. Users, stakeholders and jobs (OUT-PM01-DOMAIN-PRODUCT-BRIEF-03)
| Audience | Domain job | Evidence basis |
|---|---|---|
| Initial VP/operator | Express goals, inspect inferred assumptions, understand progress and decide consequential tradeoffs without managing implementation | SEED-01 §§2.1,21 |
| Longer-term product/business users | Change requirements and constraints while understanding affected work and outcomes | §§2.1,32.4 |
| Technical builders | Inspect or modify source and tests; debug or refactor while preserving validated intent | §§2.1,9.3,15.2 |
| Operators/lifecycle stakeholders | Bring operational evidence into diagnosis and governed change | §§13,16,25 |
| Independent validators | Challenge readiness against intended outcomes and evidence, rather than builder confidence | §§8.1,9,32.6 |

These audiences are normative seed descriptions, not research-validated personas. UX01 owns user evidence and experience acceptance; DX01 owns design expression. (SEED-01 §18.)

## 3. Desired outcomes and measurable value (OUT-PM01-DOMAIN-PRODUCT-BRIEF-04)
| Outcome | Measure | Interpretation |
|---|---|---|
| Preserve intended outcomes | Delivered requirements matching validated intent; assumption correction rate | Corrections and missing intent must remain visible, not hidden by completion counts |
| Reduce manual coordination safely | Autonomous lifecycle completion, intervention time per product, unnecessary escalation rate, decisions later reversed | Autonomy counts as value only while applicable quality and intended outcomes are met |
| Make development predictable | Idea-to-non-production, idea-to-production, blocker time and forecast calibration | Report dependencies and uncertainty rather than unconditional dates |
| Make changes trustworthy | First-pass validation, escaped defects and critical defects at release | Quality gates cannot be averaged away by velocity gains |

Sources: SEED-01 §§17,27.4,29. No numerical autonomy or intent-fidelity target is supplied; ASM-PM01-01 governs unspecified metrics.

Shared platform objective: “Approximately 5–10 newly deployed applications per week for the initial VP operator, plus ongoing updates to existing products.” Upper-bound objective: “≤7 days when requirements, access, credentials, accounts and external dependencies are available and the product remains within supported MVP scope.” These are cross-domain objectives, not PM01-only delivery guarantees or permission to bypass validation. (SEED-01 §§4.3,27.2.)

## 4. Domain scope boundary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-05)
PM01 owns coherent development intent, progress interpretation, change continuity and consequential oversight. The following interfaces preserve adjacent ownership. (SEED-01 §§25–26.)

| Adjacent owners | PM01 handoff / consumed result |
|---|---|
| PM02 / PM03 | Task needs and consequential decisions / model capability and autonomy constraints |
| PM04 / PM05 | Product context and intended outcomes / product-type creation constraints for web apps, mobile apps, browser games and mobile games |
| PM06 / PM07 | Intent, assumptions, change goals / creation interaction and code-workspace capabilities |
| PM08 / PM09 | Ready work and validation needs / build, environment, promotion and capacity status |
| PM10 / PM11 / PM12 | Context and change impact / governed data, integration/export, identity and security constraints |
| PM13 / PM14 / PM15 | Acceptance intent and change rationale / independent validation, operational diagnosis and lifecycle context |
| PM16 / PM17 | Product needs and handoff outcomes / ecosystem constraints and orchestration execution state |

APIs/backends are components of the four MVP categories, not a fifth category. PM01 consumes commercial qualification, audience, brand/IP and deployment conclusions when presenting build intent; it does not own opportunity scoring, pricing, legal clearance or infrastructure selection. NT06 pricing, NT13 privacy, NT18 accessibility, NT19 brand, UX01 research and SP13 applicability retain their seed-defined authority. (SEED-01 §§2.2,18,23.2,26,28,34.) Their output document IDs are not supplied in this context; no approved outputs are implied.

- BND-PM01-DOMAIN-PRODUCT-BRIEF-01 — not_applicable: detailed functional/nonfunctional requirements belong to the Domain PRD, not this brief.
- BND-PM01-DOMAIN-PRODUCT-BRIEF-02 — not_applicable: implementation designs and technology choices belong to Engineering.
- BND-PM01-DOMAIN-PRODUCT-BRIEF-03 — not_applicable: schedule detail belongs to the Domain Roadmap and Project plan.

## 5. Key capabilities (OUT-PM01-DOMAIN-PRODUCT-BRIEF-06)
These are outcome-level requirements owned by PM01; the Domain PRD is the downstream home for detailed elaboration, not reproduced here. Its governed output ID/file is not supplied or present in the PM01 folder.

| ID | Priority | Capability and rationale | Acceptance outcome | Source |
|---|---|---|---|---|
| PM01-REQ-01 | Critical | Preserve intent and visible assumptions to prevent building the wrong outcome | Delivered behavior traces to validated intent; consequential ambiguity is resolved before irreversible work; reversible assumptions remain visible/changeable | SEED-01 §§3,21.1 |
| PM01-REQ-02 | Critical | Gate manual and suggested Build actions on readiness, preventing silent prerequisite bypass | Build invokes formal readiness; missing prerequisites are resolved safely or routed as consequential decisions; authorized force-start records incompleteness, justification and compensating controls | §§32.3,46 |
| PM01-REQ-03 | Critical | Preserve context across planning, agent handoffs, code creation, debugging and refactoring | Changes trace to objectives and affected requirements/evidence; debugging outcomes and refactoring preservation claims receive impact-based revalidation | §§9.3,15.2,25,32.4 |
| PM01-REQ-04 | Critical | Provide understandable, auditable oversight without routine interruption | Consequential decisions expose rationale, alternatives and impacts; assumptions/actions/evidence can be inspected; maximum modes require deliberate extra authorization | §21 |
| PM01-REQ-05 | Critical | Distinguish preview/build completion from independently evidenced readiness | Production-intended changes in all four output categories pass required non-production and independent validation; critical defects block release | §§4,8–9,23–24,32.7 |
| PM01-REQ-06 | High | Present evidence-based launch forecasts to support informed authorization | Before authorization show construction, validation/testing, release/deployment and total duration, likely date/range, confidence and dependencies; update through execution and incorporate historical builds/calibration after the first completed app | §27.4 |

Acceptance outcomes summarize the cited obligations rather than adding detailed test protocols or architecture.

## 6. Critical assumptions, constraints and dependencies (OUT-PM01-DOMAIN-PRODUCT-BRIEF-07)
**ASM-PM01-01 — evidence boundary.** Absent output baselines cannot be assumed approved. PM01 uses direct SEED-01 references; unspecified metric thresholds and windows require a measured baseline and Domain KPI definition before quantitative improvement claims. PM01 owns this disposition, with SP05 measurement and UX01 evidence inputs. This is not a waiver of seed hard gates. No empirical performance or usability success is claimed.

| Constraint/dependency | PM01 treatment and validation hook | Source |
|---|---|---|
| Applicability and standards currency — SP13 | Provide changed product context; consume applicable domains/evidence and reasoned exclusions; changed audience, geography, features or policies trigger reassessment | SEED-01 §§6–7,33–36 |
| Independent assurance — PM13/SP14 | Supply intended outcomes and readiness claims; consume independent findings, current Release Evidence Package and challenger disposition before representing release readiness | §§9,32.6–7,34 |
| Decision governance — PM03/SP17 and SE23 | Present applicable authority, authentication and exception evidence; align human decisions and machine controls; changed authority invalidates affected decision assumptions | §§21,32.18–19,35–36 |
| Measurement — SP05/UX01 | Submit domain measures and comprehension claims for measurement-quality and user-evidence validation | §§18,29,34 |
| Commercial/idea handoff | Preserve idea lineage and qualification evidence; material VP edits trigger affected commercial, audience, technical, schedule, brand/IP and risk revalidation | §§28.1–4,46 |
| Forecast and delivery inputs — PM08/Engineering/PJL | Consume duration evidence and actuals; separate probabilistic launch forecast from committed project schedule; PM01 owns understandable presentation, not schedule authority | §§26.5,27.4 |
| Runtime/hardware — PM09/SE11 | Consume availability/isolation outcomes; no hardware choice or BOM copied here. Canonical strategy is SEED-01 v1.0 §§38–45 and Appendix G v2.2; physical realization belongs to SE11-PHYSICAL-INFRASTR-HARDWARE, SE11-HARDWARE-CAPACITY-SIZING and SE11-POWER-COOLING-RACK | §§38–46 |

Commercial thresholds and personal-use exemption remain governed by SEED-01 §28, not redefined by PM01. Speed does not override required quality, security, compliance, financial or non-production constraints (§4.3). Specialist reverse validation follows §§33–36; no applicability.json or workflow Appendix F/G is supplied as a readable source in this invocation, so no formal applicability decision is asserted.

### Required-source availability
SEED-01 v1.0 is the sole seed listed and was read in full. All ten dependency reads returned not_found; the PL folder listing is empty. Missing-source dispositions follow the run-context rule, not a claim that these baselines are unnecessary to the wider program.

| Source/dependency ID | Disposition |
|---|---|
| PL-REQ-ID-REGISTER | not_applicable: no path supplied and no file available in the PL folder |
| PL-PRODUCT-VISION-BRIEF | not_applicable: named file not found |
| PL-PRODUCT-STRATEGY | not_applicable: named file not found |
| PL-MASTER-PRODUCT-REQUIREM | not_applicable: named file not found |
| PL-MVP-SCOPE-DEFINITI | not_applicable: named file not found |
| PL-MASTER-PRODUCT-ROADMAP | not_applicable: named file not found |
| PL-PRODUCT-PRIORITY-FRAMEWOR | not_applicable: named file not found |
| PL-PRODUCT-KPIS-SUCCESS | not_applicable: named file not found |
| PL-PRODUCT-CONSTRAI-GUARDRAI | not_applicable: named file not found |
| PL-PRODUCT-DECISION-LOG | not_applicable: named file not found |
| PL-GREENFIE-BASELINE-EXTERNAL | not_applicable: named file not found |

Product questions are dispositioned rather than left open: clarification is risk-based (§21.1); Build is readiness-gated (§32.3); unspecified metric targets use ASM-PM01-01; detailed design and scheduling remain excluded. No unresolved brief-level product decision remains.

### Conflicts
No substantive contradiction identified against the available authoritative seed. Agreement with absent PL or adjacent-domain outputs is not asserted. Version 2's STD-NE-01 and SP18–SP22 overlay citations are not carried forward as authority because that source is outside the supplied source set for this invocation; relevant capability intent remains traced directly to SEED-01 §§27–28,46. This is a source-scope correction, not a ruling against an unavailable standard.

## 7. Success definition and KPI links (OUT-PM01-DOMAIN-PRODUCT-BRIEF-08)
Success is understandable creation and change that preserve intent, human authority and independently evidenced quality. The north star remains “the percentage of lifecycle work completed autonomously while still meeting intended outcomes and all applicable production-quality requirements.” (SEED-01 §29.1.)

PM01 uses the six capability outcomes in §5 with UX01 comprehension evidence, PM13/SP14 quality evidence, PM08 delivery evidence and SP17 authority evidence. A preview, builder assertion, missing evidence or failed hard gate is not successful delivery. Critical defects at release must be zero; improved averages cannot compensate for a failed hard gate. (SEED-01 §§4.1,8.1,17.)

The downstream Domain KPIs / Success Metrics document owns metric formulas, windows, baselines and targets; its output is not present in the PM01 folder and no governed ID is supplied. Until available, §3 and SEED-01 §29 provide the measurement families, with ASM-PM01-01 preventing invented thresholds. PL-PRODUCT-KPIS-SUCCESS is separately dispositioned above. This brief is consumable for domain planning, not an implementation specification or empirical acceptance report.

## Self-review and revision closure
The supplied validator finding “header version 2 != 3” is corrected in the unified header: version is 3. This document supersedes PM01-PRODUCT-BRIEF version 2 at the same governed target; stable PM01 requirement IDs are preserved.

- QC-PM01-DOMAIN-PRODUCT-BRIEF-01 — covered: material assertions cite SEED-01 or ASM-PM01-01; normative authority is distinguished from empirical evidence and time-sensitive sources require applicability-time revalidation.
- QC-PM01-DOMAIN-PRODUCT-BRIEF-02 — covered: ownership and validation interfaces are explicit; no known substantive conflict is hidden and absent baselines are not represented as reconciled.
- QC-PM01-DOMAIN-PRODUCT-BRIEF-03 — covered: header matches this run; prior version is explicitly superseded; unsupported inherited citations are dispositioned under Conflicts.
- QC-PM01-DOMAIN-PRODUCT-BRIEF-04 — covered: scope, accountable owners, acceptance outcomes, seed thresholds, missing-source treatment and downstream boundaries are explicit.
