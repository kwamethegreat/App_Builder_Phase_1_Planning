# Author rules (01-Agent-Instructions/author-rules.md) — authoring and revising a document

## Procedure
1. Read the RUN CONTEXT: `task_id`, `document_id`, `write_target`, `version_to_write`, `pass` (AUTHOR or REVISE).
2. Everything your context marks *included* — rules, outline criteria, required sources, dependencies — is already in
   front of you in full: do not re-read it. Read with `read_document` only what the context lists as *not included
   (read on demand)*, and a seed from the seed index when a register row you rely on points to a section whose original
   wording or data you need. Use `list_documents` on your own folder to see what you have already produced.
3. If `pass` is REVISE: read the previous review findings in your context first. Every blocking and major finding must be
   corrected; say where. Minor findings: correct or justify. Then re-read the current file with `read_document` to obtain
   its `sha` for `expected_sha`.
4. Plan the document against the outline: one section (or explicit disposition) per criterion, in the standard's order.
5. Write the document. Then self-review it against the completion checks below before writing it — this is the only review
   you control; the peer reviewer sees the same checklist.
6. `write_document` to `write_target`, with the unified header — in one call, or assembled in parts: the first call
   writes header + first section, each later call uses `mode: "append"` with the previous call's `sha` and carries only
   the new section. The file is complete and final before step 7.
7. `report_agent_status` once with the completion event.

## Completion event (the machine checks every field)
```
{
  "status": "complete",
  "task_id": "<task_id>", "document_id": "<document_id>", "version": <version_to_write>,
  "outline_coverage": {"<criterion id>": "covered" | "not_applicable", ...},   // EVERY criterion id from your context
  "source_coverage":  {"<required source id>": "covered" | "not_applicable", ...},  // EVERY required source id
  "requirement_ids_used": ["<ids you relied on or minted>"],
  "checks": {"scope": "pass", "internal_consistency": "pass", "dependency_consistency": "pass", "downstream_readiness": "pass"},
  "unresolved_issues": []
}
```
- `not_applicable` needs a one-line reason inside the document, in the section where the criterion would have been.
  Guideline outcomes (`GL-…`, implementation plans only) never take `not_applicable` — see domain-plan-rules.
- `checks` may only be `pass`. If a check would fail, fix the document; a failing check is an incomplete task.
- An event that omits a criterion, a source, or has non-empty `unresolved_issues` is rejected and you are re-invoked with
  the validator's findings. Two rejections end the task as failed. Get it right the first time.

## Writing rules
- Title = the document class name. Headings follow the outline criteria; keep their ids visible (e.g. "## 3. Actors (OUT-…-03)").
- Tables for inventories, requirements, risks, dependencies; prose for rationale. Diagrams as text (Mermaid) only when they
  remove ambiguity.
- Every requirement, decision, assumption, risk and acceptance criterion you introduce gets a stable id: `<ROLE>-REQ-nn`,
  `<ROLE>-DEC-nn`, `ASM-<ROLE>-nn`, `<ROLE>-RISK-nn`, `<ROLE>-AC-nn`.
- Length is whatever the criteria need — not shorter, not padded.
- The exclusions (`BND-…`) in your context name content that belongs to another document. Reference, do not include.
- Stage-0 register tasks (`PL-REQ-REGISTER-G01..G04`, `PL-REQ-ID-REGISTER`) add `seed_coverage` to the completion event
  and follow the Stage-0 rules in author-non-engineering.md. Compilation parts (`EL-COMPILED-PART-*`) follow
  lead-compilation-rules.md.
