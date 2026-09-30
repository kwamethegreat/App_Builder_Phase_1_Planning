# Applicability decision rules (01-Agent-Instructions/applicability-rules.md)

You are deciding which conditional specialist domains of the workflow apply to **the platform being documented** — the
AI-powered application-development and deployment platform described in the seed documents — not to any single
application that platform may later generate. A domain applies when the platform itself, or the capabilities the
platform is required to provide to the applications it generates, fall within that domain's trigger.

Inputs: every seed document (complete), the Stage-0 Product Lead package, and the `conditional_domains` list in the target block.

Output: your document must contain exactly one decision table with one row per conditional domain:

| domain | determination | evidence |
|---|---|---|
| SP01 | applies | SEED-01 §3.2 "…generated applications must accept card payments…" |
| SP07 | does_not_apply | SEED-01 §1 scope excludes hardware; no seed mentions embedded targets |
| SP12 | unknown | no seed states whether generated apps may target users under 18 |

Rules:
1. `determination` is one of `applies`, `does_not_apply`, `unknown`. Nothing else.
2. `applies` and `does_not_apply` must cite the seed or source id and the passage that supports the determination.
3. Use `unknown` only when the corpus is silent; say what was missing. `unknown` is treated as `applies`.
4. Do not infer from the absence of a feature in the platform that its generated applications will not need it.
5. Every row's evidence must be traceable by the reviewer to the cited document.
6. This task is authored under author-rules.md: the document also carries the unified header and an ordinary completion
   event. Put the table in a section headed "## Applicability decision"; list every conditional domain from the target
   block's `conditional_domains` — the machine rejects a table with a missing row, an unknown determination word, or an
   `applies`/`does_not_apply` row whose evidence cites no seed or document id, and you are re-invoked with the reason.
7. After peer review passes, the table is frozen for the whole run: `unknown` runs the domain. Decide carefully; you will
   not be asked again.
