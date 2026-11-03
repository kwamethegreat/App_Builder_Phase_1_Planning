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

