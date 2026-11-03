---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 6
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-REQ-13, SE11-REQ-14, SE11-REQ-15, SE11-REQ-16, SE11-REQ-17, SE11-REQ-18, SE11-REQ-19, SE11-REQ-20, SE11-REQ-21, SE11-REQ-22, SE11-REQ-23, SE11-REQ-24, SE11-REQ-25, SE11-REQ-26, SE11-NFR-01, SE11-NFR-02, SE11-NFR-03, SE11-NFR-04, SE11-NFR-05, SE11-NFR-06, SE11-NFR-07, SE11-NFR-08, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-DEC-09, SE11-DEC-10, SE11-DEC-11, SE11-DEC-12, SE11-DEC-13, SE11-DEC-14, SE11-DEC-15, SE11-DEC-16, SE11-DEC-17, SE11-DEC-18, SE11-DEC-19, SE11-DEC-20, SE11-DEC-21, SE11-DEC-22, SE11-DEC-23, SE11-DEC-24, SE11-DEC-25, SE11-DEC-26, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-ADR-08, SE11-ADR-09, SE11-ADR-10, SE11-ADR-11, SE11-ADR-12, SE11-ADR-13, SE11-ADR-14, SE11-ADR-15, SE11-ADR-16, SE11-ADR-17, SE11-SECREQ-01, SE11-SECREQ-02, SE11-SECREQ-03, SE11-SECREQ-04, SE11-SECREQ-05, SE11-SECREQ-06, SE11-SECREQ-07, SE11-SECREQ-08, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-RISK-09, SE11-RISK-10, SE11-RISK-11, SE11-RISK-12, SE11-RISK-13, SE11-RISK-14, SE11-RISK-15, SE11-RISK-16, SE11-RISK-17, SE11-AC-01, SE11-AC-01b, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-07a, SE11-AC-07b, SE11-AC-07c, SE11-AC-07d, SE11-AC-07e, SE11-AC-07f, SE11-AC-08, SE11-AC-09, SE11-AC-10, SE11-AC-11, SE11-AC-12, SE11-AC-12b, SE11-AC-13, SE11-AC-14, SE11-AC-15, SE11-DEP-01, SE11-DEP-02, SE11-DEP-03, SE11-DEP-04, SE11-DEP-05, SE11-DEP-06, SE11-DEP-07, SE11-DEP-08, SE11-DEP-09, SE11-DEP-10, SE11-DEP-11, SE11-DEP-12, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05, ASM-SE11-06, ASM-SE11-07, ASM-SE11-08, ASM-SE11-09, ASM-SE11-10, ASM-SE11-11, ASM-SE11-12, ASM-SE11-13, ASM-SE11-14, ASM-SE11-15, ASM-SE11-16, ASM-SE11-17, ASM-SE11-18, ASM-SE11-19]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v6 (revision of v5 after review findings REVIEWER-EN-SE11-PHYSICAL-001, 003, 006, 008, 009, 010, 011) · **Owner:** SE11 (Infrastructure, Containers & Runtime Engineering, SEED-01 §74) · **Run:** SMK-20261103114255 · **Baseline gate status:** **BLOCKED — two unmet review gates** (required source PL-REQ-ID-REGISTER not consumed, §0.3; QC-AR-03 compatibility/availability evidence absent, §11.2). The architecture content is complete and self-reviewed; the baseline is not signed off (§17).

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and reference BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, defines the contracts SE11 provides, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite by this document id and the disposition they rely on. It selects no vendor, prices nothing and purchases nothing (§15).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`, unchanged since v4), consumed sections: hardware strategy §152–§177 (document sections 37–45, including the section-40 reference-configuration table inside §160), the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note at the end of §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231), the guardrails Appendix H (§232–§238) and the domain list §74. No BOM content is recreated from memory; every specification cited below is taken from those sections (re-read in v5; the seed sha is unchanged in this run, so the v5 figures are carried forward unchanged).

## 0. Document status, source availability and limitation

### 0.1 Inputs: what was available and what was not (re-verified in this run)

| Input (context id) | Tool result in this run | What SE11 needed from it | Effect on this document |
|---|---|---|---|
| PL-REQ-ID-REGISTER (required source) | `read_document` → `not_found`; `list_documents 10-Product-Lead/` → empty | Requirement / decision / constraint ids with full specification and seed section | **UNMET SOURCE.** Not read, not consumed, not reconciled. SE11 makes **no claim** that its seed interpretation equals the register's resolved statements. The §0.5 table is a traceability of SE11's positions to SEED-01 sections only; it is not, and is not presented as, a register reconciliation. Consequence: baseline gate BLOCKED (§0.3, §17) |
| PL-REQ-REGISTER-G01 … G04 (register fragments) | `read_document` → `not_found` (index lists 60 chars, 0 sections) | Verbatim BOM appendix | BOM read directly from SEED-01 §227–§231 (permitted for SE11 by the hardware-chain rule) |
| PM09-* (14 product documents) | Absent (`list_documents 20-Product-Domains/PM09/` → empty) | MVP scope, product NFRs, acceptance criteria, risks/constraints, decision log, KPIs | **Unreconciled.** Every NFR value in §3 is an SE11 engineering proposal (ASM-SE11-06); the checks SE11 will run against each document when it exists are listed in §0.6 |
| NT16-* (8 vendor/dependency documents) | Absent | External-dependency and SLA requirements, exit/replacement assessment | **Unreconciled.** External-provider residual risks (FD-EXT-AI, FD-INTERNET, FD-EXT-REPO, hosted equivalents, T3 provider) are stated from the seed only (SE11-DEP-09) |
| EL-* (26 engineering-lead documents) | Absent (`list_documents 40-Engineering-Lead/` → empty) | System/runtime/deployment/reliability architecture, NFR ids, ADRs, interface-contract governance and register, estimates, sequencing, DoR/DoD | **Unreconciled.** No EL decision id is cited; no EL review has occurred; EL's contract register does not exist, so the SE11 contracts are registered in the SE11 register of record (§18.2) and their transcription into EL's register is a placed requirement (SE11-DEP-02) |
| SP16-* (7 FinOps documents) | Absent | Cost allocation, spend guardrails, unit economics | **Unreconciled.** The economic half of the seed's justification rule for local capacity (§238) cannot be evaluated; local-versus-hosted stays open per pool (SE11-ADR-01, gate G-LOCAL, SE11-DEP-08) |
| SEED-01 (seed, read on demand) | Available, sha unchanged since v4 | Hardware strategy and BOM | Sole substantive input of this version |
| SE11's own sibling artefacts (SE11-INTERFACE-CONTRACT, SE11-HARDWARE-CAPACITY-SIZING, SE11-POWER-COOLING-RACK) | `list_documents 50-Engineering-Domains/SE11/` → only the two smoke outputs of this document | Contract register, sizing record, rack/thermal detail | This document carries the SE11 contract register of record (§18.2) until SE11-INTERFACE-CONTRACT exists; sizing and rack detail remain referenced, not duplicated |

### 0.2 Decision status model and baseline gate status

Every decision, requirement and NFR in this version carries the status **PROV** (provisional: traceable to seed sections, not register-bound, not EL-reviewed, not product-NFR-checked). The status **REC** (reconciled) can only be assigned by a later version after SE11-AC-11 has actually consumed the register and the upstream documents. **No entry in v6 is REC.**

**Baseline gate status: BLOCKED.** Two review gates of this document class are **not satisfied** in this version and are not represented as satisfied anywhere in it:

| Gate | Criterion / source | Status | Why it cannot be closed inside the authorized corpus | What closes it |
|---|---|---|---|---|
| Gate A — authoritative baseline | OUT-AR-01 required source PL-REQ-ID-REGISTER | **UNMET SOURCE** | The file does not exist (`not_found`); the global rules forbid outside facts and forbid reading anything else | SE11-AC-11: the register and the §0.6 upstream documents are read, every SE11 position is reconciled against their actual statements, conflicts recorded and resolved by reviewers |
| Gate B — compatibility/availability | QC-AR-03 | **UNMET CRITERION** | The corpus contains no manufacturer support, firmware, qualified-list, driver or availability publication; SE11 has no access to such publications in this run and invents none (BND-04) | SE11-AC-01 (gate G1, documents only): dated, attributable evidence rows establishing at least one coherent, currently supported, practically available configuration |

Downstream documents that cite this version cite it as `SE11-PHYSICAL-INFRASTR-HARDWARE v6 (PROVISIONAL, BLOCKED)` and carry the same status for anything derived from it (SE11-REQ-11). Nothing may be ordered, built or treated as verified on this version.

### 0.3 Unmet-source and unmet-criterion dispositions, and how the completion event encodes them (findings 001 and 008)

The completion-event schema admits exactly two values per source and per criterion: `covered` or `not_applicable`. Neither word means "unmet". Previous versions encoded these two items as `covered` and were correctly rejected: an unread source is not covered, and a criterion whose required evidence does not exist is not covered. This version therefore encodes both as **`not_applicable`**, with the following single meaning, stated here as the one-line reason the author rules require and repeated where each item lives (§1.1, §11.2, §19):

> `not_applicable` = **could not be applied: the input the criterion or source requires does not exist in the authorized corpus of this run; the item is UNMET; the baseline gate is BLOCKED; no coverage is claimed.**

It does **not** mean the source or criterion is irrelevant to this document class — both are central to it, which is exactly why the baseline is blocked. The document never claims that the register was consumed, that any G1 evidence exists, or that SEL-0 (§11.3) closes the compatibility criterion; SEL-0 is a *selection record of what would be checked*, not evidence.

| Item | What v6 does (substance that is possible inside the corpus) | What remains unmet (declared, not hidden) | Event value |
|---|---|---|---|
| Required source PL-REQ-ID-REGISTER | §0.5 traces every SE11 decision, requirement, NFR, risk and assumption to the SEED-01 sections it rests on, so that the future reconciliation (SE11-AC-11) has a complete, position-by-position input; §0.6 lists the mechanical checks per upstream document; deviations from the seed are C1–C6 (§0.7, §16.6) | The register itself: its resolved requirements, decisions and constraints are unknown to SE11; equivalence with SE11's seed reading is **not** assumed (ASM-SE11-01 now states only that the file is absent); every §0.5 row is unreconciled; status PROV; gate A BLOCKED | `not_applicable` (UNMET SOURCE) |
| QC-AR-03 | §11.1 structural check from the BOM text; §11.3 records SEL-0 as the candidate set and the empty G1 register with its row schema; FC-02 made consistent with the documents-only G1 gate (commissioning never closes it); §11.4 specification classes so that no part number is baselined | Current manufacturer support and present availability: **no evidence row exists**; fingerprint v0 does not exist; gate B BLOCKED (ASM-SE11-16) | `not_applicable` (UNMET CRITERION) |

Consequences carried through the document: status PROVISIONAL/BLOCKED (§17); every entry PROV (§0.2); SE11-RISK-05 and SE11-RISK-09 open. `checks.dependency_consistency` in the completion event asserts only that this document contradicts no *existing* approved document (none exists) and is consistent with the seed; it asserts no reconciliation with absent documents. `unresolved_issues` is empty because the two gates are not issues the author can resolve: they are declared, encoded and blocking, and the document says so wherever a reader could be misled.

### 0.4 Disposition of the v5 review findings

| Finding | Correction made in v6 | Where |
|---|---|---|
| 001 (major) register not consumed; "only id binding missing" and "covered" assertions false; upstream documents unreconciled | Both assertions removed. The source is disposed as **UNMET SOURCE**, not covered; §0.5 renamed and reframed as seed-only traceability with no equivalence claim; ASM-SE11-01 rewritten to state only the absence; baseline gate A BLOCKED (§0.2, §17); event value `not_applicable` with the one-line meaning in §0.3 and §1.1; §0.6 obligations kept as the content of SE11-AC-11 | §0.1–§0.3, §0.5, §1.1, §16.5, §17, §19 |
| 003 (major) mutation not bounded under publisher loss; store told ALLOW can write indefinitely; enforcement not an obligation of each store | **Mutation lease** (SE11-DEC-23, SE11-ADR-16, SE11-REQ-24): every `SIG-PROTECTION-STATE` level carries `lease.until` = max(t3_last_ok + A_max + G, t3sub_last_ok + A_max); a store may mutate only while its own clock < `until − U` (U = 300 s clock margin, ASM-SE11-18), **independently of publisher reachability**; STALE/UNKNOWN neither extends nor is needed to end the lease. Startup, restart, clock-rollback, skew-rejection and recovery rules specified (§6.3b). Producer registration **requires** a passed lease-conformance record (SE11-AC-07e) per store build, enforced by the validator (SE11-REQ-23); the end-to-end bounded-exposure guarantee is stated as conditional on that evidence, and a store without it cannot register, so its class holds no real data (I6). New test SE11-AC-07e: publisher stopped across the expiry deadline while the store (including SE11's bootstrap store) attempts mutations | §6.3, §6.3b, §14 (AC-07e), §18.2 Part B/C, §18.3 CI-2 |
| 006 (major) S-2/M1 restart unimplementable (host has no direct UPS link for S5); S-3/N1 wakes the NAS without UPS-N's state | **S5 defined per topology** (SE11-DEC-25, §8.3b-S5): S-1 host reads UPS-A directly; **S-2/M1** host reads mains/charge through the NAS UPS service after both devices boot by AC-recovery, bounded wait W_s2 = 600 s (ASM-SE11-19), fail-safe HOST-ONLY-HOLD (no VM start, no N1, alert, poll) with the exposure recorded (SE11-RISK-17); **S-3** host eligibility from UPS-A, NAS eligibility from UPS-N **independently**: M1-N tracks UPS-N's own mains; **N1 admissible only when UPS-N is on the same branch circuit as UPS-A** (recorded in the fingerprint, identified in the electrician's sign-off, SE11-REQ-26) and with the NAS-side guard (NAS reads UPS-N after wake; on-battery → immediate own shutdown); different circuit → M1-N mandatory, else NAS attended (exposure). Timing recomputed per topology (S-2/M1: T_restart 690 s, T_service_clean 1,170 s, T_service_forced 1,770 s). Drills (k) NAS UPS service unavailable under S-2, (l) UPS-A restored while UPS-N on battery, (m) NAS-side guard | §8.1, §8.3a, §8.3b, §14 (AC-15 k–m), §16 |
| 008 (major) no G1 evidence; "covered" by redefinition rejected; FC-02 allowed a G3 pass to qualify | QC-AR-03 disposed as **UNMET CRITERION** (`not_applicable` per §0.3); no claim that SEL-0 closes the finding — SEL-0 is labelled a candidate selection record, not evidence (§11.2, §11.3, §17). **FC-02 corrected**: closed only by the board manufacturer's qualified-list entry or validated-population statement for the exact kit and population; SE11-AC-04 is a G3 test that may re-open the row and never closes it; where no documentary closure exists, the population is "not confirmed" and the in-class alternative is a listed population or kit | §0.3, §11.2 (FC-02), §11.3, §17, §19 |
| 009 (major) KEYS bootstrap circular: Part C tokens and Part B read token needed before they exist | **Bootstrap channel** (SE11-DEC-24, SE11-ADR-17, SE11-REQ-25): during the bootstrap window Part B/C are served only on a local OS-authenticated channel (no network listener) to the bootstrap store, which runs under the host agent's service account; registration is static in the host build with `auth=local-channel`; the window closes by a committed flag flip and host-agent restart that enables token-authenticated network endpoints and **removes** the channel; the validator rejects an open window once tokens exist. Trace re-executed with every credential creation and use ordered (§14 AC-07d steps 0–4), invariant I7 added, negative checks for unauthorized bootstrap attempts | §6.3c, §13 (SECREQ-03), §14 (AC-07d), §16, §18.2 |
| 010 (major) `unix_seconds × 10^6` floor not monotonic after same-second restart or clock rollback | **Incarnation-aware cursor** (SE11-DEC-22 revised, SE11-ADR-15 revised): identity = (`inc`, `seq`) with `inc` a 128-bit random value generated at every publisher start and `seq` gap-free from 1 within the incarnation; the API accepts and compares `inc`; mismatch → `409 incarnation_changed` + snapshot (explicit reset/snapshot handshake); wall-clock never enters identity; snapshots carry the last edge events so no edge is silently lost. AC-09 extended with (g) same-second double restart with store loss and (h) clock set earlier than the last issued event | §10.3, §18.2 Part B, §14 (AC-09 g–h), §16 |
| 011 (major) intake and state machine disagree on restore failure, substitute copies, fixture guards | **One authoritative transition table** (§6.3a, SE11-DEC-26): precedence P1 (scope/fixture/duplicate/order guards) → P2 (mechanism broken: two consecutive real restore failures → EXPIRED regardless of age) → P3 (age) → P4 (no-real-data states); fixture records can never advance `t3_last_ok`/`t3sub_last_ok`/`kind`; a substitute (T3-SUB) copy authorizes mutation only after its matched real-copy `RESTORE_OK` on a second machine; a single `RESTORE_FAIL` sets `admit` DENY and triggers an immediate re-copy; duplicate/out-of-order handling; §6.3, §14 and §18.2 Part C now all reference this table. New tests SE11-AC-07f: failed real restore, COPY_OK without RESTORE_OK, recurring fixture pass while real-data protection is EXPIRED, verified T3-SUB copy in EXPIRED, duplicates/out-of-order | §6.3, §6.3a, §14 (AC-07c/07f), §18.2 Part C |

### 0.5 Seed-level traceability of SE11 positions (SEED-01 only — not a register reconciliation; input to SE11-AC-11)

Each row names the SEED-01 section(s) an SE11 position rests on, the seed statement in short, SE11's position and the outcome against the seed. "Consistent" means SE11's position follows the seed statement; "Deviation Cn" means both sides are stated in §0.7 for reviewers. **No row has been checked against PL-REQ-ID-REGISTER or any upstream document; whether the register's resolved statements agree with the seed readings below is unknown.**

| SE11 id(s) | SEED-01 section(s) | Seed statement (short) | SE11 position | Outcome vs seed |
|---|---|---|---|---|
| SE11-ADR-01, gate G-LOCAL, B19 | §157, §158, §160, §168, §226 note, §238 | Provision only justified capacity; hosted equivalents acceptable where they better satisfy requirements; no premature local-compute constraints | Candidate architecture with per-element gate G-LOCAL; hosted-first workers | Consistent |
| SE11-ADR-02, B9 | §166, §167, §168, §227.9 | Windows host + Hyper-V Linux VMs + containers for durable services; WSL2 for interactive use | Adopted as the operating model | Consistent |
| SE11-ADR-03, SE11-RISK-02, B4 class | §227.4, §228.1 | Non-ECC DDR5 on the central node; ECC on the NAS | Non-ECC accepted and monitored; ECC class recorded substitute | Consistent |
| SE11-ADR-04, SE11-DEC-04, B11, §5.5 | §175, §176, §177, §227.7, §227.11, §160 table | GPU optional at initial acquisition; driven by measured demand; 750 W PSU compatible when the power budget is validated | Deferred; preconditions incl. measured power check | Consistent |
| SE11-ADR-05, SE11-REQ-03, §6.5 | §163, §164 | NAS is the durable tier, not a latency substitute; RAID is not the only backup; irreplaceable data gets an isolated copy | Host NVMe independent volumes; T1→T2→T3; protection states | Consistent |
| SE11-ADR-06/11/13, SE11-DEC-07/10/13/17/19/25, SE11-REQ-06/15/20/26, §8.3 | §165, §228.1, §229.1 | UPS protects PC, NAS and critical network components long enough for controlled shutdown; integrate graceful shutdown with Windows/NAS | Gated signalling candidates; timed sequences; admissible restart mechanisms with per-topology eligibility | Consistent; C3 records the S-3 topology substitution |
| SE11-ADR-07, SE11-DEC-08, B17 | §165, §166, §230 | Switch/rack "if local rack infrastructure is selected"; rack UPS feeds switch when used; switch ≥ 2×10GbE | Switch adopted at baseline on PD-A; rack deferred | Deviation C1 (switch power domain), C4 (switch before rack) |
| SE11-ADR-08, SE11-DEC-03/06/15 | §158, §159, §162, §164, §234, §238 | Quantities conditional on evidence; measure before resizing | Capacity candidates with decision rules; smaller default | Consistent; C5 recorded for transparency |
| SE11-ADR-09/12, SE11-DEC-09/16, SE11-REQ-02/16 | §156, §157, §163, §174, §227.6 | Reserve CPU/memory/storage I/O for stable platform operation; priority classes | Highest-priority VMs on M2_4; I/O budget on M2_2 | Deviation C2 (role labels) |
| SE11-ADR-10, SE11-DEC-11, SE11-REQ-01/14, SE11-NFR-01 | §157, §174, §175 | Noncritical jobs are paused/shed when capacity degrades | Weighted contention at the hardware layer; shedding by the scheduler on SE11 signals | Consistent |
| SE11-REQ-05 | §160 | No hard-coded host names, local paths or addresses | Portability requirement on every VM/container definition | Consistent |
| SE11-REQ-07/08, SE11-NFR-04 | §160, §234 | Capture performance/resource telemetry from the first workloads | Inventory identity; telemetry contract from first power-on | Consistent |
| SE11-REQ-09, SE11-SECREQ-02 | §12, §25, §160 | Current-practice revalidation; certified components | Firmware lifecycle with signed images and settings baseline | Consistent |
| SE11-REQ-10, B18 | §165, §231 | Two separate 15 A breakers; UPS direct to wall; 20 A optional | Requirement for qualified professionals; nothing designed; circuit identity recorded for SE11-REQ-26 | Consistent |
| SE11-REQ-13/17/18/21/24, SE11-DEC-18/23/26, SE11-NFR-05, §6.3 | §164, §31 | Isolated copy for irreplaceable data as the program matures; rollback and recovery as design requirements | Protection states with bootstrap boundary, bounded ANCHOR exposure and a consumer-enforced mutation lease | Consistent |
| SE11-SECREQ-01…08, SE11-REQ-19/25 | §59, §66, §112, §185, §228.1 | MFA, zero-trust secrets, confidential processing boundary, per-folder AES-256 | Hardware security requirements with SE11-executable checks; bootstrap channel confined to the host OS | Consistent |
| §9 failure domains, SE11-NFR-06/07 | §172, §173, §175 | Redundancy must cover actual shared failure points, not merely worker count | Named common-mode domains with owners and residuals | Consistent |
| §12 triggers, REV-* | §159, §161, §171, §226 | Evidence-driven thresholds; central node complements workers | Triggers and revision boundaries | Consistent |
| ASM-SE11-02, SE11-RISK-08 | §0, §151 | Rev 1.1 proposed; v1.0 authoritative until approval; change control | Rev 1.1 treated as operative because only it holds the hardware baseline | Deviation C6 |
| SE11-DEC-14, SEL-0, SE11-DEC-21 | §226 note, §12, §227–§231 | BOM is a reference configuration, not an assertion of owned equipment; revalidate current practice before build | Part numbers deferred pending G1; SEL-0 as the candidate reference set | Consistent |
| SE11-REQ-22, SE11-DEC-22, SE11-ADR-15 | §30, §160 | Observability by construction; telemetry from first workloads | Event protocol with incarnation-aware cursor and bootstrap condition | Consistent |

### 0.6 Upstream reconciliation obligations (the content of SE11-AC-11; none executed in this run)

| Upstream document (absent) | What SE11 checks against it | If it conflicts |
|---|---|---|
| PL-REQ-ID-REGISTER, PL-REQ-REGISTER-G01…G04 | Every §0.5 row against the register's actual statement for the same seed section; every register row touching §152–§177, §226–§238 and §59/§66/§112 against this document | Conflict recorded under §16.6 with both sides; SE11 position changed where the register governs; reviewers resolve |
| PM09-NONFUNCT-REQUIREM, PM09-ACCEPTAN-CRITERIA | SE11-NFR-01…08 values vs product NFRs; recovery targets vs product RPO/RTO | NFR value replaced or conflict recorded; dispositions re-checked |
| PM09-MVP-SCOPE, PM09-ROADMAP, PM09-PRIORITI-BACKLOG-FEATURE | Whether local hardware is in MVP scope at all (gate G-LOCAL inputs); stage windows for SE11-DEP needs | G-LOCAL outcome per pool recorded; triggers re-timed |
| PM09-PRODUCT-RISKS-CONSTRAI, PM09-PRODUCT-DECISION-LOG, PM09-PRD, PM09-PRODUCT-BRIEF, PM09-STRATEGY, PM09-USE-CASES-USER, PM09-FUNCTION-REQUIREM, PM09-CROSS-DEPENDEN-REGISTER, PM09-KPIS-SUCCESS-METRICS | Decisions touching hosting, data residency, confidential processing (§66), spending; functional needs that imply pools or data classes; KPIs that imply telemetry | ADR-01 Step 2 admissibility updated; pool/class list extended; §10.3 signals extended |
| EL-ARCHITEC-DECISION-RECORD, EL-INFRASTR-RUNTIME-ARCHITEC, EL-ENVIRONM-DEPLOYME-ARCHITEC, EL-SYSTEM-RELIABIL-RESILIEN, EL-HIGH-LEVEL-SYSTEM, EL-SYSTEM-CONTEXT-COMPONEN, EL-SYSTEM-DATA-ARCHITEC, EL-SYSTEM-IDENTITY-SECURITY, EL-SYSTEM-AI-AGENT, EL-SYSTEM-OBSERVAB-OPERATIO, EL-SYSTEM-TEST-VALIDATI | Each SE11-ADR against EL ADRs; pool naming; VM boundaries; failure-domain residual acceptance; data classes vs EL data architecture; signal consumption | Conflict recorded; EL supersedes only via a new ADR |
| EL-ENGINEER-NFR-SPECIFIC | NFR ids to bind SE11-NFR-01…08 | Binding recorded; values reconciled |
| EL-INTERFAC-CONTRACT-GOVERNAN, EL-CROSS-ENGINEER-DEPENDEN | Transcription of SE11-CREG-001…003; dependency ids | Registration references added to §18.2 |
| EL-ENGINEER-ESTIMATE-CAPACITY, EL-ENGINEER-IMPLEMEN-SEQUENCI, EL-ENGINEER-PLANNING-CHARTER, EL-ENGINEER-DEFINITI-READY, EL-ENGINEER-DEFINITI-DONE, EL-TECHNICA-VISION-ENGINEER, EL-ARCHITEC-PRINCIPL-ENGINEER, EL-ENGINEER-FEASIBIL-ARCHITEC, EL-TECHNICA-RISK-REGISTER, EL-TECHNICA-ASSUMPTI-CONSTRAI, EL-TECHNOLO-SELECTIO-BUILD | Per-pool demands for §5.3 Step 0; the stage by which each SE11-DEP is needed; DoR/DoD inclusion of SE11-REQ-13/17/18/24; technology choices affecting B9/hypervisor; risk/assumption ids | SE11-DEC-03a/06a recorded in the sizing document; DoR references; conflicts recorded |
| NT16-* (all eight) | FD-EXT-AI, FD-INTERNET, FD-EXT-REPO, T3 provider and hosted-equivalent risk/SLA; exit/replacement for the repository provider | Residual dispositions in §9 updated |
| SP16-* (all seven) | Economics for G-LOCAL and §5.3 Step 2; spend guardrails on hosted equivalents | Local-versus-hosted per pool decided |

### 0.7 Seed consistency check — deviations (both sides; §16.6 repeats them)

| Id | Seed statement | This document | Disposition |
|---|---|---|---|
| C1 | §165: the rack UPS "feeds rack PDU for local worker nodes **and switch** when used"; the same section gives the PC+NAS UPS the purpose "protect central PC, NAS **and critical network components** long enough for controlled shutdown" | The core switch is powered from PD-A (UPS-A) | Deviation accepted (SE11-DEC-08): the rack does not exist at baseline, the switch is a critical network component in the seed's own words, and in candidate S-1 the NAS shutdown command crosses it. When the rack exists the switch stays on PD-A unless S-3 (no command path) is in use, in which case it may move to PD-B as §165 states. Reviewers resolve if they read the rack clause as mandatory |
| C2 | §227.6: M2_4 = "platform data / DBs / containers", M2_2 = "VM & artifact store" | Highest-priority VM system disks are placed on M2_4 with the data; M2_2 carries High/Medium VM disks and artifacts; Mapping-V (§6.1a) may move Validation to M2_3 | Deviation recorded as SE11-DEC-09/ADR-09 with reason (§157 reservation principle, §174 priority classes) and impact (§6.1) |
| C3 | §165/§229.1: one PC+NAS UPS with "automatic graceful shutdown via PowerPanel / NAS UPS service" | SE11 does not assert that any host↔NAS signalling combination works; candidate S-3 substitutes a second UPS for the NAS | Gated decision SE11-DEC-10; S-3 is a topology substitution of B15 recorded with reason (no evidenced cross-device integration) and impact (second UPS of the B16 class, separate runtime budget, circuit condition SE11-REQ-26) |
| C4 | §166/§230: switch and rack items apply "if local rack infrastructure is selected" | The managed switch (class) is adopted at baseline without a rack | Deviation accepted (SE11-ADR-07): three or more endpoints and VLAN enforcement of `seg.*` need a switch regardless of the rack; the smallest class satisfying §230 is used (§158 no-overbuild); the interim point-to-point placement of §7.2 remains allowed |
| C5 | §227.4 and §228.3 list 4×64 GB and 6×20 TB as the reference quantities | Quantities are candidates sized by rule; defaults M-A (128 GB) and N-A (4 drives) | Not a conflict: §162, §164 and §238 make the quantities conditional; recorded for transparency (SE11-ADR-08) |
| C6 | §0: Rev 1.1 is "proposed"; "the approved v1.0 document remains authoritative until this revision is explicitly approved" | Rev 1.1 is treated as the operative seed because only Rev 1.1 contains the hardware baseline | ASM-SE11-02, SE11-RISK-08; sign-off bound to the Rev 1.1 sha so that approval or change re-enters this document |


## 1. Authoritative source baseline (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01)

**Required source PL-REQ-ID-REGISTER — UNMET SOURCE (event value `not_applicable`, meaning per §0.3: could not be applied because the file does not exist in the authorized corpus; not consumed; not reconciled; gate A BLOCKED).** This section therefore establishes the baseline against the only authoritative input available to SE11, SEED-01, and states plainly that the register-level baseline the criterion asks for is not established.

### 1.1 Exact version and sections consumed

| Item | Value |
|---|---|
| Seed | SEED-01, "Master Product Vision & Operating Architecture — Proposed Revision 1.1", "Expanded 2026 Baseline — Greenfield, Opportunity Intelligence, 19-Gap & Infrastructure Edition" (§0); file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| BOM version | Appendix G "Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note in §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231) |
| Strategy sections | §152–§154 (37.x stage boundaries, shared hardware, evidence progression), §156–§157 (38.x required logical environments, resource-reservation principle), §158–§160 (39.x no-wait/no-overbuild, evidence-driven thresholds, portability, section-40 reference configuration table), §161–§163 (40.x central node, memory, NVMe), §164–§166 (41.x NAS, UPS/electrical, rack/network and the section-42 operating model), §167–§168 (42.x layout, VMs + containers), §169–§171 (43.x workers), §172–§175 (44.x redundancy, quorum, resource classes, degradation), §176–§177 (45.x GPU) |
| Guardrails | Appendix H §232–§238 (H.1–H.7) |
| Domain boundaries | §74 (SE11 = Infrastructure, Containers & Runtime Engineering; SE12 = Database, Storage & Data; SE14 = API, Integration & Portability; SE17 = Infrastructure, Workload & Data Security; SE19 = Performance, Resilience & Specialized Validation; SE20 = SRE, Observability & Production Operations; SE01 = Core Platform & Distributed Systems) |
| Approval status of the seed | §0: "The approved v1.0 document remains authoritative until this revision is explicitly approved." The hardware baseline exists only in Rev 1.1 (conflict C6, ASM-SE11-02); sign-off binds to that exact revision and sha (§17) |
| Register binding | **None.** PL-REQ-ID-REGISTER absent; no register id is cited or invented; see §0.3 |
| Selection record | SEL-0 (§11.3): the Appendix G v2.2 set as the candidate reference configuration; part numbers deferred pending G1; **not evidence of current support or availability** |

### 1.2 Classification and engineering disposition of every BOM entry

The seed states that Appendix G "is a greenfield reference configuration, not an assertion of already-owned equipment or a mandatory topology" and that Product/Engineering "may procure, substitute, resize, or use hosted equivalents when evidence shows equal or better capability, reliability, portability, security, schedule, and economics" (§226 status note); that "local central compute, NAS, power, and worker infrastructure should be provisioned when workload evidence and economics justify it; managed/hosted equivalents remain acceptable where they better satisfy the target requirements" (§238); and that the central node "is a reference configuration rather than an inherited constraint" (§160, section 40 lead-in).

**Reading rules for the table.** (a) A disposition is the disposition *of the specification class of the reference item if local provisioning of that element is justified* under gate G-LOCAL (SE11-ADR-01); it is not a decision that local provisioning is justified. (b) **Part-number status (SE11-DEC-14):** the corpus contains no manufacturer support, firmware, qualified-list, driver or availability statement for any part number beyond the seed's own assertions at its revision date (§11.2). Every part number cited from the seed is therefore **DEFERRED-PENDING-EVIDENCE**: it is the seed's reference exemplar of the class and a member of selection record SEL-0; it is not baselined; it enters the configuration fingerprint only when its G1 (SE11-AC-01) record reads "confirmed". The *class* (§11.4) is what is adopted. (c) "Quantity/count status" separates the adopted class from any capacity figure, which is never adopted from the maximum listed configuration (ENV-DEC-017).

| # | BOM entry (seed section; the part number is the reference exemplar) | Seed class | Engineering disposition of the specification class (SE11 only) | Quantity / count status | Decision ref |
|---|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, Zen 5 homogeneous, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — class §11.4; virtualization extensions and IOMMU enabled; 230 W package limit is the compute line of the power budget (§8.2). Part number DEFERRED-PENDING-EVIDENCE | n/a (one CPU) | SE11-DEC-01, SE11-DEC-14 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — class: dual-tower air cooler ≤ 160 mm with AM5 mounting; structural check only (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi: 4×DDR5 to 256 GB; PCI_E1 Gen5 x16 (CPU); PCI_E2 Gen3 x1; PCI_E3 Gen4 x4 (shares with M2_3); M2_1 Gen5 x4 CPU; M2_2 Gen5 x4 CPU sharing with USB4; M2_3 Gen4 x2 chipset; M2_4 Gen4 x4 chipset; 4×SATA; 5 GbE; Wi-Fi 7; BT 5.4; 2×USB4; Flash BIOS; Clear CMOS (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map verified before baseline (SE11-AC-02) with fallbacks A/B/C and Mapping-V (§6.1a); Wi-Fi/Bluetooth disabled in server role; no out-of-band controller, so the management path is §10.2. Part number DEFERRED-PENDING-EVIDENCE (BIOS/CPU support currency not established, FC-01) | n/a | SE11-DEC-02, SE11-DEC-12, SE11-DEC-14 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC, single matched kit; "step down to 5600/5200 if 4-DIMM training is unstable" (§227.4; §162) | Preferred target (class); evidence-driven (quantity) | ADOPT WITH ENGINEERING CONSTRAINT for the **class** (DDR5 UDIMM matched kit on the AM5 4-slot platform, EXPO with the seed's 5600/5200 fallback, non-ECC accepted and monitored, SE11-RISK-02). Part number DEFERRED-PENDING-EVIDENCE; population qualification FC-02 open | **CANDIDATE.** 256 GB (4×64) is the reference *ceiling*, not adopted capacity. Quantity chosen by Table 5.3-R and the admission rule of §5.3 (M-A default; larger candidates only by the ordered procedure) | SE11-DEC-03, SE11-DEC-15, SE11-ADR-03, SE11-ADR-08 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch at x2 is acceptable subject to SE11-AC-02; under Mapping-V the M2_3 device carries Validation instead (§6.1a). Part number DEFERRED-PENDING-EVIDENCE | 2 devices (roles per §6.1/§6.1a) | SE11-DEC-02, SE11-DEC-12, SE11-DEC-16 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; seed roles "platform data / DBs / containers (M2_4)", "VM & artifact store (M2_2)" (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID (SE11-ADR-05); role mapping deviates from the seed's literal labels (conflict C2, SE11-DEC-09, §6.1). Part number DEFERRED-PENDING-EVIDENCE | 2 devices | SE11-ADR-05, SE11-DEC-09 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build; with the 145 W optional GPU only after the measured power-budget check the seed itself requires (§227.11: "compatible with a 750 W-class PSU when the final component power budget and headroom are validated"); any accelerator above 145 W, dual-slot, or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance, 3×140 mm fans (§227.8) | Preferred target | ADOPT — class §11.4; clearance and form factor structurally compatible with B2/B3 (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B9 | OS — Windows 11 Pro retail (§227.9; operating model §166) | Fixed by the operating model (§166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role; persistent services only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13). Edition/licence identifier DEFERRED-PENDING-EVIDENCE | n/a | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); if coexistence fails, Fallback A relocates the NIC to PCI_E1 while the GPU is deferred (SE11-DEC-12); hypervisor virtual-switch driver support not established (FC-05). Part number DEFERRED-PENDING-EVIDENCE | 1 device | SE11-DEC-02, SE11-DEC-12 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell, 24 GB ECC, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition" §175; "driven by measured demand and economics" §177) | DEFER / OPTIONAL — adoption preconditions §5.5 and trigger TRG-GPU §12.2; when triggered, Fallback A (NIC in PCI_E1) must first be undone or replaced (§6.1a) | 0 at baseline | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T: 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock (64 GB max), 2×10GbE + 2×5GbE, 2×USB4, 4×M.2, ADM/Btrfs snapshots, per-folder AES-256, "UPS support / network UPS server" (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only (never a live datastore); admin interface on `seg.mgmt`; firmware lifecycle §10.4; UPS-signalling role gated by SE11-DEC-10/19/25. Part number DEFERRED-PENDING-EVIDENCE | 1 enclosure; subject to G-LOCAL (hosted object storage is the recorded equivalent for T2/T3, §6.7) | SE11-ADR-05, SE11-DEC-10 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install on TRG-NAS-MEM (§12.2) | 0 at baseline | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target (class); count tied to retention policy (§164) | ADOPT WITH ENGINEERING CONSTRAINT for the **drive class** (3.5-inch enterprise CMR, RAID 6 mandatory at ≥ 20 TB per drive, SE11-RISK-06). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** Six drives is the reference *ceiling*; count chosen by the §6.7 rule (N-A default) | SE11-DEC-06, SE11-ADR-08 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, line-interactive AVR, 12 outlets (6 battery + surge, 6 surge only), NEMA 5-15P, USB HID, "automatic graceful shutdown via PowerPanel / NAS UPS service", RB1290X2 batteries (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement; per-candidate shutdown budget SE11-REQ-06 with fail-closed outcome (§8.4); signalling and restart integration gated by the admissibility matrix and the per-topology eligibility rules (SE11-DEC-10/13/17/19/25). Part number DEFERRED-PENDING-EVIDENCE | 1 unit (S-1/S-2); 2 units of the B15/B16 classes in S-3 | SE11-DEC-07, SE11-DEC-10, SE11-DEC-13, SE11-DEC-19, SE11-DEC-25 |
| B16 | UPS (rack) — second unit ~1000 VA / 600 W pure sine, model TBD; "when a local worker rack is used" (§229.2; §165) | Candidate ("when used") | DEFER / OPTIONAL — only with a local worker rack, **or** adopted early as the NAS unit under candidate S-3 (conflict C3), in which case its branch circuit is recorded (SE11-REQ-26) | 0 at baseline (1 if S-3) | SE11-DEC-08, SE11-DEC-10 |
| B17 | Rack — 18U; 1U 24-port switch "at least 2×10GbE"; 1U PDU; worker trays sized to measured need; 1U power-brick shelf; "no fixed initial worker count" (§230; §166) | Candidate ("If local rack infrastructure is selected", §166) | Switch: ADOPT WITH ENGINEERING CONSTRAINT by class (managed, VLAN-capable, ≥ 2×10GbE minimum per seed, ≥ 4×10GbE preferred, §7.2; conflict C4). Rack, PDU, trays, shelf: DEFER / OPTIONAL until TRG-WKR-LOCAL (§12.2) | Switch 1; rack items 0 at baseline | SE11-DEC-08, SE11-ADR-07 |
| B18 | Electrical — two separate 15 A breakers (PC+NAS UPS on one, rack UPS on the other); UPS plugged directly into wall; dedicated 20 A optional; typical ~560 W, sustained peak ~1,150–1,300 W (§231; §165) | Fixed constraint (code-regulated) | ADOPT WITH ENGINEERING CONSTRAINT — stated as a requirement for qualified professionals (SE11-REQ-10); nothing electrical is designed here; the sign-off identifies which branch circuit feeds each UPS (input to SE11-REQ-26) | n/a | SE11-REQ-10 |
| B19 | Local worker nodes (form factor and count unspecified; pool "may be local, hosted, cloud or hybrid", §168–§171) | Optional / evidence-sized | DEFER / OPTIONAL — hosted/cloud executors first (§160 "avoid premature local-compute constraints"); local class adopted on TRG-WKR-LOCAL | 0 at baseline | SE11-ADR-01 |

**Tally (authoritative; supersedes any other count):** ADOPT ×2 (B2, B8); ADOPT WITH ENGINEERING CONSTRAINT ×13 (B1, B3, B4-class, B5, B6, B7, B9, B10, B12, B14-class, B15, B17-switch, B18); DEFER / OPTIONAL ×5 (B11, B13, B16, B17 rack/PDU/trays/shelf, B19); SUBSTITUTE ×0 at baseline (S-3 would be a recorded topology substitution of B15 under SE11-DEC-10); ESCALATE ARCHITECTURE IMPACT ×0 at baseline (conditional REV-* triggers in §12.3). Capacity candidates: B4 quantity (M-A/M-B/M-A+/M-C), B14 count (N-A/N-B/N-C). **Part numbers: 17 DEFERRED-PENDING-EVIDENCE (B1–B17), 0 confirmed; all 17 are members of selection record SEL-0 (§11.3), which is a candidate list and not evidence.** No substitution is silent: any future substitution is a new SE11-DEC entry with technical reason and impact (SE11-REQ-12).


## 2. Physical architecture scope and boundaries (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-02)

### 2.1 In scope (owned by SE11)

| Element | Content of this document |
|---|---|
| Local central compute | One central node (B1–B10 classes) as the reference configuration; host role, slot/lane allocation with fallbacks, reservation mechanism (§5) |
| Worker nodes | Capability classes and placement rules for local workers if and when adopted (§4, §12); physical provisioning (trays, power, ports) when triggered |
| GPU / accelerator class | Single-slot, ≤ 145 W, PCIe x16 class; deferred (§5.5) |
| Storage / NAS | Hot NVMe tiers on the host, the durable NAS tier, the physical mapping of every volume, the storage I/O budget, the dataset classes with their bootstrap boundary, the protection transition table and the mutation lease (§6) |
| Network switching / NICs / physical segments | 10 GbE storage/core path, 5 GbE host onboard, switch class, VLAN membership and addressing of the physical segments (§7). Physical-network engineering is SE11's: §74 places SE14 in "API, Integration & Portability Engineering", not physical networking |
| Rack / placement | 18U rack class; desk/room placement constraints (§8.5) |
| UPS / power distribution | Power domains, UPS roles, per-candidate shutdown sequences, the admissibility matrix of signalling × restart mechanisms, per-topology restart eligibility, and the timing budget to service readiness (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10.1) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10.2) |
| Hardware-published signals, states, leases and the protection-evidence intake | Signals, protection levels and mutation leases published under `SE11-CONTRACT-hardware-signals@1`; evidence accepted under `SE11-CONTRACT-protection-evidence@1`; baseline record under `SE11-CONTRACT-hardware-baseline@1` (§18.2) |
| Bootstrap custody and bootstrap authority | The KEYS bootstrap custody procedure on T3-SUB media and the local bootstrap channel until the token contracts are in force (§6.3c) |

### 2.2 Out of scope (owned elsewhere; referenced, never included)

| Concern | Owner (SEED-01 §74 unless stated) | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (chain rule) | §15 |
| Electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only; the sign-off identifies branch circuits (SE11-REQ-26 consumes that fact) |
| System, runtime, deployment and reliability architecture | EL | EL cross-references this document; EL's documents are absent (SE11-DEP-02/10) |
| Capacity model and growth thresholds | SE01 (capacity concern) and SE11-HARDWARE-CAPACITY-SIZING (sizing) | §5.3 and §6.7 give candidate configurations and decision rules; the sizing document applies them (SE11-DEP-03) |
| Load shedding / job pausing policy | EL (scheduler), SE01 | SE11 publishes the signals (SE11-DEC-11, contract §18.2); the shedding policy and controller are not designed here; no SE11 guarantee depends on them |
| Data policy: dataset classification, retention, backup schedule, binding RPO/RTO, long-term key custody; the internal design of each data store | SE12 (data), SE17/SE15 (security, keys) | §6 states hardware-capable targets, protection states, the lease rule every store must enforce (SE11-REQ-24) and provisional defaults; evidence enters through SE11's contract |
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
    HOST[Central host: Win11 Pro + Hyper-V\nVMs: Core + Data on M2_4 / Build-CI + Validation on M2_2\nM2_1 host system, M2_3 scratch - or Validation under Mapping-V\nSE11 host agent: publisher, intake, bootstrap store, baseline record]
    NAS[NAS class B12: RAID 6 (count = candidate)\nsnapshots, backups, evidence, archives, REPO mirror = T2]
    SW[Managed switch class B17: >=2x10GbE (>=4 preferred) + access ports]
  end
  subgraph PD_N[Power domain N: UPS-N class B16 - only in candidate S-3; circuit recorded]
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
  UPSA[UPS-A USB-HID] -- primary signal (gated, SE11-DEC-10/19/25) --> HOST
  HOST -- network shutdown command (S-1, gated) / N1 wake (same-circuit rule) --> NAS
  T3SUB[(T3-SUB media, outside the room:\nKEYS bootstrap custody, bridging copies)] -. offline .- HOST
```

## 3. Stakeholders, concerns and quality attributes (ISO/IEC/IEEE 42010 framing)

| Stakeholder | Concern | Quality attribute (ISO/IEC 25010) | Measured by |
|---|---|---|---|
| EL | One coherent physical architecture to reference; contracts to transcribe; shedding signals to consume | Compatibility, maintainability | §4–§10 cross-references; §18.2 registered contracts; SE11-DEC-11 |
| SE01 | Capacity inputs as ranges with assumptions; signals for the scheduler | Capacity | Table 5.3-R, §6.7, §12 |
| SE12 | Durable tier, RAID/replication boundaries, protection states with a legal bootstrap, the lease rule its stores must enforce, recovery rules, the evidence contract to produce into | Reliability (recoverability, fault tolerance) | §6.3–§6.3b, §6.6, SE11-NFR-05, SE11-AC-07a–f, §18.2 Part C |
| SE14 | Pools addressed portably | Portability | SE11-REQ-05 |
| SE17 / SE15 | Trusted boot, management isolation, encryption support, bootstrap authority confinement, custody takeover | Security (confidentiality, integrity) | §13, §6.3c, SE11-AC-08a/08b |
| SE19 | Burn-in, contention, abrupt-loss and resilience test surface | Reliability (maturity), performance efficiency | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows, shutdown and restart drills | Maintainability (analysability), reliability | §10, SE11-NFR-04 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, ADR-01 gate G-LOCAL, §12 triggers |

**Measurable non-functional targets introduced by this document (status PROV; binding to EL-ENGINEER-NFR-SPECIFIC ids is unmet dependency SE11-DEP-10; values are engineering proposals, ASM-SE11-06; product NFRs unreconciled, §0.6).**

| NFR id | Quality attribute | Target (measurable) | Verified by |
|---|---|---|---|
| SE11-NFR-01 | Performance efficiency / weighted-service guarantee under contention | Under the §14 contention profile: (a) Core and Data VMs: CPU-wait ≤ 5 % in every 60 s window, Core synthetic API probe p95 ≤ 1.5 × unloaded baseline, Data 4 KiB random-read p99 ≤ 2 × unloaded baseline; (b) Validation VM: CPU-wait ≤ 10 % (it receives its full 8 vCPU from reserve + weighted floating share, §5.2); (c) Build VM: receives ≥ 11 LP-equivalents of its 16 (4 reserved + ≥ 7 floating); (d) inside the Build VM, `pool.background` receives ≤ 10 % of the VM's CPU while build jobs saturate (cgroup weight 10 : 100). No ordered shedding is claimed at the hardware layer (SE11-ADR-10) | SE11-AC-12 |
| SE11-NFR-02 | Performance efficiency / storage path | Host↔NAS ≥ 0.7 GB/s sustained for 10 min during concurrent build-cache load; no other path degrades below 80 % of its unloaded throughput | SE11-AC-05 |
| SE11-NFR-03 | Reliability / safe shutdown and restart, per UPS and per admissible candidate × mechanism | For every UPS u in the selected candidate: B_u ≤ 0.7 × R_u (B_u = critical-path budget of §8.3, R_u = measured runtime at measured load); every step completes inside its bound. Restart, given battery charge ≥ 50 % at mains restoration, an admissible combination of §8.3a and the per-topology eligibility of §8.3b-S5: **T_restart ≤ 720 s** (mains restoration → S6 entry); **T_service_clean ≤ 1,200 s** (→ every VM running, Data services started with the NAS reachable or the 300 s NAS-wait cap elapsed, protection levels re-published) after a shutdown in which every VM stopped gracefully; **T_service_forced ≤ 1,800 s** when any VM was force-stopped (bounded filesystem checks, ASM-SE11-15); database crash recovery after a forced stop is SE12's figure, measured and recorded but not bounded here (§8.3b). The S-2/M1 fail-safe HOST-ONLY-HOLD (NAS UPS service unreachable) is a recorded exposure, not a pass of the service bounds | SE11-AC-06, SE11-AC-14, SE11-AC-15 |
| SE11-NFR-04 | Maintainability / observability | 100 % of §10.3 signals exported under `SE11-CONTRACT-hardware-signals@1`, sample interval ≤ 60 s, heartbeat every 60 s, no false STALE during healthy operation, no identifier reuse across publisher incarnations, retained for at least one stage | SE11-AC-09 |
| SE11-NFR-05 | Recoverability (hardware-capable; SE12 binds the product RPO/RTO) | T1→T2 snapshot interval ≤ 1 h and full replication ≤ 24 h; single-VM restore from T2 ≤ 4 h; for every local D-IRR class with real data: state PROTECTED with kind COPY and copy age ≤ A_max = 24 h, or kind ANCHOR with age ≤ A_max from admission; expiry at A_max + G = 48 h (§6.3); **mutation of real data by any registered store ceases no later than `lease.until − U` whether or not the publisher is reachable (§6.3b)**; restore of each D-IRR class from T3 verified at every stage gate (fixture-based, SE11-AC-07b-rec) | SE11-AC-07a–f |
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
| `pool.admin` | Host OS, Hyper-V root, SE11 host agent (publisher, intake, bootstrap store, UPS logic), WSL2 + Docker Desktop interactive use (§167) | n/a | Windows host root partition | Not reservable in Hyper-V; the root partition takes floating LPs (§5.2); operational rule: VM reserves sum ≤ 16 LP so ≥ 16 LP float | Host root reserve + WSL2 cap | M2_1 |

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
| Memory | DDR5 UDIMM matched kit on four slots (board maximum 256 GB, B3); quantity per Table 5.3-R and the admission formula of §5.3; EXPO only after the stability pass; fallback DDR5-5600/5200 as the seed directs; population qualification is a G1 documentary condition (FC-02) | B4 (§227.4), §162 |
| PCIe / slots | PCI_E1 Gen5 x16 reserved for the deferred accelerator (used by the NIC under Fallback A, §6.1a); PCI_E3 Gen4 x4 carries the 10 GbE NIC by default; PCI_E2 Gen3 x1 unused (Fallback C only); 2×USB4 free for emergency storage/console | B3 (§227.3) |
| Local NVMe (4 slots, all populated) | M2_1 Gen5 x4 (CPU): 1 TB host system; M2_2 Gen5 x4 (CPU, shares with USB4): 4 TB Build/Validation VMs + artifact store; M2_3 Gen4 x2 (chipset, shares with PCI_E3): 1 TB scratch (or Validation under Mapping-V); M2_4 Gen4 x4 (chipset): 4 TB Core/Data VMs + platform data + platform container layers; total 10 TB | B5, B6 (§227.5–§227.6), §163; mapping §6.1 (SE11-DEC-09), §6.1a |
| Host OS / hypervisor | Windows 11 Pro with Hyper-V; Linux VMs for all durable services; WSL2 + Docker Desktop for interactive work only | B9 (§227.9), §166–§168 |
| Firmware baseline | UEFI Secure Boot and TPM 2.0 enabled; Wi-Fi 7 / Bluetooth disabled; "restore on AC power loss = power on"; RTC wake enabled and recorded (§8.3b); settings baseline in §13 | §13, SE11-DEC-13, SE11-DEC-17 |
| Thermal | Dual-tower air cooling ≤ 160 mm in a mesh-front mid-tower with three 140 mm intake fans; sustained 230 W CPU package (+145 W optional GPU) validated by SE11-AC-04 | B2, B8 |
| Host agent | The SE11 host agent (Part B publisher, Part C intake, bootstrap store, UPS state machine, N1 sender, baseline record writer) runs on the host OS as one service under a dedicated service account, with its event log, incarnation record, lease store and bootstrap secret store on M2_1 (§6.3c, §18.2). During the bootstrap window it serves only the local channel (§6.3c) | SE11-DEC-22, SE11-DEC-24 |

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
| Scale path | Add a second matched pair → M-A+ (SE11-AC-04 memory pass re-run; §227.4 4-DIMM fallback applies; FC-02 row for the new population) | None (board maximum; REV-MEM) | None (board maximum; REV-MEM) | Hosted elasticity for data; local as M-A |
| Trade-off recorded | Smallest justified start (§158, §238); Data working set capped at 32 GB until re-balanced or expanded | Buys capacity the model may not demonstrate; single matched kit (§227.4); 4-DIMM training risk flagged by the seed | Two kits are not "a single matched kit" (§227.4): stability must be re-proven | Confidential-processing boundary (§66), EL latency input and SP16 economics (SE11-DEP-08) decide |

Members inside the Build VM (`pool.agents`, `pool.test`) are bounded by `memory.max` ≤ 40 % of the Build VM's *current* allocation and need no separate line.

**Definitions (SE11-DEC-15).** For an allocation α: F(α) = host reserve + WSL cap + Σ statics + Σ dynamic minima; C(α) = host reserve + WSL cap + Σ statics + Σ dynamic maxima; **Req(α) = max(1.25 F(α), C(α) + H_min)**, H_min = 8 GB. α is admissible on candidate X iff Req(α) ≤ Installed(X). **Floors are fixed inputs**: the host reserve, WSL cap, every static line and every dynamic minimum are workload-derived (or, before measurement, the table defaults) and are never lowered inside the procedure. The only legal moves inside Step 1 are: (i) *raise* a static line or a dynamic minimum to meet a measured demand; (ii) *lower* a dynamic maximum down to, but not below, its minimum. A floor is changed only by a **floor revision**: a measured p95 for that pool recorded as SE11-DEC-03a in the sizing document, after which the whole procedure re-runs from Step 0. Candidate order: M-A (128) < M-A+ = M-B (256); M-A+ is used when M-A is already installed, M-B when 256 GB is required before anything is installed. M-C is not a size but a placement alternative evaluated at Step 2.

**Procedure (deterministic; every step's outcome is recorded in SE11-DEC-03a).**

- **Step 0 — inputs.** SE11-HARDWARE-CAPACITY-SIZING produces, from a traceable Stage-1 concurrent workload inventory (the inputs EL-ENGINEER-ESTIMATE-CAPACITY and SE01 own, SE11-DEP-03), the per-pool demands; the measured host root reserve replaces the 12/16 GB planning value (ASM-SE11-11). Statics and minima are raised to meet demands (move i). Compute F, C, Req for the installed (or default) candidate. If Req ≤ Installed: **admitted**, stop.
- **Step 1 — reallocate within the installed candidate.** Because F does not depend on maxima, Step 1 can succeed **only if 1.25 F ≤ Installed**. If so, set the dynamic maxima deterministically: slack S = Installed − H_min − F; give each dynamic pool a span min(S × its default-span share, its default span), where the default spans are the table's (max − min) values (M-A: Validation 12, Build 12 → equal shares); any remaining S stays as headroom. Then Req = max(1.25 F, F + Σ spans + H_min) ≤ Installed by construction: **admitted**, stop. If 1.25 F > Installed, Step 1 **fails** (recorded) — no reallocation of maxima can fix a floor failure.
- **Step 2 — hosted placement of the oversized component (M-C).** Permitted by §238 and §160. Recompute F, C, Req with that pool's static line = 0. Admissible unless a recorded reason blocks it: the confidential-processing boundary (§66) forbids hosting that data; EL's latency requirement for the Core↔Data path is not met by a hosted service; or SP16 economics (SE11-DEP-08) reject it. If admissible and Req ≤ Installed: **admitted as M-C**, stop.
- **Step 3 — next larger candidate.** Only after Steps 1 and 2 have failed for recorded reasons: on 256 GB, recompute with the 256-GB table lines raised to demands and re-run Step 1 there. If Req ≤ 256: **admitted as M-A+ (or M-B)**, with the memory stability pass re-run (SE11-AC-04) and the FC-02 documentary row for the new population closed first. The record must show the aggregate F/C/Req and both failed steps. **256 GB is never adopted on the strength of this document, nor on the strength of a single component.**
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
- Every data store that holds a local D-IRR class — wherever it runs — implements the mutation-lease rule of §6.3b (SE11-REQ-24); the VM definitions carry no exemption.

### 5.5 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger TRG-GPU (§12.2: local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability — which means that if Fallback A (NIC in PCI_E1, §6.1a) is in use it must first be replaced by Fallback B or C with a passed SE11-AC-12b — plus 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms measured full-load system draw plus 145 W ≤ 80 % of the 750 W PSU rating and that the per-candidate shutdown budgets of §8.3 still hold at the higher PD-A load; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on the client hypervisor (device assignment or partitioning, FC-07) — if none exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as a new SE11-DEC; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator or a dual-slot card is ESCALATE ARCHITECTURE IMPACT (SE11-ADR-04).


## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Authoritative physical mapping of every volume (SE11-DEC-09 / SE11-ADR-09)

This table is the single source of truth for the default mapping (Mapping-D). Sizes are initial allocations (candidate envelope, ASM-SE11-03) and are thin-provisioned so that the sizing document can resize without re-mapping. The alternative Mapping-V of §6.1a swaps the Validation disks and scratch between M2_2 and M2_3; nothing else changes.

| Volume (guest device name) | Pool | Physical device (slot, link) | Initial allocation | Notes |
|---|---|---|---|---|
| Host OS, hypervisor, SE11 host agent store (incarnation record, event log ≤ 1 GB, lease store, bootstrap secret store, local-channel socket), WSL2 distro disk | `pool.admin` | **M2_1** 1 TB (Gen5 x4, CPU) | whole device | T0 system; rebuildable from the version-controlled host build in `REPO-EXT`; encrypted (§13) |
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
| T0 system | M2_1 | Windows + WSL2 + SE11 host agent (§227.5) | Rebuildable from `REPO-EXT`; the host agent's event log, incarnation record and lease store are durable but not unique data (§18.2 recovers from their loss by a new incarnation and fail-safe leases) | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 (Gen4 x2) or `bld-scr` on M2_2 | Build cache / scratch (§227.5) | Disposable | SE11 |
| T1 hot, Highest | M2_4 | Core/Data VMs, platform data, DBs, platform containers | Independent volume; snapshot + replication to T2 | SE12 (data), EL (VM definitions) |
| T1 hot, High/Medium | M2_2 (and M2_3 for Validation under Mapping-V) | Validation/Build VMs, artifact store | Independent volume; archival replication to T2 | SE12 (artifact retention) |
| T2 durable | NAS RAID 6 | Backups, snapshots, release evidence, VM/container archives, artifacts, repository mirrors (§164) | Dual-parity array + snapshots; "not the only backup" (§164) | SE12 |
| T3 isolated copy | Off-site / hosted, encrypted; or T3-SUB isolated local media (§6.3) | "independent/off-site or otherwise isolated copy" for irreplaceable data (§164) | Independent of room, UPS, NAS and host | SE12 (policy), SE17 (keys after takeover), SE11 (bootstrap custody) |

**Scope rule (SE11-REQ-21).** The protection states of §6.3 govern **real D-IRR data stored on local hardware (T1)**. Data whose authoritative copy lives outside the local hardware is outside the local admission scope; its local copies are D-REB. This boundary is what makes the bootstrap non-circular: the first thing the platform needs — its own source, configuration and commissioning evidence — is never local D-IRR data.

**Dataset classes (provisional default, ASM-SE11-08; SE12 is the classification owner, SE11-DEP-04):**

| Class | Definition | Sub-classes and the store that enforces the creation gate and the mutation lease (§6.3, §6.3b) | Minimum protection |
|---|---|---|---|
| D-IRR (local) | Irreplaceable data on local hardware: cannot be re-derived from any other platform data or external authoritative copy | `KEYS` — commissioning secrets (host disk-encryption recovery key, NAS/switch/UPS-software administrative credentials, the Part B/C tokens) and, after takeover, platform key backups; primary T3 target = **T3SUB** during bootstrap. Enforcing store: **SE11's bootstrap store on the host during commissioning; SE17/SE15's store after takeover** (§6.3c). `DB` — non-synthetic platform databases; enforcing store: SE12's data store; primary target T3. `EVID` — release-evidence packages and decision logs produced by EL/SP14; enforcing store: SE12's evidence storage; primary target T3. `LREPO` — a *local* repository server, **not at baseline**; admitted like any class when adopted, and the class into which the T2 mirror is promoted on provider loss (FD-EXT-REPO) | T1 + T2 + T3 under the rules of §6.3–§6.3b |
| D-BND | Bounded loss: re-derivable from D-IRR or from `REPO-EXT` within an accepted window | build artifacts, locally built images, validation results, telemetry history, the SE11 event log | T1 + T2; loss window accepted by SE12 |
| D-REB | Rebuildable from definitions or external authoritative sources | caches, scratch, pulled container layers, VM system disks, **local clones and the T2 mirror of `REPO-EXT`**, **synthetic test fixtures used to verify protection mechanisms** | T1 only (the T2 mirror is itself a rebuildable copy) |
| Outside local scope | `REPO-EXT` — source repositories, IaC, host build, configuration, the version-controlled inventory file, SE11's commissioning and acceptance evidence records: authoritative copy at an **external hosted repository service**, chosen under NT16 (SE11-DEP-09) and configured before any local hardware is commissioned (§160 keeps authoritative source in version control outside any single host) | Durability is the provider's; SE11 bounds provider loss by the T2 mirror (refreshed ≤ 1 h once `PL-T2` holds) and a repository bundle on T3-SUB at every stage gate; on provider loss the mirror is promoted to `LREPO` (§9 FD-EXT-REPO) | provider + T2 mirror + T3-SUB bundle |

### 6.3 Protection states with a legal bootstrap (SE11-REQ-03, SE11-REQ-13, SE11-REQ-17, SE11-REQ-18, SE11-REQ-21, SE11-REQ-24, SE11-DEC-18, SE11-DEC-20, SE11-DEC-23, SE11-DEC-26)

**Three separate things.** *Mechanism readiness* (the T3 copy path, encryption, key recovery and restore for class *c* work) is verified on **synthetic fixtures** (D-REB) — initially before any real dataset of *c* exists (SE11-AC-07b-init) and recurrently at every stage gate while real data exists (SE11-AC-07b-rec; the fixture is a synthetic dataset carried through the same mechanism path, never counted as real data and never able to advance real-data timestamps, guard P1 in §6.3a). *Dataset protection* (a real dataset of *c* has a verified copy no older than A_max) begins when the first real dataset is admitted. *Evidence intake* is how the publisher learns of copies, restores and custody: producers push records under `SE11-CONTRACT-protection-evidence@1` (§18.2 Part C); the absence of evidence is itself the fail-safe (ageing continues), and the **mutation lease** (§6.3b) makes the stores' behaviour independent of the publisher's availability.

**Per-class record (held and published by the SE11 host agent; the authoritative field list).** For each local D-IRR class *c*:

| Field | Meaning | Changed only by |
|---|---|---|
| `store(c)` | Registered producer id of the enforcing store (null until registered) | Host-build registration (§18.2 Part C); `CUSTODY_TRANSFER` |
| `primary_target(c)` | T3 or T3SUB — the target whose verified copies define `t3_last_ok` (KEYS: T3SUB during bootstrap; DB/EVID: T3) | Registration |
| `custody_ready(c)` | KEYS only: KB-2 complete or the takeover store ready | `CUSTODY_READY` |
| `mech_state(c)` ∈ {UNVERIFIED, OK, SUSPECT}; `mech_ok(c)` = ts of the last passed fixture verification | Mechanism readiness | `MECH_FIXTURE_OK` / `MECH_FIXTURE_FAIL` (fixture = true only); a real `RESTORE_OK` clears SUSPECT |
| `real_data(c)` | True once the first real dataset was created | `DATASET_CREATED` (fixture = false); never reset |
| `t3_last_ok(c)` | Timestamp of the newest **verified real copy to the primary target** (`COPY_OK` matched by `RESTORE_OK`), or `t_create` while kind = ANCHOR | `DATASET_CREATED`; matched real `RESTORE_OK` with target = primary; never regresses |
| `t3sub_last_ok(c)` | Timestamp of the newest verified real copy to T3SUB when T3SUB is **not** the primary target (bridging substitute) | Matched real `RESTORE_OK` with target = T3SUB |
| `kind(c)` ∈ {ANCHOR, COPY} | COPY once a verified real copy to the primary target exists | First matched real `RESTORE_OK` to the primary target |
| `rfail(c)` | Count of **consecutive** failed restore verifications of real copies to the primary target | Real `RESTORE_FAIL` (+1); real `RESTORE_OK` (reset to 0) |
| `age(c)` | now − `t3_last_ok(c)` | Tick |
| `A_max`, `G` | 24 h, 24 h (ASM-SE11-10 until SE12 binds them, SE11-DEP-04); a test class may carry shorter values (§14) | Registration |
| `state(c)`, `admit(c)` ∈ {ALLOW, DENY}, `lease(c)` = {`mutate` ∈ {ALLOW, FREEZE}, `until`, `basis`} | Derived by §6.3a and §6.3b | Derivation only |

**States (summary; the transition table of §6.3a governs):**

| State of class c | Definition (P-order of §6.3a) | `admit(c)` | `lease(c).mutate` (ceiling; the store enforces `until − U`, §6.3b) | Mandatory actions / notes |
|---|---|---|---|---|
| MECH-UNVERIFIED | No real data and (mech_state ≠ OK, or `store(c)` null, or custody not ready for KEYS) | DENY — only synthetic fixtures (D-REB) may exist | n/a (no real data) | Commission the T3 mechanism; register the store; run SE11-AC-07b-init on a fixture |
| ARMED | No real data; mech_state = OK within the current stage; `store(c)` registered; custody ready (KEYS) | ALLOW → first real dataset enters PROTECTED(ANCHOR) at `t_create` and the store triggers the initial copy immediately | n/a | Re-verify the fixture at every stage gate; a fixture failure returns the class to MECH-UNVERIFIED |
| PROTECTED | Real data; `rfail` < 2; mech_state ≠ SUSPECT or `rfail` = 0 **and** `age(c)` ≤ A_max. kind = ANCHOR until the first verified real copy to the primary target | ALLOW only if `rfail` = 0 and mech_state = OK; DENY otherwise (a single restore failure or a suspect mechanism blocks new datasets until a real `RESTORE_OK`) | ALLOW with `until` = max(`t3_last_ok` + A_max + G, `t3sub_last_ok` + A_max) | Copy at interval ≤ A_max; `SIG-PROTECTION-STATE` carries state, lease and record |
| DEGRADED-IN-BUDGET | Real data; `rfail` < 2; A_max < `age(c)` ≤ A_max + G | DENY | ALLOW with the same `until` formula (it lies in the future by definition of this state) | Level change published ≤ 60 s; copy retried every 1 h; SE20 prepares a T3-SUB copy so that a verified substitute exists before expiry; exposure window logged |
| EXPIRED | Real data and (`age(c)` > A_max + G **or** `rfail` ≥ 2 — mechanism broken, precedence P2) | DENY | `until` = `t3sub_last_ok` + A_max if a **verified** T3-SUB substitute copy exists and that instant is in the future; otherwise FREEZE (`until` = null). The primary-target term is dropped when `rfail` ≥ 2 | SE20 incident; SE12 decides whether to bridge via T3-SUB or hold the freeze; every hour in EXPIRED is logged against the stage's exposure budget |

**SE11-REQ-03 (state rule).** T0/T1 is never the sole copy of D-IRR or D-BND data beyond the declared windows: every T1 dataset has a T2 copy within the snapshot interval of SE11-NFR-05; every real local D-IRR class is at every moment in exactly one of the states above, and its exposure to total local loss is **bounded** by the state rule: zero beyond `age(c)` when kind = COPY; the whole class when kind = ANCHOR, which can last at most A_max (then DEGRADED) + G (then EXPIRED, freeze or verified T3-SUB bridge). The ANCHOR window is a declared, bounded exposure, not an exception to this requirement. **Mutation exposure is bounded by the lease (§6.3b): no registered store mutates real data of c after `lease.until − U`, whatever the publisher's state.**

**Platform-level derived state (published as `SIG-PL-STATE`; "real D-IRR" means local, per SE11-REQ-21):** `PL-0` = before SE11-AC-07a (only D-REB and synthetic data on local T1; no verified T2); `PL-T2` = SE11-AC-07a passed and no real local D-IRR data exists (classes MECH-UNVERIFIED or ARMED only); `PL-T3-PENDING` = every class with real data is PROTECTED and at least one is ANCHOR; `PL-T3` = every class with real data is PROTECTED with kind COPY; `PL-DEG` = at least one class DEGRADED-IN-BUDGET and none EXPIRED; `PL-EXP` = at least one class EXPIRED.

**Invariants (checked at every step of SE11-AC-07d and by SE11-AC-10).** (I1) A real local D-IRR dataset of class c exists only if c was ARMED at the moment of its creation or c already held real data in PROTECTED with `admit` = ALLOW (creation gate). (I2) In `PL-0` and `PL-T2` no real local D-IRR data exists. (I3) In `PL-DEG`/`PL-EXP` real D-IRR data exists and is exposed to FD-STORAGE/FD-ROOM for at most `age(c)`; the exposure is bounded by A_max + G plus the T3-SUB age. (I4) SE11-AC-10 passes only in `PL-T2` or `PL-T3` (never `PL-T3-PENDING`, `PL-DEG`, `PL-EXP`). (I5) T3-dependent recovery (§6.6) is valid for class c only from a COPY; while kind = ANCHOR a loss of T1 and T2 loses the class entirely, and by the state rule that class is at most A_max + G old. (I6) No real local D-IRR data exists in a class whose enforcing store has no registered producer **with a passed lease-conformance record** — a class whose owner's store does not yet exist, or has not proven lease enforcement, is MECH-UNVERIFIED by definition, so the absence of an owner document can never produce unprotected or unboundedly mutable data. (I7) No network-reachable Part B/C endpoint exists without token authentication, and no token exists that is not a `KEYS` secret with verified custody (bootstrap window rule, §6.3c).

**Class-specific activation.**
- `REPO-EXT` (outside scope): configured in the host build **before** any local hardware is commissioned; the first commit is the host build itself; commissioning evidence, the inventory file and every SE11 acceptance record are committed there and inherit the provider's durability; the T2 mirror and the T3-SUB bundle bound provider loss (§6.2). Nothing here creates local D-IRR data.
- `KEYS`: bootstrap custody and bootstrap authority per §6.3c (KB-1 … KB-5 with the bootstrap channel).
- `DB`, `EVID`: fixture = a synthetic dataset of the class carried through the owner's backup path to T3 and restored (SE11-AC-07b-init); real data admitted from ARMED only, by the owner's store, which must have registered with its SE11-AC-07e lease-conformance record. Until SE12's store exists and registers, the class is MECH-UNVERIFIED and holds no real data (I6).
- `LREPO`: not at baseline; on adoption, fixture = a test repository; on FD-EXT-REPO promotion, the T2 mirror enters PROTECTED(ANCHOR) with `t3_last_ok := last mirror refresh` and must receive a verified T3 copy (T3-SUB bundle or a new external remote) within A_max.

**Outage tolerance.** The tolerance of class c to loss of the T3 path is its **remaining copy-age budget**, `A_max − age(c)` at the moment the outage starts (then G of degraded operation), not a fixed 24 h; mutation continues until `lease.until − U` and no longer.

**Restoration.** T3 path restored → a full copy of class c completes (`COPY_OK`) → restore verification on another machine passes (`RESTORE_OK`, same `copy_id`) → `t3_last_ok(c)` updated, kind COPY, `rfail` := 0, mech_state := OK → PROTECTED; a fresh lease is published within 60 s and the store resumes mutation only on that fresh lease (§6.3b).

**Enforcement and ownership (SE11-REQ-18, SE11-REQ-24, contract-bound).** SE11 publishes the per-class record, state, `admit(c)` and `lease(c)` under `SE11-CONTRACT-hardware-signals@1`, and accepts evidence under `SE11-CONTRACT-protection-evidence@1` (§18.2). The gates are enforced by the store that holds the class, consuming the published levels and applying the lease rule locally: SE11's bootstrap store for `KEYS` during commissioning; SE12's stores for `DB` and `EVID`; SE17/SE15's store for `KEYS` after takeover. SE11 has no hardware-level backstop inside another owner's store and does not claim one; what it guarantees is that **no class can hold real data unless its store has registered as a producer, has proven lease enforcement (SE11-AC-07e record in its registration) and consumes the levels** (I6, SE11-REQ-23 validator, SE11-AC-07d negative checks). The end-to-end bounded-exposure guarantee for class c is therefore stated as: *conditional on store(c)'s registration carrying a passed SE11-AC-07e record for the store build in use* — and because registration without that record is refused, the condition is always either satisfied or the class holds no real data. T3-SUB is an encrypted copy to removable media or a second independent location kept outside the room (§164 "otherwise isolated copy"), restore-verified on a second machine; it is the primary T3 for KEYS during bootstrap and a bridging substitute for DB/EVID.

**Verification.** SE11-AC-07b-init, SE11-AC-07b-rec, SE11-AC-07c (expiry drill), SE11-AC-07d (from-empty-platform trace, §14), SE11-AC-07e (lease enforcement under publisher outage), SE11-AC-07f (transition-table cases), SE11-AC-10 (I4).

### 6.3a Authoritative transition table (SE11-DEC-26; §14 and §18.2 Part C reference this table and define nothing contrary)

**Evaluation order on every record and on every tick (precedence).**

| Step | Rule |
|---|---|
| **P1 — scope and validity guards** (a record failing a guard changes nothing; the outcome is logged and, where stated, rejected to the producer) | (a) `producer_id` not registered, or `class` not owned by it → reject 403. (b) `fixture = true` records may change only `mech_state`/`mech_ok`; they **never** touch `real_data`, `t3_last_ok`, `t3sub_last_ok`, `kind`, `rfail` or the lease. (c) Duplicate (same `producer_id`, `copy_id`, `event`) → ignored (idempotent). (d) `RESTORE_OK`/`RESTORE_FAIL` whose `copy_id` has no prior `COPY_OK` → held for 10 min awaiting the `COPY_OK`, then rejected and logged (out-of-order tolerance). (e) A record with `ts` > publisher now + U → rejected (clock). (f) Timestamps never regress: a verified copy older than the current `t3_last_ok`/`t3sub_last_ok` leaves it unchanged. (g) `RESTORE_OK` for a real copy is valid only if `restored_on` ≠ the host that produced the copy (T3SUB: a second machine); otherwise treated as `RESTORE_FAIL` |
| **P2 — mechanism broken** | If `real_data` and `rfail` ≥ 2 → state **EXPIRED** regardless of age; lease primary term dropped (§6.3b) |
| **P3 — age** | If `real_data` and `rfail` < 2: `age` ≤ A_max → PROTECTED; ≤ A_max + G → DEGRADED-IN-BUDGET; else EXPIRED |
| **P4 — no real data** | mech_state = OK and `store` registered (with AC-07e record) and custody ready → ARMED; else MECH-UNVERIFIED |
| **Admit** | ALLOW iff state ∈ {ARMED} or (state = PROTECTED and `rfail` = 0 and mech_state = OK); DENY otherwise |
| **Lease** | Per §6.3b from the record after P1–P4 |

**Transitions (event × current situation → record change → resulting state by P2–P4).**

| Event (Part C) | `fixture` | Situation | Record change | Result |
|---|---|---|---|---|
| `MECH_FIXTURE_OK` | true | any | `mech_state` := OK; `mech_ok` := ts | No real data → ARMED if store + custody ready; real data → state by age (a fixture pass **never** changes `t3_last_ok`, so an EXPIRED class stays EXPIRED and its lease is unchanged) |
| `MECH_FIXTURE_FAIL` | true | no real data | `mech_state` := UNVERIFIED | MECH-UNVERIFIED |
| `MECH_FIXTURE_FAIL` | true | real data | `mech_state` := SUSPECT | State by age unchanged; `admit` DENY until a real `RESTORE_OK` or a later `MECH_FIXTURE_OK`; lease unchanged (ageing bounds it) |
| `MECH_FIXTURE_*` | false | any | — | Rejected (a mechanism record must be a fixture) |
| `CUSTODY_READY` | — | KEYS | `custody_ready` := true | ARMED if the other ARMED conditions hold |
| `CUSTODY_TRANSFER` | — | KEYS, both producers registered | `store(KEYS)` := new producer; old producer stays registered until its retirement is committed in the host build | Unchanged state |
| `DATASET_CREATED` | false | ARMED | `real_data` := true; `t3_last_ok` := ts; `kind` := ANCHOR | PROTECTED(ANCHOR) |
| `DATASET_CREATED` | false | PROTECTED, `admit` = ALLOW | — (further datasets inherit the class record) | Unchanged |
| `DATASET_CREATED` | false | any state with `admit` = DENY | — | Rejected 409 and logged as a **store-enforcement violation** (the store must not have created it; SE20 incident; the producer's registration is suspended → class `admit` DENY until re-registered with a fresh SE11-AC-07e record) |
| `COPY_OK` | false | real data | Copy recorded as **pending** (`copy_id`, ts, target); **no timestamp advances** | Unchanged — ageing continues until the matched `RESTORE_OK` |
| `COPY_FAIL` | false | real data | Logged | Unchanged (ageing continues) |
| `RESTORE_OK` | false | matched pending copy, target = `primary_target` | `t3_last_ok` := copy ts (if newer); `kind` := COPY; `rfail` := 0; `mech_state` := OK | State by age; fresh lease |
| `RESTORE_OK` | false | matched pending copy, target = T3SUB ≠ primary | `t3sub_last_ok` := copy ts (if newer) | State unchanged (substitute copies do not change the primary age); lease recomputed (§6.3b) — in EXPIRED this is the only way to re-authorize mutation |
| `RESTORE_FAIL` | false | matched pending copy, target = primary | `rfail` += 1; the copy is discarded (never counted); `admit` DENY; store must start a new copy immediately | `rfail` = 1 → state by age; `rfail` ≥ 2 → EXPIRED (P2) |
| `RESTORE_FAIL` | false | matched pending copy, target = T3SUB ≠ primary | Substitute copy discarded; logged | Unchanged |
| Tick (every ≤ 60 s) | — | real data | `age` recomputed | P2/P3 |
| Producer registration (host build) | — | class c | `store(c)` := id only if the registration carries a passed SE11-AC-07e record id for the store build; otherwise the validator refuses the commit (SE11-REQ-23) | P4 |

**Recovery from a failed restore.** `rfail` = 1: the store starts a new copy at once; `admit` stays DENY and the lease is unchanged (bounded by the previous verified copy); a matched `RESTORE_OK` resets everything. `rfail` ≥ 2: the mechanism is treated as broken — EXPIRED, SE20 incident, lease primary term dropped; return to PROTECTED only by a new `COPY_OK` + matched `RESTORE_OK` to the primary target; meanwhile mutation may continue only on a **verified** T3-SUB substitute copy (`until` = `t3sub_last_ok` + A_max).

### 6.3b Mutation lease — consumer-enforced bounded mutation authorization (SE11-DEC-23, SE11-ADR-16, SE11-REQ-24)

**Why.** `mutate` published as a level could be acted on indefinitely by a store that lost sight of the publisher. The lease makes the authorization **self-expiring in the store** so that the bounded-exposure claims of §6.3 hold whether the publisher is up, down, STALE, restarting or rebuilt.

**Publisher side (derivation, carried in every `SIG-PROTECTION-STATE` level, `HEARTBEAT` and `/levels` snapshot):**

| Field | Value |
|---|---|
| `lease.until` | T_primary = `t3_last_ok` + A_max + G if `rfail` < 2, else −∞; T_sub = `t3sub_last_ok` + A_max if a verified substitute exists, else −∞ (for KEYS, whose primary target is T3SUB, T_sub is not separately used); **`until` = max(T_primary, T_sub)**; `null` if both are −∞ or no real data |
| `lease.mutate` | ALLOW iff `until` is non-null and publisher now < `until`; FREEZE otherwise |
| `lease.basis` | COPY / ANCHOR / T3SUB / none |
| `lease.pub_now` | Publisher's UTC clock at issue |
| `lease.inc`, `lease.seq` | Incarnation and sequence of the issuing event (§18.2 Part B); informational for the store, used in SE11-AC-07e logs |

Invariant: `until` is a pure function of verified evidence timestamps and the class parameters; it is never extended by heartbeats, time, or anything other than a new verified copy.

**Store side (the rule every registered store implements; SE11-REQ-24):**

| # | Rule |
|---|---|
| L1 Persist | The store persists the latest lease it accepted for each class (`lease_c`) together with its own clock at receipt (`t_recv`) and a monotonic high-water mark `hw_time` = max clock value it has ever observed |
| L2 Accept | A lease is accepted only if `|t_recv − lease.pub_now| ≤ U` (U = **300 s**, ASM-SE11-18). A lease failing this check is rejected, logged, and the store treats the class as FREEZE until a lease passes (skew alert to SE20) |
| L3 Mutate | A mutation of real data of class c is permitted **iff** `lease_c.mutate` = ALLOW **and** store clock now < `lease_c.until − U`. Nothing else is consulted: STALE, UNKNOWN, publisher unreachable, host agent restarted — none of these extend or shorten the deadline |
| L4 Startup / restart | On start the store loads `lease_c`; if it exists, passes L5, and now < `until − U`, mutation continues under it; otherwise the class is FREEZE until a fresh lease from the current publisher incarnation is accepted |
| L5 Clock rollback | If store clock now < `hw_time − U`, the store FREEZEs every class and alerts; it resumes only after accepting a fresh lease (whose `pub_now` re-establishes the comparison) and only under that fresh lease |
| L6 Recovery | A class in FREEZE resumes mutation **only** on a fresh accepted lease with `mutate` = ALLOW; never by the passage of time, a clock change, or a stale persisted lease. Because the publisher carries leases in every heartbeat, recovery after an outage takes ≤ H + P = 120 s once the publisher is back and the state permits |
| L7 Creation | `admit` is not leased: a store creates a real dataset only on a current (bootstrapped, non-STALE) `admit` = ALLOW from the publisher (SE11-REQ-22) |
| L8 Evidence | The store build in use has a passed SE11-AC-07e record (publisher-outage expiry test) referenced in its producer registration; the validator refuses registration without it (SE11-REQ-23) |

**Bounded exposure, stated.** For any registered store and any class with real data, the last possible mutation instant is `max(t3_last_ok + A_max + G, t3sub_last_ok + A_max) − U` by the store's own clock (bounded from the publisher's clock by L2/L5 to within U); after that instant the store refuses writes until a new verified copy produces a fresh lease. This holds with the publisher down for any duration.

**Clock uncertainty.** U = 300 s is both the acceptance tolerance (L2) and the safety margin (L3/L5). Stores and the host agent synchronise to the same time source on `seg.mgmt`; a drift beyond U is treated as a fault, not tolerated (SE11-RISK-16).

**Interaction with ANCHOR.** For a class at ANCHOR, `until` = `t_create` + A_max + G: a newly admitted class whose first copy never verifies is frozen in every store 48 h − U after creation, which is the §6.3 exposure bound.

### 6.3c KEYS bootstrap custody and the bootstrap authority (SE11-DEC-18, SE11-DEC-24, SE11-ADR-14, SE11-ADR-17, SE11-REQ-25)

**The circularity to avoid.** Part C requires a per-producer bearer token and Part B a read token; both are `KEYS` secrets; `KEYS` cannot be ARMED before fixture evidence is submitted; and no secret may exist before `admit(KEYS)` = ALLOW. A network-token design therefore cannot reach its first legal secret. The bootstrap authority below replaces network tokens with an OS-authenticated local channel during a bounded window and then revokes it.

**Bootstrap window (`bootstrap_window = true` in the host build, committed to `REPO-EXT`).**

| Property | Specification |
|---|---|
| Who | The host agent is one service under a dedicated service account `svc-se11-agent`; the publisher (Part B), the intake (Part C) and the **bootstrap store** are components of that service |
| Channel | Part B and Part C are served **only** on a local channel on M2_1 (named pipe / Unix domain socket) with an OS ACL that admits `svc-se11-agent` only; **no network listener exists** while the window is open (I7) |
| Authentication | OS identity of the caller (ACL); no bearer token; every call logged with caller identity |
| Registration | The bootstrap store's producer registration is static in the host build: `producer_id = se11-bootstrap`, class KEYS, `primary_target = T3SUB`, `auth = local-channel`, `lease_conformance = <SE11-AC-07e record for the host-agent build>` (the test is run on the host-agent build itself, before the window opens, with a test class — it needs no network tokens) |
| Scope | Only `KEYS` can be ARMED or admitted during the window (the validator refuses any other producer registration while `bootstrap_window = true`) |
| Closing condition | `KEYS` is PROTECTED with kind COPY **and** the initial token set has been created, written to both T3-SUB media and read back (KB-3b) |
| Transition | Host build commit flips `bootstrap_window = false`; the host agent restarts (new incarnation, §18.2): network endpoints on `seg.mgmt` with token authentication are enabled; the local channel is **removed** (socket deleted; code path disabled by the flag); the bootstrap store's registration becomes `auth = token TOK-C-boot`. The flag flip is the **revocation** of the bootstrap authority |
| Validator (SE11-REQ-23) | Refuses: a host build with `bootstrap_window = true` while the inventory records any token id or `KEYS` kind = COPY; a producer registration with `auth = local-channel` while the window is closed; any network endpoint configuration while the window is open |

**Custody procedure KB (owned by SE11 so that commissioning needs no absent owner):**

| Step | Action | Channel / credential used | Record and state |
|---|---|---|---|
| KB-1 | Prepare two T3-SUB media (removable, encrypted under an operator-held passphrase never stored on the platform, ASM-SE11-17); store them outside the room | none | — |
| KB-2 | Fixture verification: a test secret written to both media, read back on a second machine, checksum-compared; `MECH_FIXTURE_OK` (fixture = true) and `CUSTODY_READY` submitted by the bootstrap store | local channel (OS ACL) | `mech_state(KEYS)` = OK, custody ready, store registered → **ARMED** |
| KB-3a | First real secret: the bootstrap store reads `admit(KEYS)` = ALLOW (local channel), generates the host disk-encryption recovery key, writes it to both media, reads back on the second machine, submits `DATASET_CREATED` then `COPY_OK target=T3SUB` + `RESTORE_OK` (same `copy_id`, `restored_on` = second machine) | local channel | PROTECTED(ANCHOR) → PROTECTED(COPY); disk encryption is enabled only after this |
| KB-3b | Initial token set, each generated → both media → read-back → `COPY_OK`/`RESTORE_OK` before use: `TOK-B-read` (consumer read token for Part B), `TOK-C-boot` (the bootstrap store's own Part C token), `TOK-B-admin` (endpoint administration). No token is used for anything until its custody evidence is accepted | local channel | KEYS COPY (n secrets); closing condition met |
| KB-3c | **Transition**: commit `bootstrap_window = false`; host agent restart; from here every Part B/C call is a network call on `seg.mgmt` with a token | token auth from this step on; local channel gone | New incarnation; INIT re-derives KEYS = PROTECTED(COPY) from persisted evidence; leases re-issued |
| KB-3d | NAS, switch and UPS-software default credentials rotated; each new credential enters KEYS through the same create → media → read-back → evidence path | `TOK-C-boot` over the network endpoint | KEYS COPY |
| KB-4 | Recurring: SE11-AC-07b-rec at every stage gate with a fresh test secret (fixture = true; cannot advance real timestamps, §6.3a P1b) | `TOK-C-boot` | `mech_ok` refreshed |
| KB-5 | Takeover: SE17/SE15 register their store as a second producer for KEYS (with its own SE11-AC-07e record and token, issued through KB-3d's path), import the secrets, copy them to their T3 path with `COPY_OK`/`RESTORE_OK`, submit `CUSTODY_TRANSFER`; only then is `se11-bootstrap` retired by a host-build commit | `TOK-C-boot` (old), new store token | KEYS stays PROTECTED throughout; `primary_target` may change to T3 at transfer |

**Unauthorized bootstrap attempts (tested in SE11-AC-07d step 9):** during the window, a network call to Part B/C fails (no listener); a local call from any OS identity other than `svc-se11-agent` is refused by the ACL and logged; after the window, a call on the local channel fails (socket absent) and a host build attempting to re-open the window with existing tokens is refused by the validator. Re-opening the window is possible only on a **rebuilt** host with an empty inventory (no token ids, KEYS re-derived as MECH-UNVERIFIED), which is the FD-NVME-M2_1 / FD-HOST rebuild path: the secrets still exist on the T3-SUB media; the rebuilt agent imports them through KB-3a/3b again with new tokens.

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
| M2_1 failure (host OS, host agent store) | All VMs stop until the host OS is rebuilt from `REPO-EXT` onto a replacement device; VM disks on M2_2/M2_4 remain intact; the host agent restarts as a **new incarnation** (§18.2) and re-derives protection levels from the evidence held in `REPO-EXT`/T2 (fail-safe: unknown → `admit` DENY and lease FREEZE until evidence is re-ingested); stores continue under their persisted leases until `until − U` (§6.3b L4) and resume on fresh leases; KEYS tokens re-imported from T3-SUB through the rebuild path of §6.3c | Spare NVMe; host build definition in `REPO-EXT`; T3-SUB media |
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
| L2 management/upstream | 5 GbE onboard, Cat6a | Host onboard LAN ↔ switch | Host/VM management, upstream gateway, external-provider traffic incl. `REPO-EXT` and T3; the S-2 NAS UPS-service client path |
| L3 NAS secondary | 10 GbE port 2 (spare), 2×5 GbE | NAS ↔ switch | Expansion: second 10 GbE consumer or link redundancy; 5 GbE for the NAS management segment (carries the N1 wake frame and the S-2 UPS-service traffic) |
| L4 worker links | 1 / 2.5 GbE (deferred) | Local workers ↔ switch access ports | "Worker links may be slower where sufficient" (§166) |
| L5 uplink | per upstream gateway | Switch ↔ gateway | Internet; external AI providers; hosted runners; T3 transfers; `REPO-EXT` |
| Wi-Fi 7 / Bluetooth | — | Host (disabled) | Not part of the architecture; disabled in firmware (§13) |

SE11-REQ-04: L1 sustains ≥ 0.7 GB/s host↔NAS during concurrent build-cache activity, and shared storage or control paths are not the first bottleneck during concurrent transfers (§166) — SE11-NFR-02, verified in SE11-AC-05 for the NIC slot actually in use (Fallback C is admissible only if this passes).

### 7.2 Switching / core role

The switch (B17 class) is the single core: managed, VLAN-capable, at least 2×10 GbE (seed minimum, §230) with ≥ 4×10 GbE preferred so that host, NAS primary, NAS secondary and one future 10 GbE consumer fit without replacement (SE11-ADR-07); 24 access ports at ≥ 1 GbE for workers, management devices and the gateway. It is adopted ahead of the rack (conflict C4) because the management segment and VLAN enforcement need it. Until the switch is installed, an interim point-to-point 10 GbE link host↔NAS with L2 to the gateway is acceptable *placement* — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2); in that interim the S-1 NAS shutdown command, the S-2 UPS-service traffic and the N1 wake frame run over the point-to-point link, which removes the switch from the shutdown and restart paths. Power: the switch is on PD-A (conflict C1; §165 names "critical network components" among the PC+NAS UPS loads) — which is also what keeps N1 and the S-2 client path deliverable while UPS-A output is live (§8.3a).

### 7.3 Segmentation (SE11 designs the physical segments, VLAN membership and addressing; SE17 owns the security policy applied between them, SE11-DEP-05; SE14 is consulted for portable naming)

| Segment | Members | Purpose | Policy owner |
|---|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS software endpoint, SE11 Part B/C endpoint (after the bootstrap window, §6.3c) | Administrative plane; MFA-protected access (§59); no workload traffic; carries the S-1/S-2 shutdown signalling, the N1 wake frames and the evidence-intake calls | SE17 (SE11-SECREQ-03) |
| `seg.storage` | Host 10 GbE, NAS 10 GbE | Backup/artifact/mirror traffic only; not routed to workers | SE17 |
| `seg.platform` | Core VM, Data VM, runtime namespaces | Stable runtime east-west | SE17 |
| `seg.build` | Build VM, Validation VM, member containers | Build/test east-west; fault injection confined here | SE17 |
| `seg.worker` | Local workers (deferred), hosted-runner VPN/egress | Disposable execution | SE17 |
| `seg.egress` | Gateway-facing | Default-deny disclosure gateway for external model inputs (§66, §185) sits on this boundary; `REPO-EXT` and T3 egress are explicit allow-list flows | SE17 / EL |

### 7.4 East-west traffic and bottleneck avoidance

- Build artifacts move Build VM → artifact store (same device, M2_2) over the host-internal virtual switch; only archival copies cross L1 to the NAS, scheduled by SE20 outside peak build windows.
- Database backups cross L1 off-peak; restore drills (§14) measure actual throughput to replace §6.4 assumptions.
- Worker-to-core control traffic is small; worker artifact pulls are served from the host artifact store, not the NAS.
- Management (`seg.mgmt`) and storage (`seg.storage`) traffic never share a VLAN; the NAS shutdown command, the N1 frame, the UPS-service traffic and evidence intake are management-plane flows.

### 7.5 Expansion ports / headroom

Free after baseline: NAS 1×10 GbE + 2×5 GbE; host 2×USB4 (emergency 10 GbE/NVMe adapters); switch access ports per §7.2. Triggers in §12.2.


## 8. Physical power / placement architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

### 8.1 Power domains

| Domain | UPS | Circuit (requirement, not design) | Loads | Status |
|---|---|---|---|---|
| PD-A | UPS-A, class B15 (1500 VA / 1000 W, pure sine, line-interactive AVR, 6 battery outlets, USB HID) | Circuit A: separate 15 A breaker; UPS plugged directly into wall (§231) | Central host, switch; NAS in S-1/S-2 | ADOPT WITH ENGINEERING CONSTRAINT |
| PD-N | UPS-N, class B16 (≥ 1000 VA / 600 W pure sine, USB HID) — **only under candidate S-3** | Circuit A or B as the electrician decides under SE11-REQ-10; **the circuit identity is recorded in the fingerprint (`ups_n_circuit`) because it decides N1 admissibility (SE11-REQ-26, §8.3a)** | NAS only | Conditional (SE11-DEC-10) |
| PD-B | UPS-B, class B16 | Circuit B: second separate 15 A breaker (§231) | Rack PDU → local workers (and the switch only under S-3, conflict C1) | DEFER / OPTIONAL with the rack |

Isolation rule (§165): worker/rack power is isolated from the host/NAS UPS so a worker fault or overload cannot drop the durable tier. The upstream gateway is placed on PD-A only if the measured PD-A load leaves the runtime reserve of §8.4 intact; otherwise it is powered separately (its loss during an outage is acceptable: no shutdown or restart sequence depends on it — N1 frames and UPS-service traffic are switched locally).

### 8.2 Device power envelopes and circuit/load assumptions

| Device | Envelope used for planning | Source / assumption |
|---|---|---|
| Central host, no GPU | ~350–480 W peak at wall (CPU package ≤ 230 W + board/memory/4×NVMe/fans/NIC + PSU losses); host-only idle/boot ~100–150 W | B1, B7; ASM-SE11-05, replaced by SE11-AC-06 measurement |
| Central host, with GPU | +145 W → ~500–630 W peak | B11 |
| NAS, 4–6 HDD + 2 M.2 | ~70–150 W (spin-up transient higher) | B12/B14 class; ASM-SE11-05 |
| Switch (+ gateway if on PD-A) | ~30–80 W | class estimate, ASM-SE11-05 |
| PD-A total | ~450–710 W without GPU; ~600–860 W with GPU (S-1/S-2); ~380–560 W / ~530–710 W under S-3 (NAS on PD-N) — below the 1000 W rating, but battery runtime at these loads is minutes: UPS-A is a controlled-shutdown device, not a ride-through supply (§165) | SE11-AC-06 verifies |
| Whole installation | Seed figures: typical ~560 W, sustained peak ~1,150–1,300 W when the rack is present (§231) | Circuit-sizing input for the electrician |

SE11-REQ-10 (qualified-professional requirement; code-regulated work is not designed here): a licensed electrician verifies that circuits A and B are separate branch circuits of adequate rating for the measured/peak loads above, that receptacles, grounding and surge arrangements meet local code, whether the optional dedicated 20 A circuit (§231) is warranted, and **identifies in the sign-off which branch circuit feeds each UPS receptacle** (consumed by SE11-REQ-26); SE11 supplies only the load figures and the two-domain requirement.

### 8.3 Safe-shutdown signalling and per-candidate timed sequences (SE11-DEC-07, SE11-DEC-10)

**Signalling topology — gated decision (SE11-DEC-10, conflict C3).** The corpus names two integration surfaces: "automatic graceful shutdown via PowerPanel / NAS UPS service" on the UPS (§229.1) and "UPS support / network UPS server" on the NAS (§228.1). It does **not** establish any protocol/client/version combination between them. SE11 records three candidates and a gate:

| Candidate | Topology | Cross-device integration required | Status |
|---|---|---|---|
| S-1 (preferred) | UPS-A USB-HID → central host running the UPS vendor's host shutdown software; the host orchestrates VM shutdown and issues an authenticated remote shutdown command to the NAS over `seg.mgmt` | Host↔UPS: vendor software on the host OS version; host→NAS: a remote shutdown interface supported by the NAS OS | Gated by G1 evidence (dated vendor documentation for both interfaces at the exact versions; FC-09) |
| S-2 | UPS-A USB-HID → NAS as network UPS server; host as network client | NAS server protocol ↔ a host client implementing it; the NAS UPS service able to command the UPS output cycle (FC-09b) — the only restart mechanism S-2 admits (§8.3a); **and** the NAS UPS service starting automatically at NAS boot and serving status to the host client within T_nasboot (FC-09b) — the host's only S5 status source under S-2 (§8.3b-S5) | Gated by G1 evidence (FC-09, FC-09b) and drill (k) |
| S-3 (protocol-agnostic fallback) | Two UPS units, each with its own USB-HID path: UPS-A → host; UPS-N (class B16) → NAS | None across devices for shutdown; for NAS restart: M1-N (FC-09b) or N1 under the same-circuit condition with the NAS-side guard (FC-09c, SE11-REQ-26) | Adopted automatically if neither S-1 nor S-2 produces evidence; recorded as a new SE11-DEC (topology substitution of B15) |

No shutdown sequence is relied on until the selected candidate × mechanism combination is admissible (§8.3a), its restart eligibility is defined for its topology (§8.3b-S5) and it has passed SE11-AC-06, SE11-AC-14 and SE11-AC-15.

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
| 0 | NAS enters its own S2: waits for the host's "client shutdown complete" message for at most W_nas_client = 240 s | Host sequence identical to S-1 rows 0–210 (Build‖Validation 0–60, Core 60–120, Data 120–210) |
| 210 | — | Host sends "client shutdown complete" to the NAS, starts host OS shutdown (no M3 arming: inadmissible under S-2, §8.3a) |
| 240 | W_nas_client elapses (host confirmation arrived at 210; if it never arrives the NAS proceeds anyway) → NAS issues M1 (D_off = 180 s) → NAS shutdown ≤ 120 s | Host off by 270 |
| 360 | NAS off (**UPS-A critical path 360 s**) | — |
| 420 | (M1) UPS-A outputs drop: 60 s after the last device off | — |

**B_A(S-2) = 60 + 360 + 30 = 450 s** → **R_A ≥ 643 s (10.7 min)**. If the NAS OS cannot wait ≥ 240 s for the client, or cannot command the UPS output cycle (FC-09b), S-2 is not admissible — a G1 check.

**Candidate S-3 — two independent sequences:**

| UPS | Sequence | Critical path | Budget | Required runtime | M1 command / output drop |
|---|---|---|---|---|---|
| UPS-A (host + switch) | As S-1 host path without the NAS command: Build‖Validation 0–60, Core 60–120, Data 120–210, M1/M3 + host shutdown 210–270 | 270 s | **B_A(S-3) = 60 + 270 + 30 = 360 s** | **R_A ≥ 515 s** at PD-A load (host + switch) | Host commands at 210, D_off = 120 → drop at 330 |
| UPS-N (NAS only) | NAS on-battery at T0 → T_hold 60 s → NAS issues M1-N (if evidenced) → NAS own shutdown ≤ 120 s | 120 s | **B_N = 60 + 120 + 30 = 210 s** | **R_N ≥ 300 s (5 min)** at the measured NAS load — measured separately in SE11-AC-06 | NAS commands at 60, D_off = 180 → drop at 240 |

The NAS shutting down before the host is harmless: no shutdown step of the host depends on the NAS, and in-flight backup jobs are resumable (§175). Restart ordering (NAS reachable before the Data services start) is handled in S6 (§8.3b).

**State machine (all candidates; the timed sequences above are the content of S2/S3; S5 eligibility is per topology, §8.3b-S5):**

| State | Entry event | Actions | Bounded exit |
|---|---|---|---|
| S0 ONLINE | mains and UPS communication healthy | normal operation; UPS telemetry sampled ≤ 60 s | — |
| S1 ON-BATTERY (hold) | E1 mains loss at T0 | publish `SIG-ONBATTERY` (the scheduler may stop admitting `pool.build`/`pool.background` work — EL/SE01 policy, SE11-DEC-11; nothing below depends on it); alert SE20 | E2 mains restored before T0 + T_hold → S0 and `SIG-ONBATTERY` cleared; else E3 → S2 |
| S2 SHUTDOWN-INITIATED | E3: T0 + T_hold elapsed, **or** UPS low-battery, **or** UPS runtime estimate < B_u for that UPS, **or** E4 UPS-communication loss while in S1 (fail-safe: proceed) | the candidate's timed sequence; **never aborted** | → S3 within the candidate's host critical path (270 s) |
| S3 HOST-OFF | host power off | NAS completes its own path (S-1: off by t = 150, already done; S-2: off by t = 360; S-3: independent) | → S4 |
| S4 ALL-OFF | all devices halted; UPS output may still be live if mains returned during S2/S3 | M1: outputs drop at the commanded time and re-energise on mains; M3: the wake-poll loop runs; otherwise attended | → S5 |
| S5 RESTART-PENDING | E5: AC applied to the devices (exhaustion-and-return, or M1's output cycle), **or** an M3 wake that finds mains online | Host boots HOST-ONLY (no VM auto-start, no N1) and establishes **mains online, charge ≥ 50 % and estimated runtime ≥ B_u / 0.7** through the **status source its topology defines (§8.3b-S5)**: direct UPS-A link (S-1, S-3) or the NAS UPS service (S-2). T_hold = 0 so that a second mains loss triggers an immediate host-only shutdown (B_hostonly = 0 + 60 + 30 = 90 s, needing R ≥ 130 s). Time spent waiting for charge is logged as *charge-limited restart* and excluded from T_restart; time spent in HOST-ONLY-HOLD (S-2 status source unavailable) is logged as **restart exposure**, not excluded | → S6 when the conditions hold; S-2: → HOST-ONLY-HOLD after W_s2 without status |
| S6 RESTARTED | charge and runtime conditions met | the S6 ladder of §8.3b (N1 if the NAS is unreachable and N1 is admissible for the topology; Data VM; NAS-wait cap; Core; Validation; Build); unclean VMs run integrity checks first; protection levels and leases re-published; SE20 post-event check of backups, telemetry and protection states | → S0 |

### 8.3a Admissibility matrix: signalling candidate × restart mechanism (SE11-DEC-19, SE11-DEC-25, SE11-ADR-13)

**Wake rule R-WAKE (the rule the matrix is derived from).** After S3, a device may be powered or woken only by (a) an AC-input cycle at its own input (exhaustion-and-return, or an M1 output cycle), or (b) a command issued by a device that has itself confirmed *mains online for the woken device's power domain* within T_decide of issuing the command. No device is woken on an unknown or on-battery power state. Consequences: under S-2 the only device with a direct UPS link is the NAS, and the NAS is off after its own shutdown; the host therefore cannot satisfy (b), and waking the NAS to ask it would violate R-WAKE — **S-2 admits only M1**. Under S-3 the host's UPS-A link confirms mains on **circuit A only**; it can satisfy (b) for the NAS only if UPS-N is fed from the same branch circuit (SE11-REQ-26); on a different circuit the NAS restarts only by M1-N (its own AC cycle, tracking UPS-N's own mains).

| Candidate | Host restart | NAS restart | Admissible combination | Inadmissible (recorded as FD-RESTART exposure, SE11-RISK-12, if no admissible combination is evidenced) |
|---|---|---|---|---|
| S-1 (UPS-A link at host) | M1 (host commands UPS-A) or M3 (RTC wake; host reads UPS-A directly) | under M1: AC cycle (same UPS-A output) + NAS firmware AC-recovery; under M3: **N1** (Wake-on-LAN sent by the host at S6 entry, NAS on the live UPS-A output — same UPS, same mains) | **S-1/M1**; **S-1/M3+N1** | S-1/M3 without evidenced N1 (NAS attended); M4 |
| S-2 (UPS-A link at NAS) | M1 only, commanded by the NAS UPS service (FC-09b) — AC cycle + host firmware AC-recovery; host S5 status via the NAS UPS service (§8.3b-S5) | M1 (same output cycle) | **S-2/M1** (with FC-09b incl. UPS-service autostart, and drill (k) passed) | **S-2/M3 (any variant)** — violates R-WAKE; refused by the configuration validator (SE11-AC-15 drill (g)); S-2 without FC-09b evidence → S-2 itself inadmissible → S-3 |
| S-3 (UPS-A at host, UPS-N at NAS) | M1 or M3 (host reads UPS-A directly) | **M1-N** (NAS commands UPS-N output cycle, FC-09b; UPS-N re-energises on *its own* mains — independent of UPS-A and of the host) **or N1** — only if `ups_n_circuit = A` (SE11-REQ-26) **and** the NAS-side guard is evidenced (FC-09c: after a wake the NAS reads UPS-N and, if on-battery or unreadable, shuts itself down immediately) | **S-3/{M1 or M3}/M1-N**; **S-3/{M1 or M3}/N1 (same circuit + guard)** | S-3/N1 with `ups_n_circuit ≠ A` or unknown, or without FC-09c — refused by the validator; NAS attended; M4 |

Rules: **if M1 is evidenced it is mandatory** for the device that owns the UPS link; M3 is used only where M1 is not; M4 is never a pass for SE11-REQ-15. The selected combination, the S5 status source and `ups_n_circuit` are recorded in the configuration fingerprint and validated against this matrix by the version-controlled configuration validator; an inadmissible combination cannot be committed.

### 8.3b Restart mechanisms, per-topology restart eligibility and end-to-end timing to service readiness (SE11-REQ-15, SE11-REQ-20, SE11-REQ-26, SE11-DEC-13, SE11-DEC-17, SE11-DEC-25)

Firmware AC-recovery settings act only when the device's AC input is actually removed and restored. If mains returns while the UPS output stays live (during S2, S3 or S4), nothing in firmware re-powers a halted device. One admissible combination of §8.3a must be commissioned. Timing constants (ASM-SE11-13, ASM-SE11-15, ASM-SE11-19; replaced by SE11-AC-15 measurements): T_boot = 120 s (AC applied or RTC wake → host UPS software able to read UPS state through a direct link), T_decide = 30 s, T_hostonly_off = 90 s, W = 300 s (wake-poll period), D_on = 60 s (UPS output restart delay once mains is present and outputs are off), T_nasboot = 180 s (AC applied or WoL → NAS shares and UPS service reachable), W_nas = 300 s (Data-services wait cap for NAS reachability), **W_s2 = 600 s** (S-2 host wait for the NAS UPS service after host boot), T_ladder = 180 s (Core → Validation → Build at 60 s steps after Data services are up), T_fsck ≤ 600 s (bounded filesystem check of an unclean VM, run in parallel across VMs).

| Mechanism | How it works | Covers | Gate |
|---|---|---|---|
| **M1 — commanded output power-cycle (mandatory if evidenced)** | The device that owns the UPS link (host in S-1/S-3; NAS in S-2 and for UPS-N in S-3) commands: "turn outputs off after D_off; restart outputs when mains is present (and battery ≥ the UPS's restart threshold)". **D_off = (worst-case last-device-off time on that UPS − command time) + 60 s guard**, per candidate: S-1 120 s (drop at 330), S-2 180 s (drop at 420), S-3 UPS-A 120 s (330) / UPS-N 180 s (240). Every device thus sees a real AC loss; when mains is already back the UPS re-energises after D_on and firmware AC-recovery fires on host and NAS → S5. The re-energise is itself evidence that the UPS saw mains at that instant | Restoration at any time during S2/S3/S4, and the exhaustion case | G1: dated vendor evidence that the UPS class and the commanding software support commanded output shutdown with auto-restart (FC-09/FC-09b); SE11-AC-15 drills |
| **M3 — wake-poll loop (alternative where M1 is not evidenced; host with a direct UPS link only)** | At the host OS shutdown command in S2 (t = 210), and again at **every** subsequent host-only shutdown while the UPS reports on-battery or unknown, the host arms a firmware RTC alarm at now + W. On wake the host boots HOST-ONLY, reads UPS-A directly within T_boot + T_decide: *mains online* → S5 (charge rule) → S6, and at S6 entry the host sends N1 to the NAS if it is unreachable and N1 is admissible; *on-battery or unknown (E4)* → host-only shutdown (T_hostonly_off) and **re-arm**. The loop ends only when a wake finds mains online or the UPS exhausts; after exhaustion the AC-input-cycle path restarts host and NAS when mains returns. **No attempt cap.** Cost: each cycle draws host-only power for ≈ 240 s per 540 s, accelerating exhaustion (SE11-RISK-14); accepted because after S3 no workload runs and no unflushed data exists | Host restoration at any time; NAS via N1 while the UPS output is live, via AC cycle after exhaustion | G1: RTC wake from soft-off on the board class; N1 (WoL from soft-off) on the NAS class and forwarding by the switch class (FC-09); SE11-AC-15 drills |
| **N1 — NAS wake by the host** | Wake-on-LAN frame from the host agent to the NAS on `seg.mgmt` (or the point-to-point link), sent only at S6 entry (mains confirmed for the NAS's power domain, R-WAKE (b)); repeated every 30 s until the NAS is reachable or W_nas elapses; no further N1 without a new S6 entry | NAS restart under S-1/M3 and S-3 (same circuit + guard) | G1 (FC-09; FC-09c for S-3); SE11-AC-15 drills (f), (h), (m) |
| **M1-N — NAS-commanded output cycle of UPS-N (S-3 only)** | As M1, issued by the NAS UPS service for its own UPS; UPS-N restarts its outputs when **its own** mains is present; the NAS boots by AC-recovery and (where FC-09b evidences it) holds its services until UPS-N charge ≥ 50 % | NAS restart under S-3, independent of UPS-A and of the host | G1 (FC-09b) |
| **M4 — attended restart (residual)** | No automatic restart; SE20 is alerted and an operator powers the devices on | Everything, with human latency | **Never a pass** for SE11-REQ-15; recorded as FD-RESTART exposure (SE11-RISK-12); REV-POWER if an SLO (§117) requires unattended restart |

**§8.3b-S5 — restart eligibility and status ownership per admitted topology (SE11-DEC-25).**

| Topology / combination | Device | Status source for "mains online, charge ≥ 50 %, runtime ≥ B_u/0.7" | Eligibility rule | Bounded wait and fail-safe outcome |
|---|---|---|---|---|
| S-1/M1, S-1/M3+N1 | Host | Direct UPS-A link (vendor software on the host) | S6 when the three conditions hold; else HOST-ONLY with T_hold = 0 (charge-limited wait, logged) | Unreadable UPS at an M3 wake → treated as on-battery → host-only shutdown and re-arm (§8.3b M3); under M1 an unreadable UPS after AC-recovery → wait up to T_decide + 300 s, then host-only shutdown with the M3 loop armed if evidenced, else HOST-ONLY-HOLD (exposure) |
| S-1 (both) | NAS | None needed: the NAS is on UPS-A; under M1 it boots on the same output cycle; under M3 it is woken by N1 only after the host confirmed UPS-A mains online | — | NAS unreachable at S6 → Data services start at the W_nas cap; backups retry later |
| **S-2/M1** | Host | **The NAS UPS service over `seg.mgmt`** (host = network UPS client). The host has no direct link. Sequence after the M1 output cycle: both devices boot by AC-recovery; the host (T_boot) polls the NAS UPS service every 30 s; the NAS service is expected within T_nasboot (FC-09b autostart) | S6 when the NAS service reports mains online, charge ≥ 50 % and runtime ≥ B_A/0.7 | If no status within **W_s2 = 600 s** after host boot → **HOST-ONLY-HOLD**: no VM start, no N1 (none exists under S-2), alert SE20 within 60 s, keep polling every 30 s indefinitely; leave HOLD only when the NAS service reports the conditions (→ S6) or an on-battery report arrives (→ immediate host-only shutdown, T_hold = 0). A mains loss during HOLD with the NAS service still absent is an **abrupt host-only loss at exhaustion** (no VMs, no unflushed platform data; integrity checks on next boot) — recorded exposure SE11-RISK-17; the re-energise after that exhaustion restarts both devices again by AC-recovery |
| S-2/M1 | NAS | Direct UPS-A link (NAS UPS service) | NAS boots on the output cycle; its own services start per the NAS OS; it serves the host | NAS service failing to start is exactly the host's HOLD case above |
| **S-3/{M1,M3}/M1-N** | Host | Direct UPS-A link | As S-1 | As S-1 |
| S-3/…/M1-N | NAS | Direct UPS-N link; **UPS-N re-energises on its own circuit's mains** (independent of UPS-A); NAS AC-recovery boots it | NAS up when its circuit has mains and UPS-N restarts outputs; where FC-09b evidences a NAS-side charge rule it is applied | If UPS-N's circuit is still out while UPS-A's is back: the host reaches S6 alone; Data services start at the W_nas cap with backups deferred; the NAS joins when its circuit returns — no wake is attempted (none is admissible) |
| **S-3/{M1,M3}/N1** (only with `ups_n_circuit = A` and FC-09c) | Host | Direct UPS-A link — which confirms mains for circuit A, the circuit feeding UPS-N | S6 as S-1; N1 sent at S6 entry | — |
| S-3/…/N1 | NAS | **NAS-side guard**: after the wake the NAS UPS service reads UPS-N; mains online → services start; on-battery or unreadable → immediate own shutdown (no T_hold; B_N − 60 = 150 s) | Eligibility is UPS-N's own state, read by the NAS, not inferred by the host | Host stops repeating N1 after W_nas; if the NAS shut itself down, the host's Data services run without backups (deferred) until the next S6 entry or an operator action; the case is a recorded exposure in the drill log (m) |

**S6 ladder (service readiness).** At S6 entry (t_S6): (1) if the NAS is unreachable and N1 is admissible for the topology, send N1 (under M1/M1-N the NAS is already powering up on its own output cycle); (2) start the Data VM at t_S6 + 0; its filesystem check runs first if it was force-stopped (≤ T_fsck); its services start when the NAS is reachable **or** W_nas = 300 s has elapsed since t_S6 (then backups retry later); (3) start Core when Data services are up; Validation 60 s after Core; Build 60 s after Validation (T_ladder = 180 s); (4) the host agent re-publishes every protection level and lease from the last evidence (§18.2 INIT) and `SIG-RESTART` with the measured times. **Service readiness** = every VM running, Data services started, protection levels re-published.

**End-to-end timing budget (SE11-REQ-20; mains restoration → S6 entry = T_restart; → service readiness = T_service; given charge ≥ 50 % at restoration, otherwise charge-limited and logged; HOST-ONLY-HOLD is excluded from no bound — it is a logged exposure):**

| Scenario | M1 (S-1; S-3 host) | **M1 (S-2; status via NAS UPS service)** | M3 (S-1 host, S-3 host) |
|---|---|---|---|
| (a) Restoration at S2 entry (t = 0; worst case for T_restart) | drop 330 + D_on 60 + T_boot 120 + T_decide 30 = **540 s** | drop 420 + D_on 60 + **max(T_boot 120, T_nasboot 180)** + T_decide 30 = **690 s** | alarm armed at 210 fires at 510 + 120 + 30 = **660 s** |
| (b) Restoration after outputs are off (M1) / immediately after an unsuccessful on-battery wake decision with output still energised (M3) | D_on 60 + 120 + 30 = 210 s | 60 + 180 + 30 = **270 s** | host-only shutdown 90 + re-armed W 300 + 120 + 30 = **540 s** worst |
| (c) Restoration during a host-only boot | n/a | n/a | ≤ T_boot + T_decide = 150 s |
| (d) Restoration after UPS exhaustion | UPS restart on mains (class threshold) + 120 + 30 | UPS restart on mains + 180 + 30 | same as M1 (AC-cycle path) |
| **T_restart bound** | **≤ 720 s (12 min)** for every scenario of every admissible combination; S-2/M1 worst case 690 s | | |
| NAS availability relative to t_S6 | NAS AC applied at the same output restart; up by D_on + T_nasboot = 240 s after mains ≈ t_S6 + 30 s → wait ≈ 30 s | NAS already up (it supplied the status) → wait 0 s | N1 at t_S6 → NAS up by t_S6 + T_nasboot = +180 s ≤ W_nas |
| S-3 NAS (M1-N) relative to t_S6 | NAS drop at 240 + D_on 60 + T_nasboot 180 = 480 s after mains on **its** circuit → before t_S6 = 540 when both circuits return together; otherwise W_nas cap applies | n/a | same |
| **T_service_clean** (all VMs stopped gracefully) = T_restart + max(NAS wait, Data VM boot; cap 300) + T_ladder | 540 + 300 + 180 = **1,020 s** | 690 + 300 + 180 = **1,170 s** | 660 + 300 + 180 = **1,140 s** |
| **Bound T_service_clean** | **≤ 1,200 s (20 min)** | | |
| **T_service_forced** (any VM force-stopped; filesystem checks ≤ T_fsck in parallel, the Data VM's check gates the ladder) = T_service_clean + T_fsck | 1,620 s | **1,770 s** | 1,740 s |
| **Bound T_service_forced** | **≤ 1,800 s (30 min)**, excluding database crash recovery, which SE12 bounds and SE11-AC-15 drill (i) measures and records | | |

Where the NAS wait is shorter than the cap (the usual case), T_service is correspondingly shorter; the bounds use the cap. **S-2/M1 has 30 s of margin on each bound**; if SE11-AC-15 measures T_nasboot > 210 s or T_fsck > 630 s, S-2 fails its bounds and the §8.4 remedies apply (candidate change to S-3 is remedy 3).

**Communication-loss handling (E4).** Loss of host↔UPS communication (direct link, or the S-2 client path) while in S0: alert; if it persists > 300 s the UPS protection is declared degraded (SE20 ticket, no workload change). If mains then fails while communication is still lost, the host has no event and the outcome is an **abrupt loss** (handled as FD-UPS-A, §9) — this residual is accepted and tested (SE11-AC-14). Loss of the NAS command path (switch or NAS unreachable) in S-1 S2: proceed; the NAS stops uncontrolled at UPS exhaustion — accepted residual with CoW crash-consistency and a mandatory scrub on restart (SE11-NFR-07). At an M3 wake, an unreadable UPS is treated as on-battery (shutdown and re-arm); this is safe only because M3 is admissible solely for a host with a direct UPS link (§8.3a).

**Shutdown budget rule (SE11-REQ-06, SE11-NFR-03).** For every UPS u of the selected candidate: B_u ≤ 0.7 × R_u, where R_u is the measured runtime at the measured load of that UPS's domain. Default budgets: S-1 B_A = 360 s; S-2 B_A = 450 s; S-3 B_A = 360 s and B_N = 210 s. The 30 % reserve is held *against measured runtime*, not against the low-battery signal; the low-battery signal and the runtime estimate are additional triggers only.

### 8.4 Fail-closed commissioning outcome

SE11-AC-06 **fails** if, for any UPS of the selected candidate, R_u < B_u / 0.7 at the measured load, or if any step exceeds its bound in the drill, or if no admissible combination of §8.3a meets T_restart ≤ 720 s and T_service_clean ≤ 1,200 s in SE11-AC-15 (M4 is a fail for any baseline whose SLO requires unattended recovery; an inadmissible combination is a fail by construction; HOST-ONLY-HOLD reached in drill (k) is a recorded exposure, and if the NAS UPS service cannot be made to autostart it is a fail of S-2). Ordered remedies, each recorded as an SE11-DEC when applied: (1) remove non-essential loads from PD-A (gateway first; the switch stays while the S-1 command path, the S-2 client path or N1 needs it); (2) shorten VM stop timeouts only with SE11-AC-13 evidence that clean stops complete within the shorter bound; (3) change candidate (S-2 → S-3 shortens B_A from 450 s to 360 s, moves the NAS load off UPS-A, gives the host a direct status source and makes M3 admissible for the host); (4) substitute UPS-A by a higher-runtime unit of the same specification class (§11.4); (5) if none suffices, REV-POWER (§12.3). Until SE11-AC-06 passes, no stable-runtime stage baseline is accepted on this hardware (§154 evidence progression) and the platform stays in `PL-T2` at most (§6.3).

### 8.5 Placement constraints (rack / desk / room)

- Central host: tower chassis free-standing with unobstructed mesh-front intake and rear exhaust, off the floor, on PD-A; not inside the 18U rack (rack is for workers/switch/PDU per §230).
- NAS: adjacent to the host, on PD-A (S-1/S-2) or PD-N (S-3), within Cat6a reach of the switch; 3.5-inch drives are vibration-sensitive — solid surface, never stacked on the host.
- Switch: rack-mounted when the rack exists; until then shelf-mounted next to the NAS on a PD-A battery-backed outlet.
- Rack (deferred): 18U; 17U used with a gap after every device or 12U without gaps for micro trays (§230); 1U switch, 1U PDU, 1U power-brick shelf, trays sized to the selected worker form factor; PD-B feeds the PDU.
- Room: lockable (§13), ambient within device operating ranges, no shared circuit with high-draw appliances (requirement to the electrician under SE11-REQ-10); the T3-SUB media (KEYS bootstrap custody, bridging copies, repository bundle) are stored outside this room (§6.3c); thermal and rack layout detail belongs to SE11-POWER-COOLING-RACK.

