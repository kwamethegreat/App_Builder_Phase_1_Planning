---
id: PM01-PRODUCT-BRIEF
version: 2
status: complete
owner: PM01
based_on: [SEED-01]
requirements: [PM01-REQ-01, PM01-REQ-02, PM01-REQ-03, PM01-REQ-04, PM01-REQ-05, PM01-REQ-06, PM01-DEC-01, PM01-DEC-02, PM01-DEC-03, ASM-PM01-01, ASM-PM01-02, ASM-PM01-03, ASM-PM01-04, PM01-RISK-01, PM01-RISK-02, PM01-RISK-03, PM01-RISK-04, PM01-AC-01, PM01-AC-02, PM01-AC-03, PM01-AC-04, PM01-AC-05, PM01-AC-06]
---

# Domain Product Brief

## 0. Domain context (OUT-PM01-DOMAIN-PRODUCT-BRIEF-01)

PM01, Autonomous Development Experience, owns product intent for the end-to-end intent-to-software experience: requirements, planning, agent workflows, code creation, debugging, refactoring and human oversight. It owns continuity across that journey, not all underlying services. This brief concerns the platform's ability to generate and change software, not feature requirements for a hypothetical generated application. Cross-domain material is limited to interfaces and constraints. (SEED-01 §§1, 25, 26.1, 26.5; supplied outline.)

This is a Stage-1 planning artifact. Completion means document authoring is complete, not that construction, specialist review or release has passed. The authoritative product source is SEED-01 v1.0, approved. The supplied outline is the content contract.

## 1. Executive summary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-02)

The domain addresses the coordination and fidelity gap between expressing an objective and obtaining maintainable software that continues to match it. The initial single VP/operator may be nontechnical and must not have to coordinate implementation detail. The value proposition is governed autonomous development, not simply rapid code generation. This is seed-defined direction, not measured evidence of market superiority. (SEED-01 §§1–3.)

PM01 connects intent or a selected qualified opportunity to planning readiness, creation, diagnosis, safe modification and independently evidenced handoffs. Routine reversible work can proceed within policy; consequential uncertainty remains visible and controllable. More autonomy is valuable only while intended outcomes and applicable production quality are satisfied. (SEED-01 §§21, 25, 29.1, 32.4.)

| Decision | Options considered | Decision, rationale and consequence |
|---|---|---|
| PM01-DEC-01 | Code-generation endpoint; approval at every step; continuous governed development | Adopt continuous intent-to-evidence development. Code alone does not establish readiness, while blanket approval defeats intelligent assumption. PM01 owns journey continuity; adjacent owners retain their authorities. SEED-01 §§8.1, 21, 26 |

## 2. Users, stakeholders and jobs-to-be-done (OUT-PM01-DOMAIN-PRODUCT-BRIEF-03)

These are seed-defined audiences, not research-validated personas. UX01 owns user evidence. (SEED-01 §§2.1, 18.1; ASM-PM01-03.)

| Audience/stakeholder | Domain job | Intended outcome |
|---|---|---|
| Initial VP/operator | Express intent or select a qualified concept; understand scope, progress and consequential decisions | Oversee development without manually coordinating agents or implementation |
| Product/business users, long term | Modify outcomes and constraints | Understand and preserve consequences of changed intent |
| Technical builders and senior technical users | Inspect or modify source; diagnose and refactor | Connect technical work and human edits to requirements and validation |
| Operations and application lifecycle owners | Turn justified failures or improvement evidence into changes | Preserve product context through diagnosis and repair; operations/lifecycle ownership stays external |
| Independent validators and authorized reviewers | Challenge readiness and authorize consequential actions | Obtain traceable acceptance context and evidence independent of builder confidence |

Sources: SEED-01 §§2.1, 9, 16, 21, 32.4, 32.11. Long-term audiences do not imply multi-user enterprise governance is part of the single-operator MVP. Generated-product end users influence context and acceptance; they are not necessarily platform operators. (SEED-01 §§1, 31.)

## 3. Desired outcomes and measurable value (OUT-PM01-DOMAIN-PRODUCT-BRIEF-04)

| Outcome | Measures and value interpretation | Source / accountable interface |
|---|---|---|
| Preserve intent | Delivered requirements matching validated intent; assumption correction and material clarification rates | PM01 with UX01/PM13; SEED-01 §§3, 29 |
| Reduce manual coordination safely | Valid autonomous completion, intervention time, unnecessary escalation, autonomous decisions later reversed | PM01 with PM03/SP17; SEED-01 §§21.6, 29.1, 29.3 |
| Predictable delivery | Idea-to-non-production, idea-to-production, change-to-production, blocker time and forecast calibration | PM01 with PM08 and estimate contributors; SEED-01 §§27.4, 29 |
| Safe creation and change | First-pass validation, escaped defects, change failures and independent findings | PM13/SP14 supply independent evidence; SEED-01 §§4.1, 17, 32.7 |

The shared MVP throughput objective is “Approximately 5–10 newly deployed applications per week for the initial VP operator, plus ongoing updates to existing products.” The upper-bound objective is “≤7 days when requirements, access, credentials, accounts and external dependencies are available and the product remains within supported MVP scope.” PM01 contributes to these platform outcomes; it does not independently guarantee capacity or dates. (SEED-01 §27.2.)

Change targets retain their qualifications: tiny change, “Seconds to minutes where validation scope permits”; small feature/fix, “Minutes”; moderate change, “Minutes to hours”; major feature/overhaul, “Hours or longer only when genuinely necessary for safe implementation and validation.” These are shared experience targets, not new latency SLOs. (SEED-01 §23.3.)

Quality includes “zero known critical defects at release” and “zero known critical security vulnerabilities that violate policy.” Velocity never overrides mandatory validation or other hard constraints. (SEED-01 §§4.1–4.3.)

**PM01-DEC-03 — no fabricated measurement precision.** Options are invented numerical targets or seed targets plus explicit baselining of unspecified measures. Adopt the latter: no empirical baseline or numerical fidelity/autonomy target was supplied. The Domain KPI artifact owns formulas, windows and calibrated targets; section 7 provides decidable acceptance outcomes meanwhile. Consequence: no quantitative improvement claim without comparable evidence. (SEED-01 §29; ASM-PM01-03.)

## 4. Domain scope boundary (OUT-PM01-DOMAIN-PRODUCT-BRIEF-05)

Included: intent/assumption continuity; understandable requirements and planning readiness; agent and human handoffs; code creation, debugging and refactoring; consequential oversight; evidence-aware completion and timing transparency. Repairs and refactoring do not bypass impact analysis, non-production validation or policy. (SEED-01 §§9.3, 15.2, 21, 25, 32.4.)

The MVP experience supports web applications, mobile applications, browser games and mobile games, with or without AI. APIs/backends are components, not a fifth MVP output category. Product-type requirements stay with PM04/PM05. (SEED-01 §§2.2, 24, Appendix F.)

| Adjacent authority | PM01 supplies | PM01 consumes; excluded ownership |
|---|---|---|
| PM02 | Development task intent and outcome evidence | Model capability/dependency status; not model routing or inference design |
| PM03, PM12 | Consequential-action context and decision links | Risk, authority, security and authentication dispositions; not approval/security policy |
| PM04, PM05 | Validated intent and change scope | Product-type feasibility and acceptance; not specialized creation pipelines |
| PM06, UX01, DX01 | Progress, oversight and creation outcomes | Interaction/user evidence and design expression; not screen or visual specifications |
| PM07 | Requirements and change-impact context | Inspectable source, diagnostics and human edits; not workspace/IDE design |
| PM08 | Readiness and traceable candidate changes | Build, non-production and promotion evidence; not delivery implementation |
| PM09 | Concurrent-work and timing-impact needs | Capacity/prerequisite constraints; not hardware or sizing |
| PM10 | Versioned context and evidence relationships | Durable context and data-evolution constraints; not storage/schema design |
| PM11 | Development context and ownership needs | Access/dependency status and export handoff; not connector/export implementation |
| PM13 | Acceptance links, change rationale and intent | Independent validation and regression scope; no builder self-certification |
| PM14, PM15 | Repair/change outcomes and development history | Operational evidence and lifecycle priorities; not incident command or retirement authority |
| PM16, PM17 | Workflow continuity and outcome needs | Technology constraints and orchestration outcomes; not stack or scheduler design |

Ownership references: SEED-01 §§18, 26, 32. PM01 consumes commercial qualification from its business authorities, pricing from NT06, privacy constraints from NT13, accessibility obligations from NT18 and brand direction from NT19; it does not define those policies. Their unavailable output IDs are not invented (ASM-PM01-02). Engineering, including SE02, owns technical realization under SEED-01 §26.5.

| Exclusion criterion | Disposition and destination |
|---|---|
| BND-PM01-DOMAIN-PRODUCT-BRIEF-01 | not_applicable: detailed functional/nonfunctional requirements belong to the Domain PRD, proposed reference PM01-PRD under ASM-PM01-02 |
| BND-PM01-DOMAIN-PRODUCT-BRIEF-02 | not_applicable: implementation design and technology choices belong to Engineering; hardware realization is referenced through SE11-PHYSICAL-INFRASTR-HARDWARE, SE11-HARDWARE-CAPACITY-SIZING and SE11-POWER-COOLING-RACK, not copied |
| BND-PM01-DOMAIN-PRODUCT-BRIEF-03 | not_applicable: schedule detail belongs to the Domain Roadmap and integrated project plan; proposed PM01-ROADMAP reference under ASM-PM01-02 |

## 5. Key capabilities at outcome level (OUT-PM01-DOMAIN-PRODUCT-BRIEF-06)

PM01 owns these platform capability outcomes. Detailed elaboration belongs to Domain PRD, proposed reference **PM01-PRD**, not an available approved source (ASM-PM01-02).

| Requirement | Priority | Outcome and rationale | Source | Acceptance |
|---|---|---|---|---|
| PM01-REQ-01 | Critical | Preserve validated intent through requirements and changes; expose assumptions and material ambiguity before irreversible work, avoiding confidently building the wrong product | SEED-01 §§3, 21.1, 32.4 | PM01-AC-01 |
| PM01-REQ-02 | Critical | Route manual and suggested concepts through formal pre-build readiness without silent prerequisite bypass, distinguishing a Build request from authorization | SEED-01 §§25, 28.1, 32.3, 46 | PM01-AC-02 |
| PM01-REQ-03 | Critical | Preserve requirements and decision context through planning, agent handoffs, creation, debugging, refactoring and impact-based revalidation, preventing change-driven intent drift | SEED-01 §§9.3, 15.2, 21.5, 32.4; supplied domain outline | PM01-AC-03 |
| PM01-REQ-04 | Critical | Make consequential actions, assumptions and tradeoffs understandable and auditable while routine work remains within authority, reducing coordination without removing control | SEED-01 §§21, 32.18–32.19 | PM01-AC-04 |
| PM01-REQ-05 | Critical | Present completion through evidence and governed handoffs, never treating a preview or builder assertion as production readiness | SEED-01 §§8.1, 9, 17, 23.1, 32.6–32.7 | PM01-AC-05 |
| PM01-REQ-06 | High | Expose evidence-based construction, testing/validation, deployment and total launch forecasts before build authorization and update them during execution, supporting informed timing decisions | SEED-01 §§27.4, 28.4, 46 | PM01-AC-06 |

**PM01-DEC-02 — Build is a readiness-gated request.** Options considered: immediate construction on selection or selection followed by formal readiness evaluation. Adopt the latter. Safe missing prerequisites are resolved autonomously; consequential decisions follow governance. An elevated-risk force-start requires authorized recording of incompleteness, rationale and compensating controls; it cannot waive production gates. Consequence: both manual and suggested concepts may receive a visible blocked/readiness disposition after selection. (SEED-01 §§21.4, 32.3, 46.)

## 6. Critical assumptions, constraints, dependencies and product questions (OUT-PM01-DOMAIN-PRODUCT-BRIEF-07)

### Assumptions and bounded dispositions

| ID | Limitation and treatment | Owner / replacement condition |
|---|---|---|
| ASM-PM01-01 | PL-REQ-ID-REGISTER has no supplied path and the visible PL folder is empty. Use stable local IDs and direct seed traces, not invented PL mappings | PM01 explicitly maps IDs when the PL register becomes available |
| ASM-PM01-02 | Required PL dependencies are absent, and canonical downstream PM01/cross-domain output links are not supplied. PM01-PRD, PM01-KPIS-SUCCESS-METRICS and PM01-ROADMAP are proposed reference labels only | PM01 replaces provisional links through explicit mapping when authoritative outputs are supplied; absent documents are not approvals |
| ASM-PM01-03 | No empirical research baseline, KPI formula standard or numeric autonomy/fidelity target is supplied. Treat unspecified measures as baseline-and-improvement measures, include failures/corrections and distinguish product type/risk | PM01 elaborates metrics with SP05 and UX01 before quantitative improvement claims |
| ASM-PM01-04 | applicability.json and workflow Appendix F/G are not supplied in this context. Conservatively retain subject-matched seed validation interfaces below, without asserting a formal applicability decision or verified appendix compliance | SP13's applicability baseline supplies definitive routing before downstream gates; absence never establishes exclusion |

### Required-source and dependency disposition

SEED-* is covered: the seed folder lists only SEED-01, read in full. SEED-01 v1.0 is normative product direction, not empirical proof that targets have been achieved. Time-sensitive rules require revalidation at applicability time (SEED-01 §§5–7). The supplied outline and inline instructions have been applied.

Each named PL dependency was requested through read_document and returned not_found; the PL folder listing is empty. Under the run's missing-source rule:

| Source/dependency | Disposition and reason |
|---|---|
| PL-REQ-ID-REGISTER | not_applicable: no supplied path or visible PL file; ASM-PM01-01 applies |
| PL-PRODUCT-VISION-BRIEF | not_applicable: named file does not exist; use SEED-01 §§1–3 directly |
| PL-PRODUCT-STRATEGY | not_applicable: named file does not exist; no PL strategy is inferred |
| PL-MASTER-PRODUCT-REQUIREM | not_applicable: named file does not exist; requirements trace directly to seed |
| PL-MVP-SCOPE-DEFINITI | not_applicable: named file does not exist; use seed MVP boundaries |
| PL-MASTER-PRODUCT-ROADMAP | not_applicable: named file does not exist; no schedule allocation is invented |
| PL-PRODUCT-PRIORITY-FRAMEWOR | not_applicable: named file does not exist; no PL priority scoring is inferred |
| PL-PRODUCT-KPIS-SUCCESS | not_applicable: named file does not exist; use seed targets and explicit measurement assumptions |
| PL-PRODUCT-CONSTRAI-GUARDRAI | not_applicable: named file does not exist; preserve seed hard constraints |
| PL-PRODUCT-DECISION-LOG | not_applicable: named file does not exist; no PL decision approval is asserted |
| PL-GREENFIE-BASELINE-EXTERNAL | not_applicable: named file does not exist; no inherited infrastructure is assumed |

### Constraints and validation interfaces

Applicable requirements, context, standards and evidence versions must remain coherent through changes. Commercial qualification, audience, forecasts, deployment recommendation and brand/IP screening are consumed as readiness inputs, not authored by PM01. Financial targets and personal-use exemption remain under SEED-01 §28 and their owning authorities. Accounts, access and critical dependencies constrain forecast certainty; fallback or approved exception remains the dependency owner's responsibility. (SEED-01 §§27.2, 32.5, 36.1, 46.)

Accepted stage behavior must remain protected while later work proceeds. Hardware strategy/reference BOM remains canonical in SEED-01 v1.0 §§38–45 and Appendix G v2.2; PM09/SE11 translate outcomes into infrastructure. No BOM, component selection or procurement assumption is introduced here. (SEED-01 §§37–39.)

| Validation authority | PM01 exposes | Returned evidence used by PM01 |
|---|---|---|
| SP13 applicability/standards | Product context, scope changes and source versions | Applicable obligations, reasoned exclusions, freshness and reviewers before readiness |
| SP14 independent assurance; PM13 | Intent, acceptance links, change rationale and builder claims | Independent findings, evidence currency and dispositions before readiness/completion claims |
| SP17 decision governance; PM03/PM12; SE23 | Alternatives, consequences, authority and decision context | Authorized decision/audit links using consistent control identities, not a parallel PM01 policy |
| SP05 analytics; UX01; NT13; SE24 | Intent, intervention, correction, completion and timing measures | Comparable user/measurement evidence consistent with privacy and data quality |
| SP15/PM15; SP16 | Lifecycle priorities, timing blockers and material cost consequences | Portfolio/capacity and spending constraints; PM01 does not set investment or financial policy |

These are reverse-validation hooks derived from SEED-01 §§33–36, not completed specialist sign-offs. Applicable specialist findings return to affected requirements and acceptance before the relevant gate can pass. Product-type, geography, minors, commerce, UGC and store triggers route through SP13 and their owners; unknown applicability is not an exclusion.

| Risk | Consequence | Treatment and owner | Trace |
|---|---|---|---|
| PM01-RISK-01 | Assumptions drift across handoffs or edits | PM01 preserves visible assumptions and impact links; PM13 independently checks acceptance | PM01-REQ-01/03; SEED-01 §§3, 9.3, 32.4 |
| PM01-RISK-02 | Preview, Build or velocity is mistaken for release authority | PM01 distinguishes request, readiness, construction and independent evidence | PM01-REQ-02/05; SEED-01 §§8.1, 32.3, 46 |
| PM01-RISK-03 | Oversight becomes constant interruption or invisible consequential autonomy | PM01 provides focused decision context; PM03/SP17 govern authority; monitor reversals/escalations | PM01-REQ-04; SEED-01 §§21, 29.3 |
| PM01-RISK-04 | Optimistic timing pressures quality gates | PM01 exposes uncertainty and revised forecasts; retain hard quality constraints | PM01-REQ-05/06; SEED-01 §§4.3, 27.4, 30 |

### Product questions and Conflicts

Clarification policy is seed-resolved: infer reversible low-risk details, surface consequential uncertainty; no question quota is invented. Build semantics are resolved by PM01-DEC-02. Unspecified metric thresholds are bounded by PM01-DEC-03 and ASM-PM01-03. Screen design, implementation and schedule questions are excluded to their owners in section 4. No question remains without a disposition for this brief's purpose.

**Conflicts:** No in-scope contradiction was identified against SEED-01 or the supplied outline. Consistency with absent PL outputs cannot be claimed. No specialist authority, seed quality gate or hardware constraint is overridden. Future material cross-domain contradictions require workflow reconciliation before the affected readiness claim, not silent resolution by PM01 (SEED-01 §§26.5, 36).

## 7. Success definition and Domain KPI links (OUT-PM01-DOMAIN-PRODUCT-BRIEF-08)

Success is an understandable, governed creation/change journey preserving intent, authority and independently evidenced quality. The platform north star remains “the percentage of lifecycle work completed autonomously while still meeting intended outcomes and all applicable production-quality requirements.” (SEED-01 §29.1.)

| Acceptance ID | Decidable outcome | Accountable evidence interface |
|---|---|---|
| PM01-AC-01 | Delivered behavior and requirements trace to validated intent; material inferred assumptions are visible/changeable; consequential ambiguity is resolved before irreversible work | PM01 with UX01/PM13; verifies PM01-REQ-01 |
| PM01-AC-02 | Both manual and suggested Build journeys invoke readiness; prerequisites do not silently pass; any force-start has the authorized elevated-risk record and material edits trigger affected revalidation | PM01 with PM03/SP13/SP17 and qualification owners; verifies PM01-REQ-02 |
| PM01-AC-03 | Creation, debugging and refactoring preserve objective-to-change-to-evidence links across agent handoffs and human edits; affected obligations are revalidated without silently redefining unaffected promises | PM01 with PM07/PM13/PM17 and SE02; verifies PM01-REQ-03 |
| PM01-AC-04 | Operator evidence demonstrates comprehension of consequential assumptions, alternatives, impacts and rationale; routine autonomy stays within policy and maximum modes have deliberate additional authorization | UX01 comprehension evidence and PM03/PM12/SP17 audit evidence; verifies PM01-REQ-04 |
| PM01-AC-05 | Creation and change evidence covers all four MVP categories; production-intended changes pass non-production and independent validation; critical defects block release and previews cannot substitute for readiness | PM04/PM05 coverage, PM13/SP14 findings and PM08 promotion evidence; verifies PM01-REQ-05 |
| PM01-AC-06 | Every app displays construction, testing/validation, release/deployment and total launch timing, likely date/range, confidence and dependencies before authorization; estimates update and use relevant build history/calibration error after the first completed app | PM01 with PM08 and estimate contributors; verifies PM01-REQ-06 |

These are brief-level acceptance outcomes for elaboration, not detailed test scripts or claims of completed validation. Sources: SEED-01 §§3, 8–9, 21, 23–24, 27.4, 32, 46.

**Domain KPIs / Success Metrics — PM01-KPIS-SUCCESS-METRICS** is a proposed downstream link under ASM-PM01-02, not an approved source. It owns formulas, observation windows, metric baselines and targets. PM01 hands off intent fidelity, valid autonomous completion, intervention time, unnecessary escalation, reversals, quality, velocity, blockers, forecast calibration and task/comprehension evidence. SP05 supports measurement integrity; UX01 owns user evidence; PM13/SP14 supply independent quality results. (SEED-01 §§18, 29, 34.)

Seed numeric/qualitative targets retain the qualifications in section 3. No new fidelity, autonomy, usability or escaped-defect numerical target is established. Failed or missing evidence is not success; hard-gate failures cannot be averaged away by improved KPIs. Comparisons require comparable risk/product context and explicit uncertainty (ASM-PM01-03; SEED-01 §17).

## Self-review and revision disposition

| Criterion | Disposition |
|---|---|
| QC-PM01-DOMAIN-PRODUCT-BRIEF-01 | covered: material assertions trace to the seed, supplied scope or stable local requirement/decision/assumption IDs; source limitations are explicit in section 6 |
| QC-PM01-DOMAIN-PRODUCT-BRIEF-02 | covered: authority boundaries and reverse-validation interfaces are explicit; Conflicts records comparison limits without fabricating absent approvals |
| QC-PM01-DOMAIN-PRODUCT-BRIEF-03 | covered: version 2 matches this REVISE invocation; requirement/decision/assumption/risk/acceptance IDs retain their previous meanings |
| QC-PM01-DOMAIN-PRODUCT-BRIEF-04 | covered: owners, boundaries, targets and their qualifications, evidence outcomes and bounded missing-source dispositions support independent consumption as a brief |

Review correction: the supplied finding, “header version 1 != 2,” is corrected in the unified header. This revision supersedes PM01-PRODUCT-BRIEF version 1 at the same target (prior SHA c597ba4df2e53c71a3aa64d21bd1e8124e17f55f). It also aligns provenance with this invocation: removes the predecessor's Stage-0/AUTHOR statements and reliance on an unprovided STD-NE-01 routing overlay, and records all required missing PL dependencies explicitly. Product outcomes and stable local IDs are preserved; no substantive seed policy is superseded. The eight outline criteria are covered in order and the three exclusions are reasoned in section 4. Author self-review passes scope, internal consistency, available-dependency consistency and brief-level downstream readiness; this is not build or release authorization.
