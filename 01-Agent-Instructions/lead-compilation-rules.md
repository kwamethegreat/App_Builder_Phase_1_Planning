# Lead compilation rules (01-Agent-Instructions/lead-compilation-rules.md) — EL, the compiled implementation plan in parts

You are compiling the platform's single implementation plan from the 25 approved domain plans. Everything in
author-rules.md, author-engineering.md and domain-plan-rules.md applies, with these differences. Since ENV-DEC-021 the
compiled plan is produced as **five parts**, each a task of its own that you author and that is peer-reviewed; the
orchestrator then **assembles** `EL-COMPILED-IMPL-PLAN` from them deterministically and runs the Stage-14 validator on the
whole. You never write the assembled document yourself.

## The frame (`EL-COMPILED-PART-00-FRAME`)
- Every section of the compiled plan except `## Steps`: Scope (union of the 25 domain scopes), Stack (shared choices from
  EL-IMPL-SCOPE-STACK; domain choices cited), Audit (every cross-domain row of every domain audit resolved — grounds:
  security > correctness > data integrity > maintainability > least surprise — or a flagged safe default, each as
  `EL-DEC-nn`), Resolved assumptions, Module map (from EL-IMPL-MODULE-MAP), Lifecycle reference (EL-IMPL-LIFECYCLE),
  `## Guideline adaptations`, `## Coverage` (`| requirement | steps |` for every domain's resolved requirements, with
  origin step ids, taken from the domain plans' coverage tables).
- The entire operator guideline is in your context; its outcomes are `GL-<section>-nn` criteria. Dispose every one
  `covered` or `adapted`. Carry every domain adaptation into your table — kept, or replaced by your own adaptation of
  the *same* outcome and said so in *what changed*; dropping one is blocked by the validator.
- Your context holds each domain plan **without its step blocks**; the steps are compiled in parts 01–04. No step block
  may appear in the frame.

## The step parts (`EL-COMPILED-PART-01..04`)
- Each part owns four canonical phases (01: foundation, local-env, contracts, data · 02: core-domain, execution-path,
  integration, capability · 03: error-logging, observability, security, performance · 04: testing, ci, docs, acceptance).
  Your context holds, from every domain plan, **only the step blocks of your phases**, plus a step index of every step in
  every plan (id | phase | title | provides | depends_on).
- Output: one `## Steps` section holding every one of those blocks — none omitted, none from another phase, none
  invented — in canonical phase order, then dependency order; origin ids (`SE14-007`) stay the ids; a step never
  precedes a step it depends on within the part; dependencies on steps in other parts are left as their ids (the index
  shows them) and are checked on the assembled whole.
- Contracts: every `CONTRACT:<id>@<v>` dependency must resolve to exactly one providing step in the whole plan; a missing
  or duplicated provider is yours to fix by decision (`EL-DEC-nn`, recorded in the frame's audit), never by deleting the
  dependency. Where two domains meet without a contract or milestone, add the minimal integrating step, owned by the
  domain whose artifact it touches, flagged `decision`.
- Hardware readiness (ENV-DEC-017): SE11's hardware work packages and milestones precede every step that needs installed
  capacity; an open `ESCALATE ARCHITECTURE IMPACT` disposition is a cross-domain audit row (frame), not a step.

## Assembly and what comes back to you
- When all five parts have passed review, the orchestrator writes `EL-COMPILED-IMPL-PLAN` = frame with `## Steps` inserted
  (parts 01–04 in order) and validates it whole (providers, cycles, phase order, coverage, adaptations). A blocking
  problem returns to the part that owns the offending step or section as a **revision with the validator's findings**:
  fix that part only, keep origin ids, do not touch content other parts own. The assembled plan then has its own
  engineering review; its findings return the same way.
- Write each part with the unified header (`id` = the part id, `owner: EL`); assemble a long part with `mode: "append"`.
  Completion event as for authors; the frame adds `adaptations` for every `adapted` outcome. The approved commit of the
  assembled `EL-COMPILED-IMPL-PLAN` is the platform's authoritative plan.
