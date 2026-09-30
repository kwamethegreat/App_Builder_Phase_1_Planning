# Peer review rules — engineering (01-Agent-Instructions/review-engineering.md) — principal REVIEWER-EN

Everything in review-non-engineering.md applies (procedure, finding types, event shape, severity rules, re-review rule).
In addition, as an engineering reviewer you verify:

- **Buildability**: a competent engineer could implement from this document plus its cited contracts without asking the
  author. Vague mechanisms, missing failure behaviour or unstated data ownership are `downstream_unusable` (major).
- **Contract discipline**: every consumed interface cites a contract id and owner; every provided contract is registered;
  no domain restates another's schema or API. Violations are `scope` or `dependency_inconsistency`.
- **Consistency with EL architecture**: boundaries, shared stack choices and cross-domain rules in EL's documents are
  honoured; deviations need an ADR that cites the EL decision it departs from.
- **NFR traceability**: quality attributes map to measurable NFR ids; security/privacy controls cite their control ids.
- **Greenfield discipline**: no presumed existing infrastructure; provisioning justified; portability designed in.
- **Implementation plans and the compiled plan** (Stage 14) — additionally:
  - every `GL-` guideline outcome in the plan's criteria is disposed `covered` or `adapted`; a plan that treats any as
    not applicable, or omits one, is `guideline_deviation` (blocking);
  - every `adapted` outcome has a row in `## Guideline adaptations` whose *what changed* alters only the means, whose
    *why* is a property of this platform (not preference), and whose *outcome preserved by* demonstrably reaches the
    original outcome — otherwise `guideline_deviation` (blocking);
  - steps are concrete, ordered, verifiable (behavioural `verify`), with `produces`, `depends_on`, `flag`, `risk`;
    cross-domain dependencies only via contracts/milestones; 100 % of the domain's resolved requirements covered;
  - the compiled plan carries every domain adaptation and every domain step with origin ids, in canonical phase order.
- Finding type `guideline_deviation` exists only for plan documents and is always blocking.
- **Hardware planning chain** (ENV-DEC-017) — for `SE11-PHYSICAL-INFRASTR-HARDWARE`, `SE11-HARDWARE-CAPACITY-SIZING`,
  `SE11-POWER-COOLING-RACK` and every document that consumes them: a BOM restated or altered without citing the seed
  section and version is `source_gap` (major) or, when invented, `unsupported_addition` (blocking); a BOM item without an
  engineering disposition, or a substitution without reason and impact, is `outline_gap` (major); procurement, vendor or
  price content is `scope` (major); sizing to the maximum listed configuration without workload evidence is
  `unsupported_addition` (major); a consumer that duplicates SE11's hardware detail instead of citing it is `scope`; a
  hardware assumption that contradicts an SE11 disposition is `dependency_inconsistency` (blocking); common-mode failure
  domains left unowned are `downstream_unusable` (major). No new finding types exist for this chain.
