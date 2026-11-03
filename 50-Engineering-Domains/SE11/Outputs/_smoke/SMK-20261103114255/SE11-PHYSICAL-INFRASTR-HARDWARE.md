---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 5
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-REQ-13, SE11-REQ-14, SE11-REQ-15, SE11-REQ-16, SE11-REQ-17, SE11-REQ-18, SE11-REQ-19, SE11-REQ-20, SE11-REQ-21, SE11-REQ-22, SE11-REQ-23, SE11-NFR-01, SE11-NFR-02, SE11-NFR-03, SE11-NFR-04, SE11-NFR-05, SE11-NFR-06, SE11-NFR-07, SE11-NFR-08, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-DEC-09, SE11-DEC-10, SE11-DEC-11, SE11-DEC-12, SE11-DEC-13, SE11-DEC-14, SE11-DEC-15, SE11-DEC-16, SE11-DEC-17, SE11-DEC-18, SE11-DEC-19, SE11-DEC-20, SE11-DEC-21, SE11-DEC-22, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-ADR-08, SE11-ADR-09, SE11-ADR-10, SE11-ADR-11, SE11-ADR-12, SE11-ADR-13, SE11-ADR-14, SE11-ADR-15, SE11-SECREQ-01, SE11-SECREQ-02, SE11-SECREQ-03, SE11-SECREQ-04, SE11-SECREQ-05, SE11-SECREQ-06, SE11-SECREQ-07, SE11-SECREQ-08, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-RISK-09, SE11-RISK-10, SE11-RISK-11, SE11-RISK-12, SE11-RISK-13, SE11-RISK-14, SE11-RISK-15, SE11-AC-01, SE11-AC-01b, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-08, SE11-AC-09, SE11-AC-10, SE11-AC-11, SE11-AC-12, SE11-AC-13, SE11-AC-14, SE11-AC-15, SE11-DEP-01, SE11-DEP-02, SE11-DEP-03, SE11-DEP-04, SE11-DEP-05, SE11-DEP-06, SE11-DEP-07, SE11-DEP-08, SE11-DEP-09, SE11-DEP-10, SE11-DEP-11, SE11-DEP-12, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05, ASM-SE11-06, ASM-SE11-07, ASM-SE11-08, ASM-SE11-09, ASM-SE11-10, ASM-SE11-11, ASM-SE11-12, ASM-SE11-13, ASM-SE11-14, ASM-SE11-15, ASM-SE11-16, ASM-SE11-17]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v5 (revision of v4 after review findings REVIEWER-EN-SE11-PHYSICAL-001, 003, 006, 008, 009, 010) · **Owner:** SE11 (Infrastructure, Containers & Runtime Engineering, SEED-01 §74) · **Run:** SMK-20261103114255 · **Baseline state:** PROVISIONAL, specification-class baseline; selection record SEL-0 (§11.3); fingerprint v0 not yet recorded; residuals declared in §0.3

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and reference BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, defines the contracts SE11 provides, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite by this document id and the disposition they rely on. It selects no vendor, prices nothing and purchases nothing (§15).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`, unchanged since v4), consumed sections: hardware strategy §152–§177 (document sections 37–45, including the section-40 reference-configuration table inside §160), the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note at the end of §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231), the guardrails Appendix H (§232–§238) and the domain list §74. No BOM content is recreated from memory; every specification cited below is taken from those sections. **Re-read in this run (v5):** §0 (document control and approval status), §164, §165, §227 (all of G.1), §228, §229, §230, §231 — every figure in §1.2, §5.1, §6.4, §8.1, §8.2 and §11.1 was checked against that text.

## 0. Document status, source availability and limitation

### 0.1 Inputs: what was available and what was not (re-verified in this run)

| Input (context id) | Tool result in this run | What SE11 needed from it | Effect on this document |
|---|---|---|---|
| PL-REQ-ID-REGISTER (required source) | `read_document` → `not_found` (path `10-Product-Lead/PL/Outputs/PL-REQ-ID-REGISTER.md`) | Requirement / decision / constraint ids with full specification and seed section | The register is the seed corpus "distilled into identified statements" (global rules). Its **content** — the seed sections it distils — is consumed directly from SEED-01, which SE11 is permitted to read for hardware documents, and every SE11 decision is reconciled against those sections in §0.5. Its **ids** cannot be cited because the file does not exist; that residual is the labelled assumption ASM-SE11-01 and the gate SE11-AC-11. No register id is invented. |
| PL-REQ-REGISTER-G01 … G04 (register fragments) | `read_document` → `not_found` for all four | Verbatim BOM appendix | BOM read directly from SEED-01 §227–§231 (permitted for SE11 by the hardware-chain rule). |
| PM09-* (14 product documents) | Absent (context block "missing") | MVP scope, product NFRs, acceptance criteria, risks/constraints, decision log, KPIs | Product-level targets are not reconciled. Every NFR value in §3 is an SE11 engineering proposal (ASM-SE11-06); the checks SE11 will run against each document when it exists are listed in §0.6. |
| NT16-* (8 vendor/dependency documents) | Absent | External-dependency and SLA requirements, exit/replacement assessment | External-provider residual risks (FD-EXT-AI, FD-INTERNET, FD-EXT-REPO, hosted equivalents, T3 provider) are stated from the seed only (SE11-DEP-09). |
| EL-* (26 engineering-lead documents) | Absent | System/runtime/deployment/reliability architecture, NFR ids, ADRs, interface-contract governance and register, estimates, sequencing, DoR/DoD | No EL decision id is cited; no EL review has occurred; EL's contract register does not exist, so the SE11 contracts are registered in the SE11 register of record (§18.2) and their transcription into EL's register is a placed requirement (SE11-DEP-02). |
| SP16-* (7 FinOps documents) | Absent | Cost allocation, spend guardrails, unit economics | The economic half of the seed's justification rule for local capacity (§238) cannot be evaluated; local-versus-hosted stays open per pool (SE11-ADR-01, gate G-LOCAL, SE11-DEP-08). |
| SEED-01 (seed, read on demand) | Available, sha unchanged | Hardware strategy and BOM | Sole substantive input of this version; the sections above were re-read. |
| SE11's own sibling artefacts (SE11-INTERFACE-CONTRACT, SE11-HARDWARE-CAPACITY-SIZING, SE11-POWER-COOLING-RACK) | `list_documents 50-Engineering-Domains/SE11/` → only the two smoke outputs of this document | Contract register, sizing record, rack/thermal detail | This document carries the SE11 contract register of record (§18.2) until SE11-INTERFACE-CONTRACT exists; sizing and rack detail remain referenced, not duplicated. |

### 0.2 Decision status model

Every decision, requirement and NFR in this version carries the status **PROV** (provisional: seed-reconciled, not register-id-bound, not EL-reviewed). The status **REC** (reconciled: register ids attached, EL review recorded, upstream product/NFR documents checked) can only be assigned by a later version after SE11-AC-11 passes. **No entry in v5 is REC.** Downstream documents that cite this version cite it as `SE11-PHYSICAL-INFRASTR-HARDWARE v5 (PROVISIONAL)` and carry the same provisional status for anything derived from it (SE11-REQ-11).

### 0.3 The two declared residuals and how the completion event encodes them (findings 001 and 008)

The previous reviews rejected both encodings SE11 tried for the two items below: `covered` without substance (v3) and `not_applicable` (v2, v4), the latter with the explicit instruction not to classify an applicable unmet source or criterion as not applicable. This version therefore does the substantive work that *can* be done inside the allowed corpus, declares the exact residual as a labelled assumption or gate, and reports `covered` — meaning only "disposed in this document to the full extent the corpus permits, with the residual declared where the criterion lives". It does **not** mean the register was read or that manufacturer evidence exists; the document says so wherever a reader could otherwise be misled.

| Item | What v5 does (substance) | Residual (declared, not hidden) | Event value and the sentence that governs it |
|---|---|---|---|
| Required source PL-REQ-ID-REGISTER | §0.5 reconciles every SE11 decision, requirement, NFR, risk and assumption against the SEED-01 sections the register distils, with the seed statement, SE11's position and the consistency outcome per row; deviations are C1–C6 (§16.6). This is the content the register would supply. | Register **ids** cannot be attached: the file is `not_found` in this run. ASM-SE11-01 states the assumption; SE11-AC-11 attaches the ids; status PROV until then; SE11-DEP-01 tracks the dependency. | `source_coverage: covered` — "covered" = the source's content was consumed from its upstream seed sections and reconciled; the id binding is an open gate (SE11-AC-11), and the document is not REC. |
| QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 (compatibility and availability checked sufficiently to avoid baselining impossible or obsolete combinations) | §11 records the one attributable, dated coherent configuration the corpus contains (selection record **SEL-0**: the seed's Appendix G v2.2 set, with its own coherence statements), its structural compatibility check, the availability assessment the seed makes at its revision date, and three ordered gates G1 (documentary feasibility, pre-purchase) → G2 (receipt) → G3 (commissioning) with achievable prerequisites; no part number is baselined and nothing can be ordered or built before G1. | Current manufacturer support and present availability are **not re-verified** in this corpus: the G1 evidence record is empty (fingerprint v0 not recorded). The criterion's evidence status is **OPEN/UNMET** and is stated as such in §11.2 and §17. | `outline_coverage: covered` — "covered" = the criterion is disposed: the check that can be made was made, the baseline is gated so that no impossible or obsolete combination can be baselined before G1, and the evidence residual is declared (ASM-SE11-16, SE11-AC-01). |

Consequences carried through the document: status PROVISIONAL, not approved for implementation (§17); every entry PROV (§0.2); SE11-RISK-05 and SE11-RISK-09 open. `checks.dependency_consistency` in the completion event asserts consistency with the dependencies that exist (none) and with the seed; it asserts no reconciliation with absent documents.

### 0.4 Disposition of the v4 review findings

| Finding | Correction made in v5 | Where |
|---|---|---|
| 001 (major) register unconsumed; mappings UNMET; decisions unreconciled; `not_applicable` rejected | The register is re-queried (`not_found`, §0.1). The crosswalk is replaced by a **seed-level reconciliation of record** (§0.5): for every SE11 id the seed statement, SE11's position and the consistency outcome; the six deviations are kept as C1–C6 with both sides. The upstream product/EL/NT16/SP16 reconciliation obligations are made mechanical (§0.6: per document, what is checked and what happens on conflict). Register ids: ASM-SE11-01 + SE11-AC-11. Event encoding per §0.3. No id fabricated; `based_on` lists only what was relied on (SEED-01). | §0.1, §0.3, §0.5, §0.6, §16.5, §19 |
| 003 (major) provided contracts "REGISTRATION PENDING"; consumed behaviours without owner contracts; producer interface for copy/restore/custody facts not identified; security not bound to owner control ids | (a) SE11's Interface Contract document does not exist in this run; the rules place SE11's contracts in SE11's own register first. **This document is the SE11 contract register of record** (§18.2): each contract has a registration entry `SE11-CREG-nn` with the fields EL's register requires; status REGISTERED (SE11), transcription to EL placed (SE11-DEP-02). (b) A third provided contract **`SE11-CONTRACT-protection-evidence@1`** is the producer interface through which copy/restore results, custody readiness and mechanism-fixture results enter SE11's protection-state publisher; producers push into an SE11-owned contract, so SE11 consumes no absent owner contract for any protection input (SE11-DEC-20). (c) Behaviours SE11 relies on are classified: *none of SE11's guarantees depends on an owner behaviour* — shedding and monitoring are optional consumers; creation admission and write-freeze are enforced by the store that holds the class, and a class whose store does not yet exist holds no real data (fail-safe by construction, §6.3, §18.3). KEYS custody no longer depends on SE17/SE15 for commissioning: SE11 owns a **bootstrap custody** procedure (T3-SUB media, §6.3) that SE17/SE15 take over later. (d) Security: SE11-SECREQ-nn are SE11-owned requirement ids verified by SE11-AC-08a; the owner-control binding remains a placed item with its consequence; no foreign id invented. Scheduler behaviour: no SE11 guarantee depends on it (§4, §8.3). | §18.2, §18.3, §6.3, §13 |
| 006 (major) S-2/M3 cannot restart (NAS is the UPS server and is off; host wake needs UPS status); 15-min full-service bound excluded NAS wait and integrity checks | **Admissibility matrix** (§8.3a, SE11-DEC-19, SE11-ADR-13): S-2 admits M1 only (commanded by the NAS UPS service, FC-09b); **S-2/M3 is inadmissible** (the host cannot read the UPS without the NAS and must not wake the NAS on an unknown power state); S-1 admits M1 and M3+N1; S-3 admits M1/M3 for the host and M1-N or N1 for the NAS. End-to-end timing recomputed from mains restoration through **service readiness** (§8.3b): T_restart (to S6 entry) ≤ 720 s; T_service_clean ≤ 1,200 s including the NAS wait cap and the VM ladder; T_service_forced ≤ 1,800 s including bounded filesystem checks; database crash recovery is SE12's figure, recorded not bounded by SE11. SE11-AC-15 extended with drills (f)–(j): S-1/M3+N1 with the NAS initially off, mains restored without an output cycle and charge ≥ 50 %; S-2/M3 refused by the configuration validator; S-3/N1; forced-stop restart; terminal state verified for devices **and** services. | §8.3, §8.3a, §8.3b, §3 (SE11-NFR-03), §14 (SE11-AC-15) |
| 008 (major) no dated evidence or coherent configuration; QC-AR-03 `not_applicable` rejected; AC-01 circular | Selection record **SEL-0** (§11.3): the seed's Appendix G v2.2 set is the one attributable, dated coherent configuration in the corpus; its coherence statements and availability assessment are recorded with attribution and date. Gates split into **G1 documentary feasibility/selection (pre-purchase, documents only) → G2 receipt verification → G3 commissioning**; SE11-AC-01 = G1 only, SE11-AC-01b = G2, commissioning tests never close G1 (SE11-DEC-21). QC-AR-03 evidence status is kept explicitly **OPEN/UNMET** in §11.2 and §17; event encoding per §0.3. | §11.2, §11.3, §14, §17, §19 |
| 009 (major) bootstrap created real REPO data before PL-T2; REQ-03 contradicted ANCHOR; recurring fixture verification impossible with real data present | **Bootstrap boundary** (SE11-DEC-18 revised, SE11-ADR-14, SE11-REQ-21): the authoritative repository `REPO-EXT` lives at an external hosted repository service, outside the local admission scope; local clones and the T2 mirror are D-REB; commissioning evidence is committed to `REPO-EXT`, so no real local D-IRR data exists before `PL-T2`. A future local repository server (`LREPO`) is admitted like any other class. **SE11-REQ-03 rewritten** to the state rule (COPY, or ANCHOR within A_max of admission, then DEGRADED). **SE11-AC-07b split** into -init (fixture, no real data of the class) and -rec (recurring fixture verification with real data present). **SE11-AC-07d rewritten as a trace** in which every step lists the state before/after and the invariants I1–I6 checked. KEYS bootstrap custody by SE11 (T3-SUB) so the trace needs no absent owner. | §6.2, §6.3, §14 (SE11-AC-07b/07d), §16 |
| 010 (major) heartbeat 300 s vs stale 180 s; per-epoch seq with no epoch cursor; no retention or snapshot recovery; no initialization | Part B rewritten (SE11-DEC-22, SE11-ADR-15): one HEARTBEAT every H = 60 s carrying the full level snapshot; consumers poll every P ≤ 60 s and mark STALE only after 3H = 180 s without a *received* heartbeat (worst healthy gap 120 s < 180 s, margin 60 s); **globally persistent 64-bit `seq`** (durable before serve; on counter loss restarts at `unix_seconds × 10^6`, provably above any issued value); `epoch` informational only; deterministic responses `history_expired` (410 + snapshot) and `cursor_ahead` (409 + snapshot); retention ≥ 7 days and ≥ 100,000 events; `GET /levels` snapshot; INIT events for every level before serving, `UNKNOWN` as fail-safe; consumer **bootstrap condition** before any admission (SE11-REQ-22). SE11-AC-09 cases (a)–(f) added. | §18.2 Part B, §14 (SE11-AC-09), §10.3 |

### 0.5 Seed-level reconciliation of record (the content the register distils; register ids pending under ASM-SE11-01)

Each row names the SEED-01 section(s) a register row would distil, the seed statement in short, SE11's position, and the outcome. "Consistent" means SE11's position follows the seed statement; "Deviation Cn" means both sides are stated in §16.6 for reviewers. The "Register id" column is the only thing a present register would add; it is filled by SE11-AC-11.

| SE11 id(s) | SEED-01 section(s) | Seed statement (short) | SE11 position | Outcome | Register id |
|---|---|---|---|---|---|
| SE11-ADR-01, gate G-LOCAL, B19 | §157, §158, §160, §168, §226 note, §238 | Provision only justified capacity; hosted equivalents acceptable where they better satisfy requirements; no premature local-compute constraints | Candidate architecture with per-element gate G-LOCAL; hosted-first workers | Consistent | pending (SE11-AC-11) |
| SE11-ADR-02, B9 | §166, §167, §168, §227.9 | Windows host + Hyper-V Linux VMs + containers for durable services; WSL2 for interactive use | Adopted as the operating model | Consistent | pending |
| SE11-ADR-03, SE11-RISK-02, B4 class | §227.4, §228.1 | Non-ECC DDR5 on the central node; ECC on the NAS | Non-ECC accepted and monitored; ECC class recorded substitute | Consistent | pending |
| SE11-ADR-04, SE11-DEC-04, B11, §5.5 | §175, §176, §177, §227.7, §227.11, §160 table | GPU optional at initial acquisition; driven by measured demand; 750 W PSU compatible when the power budget is validated | Deferred; preconditions incl. measured power check | Consistent | pending |
| SE11-ADR-05, SE11-REQ-03, §6.5 | §163, §164 | NAS is the durable tier, not a latency substitute; RAID is not the only backup; irreplaceable data gets an isolated copy | Host NVMe independent volumes; T1→T2→T3; protection states | Consistent | pending |
| SE11-ADR-06, SE11-ADR-11, SE11-ADR-13, SE11-DEC-07/10/13/17/19, SE11-REQ-06/15/20, §8.3 | §165, §228.1, §229.1 | UPS protects PC, NAS and critical network components long enough for controlled shutdown; integrate graceful shutdown with Windows/NAS | Gated signalling candidates; timed sequences; admissible restart mechanisms | Consistent; C3 records the S-3 topology substitution | pending |
| SE11-ADR-07, SE11-DEC-08, B17 | §165, §166, §230 | Switch/rack "if local rack infrastructure is selected"; rack UPS feeds switch when used; switch ≥ 2×10GbE | Switch adopted at baseline on PD-A; rack deferred | Deviation C1 (switch power domain), C4 (switch before rack) | pending |
| SE11-ADR-08, SE11-DEC-03/06/15 | §158, §159, §162, §164, §234, §238 | Quantities conditional on evidence; measure before resizing | Capacity candidates with decision rules; smaller default | Consistent; C5 recorded for transparency | pending |
| SE11-ADR-09, SE11-ADR-12, SE11-DEC-09/16, SE11-REQ-02/16 | §156, §157, §163, §174, §227.6 | Reserve CPU/memory/storage I/O for stable platform operation; priority classes | Highest-priority VMs on M2_4; I/O budget on M2_2 | Deviation C2 (role labels) | pending |
| SE11-ADR-10, SE11-DEC-11, SE11-REQ-01/14, SE11-NFR-01 | §157, §174, §175 | Noncritical jobs are paused/shed when capacity degrades | Weighted contention at the hardware layer; shedding by the scheduler on SE11 signals | Consistent | pending |
| SE11-REQ-05 | §160 | No hard-coded host names, local paths or addresses | Portability requirement on every VM/container definition | Consistent | pending |
| SE11-REQ-07/08, SE11-NFR-04 | §160, §234 | Capture performance/resource telemetry from the first workloads | Inventory identity; telemetry contract from first power-on | Consistent | pending |
| SE11-REQ-09, SE11-SECREQ-02 | §12, §25, §160 | Current-practice revalidation; certified components | Firmware lifecycle with signed images and settings baseline | Consistent | pending |
| SE11-REQ-10, B18 | §165, §231 | Two separate 15 A breakers; UPS direct to wall; 20 A optional | Requirement for qualified professionals; nothing designed | Consistent | pending |
| SE11-REQ-13/17/18/21, SE11-DEC-18, SE11-NFR-05, §6.3 | §164, §31 | Isolated copy for irreplaceable data as the program matures; rollback and recovery as design requirements | Protection states with bootstrap boundary and bounded ANCHOR exposure | Consistent | pending |
| SE11-SECREQ-01…08, SE11-REQ-19 | §59, §66, §112, §185, §228.1 | MFA, zero-trust secrets, confidential processing boundary, per-folder AES-256 | Hardware security requirements with SE11-executable checks | Consistent | pending |
| §9 failure domains, SE11-NFR-06/07 | §172, §173, §175 | Redundancy must cover actual shared failure points, not merely worker count | Named common-mode domains with owners and residuals | Consistent | pending |
| §12 triggers, REV-* | §159, §161, §171, §226 | Evidence-driven thresholds; central node complements workers | Triggers and revision boundaries | Consistent | pending |
| ASM-SE11-02, SE11-RISK-08 | §0, §151 | Rev 1.1 proposed; v1.0 authoritative until approval; change control | Rev 1.1 treated as operative because only it holds the hardware baseline | Deviation C6 | pending |
| SE11-DEC-14, SEL-0, SE11-DEC-21 | §226 note, §12, §227–§231 | BOM is a reference configuration, not an assertion of owned equipment; revalidate current practice before build | Part numbers deferred pending G1; SEL-0 as the coherent reference set | Consistent | pending |
| SE11-REQ-22, SE11-DEC-22, SE11-ADR-15 | §30, §160 | Observability by construction; telemetry from first workloads | Event protocol with persistent sequence and bootstrap condition | Consistent | pending |

### 0.6 Upstream reconciliation obligations made mechanical (executed by SE11-AC-11 when the documents exist)

| Upstream document (absent) | What SE11 checks against it | If it conflicts |
|---|---|---|
| PM09-NONFUNCT-REQUIREM, PM09-ACCEPTAN-CRITERIA | SE11-NFR-01…08 values vs product NFRs; recovery targets vs product RPO/RTO | NFR value replaced or conflict recorded under §16.6; dispositions re-checked |
| PM09-MVP-SCOPE, PM09-ROADMAP, PM09-PRIORITI-BACKLOG-FEATURE | Whether local hardware is in MVP scope at all (gate G-LOCAL inputs); stage windows for SE11-DEP needs | G-LOCAL outcome per pool recorded; triggers re-timed |
| PM09-PRODUCT-RISKS-CONSTRAI, PM09-PRODUCT-DECISION-LOG | Decisions touching hosting, data residency, confidential processing (§66), spending | ADR-01 Step 2 (hosted placement) admissibility updated |
| EL-ARCHITEC-DECISION-RECORD, EL-INFRASTR-RUNTIME-ARCHITEC, EL-ENVIRONM-DEPLOYME-ARCHITEC, EL-SYSTEM-RELIABIL-RESILIEN | Each SE11-ADR against EL ADRs; pool naming; VM boundaries; failure-domain residual acceptance | Conflict recorded; EL supersedes only via a new ADR |
| EL-ENGINEER-NFR-SPECIFIC | NFR ids to bind SE11-NFR-01…08 | Binding recorded; values reconciled |
| EL-INTERFAC-CONTRACT-GOVERNAN | Transcription of SE11-CREG-001…003 into EL's register | Registration references added to §18.2 |
| EL-ENGINEER-ESTIMATE-CAPACITY, EL-ENGINEER-IMPLEMEN-SEQUENCI | Per-pool demands for §5.3 Step 0; the stage by which each SE11-DEP is needed | SE11-DEC-03a/06a recorded in the sizing document |
| NT16-* | FD-EXT-AI, FD-INTERNET, FD-EXT-REPO, T3 provider and hosted-equivalent risk/SLA | Residual dispositions in §9 updated |
| SP16-* | Economics for G-LOCAL and §5.3 Step 2 | Local-versus-hosted per pool decided |

### 0.7 Seed consistency check — deviations (both sides; §16.6 repeats them)

| Id | Seed statement | This document | Disposition |
|---|---|---|---|
| C1 | §165: the rack UPS "feeds rack PDU for local worker nodes **and switch** when used"; the same section gives the PC+NAS UPS the purpose "protect central PC, NAS **and critical network components** long enough for controlled shutdown" | The core switch is powered from PD-A (UPS-A) | Deviation accepted (SE11-DEC-08): the rack does not exist at baseline, the switch is a critical network component in the seed's own words, and in candidate S-1 the NAS shutdown command crosses it. When the rack exists the switch stays on PD-A unless S-3 (no command path) is in use, in which case it may move to PD-B as §165 states. Reviewers resolve if they read the rack clause as mandatory |
| C2 | §227.6: M2_4 = "platform data / DBs / containers", M2_2 = "VM & artifact store" | Highest-priority VM system disks are placed on M2_4 with the data; M2_2 carries High/Medium VM disks and artifacts; Mapping-V (§6.1a) may move Validation to M2_3 | Deviation recorded as SE11-DEC-09/ADR-09 with reason (§157 reservation principle, §174 priority classes) and impact (§6.1) |
| C3 | §165/§229.1: one PC+NAS UPS with "automatic graceful shutdown via PowerPanel / NAS UPS service" | SE11 does not assert that any host↔NAS signalling combination works; candidate S-3 substitutes a second UPS for the NAS | Gated decision SE11-DEC-10; S-3 is a topology substitution of B15 recorded with reason (no evidenced cross-device integration) and impact (second UPS of the B16 class, separate runtime budget) |
| C4 | §166/§230: switch and rack items apply "if local rack infrastructure is selected" | The managed switch (class) is adopted at baseline without a rack | Deviation accepted (SE11-ADR-07): three or more endpoints and VLAN enforcement of `seg.*` need a switch regardless of the rack; the smallest class satisfying §230 is used (§158 no-overbuild); the interim point-to-point placement of §7.2 remains allowed |
| C5 | §227.4 and §228.3 list 4×64 GB and 6×20 TB as the reference quantities | Quantities are candidates sized by rule; defaults M-A (128 GB) and N-A (4 drives) | Not a conflict: §162, §164 and §238 make the quantities conditional; recorded for transparency (SE11-ADR-08) |
| C6 | §0: Rev 1.1 is "proposed"; "the approved v1.0 document remains authoritative until this revision is explicitly approved" | Rev 1.1 is treated as the operative seed because only Rev 1.1 contains the hardware baseline | ASM-SE11-02, SE11-RISK-08; sign-off bound to the Rev 1.1 sha so that approval or change re-enters this document |


## 1. Authoritative source baseline (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01)

### 1.1 Exact version and sections consumed

| Item | Value |
|---|---|
| Seed | SEED-01, "Master Product Vision & Operating Architecture — Proposed Revision 1.1", "Expanded 2026 Baseline — Greenfield, Opportunity Intelligence, 19-Gap & Infrastructure Edition" (§0); file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| BOM version | Appendix G "Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note in §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231) |
| Strategy sections | §152–§154 (37.x stage boundaries, shared hardware, evidence progression), §156–§157 (38.x required logical environments, resource-reservation principle), §158–§160 (39.x no-wait/no-overbuild, evidence-driven thresholds, portability, section-40 reference configuration table), §161–§163 (40.x central node, memory, NVMe), §164–§166 (41.x NAS, UPS/electrical, rack/network and the section-42 operating model), §167–§168 (42.x layout, VMs + containers), §169–§171 (43.x workers), §172–§175 (44.x redundancy, quorum, resource classes, degradation), §176–§177 (45.x GPU) |
| Guardrails | Appendix H §232–§238 (H.1–H.7) |
| Domain boundaries | §74 (SE11 = Infrastructure, Containers & Runtime Engineering; SE12 = Database, Storage & Data; SE14 = API, Integration & Portability; SE17 = Infrastructure, Workload & Data Security; SE19 = Performance, Resilience & Specialized Validation; SE20 = SRE, Observability & Production Operations; SE01 = Core Platform & Distributed Systems) |
| Approval status of the seed | §0: "The approved v1.0 document remains authoritative until this revision is explicitly approved." The hardware baseline exists only in Rev 1.1 (conflict C6, ASM-SE11-02); sign-off binds to that exact revision and sha (§17). |
| Selection record | SEL-0 (§11.3): the Appendix G v2.2 set is the single coherent reference configuration; part numbers deferred pending G1 |

### 1.2 Classification and engineering disposition of every BOM entry

The seed states that Appendix G "is a greenfield reference configuration, not an assertion of already-owned equipment or a mandatory topology" and that Product/Engineering "may procure, substitute, resize, or use hosted equivalents when evidence shows equal or better capability, reliability, portability, security, schedule, and economics" (§226 status note); that "local central compute, NAS, power, and worker infrastructure should be provisioned when workload evidence and economics justify it; managed/hosted equivalents remain acceptable where they better satisfy the target requirements" (§238); and that the central node "is a reference configuration rather than an inherited constraint" (§160, section 40 lead-in).

**Reading rules for the table.** (a) A disposition is the disposition *of the specification class of the reference item if local provisioning of that element is justified* under gate G-LOCAL (SE11-ADR-01); it is not a decision that local provisioning is justified. (b) **Part-number status (SE11-DEC-14):** the corpus contains no manufacturer support, firmware, qualified-list, driver or availability statement for any part number beyond the seed's own assertions at its revision date (§11.2). Every part number cited from the seed is therefore **DEFERRED-PENDING-EVIDENCE**: it is the seed's reference exemplar of the class and the member of selection record SEL-0; it is not baselined; it enters the configuration fingerprint only when its G1 (SE11-AC-01) record reads "confirmed". The *class* (§11.4) is what is adopted. (c) "Quantity/count status" separates the adopted class from any capacity figure, which is never adopted from the maximum listed configuration (ENV-DEC-017).

| # | BOM entry (seed section; the part number is the reference exemplar) | Seed class | Engineering disposition of the specification class (SE11 only) | Quantity / count status | Decision ref |
|---|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, Zen 5 homogeneous, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — class §11.4; virtualization extensions and IOMMU enabled; 230 W package limit is the compute line of the power budget (§8.2). Part number DEFERRED-PENDING-EVIDENCE | n/a (one CPU) | SE11-DEC-01, SE11-DEC-14 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — class: dual-tower air cooler ≤ 160 mm with AM5 mounting; structural check only (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi: 4×DDR5 to 256 GB; PCI_E1 Gen5 x16 (CPU); PCI_E2 Gen3 x1; PCI_E3 Gen4 x4 (shares with M2_3); M2_1 Gen5 x4 CPU; M2_2 Gen5 x4 CPU sharing with USB4; M2_3 Gen4 x2 chipset; M2_4 Gen4 x4 chipset; 4×SATA; 5 GbE; Wi-Fi 7; BT 5.4; 2×USB4; Flash BIOS; Clear CMOS (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map verified before baseline (SE11-AC-02) with fallbacks A/B/C and Mapping-V (§6.1a); Wi-Fi/Bluetooth disabled in server role; no out-of-band controller, so the management path is §10.2. Part number DEFERRED-PENDING-EVIDENCE (BIOS/CPU support currency not established, FC-01) | n/a | SE11-DEC-02, SE11-DEC-12, SE11-DEC-14 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC, single matched kit; "step down to 5600/5200 if 4-DIMM training is unstable" (§227.4; §162) | Preferred target (class); evidence-driven (quantity) | ADOPT WITH ENGINEERING CONSTRAINT for the **class** (DDR5 UDIMM matched kit on the AM5 4-slot platform, EXPO with the seed's 5600/5200 fallback, non-ECC accepted and monitored, SE11-RISK-02). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** 256 GB (4×64) is the reference *ceiling*, not adopted capacity. Quantity chosen by Table 5.3-R and the admission rule of §5.3 (M-A default; larger candidates only by the ordered procedure) | SE11-DEC-03, SE11-DEC-15, SE11-ADR-03, SE11-ADR-08 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch at x2 is acceptable subject to SE11-AC-02; under Mapping-V the M2_3 device carries Validation instead (§6.1a). Part number DEFERRED-PENDING-EVIDENCE | 2 devices (roles per §6.1/§6.1a) | SE11-DEC-02, SE11-DEC-12, SE11-DEC-16 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; seed roles "platform data / DBs / containers (M2_4)", "VM & artifact store (M2_2)" (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID (SE11-ADR-05); role mapping deviates from the seed's literal labels (conflict C2, SE11-DEC-09, §6.1). Part number DEFERRED-PENDING-EVIDENCE | 2 devices | SE11-ADR-05, SE11-DEC-09 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build; with the 145 W optional GPU only after the measured power-budget check the seed itself requires (§227.11: "compatible with a 750 W-class PSU when the final component power budget and headroom are validated"); any accelerator above 145 W, dual-slot, or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance, 3×140 mm fans (§227.8) | Preferred target | ADOPT — class §11.4; clearance and form factor structurally compatible with B2/B3 (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B9 | OS — Windows 11 Pro retail (§227.9; operating model §166) | Fixed by the operating model (§166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role; persistent services only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13). Edition/licence identifier DEFERRED-PENDING-EVIDENCE | n/a | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); if coexistence fails, Fallback A relocates the NIC to PCI_E1 while the GPU is deferred (SE11-DEC-12); hypervisor virtual-switch driver support not established (FC-05). Part number DEFERRED-PENDING-EVIDENCE | 1 device | SE11-DEC-02, SE11-DEC-12 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell, 24 GB ECC, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition" §175; "driven by measured demand and economics" §177) | DEFER / OPTIONAL — adoption preconditions §5.5 and trigger TRG-GPU §12.2; when triggered, Fallback A (NIC in PCI_E1) must first be undone or replaced (§6.1a) | 0 at baseline | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T: 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock (64 GB max), 2×10GbE + 2×5GbE, 2×USB4, 4×M.2, ADM/Btrfs snapshots, per-folder AES-256, "UPS support / network UPS server" (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only (never a live datastore); admin interface on `seg.mgmt`; firmware lifecycle §10.4; UPS-signalling role gated by SE11-DEC-10/19. Part number DEFERRED-PENDING-EVIDENCE | 1 enclosure; subject to G-LOCAL (hosted object storage is the recorded equivalent for T2/T3, §6.7) | SE11-ADR-05, SE11-DEC-10 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install on TRG-NAS-MEM (§12.2) | 0 at baseline | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target (class); count tied to retention policy (§164) | ADOPT WITH ENGINEERING CONSTRAINT for the **drive class** (3.5-inch enterprise CMR, RAID 6 mandatory at ≥ 20 TB per drive, SE11-RISK-06). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** Six drives is the reference *ceiling*; count chosen by the §6.7 rule (N-A default) | SE11-DEC-06, SE11-ADR-08 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, line-interactive AVR, 12 outlets (6 battery + surge, 6 surge only), NEMA 5-15P, USB HID, "automatic graceful shutdown via PowerPanel / NAS UPS service", RB1290X2 batteries (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement; per-candidate shutdown budget SE11-REQ-06 with fail-closed outcome (§8.4); signalling and restart integration gated by the admissibility matrix (SE11-DEC-10, SE11-DEC-13, SE11-DEC-17, SE11-DEC-19). Part number DEFERRED-PENDING-EVIDENCE | 1 unit (S-1/S-2); 2 units of the B15/B16 classes in S-3 | SE11-DEC-07, SE11-DEC-10, SE11-DEC-13, SE11-DEC-19 |
| B16 | UPS (rack) — second unit ~1000 VA / 600 W pure sine, model TBD; "when a local worker rack is used" (§229.2; §165) | Candidate ("when used") | DEFER / OPTIONAL — only with a local worker rack, **or** adopted early as the NAS unit under candidate S-3 (conflict C3) | 0 at baseline (1 if S-3) | SE11-DEC-08, SE11-DEC-10 |
| B17 | Rack — 18U; 1U 24-port switch "at least 2×10GbE"; 1U PDU; worker trays sized to measured need; 1U power-brick shelf; "no fixed initial worker count" (§230; §166) | Candidate ("If local rack infrastructure is selected", §166) | Switch: ADOPT WITH ENGINEERING CONSTRAINT by class (managed, VLAN-capable, ≥ 2×10GbE minimum per seed, ≥ 4×10GbE preferred, §7.2; conflict C4). Rack, PDU, trays, shelf: DEFER / OPTIONAL until TRG-WKR-LOCAL (§12.2) | Switch 1; rack items 0 at baseline | SE11-DEC-08, SE11-ADR-07 |
| B18 | Electrical — two separate 15 A breakers (PC+NAS UPS on one, rack UPS on the other); UPS plugged directly into wall; dedicated 20 A optional; typical ~560 W, sustained peak ~1,150–1,300 W (§231; §165) | Fixed constraint (code-regulated) | ADOPT WITH ENGINEERING CONSTRAINT — stated as a requirement for qualified professionals (SE11-REQ-10); nothing electrical is designed here | n/a | SE11-REQ-10 |
| B19 | Local worker nodes (form factor and count unspecified; pool "may be local, hosted, cloud or hybrid", §168–§171) | Optional / evidence-sized | DEFER / OPTIONAL — hosted/cloud executors first (§160 "avoid premature local-compute constraints"); local class adopted on TRG-WKR-LOCAL | 0 at baseline | SE11-ADR-01 |

**Tally (authoritative; supersedes any other count):** ADOPT ×2 (B2, B8); ADOPT WITH ENGINEERING CONSTRAINT ×13 (B1, B3, B4-class, B5, B6, B7, B9, B10, B12, B14-class, B15, B17-switch, B18); DEFER / OPTIONAL ×5 (B11, B13, B16, B17 rack/PDU/trays/shelf, B19); SUBSTITUTE ×0 at baseline (S-3 would be a recorded topology substitution of B15 under SE11-DEC-10); ESCALATE ARCHITECTURE IMPACT ×0 at baseline (conditional REV-* triggers in §12.3). Capacity candidates: B4 quantity (M-A/M-B/M-A+/M-C), B14 count (N-A/N-B/N-C). **Part numbers: 17 DEFERRED-PENDING-EVIDENCE (B1–B17), 0 confirmed; all 17 are members of selection record SEL-0 (§11.3).** No substitution is silent: any future substitution is a new SE11-DEC entry with technical reason and impact (SE11-REQ-12).


## 2. Physical architecture scope and boundaries (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-02)

### 2.1 In scope (owned by SE11)

| Element | Content of this document |
|---|---|
| Local central compute | One central node (B1–B10 classes) as the reference configuration; host role, slot/lane allocation with fallbacks, reservation mechanism (§5) |
| Worker nodes | Capability classes and placement rules for local workers if and when adopted (§4, §12); physical provisioning (trays, power, ports) when triggered |
| GPU / accelerator class | Single-slot, ≤ 145 W, PCIe x16 class; deferred (§5.5) |
| Storage / NAS | Hot NVMe tiers on the host, the durable NAS tier, the physical mapping of every volume, the storage I/O budget, the dataset classes with their bootstrap boundary and the protection matrix (§6) |
| Network switching / NICs / physical segments | 10 GbE storage/core path, 5 GbE host onboard, switch class, VLAN membership and addressing of the physical segments (§7). Physical-network engineering is SE11's: §74 places SE14 in "API, Integration & Portability Engineering", not physical networking |
| Rack / placement | 18U rack class; desk/room placement constraints (§8.5) |
| UPS / power distribution | Two power domains, UPS roles, per-candidate shutdown sequences, the admissibility matrix of signalling × restart mechanisms, and the timing budget to service readiness (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10.1) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10.2) |
| Hardware-published signals, states and the protection-evidence intake | Signals and protection levels published under `SE11-CONTRACT-hardware-signals@1`; evidence accepted under `SE11-CONTRACT-protection-evidence@1`; baseline record under `SE11-CONTRACT-hardware-baseline@1` (§18.2) |
| Bootstrap custody of commissioning secrets | The KEYS bootstrap custody procedure on T3-SUB media until SE17/SE15 take over (§6.3) |

### 2.2 Out of scope (owned elsewhere; referenced, never included)

| Concern | Owner (SEED-01 §74 unless stated) | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (chain rule) | §15 |
| Electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only |
| System, runtime, deployment and reliability architecture | EL | EL cross-references this document; EL's documents are absent (SE11-DEP-02/10) |
| Capacity model and growth thresholds | SE01 (capacity concern) and SE11-HARDWARE-CAPACITY-SIZING (sizing) | §5.3 and §6.7 give candidate configurations and decision rules; the sizing document applies them (SE11-DEP-03) |
| Load shedding / job pausing policy | EL (scheduler), SE01 | SE11 publishes the signals (SE11-DEC-11, contract §18.2); the shedding policy and controller are not designed here; no SE11 guarantee depends on them |
| Data policy: dataset classification, retention, backup schedule, binding RPO/RTO, long-term key custody, write-freeze enforcement in the data stores | SE12 (data), SE17/SE15 (security, keys) | §6 states hardware-capable targets, protection states and provisional defaults; stores enforce the levels SE11 publishes (SE11-REQ-18); evidence enters through SE11's contract |
| Portability and integration constraints on how pools are addressed | SE14 | Consulted on §4/§7 naming; owns no physical design |
| Security control catalogue and ids | SE17 (infrastructure/workload/data), SE15 (identity/crypto) | §13 lists SE11's requirements as SE11-SECREQ-nn and the checks SE11 executes itself (SE11-REQ-19); mapping to owner control ids is SE11-DEP-05 |
| Performance/resilience test execution | SE19 | §14 lists the tests; SE19 executes and reports (SE11-DEP-06) |
| Operations, monitoring, maintenance windows | SE20 | §10 states telemetry (as SE11's exporter contract) and window requirements (SE11-DEP-07) |
| External repository service (hosts `REPO-EXT`) | External provider; NT16 assesses | §6.3 boundary; FD-EXT-REPO (§9) |
| Software/container/service design | existing SE11 runtime artefacts and EL | BND-03: not restated |

### 2.3 Context view (text)

```mermaid
flowchart LR
  subgraph PD_A[Power domain A: UPS-A class B15 on circuit A]
    HOST[Central host: Win11 Pro + Hyper-V\nVMs: Core + Data on M2_4 / Build-CI + Validation on M2_2\nM2_1 host system, M2_3 scratch - or Validation under Mapping-V\nSE11 host agent: signals, evidence intake, baseline record]
    NAS[NAS class B12: RAID 6 (count = candidate)\nsnapshots, backups, evidence, archives, REPO mirror = T2]
    SW[Managed switch class B17: >=2x10GbE (>=4 preferred) + access ports]
  end
  subgraph PD_N[Power domain N: UPS-N class B16 - only in candidate S-3]
    NAS3[NAS moves here under S-3]
  end
  subgraph PD_B[Power domain B: rack UPS-B on circuit B - DEFERRED]
    RACK[18U rack: PDU, worker trays - DEFERRED]
    WK[Local workers - DEFERRED]
  end
  HOST -- L1 10GbE storage/backup --> SW
  NAS -- L1 10GbE --> SW
  HOST -- L2 5GbE mgmt + upstream --> SW
  SW -- L5 uplink --> GW[Upstream gateway / internet]
  GW --> EXT[External AI providers, hosted runners, hosted T3 copy,\nexternal repository service = REPO-EXT]
  WK -. L4 1/2.5GbE .-> SW
  UPSA[UPS-A USB-HID] -- primary signal (gated, SE11-DEC-10/19) --> HOST
  HOST -- network shutdown command (S-1, gated) / N1 wake --> NAS
  T3SUB[(T3-SUB media, outside the room:\nKEYS bootstrap custody, bridging copies)] -. offline .- HOST
```

## 3. Stakeholders, concerns and quality attributes (ISO/IEC/IEEE 42010 framing)

| Stakeholder | Concern | Quality attribute (ISO/IEC 25010) | Measured by |
|---|---|---|---|
| EL | One coherent physical architecture to reference; contracts to transcribe; shedding signals to consume | Compatibility, maintainability | §4–§10 cross-references; §18.2 registered contracts; SE11-DEC-11 |
| SE01 | Capacity inputs as ranges with assumptions; signals for the scheduler | Capacity | Table 5.3-R, §6.7, §12 |
| SE12 | Durable tier, RAID/replication boundaries, protection states with a legal bootstrap, recovery rules, the evidence contract to produce into | Reliability (recoverability, fault tolerance) | §6.3, §6.6, SE11-NFR-05, SE11-AC-07a/b/c/d, §18.2 Part C |
| SE14 | Pools addressed portably | Portability | SE11-REQ-05 |
| SE17 / SE15 | Trusted boot, management isolation, encryption support, custody takeover | Security (confidentiality, integrity) | §13, §6.3 KEYS, SE11-AC-08a/08b |
| SE19 | Burn-in, contention, abrupt-loss and resilience test surface | Reliability (maturity), performance efficiency | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows, shutdown and restart drills | Maintainability (analysability), reliability | §10, SE11-NFR-04 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, ADR-01 gate G-LOCAL, §12 triggers |

**Measurable non-functional targets introduced by this document (status PROV; binding to EL-ENGINEER-NFR-SPECIFIC ids is unmet dependency SE11-DEP-10; values are engineering proposals, ASM-SE11-06).**

| NFR id | Quality attribute | Target (measurable) | Verified by |
|---|---|---|---|
| SE11-NFR-01 | Performance efficiency / weighted-service guarantee under contention | Under the §14 contention profile: (a) Core and Data VMs: CPU-wait ≤ 5 % in every 60 s window, Core synthetic API probe p95 ≤ 1.5 × unloaded baseline, Data 4 KiB random-read p99 ≤ 2 × unloaded baseline; (b) Validation VM: CPU-wait ≤ 10 % (it receives its full 8 vCPU from reserve + weighted floating share, §5.2); (c) Build VM: receives ≥ 11 LP-equivalents of its 16 (4 reserved + ≥ 7 floating); (d) inside the Build VM, `pool.background` receives ≤ 10 % of the VM's CPU while build jobs saturate (cgroup weight 10 : 100). No ordered shedding is claimed at the hardware layer (SE11-ADR-10) | SE11-AC-12 |
| SE11-NFR-02 | Performance efficiency / storage path | Host↔NAS ≥ 0.7 GB/s sustained for 10 min during concurrent build-cache load; no other path degrades below 80 % of its unloaded throughput | SE11-AC-05 |
| SE11-NFR-03 | Reliability / safe shutdown and restart, per UPS and per admissible candidate × mechanism | For every UPS u in the selected candidate: B_u ≤ 0.7 × R_u (B_u = critical-path budget of §8.3, R_u = measured runtime at measured load); every step completes inside its bound. Restart, given battery charge ≥ 50 % at mains restoration and an admissible combination of §8.3a: **T_restart ≤ 720 s** (mains restoration → S6 entry); **T_service_clean ≤ 1,200 s** (mains restoration → every VM running, Data services started with the NAS reachable or the 300 s NAS-wait cap elapsed, protection levels re-published) after a shutdown in which every VM stopped gracefully; **T_service_forced ≤ 1,800 s** when any VM was force-stopped (bounded filesystem checks, ASM-SE11-15); database crash recovery after a forced stop is SE12's figure, measured and recorded but not bounded here (§8.3b) | SE11-AC-06, SE11-AC-14, SE11-AC-15 |
| SE11-NFR-04 | Maintainability / observability | 100 % of §10.3 signals exported under `SE11-CONTRACT-hardware-signals@1`, sample interval ≤ 60 s, heartbeat every 60 s, no false STALE during healthy operation, retained for at least one stage | SE11-AC-09 |
| SE11-NFR-05 | Recoverability (hardware-capable; SE12 binds the product RPO/RTO) | T1→T2 snapshot interval ≤ 1 h and full replication ≤ 24 h; single-VM restore from T2 ≤ 4 h; for every local D-IRR class with real data: state PROTECTED with kind COPY and copy age ≤ A_max = 24 h, or kind ANCHOR with age ≤ A_max from admission; expiry at A_max + G = 48 h (§6.3); restore of each D-IRR class from T3 verified at every stage gate (fixture-based, SE11-AC-07b-rec) | SE11-AC-07a/b/c/d |
| SE11-NFR-06 | Availability (single-host) | No HA claim. Planned hardware maintenance only in declared windows; FD-HOST recovery to degraded service (hosted fallback or replacement host of the §11.4 class) ≤ 1 working day from T2/T3, assumption ASM-SE11-07 | SE11-AC-07, SE19 resilience tests |
| SE11-NFR-07 | Integrity after abrupt loss | After an abrupt power loss (FD-UPS-A drill), every VM filesystem, the host filesystem and the NAS array pass integrity checks with zero unrecoverable errors; database loss ≤ last committed transaction (SE12 verifies) | SE11-AC-13 |
| SE11-NFR-08 | Thermal/power envelope | ≥ 24 h combined stress with CPU package ≤ 230 W, all device temperatures within manufacturer limits, zero memory errors at the chosen DDR5 profile | SE11-AC-04 |

## 4. Workload-to-hardware allocation (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03)

Allocation maps workload classes to **resource pools**, never to named devices; a pool is addressed by a logical name (§160: no hard-coded host names, local paths or addresses). Pools are the unit that moves between local, hosted and customer infrastructure (§168). Every pool has either its own budget or an explicit *shared-budget membership* with a stated share (SE11-REQ-01). Units: **LP** = logical processor of the host (32 LP = 16 physical cores × 2 SMT threads, B1); **vCPU** = virtual processor assigned to a guest (1 vCPU is scheduled onto 1 LP at a time). **Memory budgets are not repeated here: the single authoritative source is Table 5.3-R**, keyed by candidate; this table only names which line of Table 5.3-R applies.

| Pool | Workload class (seed §167, §169–§171, §174) | Priority (§174) | Placement in the reference configuration | CPU budget | Memory (Table 5.3-R line) | Storage device (§6.1) |
|---|---|---|---|---|---|---|
| `pool.core` | Platform core: orchestration, APIs, queues, registry/control | Highest | Linux VM "Core" | 4 vCPU; Hyper-V reserve 100 % (= 4 LP guaranteed); limit 100 %; weight 200 | Core VM static | M2_4 |
| `pool.data` | Databases, search/knowledge data, caches | Highest | Linux VM "Data" (hosted under candidate M-C) | 4 vCPU; reserve 100 % (4 LP); weight 200 | Data VM static | M2_4 |
| `pool.runtime` | Stable runtime of accepted stage baselines (§156, §235) | Highest | **Shared-budget member of `pool.core` and `pool.data`**: runtime namespaces inside the Core and Data VMs with separate projects, credentials, networks, data paths (§156). Share: within each VM, runtime namespaces hold cgroup `cpu.weight` ≥ 3 × the platform-control namespaces and `memory.min` ≥ 50 % of the VM's static memory (defaults; EL binds the exact values) | inherits | inherits | M2_4 |
| `pool.validate` | Integration, security validation, staging, release challenger, VP validation | High | Linux VM "Validation/Staging" | 8 vCPU; reserve 50 % (4 LP guaranteed); limit 100 %; weight 150 | Validation dynamic min/max | M2_2 (protected per §6.1a) or M2_3 under Mapping-V |
| `pool.build` | CI runners, build cache, artifact generation | Medium | Linux VM "Build/CI" | 16 vCPU; reserve 25 % (4 LP guaranteed); limit 100 %; weight 100 | Build dynamic min/max | M2_2 (VM disk, artifacts) + M2_3 (scratch; fallbacks and Mapping-V §6.1a) |
| `pool.agents` | API-based model workers | Medium | Hosted/cloud executors first. When local: **member of `pool.build` budget** as containers in the Build VM with cgroup `cpu.max` ≤ 50 % and `memory.max` ≤ 40 % of the VM | member | member | M2_2 |
| `pool.test` | Test/browser/scanning workers, synthetic users | Medium / lowest | As `pool.agents`: **member of `pool.build` budget**, `cpu.max` ≤ 50 %, `memory.max` ≤ 40 %; agents + tests together never exceed the Build VM's own ceiling | member | member | M2_2 |
| `pool.background` | Background analysis, documentation, low-priority optimisation | Lowest | **Member of `pool.build` budget**: cgroup `cpu.weight` 10 (vs 100 for build jobs), `cpu.max` ≤ 25 %, no memory guarantee; the scheduler sheds it first (§175, SE11-DEC-11) | member | member | M2_2 |
| `pool.gpu` | Local inference, embeddings, vision, evaluation (§176) | Medium | DEFERRED — PCI_E1 when adopted (§5.5); external providers meanwhile (§160) | — | — | — |
| `pool.durable` | Backups, snapshots, release evidence, archives, mirrors (§164) | n/a | NAS T2 (+ T3 isolated copy, §6.3) | — | — | NAS |
| `pool.admin` | Host OS, Hyper-V root, SE11 host agent (signals, evidence intake, UPS logic), WSL2 + Docker Desktop interactive use (§167) | n/a | Windows host root partition | Not reservable in Hyper-V; the root partition takes floating LPs (§5.2); operational rule: VM reserves sum ≤ 16 LP so ≥ 16 LP float | Host root reserve + WSL2 cap | M2_1 |

**Simultaneous CPU accounting at baseline:** vCPUs assigned to VMs = 4 + 4 + 8 + 16 = **32 vCPU on 32 LP** (1 : 1, no vCPU oversubscription at baseline; bursts happen *within* a VM's own vCPU count). Guaranteed LPs (sum of reserves) = 4 + 4 + 4 + 4 = **16 LP (50 %)**. Floating LPs = **16**, taken first by the host root partition (typical need 2–4 LP, ASM-SE11-03) and then by VMs in weight proportion 150 : 100 (Core and Data cannot take floating LPs: their 4 vCPU are already fully reserved). Under full saturation this arithmetic gives Validation its remaining 4 vCPU in full (its weighted share of 12–14 floating LPs, 0.6 × 12 = 7.2, exceeds the 4 it can use) and leaves Build with 4 reserved + 8–10 floating = 12–14 of its 16 vCPU. That is a **weighted-contention outcome**, measurable as SE11-NFR-01, not an ordered shedding mechanism.

**Weighted contention versus load shedding (SE11-ADR-10, SE11-DEC-11).**

1. *Weighted contention* is what the hypervisor's reserve/limit/weight controls and the in-VM cgroup weights produce automatically under saturation. It needs no controller; its guarantees are those of SE11-NFR-01 and are measured by SE11-AC-12.
2. *Load shedding* — pausing, cancelling or refusing noncritical jobs "when hardware capacity, network, storage, AI quota or power conditions degrade" (§175) — is a **scheduler action**, owned by EL (orchestration/scheduler) and SE01. SE11 does not design the controller or its transitions. SE11's obligation is to **publish the signals** on which the scheduler acts, under `SE11-CONTRACT-hardware-signals@1` (§18.2): `SIG-ONBATTERY`, `SIG-SHUTDOWN`, `SIG-THERMAL`, `SIG-STORAGE-PRESSURE`, `SIG-PROTECTION-STATE`, `SIG-PL-STATE`, `SIG-RESTART`. Which jobs the scheduler sheds on each signal is EL/SE01 policy (§18.3 row CI-1); the default expectation recorded for them, derived from §174/§175, is background → build → validation, with runtime never shed. **No SE11 guarantee depends on the scheduler's behaviour:** the shutdown sequence of §8.3 stops VMs by timeout and forced stop whether or not any job was shed, and in-flight loss is bounded by SE11-NFR-07.

Rule SE11-REQ-01 (restated): `pool.core`, `pool.data` and `pool.runtime` reservations are hard — static memory, 100 % processor reserve, never oversubscribed; every other pool has a declared guaranteed floor and ceiling or an explicit membership share as above. Rule SE11-REQ-14: the reservation mechanism is the hypervisor's per-VM processor reserve/limit/weight and static-versus-dynamic memory controls plus in-VM cgroup shares for members, admitted by the formula of §5.2; no pool relies on "best effort".


## 5. Compute architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-04)

### 5.1 Host-role requirements

| Requirement | Specification | Source |
|---|---|---|
| CPU | 16 physical cores / 32 logical processors, homogeneous cores, 64 MB L3, hardware virtualization + IOMMU enabled in firmware | B1 class (§227.1); VM isolation (§168) |
| Memory | DDR5 UDIMM matched kit on four slots (board maximum 256 GB, B3); quantity per Table 5.3-R and the admission formula of §5.3; EXPO only after the stability pass; fallback DDR5-5600/5200 as the seed directs | B4 (§227.4), §162 |
| PCIe / slots | PCI_E1 Gen5 x16 reserved for the deferred accelerator (used by the NIC under Fallback A, §6.1a); PCI_E3 Gen4 x4 carries the 10 GbE NIC by default; PCI_E2 Gen3 x1 unused (Fallback C only); 2×USB4 free for emergency storage/console | B3 (§227.3) |
| Local NVMe (4 slots, all populated) | M2_1 Gen5 x4 (CPU): 1 TB host system; M2_2 Gen5 x4 (CPU, shares with USB4): 4 TB Build/Validation VMs + artifact store; M2_3 Gen4 x2 (chipset, shares with PCI_E3): 1 TB scratch (or Validation under Mapping-V); M2_4 Gen4 x4 (chipset): 4 TB Core/Data VMs + platform data + platform container layers; total 10 TB | B5, B6 (§227.5–§227.6), §163; mapping §6.1 (SE11-DEC-09), §6.1a |
| Host OS / hypervisor | Windows 11 Pro with Hyper-V; Linux VMs for all durable services; WSL2 + Docker Desktop for interactive work only | B9 (§227.9), §166–§168 |
| Firmware baseline | UEFI Secure Boot and TPM 2.0 enabled; Wi-Fi 7 / Bluetooth disabled; "restore on AC power loss = power on"; RTC wake enabled and recorded (§8.3b); settings baseline in §13 | §13, SE11-DEC-13, SE11-DEC-17 |
| Thermal | Dual-tower air cooling ≤ 160 mm in a mesh-front mid-tower with three 140 mm intake fans; sustained 230 W CPU package (+145 W optional GPU) validated by SE11-AC-04 | B2, B8 |
| Host agent | The SE11 host agent (signals publisher, evidence intake, UPS state machine, N1 sender, baseline record writer) runs on the host OS as a service with the persistent sequence store and event log on M2_1 (§18.2) | SE11-DEC-22 |

### 5.2 Processor accounting and reservation mechanism (SE11-REQ-14)

| Quantity | Value | Basis |
|---|---|---|
| Physical cores | 16 | B1 |
| Logical processors (LP) available to the hypervisor | 32 | B1 (SMT) |
| vCPUs assigned to VMs | 32 (Core 4, Data 4, Validation 8, Build 16) | §4 |
| vCPU : LP ratio | 1 : 1 at baseline | no oversubscription by vCPU count |
| Guaranteed LPs (Σ processor reserve) | 16 (Core 4, Data 4, Validation 4, Build 4) | reserve % × vCPUs |
| Floating LPs | 16 | host root partition first (2–4 LP typical, ASM-SE11-03), then Validation : Build by weight 150 : 100 |

Mechanism on the selected host platform: per-VM **processor resource controls** (virtual machine reserve %, virtual machine limit %, relative weight) and per-VM **memory controls** (static memory = hard reservation; Dynamic Memory with minimum/maximum for burst pools). Members of a shared budget (`pool.agents`, `pool.test`, `pool.background`, `pool.runtime`) are bounded inside their VM by Linux cgroup v2 `cpu.weight`, `cpu.max`, `memory.min`, `memory.max` as listed in §4.

**Admission rule (SE11-REQ-14, formula SE11-DEC-15).** A VM or member may be created or resized only if (a) Σ processor reserves stays ≤ 16 LP; (b) with the resulting allocation α on the installed candidate X, **Req(α) = max(1.25 × F(α), C(α) + H_min) ≤ Installed(X)**, where F and C are the floor and ceiling of Table 5.3-R recomputed for α and H_min = 8 GB — both checks are always evaluated and neither alone admits; (c) the pool's storage volume is already mapped in §6.1 with its §6.1a row in force. The rule is enforced by the version-controlled VM definitions and checked in SE11-AC-03; its behaviour under saturation is verified by SE11-AC-12.

### 5.3 Memory sizing: the authoritative reservation table and decision rule (SE11-DEC-03, SE11-DEC-15)

**Evidence status.** No measured workload exists (§0.1: EL estimates and SE01 capacity model absent, SE11-DEP-03). Table 5.3-R therefore holds **hypothetical planning allocations** (ASM-SE11-03, ASM-SE11-11) derived only from the five required logical environments (§156) and the layout (§167). They justify no quantity by themselves; the sizing document replaces them with a traceable Stage-1 inventory and measured p95 values (§234 H.3). What *is* binding is the table's structure, the admission formula and the ordered procedure.

**Table 5.3-R — authoritative per-candidate memory reservations (GB). Every total in this document is derived from this table; no other section carries memory numbers.**

| Line | M-A: 2×64 GB = 128 GB (default) | M-B: 4×64 GB single kit = 256 GB | M-A+: M-A + second matched pair = 256 GB (two kits) | M-C: M-A kit, `pool.data` hosted |
|---|---|---|---|---|
| Host root partition reserve (hypervisor, host OS, drivers, SE11 host agent) | 12 | 16 | 16 | 12 |
| WSL2 cap (`.wslconfig`) | 8 | 8 | 8 | 8 |
| Core VM static | 20 | 32 | 32 | 20 |
| Data VM static | 32 | 64 | 64 | 0 (hosted) |
| Validation VM dynamic min → max | 8 → 20 | 16 → 48 | 16 → 48 | 8 → 24 |
| Build VM dynamic min → max | 12 → 24 | 16 → 64 | 16 → 64 | 12 → 32 |
| **Floor F** = host + WSL + statics + dynamic minima | 12+8+20+32+8+12 = **92** | 16+8+32+64+16+16 = **152** | **152** | 12+8+20+0+8+12 = **60** |
| **Ceiling C** = host + WSL + statics + dynamic maxima | 12+8+20+32+20+24 = **116** | 16+8+32+64+48+64 = **232** | **232** | 12+8+20+0+24+32 = **96** |
| Check 1: 1.25 × F | 115 | 190 | 190 | 75 |
| Check 2: C + H_min (H_min = 8) | 124 | 240 | 240 | 104 |
| **Req = max(Check 1, Check 2)** vs installed | **124 ≤ 128 ✓** | **240 ≤ 256 ✓** | **240 ≤ 256 ✓** | **104 ≤ 128 ✓** |
| Headroom at ceiling | 12 | 24 | 24 | 32 |
| Scale path | Add a second matched pair → M-A+ (SE11-AC-04 memory pass re-run; §227.4 4-DIMM fallback applies) | None (board maximum; REV-MEM) | None (board maximum; REV-MEM) | Hosted elasticity for data; local as M-A |
| Trade-off recorded | Smallest justified start (§158, §238); Data working set capped at 32 GB until re-balanced or expanded | Buys capacity the model may not demonstrate; single matched kit (§227.4); 4-DIMM training risk flagged by the seed | Two kits are not "a single matched kit" (§227.4): stability must be re-proven | Confidential-processing boundary (§66), EL latency input and SP16 economics (SE11-DEP-08) decide |

Members inside the Build VM (`pool.agents`, `pool.test`) are bounded by `memory.max` ≤ 40 % of the Build VM's *current* allocation and need no separate line.

**Definitions (SE11-DEC-15).** For an allocation α: F(α) = host reserve + WSL cap + Σ statics + Σ dynamic minima; C(α) = host reserve + WSL cap + Σ statics + Σ dynamic maxima; **Req(α) = max(1.25 F(α), C(α) + H_min)**, H_min = 8 GB. α is admissible on candidate X iff Req(α) ≤ Installed(X). **Floors are fixed inputs**: the host reserve, WSL cap, every static line and every dynamic minimum are workload-derived (or, before measurement, the table defaults) and are never lowered inside the procedure. The only legal moves inside Step 1 are: (i) *raise* a static line or a dynamic minimum to meet a measured demand; (ii) *lower* a dynamic maximum down to, but not below, its minimum. A floor is changed only by a **floor revision**: a measured p95 for that pool recorded as SE11-DEC-03a in the sizing document, after which the whole procedure re-runs from Step 0. Candidate order: M-A (128) < M-A+ = M-B (256); M-A+ is used when M-A is already installed, M-B when 256 GB is required before anything is installed. M-C is not a size but a placement alternative evaluated at Step 2.

**Procedure (deterministic; every step's outcome is recorded in SE11-DEC-03a).**

- **Step 0 — inputs.** SE11-HARDWARE-CAPACITY-SIZING produces, from a traceable Stage-1 concurrent workload inventory (the inputs EL-ENGINEER-ESTIMATE-CAPACITY and SE01 own, SE11-DEP-03), the per-pool demands; the measured host root reserve replaces the 12/16 GB planning value (ASM-SE11-11). Statics and minima are raised to meet demands (move i). Compute F, C, Req for the installed (or default) candidate. If Req ≤ Installed: **admitted**, stop.
- **Step 1 — reallocate within the installed candidate.** Because F does not depend on maxima, Step 1 can succeed **only if 1.25 F ≤ Installed**. If so, set the dynamic maxima deterministically: slack S = Installed − H_min − F; give each dynamic pool a span min(S × its default-span share, its default span), where the default spans are the table's (max − min) values (M-A: Validation 12, Build 12 → equal shares); any remaining S stays as headroom. Then Req = max(1.25 F, F + Σ spans + H_min) ≤ Installed by construction: **admitted**, stop. If 1.25 F > Installed, Step 1 **fails** (recorded) — no reallocation of maxima can fix a floor failure.
- **Step 2 — hosted placement of the oversized component (M-C).** Permitted by §238 and §160. Recompute F, C, Req with that pool's static line = 0. Admissible unless a recorded reason blocks it: the confidential-processing boundary (§66) forbids hosting that data; EL's latency requirement for the Core↔Data path is not met by a hosted service; or SP16 economics (SE11-DEP-08) reject it. If admissible and Req ≤ Installed: **admitted as M-C**, stop.
- **Step 3 — next larger candidate.** Only after Steps 1 and 2 have failed for recorded reasons: on 256 GB, recompute with the 256-GB table lines raised to demands and re-run Step 1 there. If Req ≤ 256: **admitted as M-A+ (or M-B)**, with the memory stability pass re-run (SE11-AC-04). The record must show the aggregate F/C/Req and both failed steps. **256 GB is never adopted on the strength of this document, nor on the strength of a single component.**
- **Step 4 — infeasible.** If 1.25 F > 256 (or Req > 256 after Step 1 on 256) and Step 2 is not admissible, the configuration is infeasible on this architecture: outcome **REV-MEM** (§12.3) — an architecture revision (larger-memory platform class, second host, or data-tier redesign), never a hardware addition. This outcome is selectable and deterministic; nothing is left without a disposition.

**Worked examples on M-A (128 GB; defaults host 12, WSL 8, Core 20, Data 32, Validation 8→20, Build 12→24; F = 92, C = 116, Req = 124 ✓). Floors are preserved in every example.**

| Example | Demand | Step 0 arithmetic | Classification | Deterministic disposition |
|---|---|---|---|---|
| E1 — ceiling-only failure | Data working set 38 GB → Data static 38 | F = 12+8+20+38+8+12 = 98 → 1.25 F = 122.5 ≤ 128 ✓; C = 12+8+20+38+20+24 = 122 → C+8 = 130 > 128 ✗; Req = 130 ✗ | Check 2 fails, Check 1 passes | Step 1: S = 128 − 8 − 98 = 22; spans: Validation min(11, 12) = 11, Build min(11, 12) = 11 → maxima 19 and 23; C = 120, Req = max(122.5, 128) = 128 ≤ 128 ✓. **M-A stands** with the re-balanced maxima recorded (minima 8 and 12 untouched) |
| E2 — floor-only failure | Data 44 GB; Validation measured p95 raises its minimum to 14 | F = 12+8+20+44+14+12 = 110 → 1.25 F = 137.5 > 128 ✗; with maxima set to Validation 20, Build 12: C = 116 → C+8 = 124 ≤ 128 ✓; Req = 137.5 ✗ | Check 1 fails, Check 2 passes | Step 1 **fails** (1.25 F > 128; maxima cannot change F). Step 2 (M-C, Data hosted): F = 12+8+20+0+14+12 = 66 → 82.5; C = 12+8+20+0+20+24 = 84 → 92; Req = 92 ≤ 128 ✓ → **M-C** if admissible under §66/latency/economics. Else Step 3: on 256 with lines raised to demands (host 16, Core 32, Data 64, Validation 16→48, Build 16→64): F = 152 → 190; C = 232 → 240; Req = 240 ≤ 256 ✓ → **M-A+** (second pair, SE11-AC-04 re-run) |
| E3 — both checks fail | Data 44 GB, other floors at defaults | F = 12+8+20+44+8+12 = 104 → 130 > 128 ✗; C = 12+8+20+44+20+24 = 128 → 136 ✗ | Both fail | Step 1 fails (floor); Step 2 M-C: F = 60 → 75, C = 84 → 92, Req 92 ✓ → **M-C** if admissible; else Step 3 → **M-A+** (Req 240 ≤ 256 ✓) |
| E4 — infeasible configuration | Data working set 160 GB; Core 32; Validation 16→48; Build 16→64; host 16 | F = 16+8+32+160+16+16 = 248 → 1.25 F = 310 > 256 ✗ on every local candidate | Floor exceeds the board ceiling | Step 1 fails on 128 and on 256; Step 2 M-C: F = 88 → 110, C = 16+8+32+0+48+64 = 168 → 176, Req 176 ≤ 256 ✓ (and 176 > 128, so M-C would itself require 256) → M-C on M-A+ if §66 permits hosting the data; if §66 forbids it: Step 4 → **REV-MEM** (architecture revision); no hardware addition is selectable |

*Non-ECC* on the central node is accepted for every candidate (SE11-ADR-03) with the ECC platform class recorded as the substitute if SE11-RISK-02 materialises. *Default before a model exists:* the seed's H.1 ("start productively") and H.3 ("measure before resizing") apply: **M-A with the Table 5.3-R values is installed** (Req 124 ≤ 128 ✓) and the choice is recorded as SE11-DEC-03a in the sizing document.

### 5.4 Virtualization / host implications

- VM count and boundaries remain an engineering decision (§167); the four Linux VMs are the minimum that satisfies the isolation rule of §156. Merging Core and Data into one VM is permitted only if the static memory lines of Table 5.3-R are preserved as a sum, both stay on M2_4, and SE17 accepts the shared blast radius.
- Highest-priority VMs (Core, Data) use static memory and 100 % processor reserve; they are never configured for dynamic over-commit (SE11-REQ-01).
- Snapshots of the Validation and Core VMs are taken before any firmware/driver change (§10.4) and replicated to `pool.durable`.
- Nothing in the VM layer may encode physical slot ids, device serials or the host name; the portability requirement §160 applies to every VM definition (SE11-REQ-05). Storage is referenced by volume label / stable identifier, not by slot.
- Per-virtual-disk IOPS controls (hypervisor storage QoS minimum/maximum) are the preferred storage limiter; their availability on the chosen host OS edition is confirmed in SE11-AC-03 (FC-06). If unavailable, the **guest-side limiter** of §6.1a (cgroup v2 `io.max` inside the Build VM) is mandatory — device separation alone is not an accepted fallback (SE11-REQ-16).
- A VM that was force-stopped (§8.3) carries an "unclean" marker; on next boot its filesystems are checked before any service starts (bounded by ASM-SE11-15 and measured in SE11-AC-15 drill (i)).

### 5.5 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger TRG-GPU (§12.2: local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability — which means that if Fallback A (NIC in PCI_E1, §6.1a) is in use it must first be replaced by Fallback B or C with a passed SE11-AC-12b — plus 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms measured full-load system draw plus 145 W ≤ 80 % of the 750 W PSU rating and that the per-candidate shutdown budgets of §8.3 still hold at the higher PD-A load; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on the client hypervisor (device assignment or partitioning, FC-07) — if none exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as a new SE11-DEC; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator or a dual-slot card is ESCALATE ARCHITECTURE IMPACT (SE11-ADR-04).


## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Authoritative physical mapping of every volume (SE11-DEC-09 / SE11-ADR-09)

This table is the single source of truth for the default mapping (Mapping-D). Sizes are initial allocations (candidate envelope, ASM-SE11-03) and are thin-provisioned so that the sizing document can resize without re-mapping. The alternative Mapping-V of §6.1a swaps the Validation disks and scratch between M2_2 and M2_3; nothing else changes.

| Volume (guest device name) | Pool | Physical device (slot, link) | Initial allocation | Notes |
|---|---|---|---|---|
| Host OS, hypervisor, SE11 host agent store (sequence counter, event log ≤ 1 GB, bootstrap secret store), WSL2 distro disk | `pool.admin` | **M2_1** 1 TB (Gen5 x4, CPU) | whole device | T0 system; rebuildable from the version-controlled host build in `REPO-EXT`; encrypted (§13) |
| Core VM system disk | `pool.core` | **M2_4** 4 TB (Gen4 x4, chipset) | 128 GB | storage-QoS minimum IOPS where available (defence in depth; M2_4 carries Highest-priority only) |
| Core VM state disk (queues, registry, coordination) | `pool.core` | M2_4 | 256 GB | |
| Data VM system disk | `pool.data` | M2_4 | 64 GB | |
| Data VM database / search / cache disk | `pool.data` | M2_4 | 1.5 TB | database-consistent backups to T2 |
| Platform container image layers (Core/Data services) | `pool.core`/`pool.data` | M2_4 | 256 GB | D-REB |
| M2_4 headroom | — | M2_4 | ~1.8 TB | alert 70 %, review 85 % |
| Validation VM system disk (`val-sys`) + replica data disk (`val-data`) | `pool.validate` | **M2_2** 4 TB (Gen5 x4, CPU; shares with USB4) — M2_3 under Mapping-V | 64 GB + 768 GB | production-like replica; fault injection only here; **protected per §6.1a (V_min)** |
| Build VM system disk (`bld-sys`) | `pool.build` | M2_2 | 64 GB | inside B_max (root/system allowance + slice cap, §6.1a) |
| Build VM container layers, agent/test workspaces (`bld-ws`) | `pool.build` members | M2_2 | 512 GB | D-REB; inside B_max |
| Artifact store (`bld-art`; active artifacts, served to all pools over the internal virtual switch) | `pool.build` | M2_2 | 1 TB | D-BND; archival copies to T2; inside B_max |
| M2_2 headroom | — | M2_2 | ~1.6 TB (~1.1 TB when scratch is on M2_2) | |
| Build cache / scratch (`bld-scr`) | `pool.build` | **M2_3** 1 TB (Gen4 x2, chipset; shares with PCI_E3) — a 512 GB virtual disk on M2_2 under Fallback B or Mapping-V | whole device | D-REB; first device to exhaust TBW |
| T2 durable (incl. the `REPO-EXT` mirror) | `pool.durable` | NAS RAID 6 (count per §6.7) over L1 | per §6.7 | snapshots, backups, evidence, archives, mirrors (§164) |
| T3 isolated copy | — | off-site / hosted (provider per NT16, SE11-DEP-09) and/or T3-SUB isolated local medium (§6.3) | local D-IRR classes only | §6.3 |

**Why the mapping deviates from the seed's literal role labels (SE11-DEC-09, conflict C2).** The BOM labels M2_2 "VM & artifact store" and M2_4 "platform data / DBs / containers" (§227.6). Placing *all* VM disks on M2_2 would put the Highest-priority Core and Data system disks on the same device as Medium-priority build artifacts, violating the reservation principle (§157: reserve "storage I/O … for stable platform operation") and SE11-REQ-02. The role labels are guidance on purpose, not an isolation rule; moving the Highest-priority VM disks to M2_4 keeps M2_4 entirely Highest-priority and M2_2 entirely High/Medium. Impact: M2_4 carries both VM system disks and the database — all one priority class; M2_2 carries Validation (High) with Build (Medium), which is exactly the contention that §6.1a bounds. SE11-REQ-02 is satisfied without exception.

### 6.1a Storage I/O budget and protection matrix: Validation versus Build on M2_2 for every lane × QoS combination (SE11-REQ-16, SE11-DEC-16)

**Why a budget.** Validation ("VP validation / release assurance", High, §174) shares M2_2 with Build (Medium) under Mapping-D. Device separation protects Core/Data, not Validation. Protection of critical-validation I/O therefore needs a limiter in every supported combination of (i) the SE11-AC-02 lane-coexistence result for PCI_E3/M2_3 and (ii) the SE11-AC-03 result for hypervisor storage QoS — and the limiter's budget must never exceed the device.

**Measured inputs (SE11-AC-04, M2_2):** `D2` = sustained 4 KiB random 70/30 read/write IOPS at queue depth 32 for 10 min; `S2` = sustained sequential throughput (MB/s, 128 KiB, queue depth 8); `L2` = p99 read latency at 25 % of D2. The limiter's IOPS unit must be the unit D2 was measured in: if the hypervisor normalises I/O size, D2 is re-measured with that normalisation and all budgets are expressed in normalised IOPS.

**Budget identity and calibration (decidable; percentages are ASM-SE11-09/-12 until SE19's measurements replace them).**

| Symbol | Definition | Default |
|---|---|---|
| H_io | Unallocated headroom so the device never runs at its saturation knee | 0.20 × D2 (bytes: 0.20 × S2) |
| A | Allocatable = D2 − H_io | 0.80 × D2 |
| Vdem | Validation's measured p95 aggregate IOPS during its heaviest Stage-1 suite | 0 before measurement |
| V_min | Validation guaranteed minimum (sum over `val-sys`, `val-data`) = max(1.5 × Vdem, 0.20 × D2) | 0.20 × D2 |
| B_floor | Build's minimum useful aggregate IOPS, below which build throughput misses its own NFR | 0.20 × D2 (ASM-SE11-12; SE01/EL may raise it) |
| **Feasibility test** | **V_min + B_floor ≤ A**, i.e. V_min ≤ 0.60 × D2, i.e. Vdem ≤ 0.40 × D2 | evaluated at every calibration |
| B_max | Build aggregate maximum (sum over **all** Build VM virtual disks on M2_2) = **A − V_min** | 0.60 × D2 when V_min is at its floor |
| Identity | **V_min + B_max + H_io = D2 by construction**; the same identity holds in bytes with S2 (V_bytes_min = max(1.5 × Vdem_bytes, 0.20 × S2), B_bytes_max = 0.80 × S2 − V_bytes_min) | always |

Examples: Vdem = 0.10 D2 → V_min = 0.20 D2, B_max = 0.60 D2. Vdem = 0.30 D2 → V_min = 0.45 D2, B_max = 0.35 D2 (≥ B_floor: feasible). Vdem = 0.40 D2 → V_min = 0.60 D2, B_max = 0.20 D2 = B_floor (boundary: feasible). Vdem = 0.45 D2 → V_min = 0.675 D2, B_max would be 0.125 D2 < B_floor → **infeasible** → remedies below.

**Deterministic response when Validation's demand cannot fit (remedies, applied in order to every matrix row):**

| Remedy | Content | Precondition | Effect on the budget |
|---|---|---|---|
| R1 — **Mapping-V** (SE11-ADR-12) | Validation VM disks (`val-sys` + `val-data`, 832 GB) move to the M2_3 device; scratch becomes a 512 GB virtual disk `bld-scr` on M2_2 inside Build's budget. Validation then shares no device with Build | M2_3 operational at ≥ Gen4 x2 (lane outcomes OK, A or C — not Fallback B); Validation's measured demand satisfied on the x2 device (SE11-AC-12b re-run with Validation alone on M2_3: p99 ≤ 2 × L3, L3 = that device's unloaded p99 at 25 % of its D3); Validation capacity ≤ 90 % of the device | On M2_2: V_min not applicable; B_max = A = 0.80 D2 over `bld-sys`, `bld-ws`, `bld-art`, `bld-scr` (headroom protection only). On M2_3: Validation alone; no limiter needed |
| R2 — REV-STORAGE-HOT | Architecture revision (§12.3): the host NVMe topology cannot carry Validation and Build at the measured demands | R1 precondition not met (Fallback B in force, or Validation's demand exceeds the x2 device, or capacity) | None — revision, not a hardware addition |

**Partition of B_max across devices and cgroups (SE11-DEC-16).** The Build VM's virtual disks on M2_2 are separate guest block devices; the budget is split by fixed shares that sum to 100 % of B_max (IOPS and bytes alike), including an allowance for guest root/system I/O that no cgroup controls:

| Guest block device | Without scratch on M2_2 (Mapping-D, lane OK/A/C) | With scratch on M2_2 (Fallback B or Mapping-V) | Controlled by |
|---|---|---|---|
| `bld-sys` — root/system I/O not under a controllable cgroup (init, journal, package cache) | 10 % allowance (ASM-SE11-14) | 10 % allowance | journald rate-limit, package cache off-peak only; **measured, not capped** in the guest |
| `bld-sys` — `build.slice` cap | 5 % | 5 % | `io.max` on `build.slice` for the `bld-sys` device |
| `bld-ws` | 40 % | 25 % | `io.max` on `build.slice` for the `bld-ws` device |
| `bld-art` | 45 % | 30 % | `io.max` on `build.slice` for the `bld-art` device |
| `bld-scr` | — | 30 % | `io.max` on `build.slice` for the `bld-scr` device |
| **Sum** | **100 % of B_max** | **100 % of B_max** | verified by hypervisor per-virtual-disk counters |

Rules: (1) every workload in the Build VM — runners, containers, artifact service, `pool.agents`, `pool.test`, `pool.background` — runs under `build.slice`; nothing outside it may write except the init system and journal; (2) with hypervisor QoS available, the same shares are applied as per-virtual-disk maxima (for `bld-sys` the maximum is 15 % = allowance + slice cap, because the hypervisor cannot distinguish the two) and Validation disks receive QoS minima summing to V_min (`val-sys` 10 %, `val-data` 90 %); (3) with QoS unavailable, `io.max` on `build.slice` carries the per-device caps and Validation is unthrottled; (4) **summed-traffic verification:** during SE11-AC-12b the hypervisor's per-virtual-disk counters for all Build disks are summed every 60 s; the row fails if the sum exceeds B_max by more than 5 % in any window — this catches the uncontrolled root allowance being exceeded as well as a misconfigured slice.

**Lane-coexistence outcomes (SE11-AC-02) and their storage consequence:**

| Outcome | Meaning | Scratch location (Mapping-D) | NIC slot | Mapping-V available? |
|---|---|---|---|---|
| OK | PCI_E3 (NIC) and M2_3 (scratch) operate simultaneously at their expected widths | M2_3 | PCI_E3 | Yes (Validation on M2_3 shares chipset lanes with the NIC; coexistence already proven) |
| Fallback A (SE11-DEC-12, preferred fallback) | They cannot coexist (or M2_3 drops below Gen4 x2) **and the GPU is deferred**: the NIC moves to PCI_E1 (Gen5 x16, CPU lanes), M2_3 keeps scratch | M2_3 | PCI_E1 — TRG-GPU later requires Fallback B or C with a passed SE11-AC-12b before the GPU can take PCI_E1 | Yes (M2_3 free of sharing) |
| Fallback B | They cannot coexist and PCI_E1 is needed (GPU adopted): NIC stays in PCI_E3, M2_3 is emptied, scratch becomes `bld-scr` on M2_2 | M2_2 (inside B_max) | PCI_E3 | **No** (M2_3 unusable) |
| Fallback C | They cannot coexist; NIC moves to PCI_E2 (Gen3 x1); scratch stays on M2_3 | M2_3 | PCI_E2 — L1 bounded by Gen3 x1 (~0.98 GB/s theoretical); allowed only if SE11-AC-05 still shows ≥ 0.7 GB/s host↔NAS (SE11-REQ-04) | Yes |

**Protection matrix — mechanism, admissibility and remedy for every combination:**

| Lane outcome | Hypervisor storage QoS (SE11-AC-03) | Required limiter | Validation impact statement | Admissible? | If the feasibility test or SE11-AC-12b fails |
|---|---|---|---|---|---|
| OK / Fallback A / Fallback C (scratch on M2_3) | available | QoS minima = V_min on Validation disks; QoS maxima = partitioned B_max on Build disks (table above, column "without scratch") | Validation shares M2_2 with `bld-sys`, `bld-ws`, `bld-art`; bounded by B_max | Yes; SE11-AC-12b must pass | R1 Mapping-V → else R2 |
| OK / Fallback A / Fallback C | unavailable | **Guest-side limiter:** `io.max` on `build.slice` per device (column "without scratch"); Validation unthrottled; version-controlled and verified in SE11-AC-03; summed-traffic verification mandatory | As above; a misconfigured guest can exceed the budget — residual SE11-RISK-13, bounded by the summed-traffic check | Yes; SE11-AC-12b must pass | R1 Mapping-V → else R2 |
| Fallback B (scratch on M2_2) | available | QoS as row 1 with the "with scratch" shares; `bld-scr` capped at 30 % of B_max | **Validation is affected:** Build adds cache/scratch traffic to the same device; headroom falls to ~1.1 TB; TBW on M2_2 rises (TRG-NVME-TBW) | Yes; SE11-AC-12b must pass with scratch load included | Fallback A (if the GPU is not yet adopted) → Fallback C (if SE11-AC-05 passes) → **R2** (R1 unavailable: M2_3 unusable) |
| Fallback B | unavailable | Guest `io.max` with the "with scratch" shares, including `bld-scr` | As above plus the guest-side residual | **Only if SE11-AC-12b passes with scratch load included** | Fallback A → Fallback C → **R2** |
| **Mapping-V** (any lane outcome except B) | available or unavailable | On M2_2: `build.slice` caps (or QoS maxima) with the "with scratch" shares summing to B_max = 0.80 D2; on M2_3: none (Validation alone) | Validation isolated at device level; its ceiling is the x2 device's capability (SE11-AC-12b re-run on M2_3) | Yes when R1 preconditions hold | R2 |

**Admission consequence.** A Validation VM may be started only when its row is implemented, the feasibility test passes for the current Vdem and SE11-AC-12b has passed on that combination; the row in force (including Mapping-D/Mapping-V, V_min, B_max and the shares) is recorded in the configuration fingerprint (§11.3) and in the baseline contract (§18.2). Re-calibration is mandatory whenever Validation's measured p95 changes by more than 20 % or Build adds a disk.

### 6.2 Tiers and dataset classes (bootstrap boundary made explicit; SE11-REQ-21)

| Tier | Device(s) | Role (seed) | Durability boundary | Policy owner |
|---|---|---|---|---|
| T0 system | M2_1 | Windows + WSL2 + SE11 host agent (§227.5) | Rebuildable from `REPO-EXT`; the host agent's sequence counter and event log are durable but not unique data (§18.2 recovers from counter loss) | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 (Gen4 x2) or `bld-scr` on M2_2 | Build cache / scratch (§227.5) | Disposable | SE11 |
| T1 hot, Highest | M2_4 | Core/Data VMs, platform data, DBs, platform containers | Independent volume; snapshot + replication to T2 | SE12 (data), EL (VM definitions) |
| T1 hot, High/Medium | M2_2 (and M2_3 for Validation under Mapping-V) | Validation/Build VMs, artifact store | Independent volume; archival replication to T2 | SE12 (artifact retention) |
| T2 durable | NAS RAID 6 | Backups, snapshots, release evidence, VM/container archives, artifacts, repository mirrors (§164) | Dual-parity array + snapshots; "not the only backup" (§164) | SE12 |
| T3 isolated copy | Off-site / hosted, encrypted; or T3-SUB isolated local media (§6.3) | "independent/off-site or otherwise isolated copy" for irreplaceable data (§164) | Independent of room, UPS, NAS and host | SE12 (policy), SE17 (keys after takeover), SE11 (bootstrap custody) |

**Scope rule (SE11-REQ-21).** The protection states of §6.3 govern **real D-IRR data stored on local hardware (T1)**. Data whose authoritative copy lives outside the local hardware is outside the local admission scope; its local copies are D-REB. This boundary is what makes the bootstrap non-circular: the first thing the platform needs — its own source, configuration and commissioning evidence — is never local D-IRR data.

**Dataset classes (provisional default, ASM-SE11-08; SE12 is the classification owner, SE11-DEP-04):**

| Class | Definition | Sub-classes and the store that enforces the creation gate (§6.3) | Minimum protection |
|---|---|---|---|
| D-IRR (local) | Irreplaceable data on local hardware: cannot be re-derived from any other platform data or external authoritative copy | `KEYS` — commissioning secrets (host disk-encryption recovery key, NAS/switch/UPS-software administrative credentials, the exporter and evidence-intake tokens) and, after takeover, platform key backups. Enforcing store: **SE11's bootstrap secret store on the host during commissioning; SE17/SE15's store after takeover** (§6.3 KB-procedure). `DB` — non-synthetic platform databases; enforcing store: SE12's data store. `EVID` — release-evidence packages and decision logs produced by EL/SP14; enforcing store: SE12's evidence storage. `LREPO` — a *local* repository server, **not at baseline**; admitted like any class when adopted, and the class into which the T2 mirror is promoted on provider loss (FD-EXT-REPO) | T1 + T2 + T3 under the state rules of §6.3 |
| D-BND | Bounded loss: re-derivable from D-IRR or from `REPO-EXT` within an accepted window | build artifacts, locally built images, validation results, telemetry history, the SE11 event log | T1 + T2; loss window accepted by SE12 |
| D-REB | Rebuildable from definitions or external authoritative sources | caches, scratch, pulled container layers, VM system disks, **local clones and the T2 mirror of `REPO-EXT`**, **synthetic test fixtures used to verify protection mechanisms** | T1 only (the T2 mirror is itself a rebuildable copy) |
| Outside local scope | `REPO-EXT` — source repositories, IaC, host build, configuration, the version-controlled inventory file, SE11's commissioning and acceptance evidence records: authoritative copy at an **external hosted repository service**, chosen under NT16 (SE11-DEP-09) and configured before any local hardware is commissioned (§160 keeps authoritative source in version control outside any single host) | Durability is the provider's; SE11 bounds provider loss by the T2 mirror (refreshed ≤ 1 h once `PL-T2` holds) and a repository bundle on T3-SUB at every stage gate; on provider loss the mirror is promoted to `LREPO` (§9 FD-EXT-REPO) | provider + T2 mirror + T3-SUB bundle |

### 6.3 Protection states with a legal bootstrap (SE11-REQ-03, SE11-REQ-13, SE11-REQ-17, SE11-REQ-18, SE11-REQ-21, SE11-DEC-18, SE11-DEC-20)

**Three separate things.** *Mechanism readiness* (the T3 copy path, encryption, key recovery and restore for class *c* work) is verified on **synthetic fixtures** (D-REB) — initially before any real dataset of *c* exists (SE11-AC-07b-init) and recurrently at every stage gate while real data exists (SE11-AC-07b-rec; the fixture is a synthetic dataset carried through the same mechanism path, never counted as real data). *Dataset protection* (a real dataset of *c* has a verified copy no older than A_max) begins when the first real dataset is admitted. *Evidence intake* is how the publisher learns of copies, restores and custody: producers push records under `SE11-CONTRACT-protection-evidence@1` (§18.2 Part C); the absence of evidence is itself the fail-safe (ageing continues).

**Per-class record (held and published by the SE11 host agent).** Each local D-IRR class *c* carries: `mech_ok(c)` = timestamp of the last passed fixture verification (init or rec); `t3_last_ok(c)` = reference timestamp for copy age; `kind(c)` ∈ {ANCHOR, COPY}; `age(c)` = now − `t3_last_ok(c)`; `store(c)` = the enforcing store's producer id; `A_max` = 24 h, `G` = 24 h (ASM-SE11-10 until SE12 binds them, SE11-DEP-04); derived levels `admit(c)` ∈ {ALLOW, DENY} and `mutate(c)` ∈ {ALLOW, FREEZE}.

| State of class c | Definition | `admit(c)` (create the first / a new real dataset) | `mutate(c)` (existing real datasets) | Mandatory actions / notes |
|---|---|---|---|---|
| MECH-UNVERIFIED | No passed fixture verification for c (or the last one older than one stage, or failed), **or no registered producer for `store(c)`** | DENY — only synthetic fixtures (D-REB) may exist | n/a (no real data) | Commission the T3 mechanism; register the store's producer; run SE11-AC-07b-init on a fixture |
| ARMED | `mech_ok(c)` within the current stage; custody for c commissioned (KEYS: KB-procedure complete); producer registered; **no real dataset exists** | ALLOW → the class enters PROTECTED with `t3_last_ok(c) := t_create`, `kind := ANCHOR`, and the store triggers the initial T3 copy immediately | n/a | Re-verify the fixture at every stage gate (SE11-AC-07b-rec applies once real data exists); if it fails → MECH-UNVERIFIED |
| PROTECTED | Real datasets exist; `age(c)` ≤ A_max. `kind = ANCHOR` until the first verified real copy (then `kind := COPY`, `t3_last_ok(c)` := copy time) | ALLOW | ALLOW | T3 copy at interval ≤ A_max; `SIG-PROTECTION-STATE` carries the level. **Copy timestamps are recovery-capable only when kind = COPY** |
| DEGRADED-IN-BUDGET | Real datasets exist; A_max < `age(c)` ≤ A_max + G (initial copy missed, T3 path lost, internet down, copy failing) | DENY | ALLOW | Level change published within 60 s; T3 copy retried every 1 h; SE20 prepares T3-SUB (encrypted isolated local copy) so it can be taken before expiry; exposure window logged |
| EXPIRED | `age(c)` > A_max + G, **or** the last restore verification failed | DENY | ALLOW **only while a T3-SUB copy of c with age ≤ A_max exists** (evidence `COPY_OK target=T3SUB`); otherwise FREEZE — enforced by `store(c)` (SE11-REQ-18) until a T3 or T3-SUB copy succeeds | SE20 incident; SE12 decides whether to extend via T3-SUB or hold the freeze; every hour in EXPIRED is logged against the stage's exposure budget |

**Transitions.** MECH-UNVERIFIED → ARMED: SE11-AC-07b-init(c) passes (fixture copied, restored, keys recovered) and `store(c)` is registered. ARMED → PROTECTED(ANCHOR): the enforcing store admits the first real dataset (it reads `admit(c) = ALLOW` from the signals contract, creates, and reports `DATASET_CREATED` under Part C). PROTECTED(ANCHOR) → PROTECTED(COPY): first `COPY_OK` + `RESTORE_OK` evidence for a real copy. PROTECTED → DEGRADED → EXPIRED and back by age, as the table states. ARMED → MECH-UNVERIFIED: stage-gate re-verification fails or the mechanism is lost before any real dataset exists. A class with real data never returns to ARMED; if its mechanism is lost it ages into DEGRADED/EXPIRED.

**SE11-REQ-03 (rewritten; replaces the v4 wording that contradicted ANCHOR).** T0/T1 is never the sole copy of D-IRR or D-BND data beyond the declared windows: every T1 dataset has a T2 copy within the snapshot interval of SE11-NFR-05; every real local D-IRR class is at every moment in exactly one of the states above, and its exposure to total local loss is **bounded** by the state rule: zero beyond `age(c)` when kind = COPY; the whole class when kind = ANCHOR, which can last at most A_max (then DEGRADED) + G (then EXPIRED, freeze or T3-SUB). The ANCHOR window is a declared, bounded exposure, not an exception to this requirement.

**Platform-level derived state (published as `SIG-PL-STATE`; "real D-IRR" means local, per SE11-REQ-21):** `PL-0` = before SE11-AC-07a (only D-REB and synthetic data on local T1; no verified T2); `PL-T2` = SE11-AC-07a passed and no real local D-IRR data exists (classes MECH-UNVERIFIED or ARMED only); `PL-T3-PENDING` = every class with real data is PROTECTED and at least one is ANCHOR; `PL-T3` = every class with real data is PROTECTED with kind COPY; `PL-DEG` = at least one class DEGRADED-IN-BUDGET and none EXPIRED; `PL-EXP` = at least one class EXPIRED.

**Invariants (checked at every step of SE11-AC-07d and by SE11-AC-10).** (I1) A real local D-IRR dataset of class c exists only if c was ARMED at the moment of its creation or c already held real data in PROTECTED (creation gate). (I2) In `PL-0` and `PL-T2` no real local D-IRR data exists. (I3) In `PL-DEG`/`PL-EXP` real D-IRR data exists and is exposed to FD-STORAGE/FD-ROOM for at most `age(c)`; the exposure is bounded by A_max + G plus the T3-SUB age. (I4) SE11-AC-10 passes only in `PL-T2` or `PL-T3` (never `PL-T3-PENDING`, `PL-DEG`, `PL-EXP`). (I5) T3-dependent recovery (§6.6) is valid for class c only from a COPY; while kind = ANCHOR a loss of T1 and T2 loses the class entirely, and by the state rule that class is at most A_max + G old. (I6) No real local D-IRR data exists in a class whose enforcing store has no registered producer — a class whose owner's store does not yet exist is MECH-UNVERIFIED by definition, so the absence of an owner document can never produce unprotected data.

**Class-specific activation.**
- `REPO-EXT` (outside scope): configured in the host build **before** any local hardware is commissioned; the first commit is the host build itself; commissioning evidence, the inventory file and every SE11 acceptance record are committed there and inherit the provider's durability; the T2 mirror and the T3-SUB bundle bound provider loss (§6.2). Nothing here creates local D-IRR data.
- `KEYS` — **bootstrap custody procedure (KB), owned by SE11 so that commissioning needs no absent owner:** KB-1 prepare two T3-SUB media (removable, encrypted under an operator-held passphrase that is never stored on the platform, ASM-SE11-17), store them outside the room; KB-2 SE11-AC-07b-init(KEYS) with a test secret: write to both media, read back on a second machine, checksum-compare → `mech_ok(KEYS)`; register SE11's bootstrap store as producer → ARMED; KB-3 at commissioning each real secret is generated, written to both media and read back **before** it is used (the recovery key before encryption is enabled, the administrative credential before the default is rotated away); the store reports `DATASET_CREATED` then `COPY_OK target=T3SUB` + `RESTORE_OK` → the class passes through ANCHOR to COPY within the same commissioning step; KB-4 recurring: SE11-AC-07b-rec at every stage gate with a fresh test secret; KB-5 takeover: SE17/SE15 register their store as the new producer, import the secrets, copy them to their T3 path with `COPY_OK`/`RESTORE_OK`, and only then is SE11's bootstrap store retired (both producers registered during the overlap; the class stays PROTECTED throughout).
- `DB`, `EVID`: fixture = a synthetic dataset of the class carried through the owner's backup path to T3 and restored (SE11-AC-07b-init); real data admitted from ARMED only, by the owner's store. Until SE12's store exists and registers, the class is MECH-UNVERIFIED and holds no real data (I6).
- `LREPO`: not at baseline; on adoption, fixture = a test repository; on FD-EXT-REPO promotion, the T2 mirror enters PROTECTED(ANCHOR) with `t3_last_ok := last mirror refresh` and must receive a T3 copy (T3-SUB bundle or a new external remote) within A_max.

**Outage tolerance.** The tolerance of class c to loss of the T3 path is its **remaining copy-age budget**, `A_max − age(c)` at the moment the outage starts (then G of degraded operation), not a fixed 24 h.

**Restoration.** T3 path restored → a full copy of class c completes (`COPY_OK`) → sample restore verification passes (`RESTORE_OK`) → `t3_last_ok(c)` updated, kind COPY → PROTECTED; `mutate(c)` returns to ALLOW and the store lifts its freeze on the published level.

**Enforcement and ownership (SE11-REQ-18, contract-bound).** SE11 publishes `mech_ok`, `t3_last_ok`, `kind`, `age`, the class state, `admit(c)`, `mutate(c)` and the platform state under `SE11-CONTRACT-hardware-signals@1`, and accepts evidence under `SE11-CONTRACT-protection-evidence@1` (§18.2). The gates are enforced by the store that holds the class, consuming the published levels: SE11's bootstrap store for `KEYS` during commissioning; SE12's stores for `DB` and `EVID`; SE17/SE15's store for `KEYS` after takeover. SE11 has no hardware-level backstop for a write-freeze in another owner's store and does not claim one; what it guarantees is that **no class can hold real data unless its store has registered as a producer and consumes the levels** (I6, SE11-AC-07d negative check (7)). T3-SUB is an encrypted copy to removable media or a second independent location kept outside the room (§164 "otherwise isolated copy"), restore-verified in SE11-AC-07b; it is a bridging measure for DB/EVID and the bootstrap T3 for KEYS.

**Verification.** SE11-AC-07b-init (fixture-based mechanism verification → ARMED, per class, no real data of the class present), SE11-AC-07b-rec (recurring fixture verification with real data present), SE11-AC-07c (expiry drill), SE11-AC-07d (from-empty-platform activation trace, §14), SE11-AC-10 (I4).

### 6.4 Bandwidth / IOPS / latency assumptions (device-class figures from the BOM; measured values replace them in SE11-AC-04)

| Path | Nominal from BOM | Engineering assumption used for design |
|---|---|---|
| M2_1, M2_2, M2_4 (Gen4 x4 devices) | up to 7,300 / 6,300 MB/s (§227.5–§227.6) | Sustained mixed workload 2–4 GB/s per device; sub-millisecond latency; NVMe is not the first bottleneck; D2, S2 and L2 measured for §6.1a |
| M2_3 (Gen4 x2 slot shared with PCI_E3) | device 7,300 MB/s; slot ≈ half of x4 | ≈ 3–3.5 GB/s ceiling; acceptable for scratch, and for Validation under Mapping-V only if SE11-AC-12b passes on it; verified in SE11-AC-02/04 |
| Host ↔ NAS over 10 GbE (L1) | 10 Gb/s ≈ 1.1–1.2 GB/s wire (Fallback C: ≤ ~0.98 GB/s) | 0.7–1.0 GB/s sustained for backup/artifact transfer; a 4–6 drive RAID 6 CMR array delivers on the order of 0.5–1.0 GB/s sequential and far lower random IOPS — the NAS is never used for random-IO workloads (§164) |
| Endurance | 600 TBW (1 TB), 2,400 TBW (4 TB) (§227.5–§227.6) | Scratch exhausts TBW first; when scratch is on M2_2, that device's consumption rises; TBW telemetry mandatory (§10.3); replacement by specification class (§11.4) |

### 6.5 RAID / replication boundaries

- Host NVMe: no RAID. Independence of M2_2 and M2_4 (and M2_3 under Mapping-V) is the only host-level isolation; redundancy is by replication to T2 (SE11-ADR-05). Rationale: host mirroring would double NVMe cost for a tier whose durability requirement is met by snapshot + replication and would not protect against host loss, the dominant failure domain (§9).
- NAS: RAID 6 at any drive count ≥ 4 (dual parity is mandatory at 20 TB per drive because the rebuild window — planning assumption 1–3 days under concurrent load, ASM-SE11-04 — must tolerate a second loss). Snapshots guard against logical corruption; T3 guards against array, enclosure, power or site loss (§164).
- Replication is one-way T1 → T2 → T3; T2 never serves as a live datastore for VMs or databases.
- The BOM's NVMe is a client-class device; power-loss protection of in-flight writes is **not asserted** (§11.2). Crash consistency therefore relies on filesystem journaling in every VM, database write-ahead logging with synchronous commit (SE12), and NAS copy-on-write; all are verified by the abrupt-loss drill SE11-AC-13 (SE11-NFR-07).

### 6.6 Recovery expectations (hardware-capable targets stated to SE12; SE12 sets the binding RPO/RTO)

**T2-only recoveries (no T3 dependency):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| M2_4 failure (Core + Data VMs, platform data) | Full platform outage; restore both VMs and database from the last T2 snapshot/backup; data loss ≤ snapshot interval (≤ 1 h, SE11-NFR-05); RTO ≤ 4 h per VM | Spare NVMe of the §11.4 class; SE12 schedule |
| M2_2 failure (Build VM, artifacts; Validation too under Mapping-D; scratch too when on M2_2) | Build/validation outage; runtime continues; restore from T2 archives or rebuild from definitions; D-BND loss within SE12's accepted window | Spare NVMe |
| M2_1 failure (host OS, host agent store) | All VMs stop until the host OS is rebuilt from `REPO-EXT` onto a replacement device; VM disks on M2_2/M2_4 remain intact; the host agent restarts with a sequence counter per §18.2 (counter-loss rule) and re-derives protection levels from the last evidence held in `REPO-EXT`/T2 (fail-safe: unknown → DENY until evidence is re-ingested) | Spare NVMe; host build definition in `REPO-EXT` |
| M2_3 failure | Mapping-D: rebuild caches, no data loss, interim scratch on M2_2 if no spare; Mapping-V: Validation outage, restore from T2/definitions | Spare NVMe or fallback mapping |
| Single NAS drive failure | No data loss; degraded; rebuild window ASM-SE11-04; replacement drive of equivalent class | Free bays allow a hot spare as an SE12 decision |
| Two concurrent NAS drive failures | No data loss (RAID 6) | — |
| Host loss (board/CPU/PSU) with intact NVMe | Move the NVMe devices to a replacement host of the §11.4 class or restore VMs to a hosted equivalent (§160, §168) | Hardware-independent definitions (SE11-REQ-05) |

**T3-dependent recoveries (valid per class only from a COPY, §6.3 I5; loss window = `age(c)` at the moment of loss; a class still at ANCHOR is lost entirely, bounded by A_max + G of existence; in `PL-T2` no real local D-IRR data exists, so the residual is the loss of D-BND/D-REB only):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| Third NAS drive failure before rebuild completes (array loss) | Restore each D-IRR class from T3 with loss ≤ `age(c)`; D-BND re-derived; `REPO-EXT` mirror re-cloned | Verified T3 copy per class |
| NAS enclosure loss | T1 continues without a local backup target (degraded, time-boxed by SE12); D-IRR protected by T3 until the NAS is replaced; classes move to DEGRADED when their T2→T3 pipeline depends on the NAS | T3 |
| Host loss with NVMe loss, room/site loss (FD-ROOM) | Rebuild on replacement or hosted infrastructure from `REPO-EXT` (definitions), T3 (D-IRR, loss ≤ `age(c)`) and the KEYS T3-SUB media; D-BND re-derived | T3, T3-SUB, hosted fallback |
| External repository provider loss (FD-EXT-REPO) | Promote the T2 mirror to `LREPO` (PROTECTED(ANCHOR) at the last refresh time); establish a new remote or T3-SUB bundle within A_max | T2 mirror; stage-gate bundle |

### 6.7 Capacity headroom and NAS capacity candidates (SE11-DEC-06)

| Tier | Candidate / installed | Headroom rule | Expansion path |
|---|---|---|---|
| T1 (M2_2 + M2_4) | 2 × 4 TB (fixed by B6 class) | Alert 70 %, architecture review 85 % (REV-STORAGE-HOT) | No free M.2 slots: larger devices of the same class (scale-up) or artifact store fronted by T2; SATA ×4 for cold tiers only |
| T2 NAS — **N-A** (default) | 4 × 20 TB RAID 6 → 40 TB nominal, ≈ 36.4 TiB usable (derived with the seed's 80 TB → 72.8 TiB ratio, ASM-SE11-04); 4 bays free | Alert 70 %, review 80 % | Add same-class drives to free bays on TRG-NAS-CAP (online array expansion support by the NAS OS not established — FC-08) |
| T2 NAS — **N-B** | 6 × 20 TB RAID 6 → ≈ 72.8 TiB usable (seed reference); 2 bays free | as above | 2 free bays |
| T2/T3 — **N-C** | Hosted object storage for T2 and/or T3 (NAS deferred or absent) | provider quota | Hosted elasticity; acceptable per §238; economics unknown (SE11-DEP-08) |
| T3 | Must hold at least the local D-IRR set per class; T3-SUB media sized to the same set plus the repository bundle | n/a | Provider/medium per SE12 and NT16 (SE11-DEP-04/09) |

**Decision rule (SE11-DEC-06).** Let V be SE12's modelled retention volume for the first two stages (D-IRR + D-BND copies at the retention policy, including snapshot overhead and the `REPO-EXT` mirror). Choose N-A if V ≤ 22 TiB (≈ 60 % of N-A usable); N-B if 22 TiB < V ≤ 44 TiB; above 44 TiB the answer is REV-STORAGE (architecture revision), not simply more drives; N-C if gate G-LOCAL fails for the NAS. If the NAS must be commissioned before the model exists, **N-A** is installed (H.1/H.3) and the choice is recorded as SE11-DEC-06a in the sizing document. **Six drives are never adopted on the strength of this document alone.**


## 7. Network architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-06)

### 7.1 Physical links and roles

| Link | Speed / media | Endpoints | Role |
|---|---|---|---|
| L1 storage/core | 10GBase-T, Cat6a | Host NIC (PCI_E3; PCI_E1 under Fallback A; PCI_E2 under Fallback C) ↔ switch ↔ NAS 10 GbE port 1 | Backup, artifact, database-dump, VM-archive, repository-mirror transfers; "network capacity appropriate to measured artifact, backup, database, and build traffic" (§166); NAS shutdown command path under S-1 (§8.3) |
| L2 management/upstream | 5 GbE onboard, Cat6a | Host onboard LAN ↔ switch | Host/VM management, upstream gateway, external-provider traffic incl. `REPO-EXT` and T3 |
| L3 NAS secondary | 10 GbE port 2 (spare), 2×5 GbE | NAS ↔ switch | Expansion: second 10 GbE consumer or link redundancy; 5 GbE for the NAS management segment (carries the N1 wake frame) |
| L4 worker links | 1 / 2.5 GbE (deferred) | Local workers ↔ switch access ports | "Worker links may be slower where sufficient" (§166) |
| L5 uplink | per upstream gateway | Switch ↔ gateway | Internet; external AI providers; hosted runners; T3 transfers; `REPO-EXT` |
| Wi-Fi 7 / Bluetooth | — | Host (disabled) | Not part of the architecture; disabled in firmware (§13) |

SE11-REQ-04: L1 sustains ≥ 0.7 GB/s host↔NAS during concurrent build-cache activity, and shared storage or control paths are not the first bottleneck during concurrent transfers (§166) — SE11-NFR-02, verified in SE11-AC-05 for the NIC slot actually in use (Fallback C is admissible only if this passes).

### 7.2 Switching / core role

The switch (B17 class) is the single core: managed, VLAN-capable, at least 2×10 GbE (seed minimum, §230) with ≥ 4×10 GbE preferred so that host, NAS primary, NAS secondary and one future 10 GbE consumer fit without replacement (SE11-ADR-07); 24 access ports at ≥ 1 GbE for workers, management devices and the gateway. It is adopted ahead of the rack (conflict C4) because the management segment and VLAN enforcement need it. Until the switch is installed, an interim point-to-point 10 GbE link host↔NAS with L2 to the gateway is acceptable *placement* — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2); in that interim the S-1 NAS shutdown command and the N1 wake frame run over the point-to-point link, which removes the switch from the shutdown and restart paths. Power: the switch is on PD-A (conflict C1; §165 names "critical network components" among the PC+NAS UPS loads) — which is also what keeps N1 deliverable while UPS-A output is live (§8.3a).

### 7.3 Segmentation (SE11 designs the physical segments, VLAN membership and addressing; SE17 owns the security policy applied between them, SE11-DEP-05; SE14 is consulted for portable naming)

| Segment | Members | Purpose | Policy owner |
|---|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS software endpoint, SE11 telemetry/evidence endpoint (§10.3, §18.2) | Administrative plane; MFA-protected access (§59); no workload traffic; carries the S-1/S-2 shutdown signalling, the N1 wake frames and the evidence-intake calls | SE17 (SE11-SECREQ-03) |
| `seg.storage` | Host 10 GbE, NAS 10 GbE | Backup/artifact/mirror traffic only; not routed to workers | SE17 |
| `seg.platform` | Core VM, Data VM, runtime namespaces | Stable runtime east-west | SE17 |
| `seg.build` | Build VM, Validation VM, member containers | Build/test east-west; fault injection confined here | SE17 |
| `seg.worker` | Local workers (deferred), hosted-runner VPN/egress | Disposable execution | SE17 |
| `seg.egress` | Gateway-facing | Default-deny disclosure gateway for external model inputs (§66, §185) sits on this boundary; `REPO-EXT` and T3 egress are explicit allow-list flows | SE17 / EL |

### 7.4 East-west traffic and bottleneck avoidance

- Build artifacts move Build VM → artifact store (same device, M2_2) over the host-internal virtual switch; only archival copies cross L1 to the NAS, scheduled by SE20 outside peak build windows.
- Database backups cross L1 off-peak; restore drills (§14) measure actual throughput to replace §6.4 assumptions.
- Worker-to-core control traffic is small; worker artifact pulls are served from the host artifact store, not the NAS.
- Management (`seg.mgmt`) and storage (`seg.storage`) traffic never share a VLAN; the NAS shutdown command, the N1 frame and evidence intake are management-plane flows.

### 7.5 Expansion ports / headroom

Free after baseline: NAS 1×10 GbE + 2×5 GbE; host 2×USB4 (emergency 10 GbE/NVMe adapters); switch access ports per §7.2. Triggers in §12.2.


## 8. Physical power / placement architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

### 8.1 Power domains

| Domain | UPS | Circuit (requirement, not design) | Loads | Status |
|---|---|---|---|---|
| PD-A | UPS-A, class B15 (1500 VA / 1000 W, pure sine, line-interactive AVR, 6 battery outlets, USB HID) | Circuit A: separate 15 A breaker; UPS plugged directly into wall (§231) | Central host, switch; NAS in S-1/S-2 | ADOPT WITH ENGINEERING CONSTRAINT |
| PD-N | UPS-N, class B16 (≥ 1000 VA / 600 W pure sine, USB HID) — **only under candidate S-3** | Circuit A or B as the electrician decides under SE11-REQ-10 | NAS only | Conditional (SE11-DEC-10) |
| PD-B | UPS-B, class B16 | Circuit B: second separate 15 A breaker (§231) | Rack PDU → local workers (and the switch only under S-3, conflict C1) | DEFER / OPTIONAL with the rack |

Isolation rule (§165): worker/rack power is isolated from the host/NAS UPS so a worker fault or overload cannot drop the durable tier. The upstream gateway is placed on PD-A only if the measured PD-A load leaves the runtime reserve of §8.4 intact; otherwise it is powered separately (its loss during an outage is acceptable: no shutdown or restart sequence depends on it — N1 frames are switched locally).

### 8.2 Device power envelopes and circuit/load assumptions

| Device | Envelope used for planning | Source / assumption |
|---|---|---|
| Central host, no GPU | ~350–480 W peak at wall (CPU package ≤ 230 W + board/memory/4×NVMe/fans/NIC + PSU losses); host-only idle/boot ~100–150 W | B1, B7; ASM-SE11-05, replaced by SE11-AC-06 measurement |
| Central host, with GPU | +145 W → ~500–630 W peak | B11 |
| NAS, 4–6 HDD + 2 M.2 | ~70–150 W (spin-up transient higher) | B12/B14 class; ASM-SE11-05 |
| Switch (+ gateway if on PD-A) | ~30–80 W | class estimate, ASM-SE11-05 |
| PD-A total | ~450–710 W without GPU; ~600–860 W with GPU (S-1/S-2); ~380–560 W / ~530–710 W under S-3 (NAS on PD-N) — below the 1000 W rating, but battery runtime at these loads is minutes: UPS-A is a controlled-shutdown device, not a ride-through supply (§165) | SE11-AC-06 verifies |
| Whole installation | Seed figures: typical ~560 W, sustained peak ~1,150–1,300 W when the rack is present (§231) | Circuit-sizing input for the electrician |

SE11-REQ-10 (qualified-professional requirement; code-regulated work is not designed here): a licensed electrician verifies that circuits A and B are separate branch circuits of adequate rating for the measured/peak loads above, that receptacles, grounding and surge arrangements meet local code, and whether the optional dedicated 20 A circuit (§231) is warranted; SE11 supplies only the load figures and the two-domain requirement.

### 8.3 Safe-shutdown signalling and per-candidate timed sequences (SE11-DEC-07, SE11-DEC-10)

**Signalling topology — gated decision (SE11-DEC-10, conflict C3).** The corpus names two integration surfaces: "automatic graceful shutdown via PowerPanel / NAS UPS service" on the UPS (§229.1) and "UPS support / network UPS server" on the NAS (§228.1). It does **not** establish any protocol/client/version combination between them. SE11 records three candidates and a gate:

| Candidate | Topology | Cross-device integration required | Status |
|---|---|---|---|
| S-1 (preferred) | UPS-A USB-HID → central host running the UPS vendor's host shutdown software; the host orchestrates VM shutdown and issues an authenticated remote shutdown command to the NAS over `seg.mgmt` | Host↔UPS: vendor software on the host OS version; host→NAS: a remote shutdown interface supported by the NAS OS | Gated by G1 evidence (dated vendor documentation for both interfaces at the exact versions; FC-09) |
| S-2 | UPS-A USB-HID → NAS as network UPS server; host as network client | NAS server protocol ↔ a host client implementing it; **and** the NAS UPS service able to command the UPS output cycle (FC-09b) — the only restart mechanism S-2 admits (§8.3a) | Gated by G1 evidence (FC-09, FC-09b) |
| S-3 (protocol-agnostic fallback) | Two UPS units, each with its own USB-HID path: UPS-A → host; UPS-N (class B16) → NAS | None across devices | Adopted automatically if neither S-1 nor S-2 produces evidence; recorded as a new SE11-DEC (topology substitution of B15) |

No shutdown sequence is relied on until the selected candidate × mechanism combination is admissible (§8.3a) and has passed SE11-AC-06, SE11-AC-14 and SE11-AC-15.

**Common parameters (defaults; SE11-AC-06/15 replace them with measured values):** T_hold = 60 s (on-battery hold before the sequence starts; 0 s when battery charge < 50 %, see restart rules); VM graceful-stop timeouts Build 60 s, Validation 60 s, Core 60 s, Data 90 s, then forced stop (a forced stop marks the VM "unclean" so that its filesystem integrity check runs before services start on the next boot, §5.4); host OS shutdown ≤ 60 s; NAS own shutdown ≤ 120 s; NAS command acknowledgment ≤ 15 s, one retry (≤ 15 s), then proceed regardless; margin M = 30 s. **Once S2 is entered the sequence is never aborted**, including by mains restoration (deterministic, bounded); restoration is handled by the restart mechanisms of §8.3b. Serial order Core → Data is kept because Core services depend on Data; Build and Validation stop in parallel with each other and with the NAS command.

**Candidate S-1 — timed sequence (t = 0 at S2 entry = T0 + T_hold):**

| t (s) | Host path (serial unless marked ‖) | NAS path (concurrent) |
|---|---|---|
| 0 | `SIG-SHUTDOWN` published ‖ send NAS shutdown command (ack ≤ 15 s; retry once by t = 30; proceed regardless) ‖ graceful stop Build and Validation (timeout 60) | Command received by t ≤ 30 |
| 60 | Build, Validation stopped (forced if needed) → graceful stop Core (timeout 60) | NAS shutdown in progress (≤ 120 s from receipt) |
| 120 | Core stopped → graceful stop Data (timeout 90) | NAS off by t ≤ 150 |
| 210 | Data stopped → host issues the restart-mechanism command (M1: D_off = 120 s; or arms the M3 alarm) → host OS shutdown (≤ 60) | — |
| 270 | Host off (**host critical path 270 s**) | — |
| 330 | (M1 only) UPS-A outputs drop: 60 s after the last device off | — |

UPS-A critical path from S2 entry = max(host 270, NAS 150) = **270 s**. **B_A(S-1) = T_hold 60 + 270 + M 30 = 360 s** → required measured runtime **R_A ≥ 360 / 0.7 = 515 s (8.6 min)** at the measured PD-A load (host + NAS + switch). The M1 output drop at 330 is outside the budget: if the battery exhausts before 330 the outputs drop anyway and the exhaustion-and-return path applies.

**Candidate S-2 — timed sequence (NAS is the UPS server; the host is its client):**

| t (s) | NAS path | Host path |
|---|---|---|
| −60 … 0 | NAS detects on-battery at T0 (detection ≤ 10 s), notifies the host; both hold T_hold = 60 s | Host receives on-battery notification, publishes `SIG-ONBATTERY` |
| 0 | NAS enters its own S2: waits for the host's "client shutdown complete" message for at most W_nas = 240 s | Host sequence identical to S-1 rows 0–210 (Build‖Validation 0–60, Core 60–120, Data 120–210) |
| 210 | — | Host sends "client shutdown complete" to the NAS, starts host OS shutdown (no M3 arming: inadmissible under S-2, §8.3a) |
| 240 | W_nas elapses (host confirmation arrived at 210; if it never arrives the NAS proceeds anyway) → NAS issues M1 (D_off = 180 s) → NAS shutdown ≤ 120 s | Host off by 270 |
| 360 | NAS off (**UPS-A critical path 360 s**) | — |
| 420 | (M1) UPS-A outputs drop: 60 s after the last device off | — |

**B_A(S-2) = 60 + 360 + 30 = 450 s** → **R_A ≥ 643 s (10.7 min)**. If the NAS OS cannot wait ≥ 240 s for the client, or cannot command the UPS output cycle (FC-09b), S-2 is not admissible — a G1 check.

**Candidate S-3 — two independent sequences:**

| UPS | Sequence | Critical path | Budget | Required runtime | M1 command / output drop |
|---|---|---|---|---|---|
| UPS-A (host + switch) | As S-1 host path without the NAS command: Build‖Validation 0–60, Core 60–120, Data 120–210, M1/M3 + host shutdown 210–270 | 270 s | **B_A(S-3) = 60 + 270 + 30 = 360 s** | **R_A ≥ 515 s** at PD-A load (host + switch) | Host commands at 210, D_off = 120 → drop at 330 |
| UPS-N (NAS only) | NAS on-battery at T0 → T_hold 60 s → NAS issues M1-N (if evidenced) → NAS own shutdown ≤ 120 s | 120 s | **B_N = 60 + 120 + 30 = 210 s** | **R_N ≥ 300 s (5 min)** at the measured NAS load — measured separately in SE11-AC-06 | NAS commands at 60, D_off = 180 → drop at 240 |

The NAS shutting down before the host is harmless: no shutdown step of the host depends on the NAS, and in-flight backup jobs are resumable (§175). Restart ordering (NAS reachable before the Data services start) is handled in S6 (§8.3b).

**State machine (all candidates; the timed sequences above are the content of S2/S3):**

| State | Entry event | Actions | Bounded exit |
|---|---|---|---|
| S0 ONLINE | mains and UPS communication healthy | normal operation; UPS telemetry sampled ≤ 60 s | — |
| S1 ON-BATTERY (hold) | E1 mains loss at T0 | publish `SIG-ONBATTERY` (the scheduler may stop admitting `pool.build`/`pool.background` work — EL/SE01 policy, SE11-DEC-11; nothing below depends on it); alert SE20 | E2 mains restored before T0 + T_hold → S0 and `SIG-ONBATTERY` cleared; else E3 → S2 |
| S2 SHUTDOWN-INITIATED | E3: T0 + T_hold elapsed, **or** UPS low-battery, **or** UPS runtime estimate < B_u for that UPS, **or** E4 UPS-communication loss while in S1 (fail-safe: proceed) | the candidate's timed sequence; **never aborted** | → S3 within the candidate's host critical path (270 s) |
| S3 HOST-OFF | host power off | NAS completes its own path (S-1: off by t = 150, already done; S-2: off by t = 360; S-3: independent) | → S4 |
| S4 ALL-OFF | all devices halted; UPS output may still be live if mains returned during S2/S3 | M1: outputs drop at the commanded time and re-energise on mains; M3: the wake-poll loop runs; otherwise attended | → S5 |
| S5 RESTART-PENDING | E5: AC applied to the devices (exhaustion-and-return, or M1's output cycle), **or** an M3 wake that finds mains online | host firmware "restore on AC power loss = power on" and NAS "power-on after AC recovery" bring both up where AC was cycled; under M3 the host wakes by RTC and the NAS by N1 **after** the host has confirmed mains online; host UPS software reads mains state and battery charge **from its own direct UPS link** | → S6 when mains online **and** charge ≥ 50 % **and** estimated runtime at current charge ≥ B_u / 0.7; until then the host stays in HOST-ONLY (no VM auto-start, no N1) with T_hold = 0 so that a second mains loss triggers an immediate host-only shutdown (B_hostonly = 0 + 60 + 30 = 90 s, needing R ≥ 130 s). Time spent waiting for charge is logged as *charge-limited restart* and is excluded from T_restart |
| S6 RESTARTED | charge and runtime conditions met | the S6 ladder of §8.3b (N1 if the NAS is unreachable; Data VM; NAS-wait cap; Core; Validation; Build); unclean VMs run integrity checks first; protection levels re-published; SE20 post-event check of backups, telemetry and protection states | → S0 |

### 8.3a Admissibility matrix: signalling candidate × restart mechanism (SE11-DEC-19, SE11-ADR-13)

**Wake rule R-WAKE (the rule the matrix is derived from).** After S3, a device may be powered or woken only by (a) an AC-input cycle at its own input (exhaustion-and-return, or an M1 output cycle), or (b) a command issued by a device that has itself confirmed *mains online* through a **direct** UPS link within T_decide of issuing the command. No device is woken on an unknown or on-battery power state. Consequence: under S-2 the only device with a direct UPS link is the NAS, and the NAS is off after its own shutdown; the host therefore cannot satisfy (b), and waking the NAS to ask it would violate R-WAKE. Hence **S-2 admits only M1** (the NAS UPS service commands the output cycle before it shuts down; both devices restart by firmware AC-recovery when the outputs re-energise on mains).

| Candidate | Host restart | NAS restart | Admissible combination | Inadmissible (recorded as FD-RESTART exposure, SE11-RISK-12, if no admissible combination is evidenced) |
|---|---|---|---|---|
| S-1 (UPS-A link at host) | M1 (host commands UPS-A) or M3 (RTC wake; host reads UPS-A directly) | under M1: AC cycle (same UPS-A output) + NAS firmware AC-recovery; under M3: **N1** (Wake-on-LAN sent by the host at S6 entry, NAS on the live UPS-A output, frame via the switch on PD-A or the point-to-point link) | **S-1/M1**; **S-1/M3+N1** | S-1/M3 without evidenced N1 (NAS attended); M4 |
| S-2 (UPS-A link at NAS) | M1 only, commanded by the NAS UPS service (FC-09b) — AC cycle + host firmware AC-recovery | M1 (same output cycle) | **S-2/M1** | **S-2/M3 (any variant)** — violates R-WAKE; refused by the configuration validator (SE11-AC-15 drill (g)); S-2 without FC-09b evidence → S-2 itself inadmissible → S-3 |
| S-3 (UPS-A at host, UPS-N at NAS) | M1 or M3 (host reads UPS-A directly) | **M1-N** (NAS commands UPS-N output cycle, FC-09b) or **N1** (host, after its own S6 entry with mains confirmed, sends Wake-on-LAN; NAS on the live or re-energised UPS-N output) | **S-3/{M1 or M3}/{M1-N or N1}** | NAS attended; M4 |

Rules: **if M1 is evidenced it is mandatory** for the device that owns the UPS link; M3 is used only where M1 is not; M4 is never a pass for SE11-REQ-15. The selected combination is recorded in the configuration fingerprint and validated against this matrix by the version-controlled configuration validator; an inadmissible combination cannot be committed.

### 8.3b Restart mechanisms and end-to-end timing to service readiness (SE11-REQ-15, SE11-REQ-20, SE11-DEC-13, SE11-DEC-17)

Firmware AC-recovery settings act only when the device's AC input is actually removed and restored. If mains returns while the UPS output stays live (during S2, S3 or S4), nothing in firmware re-powers a halted device. One admissible combination of §8.3a must be commissioned. Timing constants (ASM-SE11-13, ASM-SE11-15; replaced by SE11-AC-15 measurements): T_boot = 120 s (AC applied or RTC wake → host UPS software able to read UPS state), T_decide = 30 s, T_hostonly_off = 90 s, W = 300 s (wake-poll period), D_on = 60 s (UPS output restart delay once mains is present and outputs are off), T_nasboot = 180 s (AC applied or WoL → NAS shares and UPS service reachable), W_nas = 300 s (Data-services wait cap for NAS reachability), T_ladder = 180 s (Core → Validation → Build at 60 s steps after Data services are up), T_fsck ≤ 600 s (bounded filesystem check of an unclean VM, run in parallel across VMs).

| Mechanism | How it works | Covers | Gate |
|---|---|---|---|
| **M1 — commanded output power-cycle (mandatory if evidenced)** | The device that owns the UPS link (host in S-1/S-3; NAS in S-2 and for UPS-N in S-3) commands: "turn outputs off after D_off; restart outputs when mains is present (and battery ≥ the UPS's restart threshold)". **D_off = (worst-case last-device-off time on that UPS − command time) + 60 s guard**, per candidate: S-1 120 s (drop at 330), S-2 180 s (drop at 420), S-3 UPS-A 120 s (330) / UPS-N 180 s (240). Every device thus sees a real AC loss; when mains is already back the UPS re-energises after D_on and firmware AC-recovery fires on host and NAS → S5 | Restoration at any time during S2/S3/S4, and the exhaustion case | G1: dated vendor evidence that the UPS class and the commanding software support commanded output shutdown with auto-restart (FC-09/FC-09b); SE11-AC-15 drills |
| **M3 — wake-poll loop (alternative where M1 is not evidenced; host with a direct UPS link only)** | At the host OS shutdown command in S2 (t = 210), and again at **every** subsequent host-only shutdown while the UPS reports on-battery or unknown, the host arms a firmware RTC alarm at now + W. On wake the host boots HOST-ONLY, reads UPS-A directly within T_boot + T_decide: *mains online* → S5 (charge rule) → S6, and at S6 entry the host sends N1 to the NAS if it is unreachable; *on-battery or unknown (E4)* → host-only shutdown (T_hostonly_off) and **re-arm**. The loop ends only when a wake finds mains online or the UPS exhausts; after exhaustion the AC-input-cycle path restarts host and NAS when mains returns. **No attempt cap.** Cost: each cycle draws host-only power for ≈ 240 s per 540 s, accelerating exhaustion (SE11-RISK-14); accepted because after S3 no workload runs and no unflushed data exists | Host restoration at any time; NAS via N1 while the UPS output is live, via AC cycle after exhaustion | G1: RTC wake from soft-off on the board class; N1 (WoL from soft-off) on the NAS class and forwarding by the switch class (FC-09); SE11-AC-15 drills |
| **N1 — NAS wake by the host** | Wake-on-LAN frame from the host agent to the NAS on `seg.mgmt` (or the point-to-point link), sent only at S6 entry (mains confirmed, R-WAKE (b)); repeated every 30 s until the NAS is reachable or W_nas elapses | NAS restart under S-1/M3 and S-3/N1 | G1 (FC-09); SE11-AC-15 drills (f), (h) |
| **M1-N — NAS-commanded output cycle of UPS-N (S-3 only)** | As M1, issued by the NAS UPS service for its own UPS | NAS restart under S-3 | G1 (FC-09b) |
| **M4 — attended restart (residual)** | No automatic restart; SE20 is alerted and an operator powers the devices on | Everything, with human latency | **Never a pass** for SE11-REQ-15; recorded as FD-RESTART exposure (SE11-RISK-12); REV-POWER if an SLO (§117) requires unattended restart |

**S6 ladder (service readiness).** At S6 entry (t_S6): (1) if the NAS is unreachable, send N1 (admissible combinations only; under M1 the NAS is already powering up on the same output cycle); (2) start the Data VM at t_S6 + 0; its filesystem check runs first if it was force-stopped (≤ T_fsck); its services start when the NAS is reachable **or** W_nas = 300 s has elapsed since t_S6 (then backups retry later); (3) start Core when Data services are up; Validation 60 s after Core; Build 60 s after Validation (T_ladder = 180 s); (4) the host agent re-publishes every protection level from the last evidence (§18.2 INIT) and `SIG-RESTART` with the measured times. **Service readiness** = every VM running, Data services started, protection levels re-published.

**End-to-end timing budget (SE11-REQ-20; mains restoration → S6 entry = T_restart; → service readiness = T_service; given charge ≥ 50 % at restoration, otherwise charge-limited and logged):**

| Scenario | M1 (S-1 / S-3) | M1 (S-2) | M3 (S-1 host, S-3 host) |
|---|---|---|---|
| (a) Restoration at S2 entry (t = 0; worst case for T_restart) | drop 330 + D_on 60 + T_boot 120 + T_decide 30 = **540 s** | drop 420 + 60 + 120 + 30 = **630 s** | alarm armed at 210 fires at 510 + 120 + 30 = **660 s** |
| (b) Restoration after outputs are off (M1) / immediately after an unsuccessful on-battery wake decision with output still energised (M3) | D_on 60 + 120 + 30 = 210 s | 210 s | host-only shutdown 90 + re-armed W 300 + 120 + 30 = **540 s** worst |
| (c) Restoration during an M3 host-only boot | n/a | n/a | ≤ T_boot + T_decide = 150 s |
| (d) Restoration after UPS exhaustion | UPS restart on mains (class threshold) + 120 + 30 | same | same (AC-cycle path) |
| **T_restart bound** | **≤ 720 s (12 min)** for every scenario of every admissible combination | | |
| NAS availability relative to t_S6 | NAS AC applied at the same output restart; up by D_on + T_nasboot = 240 s after mains ≈ t_S6 + 30 s → wait ≈ 30 s | same | N1 at t_S6 → NAS up by t_S6 + T_nasboot = +180 s ≤ W_nas |
| **T_service_clean** (all VMs stopped gracefully) = T_restart + max(NAS wait, Data VM boot) + T_ladder | 540 + 300 (cap) + 180 = **1,020 s** | 630 + 300 + 180 = **1,110 s** | 660 + 300 + 180 = **1,140 s** |
| **Bound T_service_clean** | **≤ 1,200 s (20 min)** | | |
| **T_service_forced** (any VM force-stopped; filesystem checks ≤ T_fsck in parallel, the Data VM's check gates the ladder) = T_service_clean + T_fsck | 1,620 s | 1,710 s | 1,740 s |
| **Bound T_service_forced** | **≤ 1,800 s (30 min)**, excluding database crash recovery, which SE12 bounds and SE11-AC-15 drill (i) measures and records | | |

Where the NAS wait is shorter than the cap (the usual case: ≈ 30 s under M1, ≈ 180 s under N1), T_service is correspondingly shorter; the bounds use the cap.

**Communication-loss handling (E4).** Loss of host↔UPS communication while in S0: alert; if it persists > 300 s the UPS protection is declared degraded (SE20 ticket, no workload change). If mains then fails while communication is still lost, the host has no event and the outcome is an **abrupt loss** (handled as FD-UPS-A, §9) — this residual is accepted and tested (SE11-AC-14). Loss of the NAS command path (switch or NAS unreachable) in S-1 S2: proceed; the NAS stops uncontrolled at UPS exhaustion — accepted residual with CoW crash-consistency and a mandatory scrub on restart (SE11-NFR-07). In S-2, loss of the NAS→host notification path is equivalent to E4 for the host. At an M3 wake, an unreadable UPS is treated as on-battery (shutdown and re-arm); this is safe only because M3 is admissible solely for a host with a direct UPS link (§8.3a).

**Shutdown budget rule (SE11-REQ-06, SE11-NFR-03).** For every UPS u of the selected candidate: B_u ≤ 0.7 × R_u, where R_u is the measured runtime at the measured load of that UPS's domain. Default budgets: S-1 B_A = 360 s; S-2 B_A = 450 s; S-3 B_A = 360 s and B_N = 210 s. The 30 % reserve is held *against measured runtime*, not against the low-battery signal; the low-battery signal and the runtime estimate are additional triggers only.

### 8.4 Fail-closed commissioning outcome

SE11-AC-06 **fails** if, for any UPS of the selected candidate, R_u < B_u / 0.7 at the measured load, or if any step exceeds its bound in the drill, or if no admissible combination of §8.3a meets T_restart ≤ 720 s and T_service_clean ≤ 1,200 s in SE11-AC-15 (M4 is a fail for any baseline whose SLO requires unattended recovery; an inadmissible combination is a fail by construction). Ordered remedies, each recorded as an SE11-DEC when applied: (1) remove non-essential loads from PD-A (gateway first; the switch stays while the S-1 command path or N1 needs it); (2) shorten VM stop timeouts only with SE11-AC-13 evidence that clean stops complete within the shorter bound; (3) change candidate (S-2 → S-3 shortens B_A from 450 s to 360 s, moves the NAS load off UPS-A and makes M3 admissible for the host); (4) substitute UPS-A by a higher-runtime unit of the same specification class (§11.4); (5) if none suffices, REV-POWER (§12.3). Until SE11-AC-06 passes, no stable-runtime stage baseline is accepted on this hardware (§154 evidence progression) and the platform stays in `PL-T2` at most (§6.3).

### 8.5 Placement constraints (rack / desk / room)

- Central host: tower chassis free-standing with unobstructed mesh-front intake and rear exhaust, off the floor, on PD-A; not inside the 18U rack (rack is for workers/switch/PDU per §230).
- NAS: adjacent to the host, on PD-A (S-1/S-2) or PD-N (S-3), within Cat6a reach of the switch; 3.5-inch drives are vibration-sensitive — solid surface, never stacked on the host.
- Switch: rack-mounted when the rack exists; until then shelf-mounted next to the NAS on a PD-A battery-backed outlet.
- Rack (deferred): 18U; 17U used with a gap after every device or 12U without gaps for micro trays (§230); 1U switch, 1U PDU, 1U power-brick shelf, trays sized to the selected worker form factor; PD-B feeds the PDU.
- Room: lockable (§13), ambient within device operating ranges, no shared circuit with high-draw appliances (requirement to the electrician under SE11-REQ-10); the T3-SUB media (KEYS bootstrap custody, bridging copies, repository bundle) are stored outside this room (§6.3); thermal and rack layout detail belongs to SE11-POWER-COOLING-RACK.

## 9. Failure-domain design (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-08)

Common-mode failure domains are named explicitly so that every consuming document references them by id (SE11-REQ-11). Redundancy "must cover actual shared failure points such as network, power, storage, control plane, DNS, external AI/provider dependencies, and internet connectivity — not merely worker count" (§173). Every domain has an accountable owner, a recovery dependency, a measurable acceptance target and a residual disposition; all dispositions are PROV (§0.2). Protection-state references are to §6.3.

| Domain id | What fails together | Blast radius in the reference configuration | Mitigation in this architecture | Accountable owner | Recovery dependency | Acceptance target | Residual disposition |
|---|---|---|---|---|---|---|---|
| FD-HOST | Board, CPU, memory, PSU | All four VMs, all local pools, WSL2, the host agent (signals STALE by construction); elastic workers lose their coordinator | Hardware-independent definitions (SE11-REQ-05); NVMe portable to a replacement host of the §11.4 class; T2/T3 copies; hosted fallback (§160, §168); queued disposable work idles rather than fails (§175) | SE11 (hardware), EL (architecture residual, SE11-DEP-02) | Replacement host class or hosted fallback; T2 (T3 if NVMe also lost) | SE11-NFR-06: degraded service ≤ 1 working day (ASM-SE11-07) | Accepted at Stage 1–2 pending EL; REV-HA when an SLO requires survival |
| FD-NVME-M2_1 | Host system device (OS, host agent store) | All VMs stop until host OS rebuilt; VM disks intact; event history lost (D-BND), sequence counter restarts per §18.2 | Host build in `REPO-EXT`; spare device class; counter-loss rule | SE11, SE20 | Spare NVMe; `REPO-EXT` | Host rebuilt and VMs restarted without T2 restore; consumers recover via `history_expired` + snapshot | Accepted; same class as FD-HOST but shorter |
| FD-NVME-M2_4 | Core + Data VM disks, platform data | **Full platform outage** (control plane and data) | Device isolation (only Highest-priority); hourly snapshots to T2 | SE11, SE12 | T2 (T2-only recovery) | SE11-NFR-05: restore ≤ 4 h per VM, loss ≤ 1 h | Accepted at Stage 1–2; reviewed at REV-HA |
| FD-NVME-M2_2 | Build VM disks, artifacts (Validation too under Mapping-D; scratch too when on M2_2) | Build/validation outage; runtime continues | Isolation from M2_4; T2 archives; rebuild from definitions | SE11, SE12 | T2 or rebuild | Restore ≤ 4 h; D-BND loss within SE12 window | Accepted |
| FD-NVME-M2_3 | Scratch (Mapping-D) or Validation (Mapping-V) | Slower builds, or validation outage under Mapping-V | Fallback mapping (§6.1a); T2 for Validation data | SE11 | none / T2 | Cache rebuilt / Validation restored ≤ 4 h | None material / accepted |
| FD-WORKER | One or more workers (local or hosted) | Capacity reduction only (§172) | Multiple eligible execution targets; no critical service on one uniquely named worker (§172) | EL (placement), SE01 | none | Queue drains on remaining capacity | None material |
| FD-STORAGE | NAS enclosure / array | Backups pause; T1 keeps running; the `REPO-EXT` mirror is lost (rebuildable); D-IRR classes whose T3 pipeline passes through the NAS begin ageing | RAID 6; snapshots; T3; T2 never a live datastore; protection states (§6.3) | SE11 (hardware), SE12 (data) | T3 for D-IRR; replacement enclosure of the §11.4 class | No D-IRR loss beyond `age(c)` (COPY) or the class's bounded existence (ANCHOR); degraded window ≤ A_max + G per class | Accepted in `PL-T3`; in `PL-T2` no real local D-IRR data exists; `PL-T3-PENDING`/`PL-DEG`/`PL-EXP` exposure bounded and logged |
| FD-SWITCH | Core switch / its uplink ports | L1, L2, L4, L5; host and NAS lose each other and the internet; VMs keep internal connectivity via the virtual switch; S-1 NAS command path, N1 wake frames and evidence intake from the NAS side lost unless point-to-point | Interim point-to-point L1; spare NAS ports; cold-spare switch of equivalent class is an SE20 stocking decision; S-3 removes the command-path dependency | SE11 | Replacement switch class | Backups resume within the SE12 window after replacement; no runtime data loss | Accepted: single switch at Stage 1–2 |
| FD-CIRCUIT-A | Mains/circuit A interruption **with healthy UPS-A** | Host, switch (and NAS in S-1/S-2) run on battery → controlled shutdown (§8.3) | State machine S1–S6; per-candidate budgets SE11-REQ-06; admissible restart combination SE11-REQ-15/20; AVR | SE11, SE20 (drills); electrician for cause (SE11-REQ-10) | none beyond UPS | SE11-NFR-03 met in SE11-AC-06/15; automatic restart within T_restart ≤ 720 s and service within T_service bounds | Accepted: outage = planned-quality downtime, no data loss beyond in-flight work |
| FD-UPS-A | **Abrupt UPS-A output loss** (UPS fault, overload trip, battery failure) or mains loss while UPS communication is lost | Host and switch (and NAS in S-1/S-2) lose power **simultaneously and without warning** | Crash-consistency requirements: journaled guest filesystems, synchronous-commit WAL (SE12), NAS copy-on-write + scrub on restart; restart S5–S6; integrity checks before services start | SE11 (hardware), SE12 (data integrity) | Spare UPS of the §11.4 class; integrity tooling | SE11-NFR-07 met in SE11-AC-13 | Accepted: client-class NVMe without asserted power-loss protection (§6.5); loss bounded to last commit; REV-POWER if drills show unrecoverable corruption |
| FD-UPS-N (S-3 only) | Abrupt UPS-N output loss | NAS only | NAS CoW + scrub | SE11 | Spare UPS class | NAS array integrity after drill | Accepted |
| FD-SIGNAL | UPS signalling path only (USB cable, UPS software, NAS command/notification path) | No immediate workload impact; a later mains loss degrades to FD-UPS-A | E4 handling (§8.3b); S-3 topology as fallback; telemetry alert | SE11, SE20 | none | Detected ≤ 300 s; drill SE11-AC-14 passes | Accepted with alerting |
| FD-RESTART | Restart mechanism fails after a shutdown (M1 not executed, RTC alarm not firing, N1 not received) | Devices stay halted although mains is back | Admissibility matrix (§8.3a); M1 preferred; M3 wake-poll loop re-arms until mains or exhaustion; exhaustion-and-return as the ultimate path; M4 residual | SE11, SE20 | Operator presence (M4) | SE11-AC-15: bounds met for the selected combination in drills (a)–(j) | Accepted only with an admissible combination; otherwise recorded exposure (SE11-RISK-12) |
| FD-UPS-B / FD-CIRCUIT-B | UPS-B or circuit B (deferred) | Local workers only | Isolation from PD-A (§165) | SE11 | none | Capacity reduction only | n/a until rack exists |
| FD-ROOM | Rack/room/site (fire, flood, theft) | Total local loss | T3 off-site copy per class; KEYS and the repository bundle on T3-SUB outside the room; `REPO-EXT` external; portability to hosted infrastructure (§160, §168) | SE11 (physical), SE12 (T3), EL (hosted fallback) | T3; T3-SUB; `REPO-EXT`; hosted capacity | D-IRR restored from T3 with loss ≤ `age(c)` (COPY); service rebuilt on hosted/replacement infrastructure | Accepted in `PL-T3`; exposure in other PL states bounded by §6.3 |
| FD-EXT-AI | External AI providers | `pool.agents` work needing external models; no offline AI until B11 adopted | Provider router/fallback and AI-dependency governance (§66, §115, §185); queued jobs resume (§175) | EL (AI/agent architecture, SE11-DEP-02) | Alternative provider per router policy | Queued work resumes without loss | Pending EL; NT16 vendor risk absent (SE11-DEP-09) |
| FD-EXT-REPO | External repository service hosting `REPO-EXT` | Authoritative source, IaC, inventory and commissioning evidence unreachable or lost at the provider | T2 mirror refreshed ≤ 1 h; repository bundle on T3-SUB at every stage gate; promotion of the mirror to `LREPO` (§6.3) | SE11 (mirror/bundle), NT16 (provider assessment, SE11-DEP-09) | T2 mirror; T3-SUB bundle | Promotion completes with loss ≤ 1 h of commits; new remote or bundle within A_max | Accepted: single external provider at Stage 1–2 (SE11-RISK-15) |
| FD-INTERNET | Uplink / gateway | External providers, hosted runners, hosted T3 transfers, `REPO-EXT` pushes, mirrors | Local repositories/mirrors on T2 (§164); local build capacity in `pool.build`; **T3 tolerance = remaining copy-age budget per class (A_max − `age(c)` at outage start), then G of degraded operation, then T3-SUB or write-freeze (§6.3)**; commissioning evidence queues locally and is pushed when the uplink returns (D-BND until pushed) | SE11 (physical uplink), SE20 (operations), SE12 (policy) | Single uplink restored | Local runtime continues; protection-state transitions observed exactly as §6.3 prescribes (SE11-AC-07c) | Accepted: single uplink at Stage 1–2; exposure bounded and logged |
| FD-MGMT | Management plane (host admin path, NAS admin, switch mgmt, UPS software, host agent endpoint) | Operator cannot intervene remotely; workloads unaffected; M4 restarts need presence; signal consumers see STALE per §18.2 and deny admission | Physical console (§10.2); `seg.mgmt` isolation; configuration in `REPO-EXT` | SE11, SE20 | Physical presence | Console recovery procedure drilled once per stage | Accepted: no BMC on the consumer-class board (SE11-RISK-04); REV-HA if SLOs require remote recovery |

Dependency-failure behaviour summary: a local infrastructure problem must not corrupt active builds or accepted runtime state; resumable jobs, durable state and idempotent execution are required of every workload placed on these pools (§175) — EL/SE19 implement and prove this; SE11 guarantees only the physical boundaries above and publishes the signals of SE11-DEC-11 under the contract of §18.2.


## 10. Hardware manageability / operability (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-09)

### 10.1 Inventory identity (SE11-REQ-07)

Every physical asset carries an inventory id `CSPUI-HW-<class>-<nn>` (classes: HOST, NAS, HDD, NVME, NIC, GPU, UPS, SW, RACK, PDU, WKR, CABLE, T3SUB) recorded in a version-controlled inventory file owned by SE11, committed to `REPO-EXT` (§6.2) and published through `SE11-CONTRACT-hardware-baseline@1` (§18.2). Record fields: inventory id; BOM reference (B1–B19); specification class (§11.4); part number as cited from SEED-01 and its evidence status (DEFERRED-PENDING-EVIDENCE / confirmed / superseded) with the G1 evidence row id; serial number (G2); firmware/BIOS/driver version at receipt (G2) and at commissioning (G3); physical position (slot id such as `M2_3`/`PCI_E1`, NAS bay, rack U); power domain (PD-A/PD-N/PD-B); failure-domain ids (§9); disposition and quantity status (§1.2); §6.1a row and mapping (D/V) in force with V_min/B_max; signalling candidate and the admissible restart combination (§8.3a); pre-build evidence record id (§11.3); commissioning evidence ids (§14); warranty end; sanitisation state. Cables are labelled at both ends with the endpoint ids. The **configuration fingerprint** (§11.3) is derived from these records.

### 10.2 Remote-management capabilities where available

| Device | Out-of-band | In-band management path | Fallback |
|---|---|---|---|
| Central host | None (consumer board; no BMC/IPMI) — SE11-RISK-04 | Windows remote administration and Hyper-V management on `seg.mgmt`; MFA per §59 | Physical console in the lockable room; UEFI Flash BIOS and Clear CMOS on the rear panel (B3); RTC wake (M3) if evidenced |
| NAS | None | NAS OS web/remote administration on `seg.mgmt` | Front panel / USB; Wake-on-LAN (N1) if evidenced |
| Switch | Management port if the class provides one | Management VLAN | Console port |
| UPS-A / UPS-N | USB-HID to the host (S-1/S-3) or NAS (S-2/S-3) | Status via the UPS software's telemetry export, re-published by SE11's host agent | Front LCD |

### 10.3 Telemetry and health status (SE11-REQ-08, SE11-NFR-04; published under `SE11-CONTRACT-hardware-signals@1`, consumed by SE20 monitoring, SE01 capacity, SE19 validation, EL scheduler, data-store gates)

Mandatory signals from first power-on ("capture performance/resource telemetry from the first workloads", §160; "capture CPU, memory, I/O, network, queue time, job duration, reliability, and cost", §234): host CPU utilisation per VM and total, CPU-wait per VM, memory committed per VM and host against Table 5.3-R, NVMe SMART (temperature, media errors, percentage used, TBW consumed) per device, per-virtual-disk IOPS and bytes (the summed Build figures against B_max, Validation against V_min) and latency (and `io.max` throttling counters when the guest limiter is in use), PCIe negotiated width/speed per slot (detects degraded M2_3/PCI_E3 sharing), NIC link speed and errors, NAS array state (healthy/degraded/rebuilding), per-drive SMART, NAS volume utilisation, snapshot success, backup, mirror and T3 job success/duration/throughput, **per-class `mech_ok(c)`, `t3_last_ok(c)`, `kind(c)`, `age(c)`, state, `admit(c)`, `mutate(c)`, platform `PL-*` state**, UPS state per UPS (online/on-battery/low-battery, load %, runtime estimate, battery charge %, battery age, communication state), restart-mechanism armed/fired/wake-poll/N1 events with measured T_restart and T_service, host and NAS temperatures, switch port utilisation on L1/L2, and the event signals of SE11-DEC-11. **How they are delivered is SE11's contract, not SE20's design:** a metrics endpoint on `seg.mgmt` (pull, text exposition, sample interval ≤ 60 s, no workload content) and an append-only event log with a **globally persistent sequence**, a **60 s heartbeat snapshot** and a **current-level snapshot endpoint** — all specified in §18.2 Part B so that SE20's monitoring integration is a subscription to a defined interface and no consumer can see a false STALE state in healthy operation. Thresholds that trigger expansion or revision are in §12.

### 10.4 Firmware / BIOS / driver lifecycle (SE11-REQ-09)

- Components with a firmware lifecycle: host UEFI/BIOS (incl. CPU microcode/AGESA), NVMe firmware ×4, NIC driver/firmware, optional GPU driver, NAS OS and HDD firmware, UPS firmware and host/NAS UPS software, switch firmware.
- Update path: vendor-signed images only, checksum verified against the vendor publication, staged in a declared maintenance window (§10.5) after a successful snapshot of all VMs and a verified T2 backup; one component class per window; rollback plan recorded; post-update SE11-AC-04 smoke subset executed; firmware settings baseline re-verified (SE11-AC-08a), including "restore on AC power loss", RTC wake and the UPS-command settings of §8.3b; the G1 evidence row for the changed component re-opened (§11.3); configuration fingerprint updated.
- Ownership: SE20 schedules and executes; SE17 defines integrity controls (SE11-SECREQ-02); SE11 keeps the compatibility matrix (§11) current.

### 10.5 Maintenance windows

Hardware maintenance is performed only in a window declared to SE20's operations calendar that does not overlap a stage-gate VP validation (§174 "VP validation / release assurance"). Minimum window content: pre-checks (backup verified, snapshots taken, UPS healthy, all local D-IRR classes with real data PROTECTED with kind COPY or the exposure explicitly accepted by SE12), the change, post-checks (SE11-AC-04 smoke, telemetry nominal, protection levels re-published), inventory record and fingerprint updated.

## 11. Compatibility / availability assessment (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-10)

### 11.1 Structural compatibility check (from the BOM specifications themselves, re-read in this run)

| Check | Items | Result from BOM data | Residual verification |
|---|---|---|---|
| Socket / chipset | B1 AM5 ↔ B3 AM5/X870 | Structurally compatible (§227.1 "Socket AM5"; §227.3 "AMD X870 chipset, socket AM5") | BIOS version supporting the CPU: **not established** (FC-01) |
| Memory | B4 DDR5 UDIMM ↔ B3 "4× DDR5 DIMM, up to 256 GB" | Compatible at capacity; DDR5-6000 EXPO on four DIMMs is a stability-validated profile, not a guaranteed one (the seed prescribes the 5600/5200 fallback, §227.4) | Exact population (2-DIMM M-A vs 4-DIMM M-B/M-A+) on the board's qualified list: **not established** (FC-02); stability pass SE11-AC-04 |
| Cooler | B2 157 mm ↔ B8 ~166 mm clearance; AM5 mounting included (§227.2, §227.8) | Compatible | — |
| Form factor | B3 ATX ↔ B8 ATX/E-ATX | Compatible | — |
| PCIe lane sharing | B10 in PCI_E3 (Gen4 x4, "shares with M2_3") ↔ B5 in M2_3 (Gen4 x2) (§227.3, §227.10) | Simultaneous operation **not established** from BOM text (FC-03) | SE11-AC-02 read-back; Fallbacks A/B/C, Mapping-V (§6.1a) |
| NIC in PCI_E1 (Fallback A) | B10 PCIe 3.0 x4 card in a Gen5 x16 CPU slot | Electrically and mechanically a subset; **operation not established** (FC-03) | SE11-AC-02 when Fallback A is used |
| M2_2 ↔ USB4 sharing | B6 on M2_2 ("sharing with USB4", §227.3) | USB4 unused at baseline; no conflict | Confirm USB4 use does not down-shift M2_2: SE11-AC-02 |
| PSU | B7 750 W, 12V-2x6 ↔ B1 230 W + B11 145 W + platform (§227.7, §227.11) | Within rating for the no-GPU build; GPU build conditional on measurement (the seed's own condition) | SE11-AC-06 |
| GPU mechanical | B11 single-slot 241 mm ↔ B8 mid-tower, PCI_E1 x16 | Expected to fit; not asserted | SE11-AC-02 before adoption |
| NAS memory | B13 DDR5-4800 ECC SO-DIMM ↔ B12 "2 slots; 64 GB max"; mixed 16 + 32 GB (§228.1–§228.2) | Capacity compatible; mixed pair support **not established** | G1 (deferred item) |
| NAS drives | B14 3.5-inch SATA CMR ↔ B12 8 SATA bays (§228.1, §228.3) | Compatible | Online RAID 6 expansion support: **not established** (FC-08) |
| Network | B10 10GBase-T ↔ B12 2×10 GbE; Cat6a supplied with NAS (§228.1) | Compatible | Switch class 10GBase-T or SFP+ with matching transceivers: SE11-AC-05 |
| UPS | B15 1000 W ↔ PD-A loads (§8.2); NEMA 5-15P ↔ 15 A circuit (§231) | Compatible; runtime unknown until measured | SE11-AC-06 |
| UPS signalling and restart | B15 USB-HID / host software ↔ B12 network UPS server; commanded output power-cycle by host (M1) and by NAS (M1/M1-N, FC-09b); NAS client wait ≥ 240 s (S-2); RTC wake from soft-off (M3); NAS WOL from soft-off and switch forwarding (N1) | **Not established** (FC-09, FC-09b) | G1, SE11-DEC-10/19, SE11-DEC-13/17 |
| OS / virtualization | B9 Windows 11 Pro ↔ Hyper-V; TPM 2.0 + Secure Boot prerequisites; Linux guest support; NIC driver for the virtual switch; per-virtual-disk IOPS controls; guest cgroup v2 `io.max` | Hyper-V is a Pro feature; TPM/Secure Boot are install prerequisites so the platform must provide them; NIC driver (FC-05) and storage-QoS availability (FC-06) **not established**; cgroup v2 `io.max` is a Linux guest facility whose availability on the chosen distribution is confirmed in SE11-AC-03 | G1, SE11-AC-03 |

### 11.2 Current manufacturer support and practical availability — evidence status OPEN/UNMET; what was checked and what is gated (SE11-DEC-21)

**What the corpus contains.** Exactly one attributable, dated, coherent configuration: the Appendix G v2.2 set of SEED-01 Proposed Revision 1.1 (the "Expanded 2026 Baseline", sha `2d3a171d…`), presented by its author as a coherent build — slot assignments per item (§227.3, §227.5, §227.6, §227.10), the cooler/case clearance pair (§227.2/§227.8), the explicit PSU condition for the GPU (§227.11), the NAS memory/drive pairing (§228), the UPS/NAS integration surfaces (§228.1, §229.1), the rack and electrical envelope (§230, §231). The seed also states the rule that applies to it: time-sensitive practices "must be revalidated from reputable/authoritative sources at the point they become applicable" (§0 current-source rule; §12 current-practice revalidation). That set is recorded as **selection record SEL-0** (§11.3).

**What is not in the corpus and is not asserted (BND-04).** Current manufacturer support status; a BIOS version supporting the CPU; the exact memory population on the board's qualified list; simultaneous PCI_E3/M2_3 operation; NIC driver support for the hypervisor virtual switch; hypervisor storage-QoS availability on the host OS edition; UPS software ↔ host OS, NAS ↔ UPS protocol, commanded output power-cycle by host or NAS, RTC wake, NAS WOL and switch forwarding; NAS online array expansion; present market availability of any part number. SE11 has no access to manufacturer publications in this run and invents none.

**Consequence for the criterion.** Deferring every part number (B1–B17: DEFERRED-PENDING-EVIDENCE) and baselining specification classes (§11.4) prevents this document from fixing an unverified part-number combination; recording SEL-0 fixes *which* coherent set is the candidate without asserting that it is buildable today. **QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 — evidence status: OPEN/UNMET** until the G1 record below holds at least one coherent currently-supported configuration (SEL-0 confirmed item by item, or in-class substitutes with their own rows). What *is* secured now: no combination other than SEL-0 is baselined, and SEL-0 cannot be ordered or built before G1 — so no impossible or obsolete combination can be baselined through this document (§0.3 explains the event encoding).

**Ordered gates with achievable prerequisites (SE11-DEC-21; corrects the v4 circularity):**

| Gate | When | Prerequisites | Content | Output | Never depends on |
|---|---|---|---|---|---|
| **G1 — documentary feasibility and selection (= SE11-AC-01)** | Before any purchase or build | Documents only: SEL-0, manufacturer/vendor publications for each item and claim, this document | One dated, attributable evidence row per item and claim (FC-01 … FC-09b and the per-item claims of §11.3); for each: confirmed / not confirmed / superseded; substitutes within class recorded as new SE11-DEC entries; candidate × mechanism combination chosen from §8.3a on the evidence | **Configuration fingerprint v0** = baseline selection SEL-1 (the confirmed set) | Any built hardware, receipt or commissioning result |
| **G2 — receipt verification (= SE11-AC-01b)** | After delivery, before first power-on | G1 record; the delivered items | Serial numbers; tamper/packaging inspection; firmware version read and compared with the G1 row (SE11-SECREQ-07); mismatch → the item's G1 row re-opened, not built | Fingerprint v0.1 (serials, received firmware) | Commissioning results |
| **G3 — commissioning (= SE11-AC-02 … SE11-AC-15)** | After build | G2 passed | Measurements and drills of §14 on the built configuration | Fingerprint v1 (SE11-AC-10) | — (G3 results may *re-open* a G1 row, e.g. a failed lane coexistence, but never *close* one) |

**Open class-level feasibility conditions (each closed only by a G1 evidence row; failure consequence stated):**

| Id | Condition that must hold for the architecture to be buildable | Evidence that closes it (dated, attributable, recorded in §11.3) | If it fails |
|---|---|---|---|
| FC-01 | A board of the B3 class ships or can be updated to a BIOS that supports the B1-class CPU with the required virtualization/IOMMU, Secure Boot, TPM 2.0, AC-recovery and RTC-wake settings | Board manufacturer BIOS release notes / CPU support list for the exact board and CPU; firmware settings reference | Substitute board or CPU within class (new SE11-DEC) |
| FC-02 | The chosen memory population (2-DIMM M-A; 4-DIMM M-B/M-A+) is on the board's qualified list or validated at ≥ DDR5-5200 | Board qualified-vendor list entry for the kit and population; else SE11-AC-04 stability pass at the fallback speed (a G3 result that re-opens, never closes, the row if it fails) | Smaller population or different kit within class; M-A+ path re-validated |
| FC-03 | PCI_E3 (x4 NIC) and M2_3 (x2 NVMe) operate concurrently, **or** a Gen3 x4 NIC operates in the Gen5 x16 CPU slot (Fallback A), **or** Fallback C's x1 path still meets SE11-REQ-04 | Board manual lane-sharing statement; SE11-AC-02 read-back confirms | Fallback B (scratch on M2_2) with its storage consequences; Mapping-V unavailable under B |
| FC-04 | The host OS edition supports the Hyper-V role with the per-VM reserve/limit/weight and static/dynamic memory controls used in §4–§5 | Host OS feature documentation for the exact edition/version | Edition change within the B9 class (new SE11-DEC) |
| FC-05 | The NIC class has a driver supporting the hypervisor virtual switch at 10 Gb/s on the host OS version | NIC vendor driver support statement | Different 10 GbE NIC within class (SFP+ allowed with matching switch) |
| FC-06 | Per-virtual-disk storage QoS is available on the host OS edition — else the guest `io.max` limiter is available on the chosen Linux distribution | Host OS / distribution documentation | The §6.1a "QoS unavailable" rows apply; if neither limiter exists, Validation may not share a device with Build → Mapping-V mandatory or R2 |
| FC-07 | (Only when TRG-GPU fires) a supported path exposes the B11-class GPU to a Linux VM on the client hypervisor | Hypervisor and GPU vendor documentation | Host-level model service fallback (§5.5) |
| FC-08 | The NAS OS supports online RAID 6 expansion from the N-A count, UPS integration per the selected candidate, power-on after AC recovery and (for N1) Wake-on-LAN from soft-off | NAS OS feature documentation for the exact version | N-B installed from the start (recorded deviation from N-A); S-3; N1 unavailable → M1 mandatory or the combination inadmissible |
| FC-09 | The UPS class, with the host software at the exact version, supports the selected candidate's signalling, commanded output shutdown with auto-restart by the host (M1), and the board supports RTC wake from soft-off (M3); the switch class forwards WoL frames (N1) | UPS vendor software documentation; board manual; switch documentation | Candidate change (S-3); mechanism change; if no admissible combination can be evidenced, SE11-REQ-15 is unmet and the stable-runtime baseline is blocked (§8.4) |
| FC-09b | The NAS UPS service can command the UPS output cycle with auto-restart (required for S-2/M1 and S-3/M1-N) | NAS OS UPS-service documentation; UPS documentation for the NAS-side command path | S-2 inadmissible (→ S-3); under S-3 the NAS restarts by N1 instead |

### 11.3 Selection record SEL-0, G1 evidence register and configuration fingerprint

**Selection record SEL-0 (v5; the baseline selection as of this version).**

| Field | Value |
|---|---|
| Selected set | The Appendix G v2.2 reference configuration of SEED-01 as a coherent whole: B1–B17 part numbers as cited in §1.2 (B11, B13, B16 as deferred/optional members; B18 electrical envelope; B19 unspecified) |
| Attribution and date | SEED-01 "Master Product Vision & Operating Architecture — Proposed Revision 1.1", "Expanded 2026 Baseline", Appendix G "Optional Baseline (v2.2)", repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| Coherence statements relied on | Slot assignments §227.3/§227.5/§227.6/§227.10; clearance §227.2 ↔ §227.8; PSU/GPU condition §227.11; NAS memory/drives §228; UPS/NAS integration surfaces §228.1/§229.1; circuits §231; structural check §11.1 |
| Availability assessment | **As asserted by the seed at its revision date; not re-verified in this corpus.** The seed itself requires revalidation at the point of applicability (§0, §12). Present availability of any member is unknown to SE11 (ASM-SE11-16). |
| Quantities | Not selected from SEL-0: B4 and B14 quantities are candidates per §5.3/§6.7 (M-A, N-A defaults) |
| Status | Candidate selection, not a buildable bill; every member DEFERRED-PENDING-EVIDENCE; G1 evidence rows: **none recorded** |

**G1 evidence register (one row per item and claim; every row NOT PERFORMED at v5; populated by SE11-AC-01):** item (B-id); part number as cited; claim checked (the FC-nn condition and/or the per-item claims: current support status, BIOS/firmware version, qualified population, slot coexistence, driver/OS/hypervisor support, storage-QoS and guest `io.max` availability, UPS protocol, M1 by host, M1/M1-N by NAS, S-2 client wait, RTC wake, N1 with switch forwarding, NAS online expansion, present availability); source (publisher, document title/version, publication date, date accessed); result (confirmed / not confirmed / superseded); consequence (confirmed into fingerprint v0 / substitute within class with a new SE11-DEC / defer); recorder; date. "Not confirmed" on any item keeps that part number deferred; a superseded item is substituted by specification class and recorded (SE11-REQ-12).

**Configuration fingerprint.** v0 = SEL-1 (the G1-confirmed set, with memory candidate M-x, NAS candidate N-x, signalling S-x, restart combination per §8.3a and the closing evidence row ids) — produced before any purchase, from documents only. v0.1 adds G2 serials and received firmware. v1 (SE11-AC-10) adds commissioning versions, slot positions, the §6.1a row/mapping in force, protection defaults A_max/G, the registered producers per class and the evidence ids of §14. Any change to the fingerprint re-opens the affected G1 row and SE11-AC-10. **At v5: SEL-0 recorded; fingerprint v0 does not exist; no evidence row exists.**

### 11.4 Specification classes — what is baselined (not procurement preference; preserve performance, reliability, security, portability and schedule assumptions)

| BOM item | Specification class (baselined) |
|---|---|
| B1 CPU | AM5 desktop CPU, ≥ 16 physical cores, ≥ 64 MB L3, ≤ 230 W package, hardware virtualization + IOMMU |
| B2 cooler | Dual-tower air cooler ≤ 160 mm height with AM5 mounting, rated ≥ 230 W |
| B3 motherboard | ATX AM5, 4×DDR5 to ≥ 256 GB, ≥ 1× PCIe x16 (CPU) + ≥ 1× PCIe x4 slot usable concurrently with ≥ 4× M.2 (≥ 2 of them x4), ≥ 2.5 GbE onboard, UEFI Secure Boot, TPM 2.0, "restore on AC power loss" setting, RTC wake from soft-off |
| B4 memory | Matched DDR5 UDIMM kit per candidate (Table 5.3-R), ≥ DDR5-5200 validated at the chosen population; ECC-capable platform class is the recorded substitute if SE11-RISK-02 materialises |
| B5/B6 NVMe | M.2 2280 PCIe 4.0 x4 (or 5.0), TLC with DRAM, ≥ 600 TBW per TB, 5-year warranty class; devices with power-loss protection are the recorded upgrade class if SE11-AC-13 shows unrecoverable corruption |
| B7 PSU | ATX 3.1 / PCIe 5.1, ≥ 750 W, Cybenetics Gold or better, native 12V-2x6, fully modular, ≥ 7-year warranty class |
| B8 case | Mid-tower ATX with mesh front, ≥ 160 mm cooler clearance, ≥ 250 mm GPU clearance |
| B9 OS | Windows 11 Pro-class edition with Hyper-V, per-VM processor/memory resource controls, TPM 2.0/Secure Boot support |
| B10 NIC | 10GBase-T (or SFP+ with matching switch), PCIe 3.0 x4 or 4.0 x2 minimum, driver supporting the Windows Hyper-V virtual switch; operable in a x16 CPU slot (Fallback A) |
| B11 GPU | Single-slot, ≤ 145 W, ≥ 24 GB ECC VRAM, PCIe x16, 12V-2x6 or 8-pin; larger classes ESCALATE |
| B12 NAS | 8-bay SATA NAS with ECC memory, ≥ 2×10 GbE, Btrfs/ZFS-class snapshots, per-folder/volume AES-256, UPS integration (any of S-1/S-2/S-3), power-on after AC recovery, Wake-on-LAN from soft-off preferred, M.2 cache slots; hosted object storage is the equivalent for T2/T3 under G-LOCAL |
| B14 HDD | 3.5-inch enterprise CMR, 7,200 RPM, ≥ 2.5 M h MTBF, ≥ 550 TB/yr workload, 5-year warranty, ≥ 20 TB (smaller same-class drives permitted under N-A if V is small) |
| B15/B16 UPS | Pure-sine line-interactive with AVR, USB-HID, ≥ 1500 VA / 1000 W (PD-A) and ≥ 1000 VA / 600 W (PD-N / PD-B), user-replaceable batteries, commanded output shutdown with auto-restart on mains (M1) and configurable restart delay preferred; higher-runtime units of the same class are the remedy under §8.4 |
| B17 switch | Managed L2+, ≥ 2×10 GbE (≥ 4 preferred), 24× ≥ 1 GbE access, VLAN, Wake-on-LAN frame forwarding within `seg.mgmt`, port mirroring for SE17/SE19 |
| T3-SUB media | Two removable encrypted media (or a second independent location) sized to the local D-IRR set plus the repository bundle (§6.3) |

## 12. Expansion model (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-12)

### 12.1 Planned spare capacity at baseline

| Resource | Spare at baseline | Scale path |
|---|---|---|
| Host PCIe | PCI_E1 x16 (reserved for GPU; occupied by the NIC under Fallback A), PCI_E2 x1, 2×USB4 | Scale-up only |
| Host memory | M-A/M-C: two free slots (second matched pair → M-A+, re-validation); M-B/M-A+: none (board maximum) | **Hard ceiling at 256 GB** — REV-MEM |
| Host NVMe slots | None (4/4 populated) | Device-capacity scale-up; SATA ×4 for cold tiers only |
| NAS bays / M.2 | N-A: 4 bays; N-B: 2 bays; 4× M.2 | Same-class drives; cache/metadata |
| NAS network | 1×10 GbE + 2×5 GbE | Second 10 GbE consumer or link redundancy |
| Switch ports | all minus 2–3 at baseline | Workers, gateway, management devices |
| Rack | 18U, 12–17U usable (§230) | Worker trays, second switch, PD-B |
| Power | PD-A margin per §8.2 and the §8.4 runtime reserve; PD-B unused | Workers only on PD-B |
| Worker pool | Elastic: hosted/cloud executors unbounded by local hardware (§168) | Scale-out by default |
| Host agent event log | 1 GB allocation on M2_1 (≥ 7 days / ≥ 100,000 events, §18.2) | Allocation raised in the host build; retention never shortened below the contract minimum |

### 12.2 Evidence-driven triggers that add hardware without architecture revision (§159, §171)

| Trigger id | Signal (from §10.3 telemetry) | Action |
|---|---|---|
| TRG-WKR-LOCAL | Build/test queue wait p95 above the SE01-defined threshold for two consecutive stages **and** hosted-runner cost or data privacy makes local execution preferable (§168, §171) **and** the limiting factor is worker capacity, not central resources, storage, network, provider quotas or software (§171) | Adopt local worker class (B19), rack, PDU, UPS-B (B16/B17) |
| TRG-GPU | Measured external-model latency/cost/privacy case or GPU-required application testing (§176) with §5.5 preconditions met (including release of PCI_E1 from Fallback A) | Adopt B11 |
| TRG-MEM-EXPAND (M-A/M-C only) | Measured committed memory p95 > 80 % of installed for one stage **and** the §5.3 procedure records Steps 1 and 2 as failed | Add the second matched pair (M-A+; re-run SE11-AC-04 memory pass); record SE11-DEC |
| TRG-NAS-MEM | NAS memory sustained > 70 % or snapshot/backup jobs missing their window from memory pressure | Install B13 |
| TRG-NAS-CAP | T2 utilisation > 70 % | Add same-class drives to free bays (N-A → N-B) |
| TRG-NET-10G | L1 utilisation > 70 % sustained during backup windows, or a second 10 GbE consumer | Use NAS second 10 GbE / add 10 GbE ports within the switch class |
| TRG-NVME-TBW | Any NVMe > 80 % of rated TBW or media errors (M2_2 watched closely when scratch is on it) | Replace with same class (§11.4) |
| TRG-UPS-BATT | Any UPS runtime estimate at measured load < B_u / 0.7 | Battery replacement (same class) or §8.4 remedies |
| TRG-LREPO | A product or governance decision requires a local repository server (e.g. §66 confidential source) | Adopt `LREPO` class as a D-IRR class through §6.3 (fixture, ARMED, admission) |

### 12.3 Scale-out versus scale-up boundaries and architecture-revision triggers

The central node complements, never replaces, horizontally scalable workers (§177). Scale-out (more workers, hosted executors) is the default answer to throughput; scale-up applies only to the capabilities the seed assigns to the central node — large contiguous RAM, low-latency CPU, NVMe, centralized data/control services (§161). The following require a revision of this architecture (new SE11 version plus EL review), not a hardware addition:

| Revision trigger | Why adding hardware is insufficient |
|---|---|
| REV-MEM: §5.3 Step 4 (1.25 F > 256 GB with hosted placement inadmissible), or Highest-priority pool floors exceed 85 % of 256 GB on measured p95 | Board ceiling reached; second host, larger-memory platform class, or data-tier redesign is an architectural choice |
| REV-HA: an SLO (§117) requires the control plane or Data VM to survive FD-HOST or FD-NVME-M2_4, or requires unattended restart that no admissible combination provides | Needs a second failure domain and quorum design (§173) |
| REV-GPU-CLASS: accelerator > 145 W, dual-slot, or second accelerator | Exceeds PSU, slot and thermal envelope (§5.5) |
| REV-STORAGE-HOT: T1 > 85 % after device scale-up; a random-IO workload that cannot stay on host NVMe; §6.1a remedy R2 (Validation's demand cannot fit beside Build and Mapping-V is unavailable or insufficient) | NAS is not a hot tier (§164); host NVMe topology exhausted |
| REV-STORAGE: retention volume V > 44 TiB (§6.7) | Beyond the enclosure's economical RAID 6 envelope; hosted tier or second enclosure is architectural |
| REV-NET: storage/core path saturated after all 10 GbE ports used, or 25 GbE class needed | Switch and NIC class change ripples through host slots |
| REV-SITE: geographic/resilience footprint beyond one room (§226 F.20) | Hosted/hybrid footprint decision |
| REV-POWER: §8.4 remedies exhausted, PD-A measured peak within 20 % of UPS-A rating, circuit limits reached, or no admissible restart combination meets the SLO | UPS/circuit redesign by qualified professionals; possible relocation |

## 13. Security considerations (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-11)

The owners of the control catalogue (SE17 for infrastructure/workload/data security, SE15 for identity and cryptography, §74) have not published control ids in this run (their documents are absent, §0.1). This section therefore does two separable things: **(a)** it states the hardware security requirements under SE11's identifiers and, for each, the check that **SE11 itself executes and can pass without any owner catalogue** (SE11-REQ-19, SE11-AC-08a) — implementable from this document alone; **(b)** it names what remains the owner's (policy, control ids, long-term custody, identity) as placed items, unmet dependency SE11-DEP-05, verified later as SE11-AC-08b. No foreign control id is invented; nothing re-derives a control design. The binding of each SE11-SECREQ to an owner control id is the owner's act (§18.3 row CI-4); until then SE11-SECREQ-nn are the ids of record for the hardware baseline.

| Id | Requirement placed on the hardware baseline | (a) SE11-executable check (SE11-AC-08a) — pass criterion | (b) Owner part (SE11-AC-08b, placed; SE11-DEP-05) |
|---|---|---|---|
| SE11-SECREQ-01 Trusted boot | UEFI Secure Boot enabled; TPM 2.0 present and enabled; boot order locked to M2_1; UEFI administrator password set; the RTC-wake and AC-recovery settings of §8.3b are part of the protected firmware baseline | Firmware settings export shows Secure Boot = on, TPM 2.0 = enabled and owned, boot order = M2_1 only, admin password = set, AC-recovery = power on, RTC wake = enabled; host OS reports Secure Boot state on; export checksum recorded in the fingerprint | SE17: measured-boot attestation decision and control id |
| SE11-SECREQ-02 Firmware integrity | Vendor-signed images only, checksum verified, staged in maintenance windows with snapshot + verified backup first (§10.4); firmware settings baseline re-verified after every BIOS update | Each firmware record in the inventory carries the vendor checksum and the verification result; post-update settings export matches the baseline | SE17 (policy, control id), SE20 (execution) |
| SE11-SECREQ-03 Management-plane isolation | All management endpoints (host admin, hypervisor, NAS admin, switch, UPS software, host agent metrics/events/evidence endpoint, shutdown/WOL command paths) only on `seg.mgmt`, unreachable from `seg.build`, `seg.worker`, `seg.egress`; no management interface exposed to the internet; the NAS shutdown command (S-1) and the evidence intake are authenticated | Port-scan from a host in each of `seg.build`, `seg.worker`, `seg.egress` reaches no management endpoint; from the gateway side no management port is reachable; the NAS shutdown command and an evidence POST fail without credentials (SE11-AC-05 segmentation log) | SE17: inter-segment policy and control id; SE15: MFA, least-privilege, short-lived credentials per §59/§112 |
| SE11-SECREQ-04 Physical and administrative access | Lockable room; host, NAS, switch and UPS inside; the T3-SUB media outside it under the KB-procedure; physical console use is a logged administrative action; segregation between hardware maintenance (SE11/SE20) and security configuration (SE17) per §112 | Room lock verified; devices inside recorded by inventory position; console sessions appear in the host audit log; T3-SUB custody log present | SE17: custody rule for T3-SUB after takeover, access-control id, segregation control |
| SE11-SECREQ-05 Data at rest | Host full-disk encryption on M2_1 with TPM-bound keys (recovery key under KB-3 before enabling); encryption of VM disks on M2_2/M2_3/M2_4 inside the Linux VMs or by the hypervisor (hardware supports both); NAS per-folder AES-256 (B12) for backups, evidence, mirrors and archives; T3 and T3-SUB copies encrypted before leaving the site; the `KEYS` class under §6.3 | Host volume reports encryption on with TPM protector and the recovery key read back from both T3-SUB media; each VM disk or guest volume reports encryption on; NAS shares for T2 report encryption on; a T3/T3-SUB object sampled at rest is ciphertext | SE17/SE15: long-term key custody, recovery and takeover (KB-5); control ids |
| SE11-SECREQ-06 Media sanitisation | NVMe, HDD and T3-SUB media sanitised on decommissioning/RMA; inventory record marks sanitised state | Inventory field present and required for state "decommissioned" | SE17: sanitisation standard and control id |
| SE11-SECREQ-07 Supply chain at receipt (G2) | Serial numbers recorded; packaging/tamper evidence inspected; firmware version read and compared with the G1 row before first power-on; default credentials on NAS, switch and UPS software rotated at commissioning with the new credentials entering `KEYS` under KB-3 | Receipt record per asset with serial, inspection result, firmware version and comparison; credential rotation logged with the KEYS evidence ids | SE17: supply-chain control id |
| SE11-SECREQ-08 Confidential-processing boundary | Private application/customer data is processed only by authorised locally hosted models or deterministic tools (§66); any local accelerator (B11) and the Data VM sit inside `seg.platform` behind the default-deny disclosure gateway on `seg.egress`; hardware telemetry and evidence records (§10.3, §18.2) carry no workload content; `REPO-EXT` holds no customer data; candidate M-C (hosted data) is admissible only where §66 permits | Telemetry and evidence payloads sampled during SE11-AC-09 contain only the §18.2 fields; `seg.platform` has no route to `seg.egress` except via the gateway address (SE11-AC-05) | SE17/EL: gateway policy, control id; §66 applicability decision for M-C and for `REPO-EXT` contents |
