# Lead compilation rules (01-Agent-Instructions/lead-compilation-rules.md) — EL, the compiled implementation plan

You are compiling the platform's single implementation plan from the 25 approved domain plans. Everything in
author-rules.md, author-engineering.md and domain-plan-rules.md applies, with these differences:

## The guideline, in full
- The entire operator guideline (all sections) is in your context; its outcomes are `GL-<section>-nn` criteria. You apply
  every section when putting the plan together, not only §4. Dispose every outcome `covered` or `adapted`.
- You make the final adaptations. Carry every domain adaptation into your `## Guideline adaptations` table: keep it as
  written, or replace it with your own adaptation of the *same* outcome and say so in *what changed*. Dropping one is
  blocked by the validator. Outcomes and intent remain the operator's; you adapt means only.

## Compilation, not rewriting
- Preserve every domain step with its origin id (`SE14-007` stays visible), renumbered continuously in canonical phase
  order; a step never precedes a step it depends on, across phases and domains.
- Resolve every cross-domain audit row in your audit section with a decision and rationale (grounds order: security >
  correctness > data integrity > maintainability > least surprise), or a flagged safe default.
- Contracts: every `CONTRACT:<id>@<v>` dependency resolves to exactly one providing step; duplicates or missing providers
  are yours to fix by decision (recorded as `EL-DEC-nn`), not by deleting the dependency.
- Shared stack, boundary rules and enforcement come from your own EL documents; domain plans that restated them are
  corrected to cite them.
- Add nothing the domain plans and your EL documents do not support; where a gap between domains exists, add the
  minimal integrating step, owned by the domain whose artifact it touches, flagged `decision`.
- Hardware readiness (ENV-DEC-017): SE11's hardware work packages and their milestones are preserved and ordered before
  every step that needs installed capacity; no hardware readiness blocker is hidden from the critical path; an open
  `ESCALATE ARCHITECTURE IMPACT` disposition in an SE11 document is a cross-domain audit row you resolve, not a step.

## Output
- One document, `EL-COMPILED-IMPL-PLAN`, in the format spec's shape (same sections as a domain plan, whole-platform scope).
- Coverage: every domain's resolved requirements → steps; every provided contract → one provider; every milestone defined.
- Completion event as for authors, plus `adaptations` for every `adapted` outcome across all sections.
- The deterministic validator and the engineering peer reviewer run after you; their findings return to you as a
  revision. The approved commit of this document is the platform's authoritative plan.
