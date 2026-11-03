# Applicability decision rules (01-Agent-Instructions/applicability-rules.md)

You are deciding which conditional specialist domains of the workflow apply to **the platform being documented** — the
AI-powered application-development and deployment platform described in the seed documents — not to any single
application that platform may later generate. A domain applies when the platform itself, or the capabilities the
platform is required to provide to the applications it generates, fall within that domain's trigger.

Inputs: the Stage-0 Product Lead package — the Master Requirement ID Register (`PL-REQ-ID-REGISTER`, which carries every
seed requirement with its seed section) and the PL Stage-0 documents — and the `conditional_domains` list in the target
block. You do not receive the seeds; the register is the corpus (ENV-DEC-018).

Output: your document must contain exactly one decision table with one row per conditional domain:

| domain | determination | evidence |
|---|---|---|
| SP01 | applies | PL-REQ-ID-REGISTER PL-REQ-042 "generated applications must accept card payments" (SEED-01 §3.2) |
| SP07 | does_not_apply | PL-PRODUCT-CONSTRAI-GUARDRAI PL-CON-03 scope excludes embedded targets; no register row mentions them |
| SP12 | unknown | no register row states whether generated apps may target users under 18 |

Rules:
1. `determination` is one of `applies`, `does_not_apply`, `unknown`. Nothing else.
2. `applies` and `does_not_apply` must cite the PL document id and the requirement/decision/constraint id (and quote it)
   that supports the determination; the register's seed section reference may be added for traceability.
3. Use `unknown` only when the package is silent; say what was missing. `unknown` is treated as `applies`.
4. Do not infer from the absence of a feature in the platform that its generated applications will not need it.
5. Every row's evidence must be traceable by the reviewer to the cited document.
6. This task is authored under author-rules.md: the document also carries the unified header and an ordinary completion
   event. Put the table in a section headed "## Applicability decision"; list every conditional domain from the target
   block's `conditional_domains` — the machine rejects a table with a missing row, an unknown determination word, or an
   `applies`/`does_not_apply` row whose evidence cites no document or requirement id, and you are re-invoked with the reason.
7. After peer review passes, the table is frozen for the whole run: `unknown` runs the domain. Decide carefully; you will
   not be asked again.
