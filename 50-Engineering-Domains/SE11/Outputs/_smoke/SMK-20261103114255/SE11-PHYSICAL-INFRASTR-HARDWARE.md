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


## 1. Authoritative source baseline (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01)

### 1.1 Exact version and sections consumed

| Item | Value |
|---|---|
| Seed | SEED-01, "Master Product Vision & Operating Architecture — Proposed Revision 1.1", "Expanded 2026 Baseline — Greenfield, Opportunity Intelligence, 19-Gap & Infrastructure Edition" (§0); file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| BOM version | Appendix G "Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note in §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231) |
| Strategy sections | §152–§154 (37.x stage boundaries, shared hardware, evidence progression), §156–§157 (38.x required logical environments, resource-reservation principle, section-39 greenfield provisioning principle), §158–§160 (39.x no-wait/no-overbuild, evidence-driven thresholds, portability, section-40 reference configuration table), §161–§163 (40.x central node, memory, NVMe), §164–§166 (41.x NAS, UPS/electrical, rack/network and the section-42 operating model), §167–§168 (42.x layout, VMs + containers), §169–§171 (43.x workers), §172–§175 (44.x redundancy, quorum, resource classes, degradation), §176–§177 (45.x GPU) |
| Guardrails | Appendix H §232–§238 (H.1–H.7) |
| Domain boundaries | §74 (SE11 = Infrastructure, Containers & Runtime Engineering; SE12 = Database, Storage & Data; SE14 = API, Integration & Portability; SE17 = Infrastructure, Workload & Data Security; SE19 = Performance, Resilience & Specialized Validation; SE20 = SRE, Observability & Production Operations; SE01 = Core Platform & Distributed Systems) |
| Approval status of the seed | §0: "The approved v1.0 document remains authoritative until this revision is explicitly approved." The hardware baseline exists only in Rev 1.1 (conflict C6, ASM-SE11-02); sign-off binds to that exact revision and sha (§17). |

### 1.2 Classification and engineering disposition of every BOM entry

The seed states that Appendix G "is a greenfield reference configuration, not an assertion of already-owned equipment or a mandatory topology" and that Product/Engineering "may procure, substitute, resize, or use hosted equivalents when evidence shows equal or better capability, reliability, portability, security, schedule, and economics" (§226 status note); that "local central compute, NAS, power, and worker infrastructure should be provisioned when workload evidence and economics justify it; managed/hosted equivalents remain acceptable where they better satisfy the target requirements" (§238); and that the central node "is a reference configuration rather than an inherited constraint" (§160, section 40 lead-in).

**Reading rules for the table.** (a) A disposition is the disposition *of the specification class of the reference item if local provisioning of that element is justified* under gate G-LOCAL (SE11-ADR-01); it is not a decision that local provisioning is justified. (b) **Part-number status (SE11-DEC-14):** the corpus contains no manufacturer support, firmware, qualified-list, driver or availability statement for any part number (§11.2). Every part number cited from the seed is therefore **DEFERRED-PENDING-EVIDENCE**: it is the seed's reference exemplar of the class, it is not baselined, and it becomes part of the configuration fingerprint only when its SE11-AC-01 record reads "confirmed". The *class* (§11.4) is what is adopted — and whether a coherent, currently supported configuration of those classes exists is itself unverified (FC-01 … FC-09, §11.2). (c) "Quantity/count status" separates the adopted class from any capacity figure, which is never adopted from the maximum listed configuration (ENV-DEC-017).

| # | BOM entry (seed section; the part number is the reference exemplar) | Seed class | Engineering disposition of the specification class (SE11 only) | Quantity / count status | Decision ref |
|---|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, Zen 5 homogeneous, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — class §11.4; virtualization extensions and IOMMU enabled; 230 W package limit is the compute line of the power budget (§8.2). Part number DEFERRED-PENDING-EVIDENCE | n/a (one CPU) | SE11-DEC-01, SE11-DEC-14 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — class: dual-tower air cooler ≤ 160 mm with AM5 mounting; structural check only (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi: 4×DDR5 to 256 GB; PCI_E1 Gen5 x16 (CPU); PCI_E2 Gen3 x1; PCI_E3 Gen4 x4 (shares with M2_3); M2_1 Gen5 x4 CPU; M2_2 Gen5 x4 CPU sharing with USB4; M2_3 Gen4 x2 chipset; M2_4 Gen4 x4 chipset; 4×SATA; 5 GbE; Wi-Fi 7; BT 5.4; 2×USB4; Flash BIOS; Clear CMOS (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map verified before baseline (SE11-AC-02) with fallbacks A/B/C and Mapping-V (§6.1a); Wi-Fi/Bluetooth disabled in server role; no out-of-band controller, so the management path is §10.2. Part number DEFERRED-PENDING-EVIDENCE (BIOS/CPU support currency not established, FC-01) | n/a | SE11-DEC-02, SE11-DEC-12, SE11-DEC-14 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC, single matched kit; "step down to 5600/5200 if 4-DIMM training is unstable" (§227.4; §162) | Preferred target (class); evidence-driven (quantity) | ADOPT WITH ENGINEERING CONSTRAINT for the **class** (DDR5 UDIMM matched kit on the AM5 4-slot platform, EXPO with the seed's 5600/5200 fallback, non-ECC accepted and monitored, SE11-RISK-02). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** 256 GB (4×64) is the reference *ceiling*, not adopted capacity. Quantity chosen by Table 5.3-R and the admission rule of §5.3 (M-A default; larger candidates only by the ordered procedure) | SE11-DEC-03, SE11-DEC-15, SE11-ADR-03, SE11-ADR-08 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch at x2 is acceptable subject to SE11-AC-02; under Mapping-V the M2_3 device carries Validation instead (§6.1a). Part number DEFERRED-PENDING-EVIDENCE | 2 devices (roles per §6.1/§6.1a) | SE11-DEC-02, SE11-DEC-12, SE11-DEC-16 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; seed roles "platform data / DBs / containers (M2_4)", "VM & artifact store (M2_2)" (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID (SE11-ADR-05); role mapping deviates from the seed's literal labels (conflict C2, SE11-DEC-09, §6.1). Part number DEFERRED-PENDING-EVIDENCE | 2 devices | SE11-ADR-05, SE11-DEC-09 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build; with the 145 W optional GPU only after the measured power-budget check the seed itself requires (§227.11; §160 table); any accelerator above 145 W, dual-slot, or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance, 3×140 mm fans (§227.8) | Preferred target | ADOPT — class §11.4; clearance and form factor structurally compatible with B2/B3 (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B9 | OS — Windows 11 Pro retail (§227.9; operating model §166) | Fixed by the operating model (§166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role; persistent services only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13). Edition/licence identifier DEFERRED-PENDING-EVIDENCE | n/a | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); if coexistence fails, Fallback A relocates the NIC to PCI_E1 while the GPU is deferred (SE11-DEC-12); hypervisor virtual-switch driver support not established (FC-05). Part number DEFERRED-PENDING-EVIDENCE | 1 device | SE11-DEC-02, SE11-DEC-12 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell, 24 GB ECC, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition" §175; "driven by measured demand and economics" §177) | DEFER / OPTIONAL — adoption preconditions §5.5 and trigger TRG-GPU §12.2; when triggered, Fallback A (NIC in PCI_E1) must first be undone or replaced (§6.1a) | 0 at baseline | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T: 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock (64 GB max), 2×10GbE + 2×5GbE, 2×USB4, 4×M.2, ADM/Btrfs snapshots, per-folder AES-256, "UPS support / network UPS server" (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only (never a live datastore); admin interface on `seg.mgmt`; firmware lifecycle §10.4; UPS-signalling role gated by SE11-DEC-10. Part number DEFERRED-PENDING-EVIDENCE | 1 enclosure; subject to G-LOCAL (hosted object storage is the recorded equivalent for T2/T3, §6.7) | SE11-ADR-05, SE11-DEC-10 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install on TRG-NAS-MEM (§12.2) | 0 at baseline | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target (class); count tied to retention policy (§164) | ADOPT WITH ENGINEERING CONSTRAINT for the **drive class** (3.5-inch enterprise CMR, RAID 6 mandatory at ≥ 20 TB per drive, SE11-RISK-06). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** Six drives is the reference *ceiling*; count chosen by the §6.7 rule (N-A default) | SE11-DEC-06, SE11-ADR-08 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, line-interactive AVR, 12 outlets (6 battery + surge, 6 surge only), NEMA 5-15P, USB HID, "automatic graceful shutdown via PowerPanel / NAS UPS service", RB1290X2 batteries (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement; per-candidate shutdown budget SE11-REQ-06 with fail-closed outcome (§8.4); signalling and restart integration gated (SE11-DEC-10, SE11-DEC-13, SE11-DEC-17). Part number DEFERRED-PENDING-EVIDENCE | 1 unit (S-1/S-2); 2 units of the B15/B16 classes in S-3 | SE11-DEC-07, SE11-DEC-10, SE11-DEC-13 |
| B16 | UPS (rack) — second unit ~1000 VA / 600 W pure sine, model TBD; "when a local worker rack is used" (§229.2; §165) | Candidate ("when used") | DEFER / OPTIONAL — only with a local worker rack, **or** adopted early as the NAS unit under candidate S-3 (conflict C3) | 0 at baseline (1 if S-3) | SE11-DEC-08, SE11-DEC-10 |
| B17 | Rack — 18U; 1U 24-port switch "at least 2×10GbE"; 1U PDU; worker trays sized to measured need; 1U power-brick shelf; "no fixed initial worker count" (§230; §166) | Candidate ("If local rack infrastructure is selected", §166) | Switch: ADOPT WITH ENGINEERING CONSTRAINT by class (managed, VLAN-capable, ≥ 2×10GbE minimum per seed, ≥ 4×10GbE preferred, §7.2; conflict C4). Rack, PDU, trays, shelf: DEFER / OPTIONAL until TRG-WKR-LOCAL (§12.2) | Switch 1; rack items 0 at baseline | SE11-DEC-08, SE11-ADR-07 |
| B18 | Electrical — two separate 15 A breakers (PC+NAS UPS on one, rack UPS on the other); UPS plugged directly into wall; dedicated 20 A optional; typical ~560 W, sustained peak ~1,150–1,300 W (§231; §165) | Fixed constraint (code-regulated) | ADOPT WITH ENGINEERING CONSTRAINT — stated as a requirement for qualified professionals (SE11-REQ-10); nothing electrical is designed here | n/a | SE11-REQ-10 |
| B19 | Local worker nodes (form factor and count unspecified; pool "may be local, hosted, cloud or hybrid", §168–§171) | Optional / evidence-sized | DEFER / OPTIONAL — hosted/cloud executors first (§160 "avoid premature local-compute constraints"); local class adopted on TRG-WKR-LOCAL | 0 at baseline | SE11-ADR-01 |

**Tally (authoritative; supersedes any other count):** ADOPT ×2 (B2, B8); ADOPT WITH ENGINEERING CONSTRAINT ×13 (B1, B3, B4-class, B5, B6, B7, B9, B10, B12, B14-class, B15, B17-switch, B18); DEFER / OPTIONAL ×5 (B11, B13, B16, B17 rack/PDU/trays/shelf, B19); SUBSTITUTE ×0 at baseline (S-3 would be a recorded topology substitution of B15 under SE11-DEC-10); ESCALATE ARCHITECTURE IMPACT ×0 at baseline (conditional REV-* triggers in §12.3). Capacity candidates: B4 quantity (M-A/M-B/M-A+/M-C), B14 count (N-A/N-B/N-C). **Part numbers: 17 DEFERRED-PENDING-EVIDENCE (B1–B17), 0 confirmed.** No substitution is silent: any future substitution is a new SE11-DEC entry with technical reason and impact (SE11-REQ-12).

## 2. Physical architecture scope and boundaries (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-02)

### 2.1 In scope (owned by SE11)

| Element | Content of this document |
|---|---|
| Local central compute | One central node (B1–B10 classes) as the reference configuration; host role, slot/lane allocation with fallbacks, reservation mechanism (§5) |
| Worker nodes | Capability classes and placement rules for local workers if and when adopted (§4, §12); physical provisioning (trays, power, ports) when triggered |
| GPU / accelerator class | Single-slot, ≤ 145 W, PCIe x16 class; deferred (§5.5) |
| Storage / NAS | Hot NVMe tiers on the host, the durable NAS tier, the physical mapping of every volume, the storage I/O budget and the protection matrix (§6) |
| Network switching / NICs / physical segments | 10 GbE storage/core path, 5 GbE host onboard, switch class, VLAN membership and addressing of the physical segments (§7). Physical-network engineering is SE11's: §74 places SE14 in "API, Integration & Portability Engineering", not physical networking |
| Rack / placement | 18U rack class; desk/room placement constraints (§8.5) |
| UPS / power distribution | Two power domains, UPS roles, per-candidate shutdown sequences, restart mechanisms with their timing budget (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10.1) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10.2) |
| Hardware-published signals and states | On-battery, shutdown, thermal, storage-pressure, protection-state and platform-state signals published under `SE11-CONTRACT-hardware-signals@1` (§18.2) for the scheduler, data owners and operations to consume (SE11-DEC-11, §6.3, §8.3) |

### 2.2 Out of scope (owned elsewhere; referenced, never included)

| Concern | Owner (SEED-01 §74 unless stated) | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (chain rule) | §15 |
| Electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only |
| System, runtime, deployment and reliability architecture | EL | EL cross-references this document; EL's documents are absent (SE11-DEP-02/10) |
| Capacity model and growth thresholds | SE01 (capacity concern) and SE11-HARDWARE-CAPACITY-SIZING (sizing) | §5.3 and §6.7 give candidate configurations and decision rules; the sizing document applies them (SE11-DEP-03) |
| Load shedding / job pausing policy | EL (scheduler), SE01 | SE11 publishes the signals (SE11-DEC-11, contract §18.2); the shedding policy and controller are not designed here |
| Data policy: dataset classification, retention, backup schedule, binding RPO/RTO, key custody, write-freeze enforcement in the data stores | SE12 (data), SE17 (security) | §6 states hardware-capable targets, protection states and provisional defaults; enforcement obligations are placed requirements (SE11-REQ-18) with unmet dependency SE11-DEP-04 |
| Portability and integration constraints on how pools are addressed | SE14 | Consulted on §4/§7 naming; owns no physical design |
| Security control catalogue and ids | SE17 (infrastructure/workload/data), SE15 (identity/crypto) | §13 lists SE11's requirements as SE11-SECREQ-nn and the checks SE11 executes itself (SE11-REQ-19); mapping to owner control ids is SE11-DEP-05 |
| Performance/resilience test execution | SE19 | §14 lists the tests; SE19 executes and reports (SE11-DEP-06) |
| Operations, monitoring, maintenance windows | SE20 | §10 states telemetry (as SE11's exporter contract) and window requirements (SE11-DEP-07) |
| Software/container/service design | existing SE11 runtime artefacts and EL | BND-03: not restated |

### 2.3 Context view (text)

```mermaid
flowchart LR
  subgraph PD_A[Power domain A: UPS-A class B15 on circuit A]
    HOST[Central host: Win11 Pro + Hyper-V\nVMs: Core + Data on M2_4 / Build-CI + Validation on M2_2\nM2_1 host system, M2_3 scratch - or Validation under Mapping-V]
    NAS[NAS class B12: RAID 6 (count = candidate)\nsnapshots, backups, evidence, archives = T2]
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
  GW --> EXT[External AI providers, hosted runners, hosted T3 copy]
  WK -. L4 1/2.5GbE .-> SW
  UPSA[UPS-A USB-HID] -- primary signal (gated, SE11-DEC-10) --> HOST
  HOST -- network shutdown command (S-1, gated) --> NAS
```

## 3. Stakeholders, concerns and quality attributes (ISO/IEC/IEEE 42010 framing)

| Stakeholder | Concern | Quality attribute (ISO/IEC 25010) | Measured by |
|---|---|---|---|
| EL | One coherent physical architecture to reference; contracts to register; shedding signals to consume | Compatibility, maintainability | §4–§10 cross-references; §18.2 contract definitions; SE11-DEC-11 |
| SE01 | Capacity inputs as ranges with assumptions; signals for the scheduler | Capacity | Table 5.3-R, §6.7, §12 |
| SE12 | Durable tier, RAID/replication boundaries, protection states with a legal bootstrap, recovery rules | Reliability (recoverability, fault tolerance) | §6.3, §6.6, SE11-NFR-05, SE11-AC-07a/b/c/d |
| SE14 | Pools addressed portably | Portability | SE11-REQ-05 |
| SE17 / SE15 | Trusted boot, management isolation, encryption support | Security (confidentiality, integrity) | §13, SE11-AC-08a/08b |
| SE19 | Burn-in, contention, abrupt-loss and resilience test surface | Reliability (maturity), performance efficiency | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows, shutdown and restart drills | Maintainability (analysability), reliability | §10, SE11-NFR-04 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, ADR-01 gate G-LOCAL, §12 triggers |

**Measurable non-functional targets introduced by this document (status PROV; binding to EL-ENGINEER-NFR-SPECIFIC ids is unmet dependency SE11-DEP-10; values are engineering proposals, ASM-SE11-06).**

| NFR id | Quality attribute | Target (measurable) | Verified by |
|---|---|---|---|
| SE11-NFR-01 | Performance efficiency / weighted-service guarantee under contention | Under the §14 contention profile: (a) Core and Data VMs: CPU-wait ≤ 5 % in every 60 s window, Core synthetic API probe p95 ≤ 1.5 × unloaded baseline, Data 4 KiB random-read p99 ≤ 2 × unloaded baseline; (b) Validation VM: CPU-wait ≤ 10 % (it receives its full 8 vCPU from reserve + weighted floating share, §5.2); (c) Build VM: receives ≥ 11 LP-equivalents of its 16 (4 reserved + ≥ 7 floating); (d) inside the Build VM, `pool.background` receives ≤ 10 % of the VM's CPU while build jobs saturate (cgroup weight 10 : 100). No ordered shedding is claimed at the hardware layer (SE11-ADR-10) | SE11-AC-12 |
| SE11-NFR-02 | Performance efficiency / storage path | Host↔NAS ≥ 0.7 GB/s sustained for 10 min during concurrent build-cache load; no other path degrades below 80 % of its unloaded throughput | SE11-AC-05 |
| SE11-NFR-03 | Reliability / safe shutdown and restart, per UPS and per candidate | For every UPS u in the selected candidate: B_u ≤ 0.7 × R_u, where B_u is the critical-path budget of §8.3 and R_u the measured runtime at measured load; every step completes inside its bound. Restart: **T_restart ≤ 720 s (12 min)** from mains restoration to S6 entry for the commissioned mechanism, given battery charge ≥ 50 % at restoration (derived budget: M1 ≤ 540 s, M3 ≤ 660 s, §8.3); VM readiness ladder adds T_ready ≤ 180 s, so full service ≤ 15 min | SE11-AC-06, SE11-AC-14, SE11-AC-15 |
| SE11-NFR-04 | Maintainability / observability | 100 % of §10.3 signals exported under `SE11-CONTRACT-hardware-signals@1`, sample interval ≤ 60 s, retained for at least one stage | SE11-AC-09 |
| SE11-NFR-05 | Recoverability (hardware-capable; SE12 binds the product RPO/RTO) | T1→T2 snapshot interval ≤ 1 h and full replication ≤ 24 h; single-VM restore from T2 ≤ 4 h; for every D-IRR class with real data: T3 copy age ≤ A_max = 24 h in state PROTECTED, expiry at A_max + G = 48 h (§6.3); first real copy of a newly admitted class within A_max of its creation; restore of each D-IRR class from T3 verified at every stage gate | SE11-AC-07a/b/c/d |
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
| `pool.admin` | Host OS, Hyper-V root, WSL2 + Docker Desktop interactive use (§167) | n/a | Windows host root partition | Not reservable in Hyper-V; the root partition takes floating LPs (§5.2); operational rule: VM reserves sum ≤ 16 LP so ≥ 16 LP float | Host root reserve + WSL2 cap | M2_1 |

**Simultaneous CPU accounting at baseline:** vCPUs assigned to VMs = 4 + 4 + 8 + 16 = **32 vCPU on 32 LP** (1 : 1, no vCPU oversubscription at baseline; bursts happen *within* a VM's own vCPU count). Guaranteed LPs (sum of reserves) = 4 + 4 + 4 + 4 = **16 LP (50 %)**. Floating LPs = **16**, taken first by the host root partition (typical need 2–4 LP, ASM-SE11-03) and then by VMs in weight proportion 150 : 100 (Core and Data cannot take floating LPs: their 4 vCPU are already fully reserved). Under full saturation this arithmetic gives Validation its remaining 4 vCPU in full (its weighted share of 12–14 floating LPs, 0.6 × 12 = 7.2, exceeds the 4 it can use) and leaves Build with 4 reserved + 8–10 floating = 12–14 of its 16 vCPU. That is a **weighted-contention outcome**, measurable as SE11-NFR-01, not an ordered shedding mechanism.

**Weighted contention versus load shedding (SE11-ADR-10, SE11-DEC-11).** 

1. *Weighted contention* is what the hypervisor's reserve/limit/weight controls and the in-VM cgroup weights produce automatically under saturation. It needs no controller; its guarantees are those of SE11-NFR-01 and are measured by SE11-AC-12.
2. *Load shedding* — pausing, cancelling or refusing noncritical jobs "when hardware capacity, network, storage, AI quota or power conditions degrade" (§175) — is a **scheduler action**, owned by EL (orchestration/scheduler) and SE01. SE11 does not design the controller or its transitions. SE11's obligation is to **publish the signals** on which the scheduler acts. The signal catalogue, delivery guarantee (≤ 60 s from the condition), ordering, retention and failure semantics are fixed in `SE11-CONTRACT-hardware-signals@1` (§18.2): `SIG-ONBATTERY`, `SIG-SHUTDOWN`, `SIG-THERMAL`, `SIG-STORAGE-PRESSURE`, `SIG-PROTECTION-STATE`, `SIG-PL-STATE`. Which jobs the scheduler sheds on each signal is EL/SE01 policy (placed requirement, unmet dependency SE11-DEP-03; see §18.3 row CI-1); the default expectation recorded for them, derived from §174/§175, is background → build → validation, with runtime never shed.

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
| Firmware baseline | UEFI Secure Boot and TPM 2.0 enabled; Wi-Fi 7 / Bluetooth disabled; "restore on AC power loss = power on"; RTC wake enabled and recorded (§8.3); settings baseline in §13 | §13, SE11-DEC-13, SE11-DEC-17 |
| Thermal | Dual-tower air cooling ≤ 160 mm in a mesh-front mid-tower with three 140 mm intake fans; sustained 230 W CPU package (+145 W optional GPU) validated by SE11-AC-04 | B2, B8 |

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

### 5.3 Memory sizing: the authoritative reservation table and decision rule (SE11-DEC-03, SE11-DEC-15; corrects finding 004)

**Evidence status.** No measured workload exists (§0.1: EL estimates and SE01 capacity model absent, SE11-DEP-03). Table 5.3-R therefore holds **hypothetical planning allocations** (ASM-SE11-03, ASM-SE11-11) derived only from the five required logical environments (§156) and the layout (§167). They justify no quantity by themselves; the sizing document replaces them with a traceable Stage-1 inventory and measured p95 values (§234 H.3). What *is* binding is the table's structure, the admission formula and the ordered procedure.

**Table 5.3-R — authoritative per-candidate memory reservations (GB). Every total in this document is derived from this table; no other section carries memory numbers.**

| Line | M-A: 2×64 GB = 128 GB (default) | M-B: 4×64 GB single kit = 256 GB | M-A+: M-A + second matched pair = 256 GB (two kits) | M-C: M-A kit, `pool.data` hosted |
|---|---|---|---|---|
| Host root partition reserve (hypervisor, host OS, drivers, management agents) | 12 | 16 | 16 | 12 |
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
| E2 — floor-only failure (the reviewer's F = 110 / C = 116 case) | Data 44 GB; Validation measured p95 raises its minimum to 14 | F = 12+8+20+44+14+12 = 110 → 1.25 F = 137.5 > 128 ✗; with maxima set to Validation 20, Build 12: C = 116 → C+8 = 124 ≤ 128 ✓; Req = 137.5 ✗ | Check 1 fails, Check 2 passes | Step 1 **fails** (1.25 F > 128; maxima cannot change F). Step 2 (M-C, Data hosted): F = 12+8+20+0+14+12 = 66 → 82.5; C = 12+8+20+0+20+24 = 84 → 92; Req = 92 ≤ 128 ✓ → **M-C** if admissible under §66/latency/economics. Else Step 3: on 256 with lines raised to demands (host 16, Core 32, Data 64, Validation 16→48, Build 16→64): F = 152 → 190; C = 232 → 240; Req = 240 ≤ 256 ✓ → **M-A+** (second pair, SE11-AC-04 re-run) |
| E3 — both checks fail | Data 44 GB, other floors at defaults | F = 12+8+20+44+8+12 = 104 → 130 > 128 ✗; C = 12+8+20+44+20+24 = 128 → 136 ✗ | Both fail | Step 1 fails (floor); Step 2 M-C: F = 60 → 75, C = 84 → 92, Req 92 ✓ → **M-C** if admissible; else Step 3 → **M-A+** (Req 240 ≤ 256 ✓) |
| E4 — infeasible configuration | Data working set 160 GB; Core 32; Validation 16→48; Build 16→64; host 16 | F = 16+8+32+160+16+16 = 248 → 1.25 F = 310 > 256 ✗ on every local candidate | Floor exceeds the board ceiling | Step 1 fails on 128 and on 256; Step 2 M-C: F = 88 → 110, C = 16+8+32+0+48+64 = 168 → 176, Req 176 ≤ 256 ✓ (and 176 > 128, so M-C would itself require 256) → M-C on M-A+ if §66 permits hosting the data; if §66 forbids it: Step 4 → **REV-MEM** (architecture revision); no hardware addition is selectable |

*Non-ECC* on the central node is accepted for every candidate (SE11-ADR-03) with the ECC platform class recorded as the substitute if SE11-RISK-02 materialises. *Default before a model exists:* the seed's H.1 ("start productively") and H.3 ("measure before resizing") apply: **M-A with the Table 5.3-R values is installed** (Req 124 ≤ 128 ✓) and the choice is recorded as SE11-DEC-03a in the sizing document.

### 5.4 Virtualization / host implications

- VM count and boundaries remain an engineering decision (§167); the four Linux VMs are the minimum that satisfies the isolation rule of §156. Merging Core and Data into one VM is permitted only if the static memory lines of Table 5.3-R are preserved as a sum, both stay on M2_4, and SE17 accepts the shared blast radius.
- Highest-priority VMs (Core, Data) use static memory and 100 % processor reserve; they are never configured for dynamic over-commit (SE11-REQ-01).
- Snapshots of the Validation and Core VMs are taken before any firmware/driver change (§10.4) and replicated to `pool.durable`.
- Nothing in the VM layer may encode physical slot ids, device serials or the host name; the portability requirement §160 applies to every VM definition (SE11-REQ-05). Storage is referenced by volume label / stable identifier, not by slot.
- Per-virtual-disk IOPS controls (hypervisor storage QoS minimum/maximum) are the preferred storage limiter; their availability on the chosen host OS edition is confirmed in SE11-AC-03 (FC-06). If unavailable, the **guest-side limiter** of §6.1a (cgroup v2 `io.max` inside the Build VM) is mandatory — device separation alone is not an accepted fallback (SE11-REQ-16).

### 5.5 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger TRG-GPU (§12.2: local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability — which means that if Fallback A (NIC in PCI_E1, §6.1a) is in use it must first be replaced by Fallback B or C with a passed SE11-AC-12b — plus 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms measured full-load system draw plus 145 W ≤ 80 % of the 750 W PSU rating and that the per-candidate shutdown budgets of §8.3 still hold at the higher PD-A load; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on the client hypervisor (device assignment or partitioning, FC-07) — if none exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as a new SE11-DEC; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator or a dual-slot card is ESCALATE ARCHITECTURE IMPACT (SE11-ADR-04).


## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Authoritative physical mapping of every volume (SE11-DEC-09 / SE11-ADR-09)

This table is the single source of truth for the default mapping (Mapping-D). Sizes are initial allocations (candidate envelope, ASM-SE11-03) and are thin-provisioned so that the sizing document can resize without re-mapping. The alternative Mapping-V of §6.1a swaps the Validation disks and scratch between M2_2 and M2_3; nothing else changes.

| Volume (guest device name) | Pool | Physical device (slot, link) | Initial allocation | Notes |
|---|---|---|---|---|
| Host OS, hypervisor, WSL2 distro disk | `pool.admin` | **M2_1** 1 TB (Gen5 x4, CPU) | whole device | T0 system; rebuildable from version-controlled host build; encrypted (§13) |
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
| T2 durable | `pool.durable` | NAS RAID 6 (count per §6.7) over L1 | per §6.7 | snapshots, backups, evidence, archives, mirrors (§164) |
| T3 isolated copy | — | off-site / hosted (provider per NT16, SE11-DEP-09) and/or T3-SUB isolated local medium (§6.3) | class D-IRR only | §6.3 |

**Why the mapping deviates from the seed's literal role labels (SE11-DEC-09, conflict C2).** The BOM labels M2_2 "VM & artifact store" and M2_4 "platform data / DBs / containers" (§227.6). Placing *all* VM disks on M2_2 would put the Highest-priority Core and Data system disks on the same device as Medium-priority build artifacts, violating the reservation principle (§157: reserve "storage I/O … for stable platform operation") and SE11-REQ-02. The role labels are guidance on purpose, not an isolation rule; moving the Highest-priority VM disks to M2_4 keeps M2_4 entirely Highest-priority and M2_2 entirely High/Medium. Impact: M2_4 carries both VM system disks and the database — all one priority class; M2_2 carries Validation (High) with Build (Medium), which is exactly the contention that §6.1a bounds. SE11-REQ-02 is satisfied without exception.

### 6.1a Storage I/O budget and protection matrix: Validation versus Build on M2_2 for every lane × QoS combination (SE11-REQ-16, SE11-DEC-16; corrects finding 005)

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

Examples: Vdem = 0.10 D2 → V_min = 0.20 D2, B_max = 0.60 D2. Vdem = 0.30 D2 → V_min = 0.45 D2, B_max = 0.35 D2 (≥ B_floor: feasible). Vdem = 0.40 D2 → V_min = 0.60 D2, B_max = 0.20 D2 = B_floor (boundary: feasible). Vdem = 0.45 D2 → V_min = 0.675 D2, B_max would be 0.125 D2 < B_floor → **infeasible** → remedies below. The v3 rule (fixed B_max = 60 % with V_min free to grow) is withdrawn.

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

### 6.2 Tiers and dataset classes

| Tier | Device(s) | Role (seed) | Durability boundary | Policy owner |
|---|---|---|---|---|
| T0 system | M2_1 | Windows + WSL2 (§227.5) | Rebuildable; no unique data | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 (Gen4 x2) or `bld-scr` on M2_2 | Build cache / scratch (§227.5) | Disposable | SE11 |
| T1 hot, Highest | M2_4 | Core/Data VMs, platform data, DBs, platform containers | Independent volume; snapshot + replication to T2 | SE12 (data), EL (VM definitions) |
| T1 hot, High/Medium | M2_2 (and M2_3 for Validation under Mapping-V) | Validation/Build VMs, artifact store | Independent volume; archival replication to T2 | SE12 (artifact retention) |
| T2 durable | NAS RAID 6 | Backups, snapshots, release evidence, VM/container archives, artifacts, mirrors (§164) | Dual-parity array + snapshots; "not the only backup" (§164) | SE12 |
| T3 isolated copy | Off-site / hosted, encrypted; or T3-SUB isolated local medium (§6.3) | "independent/off-site or otherwise isolated copy" for irreplaceable data (§164) | Independent of room, UPS, NAS and host | SE12 (policy), SE17 (keys) |

**Dataset classes (provisional default, ASM-SE11-08; SE12 is the classification owner, SE11-DEP-04):**

| Class | Definition | D-IRR sub-classes used by the protection states (with the service that enforces the creation gate, §6.3) | Minimum protection |
|---|---|---|---|
| D-IRR | Irreplaceable: cannot be re-derived from any other platform data | `REPO` (source repositories, IaC, configuration, **the version-controlled inventory file and SE11's commissioning evidence records** — enforced by SE11, which configures the hosted remote in the host build); `DB` (non-synthetic platform databases — SE12); `EVID` (release-evidence packages, decision logs — EL/SP14 as package producers, stored by SE12's policy); `KEYS` (secret/key backups — SE17/SE15; the KEYS T3 copy is encrypted under an offline custody secret held outside the platform so that it never depends on KEYS itself) | T1 + T2 + T3 under the state rules of §6.3 |
| D-BND | Bounded loss: re-derivable from D-IRR within an accepted window | build artifacts, locally built images, validation results, telemetry history | T1 + T2; loss window accepted by SE12 |
| D-REB | Rebuildable from definitions or external sources | caches, scratch, pulled container layers, VM system disks, **synthetic test fixtures used to verify protection mechanisms** | T1 only |

`INV` is no longer a separate protection class: inventory records and commissioning evidence live in `REPO`, which is protected from day one (§6.3), so producing commissioning evidence never depends on a class that does not yet exist (corrects finding 009's INV/EVID circularity).

### 6.3 Protection states with a legal bootstrap (SE11-REQ-13, SE11-REQ-17, SE11-REQ-18, SE11-DEC-18; corrects finding 009)

**Two separate things.** *Mechanism readiness* (the T3 copy path, encryption, key recovery and restore for class *c* work) is verified on **synthetic fixtures** (D-REB) before any real dataset of *c* exists. *Dataset protection* (a real dataset of *c* has a verified copy no older than A_max) begins when the first real dataset is admitted. The states below keep them apart so that the first real dataset can be created without an exemption.

**Per-class record.** Each D-IRR sub-class *c* carries: `mech_ok(c)` = timestamp of the last passed fixture verification (SE11-AC-07b); `t3_last_ok(c)` = reference timestamp for copy age; `kind(c)` ∈ {ANCHOR, COPY}; `age(c)` = now − `t3_last_ok(c)`; `A_max` = 24 h, `G` = 24 h (ASM-SE11-10 until SE12 binds them, SE11-DEP-04).

| State of class c | Definition | Create the first / a new real dataset of c | Mutate existing real datasets of c | Mandatory actions / notes |
|---|---|---|---|---|
| MECH-UNVERIFIED | No passed fixture verification for c (or the last one older than one stage, or failed) | **Prohibited** — only synthetic fixtures (D-REB) may exist | n/a (no real data) | Commission the T3 mechanism; run SE11-AC-07b on a fixture |
| ARMED | `mech_ok(c)` within the current stage; key custody for c commissioned; **no real dataset exists** | **Permitted** → the class enters PROTECTED with `t3_last_ok(c) := t_create`, `kind := ANCHOR`, and the owning service triggers the initial T3 copy immediately | n/a | Re-verify the fixture at every stage gate; if it fails → MECH-UNVERIFIED |
| PROTECTED | Real datasets exist; `age(c)` ≤ A_max. `kind = ANCHOR` until the first verified real copy (then `kind := COPY`, `t3_last_ok(c)` := copy time) | Permitted | Permitted | T3 copy at interval ≤ A_max; `SIG-PROTECTION-STATE` not raised. **Copy timestamps become valid (recovery-capable) only when kind = COPY** |
| DEGRADED-IN-BUDGET | Real datasets exist; A_max < `age(c)` ≤ A_max + G (initial copy missed, T3 path lost, internet down, copy failing) | **Prohibited** | Permitted | `SIG-PROTECTION-STATE` raised within 60 s; T3 copy retried every 1 h; SE20 prepares T3-SUB (encrypted isolated local copy, §6.2) so it can be taken before expiry; exposure window logged |
| EXPIRED | `age(c)` > A_max + G, **or** the last restore verification failed | Prohibited | Permitted **only while a T3-SUB copy of c with age ≤ A_max exists**; otherwise the class is placed in **write-freeze** (read-only) by its data-store owner (SE11-REQ-18) until a T3 or T3-SUB copy succeeds | SE20 incident; SE12 decides whether to extend via T3-SUB or hold the freeze; every hour in EXPIRED is logged against the stage's exposure budget |

**Transitions.** MECH-UNVERIFIED → ARMED: SE11-AC-07b(c) passes (fixture copied, restored, keys recovered). ARMED → PROTECTED(ANCHOR): the owning service admits the first real dataset. PROTECTED(ANCHOR) → PROTECTED(COPY): first verified real copy. PROTECTED → DEGRADED → EXPIRED and back by age, as the table states. ARMED → MECH-UNVERIFIED: stage-gate re-verification fails or the mechanism is lost before any real dataset exists. A class with real data never returns to ARMED; if its mechanism is lost it ages into DEGRADED/EXPIRED.

**Platform-level derived state (published as `SIG-PL-STATE`):** `PL-0` = before SE11-AC-07a (only D-REB and synthetic data may exist); `PL-T2` = SE11-AC-07a passed and no real D-IRR data exists (classes MECH-UNVERIFIED or ARMED only); `PL-T3-PENDING` = every class with real data is PROTECTED and at least one is ANCHOR; `PL-T3` = every class with real data is PROTECTED with kind COPY; `PL-DEG` = at least one class DEGRADED-IN-BUDGET and none EXPIRED; `PL-EXP` = at least one class EXPIRED.

**Invariants (reconciled with §6.6, §9, SE11-AC-07b/c/d and SE11-AC-10).** (I1) A real D-IRR dataset of class c exists only if c was ARMED at the moment of its creation or c already held real data in PROTECTED (creation gate). (I2) In `PL-T2` no real D-IRR data exists. (I3) In `PL-DEG`/`PL-EXP` real D-IRR data exists and is exposed to FD-STORAGE/FD-ROOM for at most `age(c)`; the exposure is bounded by A_max + G plus the T3-SUB age. (I4) SE11-AC-10 passes only in `PL-T2` or `PL-T3` (never `PL-T3-PENDING`, `PL-DEG`, `PL-EXP`). (I5) T3-dependent recovery (§6.6) is valid for class c only from a COPY; while kind = ANCHOR a loss of T1 and T2 loses the class entirely, and by the state rule that class is at most A_max + G old — this is the bounded, declared exposure of a newly admitted class.

**Class-specific activation.** `REPO`: the T3 copy is a hosted remote at an external repository service, configured by SE11 in the host build **before** any local hardware is commissioned (§160 keeps authoritative source in version control outside any single host); its fixture is the first commit, so `REPO` reaches ARMED and then PROTECTED(COPY) on day one — commissioning evidence and the inventory file are committed there and inherit that protection. `KEYS`: fixture = a test key under the offline custody secret; real custody is created only from ARMED, with the initial copy immediate. `DB`, `EVID`: fixture = a synthetic dataset of the class; real data admitted from ARMED only.

**Outage tolerance.** The tolerance of class c to loss of the T3 path is its **remaining copy-age budget**, `A_max − age(c)` at the moment the outage starts (then G of degraded operation), not a fixed 24 h. A class whose last copy is 20 h old enters DEGRADED-IN-BUDGET 4 h into an internet outage; a class admitted 20 h ago with kind ANCHOR and no copy yet does the same.

**Restoration.** T3 path restored → a full copy of class c completes → sample restore verification passes → `t3_last_ok(c)` updated, kind COPY → PROTECTED; any write-freeze is lifted by the data-store owner on `SIG-PROTECTION-STATE` clearing.

**Enforcement and ownership (SE11-REQ-18, contract-bound).** SE11 publishes `mech_ok`, `t3_last_ok`, `kind`, `age`, the class state and the platform state under `SE11-CONTRACT-hardware-signals@1` (§18.2) with the delivery and failure semantics fixed there. The gates are enforced by the services that own the data stores, consuming that contract: SE11 for `REPO`; SE12 for `DB` and the storage of `EVID`; SE17/SE15 for `KEYS`; EL's Definition of Ready for any new data-bearing service (it must name the class and the enforcing store); SE20's operational checklist as the process gate. **Write-freeze enforcement is assigned to SE12 as the data-store owner** (placed requirement SE11-REQ-18; status UNMET until SE12's document exists, §18.3 row CI-2). SE11 has no hardware-level backstop for a write-freeze and does not claim one. T3-SUB is an encrypted copy to a removable medium or a second independent location kept outside the room (§164 "otherwise isolated copy"), restore-verified in SE11-AC-07b; it is a bridging measure, not a replacement for T3.

**Verification.** SE11-AC-07b (fixture-based mechanism verification → ARMED, per class), SE11-AC-07c (expiry drill), SE11-AC-07d (from-empty-platform activation: PL-0 → PL-T2 → first real datasets → PL-T3 without any exemption), SE11-AC-10 (I4).

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
| M2_1 failure (host OS) | All VMs stop until the host OS is rebuilt from the version-controlled host build onto a replacement device; VM disks on M2_2/M2_4 remain intact | Spare NVMe; host build definition in version control |
| M2_3 failure | Mapping-D: rebuild caches, no data loss, interim scratch on M2_2 if no spare; Mapping-V: Validation outage, restore from T2/definitions | Spare NVMe or fallback mapping |
| Single NAS drive failure | No data loss; degraded; rebuild window ASM-SE11-04; replacement drive of equivalent class | Free bays allow a hot spare as an SE12 decision |
| Two concurrent NAS drive failures | No data loss (RAID 6) | — |
| Host loss (board/CPU/PSU) with intact NVMe | Move the NVMe devices to a replacement host of the §11.4 class or restore VMs to a hosted equivalent (§160, §168) | Hardware-independent definitions (SE11-REQ-05) |

**T3-dependent recoveries (valid per class only from a COPY, §6.3 I5; loss window = `age(c)` at the moment of loss; a class still at ANCHOR is lost entirely, bounded by A_max + G of existence; in `PL-T2` no real D-IRR data exists, so the residual is the loss of D-BND/D-REB only):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| Third NAS drive failure before rebuild completes (array loss) | Restore each D-IRR class from T3 with loss ≤ `age(c)`; D-BND re-derived | Verified T3 copy per class |
| NAS enclosure loss | T1 continues without a local backup target (degraded, time-boxed by SE12); D-IRR protected by T3 until NAS is replaced; classes move to DEGRADED when their T2→T3 pipeline depends on the NAS | T3 |
| Host loss with NVMe loss, room/site loss (FD-ROOM) | Rebuild on replacement or hosted infrastructure from T3 (D-IRR, loss ≤ `age(c)`) and definitions; D-BND re-derived | T3, hosted fallback |

### 6.7 Capacity headroom and NAS capacity candidates (SE11-DEC-06)

| Tier | Candidate / installed | Headroom rule | Expansion path |
|---|---|---|---|
| T1 (M2_2 + M2_4) | 2 × 4 TB (fixed by B6 class) | Alert 70 %, architecture review 85 % (REV-STORAGE-HOT) | No free M.2 slots: larger devices of the same class (scale-up) or artifact store fronted by T2; SATA ×4 for cold tiers only |
| T2 NAS — **N-A** (default) | 4 × 20 TB RAID 6 → 40 TB nominal, ≈ 36.4 TiB usable (derived with the seed's 80 TB → 72.8 TiB ratio, ASM-SE11-04); 4 bays free | Alert 70 %, review 80 % | Add same-class drives to free bays on TRG-NAS-CAP (online array expansion support by the NAS OS not established — FC-08) |
| T2 NAS — **N-B** | 6 × 20 TB RAID 6 → ≈ 72.8 TiB usable (seed reference); 2 bays free | as above | 2 free bays |
| T2/T3 — **N-C** | Hosted object storage for T2 and/or T3 (NAS deferred or absent) | provider quota | Hosted elasticity; acceptable per §238; economics unknown (SE11-DEP-08) |
| T3 | Must hold at least the D-IRR set per class; T3-SUB medium sized to the same set | n/a | Provider/medium per SE12 and NT16 (SE11-DEP-04/09) |

**Decision rule (SE11-DEC-06).** Let V be SE12's modelled retention volume for the first two stages (D-IRR + D-BND copies at the retention policy, including snapshot overhead). Choose N-A if V ≤ 22 TiB (≈ 60 % of N-A usable); N-B if 22 TiB < V ≤ 44 TiB; above 44 TiB the answer is REV-STORAGE (architecture revision), not simply more drives; N-C if gate G-LOCAL fails for the NAS. If the NAS must be commissioned before the model exists, **N-A** is installed (H.1/H.3) and the choice is recorded as SE11-DEC-06a in the sizing document. **Six drives are never adopted on the strength of this document alone.**


## 7. Network architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-06)

### 7.1 Physical links and roles

| Link | Speed / media | Endpoints | Role |
|---|---|---|---|
| L1 storage/core | 10GBase-T, Cat6a | Host NIC (PCI_E3; PCI_E1 under Fallback A; PCI_E2 under Fallback C) ↔ switch ↔ NAS 10 GbE port 1 | Backup, artifact, database-dump, VM-archive transfers; "network capacity appropriate to measured artifact, backup, database, and build traffic" (§166); NAS shutdown command path under S-1 (§8.3) |
| L2 management/upstream | 5 GbE onboard, Cat6a | Host onboard LAN ↔ switch | Host/VM management, upstream gateway, external-provider traffic |
| L3 NAS secondary | 10 GbE port 2 (spare), 2×5 GbE | NAS ↔ switch | Expansion: second 10 GbE consumer or link redundancy; 5 GbE for the NAS management segment |
| L4 worker links | 1 / 2.5 GbE (deferred) | Local workers ↔ switch access ports | "Worker links may be slower where sufficient" (§166) |
| L5 uplink | per upstream gateway | Switch ↔ gateway | Internet; external AI providers; hosted runners; T3 transfers |
| Wi-Fi 7 / Bluetooth | — | Host (disabled) | Not part of the architecture; disabled in firmware (§13) |

SE11-REQ-04: L1 sustains ≥ 0.7 GB/s host↔NAS during concurrent build-cache activity, and shared storage or control paths are not the first bottleneck during concurrent transfers (§166) — SE11-NFR-02, verified in SE11-AC-05 for the NIC slot actually in use (Fallback C is admissible only if this passes).

### 7.2 Switching / core role

The switch (B17 class) is the single core: managed, VLAN-capable, at least 2×10 GbE (seed minimum, §230) with ≥ 4×10 GbE preferred so that host, NAS primary, NAS secondary and one future 10 GbE consumer fit without replacement (SE11-ADR-07); 24 access ports at ≥ 1 GbE for workers, management devices and the gateway. It is adopted ahead of the rack (conflict C4) because the management segment and VLAN enforcement need it. Until the switch is installed, an interim point-to-point 10 GbE link host↔NAS with L2 to the gateway is acceptable *placement* — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2); in that interim the S-1 NAS shutdown command runs over the point-to-point link, which removes the switch from the shutdown path. Power: the switch is on PD-A (conflict C1; §165 names "critical network components" among the PC+NAS UPS loads).

### 7.3 Segmentation (SE11 designs the physical segments, VLAN membership and addressing; SE17 owns the security policy applied between them, SE11-DEP-05; SE14 is consulted for portable naming)

| Segment | Members | Purpose | Policy owner |
|---|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS software endpoint, SE11 telemetry exporter endpoint (§10.3) | Administrative plane; MFA-protected access (§59); no workload traffic; carries the S-1/S-2 shutdown signalling and N1 wake frames | SE17 (SE11-SECREQ-03) |
| `seg.storage` | Host 10 GbE, NAS 10 GbE | Backup/artifact traffic only; not routed to workers | SE17 |
| `seg.platform` | Core VM, Data VM, runtime namespaces | Stable runtime east-west | SE17 |
| `seg.build` | Build VM, Validation VM, member containers | Build/test east-west; fault injection confined here | SE17 |
| `seg.worker` | Local workers (deferred), hosted-runner VPN/egress | Disposable execution | SE17 |
| `seg.egress` | Gateway-facing | Default-deny disclosure gateway for external model inputs (§66, §185) sits on this boundary | SE17 / EL |

### 7.4 East-west traffic and bottleneck avoidance

- Build artifacts move Build VM → artifact store (same device, M2_2) over the host-internal virtual switch; only archival copies cross L1 to the NAS, scheduled by SE20 outside peak build windows.
- Database backups cross L1 off-peak; restore drills (§14) measure actual throughput to replace §6.4 assumptions.
- Worker-to-core control traffic is small; worker artifact pulls are served from the host artifact store, not the NAS.
- Management (`seg.mgmt`) and storage (`seg.storage`) traffic never share a VLAN; the NAS shutdown command is a management-plane flow.

### 7.5 Expansion ports / headroom

Free after baseline: NAS 1×10 GbE + 2×5 GbE; host 2×USB4 (emergency 10 GbE/NVMe adapters); switch access ports per §7.2. Triggers in §12.2.

## 8. Physical power / placement architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

### 8.1 Power domains

| Domain | UPS | Circuit (requirement, not design) | Loads | Status |
|---|---|---|---|---|
| PD-A | UPS-A, class B15 (1500 VA / 1000 W, pure sine, line-interactive AVR, 6 battery outlets, USB HID) | Circuit A: separate 15 A breaker; UPS plugged directly into wall (§231) | Central host, switch; NAS in S-1/S-2 | ADOPT WITH ENGINEERING CONSTRAINT |
| PD-N | UPS-N, class B16 (≥ 1000 VA / 600 W pure sine, USB HID) — **only under candidate S-3** | Circuit A or B as the electrician decides under SE11-REQ-10 | NAS only | Conditional (SE11-DEC-10) |
| PD-B | UPS-B, class B16 | Circuit B: second separate 15 A breaker (§231) | Rack PDU → local workers (and the switch only under S-3, conflict C1) | DEFER / OPTIONAL with the rack |

Isolation rule (§165): worker/rack power is isolated from the host/NAS UPS so a worker fault or overload cannot drop the durable tier. The upstream gateway is placed on PD-A only if the measured PD-A load leaves the runtime reserve of §8.4 intact; otherwise it is powered separately (its loss during an outage is acceptable: no shutdown sequence depends on it).

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

### 8.3 Safe-shutdown signalling, per-candidate timed sequences and restart (SE11-DEC-07, SE11-DEC-10, SE11-DEC-13, SE11-DEC-17; corrects finding 006)

**Signalling topology — gated decision (SE11-DEC-10, conflict C3).** The corpus names two integration surfaces: "automatic graceful shutdown via PowerPanel / NAS UPS service" on the UPS (§229.1) and "UPS support / network UPS server" on the NAS (§228.1). It does **not** establish any protocol/client/version combination between them. SE11 records three candidates and a gate:

| Candidate | Topology | Cross-device integration required | Status |
|---|---|---|---|
| S-1 (preferred) | UPS-A USB-HID → central host running the UPS vendor's host shutdown software; the host orchestrates VM shutdown and issues an authenticated remote shutdown command to the NAS over `seg.mgmt` | Host↔UPS: vendor software on the host OS version; host→NAS: a remote shutdown interface supported by the NAS OS | Gated by SE11-AC-01 evidence (dated vendor documentation for both interfaces at the exact versions; FC-09) |
| S-2 | UPS-A USB-HID → NAS as network UPS server; host as network client | NAS server protocol ↔ a host client implementing it | Gated by SE11-AC-01 evidence (FC-09) |
| S-3 (protocol-agnostic fallback) | Two UPS units, each with its own USB-HID path: UPS-A → host; UPS-N (class B16) → NAS | None across devices | Adopted automatically if neither S-1 nor S-2 produces evidence; recorded as a new SE11-DEC (topology substitution of B15) |

No shutdown sequence is relied on until the selected candidate has passed SE11-AC-06, SE11-AC-14 and SE11-AC-15.

**Common parameters (defaults; SE11-AC-06/15 replace them with measured values):** T_hold = 60 s (on-battery hold before the sequence starts; 0 s when battery charge < 50 %, see restart rules); VM graceful-stop timeouts Build 60 s, Validation 60 s, Core 60 s, Data 90 s, then forced stop (a forced stop marks the VM "unclean" so that its filesystem/database integrity check runs before services start on the next boot); host OS shutdown ≤ 60 s; NAS own shutdown ≤ 120 s; NAS command acknowledgment ≤ 15 s, one retry (≤ 15 s), then proceed regardless; margin M = 30 s. **Once S2 is entered the sequence is never aborted**, including by mains restoration (deterministic, bounded); restoration is handled by the restart mechanisms below. Serial order Core → Data is kept because Core services depend on Data; Build and Validation stop in parallel with each other and with the NAS command.

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
| 210 | — | Host sends "client shutdown complete" to the NAS, arms M3 if M3 is the mechanism, starts host OS shutdown |
| 240 | W_nas elapses (host confirmation arrived at 210; if it never arrives the NAS proceeds anyway) → NAS issues M1 (D_off = 180 s) → NAS shutdown ≤ 120 s | Host off by 270 |
| 360 | NAS off (**UPS-A critical path 360 s**) | — |
| 420 | (M1 only) UPS-A outputs drop: 60 s after the last device off | — |

**B_A(S-2) = 60 + 360 + 30 = 450 s** → **R_A ≥ 643 s (10.7 min)**. If the NAS OS cannot wait ≥ 240 s for the client, S-2 is not admissible (the host would lose power mid-sequence) — an SE11-AC-01 check.

**Candidate S-3 — two independent sequences:**

| UPS | Sequence | Critical path | Budget | Required runtime | M1 command / output drop |
|---|---|---|---|---|---|
| UPS-A (host + switch) | As S-1 host path without the NAS command: Build‖Validation 0–60, Core 60–120, Data 120–210, M1/M3 + host shutdown 210–270 | 270 s | **B_A(S-3) = 60 + 270 + 30 = 360 s** | **R_A ≥ 515 s** at PD-A load (host + switch) | Host commands at 210, D_off = 120 → drop at 330 |
| UPS-N (NAS only) | NAS on-battery at T0 → T_hold 60 s → NAS issues M1 → NAS own shutdown ≤ 120 s | 120 s | **B_N = 60 + 120 + 30 = 210 s** | **R_N ≥ 300 s (5 min)** at the measured NAS load — measured separately in SE11-AC-06 | NAS commands at 60, D_off = 180 → drop at 240 |

The NAS shutting down before the host is harmless: no shutdown step of the host depends on the NAS, and in-flight backup jobs are resumable (§175). Restart ordering (NAS reachable before the Data VM starts) is handled in S6 below.

**State machine (all candidates; the timed sequences above are the content of S2/S3):**

| State | Entry event | Actions | Bounded exit |
|---|---|---|---|
| S0 ONLINE | mains and UPS communication healthy | normal operation; UPS telemetry sampled ≤ 60 s | — |
| S1 ON-BATTERY (hold) | E1 mains loss at T0 | publish `SIG-ONBATTERY` (the scheduler stops admitting `pool.build`/`pool.background` work — EL/SE01 policy, SE11-DEC-11); alert SE20 | E2 mains restored before T0 + T_hold → S0 and `SIG-ONBATTERY` cleared; else E3 → S2 |
| S2 SHUTDOWN-INITIATED | E3: T0 + T_hold elapsed, **or** UPS low-battery, **or** UPS runtime estimate < B_u for that UPS, **or** E4 UPS-communication loss while in S1 (fail-safe: proceed) | the candidate's timed sequence; **never aborted** | → S3 within the candidate's host critical path (270 s) |
| S3 HOST-OFF | host power off | NAS completes its own path (S-1: off by t = 150, already done; S-2: off by t = 360; S-3: independent) | → S4 |
| S4 ALL-OFF | all devices halted; UPS output may still be live if mains returned during S2/S3 | M1: outputs drop at the commanded time and re-energise on mains; M3: the wake-poll loop runs; otherwise attended | → S5 |
| S5 RESTART-PENDING | E5: AC applied to the devices (exhaustion-and-return, or M1's output cycle), **or** an M3 wake that finds mains online | host firmware "restore on AC power loss = power on" and NAS "power-on after AC recovery" bring both up (M3: host wakes by RTC; NAS by N1); host UPS software reads mains state and battery charge | → S6 when mains online **and** charge ≥ 50 % **and** estimated runtime at current charge ≥ B_u / 0.7; until then the host stays in HOST-ONLY (no VM auto-start) with T_hold = 0 so that a second mains loss triggers an immediate host-only shutdown (B_hostonly = 0 + 60 + 30 = 90 s, needing R ≥ 130 s). Time spent waiting for charge is logged as *charge-limited restart* and is excluded from T_restart |
| S6 RESTARTED | charge and runtime conditions met | VM auto-start order with delays: Data (0 s) → Core (60 s) → Validation (120 s) → Build (180 s) = T_ready 180 s; the host waits up to 300 s for NAS reachability before Data VM services start, then proceeds (backups retry); unclean VMs run integrity checks first; SE20 post-event check of backups, telemetry and protection states | → S0 |

**Restart mechanisms (SE11-REQ-15, SE11-REQ-20, SE11-DEC-13, SE11-DEC-17).** Firmware AC-recovery settings act only when the device's AC input is actually removed and restored. If mains returns while the UPS output stays live (during S2, S3 or S4), nothing in firmware re-powers a halted device. One of the following mechanisms must be commissioned, in this order of preference, and the selected one recorded in the configuration fingerprint. Timing constants (ASM-SE11-13, replaced by SE11-AC-15 measurements): T_boot = 120 s (AC applied or RTC wake → host UPS software able to read UPS state), T_decide = 30 s, T_hostonly_off = 90 s, W = 300 s (wake-poll period), D_on = 60 s (UPS output restart delay once mains is present and outputs are off), T_ready = 180 s.

| Mechanism | How it works | Covers | Admissible for SE11-REQ-15? | Gate |
|---|---|---|---|---|
| **M1 — commanded output power-cycle (mandatory if evidenced)** | The device that owns the UPS link (host in S-1/S-3, NAS in S-2; each device for its own UPS in S-3) commands: "turn outputs off after D_off; restart outputs when mains is present (and battery ≥ the UPS's restart threshold)". **D_off = (worst-case last-device-off time on that UPS − command time) + 60 s guard**, per candidate: S-1 120 s (drop at 330), S-2 180 s (drop at 420), S-3 UPS-A 120 s (330) / UPS-N 180 s (240). Every device thus sees a real AC loss; when mains is already back the UPS re-energises after D_on and firmware AC-recovery fires on host and NAS → S5 | Restoration at any time during S2/S3/S4, and the exhaustion case | Yes (host and NAS) | SE11-AC-01: dated vendor evidence that the UPS class and the commanding software support commanded output shutdown with auto-restart (FC-09); SE11-AC-15 drill |
| **M3 — wake-poll loop (alternative where M1 is not evidenced)** | At the host OS shutdown command in S2 (t = 210), and again at **every** subsequent host-only shutdown while the UPS reports on-battery or unknown, the host arms a firmware RTC alarm at now + W. On wake the host boots HOST-ONLY, reads the UPS within T_boot + T_decide: *mains online* → S5 (charge rule) → S6, and the host sends N1 (Wake-on-LAN) to the NAS; *on-battery or unknown (E4)* → host-only shutdown (T_hostonly_off) and **re-arm**. The loop ends only when a wake finds mains online or the UPS exhausts; after exhaustion the AC-input-cycle path restarts host and NAS when mains returns, and any pending alarm is irrelevant. **No attempt cap** — a cap would reopen the "halted indefinitely" gap. Cost: each cycle draws host-only power for ≈ T_boot + T_decide + T_hostonly_off = 240 s per 540 s, accelerating exhaustion (SE11-RISK-14); accepted because after S3 no workload runs and no unflushed data exists, and exhaustion leads to the robust AC-cycle path | Host restoration at any time; NAS via N1 while UPS output is live, via AC cycle after exhaustion | **Host: yes.** NAS: **only with N1 evidenced** (or the NAS on UPS-N under S-3 with its own M1). **M3 without an evidenced NAS wake is ATTENDED-ONLY for the NAS and inadmissible for SE11-REQ-15** (recorded as FD-RESTART exposure, SE11-RISK-12) | SE11-AC-01 (RTC wake from soft-off on the board class, N1 WOL on the NAS class; FC-09); SE11-AC-15 drills (a)–(e) |
| **M4 — attended restart (residual)** | No automatic restart; SE20 is alerted (the UPS software's last message before shutdown and the absence of the expected S5 telemetry) and an operator powers the devices on | Everything, with human latency | **No** — ATTENDED-ONLY; inadmissible for SE11-REQ-15; blocks any stable-runtime baseline whose SLO requires unattended recovery | Recorded as FD-MGMT/FD-RESTART exposure (SE11-RISK-12); REV-POWER if an SLO (§117) requires unattended restart |

**End-to-end restart timing budget (SE11-REQ-20; T_restart = mains restoration → S6 entry, given charge ≥ 50 % at restoration; otherwise charge-limited and logged):**

| Scenario | M1 (S-1 / S-3) | M1 (S-2) | M3 (any candidate, host) |
|---|---|---|---|
| (a) Restoration at S2 entry (t = 0; worst case) | drop 330 + D_on 60 + T_boot 120 + T_decide 30 = **540 s** | drop 420 + 60 + 120 + 30 = **630 s** | alarm armed at 210 fires at 510 + 120 + 30 = **660 s** |
| (b) Restoration after outputs are off (M1) / immediately after an unsuccessful on-battery wake decision with output still energised (M3) | D_on 60 + 120 + 30 = 210 s | 210 s | host-only shutdown 90 + re-armed W 300 + 120 + 30 = **540 s** worst (restoration just after the decision); 450 s if measured from the re-arm |
| (c) Restoration during an M3 host-only boot | n/a | n/a | ≤ T_boot + T_decide = 150 s |
| (d) Restoration after UPS exhaustion | UPS restart on mains (class threshold) + 120 + 30 | same | same (AC-cycle path) |
| **Bound** | **T_restart ≤ 720 s (12 min)** holds for every scenario of every admissible mechanism; VM readiness adds T_ready 180 s → full service ≤ 15 min | | |

The v3 bound of 10 min is withdrawn: it was not derivable for restoration at S2 entry under any mechanism. Rule: **if M1 is evidenced it is mandatory**; M3 is used only where M1 is not; M4 is never a pass for SE11-REQ-15.

**Communication-loss handling (E4).** Loss of host↔UPS communication while in S0: alert; if it persists > 300 s the UPS protection is declared degraded (SE20 ticket, no workload change). If mains then fails while communication is still lost, the host has no event and the outcome is an **abrupt loss** (handled as FD-UPS-A, §9) — this residual is accepted and tested (SE11-AC-14). Loss of the NAS command path (switch or NAS unreachable) in S-1 S2: proceed; the NAS stops uncontrolled at UPS exhaustion — accepted residual with CoW crash-consistency and a mandatory scrub on restart (SE11-NFR-07). In S-2, loss of the NAS→host notification path is equivalent to E4 for the host. At an M3 wake, an unreadable UPS is treated as on-battery (shutdown and re-arm).

**Shutdown budget rule (SE11-REQ-06, SE11-NFR-03).** For every UPS u of the selected candidate: B_u ≤ 0.7 × R_u, where R_u is the measured runtime at the measured load of that UPS's domain. Default budgets: S-1 B_A = 360 s; S-2 B_A = 450 s; S-3 B_A = 360 s and B_N = 210 s. The 30 % reserve is held *against measured runtime*, not against the low-battery signal; the low-battery signal and the runtime estimate are additional triggers only.

### 8.4 Fail-closed commissioning outcome

SE11-AC-06 **fails** if, for any UPS of the selected candidate, R_u < B_u / 0.7 at the measured load, or if any step exceeds its bound in the drill, or if no admissible restart mechanism meets T_restart ≤ 720 s in SE11-AC-15 (M4 is a fail for any baseline whose SLO requires unattended recovery; M3 without an evidenced NAS wake is a fail for the NAS). Ordered remedies, each recorded as an SE11-DEC when applied: (1) remove non-essential loads from PD-A (gateway first; the switch stays while the S-1 command path needs it); (2) shorten VM stop timeouts only with SE11-AC-13 evidence that clean stops complete within the shorter bound; (3) change candidate (S-2 → S-3 shortens B_A from 450 s to 360 s and moves the NAS load off UPS-A); (4) substitute UPS-A by a higher-runtime unit of the same specification class (§11.4); (5) if none suffices, REV-POWER (§12.3). Until SE11-AC-06 passes, no stable-runtime stage baseline is accepted on this hardware (§154 evidence progression) and the platform stays in `PL-T2` at most (§6.3).

### 8.5 Placement constraints (rack / desk / room)

- Central host: tower chassis free-standing with unobstructed mesh-front intake and rear exhaust, off the floor, on PD-A; not inside the 18U rack (rack is for workers/switch/PDU per §230).
- NAS: adjacent to the host, on PD-A (S-1/S-2) or PD-N (S-3), within Cat6a reach of the switch; 3.5-inch drives are vibration-sensitive — solid surface, never stacked on the host.
- Switch: rack-mounted when the rack exists; until then shelf-mounted next to the NAS on a PD-A battery-backed outlet.
- Rack (deferred): 18U; 17U used with a gap after every device or 12U without gaps for micro trays (§230); 1U switch, 1U PDU, 1U power-brick shelf, trays sized to the selected worker form factor; PD-B feeds the PDU.
- Room: lockable (§13), ambient within device operating ranges, no shared circuit with high-draw appliances (requirement to the electrician under SE11-REQ-10); the T3-SUB medium is stored outside this room (§6.3); thermal and rack layout detail belongs to SE11-POWER-COOLING-RACK.

## 9. Failure-domain design (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-08)

Common-mode failure domains are named explicitly so that every consuming document references them by id (SE11-REQ-11). Redundancy "must cover actual shared failure points such as network, power, storage, control plane, DNS, external AI/provider dependencies, and internet connectivity — not merely worker count" (§173). Every domain has an accountable owner, a recovery dependency, a measurable acceptance target and a residual disposition; all dispositions are PROV (§0.2). Protection-state references are to §6.3.

| Domain id | What fails together | Blast radius in the reference configuration | Mitigation in this architecture | Accountable owner | Recovery dependency | Acceptance target | Residual disposition |
|---|---|---|---|---|---|---|---|
| FD-HOST | Board, CPU, memory, PSU | All four VMs, all local pools, WSL2; elastic workers lose their coordinator | Hardware-independent definitions (SE11-REQ-05); NVMe portable to a replacement host of the §11.4 class; T2/T3 copies; hosted fallback (§160, §168); queued disposable work idles rather than fails (§175) | SE11 (hardware), EL (architecture residual, SE11-DEP-02) | Replacement host class or hosted fallback; T2 (T3 if NVMe also lost) | SE11-NFR-06: degraded service ≤ 1 working day (ASM-SE11-07) | Accepted at Stage 1–2 pending EL; REV-HA when an SLO requires survival |
| FD-NVME-M2_1 | Host system device | All VMs stop until host OS rebuilt; VM disks intact | Version-controlled host build; spare device class | SE11, SE20 | Spare NVMe; host build definition | Host rebuilt and VMs restarted without T2 restore | Accepted; same class as FD-HOST but shorter |
| FD-NVME-M2_4 | Core + Data VM disks, platform data | **Full platform outage** (control plane and data) | Device isolation (only Highest-priority); hourly snapshots to T2 | SE11, SE12 | T2 (T2-only recovery) | SE11-NFR-05: restore ≤ 4 h per VM, loss ≤ 1 h | Accepted at Stage 1–2; reviewed at REV-HA |
| FD-NVME-M2_2 | Build VM disks, artifacts (Validation too under Mapping-D; scratch too when on M2_2) | Build/validation outage; runtime continues | Isolation from M2_4; T2 archives; rebuild from definitions | SE11, SE12 | T2 or rebuild | Restore ≤ 4 h; D-BND loss within SE12 window | Accepted |
| FD-NVME-M2_3 | Scratch (Mapping-D) or Validation (Mapping-V) | Slower builds, or validation outage under Mapping-V | Fallback mapping (§6.1a); T2 for Validation data | SE11 | none / T2 | Cache rebuilt / Validation restored ≤ 4 h | None material / accepted |
| FD-WORKER | One or more workers (local or hosted) | Capacity reduction only (§172) | Multiple eligible execution targets; no critical service on one uniquely named worker (§172) | EL (placement), SE01 | none | Queue drains on remaining capacity | None material |
| FD-STORAGE | NAS enclosure / array | Backups pause; T1 keeps running; D-IRR classes whose T3 pipeline passes through the NAS begin ageing | RAID 6; snapshots; T3; T2 never a live datastore; protection states (§6.3) | SE11 (hardware), SE12 (data) | T3 for D-IRR; replacement enclosure of the §11.4 class | No D-IRR loss beyond `age(c)` (COPY) or the class's bounded existence (ANCHOR); degraded window ≤ A_max + G per class | Accepted in `PL-T3`; in `PL-T2` no real D-IRR data exists; `PL-T3-PENDING`/`PL-DEG`/`PL-EXP` exposure bounded and logged |
| FD-SWITCH | Core switch / its uplink ports | L1, L2, L4, L5; host and NAS lose each other and the internet; VMs keep internal connectivity via the virtual switch; S-1 NAS command path and N1 wake frames lost unless point-to-point | Interim point-to-point L1; spare NAS ports; cold-spare switch of equivalent class is an SE20 stocking decision; S-3 removes the command-path dependency | SE11 | Replacement switch class | Backups resume within the SE12 window after replacement; no runtime data loss | Accepted: single switch at Stage 1–2 |
| FD-CIRCUIT-A | Mains/circuit A interruption **with healthy UPS-A** | Host, switch (and NAS in S-1/S-2) run on battery → controlled shutdown (§8.3) | State machine S1–S6; per-candidate budgets SE11-REQ-06; restart mechanism SE11-REQ-15/20; AVR | SE11, SE20 (drills); electrician for cause (SE11-REQ-10) | none beyond UPS | SE11-NFR-03 met in SE11-AC-06/15; automatic restart within T_restart ≤ 720 s | Accepted: outage = planned-quality downtime, no data loss beyond in-flight work |
| FD-UPS-A | **Abrupt UPS-A output loss** (UPS fault, overload trip, battery failure) or mains loss while UPS communication is lost | Host and switch (and NAS in S-1/S-2) lose power **simultaneously and without warning** | Crash-consistency requirements: journaled guest filesystems, synchronous-commit WAL (SE12), NAS copy-on-write + scrub on restart; restart S5–S6; integrity checks before services start | SE11 (hardware), SE12 (data integrity) | Spare UPS of the §11.4 class; integrity tooling | SE11-NFR-07 met in SE11-AC-13 | Accepted: client-class NVMe without asserted power-loss protection (§6.5); loss bounded to last commit; REV-POWER if drills show unrecoverable corruption |
| FD-UPS-N (S-3 only) | Abrupt UPS-N output loss | NAS only | NAS CoW + scrub | SE11 | Spare UPS class | NAS array integrity after drill | Accepted |
| FD-SIGNAL | UPS signalling path only (USB cable, UPS software, NAS command/notification path) | No immediate workload impact; a later mains loss degrades to FD-UPS-A | E4 handling (§8.3); S-3 topology as fallback; telemetry alert | SE11, SE20 | none | Detected ≤ 300 s; drill SE11-AC-14 passes | Accepted with alerting |
| FD-RESTART | Restart mechanism fails after a shutdown (M1 not executed, RTC alarm not firing, WOL not received) | Devices stay halted although mains is back | M1 preferred; M3 wake-poll loop re-arms until mains or exhaustion; exhaustion-and-return as the ultimate path; M4 residual (§8.3) | SE11, SE20 | Operator presence (M4) | SE11-AC-15: T_restart ≤ 720 s for the selected mechanism in drills (a)–(e) | Accepted only with M1, or M3 + evidenced NAS wake; otherwise recorded exposure (SE11-RISK-12) |
| FD-UPS-B / FD-CIRCUIT-B | UPS-B or circuit B (deferred) | Local workers only | Isolation from PD-A (§165) | SE11 | none | Capacity reduction only | n/a until rack exists |
| FD-ROOM | Rack/room/site (fire, flood, theft) | Total local loss | T3 off-site copy per class; portability to hosted infrastructure (§160, §168) | SE11 (physical), SE12 (T3), EL (hosted fallback) | T3; hosted capacity | D-IRR restored from T3 with loss ≤ `age(c)` (COPY); service rebuilt on hosted/replacement infrastructure | Accepted in `PL-T3`; exposure in other PL states bounded by §6.3 |
| FD-EXT-AI | External AI providers | `pool.agents` work needing external models; no offline AI until B11 adopted | Provider router/fallback and AI-dependency governance (§66, §115, §185); queued jobs resume (§175) | EL (AI/agent architecture, SE11-DEP-02) | Alternative provider per router policy | Queued work resumes without loss | Pending EL; NT16 vendor risk absent (SE11-DEP-09) |
| FD-INTERNET | Uplink / gateway | External providers, hosted runners, hosted T3 transfers, mirrors | Local repositories/mirrors on T2 (§164); local build capacity in `pool.build`; **T3 tolerance = remaining copy-age budget per class (A_max − `age(c)` at outage start), then G of degraded operation, then T3-SUB or write-freeze (§6.3)** | SE11 (physical uplink), SE20 (operations), SE12 (policy) | Single uplink restored | Local runtime continues; protection-state transitions observed exactly as §6.3 prescribes (SE11-AC-07c) | Accepted: single uplink at Stage 1–2; exposure bounded and logged |
| FD-MGMT | Management plane (host admin path, NAS admin, switch mgmt, UPS software, telemetry exporter) | Operator cannot intervene remotely; workloads unaffected; M4 restarts need presence; signal consumers see the contract's "stale" state (§18.2) | Physical console (§10.2); `seg.mgmt` isolation; configuration in version control | SE11, SE20 | Physical presence | Console recovery procedure drilled once per stage | Accepted: no BMC on the consumer-class board (SE11-RISK-04); REV-HA if SLOs require remote recovery |

Dependency-failure behaviour summary: a local infrastructure problem must not corrupt active builds or accepted runtime state; resumable jobs, durable state and idempotent execution are required of every workload placed on these pools (§175) — EL/SE19 implement and prove this; SE11 guarantees only the physical boundaries above and publishes the signals of SE11-DEC-11 under the contract of §18.2.


## 10. Hardware manageability / operability (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-09)

### 10.1 Inventory identity (SE11-REQ-07)

Every physical asset carries an inventory id `CSPUI-HW-<class>-<nn>` (classes: HOST, NAS, HDD, NVME, NIC, GPU, UPS, SW, RACK, PDU, WKR, CABLE, T3SUB) recorded in a version-controlled inventory file owned by SE11, committed to `REPO` (§6.3) and published through `SE11-CONTRACT-hardware-baseline@1` (§18.2). Record fields: inventory id; BOM reference (B1–B19); specification class (§11.4); part number as cited from SEED-01 and its evidence status (DEFERRED-PENDING-EVIDENCE / confirmed / superseded); serial number; firmware/BIOS/driver version at commissioning; physical position (slot id such as `M2_3`/`PCI_E1`, NAS bay, rack U); power domain (PD-A/PD-N/PD-B); failure-domain ids (§9); disposition and quantity status (§1.2); §6.1a row and mapping (D/V) in force with V_min/B_max; signalling candidate and restart mechanism; pre-build evidence record id (§11.3); commissioning evidence ids (§14); warranty end; sanitisation state. Cables are labelled at both ends with the endpoint ids. The **configuration fingerprint** (§11.3) is derived from these records.

### 10.2 Remote-management capabilities where available

| Device | Out-of-band | In-band management path | Fallback |
|---|---|---|---|
| Central host | None (consumer board; no BMC/IPMI) — SE11-RISK-04 | Windows remote administration and Hyper-V management on `seg.mgmt`; MFA per §59 | Physical console in the lockable room; UEFI Flash BIOS and Clear CMOS on the rear panel (B3); RTC wake (M3) if evidenced |
| NAS | None | NAS OS web/remote administration on `seg.mgmt` | Front panel / USB; Wake-on-LAN (N1) if evidenced |
| Switch | Management port if the class provides one | Management VLAN | Console port |
| UPS-A / UPS-N | USB-HID to the host (S-1/S-3) or NAS (S-2/S-3) | Status via the UPS software's telemetry export, re-published by SE11's exporter | Front LCD |

### 10.3 Telemetry and health status (SE11-REQ-08, SE11-NFR-04; published under `SE11-CONTRACT-hardware-signals@1`, consumed by SE20 monitoring, SE01 capacity, SE19 validation, EL scheduler)

Mandatory signals from first power-on ("capture performance/resource telemetry from the first workloads", §160; "capture CPU, memory, I/O, network, queue time, job duration, reliability, and cost", §234): host CPU utilisation per VM and total, CPU-wait per VM, memory committed per VM and host against Table 5.3-R, NVMe SMART (temperature, media errors, percentage used, TBW consumed) per device, per-virtual-disk IOPS and bytes (the summed Build figures against B_max, Validation against V_min) and latency (and `io.max` throttling counters when the guest limiter is in use), PCIe negotiated width/speed per slot (detects degraded M2_3/PCI_E3 sharing), NIC link speed and errors, NAS array state (healthy/degraded/rebuilding), per-drive SMART, NAS volume utilisation, snapshot success, backup and T3 job success/duration/throughput, **per-class `mech_ok(c)`, `t3_last_ok(c)`, `kind(c)`, `age(c)` and protection state, platform `PL-*` state**, UPS state per UPS (online/on-battery/low-battery, load %, runtime estimate, battery charge %, battery age, communication state), restart-mechanism armed/fired/wake-poll events, host and NAS temperatures, switch port utilisation on L1/L2, and the event signals of SE11-DEC-11. **How they are delivered is SE11's contract, not SE20's design:** a metrics endpoint on `seg.mgmt` (pull, text exposition, sample interval ≤ 60 s, no workload content) and an append-only event log (push to a local durable queue in the Core VM with at-least-once delivery and a monotonic sequence number) — both specified in §18.2 Part B so that SE20's monitoring integration is a subscription to a defined interface. Thresholds that trigger expansion or revision are in §12.

### 10.4 Firmware / BIOS / driver lifecycle (SE11-REQ-09)

- Components with a firmware lifecycle: host UEFI/BIOS (incl. CPU microcode/AGESA), NVMe firmware ×4, NIC driver/firmware, optional GPU driver, NAS OS and HDD firmware, UPS firmware and host/NAS UPS software, switch firmware.
- Update path: vendor-signed images only, checksum verified against the vendor publication, staged in a declared maintenance window (§10.5) after a successful snapshot of all VMs and a verified T2 backup; one component class per window; rollback plan recorded; post-update SE11-AC-04 smoke subset executed; firmware settings baseline re-verified (SE11-AC-08a), including "restore on AC power loss", RTC wake and the UPS-command settings of §8.3; configuration fingerprint updated.
- Ownership: SE20 schedules and executes; SE17 defines integrity controls (SE11-SECREQ-02); SE11 keeps the compatibility matrix (§11) current.

### 10.5 Maintenance windows

Hardware maintenance is performed only in a window declared to SE20's operations calendar that does not overlap a stage-gate VP validation (§174 "VP validation / release assurance"). Minimum window content: pre-checks (backup verified, snapshots taken, UPS healthy, all D-IRR classes with real data PROTECTED with kind COPY or the exposure explicitly accepted by SE12), the change, post-checks (SE11-AC-04 smoke, telemetry nominal), inventory record and fingerprint updated.

## 11. Compatibility / availability assessment (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-10)

### 11.1 Structural compatibility check (from the BOM specifications themselves)

| Check | Items | Result from BOM data | Residual verification |
|---|---|---|---|
| Socket / chipset | B1 AM5 ↔ B3 AM5/X870 | Structurally compatible | BIOS version supporting the CPU: **not established** (FC-01) |
| Memory | B4 DDR5 UDIMM ↔ B3 "4× DDR5 DIMM, up to 256 GB" | Compatible at capacity; DDR5-6000 EXPO on four DIMMs is a stability-validated profile, not a guaranteed one (the seed prescribes the 5600/5200 fallback) | Exact population (2-DIMM M-A vs 4-DIMM M-B/M-A+) on the board's qualified list: **not established** (FC-02); stability pass SE11-AC-04 |
| Cooler | B2 157 mm ↔ B8 ~166 mm clearance; AM5 mounting included | Compatible | — |
| Form factor | B3 ATX ↔ B8 ATX/E-ATX | Compatible | — |
| PCIe lane sharing | B10 in PCI_E3 (Gen4 x4, "shares with M2_3") ↔ B5 in M2_3 (Gen4 x2) | Simultaneous operation **not established** from BOM text (FC-03) | SE11-AC-02 read-back; Fallbacks A/B/C, Mapping-V (§6.1a) |
| NIC in PCI_E1 (Fallback A) | B10 PCIe 3.0 x4 card in a Gen5 x16 CPU slot | Electrically and mechanically a subset; **operation not established** (FC-03) | SE11-AC-02 when Fallback A is used |
| M2_2 ↔ USB4 sharing | B6 on M2_2 ("sharing with USB4") | USB4 unused at baseline; no conflict | Confirm USB4 use does not down-shift M2_2: SE11-AC-02 |
| PSU | B7 750 W, 12V-2x6 ↔ B1 230 W + B11 145 W + platform | Within rating for the no-GPU build; GPU build conditional on measurement (seed condition) | SE11-AC-06 |
| GPU mechanical | B11 single-slot 241 mm ↔ B8 mid-tower, PCI_E1 x16 | Expected to fit; not asserted | SE11-AC-02 before adoption |
| NAS memory | B13 DDR5-4800 ECC SO-DIMM ↔ B12 "2 slots; 64 GB max"; mixed 16 + 32 GB | Capacity compatible; mixed pair support **not established** | SE11-AC-01 (deferred item) |
| NAS drives | B14 3.5-inch SATA CMR ↔ B12 8 SATA bays | Compatible | Online RAID 6 expansion support: **not established** (FC-08) |
| Network | B10 10GBase-T ↔ B12 2×10 GbE; Cat6a supplied with NAS (§228.1) | Compatible | Switch class 10GBase-T or SFP+ with matching transceivers: SE11-AC-05 |
| UPS | B15 1000 W ↔ PD-A loads (§8.2); NEMA 5-15P ↔ 15 A circuit (§231) | Compatible; runtime unknown until measured | SE11-AC-06 |
| UPS signalling and restart | B15 USB-HID / host software ↔ B12 network UPS server; commanded output power-cycle (M1); NAS client wait ≥ 240 s (S-2); RTC wake from soft-off (M3); NAS WOL (N1) | **Not established** (FC-09) | SE11-AC-01, SE11-DEC-10, SE11-DEC-13/17 |
| OS / virtualization | B9 Windows 11 Pro ↔ Hyper-V; TPM 2.0 + Secure Boot prerequisites; Linux guest support; NIC driver for the virtual switch; per-virtual-disk IOPS controls; guest cgroup v2 `io.max` | Hyper-V is a Pro feature; TPM/Secure Boot are install prerequisites so the platform must provide them; NIC driver (FC-05) and storage-QoS availability (FC-06) **not established**; cgroup v2 `io.max` is a Linux guest facility whose availability on the chosen distribution is confirmed in SE11-AC-03 | SE11-AC-01, SE11-AC-03 |

### 11.2 Current manufacturer support and practical availability — NOT ESTABLISHED; outcome UNMET (corrects finding 008)

The allowed corpus contains no manufacturer support statement, firmware/BIOS release information, qualified-vendor list, driver compatibility statement or market availability for any BOM item, and SE11 has no access to manufacturer publications in this run. For every item the following are therefore **not established** and **not asserted** (BND-04): current manufacturer support status; a BIOS version supporting the CPU; the exact memory population on the board's qualified list; simultaneous PCI_E3/M2_3 operation; NIC driver support for the hypervisor virtual switch; hypervisor storage-QoS availability on the host OS edition; UPS software ↔ host OS, NAS ↔ UPS protocol, commanded output power-cycle, RTC wake and NAS WOL support; NAS online array expansion; practical availability of any part number.

**What the class baseline does and does not do (SE11-DEC-14).** Deferring every part number (B1–B17: DEFERRED-PENDING-EVIDENCE, §1.2) and baselining specification classes (§11.4) prevents this document from fixing an unverified part-number combination. It does **not** demonstrate that a coherent, currently supported configuration of those classes exists: the conditions below are class-level feasibility conditions that only dated, attributable pre-build evidence can close. Until SE11-AC-01 records at least one coherent supported configuration (or supported alternative within class), **QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 is UNMET** (§0.3), no buildable bill exists, the configuration fingerprint is empty, and the baseline stays PROVISIONAL (§17).

**Open class-level feasibility conditions (each closed only by the stated evidence; failure consequence stated):**

| Id | Condition that must hold for the architecture to be buildable | Evidence that closes it (dated, attributable, recorded in §11.3) | If it fails |
|---|---|---|---|
| FC-01 | A board of the B3 class ships or can be updated to a BIOS that supports the B1-class CPU with the required virtualization/IOMMU, Secure Boot, TPM 2.0, AC-recovery and RTC-wake settings | Board manufacturer BIOS release notes / CPU support list for the exact board and CPU; firmware settings reference | Substitute board or CPU within class (new SE11-DEC) |
| FC-02 | The chosen memory population (2-DIMM M-A; 4-DIMM M-B/M-A+) is on the board's qualified list or validated at ≥ DDR5-5200 | Board qualified-vendor list entry for the kit and population; else SE11-AC-04 stability pass at the fallback speed | Smaller population or different kit within class; M-A+ path re-validated |
| FC-03 | PCI_E3 (x4 NIC) and M2_3 (x2 NVMe) operate concurrently, **or** a Gen3 x4 NIC operates in the Gen5 x16 CPU slot (Fallback A), **or** Fallback C's x1 path still meets SE11-REQ-04 | Board manual lane-sharing statement; SE11-AC-02 read-back | Fallback B (scratch on M2_2) with its storage consequences; Mapping-V unavailable under B |
| FC-04 | The host OS edition supports the Hyper-V role with the per-VM reserve/limit/weight and static/dynamic memory controls used in §4–§5 | Host OS feature documentation for the exact edition/version | Edition change within the B9 class (new SE11-DEC) |
| FC-05 | The NIC class has a driver supporting the hypervisor virtual switch at 10 Gb/s on the host OS version | NIC vendor driver support statement; SE11-AC-03 | Different 10 GbE NIC within class (SFP+ allowed with matching switch) |
| FC-06 | Per-virtual-disk storage QoS is available on the host OS edition — else the guest `io.max` limiter is available on the chosen Linux distribution | Host OS / distribution documentation; SE11-AC-03 | The §6.1a "QoS unavailable" rows apply; if neither limiter exists, Validation may not share a device with Build → Mapping-V mandatory or R2 |
| FC-07 | (Only when TRG-GPU fires) a supported path exposes the B11-class GPU to a Linux VM on the client hypervisor | Hypervisor and GPU vendor documentation | Host-level model service fallback (§5.5) |
| FC-08 | The NAS OS supports online RAID 6 expansion from the N-A count, UPS integration per the selected candidate, power-on after AC recovery and (for M3) Wake-on-LAN | NAS OS feature documentation for the exact version | N-B installed from the start (recorded deviation from N-A) ; S-3; N1 unavailable → M1 mandatory or NAS attended |
| FC-09 | The UPS class, with the host/NAS software at the exact versions, supports the selected signalling candidate, commanded output shutdown with auto-restart (M1), and the board supports RTC wake from soft-off (M3) | UPS vendor software documentation; board manual; SE11-AC-15 | Candidate change (S-3); mechanism change (M3); if neither M1 nor M3 can be evidenced, SE11-REQ-15 is unmet and the stable-runtime baseline is blocked (§8.4) |

### 11.3 Pre-build support evidence record (SE11-AC-01) and baseline selection / configuration fingerprint

**Pre-build evidence register (template; one row per item and claim; every row is NOT PERFORMED at v4):** item (B-id); part number as cited; claim checked (the FC-nn condition and/or the per-item claims: support status, BIOS/firmware version, qualified population, slot coexistence, driver/OS/hypervisor support, storage-QoS and guest `io.max` availability, UPS protocol, M1, S-2 client wait, RTC wake, N1, NAS online expansion, availability); source (publisher, document title/version, date accessed); result (confirmed / not confirmed / superseded); consequence (confirmed into the fingerprint / substitute within class with a new SE11-DEC / defer); recorder; date. "Not confirmed" on any item keeps that part number deferred; a superseded item is substituted by specification class and recorded (SE11-REQ-12).

**Baseline selection record (separate from commissioning evidence).** When SE11-AC-01 completes, SE11 records *one* coherent configuration — the ordered list of (B-id, confirmed part number or in-class substitute, evidence row ids closing FC-01 … FC-09 as applicable, memory candidate M-x, NAS candidate N-x, signalling S-x, restart M-x/N-x) — as **configuration fingerprint v0**. That record is the sole basis on which QC-AR-03 can later be reported met; it is produced before any purchase or build and is independent of the commissioning tests. **At v4: fingerprint v0 does not exist; no selection has been made; no evidence row exists.**

**Commissioning tests (after build, §14):** SE11-AC-02 … SE11-AC-15 measure what the built configuration actually does; they never substitute for the pre-build record. The fingerprint is updated to v1 at SE11-AC-10 with serials, firmware versions, slot positions, the §6.1a row/mapping in force, protection-state defaults A_max/G and the evidence ids. Any change to the fingerprint re-opens SE11-AC-01 for the changed item and SE11-AC-10 for the baseline.

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
| B12 NAS | 8-bay SATA NAS with ECC memory, ≥ 2×10 GbE, Btrfs/ZFS-class snapshots, per-folder/volume AES-256, UPS integration (any of S-1/S-2/S-3), power-on after AC recovery, Wake-on-LAN preferred, M.2 cache slots; hosted object storage is the equivalent for T2/T3 under G-LOCAL |
| B14 HDD | 3.5-inch enterprise CMR, 7,200 RPM, ≥ 2.5 M h MTBF, ≥ 550 TB/yr workload, 5-year warranty, ≥ 20 TB (smaller same-class drives permitted under N-A if V is small) |
| B15/B16 UPS | Pure-sine line-interactive with AVR, USB-HID, ≥ 1500 VA / 1000 W (PD-A) and ≥ 1000 VA / 600 W (PD-N / PD-B), user-replaceable batteries, commanded output shutdown with auto-restart on mains (M1) and configurable restart delay preferred; higher-runtime units of the same class are the remedy under §8.4 |
| B17 switch | Managed L2+, ≥ 2×10 GbE (≥ 4 preferred), 24× ≥ 1 GbE access, VLAN, port mirroring for SE17/SE19 |
| T3-SUB medium | Removable encrypted medium or second independent location sized to the D-IRR set (§6.3) |

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

### 12.3 Scale-out versus scale-up boundaries and architecture-revision triggers

The central node complements, never replaces, horizontally scalable workers (§177). Scale-out (more workers, hosted executors) is the default answer to throughput; scale-up applies only to the capabilities the seed assigns to the central node — large contiguous RAM, low-latency CPU, NVMe, centralized data/control services (§161). The following require a revision of this architecture (new SE11 version plus EL review), not a hardware addition:

| Revision trigger | Why adding hardware is insufficient |
|---|---|
| REV-MEM: §5.3 Step 4 (1.25 F > 256 GB with hosted placement inadmissible), or Highest-priority pool floors exceed 85 % of 256 GB on measured p95 | Board ceiling reached; second host, larger-memory platform class, or data-tier redesign is an architectural choice |
| REV-HA: an SLO (§117) requires the control plane or Data VM to survive FD-HOST or FD-NVME-M2_4, or requires unattended restart that no evidenced mechanism provides | Needs a second failure domain and quorum design (§173) |
| REV-GPU-CLASS: accelerator > 145 W, dual-slot, or second accelerator | Exceeds PSU, slot and thermal envelope (§5.5) |
| REV-STORAGE-HOT: T1 > 85 % after device scale-up; a random-IO workload that cannot stay on host NVMe; §6.1a remedy R2 (Validation's demand cannot fit beside Build and Mapping-V is unavailable or insufficient) | NAS is not a hot tier (§164); host NVMe topology exhausted |
| REV-STORAGE: retention volume V > 44 TiB (§6.7) | Beyond the enclosure's economical RAID 6 envelope; hosted tier or second enclosure is architectural |
| REV-NET: storage/core path saturated after all 10 GbE ports used, or 25 GbE class needed | Switch and NIC class change ripples through host slots |
| REV-SITE: geographic/resilience footprint beyond one room (§226 F.20) | Hosted/hybrid footprint decision |
| REV-POWER: §8.4 remedies exhausted, PD-A measured peak within 20 % of UPS-A rating, circuit limits reached, or no admissible restart mechanism meets the SLO | UPS/circuit redesign by qualified professionals; possible relocation |

## 13. Security considerations (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-11)

The owners of the control catalogue (SE17 for infrastructure/workload/data security, SE15 for identity and cryptography, §74) have not published control ids in this run (their documents are absent, §0.1). This section therefore does two separable things (corrects finding 003's security part): **(a)** it states the hardware security requirements under SE11's identifiers and, for each, the check that **SE11 itself executes and can pass without any owner catalogue** (SE11-REQ-19, SE11-AC-08a) — these are implementable from this document alone; **(b)** it names what remains the owner's (policy, control ids, custody, identity) as placed requirements, unmet dependency SE11-DEP-05, verified later as SE11-AC-08b. No foreign control id is invented; nothing re-derives a control design.

| Id | Requirement placed on the hardware baseline | (a) SE11-executable check (SE11-AC-08a) — pass criterion | (b) Owner part (SE11-AC-08b, UNMET until SE11-DEP-05) |
|---|---|---|---|
| SE11-SECREQ-01 Trusted boot | UEFI Secure Boot enabled; TPM 2.0 present and enabled; boot order locked to M2_1; UEFI administrator password set; the RTC-wake and AC-recovery settings of §8.3 are part of the protected firmware baseline | Firmware settings export shows Secure Boot = on, TPM 2.0 = enabled and owned, boot order = M2_1 only, admin password = set, AC-recovery = power on, RTC wake = enabled; host OS reports Secure Boot state on; export checksum recorded in the fingerprint | SE17: measured-boot attestation decision and control id |
| SE11-SECREQ-02 Firmware integrity | Vendor-signed images only, checksum verified, staged in maintenance windows with snapshot + verified backup first (§10.4); firmware settings baseline re-verified after every BIOS update | Each firmware record in the inventory carries the vendor checksum and the verification result; post-update settings export matches the baseline | SE17 (policy, control id), SE20 (execution) |
| SE11-SECREQ-03 Management-plane isolation | All management endpoints (host admin, hypervisor, NAS admin, switch, UPS software, telemetry exporter, shutdown/WOL command paths) only on `seg.mgmt`, unreachable from `seg.build`, `seg.worker`, `seg.egress`; no management interface exposed to the internet; the NAS shutdown command (S-1) is authenticated | Port-scan from a host in each of `seg.build`, `seg.worker`, `seg.egress` reaches no management endpoint; from the gateway side no management port is reachable; the NAS shutdown command fails without credentials (SE11-AC-05 segmentation log) | SE17: inter-segment policy and control id; SE15: MFA, least-privilege, short-lived credentials per §59/§112 |
| SE11-SECREQ-04 Physical and administrative access | Lockable room; host, NAS, switch and UPS inside; the T3-SUB medium outside it; physical console use is a logged administrative action; segregation between hardware maintenance (SE11/SE20) and security configuration (SE17) per §112 | Room lock verified; devices inside recorded by inventory position; console sessions appear in the host audit log | SE17: custody rule for T3-SUB, access-control id, segregation control |
| SE11-SECREQ-05 Data at rest | Host full-disk encryption on M2_1 with TPM-bound keys; encryption of VM disks on M2_2/M2_3/M2_4 inside the Linux VMs or by the hypervisor (hardware supports both); NAS per-folder AES-256 (B12) for backups, evidence and archives; T3 and T3-SUB copies encrypted before leaving the site; the `KEYS` class under §6.3 | Host volume reports encryption on with TPM protector; each VM disk or guest volume reports encryption on; NAS shares for T2 report encryption on; a T3/T3-SUB object sampled at rest is ciphertext | SE17/SE15: key custody, recovery and the offline custody secret for KEYS; control ids |
| SE11-SECREQ-06 Media sanitisation | NVMe, HDD and T3-SUB media sanitised on decommissioning/RMA; inventory record marks sanitised state | Inventory field present and required for state "decommissioned" | SE17: sanitisation standard and control id |
| SE11-SECREQ-07 Supply chain at receipt | Serial numbers recorded; packaging/tamper evidence inspected; firmware version read and compared with the vendor's published current version before first power-on; default credentials on NAS, switch and UPS software rotated at commissioning | Receipt record per asset with serial, inspection result, firmware version and comparison; credential rotation logged | SE17: supply-chain control id |
| SE11-SECREQ-08 Confidential-processing boundary | Private application/customer data is processed only by authorised locally hosted models or deterministic tools (§66); any local accelerator (B11) and the Data VM sit inside `seg.platform` behind the default-deny disclosure gateway on `seg.egress`; hardware telemetry export (§10.3) carries no workload content; candidate M-C (hosted data) is admissible only where §66 permits | Telemetry payload sampled during SE11-AC-09 contains only the §10.3 fields; `seg.platform` has no route to `seg.egress` except via the gateway address (SE11-AC-05) | SE17/EL: gateway policy, control id; §66 applicability decision for M-C |


## 14. Validation / evidence plan (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-14)

Pre-build checks (AC-01, AC-11) are separate from commissioning tests (AC-02 … AC-15); commissioning never substitutes for the pre-build record (§11.3). Executing owners are named; where the owner's test or operations contract does not yet exist the dependency id is given. Every acceptance record is committed to `REPO` (§6.3), so no evidence depends on a protection class that does not yet exist.

| AC id | Check | Pass criterion | Evidence artefact | Executing owner | Needed before |
|---|---|---|---|---|---|
| SE11-AC-01 | **Pre-build** support, compatibility and availability evidence record (§11.3) | Every B1–B17 item has a dated, attributable record for each claim in §11.3; every applicable FC-01 … FC-09 condition closed or its failure consequence applied; part numbers move from DEFERRED-PENDING-EVIDENCE to confirmed, substituted within class (new SE11-DEC) or deferred; signalling candidate S-1/S-2 evidenced or S-3 adopted; restart mechanism M1 or M3 (+N1) evidenced — else SE11-REQ-15 recorded unmet; S-2 NAS client wait ≥ 240 s evidenced if S-2; receipt check (SE11-SECREQ-07) complete; **configuration fingerprint v0 recorded as the baseline selection** | Evidence register rows; fingerprint v0 | SE11 (SE20 assists at receipt) | Any build; QC-AR-03 closure |
| SE11-AC-11 | **Pre-build** reconciliation of this document to PL-REQ-ID-REGISTER rows (via the §0.5 crosswalk) and to EL/PM09/NT16/SP16 decisions once they exist (SE11-DEP-01/02/08/09/10); registration of the §18.2 contracts in SE11-INTERFACE-CONTRACT and EL's register | Every row of §0.5 carries a register id; every ADR checked against EL ADRs; NFR values bound to EL/PM09 NFR ids or recorded as conflicts; C1–C6 resolved by reviewers; contracts registered; status PROV → REC | Reconciliation table and registration references in a later version of this document | SE11, EL review | Baseline status above PROVISIONAL |
| SE11-AC-02 | Slot, lane and mechanical verification | Negotiated PCIe width/speed for M2_1–M2_4 and the NIC slot with all devices installed; PCI_E3/M2_3 coexistence confirmed or Fallback A/B/C invoked and recorded (SE11-DEC-02/12); cooler/case clearance photos; GPU mechanical check when B11 is triggered | Link-state dump; inventory photos | SE11 | Stage 1 |
| SE11-AC-03 | OS / virtualization enablement and reservation mechanism | Hyper-V operational with the four VMs at the §4 reserve/limit/weight settings and the Table 5.3-R memory lines of the installed candidate; admission formula Req ≤ Installed (§5.2) encoded in version-controlled definitions; hypervisor storage QoS present **or** guest `io.max` limiter configured on `build.slice` per the §6.1a row and shares in force; NIC bound to the virtual switch at 10 Gb/s; Secure Boot + TPM reported enabled; "restore on AC power loss" and RTC wake settings verified; GPU-to-VM path evaluated when triggered | Hypervisor and guest configuration export | SE11 with EL (SE11-DEP-02) | Stage 1 |
| SE11-AC-04 | Burn-in and performance baseline (SE11-NFR-08) | ≥ 24 h combined CPU/memory/NVMe stress with zero memory errors at the chosen DDR5 profile (fallback 5600/5200 per B4) at the installed population; thermals within limits; NVMe sequential/random, **D2, S2 and L2 for M2_2 and D3/L3 for M2_3 (§6.1a)**, per-virtual-disk and L1 throughput recorded as the measured replacement for §6.4 | Stress logs; telemetry export; baseline table | SE19 (executes, SE11-DEP-06), SE11 (accepts) | Stage 1 |
| SE11-AC-05 | Network path and segmentation (SE11-NFR-02, SE11-SECREQ-03) | Host↔NAS ≥ 0.7 GB/s sustained 10 min under concurrent build-cache load **with the NIC in the slot actually in use** (Fallback C admissible only on pass); `seg.*` enforced; management plane unreachable from build/worker/egress segments; NAS shutdown command rejected without credentials | Throughput log; segmentation test log | SE11 (physical design/test and the SE11-SECREQ-03 check), SE17 (policy, SE11-DEP-05), SE19 (measurement) | Stage 1 |
| SE11-AC-12 | CPU contention and weighted-service test (SE11-NFR-01) | Profile: Build VM 100 % CPU on all 16 vCPU, Validation VM 100 % on 8 vCPU, `pool.background` saturating inside Build, host root busy, T1→T2 backup transfer running on L1; measured: Core/Data CPU-wait ≤ 5 %, Core probe p95 ≤ 1.5 × baseline, Data random-read p99 ≤ 2 × baseline, Validation CPU-wait ≤ 10 %, Build ≥ 11 LP-equivalents, background ≤ 10 % of Build VM CPU | Load-test report with per-VM CPU share | SE19 (executes), SE11 (accepts) | Stage 1 before stable-runtime baseline |
| SE11-AC-12b | Storage budget, contention and critical-validation I/O test (SE11-REQ-16, SE11-DEC-16) | For the §6.1a row in force, four cases: **(i) default calibration** (V_min = 0.20 D2, B_max = 0.60 D2): Build drives every M2_2-backed virtual disk (`bld-sys`, `bld-ws`, `bld-art`, and `bld-scr` where on M2_2) at queue depth 32 for 10 min **plus a root/system I/O generator on `bld-sys` outside `build.slice`**; Validation 4 KiB random-read p99 ≤ 2 × L2 and achieved IOPS ≥ V_min throughout; hypervisor-summed Build IOPS and bytes ≤ B_max (+5 %) in every 60 s window; limiter counters show the per-device caps; **(ii) elevated demand**: Vdem set to 0.30 D2 → V_min = 0.45 D2, B_max = 0.35 D2 re-applied; same criteria; **(iii) infeasible-demand drill**: Vdem set to 0.45 D2 → the admission rule must refuse the row (V_min + B_floor > A) and the recorded remedy must be R1 or R2; where R1 applies, **(iv) Mapping-V**: Validation alone on M2_3 at its measured demand (p99 ≤ 2 × L3) while Build runs at B_max = 0.80 D2 on M2_2 with all disks including `bld-scr`; summed Build traffic ≤ B_max. Any failed case → the row is inadmissible; apply the row's remedy column | fio/latency report per disk; limiter configuration; hypervisor counter sums per window | SE19 (executes), SE11 (accepts) | Stage 1 before any Validation workload shares a device with Build |
| SE11-AC-06 | Power measurement and mains-loss drills (SE11-NFR-03; fail-closed §8.4) | Measured load of every power domain (idle, host-only boot, typical, full stress, with/without GPU); measured runtime R_u for every UPS of the selected candidate at full-stress load (**S-3: R_N measured separately at NAS load**); drills: (a) full outage past exhaustion — S1 → S6 with every step inside its bound and B_u ≤ 0.7 R_u; (b) mains restored during S1 — return to S0, no shutdown; (c) mains restored at S2 entry — sequence completes unaborted, restart via the selected mechanism with T_restart ≤ 720 s; (d) mains restored in S3/S4 before output drop — same; (e) second outage while charge < 50 % — host-only shutdown within 90 s, no VM start; (f) S-2 only: NAS waits ≥ 240 s for the client; VMs and NAS return clean in every drill; electrician's sign-off of circuits on file (SE11-REQ-10) | Power table per domain; drill log with timestamps per step and scenario; professional sign-off reference | SE11 (measurement), SE20 (drill, SE11-DEP-07), qualified electrician (circuits, SE11-DEP-12) | Stage 1 before stable-runtime baseline |
| SE11-AC-15 | Restart-mechanism drill (SE11-REQ-15, SE11-REQ-20, FD-RESTART) | Measured T_boot, T_decide, T_hostonly_off, D_on replace ASM-SE11-13. **M1:** outputs drop 60–120 s after the last device on that UPS is off, for every UPS of the candidate (S-1: ≈ 330 s; S-2: ≈ 420 s; S-3: 330 s / 240 s); re-energise on mains after D_on; host and NAS auto-power-on; T_restart ≤ 720 s in drills (a) restoration at S2 entry, (b) restoration after output drop, (d) restoration after exhaustion. **M3:** (a) restoration at S2 entry → first wake restores within 660 s; (b) **restoration immediately after an unsuccessful on-battery wake decision while UPS output remains energised** → the re-armed alarm restores within 540 s; (c) restoration during a host-only boot → S6 within 150 s; (d) UPS exhaustion during the loop → AC-cycle restart when mains returns; (e) UPS unreadable at a wake → treated as on-battery, re-armed; N1 wakes the NAS and the Data VM waits ≤ 300 s for it. Any M3 drill in which the host stays halted with mains present is a fail. **M4:** alert delivered and procedure documented — recorded as exposure, never a pass for SE11-REQ-15 | Drill log; UPS event log; RTC/wake log | SE20 (drill), SE11 (accepts) | Stage 1 |
| SE11-AC-14 | Signalling-path-loss drill (FD-SIGNAL) | (a) USB/UPS-software path removed while on mains: alert ≤ 300 s; (b) S-1 NAS command path removed during S2: host completes its sequence inside 270 s and the NAS follows its own fallback; (c) S-2 NAS→host notification path removed: host treats as E4; (d) communication lost then mains lost: outcome recorded as abrupt loss and handled by SE11-AC-13 | Drill log | SE20 (drill), SE11 (accepts) | Stage 1 |
| SE11-AC-13 | Abrupt-loss drill (FD-UPS-A / FD-UPS-N, SE11-NFR-07) | UPS output removed under the SE11-AC-12/12b contention profile; on restart every VM and host filesystem and the NAS array pass integrity checks with zero unrecoverable errors; database loss ≤ last committed transaction (SE12 verifies, SE11-DEP-04); scrub completes | Integrity-check logs; SE12 verification record | SE19/SE20 (drill), SE12 (data), SE11 (accepts) | Stage 1 before any real D-IRR admission |
| SE11-AC-07a | T1→T2 protection (`PL-T2`) | Snapshot + replication verified; restore of a VM and a database from T2 to a clean volume within SE11-NFR-05 (SE12's binding RTO if stricter); NAS single-drive pull with rebuild time recorded (replaces ASM-SE11-04) | Restore drill log; rebuild timing | SE12 (policy, SE11-DEP-04), SE19/SE20 (drill) | Stage 1 |
| SE11-AC-07b | T3 **mechanism** verification per D-IRR class on a synthetic fixture (→ ARMED, §6.3) | For each class: T3 mechanism commissioned; a synthetic fixture of the class copied, copy interval ≤ A_max demonstrated, restored from T3 and compared; T3 and T3-SUB encryption and key recovery verified (for KEYS: under the offline custody secret); T3-SUB copy and restore of the fixture verified; `mech_ok(c)` published; **no real dataset of the class exists at the time of the test** | T3 inventory; fixture restore log | SE12 (policy), SE17 (keys), SE20 (drill), SE11 for REPO | **Before the first real dataset of that class is admitted** (REPO: before local commissioning; DB/EVID/KEYS: before non-synthetic data enters the platform) |
| SE11-AC-07c | Protection-expiry drill (§6.3, FD-INTERNET) | Starting with a class at `age` = A_max − 1 h, cut the T3 path: DEGRADED-IN-BUDGET at +1 h with `SIG-PROTECTION-STATE` raised ≤ 60 s and creation of a new dataset of that class refused by the owning store; EXPIRED at +25 h with either a T3-SUB copy ≤ A_max old permitting mutation or the data-store owner's write-freeze observed (SE11-REQ-18); restore the path: full copy, restore verification, PROTECTED(COPY), freeze lifted. **SE11's own pass criterion** is limited to the signal timing and state transitions it publishes; the refusal and freeze observations are the owners' pass criteria (unmet until SE11-DEP-02/04) and are recorded as such | Drill log with state transitions and permission checks | SE20 (drill), SE12 and EL (enforcement, SE11-DEP-02/04), SE11 (accepts its part) | Stage 1 before any D-IRR class other than REPO holds real data |
| SE11-AC-07d | **From-empty-platform activation** (SE11-DEC-18) | Starting at `PL-0` with no real D-IRR data: (1) REPO: hosted remote configured in the host build, first commit = fixture → ARMED → first real commit → PROTECTED(ANCHOR) → push verified → PROTECTED(COPY); (2) SE11-AC-07a → `PL-T2`; (3) KEYS: fixture key under the custody secret → ARMED → real custody created → ANCHOR → immediate copy → COPY; (4) DB: synthetic DB fixture → ARMED → first real database admitted by SE12's store → ANCHOR → initial copy within A_max → COPY; (5) EVID similarly; (6) platform reaches `PL-T3` with every transition logged and **no step requiring an exemption from SE11-REQ-13/17**; (7) a negative check: an attempted real-dataset creation while the class is MECH-UNVERIFIED is refused | Activation log with per-class state history | SE20 (drill), SE12/SE17/EL (their stores), SE11 (REPO and acceptance) | Stage 1 before `PL-T3` is claimed |
| SE11-AC-08a | Security baseline — SE11-executable checks (SE11-REQ-19, §13 column a) | Every SE11-SECREQ-01 … 08 check in column (a) passes against the inventory ids; default credentials rotated; firmware settings export checksum in the fingerprint | SE11 check log referencing inventory ids | SE11 (SE20 assists) | Stage 1 (host, NAS); full at Stage 3 |
| SE11-AC-08b | Security baseline — owner controls (§13 column b) | Each SE11-SECREQ mapped to an owner control id with the owner's evidence | Owner control evidence referencing inventory ids | SE17 (SE15 for keys/identity; SE11-DEP-05) | Stage 3; UNMET until SE11-DEP-05 |
| SE11-AC-09 | Telemetry coverage (SE11-NFR-04) | Every §10.3 signal and every SE11-DEC-11 event visible at the §18.2 Part B endpoint/event log with the contract's semantics (sequence numbers monotonic, stale flag after 180 s silence, payload carries no workload content); SE20 alert thresholds from §12.2 and the per-class protection states configured on top of it | Exporter conformance log; dashboard/alert export | SE11 (exporter conformance), SE20 (monitoring, SE11-DEP-07) | Stage 1 |
| SE11-AC-10 | Inventory and baseline sign-off | Inventory complete; configuration fingerprint v1 recorded; platform in `PL-T2` (no real D-IRR) or `PL-T3` (all real classes PROTECTED with COPY) — never `PL-T3-PENDING`/`PL-DEG`/`PL-EXP`; §6.1a row/mapping and restart mechanism recorded; §17 record filled with evidence ids of AC-01 … AC-15; baseline contract record (§18.2) updated | Signed baseline record | SE11 | Before downstream consumption as "VERIFIED" |

Resilience tests beyond the above (fault injection on `pool.validate`, switch loss, NAS loss, provider loss, uplink loss) are specified and run by SE19 against the §9 domains; SE11 supplies the physical means (spare cables, drive-pull and power-cut procedures) and accepts the evidence.

## 15. Exclusions (BND-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01 … AR-04)

| Exclusion | Disposition in this document |
|---|---|
| BND-01 Purchase orders, price negotiation, vendor-selection scorecards, procurement workflow | Excluded. No prices, suppliers, order quantities or purchase approvals appear; part numbers are cited only as the seed's reference exemplars and are not baselined (SE11-DEC-14); alternatives are by specification class (§11.4). Nobody owns procurement in this chain. |
| BND-02 Project-owned acquisition dates | Excluded. Only dependency windows are referenced ("Stage 1", "before the first real dataset of the class"); no calendar dates. |
| BND-03 Detailed software/container/service design owned by existing SE11 artefacts | Excluded. §4–§6 stop at pools, VM boundaries, hypervisor reservation controls, limiter configuration, cgroup budget boundaries and volume mapping; service design, images, pipelines and the scheduler's shedding controller are referenced to EL and SE11's runtime artefacts. The exporter/event interface of §18.2 is an interface contract, not a service design. |
| BND-04 Unverified assumptions presented as confirmed hardware facts | Complied with. Every non-seed figure is an engineering assumption (ASM-SE11-nn) or a validation gate (SE11-AC-nn); support, compatibility and availability are explicitly **not established** (§11.2, FC-01 … FC-09) and part numbers are deferred; no vendor protocol, restart or compatibility capability is asserted (§8.3); no claim that the class baseline is feasible is made. |

