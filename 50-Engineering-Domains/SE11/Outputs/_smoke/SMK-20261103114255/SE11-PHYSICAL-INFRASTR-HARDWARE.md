---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 4
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-REQ-13, SE11-REQ-14, SE11-REQ-15, SE11-REQ-16, SE11-REQ-17, SE11-REQ-18, SE11-REQ-19, SE11-REQ-20, SE11-NFR-01, SE11-NFR-02, SE11-NFR-03, SE11-NFR-04, SE11-NFR-05, SE11-NFR-06, SE11-NFR-07, SE11-NFR-08, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-DEC-09, SE11-DEC-10, SE11-DEC-11, SE11-DEC-12, SE11-DEC-13, SE11-DEC-14, SE11-DEC-15, SE11-DEC-16, SE11-DEC-17, SE11-DEC-18, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-ADR-08, SE11-ADR-09, SE11-ADR-10, SE11-ADR-11, SE11-ADR-12, SE11-SECREQ-01, SE11-SECREQ-02, SE11-SECREQ-03, SE11-SECREQ-04, SE11-SECREQ-05, SE11-SECREQ-06, SE11-SECREQ-07, SE11-SECREQ-08, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-RISK-09, SE11-RISK-10, SE11-RISK-11, SE11-RISK-12, SE11-RISK-13, SE11-RISK-14, SE11-AC-01, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-08, SE11-AC-09, SE11-AC-10, SE11-AC-11, SE11-AC-12, SE11-AC-13, SE11-AC-14, SE11-AC-15, SE11-DEP-01, SE11-DEP-02, SE11-DEP-03, SE11-DEP-04, SE11-DEP-05, SE11-DEP-06, SE11-DEP-07, SE11-DEP-08, SE11-DEP-09, SE11-DEP-10, SE11-DEP-11, SE11-DEP-12, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05, ASM-SE11-06, ASM-SE11-07, ASM-SE11-08, ASM-SE11-09, ASM-SE11-10, ASM-SE11-11, ASM-SE11-12, ASM-SE11-13, ASM-SE11-14]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v4 (revision of v3 after review findings REVIEWER-EN-SE11-PHYSICAL-001, 003, 004, 005, 006, 008, 009) · **Owner:** SE11 (Infrastructure, Containers & Runtime Engineering, SEED-01 §74) · **Run:** SMK-20261103114255 · **Baseline state:** PROVISIONAL, specification-class baseline, no part-number fingerprint, **two gaps open by necessity** (§0.3)

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and reference BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite by this document id and the disposition they rely on. It selects no vendor, prices nothing and purchases nothing (§15).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`), consumed sections: hardware strategy §152–§177 (document sections 37–45, including the section-40 reference-configuration table inside §160), the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note at the end of §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231), the guardrails Appendix H (§232–§238) and the domain list §74. No BOM content is recreated from memory; every specification cited below is taken from those sections (§165, §227.3, §228.1 and §229.1 re-read for this revision).

## 0. Document status, source availability and limitation

### 0.1 Inputs: what was available and what was not (re-verified for v4)

| Input (context id) | Availability at authoring (v4) | What SE11 needed from it | Effect of absence on this document |
|---|---|---|---|
| PL-REQ-ID-REGISTER (required source) | **Absent** — context block marked "missing"; `list_documents 10-Product-Lead/` returns no files | Requirement / decision / constraint ids with full specification and seed section | **UNMET SOURCE (SE11-DEP-01), OPEN.** The register applies and is required; it was not consumed because it does not exist in the repository. No register id is cited or invented. The seed-section crosswalk of §0.5 is preparation for reconciliation, not reconciliation. The implementation restriction (§17) stays until SE11-AC-11 attaches register ids. |
| PL-REQ-REGISTER-G01 … G04 (register fragments) | **Absent** (index lists 60 chars, 0 sections) | Verbatim BOM appendix | BOM read directly from SEED-01 §227–§231, which the hardware chain rule permits for SE11. |
| PM09-* (14 product documents) | **Absent** (`list_documents 20-Product-Domains/PM09/` empty) | MVP scope, product NFRs, acceptance criteria, risks/constraints, decision log, KPIs | Product-level targets are not reconciled. Every NFR value in §3 is an SE11 engineering proposal (ASM-SE11-06). |
| NT16-* (8 vendor/dependency documents) | **Absent** (folder holds one unrelated probe file; none of the eight required documents) | External-dependency and SLA requirements, exit/replacement assessment | External-provider residual risks (FD-EXT-AI, FD-INTERNET, hosted equivalents, T3 provider) are stated from the seed only (SE11-DEP-09). |
| EL-* (26 engineering-lead documents) | **Absent** (`list_documents 40-Engineering-Lead/` empty) | System/runtime/deployment/reliability architecture, NFR ids, ADRs, interface-contract governance and register, estimates, sequencing, DoR/DoD | No EL decision id is cited; no EL review has occurred; the provided contracts cannot be registered in EL's register (§18.2). |
| SP16-* (7 FinOps documents) | **Absent** | Cost allocation, spend guardrails, unit economics | The economic half of the seed's justification rule for local capacity (§238) cannot be evaluated; local-versus-hosted stays open per pool (SE11-ADR-01, gate G-LOCAL, SE11-DEP-08). |
| SEED-01 (seed, read on demand) | Available | Hardware strategy and BOM | Sole substantive input of this version. |

### 0.2 Decision status model

Every decision, requirement and NFR in this version carries the status **PROV** (provisional, seed-derived, not reconciled). The status **REC** (reconciled: register ids attached, EL review recorded, upstream product/NFR documents checked) can only be assigned by a later version after SE11-AC-11 passes. **No entry in v4 is REC.** Downstream documents that cite this version cite it as `SE11-PHYSICAL-INFRASTR-HARDWARE v4 (PROVISIONAL)` and carry the same provisional status for anything derived from it (SE11-REQ-11).

### 0.3 Open gaps and how the completion event encodes them (corrects findings 001 and 008)

The v3 reading "`covered` = sought and found absent" is **withdrawn**; it made a machine-readable value mean its opposite. The v2 reading "`not_applicable` = inapplicable" was equally wrong. This version states the truth in the document and uses the only event value that does not assert satisfaction:

| Item | Substantive status | Event value reported | One-line reason for the event value (required by the author rules) |
|---|---|---|---|
| Required source PL-REQ-ID-REGISTER | **UNMET SOURCE — OPEN** (SE11-DEP-01). Not consumed, not reconciled, no ids mapped. Finding 001 is **not closed** by this version and cannot be closed by SE11 until the register exists | `source_coverage: not_applicable` | The source could not be applied in this run because it does not exist in the repository; this is a source gap, not a judgement that the source is irrelevant, and the document is **not source-complete** |
| QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 (compatibility and availability checked sufficiently) | **UNMET — OPEN.** No dated, attributable manufacturer support or availability evidence exists in the allowed corpus; whether one coherent supported configuration of the §11.4 classes exists today is **unverified** (§11.2, feasibility conditions FC-01 … FC-09). Finding 008 is **not closed** by this version | `outline_coverage: not_applicable` | The criterion cannot be met in this run because the evidence it requires does not exist in the allowed corpus; its outcome is UNMET, tracked by SE11-AC-01 and the FC-nn conditions; no closure is claimed |

Neither value, and nothing else in the completion event, asserts that either item is satisfied. `checks.dependency_consistency` reports consistency with the dependencies that exist (none) and with the seed; it does not assert reconciliation with the absent documents. Consequences carried through the document: status PROVISIONAL, not approved for implementation (§17); every disposition PROV (§0.2); risk SE11-RISK-09 open.

### 0.4 Disposition of the v3 review findings

| Finding | Correction made in v4 | Where |
|---|---|---|
| 001 source gap redefined as `covered` | Redefinition removed; the gap is stated as OPEN and UNMET with the honest event encoding and reason (§0.3); no register id, approval or availability fabricated; `based_on` unchanged (only SEED-01 was relied on); implementation restriction retained; the crosswalk is labelled preparation, not reconciliation | §0.1, §0.3, §0.5, §17, §19 |
| 003 contract discipline: unregistered provided contract; consumed behaviours without owner contract ids; write-freeze enforcement unassigned | SE11 cannot register anything in artefacts that do not exist and does not fabricate owner contracts. What is corrected: (a) the provided interfaces are now two fully specified contracts (schema, delivery, failure semantics, versioning) with a pre-filled registration record and an explicit **REGISTRATION PENDING** status naming the two missing registers; (b) each consumed cross-domain behaviour is decomposed into *SE11's side* (specified here and implementable from this document alone) and *the owner's side* (a placed requirement with owner, stage, status UNMET and the consequence while unmet) — no dependency label is treated as closure; (c) write-freeze enforcement is **assigned** to the data-store owner (SE12) by placed requirement SE11-REQ-18, with EL's Definition-of-Ready and SE20's checklist as process gates — assigned, not accepted; (d) the security section is split into checks SE11 can execute and pass without the owner's control catalogue (SE11-REQ-19, SE11-AC-08a) and the owner-mapping that remains unmet; (e) telemetry integration is specified as SE11's exporter contract so that SE20's consumption is a subscription, not a design dependency | §18, §4, §6.3, §10.3, §13 |
| 004 reallocation example weakened floors; expansion keyed to Check 2 only; no outcome for floor-only failure | Floors are fixed inputs; the only legal reallocation moves are raising a floor to meet demand and lowering a maximum down to its minimum; required capacity **Req = max(1.25 F, C + H_min)** governs selection and expansion; ordered Steps 1–4 with deterministic outcomes; worked examples for ceiling-only failure, floor-only failure, both-fail and an infeasible configuration (SE11-DEC-15) | §5.2, §5.3 |
| 005 §6.1a budget could exceed the device; no per-device/cgroup split; remedies only on one row | Budget identity **V_min + B_max + H_io = D2** enforced by construction (B_max = 0.8 D2 − V_min), feasibility test V_min + B_floor ≤ 0.8 D2 with a deterministic response when Validation's demand cannot fit (Mapping-V: Validation isolated on M2_3; else REV-STORAGE-HOT); per-virtual-disk and per-cgroup shares that sum to B_max including a root/system I/O allowance; summed-traffic verification; remedies attached to every matrix row; SE11-AC-12b extended with elevated-demand, all-devices-simultaneous and infeasible-demand cases (SE11-DEC-16) | §6.1a, §14 |
| 006 M3 could leave the platform halted; M1 timing inconsistent with AC-15 | M3 redefined as a **wake-poll loop** that re-arms on every on-battery wake until mains is present or the UPS exhausts (then the AC-input-cycle path applies), so no restoration time is uncovered; M3 without evidenced NAS wake (N1) and M4 classified attended-only and inadmissible for the automatic-restart requirement; one end-to-end timing budget per mechanism (alarm/output-cycle, boot, decision, VM ladder) with the bound set by derivation (T_restart ≤ 12 min to S6 entry, not the unsupported 10 min); M1 output-off delay D_off derived per candidate so that outputs drop 60 s after the last device is off; drills for restoration immediately after S2 entry and immediately after an unsuccessful on-battery wake with output energised (SE11-DEC-17, SE11-REQ-20) | §8.3, §8.4, §3, §14 |
| 008 QC-AR-03 claimed closed by abstraction to classes | The sentence asserting that specification classes "cannot be impossible or obsolete" is **removed**; class-level feasibility conditions FC-01 … FC-09 are listed as open conditions with the evidence that closes each and the consequence if it fails; the baseline selection/fingerprint record is a separate pre-build artefact (fingerprint v0: none) distinct from commissioning evidence; QC-AR-03 is reported UNMET (§0.3) | §11.2, §11.3, §17, §19 |
| 009 no legal bootstrap for protection states | Mechanism readiness separated from dataset protection: new states MECH-UNVERIFIED and ARMED (fixture-verified mechanism, commissioned key custody, no real dataset), creation permitted from ARMED, first real dataset enters PROTECTED with an **ANCHOR** timestamp (t_create) that the first verified copy replaces (**COPY**); recovery validity defined per kind; the enforcing service per class named; state table, SE11-REQ-13/17, platform states, SE11-AC-07b/07c reconciled; from-empty activation test SE11-AC-07d added; commissioning evidence is stored in `REPO` (protected from day one) so INV/EVID do not block commissioning (SE11-DEC-18) | §6.2, §6.3, §14, §18.3 |

### 0.5 Pre-register crosswalk (preparation only) and seed consistency check

**Crosswalk.** PL-REQ-ID-REGISTER rows name the seed section they distil. The table keys every SE11 identifier to the SEED-01 section(s) it derives from so that attaching register ids in SE11-AC-11 is a lookup. It is **not** a mapping to the register: the "Register id" column is empty because the register is absent (UNMET, SE11-DEP-01).

| SE11 id(s) | Derived from SEED-01 | Register id |
|---|---|---|
| SE11-ADR-01, gate G-LOCAL, B19 | §157, §158, §160, §168, §226 status note, §238 | UNMET |
| SE11-ADR-02, B9 | §166, §167, §168, §227.9 | UNMET |
| SE11-ADR-03, SE11-RISK-02, B4 class | §227.4, §228.1 (ECC on NAS) | UNMET |
| SE11-ADR-04, SE11-DEC-04, B11, §5.5 | §175, §176, §177, §227.7, §227.11, §160 table | UNMET |
| SE11-ADR-05, SE11-REQ-03, §6.5 | §163, §164 | UNMET |
| SE11-ADR-06, SE11-ADR-11, SE11-DEC-07, SE11-DEC-10, SE11-DEC-13, SE11-DEC-17, SE11-REQ-06, SE11-REQ-15, SE11-REQ-20, §8.3 | §165, §228.1, §229.1 | UNMET |
| SE11-ADR-07, SE11-DEC-08, B17 | §165 ("critical network components"), §166, §230 | UNMET |
| SE11-ADR-08, SE11-DEC-03, SE11-DEC-06, SE11-DEC-15 | §158, §159, §162, §164 ("according to retention policy"), §234, §238 | UNMET |
| SE11-ADR-09, SE11-ADR-12, SE11-DEC-09, SE11-DEC-16, SE11-REQ-02, SE11-REQ-16 | §156, §157, §163, §174, §227.6 | UNMET |
| SE11-ADR-10, SE11-DEC-11, SE11-REQ-01, SE11-REQ-14, SE11-NFR-01 | §157, §174, §175 | UNMET |
| SE11-REQ-05 | §160 | UNMET |
| SE11-REQ-07, SE11-REQ-08, SE11-NFR-04 | §160 ("capture performance/resource telemetry from the first workloads"), §234 | UNMET |
| SE11-REQ-09, SE11-SECREQ-02 | §12 (current-practice revalidation), §25 (certified component registry), §160 | UNMET |
| SE11-REQ-10, B18 | §165, §231 | UNMET |
| SE11-REQ-13, SE11-REQ-17, SE11-REQ-18, SE11-DEC-18, SE11-NFR-05, §6.3 | §164 ("truly irreplaceable data should have an independent/off-site or otherwise isolated copy"), §31 | UNMET |
| SE11-SECREQ-01…08, SE11-REQ-19 | §59, §66, §112, §185, §228.1 (AES-256) | UNMET |
| §9 failure domains, SE11-NFR-06/07 | §172, §173, §175 | UNMET |
| §12 triggers and REV-* | §159, §161, §171, §177, §226 (F.20) | UNMET |
| ASM-SE11-02, SE11-RISK-08 | §0 (approval status), §151 | UNMET |

**Seed consistency check** (against SEED-01 as the common root; the absent EL/PM09/NT16/SP16 documents cannot be checked and no consistency with them is asserted). Six deviations/conflicts, each with a disposition; §16.6 repeats them as the rules require.

| Id | Seed statement | This document | Disposition |
|---|---|---|---|
| C1 | §165: the rack UPS "feeds rack PDU for local worker nodes **and switch** when used"; the same section gives the PC+NAS UPS the purpose "protect central PC, NAS **and critical network components** long enough for controlled shutdown" | The core switch is powered from PD-A (UPS-A) | Deviation from the rack-UPS clause accepted (SE11-DEC-08): the rack does not exist at baseline, the switch is a critical network component in the seed's own words, and in candidate S-1 the NAS shutdown command crosses it. When the rack exists the switch stays on PD-A unless S-3 (no command path) is in use, in which case it may move to PD-B as §165 states. Reviewers resolve if they read the rack clause as mandatory |
| C2 | §227.6: M2_4 = "platform data / DBs / containers", M2_2 = "VM & artifact store" | Highest-priority VM system disks are placed on M2_4 with the data; M2_2 carries High/Medium VM disks and artifacts; Mapping-V (§6.1a) may move Validation to M2_3 | Deviation recorded as SE11-DEC-09/ADR-09 with reason (§157 reservation principle, §174 priority classes) and impact (§6.1) |
| C3 | §165/§229.1: one PC+NAS UPS with "automatic graceful shutdown via PowerPanel / NAS UPS service" | SE11 does not assert that any host↔NAS signalling combination works; candidate S-3 substitutes a second UPS for the NAS | Gated decision SE11-DEC-10; S-3 is a topology substitution of B15 recorded with reason (no evidenced cross-device integration) and impact (second UPS of the B16 class, separate runtime budget) |
| C4 | §166/§230: switch and rack items apply "if local rack infrastructure is selected" | The managed switch (class) is adopted at baseline without a rack | Deviation accepted (SE11-ADR-07): three or more endpoints and VLAN enforcement of `seg.*` need a switch regardless of the rack; the smallest class satisfying §230 is used (§158 no-overbuild); the interim point-to-point placement of §7.2 remains allowed |
| C5 | §227.4 and §228.3 list 4×64 GB and 6×20 TB as the reference quantities | Quantities are candidates sized by rule; defaults M-A (128 GB) and N-A (4 drives) | Not a conflict: §162, §164 and §238 make the quantities conditional; recorded for transparency (SE11-ADR-08) |
| C6 | §0: Rev 1.1 is "proposed"; "the approved v1.0 document remains authoritative until this revision is explicitly approved" | Rev 1.1 is treated as the operative seed because only Rev 1.1 contains the hardware baseline | ASM-SE11-02, SE11-RISK-08; sign-off bound to the Rev 1.1 sha so that approval or change re-enters this document |

