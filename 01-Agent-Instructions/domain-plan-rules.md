# Domain implementation-plan rules (01-Agent-Instructions/domain-plan-rules.md) — SE01–SE25, Stage 14

You are producing your domain's implementation plan: the executable sequence by which your approved designs become
software. Everything in author-rules.md and author-engineering.md applies. In addition:

## The guideline (operator standard STD-IMPL, §4 "How to author the implementation plan")
- The section is in your context in full. Its outcomes are listed as `GL-4-nn` criteria. **Outcomes and intent are fixed.**
- Dispose every `GL-4-nn` as `covered` or `adapted` in `outline_coverage`. `not_applicable` does not exist for them.
- `adapted` is allowed only where the guideline's *means* cannot be applied to this platform as written. It changes how the
  outcome is reached, never what the outcome is. Every adaptation is recorded twice, identically:
  1. in the completion event: `"adaptations": {"GL-4-nn": {"changed": "...", "reason": "...", "outcome_preserved_by": "..."}}`
  2. in the document, section `## Guideline adaptations`, table `| outcome | what changed | why this platform required it | outcome preserved by |`
  A missing or incomplete record rejects the completion; an adaptation that alters the outcome is a blocking review finding.
- No adaptations ⇒ still include the section with an empty table.

## Plan format (format spec; validated by machine)
- Front matter adds `requires:` and `provides:` (contracts with versions and milestones) and `format: implementation-plan-format v1`.
- Sections in order: Scope; Stack (domain-owned choices; shared ones cite `EL-IMPL-STACK@<version>`); Audit — conflicts,
  errors, gaps; Resolved assumptions; Module map; Lifecycle reference (if you own a stateful unit); Steps; Guideline
  adaptations; Coverage.
- Steps: ids `<ROLE>-001…` continuous; each has `produces`, `depends_on` (own step ids, `CONTRACT:<id>@<v>` or
  `MILESTONE:<name>` — never another domain's step), `verify` (asserts behaviour, not existence), `flag` (impl |
  decision | unsure), `risk` (yes for auth, trust boundaries, state machines, secrets, destructive/irreversible ops,
  migrations, contract schemas), `phase` (canonical key), `requirements`. No step references an artifact not yet produced.
- Scope = 100 % of `<ROLE>-REQ-*` resolved requirements; the Coverage table maps each to at least one step. No deferred bucket.
- Cross-domain audit rows you cannot settle get `scope: cross-domain` and a safe reversible default; EL resolves them.

## Sources
Your approved domain documents (all of them), `EL-CONTRACT-REGISTER`, EL's architecture and stack documents, the seeds,
the guideline §4. Cite the design document id behind every step.

## Hardware readiness work packages (SE11, ENV-DEC-017)
SE11's plan includes, where its hardware documents make them applicable, steps for: inventory verification against the
approved specification classes; firmware/BIOS/driver baseline; physical installation; storage and network configuration;
UPS monitoring and graceful-shutdown integration; telemetry/health integration; capacity/performance validation; physical
failure/resilience verification. Each cites `SE11-PHYSICAL-INFRASTR-HARDWARE`, `SE11-HARDWARE-CAPACITY-SIZING` or
`SE11-POWER-COOLING-RACK`; facility/electrical validation by qualified professionals is a `MILESTONE:` dependency, never a
step SE11 performs. Other domains depend on hardware readiness only through `MILESTONE:` or `CONTRACT:` dependencies.
