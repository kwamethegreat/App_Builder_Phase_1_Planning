---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 3
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-REQ-13, SE11-REQ-14, SE11-REQ-15, SE11-REQ-16, SE11-REQ-17, SE11-NFR-01, SE11-NFR-02, SE11-NFR-03, SE11-NFR-04, SE11-NFR-05, SE11-NFR-06, SE11-NFR-07, SE11-NFR-08, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-DEC-09, SE11-DEC-10, SE11-DEC-11, SE11-DEC-12, SE11-DEC-13, SE11-DEC-14, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-ADR-08, SE11-ADR-09, SE11-ADR-10, SE11-SECREQ-01, SE11-SECREQ-02, SE11-SECREQ-03, SE11-SECREQ-04, SE11-SECREQ-05, SE11-SECREQ-06, SE11-SECREQ-07, SE11-SECREQ-08, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-RISK-09, SE11-RISK-10, SE11-RISK-11, SE11-RISK-12, SE11-RISK-13, SE11-AC-01, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-08, SE11-AC-09, SE11-AC-10, SE11-AC-11, SE11-AC-12, SE11-AC-13, SE11-AC-14, SE11-AC-15, SE11-DEP-01, SE11-DEP-02, SE11-DEP-03, SE11-DEP-04, SE11-DEP-05, SE11-DEP-06, SE11-DEP-07, SE11-DEP-08, SE11-DEP-09, SE11-DEP-10, SE11-DEP-11, SE11-DEP-12, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05, ASM-SE11-06, ASM-SE11-07, ASM-SE11-08, ASM-SE11-09, ASM-SE11-10, ASM-SE11-11]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v3 (revision of v2 after review findings REVIEWER-EN-SE11-PHYSICAL-001 … 006, 008, 009) · **Owner:** SE11 (Infrastructure, Containers & Runtime Engineering, SEED-01 §74) · **Run:** SMK-20261103114255 · **Baseline state:** PROVISIONAL, specification-class baseline, no part-number fingerprint (§0, §11, §17)

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and reference BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite by this document id and the disposition they rely on. It selects no vendor, prices nothing and purchases nothing (§15).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`), consumed sections: hardware strategy §152–§177 (document sections 37–45, including the section-40 reference-configuration table inside §160), the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note at the end of §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231), the guardrails Appendix H (§232–§238) and the domain list §74. No BOM content is recreated from memory; every specification cited below is taken from those sections, re-read in this revision.

## 0. Document status, source availability and limitation

### 0.1 Inputs: what was available and what was not (re-verified for v3)

| Input (context id) | Availability at authoring (v3) | What SE11 needed from it | Effect of absence on this document |
|---|---|---|---|
| PL-REQ-ID-REGISTER (required source) | **Absent** — context block marked "missing"; `list_documents 10-Product-Lead/` returns no files | Requirement / decision / constraint ids with full specification and seed section | **UNMET SOURCE (SE11-DEP-01).** Not "inapplicable": the register applies and is required. The maximum achievable mapping with the inputs that do exist is pre-built in §0.5 (a seed-section crosswalk keyed exactly as register rows are keyed); no register id is cited or invented. The restriction on implementation (§17) stays until SE11-AC-11 attaches register ids. |
| PL-REQ-REGISTER-G01 … G04 (register fragments) | **Absent** (index lists 60 chars, 0 sections) | Verbatim BOM appendix | BOM read directly from SEED-01 §227–§231, which the hardware chain rule permits for SE11. |
| PM09-* (14 product documents) | **Absent** (`list_documents 20-Product-Domains/PM09/` empty) | MVP scope, product NFRs, acceptance criteria, risks/constraints, decision log, KPIs | Product-level targets are not reconciled. Every NFR value in §3 is an SE11 engineering proposal (ASM-SE11-06). |
| NT16-* (8 vendor/dependency documents) | **Absent** | External-dependency and SLA requirements, exit/replacement assessment | External-provider residual risks (FD-EXT-AI, FD-INTERNET, hosted equivalents, T3 provider) are stated from the seed only (SE11-DEP-09). |
| EL-* (26 engineering-lead documents) | **Absent** (`list_documents 40-Engineering-Lead/EL/Outputs/` empty) | System/runtime/deployment/reliability architecture, NFR ids, ADRs, interface-contract governance, estimates, sequencing, DoR/DoD | No EL decision id is cited; no EL review has occurred; the provided contract is DEFINED-UNREGISTERED (§18.2, SE11-DEP-02). |
| SP16-* (7 FinOps documents) | **Absent** | Cost allocation, spend guardrails, unit economics | The economic half of the seed's justification rule for local capacity (§238) cannot be evaluated; local-versus-hosted stays open per pool (SE11-ADR-01, gate G-LOCAL, SE11-DEP-08). |
| SEED-01 (seed, read on demand) | Available | Hardware strategy and BOM | Sole substantive input of this version. The seed is also the common root from which every absent upstream document would have been derived, so the consistency checks of §0.5 are run against it. |

### 0.2 Decision status model

Every decision, requirement and NFR in this version carries the status **PROV** (provisional, seed-derived, not reconciled). The status **REC** (reconciled: register ids attached, EL review recorded, upstream product/NFR documents checked) can only be assigned by a later version after SE11-AC-11 passes. **No entry in v3 is REC.** Downstream documents that cite this version cite it as `SE11-PHYSICAL-INFRASTR-HARDWARE v3 (PROVISIONAL)` and carry the same provisional status for anything derived from it (SE11-REQ-11).

### 0.3 Source disposition in the completion event (corrects finding 001)

The v2 reading "`not_applicable` = could not be applied" is withdrawn: a missing source is not an inapplicable source. The substantive disposition of PL-REQ-ID-REGISTER is **UNMET SOURCE** (SE11-DEP-01). The completion-event schema admits only `covered` or `not_applicable`; this document reports `covered` with the meaning fixed by the global rules' corpus-silence procedure and nothing more: the source was sought and found absent; the absence is an explicit labelled assumption (ASM-SE11-01); the content the source would have supplied is replaced, to the extent the rules allow, by direct citation of the seed sections that the register rows themselves cite, pre-mapped in §0.5; no register id is cited, invented or approximated. `covered` therefore does **not** mean "consumed" or "reconciled". The gap is not resolved; §17 keeps the baseline PROVISIONAL and not approved for implementation until SE11-AC-11 passes.

### 0.4 Disposition of the v2 review findings

| Finding | Correction made in v3 | Where |
|---|---|---|
| 001 source gap reported as not_applicable; no register mapping or upstream checks | `not_applicable` interpretation removed (§0.3); UNMET SOURCE disposition with dependency id; the register mapping is pre-built as a seed-section crosswalk for every SE11 id (§0.5); consistency checks run against the only available authoritative input (SEED-01) with six **actual conflicts/deviations recorded and dispositioned** (C1–C6, §0.5 and §16.6); implementation restriction retained (§17); no ids, approvals or availability fabricated | §0.3, §0.5, §16.6, §17, §19 |
| 002 automatic ">32 GB component → M-B" rule bypassed workload sizing | Rule deleted. 256 GB (M-B or M-A+) is selectable only from an aggregate concurrent reservation calculation (host reserve + WSL cap + statics + dynamic minima/maxima + headroom) and only after reallocation within the installed candidate (step 1) and the hosted alternative (step 2) have been tried and their failure recorded in SE11-DEC-03a; worked example included | §5.3 |
| 003 contracts unregistered, consumed interfaces unbound, yet decisions rely on them | No owner contract exists in the corpus, so none is cited or invented. Each consumed interface is now an **unmet dependency with an id (SE11-DEP-nn)** stating the dependent SE11 ids and the behaviour while unmet; the provided contract is DEFINED-UNREGISTERED with the two registration steps (SE11's Interface Contract document, EL's register) listed as unmet dependencies; NFR mappings and security-control references point to the dependency ids rather than claiming coverage | §18, §3, §13 |
| 004 inconsistent reservation numbers; M-A headroom violation; undefined "shedding order" | One authoritative per-candidate reservation table (Table 5.3-R); §4 no longer carries memory numbers; every total and both admission checks derived from the table; M-A re-balanced so that 128 GB satisfies both checks; weighted contention (hypervisor reserves/weights, measurable) separated from load shedding (scheduler action owned by EL/SE01, driven by SE11-published signals); SE11-NFR-01 and SE11-AC-12 restated as weighted-service guarantees | §4, §5.2, §5.3, SE11-DEC-11, SE11-ADR-10, §14 |
| 005 Validation unprotected from Build I/O when QoS absent; fallback impact mis-stated | Storage protection matrix for every combination of lane coexistence × QoS availability with a decidable calibration rule for limits (V_min, B_max from measured device capacity), guest-side `io.max` as the alternative limiter, a new first fallback (NIC relocated to PCI_E1 while the GPU is deferred) that avoids sharing altogether, the double-fallback allowed only on a passed contention test, and the lane-sharing fallback impact corrected to include Validation; acceptance SE11-AC-12b measures the critical-validation storage outcome | §6.1, §6.1a, SE11-REQ-16, SE11-DEC-12, §14 |
| 006 shutdown budget understated; NAS runtime not separated; restart undefined for restoration during S2 / without output power cycle | Candidate-specific timed sequences (S-1, S-2, S-3) with explicit concurrent/serial steps, bounded retries, critical-path totals and a remaining-runtime requirement per UPS; B recomputed per candidate; restart mechanisms defined (M1 commanded output power-cycle, M3 RTC wake, M4 attended residual; N1 WOL for the NAS) with gates and a low-charge rule; all scenarios added to SE11-AC-06/14/15 with pass criteria | §8.3, §8.4, SE11-REQ-15, SE11-DEC-13, §14 |
| 008 QC-AR-03 reported not_applicable although applicable; no evidence; no fingerprint | Reported as **addressed by design change, evidence UNMET**: part numbers are no longer baselined — every part number is DEFERRED-PENDING-EVIDENCE (SE11-DEC-14) and the baseline is bound to specification classes (§11.4) plus the seed sha; pre-build checks (SE11-AC-01) stay separate from commissioning tests; no criterion closure at part-number level and no implementation-ready sign-off is claimed | §1.2, §11.2, §11.3, §17, §19 |
| 009 degraded protection contradicted invariants; outage tolerance ignored copy age | Per-class protection states (ABSENT / PROTECTED / DEGRADED-IN-BUDGET / EXPIRED) with last-successful-copy timestamp, maximum copy age A_max and grace G, explicit creation and mutation permissions, expiry actions (T3-SUB isolated local copy, else write-freeze of the class), restoration rule; invariants, failure table and SE11-AC-10 reconciled; outage tolerance = remaining copy-age budget; expiry-during-outage drill SE11-AC-07c | §6.3, SE11-REQ-17, §9, §14 |

### 0.5 Pre-register crosswalk and upstream consistency check (what can be done with the available authoritative input)

**Crosswalk.** PL-REQ-ID-REGISTER rows name the seed section they distil. The table below therefore keys every SE11 identifier to the SEED-01 section(s) it derives from, so that attaching register ids in SE11-AC-11 is a lookup, not a re-derivation. Column "Register id" is deliberately empty-by-rule (UNMET, SE11-DEP-01).

| SE11 id(s) | Derived from SEED-01 | Register id |
|---|---|---|
| SE11-ADR-01, gate G-LOCAL, B19 | §157 (section-39 provisioning principle), §158, §160, §168, §226 status note, §238 | UNMET |
| SE11-ADR-02, B9 | §166, §167, §168, §227.9 | UNMET |
| SE11-ADR-03, SE11-RISK-02, B4 class | §227.4, §228.1 (ECC on NAS) | UNMET |
| SE11-ADR-04, SE11-DEC-04, B11, §5.5 | §175, §176, §177, §227.7, §227.11, §160 table | UNMET |
| SE11-ADR-05, SE11-REQ-03, §6.5 | §163, §164 | UNMET |
| SE11-ADR-06, SE11-DEC-07, SE11-DEC-10, SE11-DEC-13, SE11-REQ-06, SE11-REQ-15, §8.3 | §165, §228.1, §229.1 | UNMET |
| SE11-ADR-07, SE11-DEC-08, B17 | §166, §230 | UNMET |
| SE11-ADR-08, SE11-DEC-03, SE11-DEC-06 | §158, §159, §162, §164 ("according to retention policy"), §234, §238 | UNMET |
| SE11-ADR-09, SE11-DEC-09, SE11-REQ-02, SE11-REQ-16 | §156, §157, §163, §174, §227.6 | UNMET |
| SE11-ADR-10, SE11-DEC-11, SE11-REQ-01, SE11-REQ-14, SE11-NFR-01 | §157, §174, §175 | UNMET |
| SE11-REQ-05 | §160 | UNMET |
| SE11-REQ-07, SE11-REQ-08, SE11-NFR-04 | §160 ("capture performance/resource telemetry from the first workloads"), §234 | UNMET |
| SE11-REQ-09, SE11-SECREQ-02 | §12 (current-practice revalidation), §25 (certified component registry), §160 | UNMET |
| SE11-REQ-10, B18 | §165, §231 | UNMET |
| SE11-REQ-13, SE11-REQ-17, SE11-NFR-05, §6.3 | §164 ("truly irreplaceable data should have an independent/off-site or otherwise isolated copy"), §31 | UNMET |
| SE11-SECREQ-01…08 | §59, §66, §112, §185, §228.1 (AES-256) | UNMET |
| §9 failure domains, SE11-NFR-06/07 | §172, §173, §175 | UNMET |
| §12 triggers and REV-* | §159, §161, §171, §177, §226 (F.20) | UNMET |
| ASM-SE11-02, SE11-RISK-08 | §0 (approval status), §151 | UNMET |

**Upstream consistency check (performed against SEED-01 as the common root; the absent EL/PM09/NT16/SP16 documents cannot be checked and no consistency with them is asserted).** Result: six actual deviations/conflicts between this architecture and the literal seed text, each with a disposition. They are the only known conflicts; §16.6 repeats them in the Conflicts section as the rules require.

| Id | Seed statement | This document | Disposition |
|---|---|---|---|
| C1 | §165: the rack UPS "feeds rack PDU for local worker nodes **and switch** when used" | The core switch is powered from PD-A (UPS-A), not the deferred rack UPS, because in candidate S-1 the NAS shutdown command crosses it and because the rack does not exist at baseline | Deviation accepted (SE11-DEC-08): the seed's placement presupposes a rack; while PD-B is absent the switch must be on battery-backed PD-A; when the rack exists the switch stays on PD-A unless S-3 (no command path) is in use, in which case it may move to PD-B as the seed states. Reviewers resolve if they read §165 as mandatory |
| C2 | §227.6: M2_4 = "platform data / DBs / containers", M2_2 = "VM & artifact store" | Highest-priority VM system disks are placed on M2_4 with the data; M2_2 carries High/Medium VM disks and artifacts | Deviation recorded as SE11-DEC-09/ADR-09 with reason (§157 reservation principle, §174 priority classes) and impact (§6.1) |
| C3 | §165/§229.1: one PC+NAS UPS with "automatic graceful shutdown via PowerPanel / NAS UPS service" | SE11 does not assert that any host↔NAS signalling combination works; candidate S-3 substitutes a second UPS for the NAS | Gated decision SE11-DEC-10; S-3 is a topology substitution of B15 recorded with reason (no evidenced cross-device integration) and impact (second UPS of the B16 class, separate runtime budget) |
| C4 | §166/§230: switch and rack items apply "if local rack infrastructure is selected" | The managed switch (class) is adopted at baseline without a rack | Deviation accepted (SE11-ADR-07): three or more endpoints (host 10 GbE, host 5 GbE, NAS 10 GbE, NAS 5 GbE management, gateway, UPS software endpoint) and VLAN enforcement of `seg.*` need a switch regardless of the rack; the smallest class satisfying §230 is used (§158 no-overbuild); the interim point-to-point placement of §7.2 remains allowed |
| C5 | §227.4 and §228.3 list 4×64 GB and 6×20 TB as the reference quantities | Quantities are candidates sized by rule; defaults M-A (128 GB) and N-A (4 drives) | Not a conflict: §162 ("evidence-driven sizing decision, not a fixed prerequisite"), §164 ("according to retention policy") and §238 make the quantities conditional; recorded for transparency (SE11-ADR-08) |
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

**Reading rules for the table.** (a) A disposition is the disposition *of the specification class of the reference item if local provisioning of that element is justified* under gate G-LOCAL (SE11-ADR-01); it is not a decision that local provisioning is justified. (b) **Part-number status (SE11-DEC-14, corrects finding 008):** the corpus contains no manufacturer support, firmware, qualified-list, driver or availability statement for any part number (§11.2). Every part number cited from the seed is therefore **DEFERRED-PENDING-EVIDENCE**: it is the seed's reference exemplar of the class, it is not baselined, and it becomes part of the configuration fingerprint only when its SE11-AC-01 record reads "confirmed". The *class* (§11.4) is what is adopted. Impact: there is no buildable bill in this document; downstream documents cite classes and candidate ids, never part numbers. (c) "Quantity/count status" separates the adopted class from any capacity figure, which is never adopted from the maximum listed configuration (ENV-DEC-017).

| # | BOM entry (seed section; the part number is the reference exemplar) | Seed class | Engineering disposition of the specification class (SE11 only) | Quantity / count status | Decision ref |
|---|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, Zen 5 homogeneous, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — class §11.4; virtualization extensions and IOMMU enabled; 230 W package limit is the compute line of the power budget (§8.2). Part number DEFERRED-PENDING-EVIDENCE | n/a (one CPU) | SE11-DEC-01, SE11-DEC-14 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — class: dual-tower air cooler ≤ 160 mm with AM5 mounting; structural check only (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi: 4×DDR5 to 256 GB; PCI_E1 Gen5 x16 (CPU); PCI_E2 Gen3 x1; PCI_E3 Gen4 x4 (shares with M2_3); M2_1 Gen5 x4 CPU; M2_2 Gen5 x4 CPU sharing with USB4; M2_3 Gen4 x2 chipset; M2_4 Gen4 x4 chipset; 4×SATA; 5 GbE; Wi-Fi 7; BT 5.4; 2×USB4; Flash BIOS; Clear CMOS (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map verified before baseline (SE11-AC-02) with fallbacks A/B/C (§6.1a); Wi-Fi/Bluetooth disabled in server role; no out-of-band controller, so the management path is §10.2. Part number DEFERRED-PENDING-EVIDENCE (BIOS/CPU support currency not established, §11.2) | n/a | SE11-DEC-02, SE11-DEC-12, SE11-DEC-14 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC, single matched kit; "step down to 5600/5200 if 4-DIMM training is unstable" (§227.4; §162) | Preferred target (class); evidence-driven (quantity) | ADOPT WITH ENGINEERING CONSTRAINT for the **class** (DDR5 UDIMM matched kit on the AM5 4-slot platform, EXPO with the seed's 5600/5200 fallback, non-ECC accepted and monitored, SE11-RISK-02). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** 256 GB (4×64) is the reference *ceiling*, not adopted capacity. Quantity chosen by Table 5.3-R and the rule in §5.3 (M-A default; M-B/M-A+ only from an aggregate calculation) | SE11-DEC-03, SE11-ADR-03, SE11-ADR-08 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch at x2 is acceptable subject to SE11-AC-02; fallbacks §6.1a. Part number DEFERRED-PENDING-EVIDENCE | 2 devices (roles fixed by §6.1) | SE11-DEC-02, SE11-DEC-12 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; seed roles "platform data / DBs / containers (M2_4)", "VM & artifact store (M2_2)" (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID (SE11-ADR-05); role mapping deviates from the seed's literal labels (conflict C2, SE11-DEC-09, §6.1). Part number DEFERRED-PENDING-EVIDENCE | 2 devices | SE11-ADR-05, SE11-DEC-09 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build; with the 145 W optional GPU only after the measured power-budget check the seed itself requires (§227.11; §160 table); any accelerator above 145 W, dual-slot, or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance, 3×140 mm fans (§227.8) | Preferred target | ADOPT — class §11.4; clearance and form factor structurally compatible with B2/B3 (§11.1). Part number DEFERRED-PENDING-EVIDENCE | n/a | SE11-DEC-14 |
| B9 | OS — Windows 11 Pro retail (§227.9; operating model §166) | Fixed by the operating model (§166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role; persistent services only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13). Edition/licence identifier DEFERRED-PENDING-EVIDENCE | n/a | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); if coexistence fails, Fallback A relocates the NIC to PCI_E1 while the GPU is deferred (SE11-DEC-12); hypervisor virtual-switch driver support not established (§11.2, SE11-AC-01). Part number DEFERRED-PENDING-EVIDENCE | 1 device | SE11-DEC-02, SE11-DEC-12 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell, 24 GB ECC, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition" §175; "driven by measured demand and economics" §177) | DEFER / OPTIONAL — adoption preconditions §5.5 and trigger TRG-GPU §12.2; when triggered, Fallback A (NIC in PCI_E1) must first be undone or replaced (§6.1a) | 0 at baseline | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T: 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock (64 GB max), 2×10GbE + 2×5GbE, 2×USB4, 4×M.2, ADM/Btrfs snapshots, per-folder AES-256, "UPS support / network UPS server" (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only (never a live datastore); admin interface on `seg.mgmt`; firmware lifecycle §10.4; UPS-signalling role gated by SE11-DEC-10. Part number DEFERRED-PENDING-EVIDENCE | 1 enclosure; subject to G-LOCAL (hosted object storage is the recorded equivalent for T2/T3, §6.7) | SE11-ADR-05, SE11-DEC-10 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install on TRG-NAS-MEM (§12.2) | 0 at baseline | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target (class); count tied to retention policy (§164) | ADOPT WITH ENGINEERING CONSTRAINT for the **drive class** (3.5-inch enterprise CMR, RAID 6 mandatory at ≥ 20 TB per drive, SE11-RISK-06). Part number DEFERRED-PENDING-EVIDENCE | **CANDIDATE.** Six drives is the reference *ceiling*; count chosen by the §6.7 rule (N-A default) | SE11-DEC-06, SE11-ADR-08 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, line-interactive AVR, 12 outlets (6 battery + surge, 6 surge only), NEMA 5-15P, USB HID, "automatic graceful shutdown via PowerPanel / NAS UPS service", RB1290X2 batteries (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement; per-candidate shutdown budget SE11-REQ-06 with fail-closed outcome (§8.4); signalling and restart integration gated (SE11-DEC-10, SE11-DEC-13). Part number DEFERRED-PENDING-EVIDENCE | 1 unit (S-1/S-2); 2 units of the B15/B16 classes in S-3 | SE11-DEC-07, SE11-DEC-10, SE11-DEC-13 |
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
| Storage / NAS | Hot NVMe tiers on the host, the durable NAS tier, the physical mapping of every volume and the storage protection matrix (§6) |
| Network switching / NICs / physical segments | 10 GbE storage/core path, 5 GbE host onboard, switch class, VLAN membership and addressing of the physical segments (§7). Physical-network engineering is SE11's: §74 places SE14 in "API, Integration & Portability Engineering", not physical networking |
| Rack / placement | 18U rack class; desk/room placement constraints (§8.5) |
| UPS / power distribution | Two power domains, UPS roles, per-candidate shutdown sequences, restart mechanisms (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10.1) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10.2) |
| Hardware-published signals | On-battery, thermal, storage-pressure and protection-state signals that the scheduler and data owners consume (SE11-DEC-11, §6.3, §8.3) |

### 2.2 Out of scope (owned elsewhere; referenced, never included)

| Concern | Owner (SEED-01 §74 unless stated) | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (chain rule) | §15 |
| Electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only |
| System, runtime, deployment and reliability architecture | EL | EL cross-references this document; EL's documents are absent (SE11-DEP-02/10) |
| Capacity model and growth thresholds | SE01 (capacity concern) and SE11-HARDWARE-CAPACITY-SIZING (sizing) | §5.3 and §6.7 give candidate configurations and decision rules; the sizing document applies them (SE11-DEP-03) |
| Load shedding / job pausing policy | EL (scheduler), SE01 | SE11 publishes the signals (SE11-DEC-11); the shedding policy and controller are not designed here |
| Data policy: dataset classification, retention, backup schedule, binding RPO/RTO, key custody, write-freeze enforcement | SE12 (data), SE17 (security) | §6 states hardware-capable targets, protection states and provisional defaults until SE12's document exists (SE11-DEP-04) |
| Portability and integration constraints on how pools are addressed | SE14 | Consulted on §4/§7 naming; owns no physical design |
| Security control catalogue and ids | SE17 (infrastructure/workload/data), SE15 (identity/crypto) | §13 lists SE11's requirements as SE11-SECREQ-nn; mapping to owner control ids is SE11-DEP-05 |
| Performance/resilience test execution | SE19 | §14 lists the tests; SE19 executes and reports (SE11-DEP-06) |
| Operations, monitoring, maintenance windows | SE20 | §10 states telemetry and window requirements (SE11-DEP-07) |
| Software/container/service design | existing SE11 runtime artefacts and EL | BND-03: not restated |

### 2.3 Context view (text)

```mermaid
flowchart LR
  subgraph PD_A[Power domain A: UPS-A class B15 on circuit A]
    HOST[Central host: Win11 Pro + Hyper-V\nVMs: Core + Data on M2_4 / Build-CI + Validation on M2_2\nM2_1 host system, M2_3 scratch]
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
| EL | One coherent physical architecture to reference; contract to register; shedding signals to consume | Compatibility, maintainability | §4–§10 cross-references; §18.2 contract definition; SE11-DEC-11 |
| SE01 | Capacity inputs as ranges with assumptions; signals for the scheduler | Capacity | Table 5.3-R, §6.7, §12 |
| SE12 | Durable tier, RAID/replication boundaries, protection states and recovery rules | Reliability (recoverability, fault tolerance) | §6.3, §6.6, SE11-NFR-05, SE11-AC-07a/b/c |
| SE14 | Pools addressed portably | Portability | SE11-REQ-05 |
| SE17 / SE15 | Trusted boot, management isolation, encryption support | Security (confidentiality, integrity) | §13, SE11-AC-08 |
| SE19 | Burn-in, contention, abrupt-loss and resilience test surface | Reliability (maturity), performance efficiency | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows, shutdown and restart drills | Maintainability (analysability), reliability | §10, SE11-NFR-04 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, ADR-01 gate G-LOCAL, §12 triggers |

**Measurable non-functional targets introduced by this document (status PROV; binding to EL-ENGINEER-NFR-SPECIFIC ids is unmet dependency SE11-DEP-10; values are engineering proposals, ASM-SE11-06).**

| NFR id | Quality attribute | Target (measurable) | Verified by |
|---|---|---|---|
| SE11-NFR-01 | Performance efficiency / weighted-service guarantee under contention (replaces v2's "throttling order") | Under the §14 contention profile: (a) Core and Data VMs: CPU-wait ≤ 5 % in every 60 s window, Core synthetic API probe p95 ≤ 1.5 × unloaded baseline, Data 4 KiB random-read p99 ≤ 2 × unloaded baseline; (b) Validation VM: CPU-wait ≤ 10 % (it receives its full 8 vCPU from reserve + weighted floating share, §5.2); (c) Build VM: receives ≥ 11 LP-equivalents of its 16 (4 reserved + ≥ 7 floating); (d) inside the Build VM, `pool.background` receives ≤ 10 % of the VM's CPU while build jobs saturate (cgroup weight 10 : 100). No ordered shedding is claimed at the hardware layer (SE11-ADR-10) | SE11-AC-12 |
| SE11-NFR-02 | Performance efficiency / storage path | Host↔NAS ≥ 0.7 GB/s sustained for 10 min during concurrent build-cache load; no other path degrades below 80 % of its unloaded throughput | SE11-AC-05 |
| SE11-NFR-03 | Reliability / safe shutdown, per UPS and per candidate | For every UPS u in the selected candidate: B_u ≤ 0.7 × R_u, where B_u is the critical-path budget of §8.3 and R_u the measured runtime at measured load; every step completes inside its bound; restart after restoration completes within T_restart ≤ 10 min for the mechanism selected under SE11-DEC-13 | SE11-AC-06, SE11-AC-14, SE11-AC-15 |
| SE11-NFR-04 | Maintainability / observability | 100 % of §10.3 signals exported, sample interval ≤ 60 s, retained for at least one stage | SE11-AC-09 |
| SE11-NFR-05 | Recoverability (hardware-capable; SE12 binds the product RPO/RTO) | T1→T2 snapshot interval ≤ 1 h and full replication ≤ 24 h; single-VM restore from T2 ≤ 4 h; for every D-IRR class: T3 copy age ≤ A_max = 24 h in state PROTECTED, expiry at A_max + G = 48 h (§6.3); restore of each D-IRR class from T3 verified at every stage gate | SE11-AC-07a/b/c |
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
| `pool.validate` | Integration, security validation, staging, release challenger, VP validation | High | Linux VM "Validation/Staging" | 8 vCPU; reserve 50 % (4 LP guaranteed); limit 100 %; weight 150 | Validation dynamic min/max | M2_2 (protected per §6.1a) |
| `pool.build` | CI runners, build cache, artifact generation | Medium | Linux VM "Build/CI" | 16 vCPU; reserve 25 % (4 LP guaranteed); limit 100 %; weight 100 | Build dynamic min/max | M2_2 (VM disk, artifacts) + M2_3 (scratch; fallbacks §6.1a) |
| `pool.agents` | API-based model workers | Medium | Hosted/cloud executors first. When local: **member of `pool.build` budget** as containers in the Build VM with cgroup `cpu.max` ≤ 50 % and `memory.max` ≤ 40 % of the VM | member | member | M2_2 |
| `pool.test` | Test/browser/scanning workers, synthetic users | Medium / lowest | As `pool.agents`: **member of `pool.build` budget**, `cpu.max` ≤ 50 %, `memory.max` ≤ 40 %; agents + tests together never exceed the Build VM's own ceiling | member | member | M2_2 |
| `pool.background` | Background analysis, documentation, low-priority optimisation | Lowest | **Member of `pool.build` budget**: cgroup `cpu.weight` 10 (vs 100 for build jobs), `cpu.max` ≤ 25 %, no memory guarantee; the scheduler sheds it first (§175, SE11-DEC-11) | member | member | M2_2 |
| `pool.gpu` | Local inference, embeddings, vision, evaluation (§176) | Medium | DEFERRED — PCI_E1 when adopted (§5.5); external providers meanwhile (§160) | — | — | — |
| `pool.durable` | Backups, snapshots, release evidence, archives, mirrors (§164) | n/a | NAS T2 (+ T3 isolated copy, §6.3) | — | — | NAS |
| `pool.admin` | Host OS, Hyper-V root, WSL2 + Docker Desktop interactive use (§167) | n/a | Windows host root partition | Not reservable in Hyper-V; the root partition takes floating LPs (§5.2); operational rule: VM reserves sum ≤ 16 LP so ≥ 16 LP float | Host root reserve + WSL2 cap | M2_1 |

**Simultaneous CPU accounting at baseline:** vCPUs assigned to VMs = 4 + 4 + 8 + 16 = **32 vCPU on 32 LP** (1 : 1, no vCPU oversubscription at baseline; bursts happen *within* a VM's own vCPU count). Guaranteed LPs (sum of reserves) = 4 + 4 + 4 + 4 = **16 LP (50 %)**. Floating LPs = **16**, taken first by the host root partition (typical need 2–4 LP, ASM-SE11-03) and then by VMs in weight proportion 150 : 100 (Core and Data cannot take floating LPs: their 4 vCPU are already fully reserved). Under full saturation this arithmetic gives Validation its remaining 4 vCPU in full (its weighted share of 12–14 floating LPs, 0.6 × 12 = 7.2, exceeds the 4 it can use) and leaves Build with 4 reserved + 8–10 floating = 12–14 of its 16 vCPU. That is a **weighted-contention outcome**, measurable as SE11-NFR-01, not an ordered shedding mechanism.

**Weighted contention versus load shedding (corrects finding 004; SE11-ADR-10, SE11-DEC-11).** Two different things were conflated in v2:

1. *Weighted contention* is what the hypervisor's reserve/limit/weight controls and the in-VM cgroup weights produce automatically under saturation. It needs no controller; its guarantees are those of SE11-NFR-01 and are measured by SE11-AC-12.
2. *Load shedding* — pausing, cancelling or refusing noncritical jobs "when hardware capacity, network, storage, AI quota or power conditions degrade" (§175) — is a **scheduler action**, owned by EL (orchestration/scheduler) and SE01. SE11 does not design the controller or its transitions. SE11's obligation is to **publish the signals** on which the scheduler acts, each delivered to the telemetry/event path of §10.3 within 60 s of the condition: `SIG-ONBATTERY` (UPS state S1 entered / left), `SIG-SHUTDOWN` (state S2 entered: no further scheduling will be honoured; jobs have ≤ 60 s), `SIG-THERMAL` (any monitored temperature above its manufacturer limit minus 5 °C), `SIG-STORAGE-PRESSURE` (any T1 device > 85 % used or any NVMe > 80 % TBW), `SIG-PROTECTION-STATE` (any D-IRR class leaves PROTECTED, §6.3), `SIG-PL-STATE` (platform protection level). Which jobs the scheduler sheds on each signal is EL/SE01 policy (unmet dependency SE11-DEP-03); the default expectation recorded for them, derived from §174/§175, is background → build → validation, with runtime never shed.

Rule SE11-REQ-01 (restated): `pool.core`, `pool.data` and `pool.runtime` reservations are hard — static memory, 100 % processor reserve, never oversubscribed; every other pool has a declared guaranteed floor and ceiling or an explicit membership share as above. Rule SE11-REQ-14: the reservation mechanism is the hypervisor's per-VM processor reserve/limit/weight and static-versus-dynamic memory controls plus in-VM cgroup shares for members; no pool relies on "best effort".

## 5. Compute architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-04)

### 5.1 Host-role requirements

| Requirement | Specification | Source |
|---|---|---|
| CPU | 16 physical cores / 32 logical processors, homogeneous cores, 64 MB L3, hardware virtualization + IOMMU enabled in firmware | B1 class (§227.1); VM isolation (§168) |
| Memory | DDR5 UDIMM matched kit on four slots (board maximum 256 GB, B3); quantity per Table 5.3-R; EXPO only after the stability pass; fallback DDR5-5600/5200 as the seed directs | B4 (§227.4), §162 |
| PCIe / slots | PCI_E1 Gen5 x16 reserved for the deferred accelerator (used by the NIC under Fallback A, §6.1a); PCI_E3 Gen4 x4 carries the 10 GbE NIC by default; PCI_E2 Gen3 x1 unused (Fallback C only); 2×USB4 free for emergency storage/console | B3 (§227.3) |
| Local NVMe (4 slots, all populated) | M2_1 Gen5 x4 (CPU): 1 TB host system; M2_2 Gen5 x4 (CPU, shares with USB4): 4 TB Build/Validation VMs + artifact store; M2_3 Gen4 x2 (chipset, shares with PCI_E3): 1 TB scratch; M2_4 Gen4 x4 (chipset): 4 TB Core/Data VMs + platform data + platform container layers; total 10 TB | B5, B6 (§227.5–§227.6), §163; mapping §6.1 (SE11-DEC-09) |
| Host OS / hypervisor | Windows 11 Pro with Hyper-V; Linux VMs for all durable services; WSL2 + Docker Desktop for interactive work only | B9 (§227.9), §166–§168 |
| Firmware baseline | UEFI Secure Boot and TPM 2.0 enabled; Wi-Fi 7 / Bluetooth disabled; "restore on AC power loss = power on"; RTC wake capability recorded (§8.3); settings baseline in §13 | §13, SE11-DEC-13 |
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

Mechanism on the selected host platform: per-VM **processor resource controls** (virtual machine reserve %, virtual machine limit %, relative weight) and per-VM **memory controls** (static memory = hard reservation; Dynamic Memory with minimum/maximum for burst pools). Members of a shared budget (`pool.agents`, `pool.test`, `pool.background`, `pool.runtime`) are bounded inside their VM by Linux cgroup v2 `cpu.weight`, `cpu.max`, `memory.min`, `memory.max` as listed in §4. **Admission rule (all derived from Table 5.3-R):** a VM or member may be created or resized only if (a) Σ processor reserves stays ≤ 16 LP, (b) the memory floor F and ceiling C recomputed from Table 5.3-R satisfy both checks of §5.3 for the installed candidate, and (c) the pool's storage volume is already mapped in §6.1 with its §6.1a protection row. The rule is enforced by the version-controlled VM definitions and checked in SE11-AC-03; its behaviour under saturation is verified by SE11-AC-12.

### 5.3 Memory sizing: the authoritative reservation table and decision rule (SE11-DEC-03, corrects findings 002 and 004)

**Evidence status.** No measured workload exists (§0.1: EL estimates and SE01 capacity model absent, SE11-DEP-03). Table 5.3-R therefore holds **hypothetical planning allocations** (ASM-SE11-03, ASM-SE11-11) derived only from the five required logical environments (§156) and the layout (§167). They justify no quantity by themselves; the sizing document replaces them with a traceable Stage-1 inventory and measured p95 values (§234 H.3). What *is* binding is the table's structure, the two admission checks and the decision rule.

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
| Check 1: installed ≥ 1.25 × F | 128 ≥ 115 ✓ | 256 ≥ 190 ✓ | 256 ≥ 190 ✓ | 128 ≥ 75 ✓ |
| Check 2: installed ≥ C + H_min (H_min = 8) | 128 ≥ 124 ✓ | 256 ≥ 240 ✓ | 256 ≥ 240 ✓ | 128 ≥ 104 ✓ |
| Headroom at ceiling | 12 | 24 | 24 | 32 |
| Scale path | Add a second matched pair → M-A+ (SE11-AC-04 memory pass re-run; §227.4 4-DIMM fallback applies) | None (board maximum; REV-MEM) | None (board maximum; REV-MEM) | Hosted elasticity for data; local as M-A |
| Trade-off recorded | Smallest justified start (§158, §238); Data working set capped at 32 GB until re-balanced or expanded | Buys capacity the model may not demonstrate; single matched kit (§227.4); 4-DIMM training risk flagged by the seed | Two kits are not "a single matched kit" (§227.4): stability must be re-proven | Confidential-processing boundary (§66), EL latency input and SP16 economics (SE11-DEP-08) decide |

Members inside the Build VM (`pool.agents`, `pool.test`) are bounded by `memory.max` ≤ 40 % of the Build VM's *current* allocation and need no separate line.

**Decision rule (SE11-DEC-03).**

1. *Inputs.* SE11-HARDWARE-CAPACITY-SIZING produces, from a traceable Stage-1 concurrent workload inventory (the inputs EL-ENGINEER-ESTIMATE-CAPACITY and SE01 own, SE11-DEP-03), a per-pool floor and ceiling; the measured host root reserve replaces the 12/16 GB planning value (ASM-SE11-11). F and C are recomputed with the Table 5.3-R formula — **always as the aggregate of all concurrently resident pools plus host overhead plus WSL cap, never from one component**.
2. *Selection.* The initial quantity is the smallest candidate whose installed capacity satisfies **both** Check 1 (installed ≥ 1.25 × F) and Check 2 (installed ≥ C + 8 GB).
3. *Default before a model exists.* The seed's H.1 ("start productively") and H.3 ("measure before resizing") apply: **M-A with the Table 5.3-R values is installed**; the choice and basis are recorded as SE11-DEC-03a in the sizing document. M-A satisfies both checks with those values (Check 1: 128 ≥ 115; Check 2: 128 ≥ 124), so the default no longer violates the rule it is subject to.
4. *A component larger than its pool allocation* (for example a database working set of 44 GB against the M-A Data static of 32 GB) does **not** by itself select a larger candidate. The sizing document must work through, in order, and record the outcome of each step in SE11-DEC-03a:
   - **Step 1 — reallocate within the installed candidate.** Raise the affected static line and lower the dynamic maxima/minima of the other pools, keeping every pool at or above its own floor, and re-run both checks. Worked example on M-A: Data static 44, Validation 6 → 16, Build 8 → 16: F = 12+8+20+44+6+8 = 98 → 1.25 F = 122.5 ≤ 128 ✓; C = 12+8+20+44+16+16 = 116 → C + 8 = 124 ≤ 128 ✓. Both checks pass; M-A stands with a recorded re-balance. Step 1 fails only when no allocation satisfying both checks keeps every pool at or above its floor.
   - **Step 2 — hosted alternative (M-C) for the oversized component.** Permitted by §238 and §160; it fails only for a recorded reason: the confidential-processing boundary (§66) forbids hosting that data, EL's latency requirement for the Core↔Data path is not met by a hosted service, or SP16 economics (SE11-DEP-08) reject it.
   - **Step 3 — 256 GB (M-B or M-A+) only if Steps 1 and 2 both failed for recorded reasons** *and* the aggregate C from the model (not the single component) requires it under Check 2. The record in SE11-DEC-03a must show the aggregate calculation and both failed steps. **256 GB is never adopted on the strength of this document, nor on the strength of a single component.**
5. *Non-ECC* on the central node is accepted for every candidate (SE11-ADR-03) with the ECC platform class recorded as the substitute if SE11-RISK-02 materialises.

### 5.4 Virtualization / host implications

- VM count and boundaries remain an engineering decision (§167); the four Linux VMs are the minimum that satisfies the isolation rule of §156. Merging Core and Data into one VM is permitted only if the static memory lines of Table 5.3-R are preserved as a sum, both stay on M2_4, and SE17 accepts the shared blast radius.
- Highest-priority VMs (Core, Data) use static memory and 100 % processor reserve; they are never configured for dynamic over-commit (SE11-REQ-01).
- Snapshots of the Validation and Core VMs are taken before any firmware/driver change (§10.4) and replicated to `pool.durable`.
- Nothing in the VM layer may encode physical slot ids, device serials or the host name; the portability requirement §160 applies to every VM definition (SE11-REQ-05). Storage is referenced by volume label / stable identifier, not by slot.
- Per-virtual-disk IOPS controls (hypervisor storage QoS minimum/maximum) are the preferred storage limiter; their availability on the chosen host OS edition is confirmed in SE11-AC-03. If unavailable, the **guest-side limiter** of §6.1a (cgroup v2 `io.max` inside the Build VM) is mandatory — device separation alone is no longer an accepted fallback (SE11-REQ-16, corrects finding 005).

### 5.5 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger TRG-GPU (§12.2: local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability — which means that if Fallback A (NIC in PCI_E1, §6.1a) is in use it must first be replaced by Fallback B or C with a passed SE11-AC-12b — plus 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms measured full-load system draw plus 145 W ≤ 80 % of the 750 W PSU rating and that the per-candidate shutdown budgets of §8.3 still hold at the higher PD-A load; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on the client hypervisor (device assignment or partitioning) — if none exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as a new SE11-DEC; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator or a dual-slot card is ESCALATE ARCHITECTURE IMPACT (SE11-ADR-04).

## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Authoritative physical mapping of every volume (SE11-DEC-09 / SE11-ADR-09)

This table is the single source of truth. Sizes are initial allocations (candidate envelope, ASM-SE11-03) and are thin-provisioned so that the sizing document can resize without re-mapping.

| Volume | Pool | Physical device (slot, link) | Initial allocation | Notes |
|---|---|---|---|---|
| Host OS, hypervisor, WSL2 distro disk | `pool.admin` | **M2_1** 1 TB (Gen5 x4, CPU) | whole device | T0 system; rebuildable from version-controlled host build; encrypted (§13) |
| Core VM system disk | `pool.core` | **M2_4** 4 TB (Gen4 x4, chipset) | 128 GB | storage-QoS minimum IOPS where available (defence in depth; M2_4 carries Highest-priority only) |
| Core VM state disk (queues, registry, coordination) | `pool.core` | M2_4 | 256 GB | |
| Data VM system disk | `pool.data` | M2_4 | 64 GB | |
| Data VM database / search / cache disk | `pool.data` | M2_4 | 1.5 TB | database-consistent backups to T2 |
| Platform container image layers (Core/Data services) | `pool.core`/`pool.data` | M2_4 | 256 GB | D-REB |
| M2_4 headroom | — | M2_4 | ~1.8 TB | alert 70 %, review 85 % |
| Validation VM system + replica data disks | `pool.validate` | **M2_2** 4 TB (Gen5 x4, CPU; shares with USB4) | 64 GB + 768 GB | production-like replica; fault injection only here; **protected per §6.1a (V_min)** |
| Build VM system disk | `pool.build` | M2_2 | 64 GB | counted in B_max |
| Build VM container layers, agent/test workspaces | `pool.build` members | M2_2 | 512 GB | D-REB; counted in B_max |
| Artifact store (active artifacts, served to all pools over the internal virtual switch) | `pool.build` | M2_2 | 1 TB | D-BND; archival copies to T2; counted in B_max |
| M2_2 headroom | — | M2_2 | ~1.6 TB (~1.1 TB under Fallback B) | |
| Build cache / scratch | `pool.build` | **M2_3** 1 TB (Gen4 x2, chipset; shares with PCI_E3) | whole device | D-REB; first device to exhaust TBW; moves to M2_2 only under Fallback B (§6.1a) |
| T2 durable | `pool.durable` | NAS RAID 6 (count per §6.7) over L1 | per §6.7 | snapshots, backups, evidence, archives, mirrors (§164) |
| T3 isolated copy | — | off-site / hosted (provider per NT16, SE11-DEP-09) and/or T3-SUB isolated local medium (§6.3) | class D-IRR only | §6.3 |

**Why the mapping deviates from the seed's literal role labels (SE11-DEC-09, conflict C2).** The BOM labels M2_2 "VM & artifact store" and M2_4 "platform data / DBs / containers" (§227.6). Placing *all* VM disks on M2_2 would put the Highest-priority Core and Data system disks on the same device as Medium-priority build artifacts, violating the reservation principle (§157: reserve "storage I/O … for stable platform operation") and SE11-REQ-02. The role labels are guidance on purpose, not an isolation rule; moving the Highest-priority VM disks to M2_4 keeps M2_4 entirely Highest-priority and M2_2 entirely High/Medium. Impact: M2_4 carries both VM system disks and the database — all one priority class; M2_2 carries Validation (High) with Build (Medium), which is exactly the contention that §6.1a bounds. SE11-REQ-02 is satisfied without exception.

### 6.1a Storage protection matrix: Validation versus Build on M2_2 for every lane × QoS combination (SE11-REQ-16, corrects finding 005)

**Why a matrix.** Validation ("VP validation / release assurance", High, §174) shares M2_2 with Build (Medium). Device separation protects Core/Data, not Validation. Protection of critical-validation I/O therefore needs a limiter in every supported combination of (i) the SE11-AC-02 lane-coexistence result for PCI_E3/M2_3 and (ii) the SE11-AC-03 result for hypervisor storage QoS.

**Calibration rule (decidable; percentages are ASM-SE11-09 until SE19's measurements replace them).** In SE11-AC-04 measure for M2_2: `D2` = sustained 4 KiB random 70/30 read/write IOPS at queue depth 32 for 10 min, and `L2` = its p99 read latency at 25 % of D2. Then:

- `V_min` (Validation guaranteed minimum, sum over Validation virtual disks) = max(1.5 × Validation's measured p95 IOPS demand under its heaviest Stage-1 suite, 20 % × D2); before the demand is measured, V_min = 20 % × D2.
- `B_max` (Build aggregate maximum, sum over **all** Build VM virtual disks on M2_2: system, layers/workspaces, artifacts, and scratch when Fallback B applies) = 60 % × D2.
- The remaining ≥ 20 % of D2 is unallocated so that the device never runs at the saturation knee.
- Acceptance SE11-AC-12b: with Build driving every one of its M2_2 disks at queue depth 32 (and scratch wherever it is), Validation's 4 KiB random-read p99 ≤ 2 × L2 and Validation's achieved IOPS ≥ V_min for 10 min.

**Lane-coexistence outcomes (SE11-AC-02) and their storage consequence:**

| Outcome | Meaning | Scratch location | NIC slot |
|---|---|---|---|
| OK | PCI_E3 (NIC) and M2_3 (scratch) operate simultaneously at their expected widths | M2_3 | PCI_E3 |
| Fallback A (SE11-DEC-12, preferred fallback) | They cannot coexist (or M2_3 drops below Gen4 x2) **and the GPU is deferred**: the NIC moves to PCI_E1 (Gen5 x16, CPU lanes), M2_3 keeps scratch | M2_3 | PCI_E1 — no storage change; TRG-GPU later requires Fallback B or C with a passed SE11-AC-12b before the GPU can take PCI_E1 |
| Fallback B | They cannot coexist and PCI_E1 is needed (GPU adopted): NIC stays in PCI_E3, M2_3 is emptied, scratch becomes a 512 GB virtual disk on M2_2 | M2_2 (inside B_max) | PCI_E3 |
| Fallback C | They cannot coexist; NIC moves to PCI_E2 (Gen3 x1); scratch stays on M2_3 | M2_3 | PCI_E2 — L1 is bounded by Gen3 x1 (~0.98 GB/s theoretical); allowed only if SE11-AC-05 still shows ≥ 0.7 GB/s host↔NAS (SE11-REQ-04) |

**Protection matrix — mechanism and admissibility for every combination:**

| Lane outcome | Hypervisor storage QoS (SE11-AC-03) | Required limiter | Validation impact statement | Admissible? |
|---|---|---|---|---|
| OK / Fallback A / Fallback C (scratch on M2_3) | available | QoS minimum = V_min on Validation disks; QoS maximum = B_max aggregate on Build disks | Validation shares M2_2 with Build VM disk + layers + artifacts; bounded by B_max | Yes; SE11-AC-12b must pass |
| OK / Fallback A / Fallback C | unavailable | **Guest-side limiter:** cgroup v2 `io.max` in the Build VM on every block device backed by M2_2, aggregate riops + wiops ≤ B_max (and a bytes cap at 60 % of measured M2_2 sequential throughput); Validation unthrottled; version-controlled and verified in SE11-AC-03 | As above; the limiter is inside the Build guest rather than the hypervisor, so a misconfigured guest can exceed it — residual recorded in SE11-RISK-13 | Yes; SE11-AC-12b must pass |
| Fallback B (scratch on M2_2) | available | QoS as row 1 with the scratch disk counted inside B_max; QoS maximum on scratch individually ≤ 50 % of B_max | **Validation is affected** (v2 wrongly called this Build-internal): Build now adds cache/scratch traffic to the same device; headroom falls to ~1.1 TB; TBW on M2_2 rises (TRG-NVME-TBW) | Yes; SE11-AC-12b must pass with scratch load included |
| Fallback B | unavailable | Guest `io.max` covering the scratch block device as well, aggregate ≤ B_max | As above plus the guest-side residual | **Only if SE11-AC-12b passes with scratch load included.** If it fails, this combination is **disallowed**: remedy in order — Fallback A (if the GPU is not yet adopted), Fallback C (if SE11-AC-05 passes), or ESCALATE ARCHITECTURE IMPACT (REV-STORAGE-HOT: the host NVMe topology cannot carry scratch + artifacts + validation; a NIC class or board class change is architectural) |

**Admission consequence.** A Validation VM may be started on M2_2 only when its §6.1a row is implemented and SE11-AC-12b has passed on that combination; the row in force is recorded in the configuration fingerprint (§11.3) and in the contract record (§18.2).

### 6.2 Tiers and dataset classes

| Tier | Device(s) | Role (seed) | Durability boundary | Policy owner |
|---|---|---|---|---|
| T0 system | M2_1 | Windows + WSL2 (§227.5) | Rebuildable; no unique data | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 (Gen4 x2) or M2_2 under Fallback B | Build cache / scratch (§227.5) | Disposable | SE11 |
| T1 hot, Highest | M2_4 | Core/Data VMs, platform data, DBs, platform containers | Independent volume; snapshot + replication to T2 | SE12 (data), EL (VM definitions) |
| T1 hot, High/Medium | M2_2 | Validation/Build VMs, artifact store | Independent volume; archival replication to T2 | SE12 (artifact retention) |
| T2 durable | NAS RAID 6 | Backups, snapshots, release evidence, VM/container archives, artifacts, mirrors (§164) | Dual-parity array + snapshots; "not the only backup" (§164) | SE12 |
| T3 isolated copy | Off-site / hosted, encrypted; or T3-SUB isolated local medium (§6.3) | "independent/off-site or otherwise isolated copy" for irreplaceable data (§164) | Independent of room, UPS, NAS and host | SE12 (policy), SE17 (keys) |

**Dataset classes (provisional default, ASM-SE11-08; SE12 is the classification owner, SE11-DEP-04):**

| Class | Definition | D-IRR sub-classes used by the protection states | Minimum protection |
|---|---|---|---|
| D-IRR | Irreplaceable: cannot be re-derived from any other platform data | `REPO` (source repositories, IaC, configuration), `DB` (non-synthetic platform databases), `EVID` (release-evidence packages, decision logs), `INV` (inventory records, telemetry baselines required by evidence), `KEYS` (secret/key backups) | T1 + T2 + verified T3, state PROTECTED before the dataset exists (§6.3) |
| D-BND | Bounded loss: re-derivable from D-IRR within an accepted window | build artifacts, locally built images, validation results, telemetry history | T1 + T2; loss window accepted by SE12 |
| D-REB | Rebuildable from definitions or external sources | caches, scratch, pulled container layers, VM system disks | T1 only |

### 6.3 Protection states, permissions and expiry (SE11-REQ-13, SE11-REQ-17; corrects finding 009)

**Per-class state.** Each D-IRR sub-class *c* carries: `t3_last_ok(c)` = timestamp of the last successful, verified T3 copy; `age(c)` = now − `t3_last_ok(c)`; `A_max` = maximum copy age (default 24 h, SE11-NFR-05); `G` = grace (default 24 h); both defaults are ASM-SE11-10 until SE12 binds them (SE11-DEP-04). States:

| State of class c | Definition | Create a new dataset of class c | Mutate an existing dataset of class c | Mandatory actions |
|---|---|---|---|---|
| ABSENT | No dataset of class c exists on the platform | **Prohibited** until SE11-AC-07b passes for class c (T3 mechanism commissioned, restore verified, `t3_last_ok` set) | n/a | — |
| PROTECTED | Datasets exist; `age(c)` ≤ A_max; last restore verification passed | Permitted | Permitted | T3 copy at interval ≤ A_max; `SIG-PROTECTION-STATE` not raised |
| DEGRADED-IN-BUDGET | Datasets exist; A_max < `age(c)` ≤ A_max + G (T3 mechanism lost, internet down, copy failing) | **Prohibited** (no new datasets/classes of D-IRR are admitted) | Permitted | `SIG-PROTECTION-STATE` raised within 60 s; T3 copy retried every 1 h; SE20 prepares T3-SUB (encrypted isolated local copy, §6.2) so it can be taken before expiry; exposure window logged |
| EXPIRED | `age(c)` > A_max + G, **or** the last restore verification failed | Prohibited | Permitted **only while a T3-SUB copy of class c with age ≤ A_max exists**; otherwise the class is placed in **write-freeze** (read-only) by its owning service until a T3 or T3-SUB copy succeeds | SE20 incident; SE12 decides whether to extend via T3-SUB or hold the freeze; every hour in EXPIRED is logged against the stage's exposure budget |

**Platform-level derived state (published as `SIG-PL-STATE`):** `PL-T2` = SE11-AC-07a passed and every D-IRR class is ABSENT (only D-BND/D-REB data exist); `PL-T3` = every existing D-IRR class is PROTECTED; `PL-DEG` = at least one class DEGRADED-IN-BUDGET and none EXPIRED; `PL-EXP` = at least one class EXPIRED. Before SE11-AC-07a the platform is `PL-0` (unprotected-initial): only D-REB and synthetic data may exist.

**Invariants (reconciled with §6.6, §9 and SE11-AC-10).** (I1) A D-IRR dataset of class c exists only if class c has been PROTECTED at least once (creation gate). (I2) In `PL-T2` no D-IRR data exists. (I3) In `PL-DEG`/`PL-EXP` D-IRR data **does** exist and is exposed to FD-STORAGE/FD-ROOM for at most `age(c)`; the exposure is bounded by A_max + G plus the T3-SUB age. (I4) SE11-AC-10 passes only in `PL-T2` (no D-IRR) or `PL-T3` (all PROTECTED). (I5) T3-dependent recovery (§6.6) is valid for class c only from its last successful T3 or T3-SUB copy; the loss window is `age(c)` at the moment of loss.

**Class-specific activation.** `REPO`: the T3 copy is a hosted remote at an external repository service, active before any local hardware is commissioned (§160 keeps authoritative source in version control outside any single host), so `REPO` reaches PROTECTED on day one. `DB`, `EVID`, `INV`, `KEYS`: the encrypted off-site copy mechanism must pass SE11-AC-07b for that class before the first non-synthetic record is admitted.

**Outage tolerance (corrects FD-INTERNET).** The tolerance of class c to loss of the T3 path is its **remaining copy-age budget**, `A_max − age(c)` at the moment the outage starts (then G of degraded operation), not a fixed 24 h. A class whose last copy is 20 h old enters DEGRADED-IN-BUDGET 4 h into an internet outage.

**Restoration.** T3 path restored → a full copy of class c completes → sample restore verification passes → `t3_last_ok(c)` updated → PROTECTED; any write-freeze is lifted by the owning service on `SIG-PROTECTION-STATE` clearing.

**Enforcement and ownership.** SE11 publishes the states and timestamps (`SIG-PROTECTION-STATE`, `SIG-PL-STATE`, §10.3). Creation gating, mutation permission and write-freeze are enforced by the owning services (EL for admission in Definition of Ready, SE12 for the data stores, SE20 for the operational checklist) — unmet dependencies SE11-DEP-02/04/07. SE11 has no hardware-level backstop for a write-freeze and does not claim one. T3-SUB is an encrypted copy to a removable medium or a second independent location kept outside the room (§164 "otherwise isolated copy"), restore-verified in SE11-AC-07b; it is a bridging measure, not a replacement for T3.

**Verification.** SE11-AC-07b (activation per class), SE11-AC-07c (expiry drill: internet/T3 loss starting at `age` = A_max − 1 h; DEGRADED at +1 h, EXPIRED at +25 h, permissions enforced, T3-SUB or freeze observed, recovery to PROTECTED after restoration), SE11-AC-10 (I4).

### 6.4 Bandwidth / IOPS / latency assumptions (device-class figures from the BOM; measured values replace them in SE11-AC-04)

| Path | Nominal from BOM | Engineering assumption used for design |
|---|---|---|
| M2_1, M2_2, M2_4 (Gen4 x4 devices) | up to 7,300 / 6,300 MB/s (§227.5–§227.6) | Sustained mixed workload 2–4 GB/s per device; sub-millisecond latency; NVMe is not the first bottleneck; D2 and L2 measured for §6.1a |
| M2_3 (Gen4 x2 slot shared with PCI_E3) | device 7,300 MB/s; slot ≈ half of x4 | ≈ 3–3.5 GB/s ceiling; acceptable for scratch; verified in SE11-AC-02/04 |
| Host ↔ NAS over 10 GbE (L1) | 10 Gb/s ≈ 1.1–1.2 GB/s wire (Fallback C: ≤ ~0.98 GB/s) | 0.7–1.0 GB/s sustained for backup/artifact transfer; a 4–6 drive RAID 6 CMR array delivers on the order of 0.5–1.0 GB/s sequential and far lower random IOPS — the NAS is never used for random-IO workloads (§164) |
| Endurance | 600 TBW (1 TB), 2,400 TBW (4 TB) (§227.5–§227.6) | Scratch (M2_3) exhausts TBW first; under Fallback B, M2_2 consumption rises; TBW telemetry mandatory (§10.3); replacement by specification class (§11.4) |

### 6.5 RAID / replication boundaries

- Host NVMe: no RAID. Independence of M2_2 and M2_4 is the only host-level isolation; redundancy is by replication to T2 (SE11-ADR-05). Rationale: host mirroring would double NVMe cost for a tier whose durability requirement is met by snapshot + replication and would not protect against host loss, the dominant failure domain (§9).
- NAS: RAID 6 at any drive count ≥ 4 (dual parity is mandatory at 20 TB per drive because the rebuild window — planning assumption 1–3 days under concurrent load, ASM-SE11-04 — must tolerate a second loss). Snapshots guard against logical corruption; T3 guards against array, enclosure, power or site loss (§164).
- Replication is one-way T1 → T2 → T3; T2 never serves as a live datastore for VMs or databases.
- The BOM's NVMe is a client-class device; power-loss protection of in-flight writes is **not asserted** (§11.2). Crash consistency therefore relies on filesystem journaling in every VM, database write-ahead logging with synchronous commit (SE12), and NAS copy-on-write; all are verified by the abrupt-loss drill SE11-AC-13 (SE11-NFR-07).

### 6.6 Recovery expectations (hardware-capable targets stated to SE12; SE12 sets the binding RPO/RTO)

**T2-only recoveries (no T3 dependency):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| M2_4 failure (Core + Data VMs, platform data) | Full platform outage; restore both VMs and database from the last T2 snapshot/backup; data loss ≤ snapshot interval (≤ 1 h, SE11-NFR-05); RTO ≤ 4 h per VM | Spare NVMe of the §11.4 class; SE12 schedule |
| M2_2 failure (Validation + Build VMs, artifacts; scratch too under Fallback B) | Build/validation outage; runtime continues; restore from T2 archives or rebuild from definitions; D-BND loss within SE12's accepted window | Spare NVMe |
| M2_1 failure (host OS) | All VMs stop until the host OS is rebuilt from the version-controlled host build onto a replacement device; VM disks on M2_2/M2_4 remain intact | Spare NVMe; host build definition in version control |
| M2_3 failure | Rebuild caches; no data loss; interim Fallback B mapping if no spare | Spare NVMe or fallback mapping |
| Single NAS drive failure | No data loss; degraded; rebuild window ASM-SE11-04; replacement drive of equivalent class | Free bays allow a hot spare as an SE12 decision |
| Two concurrent NAS drive failures | No data loss (RAID 6) | — |
| Host loss (board/CPU/PSU) with intact NVMe | Move the NVMe devices to a replacement host of the §11.4 class or restore VMs to a hosted equivalent (§160, §168) | Hardware-independent definitions (SE11-REQ-05) |

**T3-dependent recoveries (valid per class from its last successful T3/T3-SUB copy; loss window = `age(c)` at the moment of loss, §6.3 I5; in `PL-T2` no D-IRR data exists, so the residual is the loss of D-BND/D-REB only):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| Third NAS drive failure before rebuild completes (array loss) | Restore each D-IRR class from T3 with loss ≤ `age(c)`; D-BND re-derived | Verified T3 copy per class |
| NAS enclosure loss | T1 continues without a local backup target (degraded, time-boxed by SE12); D-IRR protected by T3 until NAS is replaced; classes move to DEGRADED when their T2→T3 pipeline depends on the NAS | T3 |
| Host loss with NVMe loss, room/site loss (FD-ROOM) | Rebuild on replacement or hosted infrastructure from T3 (D-IRR, loss ≤ `age(c)`) and definitions; D-BND re-derived | T3, hosted fallback |

### 6.7 Capacity headroom and NAS capacity candidates (SE11-DEC-06)

| Tier | Candidate / installed | Headroom rule | Expansion path |
|---|---|---|---|
| T1 (M2_2 + M2_4) | 2 × 4 TB (fixed by B6 class) | Alert 70 %, architecture review 85 % (REV-STORAGE-HOT) | No free M.2 slots: larger devices of the same class (scale-up) or artifact store fronted by T2; SATA ×4 for cold tiers only |
| T2 NAS — **N-A** (default) | 4 × 20 TB RAID 6 → 40 TB nominal, ≈ 36.4 TiB usable (derived with the seed's 80 TB → 72.8 TiB ratio, ASM-SE11-04); 4 bays free | Alert 70 %, review 80 % | Add same-class drives to free bays on TRG-NAS-CAP (online array expansion support by the NAS OS not established — SE11-AC-01 item) |
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

The switch (B17 class) is the single core: managed, VLAN-capable, at least 2×10 GbE (seed minimum, §230) with ≥ 4×10 GbE preferred so that host, NAS primary, NAS secondary and one future 10 GbE consumer fit without replacement (SE11-ADR-07); 24 access ports at ≥ 1 GbE for workers, management devices and the gateway. It is adopted ahead of the rack (conflict C4) because the management segment and VLAN enforcement need it. Until the switch is installed, an interim point-to-point 10 GbE link host↔NAS with L2 to the gateway is acceptable *placement* — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2); in that interim the S-1 NAS shutdown command runs over the point-to-point link, which removes the switch from the shutdown path. Power: the switch is on PD-A (conflict C1).

### 7.3 Segmentation (SE11 designs the physical segments, VLAN membership and addressing; SE17 owns the security policy applied between them, SE11-DEP-05; SE14 is consulted for portable naming)

| Segment | Members | Purpose | Policy owner |
|---|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS software endpoint | Administrative plane; MFA-protected access (§59); no workload traffic; carries the S-1/S-2 shutdown signalling | SE17 (SE11-SECREQ-03) |
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
| Central host, no GPU | ~350–480 W peak at wall (CPU package ≤ 230 W + board/memory/4×NVMe/fans/NIC + PSU losses) | B1, B7; ASM-SE11-05, replaced by SE11-AC-06 measurement |
| Central host, with GPU | +145 W → ~500–630 W peak | B11 |
| NAS, 4–6 HDD + 2 M.2 | ~70–150 W (spin-up transient higher) | B12/B14 class; ASM-SE11-05 |
| Switch (+ gateway if on PD-A) | ~30–80 W | class estimate, ASM-SE11-05 |
| PD-A total | ~450–710 W without GPU; ~600–860 W with GPU (S-1/S-2); ~380–560 W / ~530–710 W under S-3 (NAS on PD-N) — below the 1000 W rating, but battery runtime at these loads is minutes: UPS-A is a controlled-shutdown device, not a ride-through supply (§165) | SE11-AC-06 verifies |
| Whole installation | Seed figures: typical ~560 W, sustained peak ~1,150–1,300 W when the rack is present (§231) | Circuit-sizing input for the electrician |

SE11-REQ-10 (qualified-professional requirement; code-regulated work is not designed here): a licensed electrician verifies that circuits A and B are separate branch circuits of adequate rating for the measured/peak loads above, that receptacles, grounding and surge arrangements meet local code, and whether the optional dedicated 20 A circuit (§231) is warranted; SE11 supplies only the load figures and the two-domain requirement.

### 8.3 Safe-shutdown signalling, per-candidate timed sequences and restart (SE11-DEC-07, SE11-DEC-10, SE11-DEC-13; corrects finding 006)

**Signalling topology — gated decision (SE11-DEC-10, conflict C3).** The corpus names two integration surfaces: "automatic graceful shutdown via PowerPanel / NAS UPS service" on the UPS (§229.1) and "UPS support / network UPS server" on the NAS (§228.1). It does **not** establish any protocol/client/version combination between them. SE11 records three candidates and a gate:

| Candidate | Topology | Cross-device integration required | Status |
|---|---|---|---|
| S-1 (preferred) | UPS-A USB-HID → central host running the UPS vendor's host shutdown software; the host orchestrates VM shutdown and issues an authenticated remote shutdown command to the NAS over `seg.mgmt` | Host↔UPS: vendor software on the host OS version; host→NAS: a remote shutdown interface supported by the NAS OS | Gated by SE11-AC-01 evidence (dated vendor documentation for both interfaces at the exact versions) |
| S-2 | UPS-A USB-HID → NAS as network UPS server; host as network client | NAS server protocol ↔ a host client implementing it | Gated by SE11-AC-01 evidence |
| S-3 (protocol-agnostic fallback) | Two UPS units, each with its own USB-HID path: UPS-A → host; UPS-N (class B16) → NAS | None across devices | Adopted automatically if neither S-1 nor S-2 produces evidence; recorded as a new SE11-DEC (topology substitution of B15) |

No shutdown sequence is relied on until the selected candidate has passed SE11-AC-06, SE11-AC-14 and SE11-AC-15.

**Common parameters (defaults; SE11-AC-06 replaces them with measured values):** T_hold = 60 s (on-battery hold before the sequence starts; 0 s when battery charge < 50 %, see restart rules); VM graceful-stop timeouts Build 60 s, Validation 60 s, Core 60 s, Data 90 s, then forced stop (a forced stop marks the VM "unclean" so that its filesystem/database integrity check runs before services start on the next boot); host OS shutdown ≤ 60 s; NAS own shutdown ≤ 120 s; NAS command acknowledgment ≤ 15 s, one retry (≤ 15 s), then proceed regardless; margin M = 30 s. **Once S2 is entered the sequence is never aborted**, including by mains restoration (deterministic, bounded); restoration is handled by the restart rules below. Serial order Core → Data is kept because Core services depend on Data; Build and Validation stop in parallel with each other and with the NAS command.

**Candidate S-1 — timed sequence (t = 0 at S2 entry = T0 + T_hold):**

| t (s) | Host path (serial unless marked ‖) | NAS path (concurrent) |
|---|---|---|
| 0 | `SIG-SHUTDOWN` published ‖ send NAS shutdown command (ack ≤ 15 s; retry once by t = 30; proceed regardless) ‖ graceful stop Build and Validation (timeout 60) | Command received by t ≤ 30 |
| 60 | Build, Validation stopped (forced if needed) → graceful stop Core (timeout 60) | NAS shutdown in progress (≤ 120 s from receipt) |
| 120 | Core stopped → graceful stop Data (timeout 90) | NAS off by t ≤ 150 |
| 210 | Data stopped → host issues the restart-mechanism command (M1, below) → host OS shutdown (≤ 60) | — |
| 270 | Host off (**host critical path 270 s**) | — |

UPS-A critical path from S2 entry = max(host 270, NAS 150) = **270 s**. **B_A(S-1) = T_hold 60 + 270 + M 30 = 360 s** → required measured runtime **R_A ≥ 360 / 0.7 = 515 s (8.6 min)** at the measured PD-A load (host + NAS + switch).

**Candidate S-2 — timed sequence (NAS is the UPS server; the host is its client):**

| t (s) | NAS path | Host path |
|---|---|---|
| −60 … 0 | NAS detects on-battery at T0 (detection ≤ 10 s), notifies the host; both hold T_hold = 60 s | Host receives on-battery notification, publishes `SIG-ONBATTERY` |
| 0 | NAS enters its own S2: waits for the host's "client shutdown complete" message for at most W_nas = 240 s | Host sequence identical to S-1 rows 0–210 (Build‖Validation 0–60, Core 60–120, Data 120–210) |
| 210 | — | Host sends "client shutdown complete" to the NAS, issues M1, starts host OS shutdown |
| 240 | W_nas elapses (host confirmation arrived at 210; if it never arrives the NAS proceeds anyway) → NAS shutdown ≤ 120 s | Host off by 270 |
| 360 | NAS off (**UPS-A critical path 360 s**) | — |

**B_A(S-2) = 60 + 360 + 30 = 450 s** → **R_A ≥ 643 s (10.7 min)**. If the NAS OS cannot wait ≥ 240 s for the client, S-2 is not admissible (the host would lose power mid-sequence) — an SE11-AC-01 check.

**Candidate S-3 — two independent sequences:**

| UPS | Sequence | Critical path | Budget | Required runtime |
|---|---|---|---|---|
| UPS-A (host + switch) | As S-1 host path without the NAS command: Build‖Validation 0–60, Core 60–120, Data 120–210, M1 + host shutdown 210–270 | 270 s | **B_A(S-3) = 60 + 270 + 30 = 360 s** | **R_A ≥ 515 s** at PD-A load (host + switch) |
| UPS-N (NAS only) | NAS on-battery at T0 → T_hold 60 s → NAS own shutdown ≤ 120 s | 120 s | **B_N = 60 + 120 + 30 = 210 s** | **R_N ≥ 300 s (5 min)** at the measured NAS load — the independent NAS-runtime case, measured separately in SE11-AC-06 |

The NAS shutting down before the host is harmless: no shutdown step of the host depends on the NAS, and in-flight backup jobs are resumable (§175). Restart ordering (NAS reachable before the Data VM starts) is handled in S6 below.

**State machine (all candidates; the timed sequences above are the content of S2/S3):**

| State | Entry event | Actions | Bounded exit |
|---|---|---|---|
| S0 ONLINE | mains and UPS communication healthy | normal operation; UPS telemetry sampled ≤ 60 s | — |
| S1 ON-BATTERY (hold) | E1 mains loss at T0 | publish `SIG-ONBATTERY` (the scheduler stops admitting `pool.build`/`pool.background` work — EL/SE01 policy, SE11-DEC-11); alert SE20 | E2 mains restored before T0 + T_hold → S0 and `SIG-ONBATTERY` cleared; else E3 → S2 |
| S2 SHUTDOWN-INITIATED | E3: T0 + T_hold elapsed, **or** UPS low-battery, **or** UPS runtime estimate < B_u for that UPS, **or** E4 UPS-communication loss while in S1 (fail-safe: proceed) | the candidate's timed sequence; **never aborted** | → S3 within the candidate's host critical path (270 s) |
| S3 HOST-OFF | host power off | NAS completes its own path (S-1: off by t = 150, already done; S-2: off by t = 360; S-3: independent) | → S4 |
| S4 ALL-OFF | all devices halted; UPS output may still be live if mains returned during S2/S3 | restart mechanism M1 (commanded output power-cycle) fires if armed; otherwise M3/M4 | → S5 |
| S5 RESTART-PENDING | E5 mains present and AC applied to the devices (by exhaustion-and-return, or by M1's output cycle) | host firmware "restore on AC power loss = power on" and NAS "power-on after AC recovery" bring both up; host UPS software reads battery charge | → S6 when charge ≥ 50 % **and** estimated runtime at current charge ≥ B_u / 0.7; until then the host stays in HOST-ONLY (no VM auto-start) with T_hold = 0 so that a second mains loss triggers an immediate host-only shutdown (B_hostonly = 0 + 60 + 30 = 90 s, needing R ≥ 130 s) |
| S6 RESTARTED | charge and runtime conditions met | VM auto-start order with delays: Data (0 s) → Core (60 s) → Validation (120 s) → Build (180 s); NAS reachable before Data VM services start; unclean VMs run integrity checks first; SE20 post-event check of backups, telemetry and protection states | → S0 |

**Restart mechanisms (SE11-REQ-15, SE11-DEC-13; corrects the undefined restoration-during-S2 and no-output-cycle cases).** Firmware AC-recovery settings only act when the device's AC input is actually removed and restored. If mains returns while the UPS output stays live (during S2, S3 or S4), nothing in firmware re-powers a halted device. Therefore one of the following mechanisms must be commissioned, in this order of preference, and the selected one recorded in the configuration fingerprint:

| Mechanism | How it works | Covers | Gate |
|---|---|---|---|
| **M1 — commanded output power-cycle (required if evidenced)** | At t = 210 the host UPS software (S-1/S-3) — or the NAS UPS service (S-2) — commands the UPS: "turn outputs off after D_off = 90 s; restart outputs when mains is present (and battery ≥ the UPS's restart threshold)". Outputs drop at ≈ t = 300 (after host off at 270 and NAS off at ≤ 150 / 360 — in S-2, D_off is issued by the NAS at its own t = 360 instead), so every device sees a real AC loss. When mains is already back, the UPS re-energises immediately and firmware AC-recovery fires on host and NAS → S5. In S-3 each UPS is commanded by its own device | Restoration during S2/S3/S4, and the exhaustion case | SE11-AC-01: dated vendor evidence that the UPS class and the host/NAS software support commanded output shutdown with auto-restart at the exact versions; SE11-AC-15 drill |
| **M3 — scheduled wake (alternative for the host)** | Before host OS shutdown the host arms a firmware RTC wake alarm at T_wake = now + 10 min. If AC is present at T_wake the host powers on, reads UPS state: mains online → continue to S5; still on battery → immediate host-only shutdown (90 s) and the alarm is **not** re-armed (one attempt per outage, bounding energy use). NAS restart then relies on N1 (Wake-on-LAN sent by the host once in S6; NAS WOL support is an SE11-AC-01 item) | Host restoration during S2/S3/S4 without an output cycle; NAS via N1 | SE11-AC-01 (RTC wake and NAS WOL evidence); SE11-AC-15 drill |
| **M4 — attended restart (residual)** | No automatic restart; SE20 is alerted (the UPS software's last message before shutdown and the absence of the expected S5 telemetry) and an operator powers the devices on | Everything, with human latency | Accepted only while M1 and M3 are unevidenced; recorded as FD-MGMT exposure (SE11-RISK-12); REV-POWER if an SLO (§117) requires unattended restart |

Rule: **if M1 is evidenced it is mandatory**; M3 is used only where M1 is not; M4 is the fail-closed residual and blocks any stable-runtime baseline whose SLO requires unattended recovery. Whatever mechanism is selected, T_restart (mains restoration → S6 entry, given charge ≥ 50 %) must be ≤ 10 min (SE11-NFR-03).

**Communication-loss handling (E4).** Loss of host↔UPS communication while in S0: alert; if it persists > 300 s the UPS protection is declared degraded (SE20 ticket, no workload change). If mains then fails while communication is still lost, the host has no event and the outcome is an **abrupt loss** (handled as FD-UPS-A, §9) — this residual is accepted and tested (SE11-AC-14). Loss of the NAS command path (switch or NAS unreachable) in S-1 S2: proceed; the NAS stops uncontrolled at UPS exhaustion — accepted residual with CoW crash-consistency and a mandatory scrub on restart (SE11-NFR-07). In S-2, loss of the NAS→host notification path is equivalent to E4 for the host.

**Shutdown budget rule (SE11-REQ-06, SE11-NFR-03).** For every UPS u of the selected candidate: B_u ≤ 0.7 × R_u, where R_u is the measured runtime at the measured load of that UPS's domain. Default budgets: S-1 B_A = 360 s; S-2 B_A = 450 s; S-3 B_A = 360 s and B_N = 210 s. The 30 % reserve is held *against measured runtime*, not against the low-battery signal; the low-battery signal and the runtime estimate are additional triggers only.

### 8.4 Fail-closed commissioning outcome

SE11-AC-06 **fails** if, for any UPS of the selected candidate, R_u < B_u / 0.7 at the measured load, or if any step exceeds its bound in the drill, or if no restart mechanism meets T_restart ≤ 10 min (M4 counts as a fail for any baseline whose SLO requires unattended recovery). Ordered remedies, each recorded as an SE11-DEC when applied: (1) remove non-essential loads from PD-A (gateway first; the switch stays while the S-1 command path needs it); (2) shorten VM stop timeouts only with SE11-AC-13 evidence that clean stops complete within the shorter bound; (3) change candidate (S-1 → S-3 shortens B_A from 450 s under S-2 to 360 s and moves the NAS load off UPS-A); (4) substitute UPS-A by a higher-runtime unit of the same specification class (§11.4); (5) if none suffices, REV-POWER (§12.3). Until SE11-AC-06 passes, no stable-runtime stage baseline is accepted on this hardware (§154 evidence progression) and the platform stays in `PL-T2` (§6.3).

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
| FD-NVME-M2_2 | Validation + Build VM disks, artifacts (and scratch under Fallback B) | Build/validation outage; runtime continues | Isolation from M2_4; T2 archives; rebuild from definitions | SE11, SE12 | T2 or rebuild | Restore ≤ 4 h; D-BND loss within SE12 window | Accepted |
| FD-NVME-M2_3 | Scratch | Slower builds | Fallback B mapping (§6.1a) | SE11 | none | Cache rebuilt | None material |
| FD-WORKER | One or more workers (local or hosted) | Capacity reduction only (§172) | Multiple eligible execution targets; no critical service on one uniquely named worker (§172) | EL (placement), SE01 | none | Queue drains on remaining capacity | None material |
| FD-STORAGE | NAS enclosure / array | Backups pause; T1 keeps running; D-IRR classes whose T3 pipeline passes through the NAS begin ageing | RAID 6; snapshots; T3; T2 never a live datastore; protection states (§6.3) | SE11 (hardware), SE12 (data) | T3 for D-IRR; replacement enclosure of the §11.4 class | No D-IRR loss beyond `age(c)`; degraded window ≤ A_max + G per class | Accepted in `PL-T3`; in `PL-T2` no D-IRR data exists; `PL-DEG`/`PL-EXP` exposure bounded and logged |
| FD-SWITCH | Core switch / its uplink ports | L1, L2, L4, L5; host and NAS lose each other and the internet; VMs keep internal connectivity via the virtual switch; S-1 NAS command path lost unless point-to-point | Interim point-to-point L1; spare NAS ports; cold-spare switch of equivalent class is an SE20 stocking decision; S-3 removes the command-path dependency | SE11 | Replacement switch class | Backups resume within the SE12 window after replacement; no runtime data loss | Accepted: single switch at Stage 1–2 |
| FD-CIRCUIT-A | Mains/circuit A interruption **with healthy UPS-A** | Host, switch (and NAS in S-1/S-2) run on battery → controlled shutdown (§8.3) | State machine S1–S6; per-candidate budgets SE11-REQ-06; restart mechanism SE11-REQ-15; AVR | SE11, SE20 (drills); electrician for cause (SE11-REQ-10) | none beyond UPS | SE11-NFR-03 met in SE11-AC-06/15; automatic restart within T_restart | Accepted: outage = planned-quality downtime, no data loss beyond in-flight work |
| FD-UPS-A | **Abrupt UPS-A output loss** (UPS fault, overload trip, battery failure) or mains loss while UPS communication is lost | Host and switch (and NAS in S-1/S-2) lose power **simultaneously and without warning** | Crash-consistency requirements: journaled guest filesystems, synchronous-commit WAL (SE12), NAS copy-on-write + scrub on restart; restart S5–S6; integrity checks before services start | SE11 (hardware), SE12 (data integrity) | Spare UPS of the §11.4 class; integrity tooling | SE11-NFR-07 met in SE11-AC-13 | Accepted: client-class NVMe without asserted power-loss protection (§6.5); loss bounded to last commit; REV-POWER if drills show unrecoverable corruption |
| FD-UPS-N (S-3 only) | Abrupt UPS-N output loss | NAS only | NAS CoW + scrub | SE11 | Spare UPS class | NAS array integrity after drill | Accepted |
| FD-SIGNAL | UPS signalling path only (USB cable, UPS software, NAS command/notification path) | No immediate workload impact; a later mains loss degrades to FD-UPS-A | E4 handling (§8.3); S-3 topology as fallback; telemetry alert | SE11, SE20 | none | Detected ≤ 300 s; drill SE11-AC-14 passes | Accepted with alerting |
| FD-RESTART | Restart mechanism fails after a shutdown (M1 not executed, RTC wake missed, WOL not received) | Devices stay halted although mains is back | M1 preferred, M3 alternative, M4 residual (§8.3) | SE11, SE20 | Operator presence (M4) | SE11-AC-15: T_restart ≤ 10 min for the selected mechanism | Accepted only with M1 or M3 evidenced; otherwise recorded exposure (SE11-RISK-12) |
| FD-UPS-B / FD-CIRCUIT-B | UPS-B or circuit B (deferred) | Local workers only | Isolation from PD-A (§165) | SE11 | none | Capacity reduction only | n/a until rack exists |
| FD-ROOM | Rack/room/site (fire, flood, theft) | Total local loss | T3 off-site copy per class; portability to hosted infrastructure (§160, §168) | SE11 (physical), SE12 (T3), EL (hosted fallback) | T3; hosted capacity | D-IRR restored from T3 with loss ≤ `age(c)`; service rebuilt on hosted/replacement infrastructure | Accepted in `PL-T3`; exposure in `PL-DEG`/`PL-EXP` bounded by §6.3 |
| FD-EXT-AI | External AI providers | `pool.agents` work needing external models; no offline AI until B11 adopted | Provider router/fallback and AI-dependency governance (§66, §115, §185); queued jobs resume (§175) | EL (AI/agent architecture, SE11-DEP-02) | Alternative provider per router policy | Queued work resumes without loss | Pending EL; NT16 vendor risk absent (SE11-DEP-09) |
| FD-INTERNET | Uplink / gateway | External providers, hosted runners, hosted T3 transfers, mirrors | Local repositories/mirrors on T2 (§164); local build capacity in `pool.build`; **T3 tolerance = remaining copy-age budget per class (A_max − `age(c)` at outage start), then G of degraded operation, then T3-SUB or write-freeze (§6.3)** | SE11 (physical uplink), SE20 (operations), SE12 (policy) | Single uplink restored | Local runtime continues; protection-state transitions observed exactly as §6.3 prescribes (SE11-AC-07c) | Accepted: single uplink at Stage 1–2; exposure bounded and logged |
| FD-MGMT | Management plane (host admin path, NAS admin, switch mgmt, UPS software) | Operator cannot intervene remotely; workloads unaffected; M4 restarts need presence | Physical console (§10.2); `seg.mgmt` isolation; configuration in version control | SE11, SE20 | Physical presence | Console recovery procedure drilled once per stage | Accepted: no BMC on the consumer-class board (SE11-RISK-04); REV-HA if SLOs require remote recovery |

Dependency-failure behaviour summary: a local infrastructure problem must not corrupt active builds or accepted runtime state; resumable jobs, durable state and idempotent execution are required of every workload placed on these pools (§175) — EL/SE19 implement and prove this; SE11 guarantees only the physical boundaries above and publishes the signals of SE11-DEC-11.

## 10. Hardware manageability / operability (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-09)

### 10.1 Inventory identity (SE11-REQ-07)

Every physical asset carries an inventory id `CSPUI-HW-<class>-<nn>` (classes: HOST, NAS, HDD, NVME, NIC, GPU, UPS, SW, RACK, PDU, WKR, CABLE, T3SUB) recorded in a version-controlled inventory file owned by SE11 and published through the hardware-baseline contract (§18.2). Record fields: inventory id; BOM reference (B1–B19); specification class (§11.4); part number as cited from SEED-01 and its evidence status (DEFERRED-PENDING-EVIDENCE / confirmed / superseded); serial number; firmware/BIOS/driver version at commissioning; physical position (slot id such as `M2_3`/`PCI_E1`, NAS bay, rack U); power domain (PD-A/PD-N/PD-B); failure-domain ids (§9); disposition and quantity status (§1.2); §6.1a row in force; signalling candidate and restart mechanism; pre-build evidence record id (§11.3); commissioning evidence ids (§14); warranty end; sanitisation state. Cables are labelled at both ends with the endpoint ids. The **configuration fingerprint** (§11.3) is derived from these records.

### 10.2 Remote-management capabilities where available

| Device | Out-of-band | In-band management path | Fallback |
|---|---|---|---|
| Central host | None (consumer board; no BMC/IPMI) — SE11-RISK-04 | Windows remote administration and Hyper-V management on `seg.mgmt`; MFA per §59 | Physical console in the lockable room; UEFI Flash BIOS and Clear CMOS on the rear panel (B3); RTC wake (M3) if evidenced |
| NAS | None | NAS OS web/remote administration on `seg.mgmt` | Front panel / USB; Wake-on-LAN (N1) if evidenced |
| Switch | Management port if the class provides one | Management VLAN | Console port |
| UPS-A / UPS-N | USB-HID to the host (S-1/S-3) or NAS (S-2/S-3) | Status via the UPS software's telemetry export | Front LCD |

### 10.3 Telemetry and health status (SE11-REQ-08, SE11-NFR-04; consumed by SE20 monitoring, SE01 capacity, SE19 validation, EL scheduler)

Mandatory signals from first power-on ("capture performance/resource telemetry from the first workloads", §160; "capture CPU, memory, I/O, network, queue time, job duration, reliability, and cost", §234): host CPU utilisation per VM and total, CPU-wait per VM, memory committed per VM and host against Table 5.3-R, NVMe SMART (temperature, media errors, percentage used, TBW consumed) per device, per-virtual-disk IOPS and latency (and `io.max` throttling counters when the guest limiter is in use), PCIe negotiated width/speed per slot (detects degraded M2_3/PCI_E3 sharing), NIC link speed and errors, NAS array state (healthy/degraded/rebuilding), per-drive SMART, NAS volume utilisation, snapshot success, backup and T3 job success/duration/throughput, **per-class `t3_last_ok(c)`, `age(c)` and protection state, platform `PL-*` state**, UPS state per UPS (online/on-battery/low-battery, load %, runtime estimate, battery charge %, battery age, communication state), restart-mechanism armed/fired events, host and NAS temperatures, switch port utilisation on L1/L2, and the event signals of SE11-DEC-11 (`SIG-ONBATTERY`, `SIG-SHUTDOWN`, `SIG-THERMAL`, `SIG-STORAGE-PRESSURE`, `SIG-PROTECTION-STATE`, `SIG-PL-STATE`). Thresholds that trigger expansion or revision are in §12.

### 10.4 Firmware / BIOS / driver lifecycle (SE11-REQ-09)

- Components with a firmware lifecycle: host UEFI/BIOS (incl. CPU microcode/AGESA), NVMe firmware ×4, NIC driver/firmware, optional GPU driver, NAS OS and HDD firmware, UPS firmware and host/NAS UPS software, switch firmware.
- Update path: vendor-signed images only, checksum verified against the vendor publication, staged in a declared maintenance window (§10.5) after a successful snapshot of all VMs and a verified T2 backup; one component class per window; rollback plan recorded; post-update SE11-AC-04 smoke subset executed; firmware settings baseline re-verified (SE11-AC-08), including "restore on AC power loss" and the RTC-wake/UPS-command settings of §8.3; configuration fingerprint updated.
- Ownership: SE20 schedules and executes; SE17 defines integrity controls (SE11-SECREQ-02); SE11 keeps the compatibility matrix (§11) current.

### 10.5 Maintenance windows

Hardware maintenance is performed only in a window declared to SE20's operations calendar that does not overlap a stage-gate VP validation (§174 "VP validation / release assurance"). Minimum window content: pre-checks (backup verified, snapshots taken, UPS healthy, all D-IRR classes PROTECTED or the exposure explicitly accepted by SE12), the change, post-checks (SE11-AC-04 smoke, telemetry nominal), inventory record and fingerprint updated.

## 11. Compatibility / availability assessment (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-10)

### 11.1 Structural compatibility check (from the BOM specifications themselves)

| Check | Items | Result from BOM data | Residual verification |
|---|---|---|---|
| Socket / chipset | B1 AM5 ↔ B3 AM5/X870 | Structurally compatible | BIOS version supporting the CPU: **not established** (§11.2) |
| Memory | B4 DDR5 UDIMM ↔ B3 "4× DDR5 DIMM, up to 256 GB" | Compatible at capacity; DDR5-6000 EXPO on four DIMMs is a stability-validated profile, not a guaranteed one (the seed prescribes the 5600/5200 fallback) | Exact population (2-DIMM M-A vs 4-DIMM M-B/M-A+) on the board's qualified list: **not established**; stability pass SE11-AC-04 |
| Cooler | B2 157 mm ↔ B8 ~166 mm clearance; AM5 mounting included | Compatible | — |
| Form factor | B3 ATX ↔ B8 ATX/E-ATX | Compatible | — |
| PCIe lane sharing | B10 in PCI_E3 (Gen4 x4, "shares with M2_3") ↔ B5 in M2_3 (Gen4 x2) | Simultaneous operation **not established** from BOM text | SE11-AC-02 read-back; Fallbacks A/B/C (§6.1a) |
| NIC in PCI_E1 (Fallback A) | B10 PCIe 3.0 x4 card in a Gen5 x16 CPU slot | Electrically and mechanically a subset; **operation not established** | SE11-AC-02 when Fallback A is used |
| M2_2 ↔ USB4 sharing | B6 on M2_2 ("sharing with USB4") | USB4 unused at baseline; no conflict | Confirm USB4 use does not down-shift M2_2: SE11-AC-02 |
| PSU | B7 750 W, 12V-2x6 ↔ B1 230 W + B11 145 W + platform | Within rating for the no-GPU build; GPU build conditional on measurement (seed condition) | SE11-AC-06 |
| GPU mechanical | B11 single-slot 241 mm ↔ B8 mid-tower, PCI_E1 x16 | Expected to fit; not asserted | SE11-AC-02 before adoption |
| NAS memory | B13 DDR5-4800 ECC SO-DIMM ↔ B12 "2 slots; 64 GB max"; mixed 16 + 32 GB | Capacity compatible; mixed pair support **not established** | SE11-AC-01 (deferred item) |
| NAS drives | B14 3.5-inch SATA CMR ↔ B12 8 SATA bays | Compatible | Online RAID 6 expansion support: **not established** (SE11-AC-01) |
| Network | B10 10GBase-T ↔ B12 2×10 GbE; Cat6a supplied with NAS (§228.1) | Compatible | Switch class 10GBase-T or SFP+ with matching transceivers: SE11-AC-05 |
| UPS | B15 1000 W ↔ PD-A loads (§8.2); NEMA 5-15P ↔ 15 A circuit (§231) | Compatible; runtime unknown until measured | SE11-AC-06 |
| UPS signalling and restart | B15 USB-HID / host software ↔ B12 network UPS server; commanded output power-cycle (M1); NAS client wait ≥ 240 s (S-2); RTC wake (M3); NAS WOL (N1) | **Not established** (§8.3) | SE11-AC-01, SE11-DEC-10, SE11-DEC-13 |
| OS / virtualization | B9 Windows 11 Pro ↔ Hyper-V; TPM 2.0 + Secure Boot prerequisites; Linux guest support; NIC driver for the virtual switch; per-virtual-disk IOPS controls; guest cgroup v2 `io.max` | Hyper-V is a Pro feature; TPM/Secure Boot are install prerequisites so the platform must provide them; NIC driver and storage-QoS availability **not established**; cgroup v2 `io.max` is a Linux guest facility whose availability on the chosen distribution is confirmed in SE11-AC-03 | SE11-AC-01, SE11-AC-03 |

### 11.2 Current manufacturer support and practical availability — NOT ESTABLISHED; consequence applied (corrects finding 008)

The allowed corpus contains no manufacturer support statement, firmware/BIOS release information, qualified-vendor list, driver compatibility statement or market availability for any BOM item, and SE11 has no access to manufacturer publications in this run. For every item the following are therefore **not established** and **not asserted** (BND-04): current manufacturer support status; a BIOS version supporting the CPU; the exact memory population on the board's qualified list; simultaneous PCI_E3/M2_3 operation; NIC driver support for the hypervisor virtual switch; hypervisor storage-QoS availability on the host OS edition; UPS software ↔ host OS, NAS ↔ UPS protocol, commanded output power-cycle, RTC wake and NAS WOL support; NAS online array expansion; practical availability of any part number.

**Consequence (SE11-DEC-14).** Rather than baselining an unverified part-number combination, this document (a) **defers every part number** (B1–B17: DEFERRED-PENDING-EVIDENCE, §1.2); (b) **baselines specification classes** (§11.4) and candidate ids, which are satisfiable by any current item of the class and so cannot be "impossible or obsolete"; (c) records that **no buildable bill and no configuration fingerprint exist** at this version; (d) keeps the baseline PROVISIONAL and not approved for implementation (§17). QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 is thereby addressed by design change; **its evidence-level outcome remains UNMET** and is closed only by the pre-build evidence record of §11.3, which is a separate activity from the commissioning tests of §14.

### 11.3 Pre-build support evidence record (SE11-AC-01) and configuration fingerprint

**Pre-build checks (before any build, per item; dated and attributable):** manufacturer support status; BIOS/firmware version required for the combination; memory population and profile on the qualified list; slot coexistence statement (PCI_E3/M2_3; PCI_E1 with a Gen3 x4 card for Fallback A); driver/OS/hypervisor support statement; storage-QoS and guest `io.max` availability; UPS software/protocol statement, commanded output power-cycle (M1), NAS client wait (S-2), RTC wake (M3), NAS WOL (N1); NAS online expansion; availability statement. Evidence record fields: item (B-id), part number as cited, claim checked, source (publisher, document title/version, date accessed), result (confirmed / not confirmed / superseded), consequence (part number confirmed into the fingerprint / substitute within the class per §11.4 with a new SE11-DEC / defer), recorder. "Not confirmed" on any item keeps that part number deferred; a superseded item is substituted by specification class and recorded (SE11-REQ-12).

**Commissioning tests (after build, §14):** SE11-AC-02 … SE11-AC-15 measure what the built configuration actually does; they never substitute for the pre-build record.

**Configuration fingerprint.** Sign-off (§17) binds to the exact evidenced configuration: the ordered list of (B-id, confirmed part number, serial, firmware/BIOS/driver version, slot/bay position, memory population and candidate M-x, NAS candidate N-x, §6.1a row in force, signalling topology S-x, restart mechanism M-x/N-x, protection-state defaults A_max/G). Any change to the fingerprint re-opens SE11-AC-01 for the changed item and SE11-AC-10 for the baseline. **Fingerprint at v3: none.**

### 11.4 Specification classes — what is baselined (not procurement preference; preserve performance, reliability, security, portability and schedule assumptions)

| BOM item | Specification class (baselined) |
|---|---|
| B1 CPU | AM5 desktop CPU, ≥ 16 physical cores, ≥ 64 MB L3, ≤ 230 W package, hardware virtualization + IOMMU |
| B2 cooler | Dual-tower air cooler ≤ 160 mm height with AM5 mounting, rated ≥ 230 W |
| B3 motherboard | ATX AM5, 4×DDR5 to ≥ 256 GB, ≥ 1× PCIe x16 (CPU) + ≥ 1× PCIe x4 slot usable concurrently with ≥ 4× M.2 (≥ 2 of them x4), ≥ 2.5 GbE onboard, UEFI Secure Boot, TPM 2.0, "restore on AC power loss" setting, RTC wake |
| B4 memory | Matched DDR5 UDIMM kit per candidate (Table 5.3-R), ≥ DDR5-5200 validated at the chosen population; ECC-capable platform class is the recorded substitute if SE11-RISK-02 materialises |
| B5/B6 NVMe | M.2 2280 PCIe 4.0 x4 (or 5.0), TLC with DRAM, ≥ 600 TBW per TB, 5-year warranty class; devices with power-loss protection are the recorded upgrade class if SE11-AC-13 shows unrecoverable corruption |
| B7 PSU | ATX 3.1 / PCIe 5.1, ≥ 750 W, Cybenetics Gold or better, native 12V-2x6, fully modular, ≥ 7-year warranty class |
| B8 case | Mid-tower ATX with mesh front, ≥ 160 mm cooler clearance, ≥ 250 mm GPU clearance |
| B9 OS | Windows 11 Pro-class edition with Hyper-V, TPM 2.0/Secure Boot support |
| B10 NIC | 10GBase-T (or SFP+ with matching switch), PCIe 3.0 x4 or 4.0 x2 minimum, driver supporting the Windows Hyper-V virtual switch; operable in a x16 CPU slot (Fallback A) |
| B11 GPU | Single-slot, ≤ 145 W, ≥ 24 GB ECC VRAM, PCIe x16, 12V-2x6 or 8-pin; larger classes ESCALATE |
| B12 NAS | 8-bay SATA NAS with ECC memory, ≥ 2×10 GbE, Btrfs/ZFS-class snapshots, per-folder/volume AES-256, UPS integration (any of S-1/S-2/S-3), power-on after AC recovery, M.2 cache slots; hosted object storage is the equivalent for T2/T3 under G-LOCAL |
| B14 HDD | 3.5-inch enterprise CMR, 7,200 RPM, ≥ 2.5 M h MTBF, ≥ 550 TB/yr workload, 5-year warranty, ≥ 20 TB (smaller same-class drives permitted under N-A if V is small) |
| B15/B16 UPS | Pure-sine line-interactive with AVR, USB-HID, ≥ 1500 VA / 1000 W (PD-A) and ≥ 1000 VA / 600 W (PD-N / PD-B), user-replaceable batteries, commanded output shutdown with auto-restart (M1) preferred; higher-runtime units of the same class are the remedy under §8.4 |
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
| TRG-MEM-EXPAND (M-A/M-C only) | Measured committed memory p95 > 80 % of installed for one stage **and** the Step-1/Step-2 re-balance of §5.3 recorded as insufficient | Add the second matched pair (M-A+; re-run SE11-AC-04 memory pass); record SE11-DEC |
| TRG-NAS-MEM | NAS memory sustained > 70 % or snapshot/backup jobs missing their window from memory pressure | Install B13 |
| TRG-NAS-CAP | T2 utilisation > 70 % | Add same-class drives to free bays (N-A → N-B) |
| TRG-NET-10G | L1 utilisation > 70 % sustained during backup windows, or a second 10 GbE consumer | Use NAS second 10 GbE / add 10 GbE ports within the switch class |
| TRG-NVME-TBW | Any NVMe > 80 % of rated TBW or media errors (M2_2 watched closely under Fallback B) | Replace with same class (§11.4) |
| TRG-UPS-BATT | Any UPS runtime estimate at measured load < B_u / 0.7 | Battery replacement (same class) or §8.4 remedies |

### 12.3 Scale-out versus scale-up boundaries and architecture-revision triggers

The central node complements, never replaces, horizontally scalable workers (§177). Scale-out (more workers, hosted executors) is the default answer to throughput; scale-up applies only to the capabilities the seed assigns to the central node — large contiguous RAM, low-latency CPU, NVMe, centralized data/control services (§161). The following require a revision of this architecture (new SE11 version plus EL review), not a hardware addition:

| Revision trigger | Why adding hardware is insufficient |
|---|---|
| REV-MEM: Highest-priority pool floors exceed 85 % of 256 GB on measured p95 | Board ceiling reached; second host, larger-memory platform class, or hosted data services (M-C) is an architectural choice |
| REV-HA: an SLO (§117) requires the control plane or Data VM to survive FD-HOST or FD-NVME-M2_4, or requires unattended restart that no evidenced mechanism provides | Needs a second failure domain and quorum design (§173) |
| REV-GPU-CLASS: accelerator > 145 W, dual-slot, or second accelerator | Exceeds PSU, slot and thermal envelope (§5.5) |
| REV-STORAGE-HOT: T1 > 85 % after device scale-up, a random-IO workload that cannot stay on host NVMe, or the double-fallback of §6.1a failing SE11-AC-12b with no admissible alternative | NAS is not a hot tier (§164); host NVMe topology exhausted |
| REV-STORAGE: retention volume V > 44 TiB (§6.7) | Beyond the enclosure's economical RAID 6 envelope; hosted tier or second enclosure is architectural |
| REV-NET: storage/core path saturated after all 10 GbE ports used, or 25 GbE class needed | Switch and NIC class change ripples through host slots |
| REV-SITE: geographic/resilience footprint beyond one room (§226 F.20) | Hosted/hybrid footprint decision |
| REV-POWER: §8.4 remedies exhausted, PD-A measured peak within 20 % of UPS-A rating, circuit limits reached, or no restart mechanism meets the SLO | UPS/circuit redesign by qualified professionals; possible relocation |

## 13. Security considerations (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-11)

The owners of the control catalogue (SE17 for infrastructure/workload/data security, SE15 for identity and cryptography, §74) have not published control ids in this run (their documents are absent, §0.1). This section therefore states SE11's hardware security **requirements** under SE11's own identifiers; mapping each to the owner's control id is unmet dependency **SE11-DEP-05**, and no foreign id is invented. Nothing here re-derives a control design.

| Id | Requirement placed on the hardware baseline | Proposed owner for the control | Verified by |
|---|---|---|---|
| SE11-SECREQ-01 Trusted boot | UEFI Secure Boot enabled; TPM 2.0 present and enabled; boot order locked to M2_1; UEFI administrator password set; measured-boot attestation is the owner's decision; the RTC-wake and AC-recovery settings of §8.3 are part of the protected firmware baseline | SE17 | SE11-AC-08 |
| SE11-SECREQ-02 Firmware integrity | Vendor-signed images only, checksum verified, staged in maintenance windows with snapshot + verified backup first (§10.4); firmware settings baseline re-verified after every BIOS update | SE17 (policy), SE20 (execution) | SE11-AC-08 |
| SE11-SECREQ-03 Management-plane isolation | All management endpoints (host admin, hypervisor, NAS admin, switch, UPS software, shutdown/WOL command paths) only on `seg.mgmt`, unreachable from `seg.build`, `seg.worker`, `seg.egress`; MFA and least-privilege, short-lived credentials per §59, §112; no management interface exposed to the internet; the NAS shutdown command (S-1) is authenticated | SE17 (network policy), SE15 (identity) | SE11-AC-05, SE11-AC-08 |
| SE11-SECREQ-04 Physical and administrative access | Lockable room; host, NAS, switch and UPS inside; the T3-SUB medium outside it under SE17's custody rule; physical console use is a logged administrative action; segregation between hardware maintenance (SE11/SE20) and security configuration (SE17) per §112 | SE17 | SE11-AC-08 |
| SE11-SECREQ-05 Data at rest | Host full-disk encryption on M2_1 with TPM-bound keys; encryption of VM disks on M2_2/M2_4 inside the Linux VMs or by the hypervisor (hardware supports both; owner decides); NAS per-folder AES-256 (B12) for backups, evidence and archives; T3 and T3-SUB copies encrypted before leaving the site; key custody and recovery under the owner's control, with the `KEYS` class itself PROTECTED (§6.3) | SE17, SE15 (keys) | SE11-AC-08 |
| SE11-SECREQ-06 Media sanitisation | NVMe, HDD and T3-SUB media sanitised on decommissioning/RMA; inventory record marks sanitised state | SE17 | SE11-AC-10 |
| SE11-SECREQ-07 Supply chain at receipt | Serial numbers recorded; packaging/tamper evidence inspected; firmware version read and compared with the vendor's published current version before first power-on; default credentials on NAS, switch and UPS software rotated at commissioning | SE17 | SE11-AC-01 (pre-build), SE11-AC-10 |
| SE11-SECREQ-08 Confidential-processing boundary | Private application/customer data is processed only by authorised locally hosted models or deterministic tools (§66); any local accelerator (B11) and the Data VM sit inside `seg.platform` behind the default-deny disclosure gateway on `seg.egress`; hardware telemetry export (§10.3) carries no workload content; candidate M-C (hosted data) is admissible only where §66 permits | SE17, EL | SE11-AC-05, SE11-AC-09 |

## 14. Validation / evidence plan (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-14)

Pre-build checks (AC-01, AC-11) are separate from commissioning tests (AC-02 … AC-15); commissioning never substitutes for the pre-build record (§11.3). Executing owners are named; where the owner's test or operations contract does not yet exist the dependency id is given.

| AC id | Check | Pass criterion | Evidence artefact | Executing owner | Needed before |
|---|---|---|---|---|---|
| SE11-AC-01 | **Pre-build** support, compatibility and availability evidence record (§11.3) | Every B1–B17 item has a dated, attributable record for each claim in §11.3; part numbers move from DEFERRED-PENDING-EVIDENCE to confirmed, substituted within class (new SE11-DEC) or deferred; signalling candidate S-1/S-2 evidenced or S-3 adopted; restart mechanism M1 or M3 (+N1) evidenced or M4 recorded; S-2 NAS client wait ≥ 240 s evidenced if S-2; receipt check (SE11-SECREQ-07) complete | Evidence record attached to the inventory; configuration fingerprint v0 | SE11 (SE20 assists at receipt) | Any build |
| SE11-AC-11 | **Pre-build** reconciliation of this document to PL-REQ-ID-REGISTER rows (via the §0.5 crosswalk) and to EL/PM09/NT16/SP16 decisions once they exist (SE11-DEP-01/02/08/09/10) | Every row of §0.5 carries a register id; every ADR checked against EL ADRs; NFR values bound to EL/PM09 NFR ids or recorded as conflicts; C1–C6 resolved by reviewers; status PROV → REC | Reconciliation table in a later version of this document | SE11, EL review | Baseline status above PROVISIONAL |
| SE11-AC-02 | Slot, lane and mechanical verification | Negotiated PCIe width/speed for M2_1–M2_4 and the NIC slot with all devices installed; PCI_E3/M2_3 coexistence confirmed or Fallback A/B/C invoked and recorded (SE11-DEC-02/12); cooler/case clearance photos; GPU mechanical check when B11 is triggered | Link-state dump; inventory photos | SE11 | Stage 1 |
| SE11-AC-03 | OS / virtualization enablement and reservation mechanism | Hyper-V operational with the four VMs at the §4 reserve/limit/weight settings and the Table 5.3-R memory lines of the installed candidate; admission rule (§5.2) encoded in version-controlled definitions; hypervisor storage QoS present **or** guest `io.max` limiter configured per the §6.1a row in force; NIC bound to the virtual switch at 10 Gb/s; Secure Boot + TPM reported enabled; "restore on AC power loss" and RTC wake settings verified; GPU-to-VM path evaluated when triggered | Hypervisor and guest configuration export | SE11 with EL (SE11-DEP-02) | Stage 1 |
| SE11-AC-04 | Burn-in and performance baseline (SE11-NFR-08) | ≥ 24 h combined CPU/memory/NVMe stress with zero memory errors at the chosen DDR5 profile (fallback 5600/5200 per B4) at the installed population; thermals within limits; NVMe sequential/random, **D2 and L2 for M2_2 (§6.1a)**, per-virtual-disk and L1 throughput recorded as the measured replacement for §6.4 | Stress logs; telemetry export; baseline table | SE19 (executes, SE11-DEP-06), SE11 (accepts) | Stage 1 |
| SE11-AC-05 | Network path and segmentation (SE11-NFR-02, SE11-SECREQ-03) | Host↔NAS ≥ 0.7 GB/s sustained 10 min under concurrent build-cache load **with the NIC in the slot actually in use** (Fallback C admissible only on pass); `seg.*` enforced; management plane unreachable from build/worker/egress segments | Throughput log; segmentation test log | SE11 (physical design/test), SE17 (policy, SE11-DEP-05), SE19 (measurement) | Stage 1 |
| SE11-AC-12 | CPU contention and weighted-service test (SE11-NFR-01) | Profile: Build VM 100 % CPU on all 16 vCPU, Validation VM 100 % on 8 vCPU, `pool.background` saturating inside Build, host root busy, T1→T2 backup transfer running on L1; measured: Core/Data CPU-wait ≤ 5 %, Core probe p95 ≤ 1.5 × baseline, Data random-read p99 ≤ 2 × baseline, Validation CPU-wait ≤ 10 %, Build ≥ 11 LP-equivalents, background ≤ 10 % of Build VM CPU | Load-test report with per-VM CPU share | SE19 (executes), SE11 (accepts) | Stage 1 before stable-runtime baseline |
| SE11-AC-12b | Storage contention and critical-validation I/O test (SE11-REQ-16) | For the §6.1a row in force: Build drives every M2_2-backed virtual disk (and scratch where it is) at queue depth 32 for 10 min; Validation 4 KiB random-read p99 ≤ 2 × L2 and achieved IOPS ≥ V_min throughout; limiter counters show B_max enforced. Fail → the row is inadmissible; apply §6.1a remedies | fio/latency report per disk; limiter configuration | SE19 (executes), SE11 (accepts) | Stage 1 before any Validation workload on M2_2 |
| SE11-AC-06 | Power measurement and mains-loss drills (SE11-NFR-03; fail-closed §8.4) | Measured load of every power domain (idle, typical, full stress, with/without GPU); measured runtime R_u for every UPS of the selected candidate at full-stress load (**S-3: R_N measured separately at NAS load**); drills: (a) full outage past exhaustion — S1 → S6 with every step inside its bound and B_u ≤ 0.7 R_u; (b) mains restored during S1 — return to S0, no shutdown; (c) mains restored during S2 — sequence completes unaborted, restart via the selected mechanism within T_restart ≤ 10 min; (d) mains restored in S3/S4 before output drop — same as (c); (e) second outage while charge < 50 % — host-only shutdown within 90 s, no VM start; (f) S-2 only: NAS waits ≥ 240 s for the client; VMs and NAS return clean in every drill; electrician's sign-off of circuits on file (SE11-REQ-10) | Power table per domain; drill log with timestamps per step and scenario; professional sign-off reference | SE11 (measurement), SE20 (drill, SE11-DEP-07), qualified electrician (circuits, SE11-DEP-12) | Stage 1 before stable-runtime baseline |
| SE11-AC-15 | Restart-mechanism drill (SE11-REQ-15, FD-RESTART) | M1: output power-cycle observed ≈ 90 s after host off, re-energise on mains, host and NAS auto-power-on, T_restart ≤ 10 min; or M3: RTC wake fires once, host checks UPS state, continues or shuts down host-only, NAS woken by N1; M4: alert delivered and procedure documented (recorded as exposure, not a pass for unattended SLOs) | Drill log; UPS event log | SE20 (drill), SE11 (accepts) | Stage 1 |
| SE11-AC-14 | Signalling-path-loss drill (FD-SIGNAL) | (a) USB/UPS-software path removed while on mains: alert ≤ 300 s; (b) S-1 NAS command path removed during S2: host completes its sequence inside 270 s and the NAS follows its own fallback; (c) S-2 NAS→host notification path removed: host treats as E4; (d) communication lost then mains lost: outcome recorded as abrupt loss and handled by SE11-AC-13 | Drill log | SE20 (drill), SE11 (accepts) | Stage 1 |
| SE11-AC-13 | Abrupt-loss drill (FD-UPS-A / FD-UPS-N, SE11-NFR-07) | UPS output removed under the SE11-AC-12/12b contention profile; on restart every VM and host filesystem and the NAS array pass integrity checks with zero unrecoverable errors; database loss ≤ last committed transaction (SE12 verifies, SE11-DEP-04); scrub completes | Integrity-check logs; SE12 verification record | SE19/SE20 (drill), SE12 (data), SE11 (accepts) | Stage 1 before any D-IRR admission |
| SE11-AC-07a | T1→T2 protection (`PL-T2`) | Snapshot + replication verified; restore of a VM and a database from T2 to a clean volume within SE11-NFR-05 (SE12's binding RTO if stricter); NAS single-drive pull with rebuild time recorded (replaces ASM-SE11-04) | Restore drill log; rebuild timing | SE12 (policy, SE11-DEP-04), SE19/SE20 (drill) | Stage 1 |
| SE11-AC-07b | T3 activation per D-IRR class (`PROTECTED`) | For each class: T3 mechanism commissioned; copy interval ≤ A_max demonstrated; restore of the class from T3 verified; T3 and T3-SUB encryption and key recovery verified (SE11-SECREQ-05); T3-SUB copy and restore verified; `t3_last_ok(c)` published | T3 inventory; restore log | SE12 (policy), SE17 (keys), SE20 (drill) | **Before the first dataset of that class exists** (REPO: before local commissioning; DB/EVID/INV/KEYS: before non-synthetic data enters the platform) |
| SE11-AC-07c | Protection-expiry drill (§6.3, FD-INTERNET) | Starting with a class at `age` = A_max − 1 h, cut the T3 path: DEGRADED-IN-BUDGET at +1 h with `SIG-PROTECTION-STATE` raised ≤ 60 s and creation of a new dataset of that class refused; EXPIRED at +25 h with either a T3-SUB copy ≤ A_max old permitting mutation or the owning service's write-freeze observed; restore the path: full copy, restore verification, PROTECTED, freeze lifted | Drill log with state transitions and permission checks | SE20 (drill), SE12 and EL (enforcement, SE11-DEP-02/04), SE11 (accepts) | Stage 1 before any D-IRR class other than REPO is activated |
| SE11-AC-08 | Security baseline of hardware | SE11-SECREQ-01 … 08 verified against the inventory ids; default credentials rotated; encryption active where required | Owner control evidence referencing inventory ids | SE17 (SE15 for keys/identity; SE11-DEP-05) | Stage 1 (host, NAS); full at Stage 3 |
| SE11-AC-09 | Telemetry coverage (SE11-NFR-04) | Every §10.3 signal and every SE11-DEC-11 event visible in SE20 monitoring with alert thresholds from §12.2 and the per-class protection states | Dashboard/alert export | SE20 (SE11-DEP-07) | Stage 1 |
| SE11-AC-10 | Inventory and baseline sign-off | Inventory complete; configuration fingerprint recorded; platform in `PL-T2` (no D-IRR) or `PL-T3` (all classes PROTECTED) — never `PL-DEG`/`PL-EXP`; §6.1a row and restart mechanism recorded; §17 record filled with evidence ids of AC-01 … AC-15; contract record (§18.2) updated | Signed baseline record | SE11 | Before downstream consumption as "VERIFIED" |

Resilience tests beyond the above (fault injection on `pool.validate`, switch loss, NAS loss, provider loss, uplink loss) are specified and run by SE19 against the §9 domains; SE11 supplies the physical means (spare cables, drive-pull and power-cut procedures) and accepts the evidence.

## 15. Exclusions (BND-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01 … AR-04)

| Exclusion | Disposition in this document |
|---|---|
| BND-01 Purchase orders, price negotiation, vendor-selection scorecards, procurement workflow | Excluded. No prices, suppliers, order quantities or purchase approvals appear; part numbers are cited only as the seed's reference exemplars and are not baselined (SE11-DEC-14); alternatives are by specification class (§11.4). Nobody owns procurement in this chain. |
| BND-02 Project-owned acquisition dates | Excluded. Only dependency windows are referenced ("Stage 1", "before the first dataset of the class"); no calendar dates. |
| BND-03 Detailed software/container/service design owned by existing SE11 artefacts | Excluded. §4–§6 stop at pools, VM boundaries, hypervisor reservation controls, limiter configuration and volume mapping; service design, images, pipelines and the scheduler's shedding controller are referenced to EL and SE11's runtime artefacts. The cgroup share and `io.max` defaults are budget boundaries, not service design. |
| BND-04 Unverified assumptions presented as confirmed hardware facts | Complied with. Every non-seed figure is an engineering assumption (ASM-SE11-nn) or a validation gate (SE11-AC-nn); support, compatibility and availability are explicitly **not established** and part numbers are deferred (§11.2); no vendor protocol, restart or compatibility capability is asserted (§8.3). |

## 16. Architecture risks, decisions and ADRs (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-13)

### 16.1 Architecture decision records (all PROV, §0.2)

| ADR | Decision | Alternatives considered | Rationale |
|---|---|---|---|
| SE11-ADR-01 | The **candidate** physical architecture is one central node + durable NAS + elastic hosted-first worker pool. Each local element passes gate **G-LOCAL** before it is provisioned: workload evidence *and* economics justify it (§238), and no managed/hosted equivalent better satisfies the target requirements. Until G-LOCAL evidence exists (SE11-DEP-03/08), every pool may be delivered locally or hosted | (a) Two-node local cluster from day one — rejected now: no measured need, violates no-overbuild (§158). (b) All-hosted — **not rejected**: the seed's acceptable equivalent (§238, §160) and the fallback for FD-HOST/FD-ROOM; §66 favours local handling of confidential data but does not mandate local hardware | §160, §226, §238 |
| SE11-ADR-02 | Windows 11 Pro host with Hyper-V Linux VMs for all durable services; WSL2 for interactive use only | Bare-metal Linux hypervisor — rejected: the seed fixes the preferred operating model (§166) and retains Windows for workstation/admin use (§227.9); portability is preserved at the VM/container-definition level (§168) | §166–§168 |
| SE11-ADR-03 | Non-ECC DDR5 on the consumer AM5 platform accepted for the central node, monitored | ECC workstation/server class — recorded substitute if memory-error telemetry or data-integrity incidents attributable to memory occur (SE11-RISK-02) | §227.4; durable tier (NAS) is ECC (§228.1) |
| SE11-ADR-04 | GPU deferred; adoption gated by §5.5 and TRG-GPU; accelerator class capped at single-slot ≤ 145 W within this architecture | Adopt at first build — rejected: §175/§177 make it optional and demand-driven; external providers are the default (§160) | §175–§177 |
| SE11-ADR-05 | Host NVMe as independent volumes without RAID; NAS as durable/backup tier only; one-way replication T1 → T2 → T3 | Host NVMe mirroring — rejected (does not address FD-HOST; doubles cost); NAS as live VM datastore — rejected (§164: not a latency substitute; would make FD-STORAGE a hot-path SPOF) | §163, §164 |
| SE11-ADR-06 | UPS signalling is a **gated** selection among S-1 (preferred), S-2 and S-3 (§8.3), decided by SE11-DEC-10 on pre-build evidence; shutdown order NAS-command ‖ Build ‖ Validation → Core → Data → host; per-candidate budgets; restart by an evidenced mechanism (SE11-DEC-13) | v1 chose S-2 without compatibility evidence — demoted to a candidate; firmware AC-recovery alone as the restart mechanism — rejected (does not fire without an AC-input cycle) | §165, §228.1, §229.1 |
| SE11-ADR-07 | Single managed switch, ≥ 2×10 GbE minimum (seed), ≥ 4×10 GbE preferred, adopted ahead of the rack (conflict C4), powered from PD-A (conflict C1); interim point-to-point 10 GbE allowed as placement | Unmanaged switch — rejected (segmentation needs VLANs); dual redundant switches — rejected now (§166 "purchased incrementally from measured need"); no switch until the rack — rejected (management segment and VLAN enforcement need it) | §166, §230 |
| SE11-ADR-08 | Capacity **quantities** (memory kit, NAS drive count) are candidates governed by decision rules (§5.3, §6.7) and the seed's H.1/H.3 default to the smaller configuration; the maximum listed configuration is never adopted on the strength of this document or of a single oversized component | Adopt the seed's listed quantities as given — rejected: ENV-DEC-017, §162, §238; single-component trigger to the maximum — rejected (finding 002) | §158, §162, §234, §238 |
| SE11-ADR-09 | Storage mapping places Highest-priority VM disks on M2_4 and High/Medium VM disks + artifacts on M2_2 (§6.1), deviating from the BOM's literal role labels (C2), with a mandatory limiter for Validation versus Build on M2_2 in every lane × QoS combination (§6.1a) | Literal seed mapping (all VMs on M2_2) with IOPS controls only — rejected: puts Highest and Medium pools on one device, contrary to §157 and SE11-REQ-02; device separation alone as the QoS fallback — rejected (finding 005): leaves Validation unprotected | §157, §163, §174 |
| SE11-ADR-10 (new) | At the hardware layer, priority is implemented as **weighted contention** (hypervisor reserves/limits/weights, in-VM cgroup weights) with measurable guarantees (SE11-NFR-01); **load shedding** is a scheduler action owned by EL/SE01 and driven by SE11-published signals (SE11-DEC-11); SE11 designs no shedding controller | Hardware-layer "throttling order" claim (v2) — rejected: not implementable without a controller; a SE11-owned shedding controller — rejected: §175 assigns it to the scheduler, and it is service design (BND-03) | §157, §174, §175 |

### 16.2 Decisions (SE11-DEC-nn; all PROV)

| Id | Decision | Impact |
|---|---|---|
| SE11-DEC-01 | B1 class adopted with virtualization/IOMMU enabled and 230 W package limit as the compute power line | §8.2; SE11-AC-04 |
| SE11-DEC-02 | B3/B5/B10 classes adopted with the PCI_E3–M2_3 lane-sharing constraint; outcome recorded from SE11-AC-02 (OK / Fallback A / B / C per §6.1a) | §6.1a; SE11-AC-02 |
| SE11-DEC-03 | B4 adopted as a specification class; quantity is a candidate (M-A default; M-B/M-A+/M-C) selected by the Table 5.3-R rule in SE11-HARDWARE-CAPACITY-SIZING (recorded there as SE11-DEC-03a with the aggregate calculation and the Step 1/Step 2 outcomes); 256 GB not adopted here | §5.3; SE11-RISK-02, SE11-RISK-10 |
| SE11-DEC-04 | B7 adopted; GPU power conditional on SE11-AC-06; > 145 W class escalates | §5.5; REV-GPU-CLASS |
| SE11-DEC-05 | B13 deferred to TRG-NAS-MEM | stock 16 GB ECC until telemetry justifies |
| SE11-DEC-06 | B14 adopted as a drive class with RAID 6 mandatory; count is a candidate (N-A/N-B/N-C) selected by the §6.7 rule with SE12's retention model (recorded as SE11-DEC-06a); six drives not adopted here | §6.7; SE11-RISK-06, SE11-RISK-10 |
| SE11-DEC-07 | Shutdown state machine, per-candidate timed sequences, budgets B_A/B_N and the fail-closed outcome of §8.4 | SE11-REQ-06, SE11-NFR-03 |
| SE11-DEC-08 | Switch adopted by class now on PD-A (C1, C4); rack/PDU/trays/UPS-B/local workers deferred to TRG-WKR-LOCAL | §7.2, §8.1, §12.2 |
| SE11-DEC-09 | Authoritative volume mapping of §6.1; Highest-priority VMs on M2_4; deviation from literal BOM role labels recorded with reason and impact (C2) | §6.1, §9 |
| SE11-DEC-10 | UPS signalling topology gated: S-1 preferred, S-2 alternative (admissible only with NAS client wait ≥ 240 s), S-3 automatic fallback (topology substitution of B15, C3); none relied on before SE11-AC-01/06/14/15 | §8.3; SE11-RISK-11 |
| SE11-DEC-11 (new) | SE11 publishes the hardware signals `SIG-ONBATTERY`, `SIG-SHUTDOWN`, `SIG-THERMAL`, `SIG-STORAGE-PRESSURE`, `SIG-PROTECTION-STATE`, `SIG-PL-STATE` within 60 s of the condition; the shedding policy that consumes them is EL/SE01's (SE11-DEP-02/03) | §4, §8.3, §10.3 |
| SE11-DEC-12 (new) | Lane-sharing Fallback A: if PCI_E3 and M2_3 cannot coexist and the GPU is deferred, the NIC moves to PCI_E1 and scratch stays on M2_3; TRG-GPU then requires Fallback B or C with a passed SE11-AC-12b before PCI_E1 is released | §6.1a, §5.5 |
| SE11-DEC-13 (new) | Restart after shutdown: M1 (commanded UPS output power-cycle with auto-restart) is mandatory where evidenced; M3 (RTC wake + N1 NAS WOL) where M1 is not; M4 (attended) is the fail-closed residual that blocks baselines whose SLO requires unattended recovery | §8.3, SE11-REQ-15, SE11-RISK-12 |
| SE11-DEC-14 (new) | Every seed part number (B1–B17) is DEFERRED-PENDING-EVIDENCE; the baseline is bound to specification classes (§11.4) and candidate ids; a part number enters the configuration fingerprint only with a "confirmed" SE11-AC-01 record | §1.2, §11.2, §11.3, §17 |

### 16.3 Requirements introduced by this document (SE11-REQ-nn; all PROV)

| Id | Requirement | Verified by |
|---|---|---|
| SE11-REQ-01 | Hard reservations (static memory, 100 % processor reserve) for `pool.core`, `pool.data`, `pool.runtime`; every other pool has a declared floor/ceiling or an explicit shared-budget membership with a stated share | SE11-AC-03, SE11-AC-12 |
| SE11-REQ-02 | No Highest-priority pool shares a physical NVMe device with a Medium-priority pool | SE11-AC-02/03 (mapping §6.1) |
| SE11-REQ-03 | T0/T1 is never the sole copy of D-IRR or D-BND data; every T1 dataset has a T2 copy; every D-IRR class has a verified T3 copy with age tracked per §6.3 | SE11-AC-07a/b/c |
| SE11-REQ-04 | L1 sustains ≥ 0.7 GB/s host↔NAS under concurrent build-cache load with the NIC in its actual slot; shared paths are not the first bottleneck | SE11-AC-05 |
| SE11-REQ-05 | VM/container definitions carry no physical slot ids, serials or host names (portability §160) | SE11-AC-03 review |
| SE11-REQ-06 | For every UPS of the selected candidate, B_u ≤ 0.7 × measured R_u; every step bounded; fail-closed if unmet | SE11-AC-06, SE11-AC-14 |
| SE11-REQ-07 | Inventory identity scheme, record fields and configuration fingerprint (§10.1, §11.3) for every asset and cable | SE11-AC-10 |
| SE11-REQ-08 | Telemetry signals of §10.3, including per-class protection states and the SE11-DEC-11 events, exported from first power-on | SE11-AC-09 |
| SE11-REQ-09 | Firmware/driver lifecycle per §10.4 with snapshot + verified backup precondition | SE11-AC-08, SE20 |
| SE11-REQ-10 | Electrical circuits verified and, where needed, installed by a licensed electrician against §8.2 load figures; SE11 designs no electrical work | SE11-AC-06 sign-off reference |
| SE11-REQ-11 | Downstream documents cite this document id **with its status (PROVISIONAL in v3)**, the B-id + class disposition + quantity status they rely on, the §6.1a row, and the §9 failure-domain ids | EL review (SE11-DEP-02) |
| SE11-REQ-12 | Any substitution of a dispositioned item is recorded as a new SE11-DEC with technical reason and impact before use; silent substitution is prohibited | SE11-AC-10 |
| SE11-REQ-13 | Protection activation: a D-IRR dataset of class c may be created only while class c is PROTECTED; in `PL-T2` only D-BND/D-REB data exist (§6.3) | SE11-AC-07b, SE11-AC-10 |
| SE11-REQ-14 | Reservation mechanism: hypervisor processor reserve/limit/weight, static vs dynamic memory per Table 5.3-R, storage limiter per §6.1a, in-VM cgroup shares; admission rule of §5.2 | SE11-AC-03, SE11-AC-12 |
| SE11-REQ-15 (new) | A restart mechanism that re-powers host and NAS after a controlled shutdown without depending on an AC-input cycle (M1, else M3 + N1) is commissioned; T_restart ≤ 10 min; the low-charge rules of S5 apply | SE11-AC-15, SE11-AC-06 (c)(d)(e) |
| SE11-REQ-16 (new) | Validation versus Build storage protection on M2_2: for the lane × QoS combination in force, a limiter (hypervisor QoS or guest `io.max`) enforces V_min / B_max per the §6.1a calibration rule; the double-fallback is admissible only on a passed SE11-AC-12b | SE11-AC-03, SE11-AC-12b |
| SE11-REQ-17 (new) | Per-class protection states with `t3_last_ok`, A_max and G; creation prohibited outside PROTECTED; mutation in EXPIRED only under a current T3-SUB copy, else write-freeze; outage tolerance = remaining copy-age budget; states published as signals | SE11-AC-07b/c, SE11-AC-09, SE11-AC-10 |

### 16.4 Risks

| Id | Risk | Likelihood / impact | Mitigation | Owner |
|---|---|---|---|---|
| SE11-RISK-01 | Single central host is the control-plane and data failure domain (FD-HOST, FD-NVME-M2_4) | Medium / High | SE11-REQ-05, T2/T3, hosted fallback (ADR-01), REV-HA | SE11, EL |
| SE11-RISK-02 | Non-ECC host memory → silent corruption in the Data VM | Low / High | SE11-AC-04 memory pass; database checksums and backup verification (SE12); ECC class substitute (ADR-03) | SE11, SE12 |
| SE11-RISK-03 | PCI_E3/M2_3 sharing reduces bandwidth or is mutually exclusive | Medium / Medium | SE11-AC-02; Fallbacks A/B/C (§6.1a) | SE11 |
| SE11-RISK-04 | No out-of-band management; a hung host needs physical presence | High / Medium | Physical console; SE20 auto-restart policy; REV-HA if SLOs require | SE11, SE20 |
| SE11-RISK-05 | Support or availability of a reference part number has lapsed (BOM v2.2 is a point-in-time reference; nothing is established, §11.2) | **High** / Medium | Part numbers deferred (SE11-DEC-14); §11.4 classes; SE11-AC-01 before any build; SE11-REQ-12 | SE11 |
| SE11-RISK-06 | Long RAID 6 rebuild at 20 TB exposes the array to a third failure | Low / High | RAID 6; T3; rebuild timing measured (AC-07a); hot-spare option | SE12, SE11 |
| SE11-RISK-07 | UPS runtime at measured load insufficient for the per-candidate budget (notably S-2's 450 s) | Medium / High | Fail-closed §8.4 remedies incl. candidate change; TRG-UPS-BATT | SE11, SE20 |
| SE11-RISK-08 | Seed status: Rev 1.1 "proposed" while v1.0 "remains authoritative" (§0, C6); hardware baseline could change on approval | Low / Medium | Sign-off bound to sha and revision; change control per §151/§104 re-enters this document | SE11, PL |
| SE11-RISK-09 | Every required source and dependency was absent; reconciliation may change dispositions, NFRs or ADRs | **High** / Medium | All entries PROV; SE11-AC-11 gate; SE11-REQ-11 propagates provisional status; unmet dependencies tracked as SE11-DEP-nn | SE11, EL, PL |
| SE11-RISK-10 | Capacity candidates must be chosen before a traceable model exists; H.1/H.3 defaults (M-A, N-A) may be undersized for Stage 1 or the later expansion may fail stability re-validation | Medium / Medium | Table 5.3-R re-balance (Step 1), M-C (Step 2), TRG-MEM-EXPAND, TRG-NAS-CAP; SE11-DEC-03a/06a record basis | SE11, SE01, SE12 |
| SE11-RISK-11 | No supported UPS signalling combination can be evidenced (S-1/S-2) | Medium / High | S-3 automatic fallback (two UPS, native USB each); no reliance before AC-06/14/15 | SE11 |
| SE11-RISK-12 (new) | No evidenced automatic restart mechanism (M1/M3): after an outage in which mains returns before UPS exhaustion the platform stays down until attended | Medium / High | SE11-AC-01 evidence hunt for M1 then M3; M4 recorded as FD-RESTART/FD-MGMT exposure; REV-POWER if an SLO requires unattended restart | SE11, SE20 |
| SE11-RISK-13 (new) | Guest-side `io.max` limiter (QoS-unavailable rows of §6.1a) can be exceeded by a misconfigured Build guest; write-freeze under EXPIRED halts D-IRR mutation and therefore platform operation | Low / Medium; Low / High | Limiter configuration version-controlled and verified in SE11-AC-03; SE11-AC-12b; T3-SUB prepared during DEGRADED so that EXPIRED rarely freezes; SE12 policy (SE11-DEP-04) | SE11, SE12, SE20 |

### 16.5 Assumptions (explicit, labelled; corpus silent)

| Id | Assumption | Resolution path |
|---|---|---|
| ASM-SE11-01 | PL-REQ-ID-REGISTER and fragments G01–G04 are absent; when present, their rows for §152–§177 and Appendices G/H map onto the §0.5 crosswalk | SE11-AC-11 attaches register ids (SE11-DEP-01) |
| ASM-SE11-02 | SEED-01 Rev 1.1 is the operative seed despite its "proposed" status note (C6) | PL confirms; SE11-RISK-08 |
| ASM-SE11-03 | Table 5.3-R allocations and the host root need of 2–4 LP are hypothetical pre-measurement estimates derived from §156/§167 | Replaced by SE11-HARDWARE-CAPACITY-SIZING and measured p95 (§234) |
| ASM-SE11-04 | RAID 6 rebuild at 20 TB under concurrent load: 1–3 days; N-A usable capacity ≈ 36.4 TiB derived from the seed's 80 TB → 72.8 TiB ratio | Measured in SE11-AC-07a |
| ASM-SE11-05 | Device power envelopes in §8.2 are class estimates; the seed's ~560 W typical / 1,150–1,300 W peak remain the circuit-sizing figures | Measured in SE11-AC-06 |
| ASM-SE11-06 | SE11-NFR-01 … 08 values are engineering proposals; product NFRs (PM09) and EL NFR ids are absent | Bound or corrected in SE11-AC-11 (SE11-DEP-10) |
| ASM-SE11-07 | FD-HOST recovery to degraded service ≤ 1 working day assumes a replacement host of the §11.4 class or hosted capacity is obtainable | SE20 spare/hosted readiness; SE19 resilience test |
| ASM-SE11-08 | Dataset classification D-IRR/D-BND/D-REB, sub-classes and examples (§6.2) are a provisional default pending SE12 | SE12 document replaces (SE11-DEP-04) |
| ASM-SE11-09 (new) | §6.1a calibration percentages (V_min ≥ 20 % D2, B_max = 60 % D2, 20 % unallocated) are engineering defaults | Replaced by SE19 measurements and Validation's measured demand (SE11-AC-04/12b) |
| ASM-SE11-10 (new) | A_max = 24 h and G = 24 h are SE11 defaults for the protection states | SE12 binds them (SE11-DEP-04) |
| ASM-SE11-11 (new) | Host root partition reserve 12 GB (M-A/M-C) / 16 GB (M-B/M-A+) and WSL2 cap 8 GB | Measured in SE11-AC-03/04 and fed back into Table 5.3-R by the sizing document |

### 16.6 Conflicts

No upstream product, EL, NT16 or SP16 document was available to check (§0.1); no consistency with them is asserted, and SE11-AC-11 records any conflict with them when they exist. Against the only available authoritative input, SEED-01, the consistency check of §0.5 found **six actual deviations/conflicts**, each stated with both sides and SE11's disposition for reviewers to resolve: **C1** switch power domain (§165 says rack UPS; this document says PD-A); **C2** M2_2/M2_4 role labels (§227.6; SE11-DEC-09); **C3** single PC+NAS UPS with integrated shutdown (§165/§229.1; candidate S-3 adds a NAS UPS); **C4** switch adopted before the rack (§166/§230 conditionality; SE11-ADR-07); **C5** reference quantities versus candidates (not a conflict by §162/§164/§238, recorded for transparency); **C6** Rev 1.1 "proposed" status (§0; ASM-SE11-02). Where this document would otherwise have to choose between a seed statement and an engineering requirement, it has recorded the deviation rather than silently following either side.

## 17. Baseline sign-off record (QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

| Field | Value |
|---|---|
| Baseline id | SE11-HW-BASELINE-3-PROV |
| Bound to | SEED-01 Proposed Revision 1.1, Appendix G BOM v2.2, sections §74, §152–§177, §226–§238; file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| What the baseline is | A **specification-class baseline**: the §11.4 classes with the §1.2 dispositions, the candidate ids and decision rules (Table 5.3-R, §6.7), the volume mapping (§6.1) with its protection matrix (§6.1a), the protection states (§6.3), the signalling/restart candidates (§8.3), the failure domains (§9) and the validation plan (§14). It is **not** a part-number bill |
| Configuration fingerprint | **None** — no part number is confirmed (SE11-DEC-14); SE11-AC-01 not performed |
| Dispositions | Per §1.2 tally: ADOPT ×2; ADOPT WITH ENGINEERING CONSTRAINT ×13; DEFER / OPTIONAL ×5; SUBSTITUTE ×0; ESCALATE ×0 (conditional REV-*); part numbers 17 deferred / 0 confirmed; capacity candidates B4 (M-A default), B14 (N-A default); signalling S-1/S-2/S-3; restart M1/M3/M4 |
| Status ladder | **PROVISIONAL** (this version) → RECONCILED (SE11-AC-11 passed: register ids attached, EL review recorded, C1–C6 resolved) → EVIDENCED (SE11-AC-01 passed: fingerprint v0 recorded, part numbers confirmed) → VERIFIED (SE11-AC-02 … 15 evidence attached; SE11-AC-10 signed). Each step is a new version of this document and an update of the contract record (§18.2) |
| Verification state | **DISPOSITIONED — PROVISIONAL — NOT APPROVED FOR DOWNSTREAM IMPLEMENTATION.** Downstream documents may cite the class dispositions, pool ids, candidate ids, failure-domain ids, protection states, signals, NFR proposals and decision rules as *provisional* (SE11-REQ-11); nothing may be built, ordered or treated as verified on this version |
| Provided contract | `SE11-CONTRACT-hardware-baseline@1` — **DEFINED-UNREGISTERED** (§18.2; SE11-DEP-02, SE11-DEP-11) |
| Sign-off | SE11 (author): architecture dispositions complete at PROVISIONAL status, pending SE11-AC-11 and SE11-AC-01. EL review: **not performed** (documents absent). SE01/SE12/SE17/SE19/SE20 inputs: unmet dependencies (§18.3), none received |

## 18. Cross-domain dependencies and interface contracts

### 18.1 Dependencies by owning role

| Owning role (§74) | What is needed from / supplied to them | Dependency id | Needed by |
|---|---|---|---|
| PL | Register ids for the §0.5 crosswalk | SE11-DEP-01 | SE11-AC-11 |
| EL | Reference this document (not duplicate) in system/runtime/deployment/reliability/estimate documents; bind services to pools (§4); consume SE11-DEC-11 signals in the scheduler; review ADR-01 … 10; register the provided contract; accept FD-HOST/FD-EXT-AI/FD-RESTART residuals; include SE11-REQ-13/17 in Definition of Ready for data-bearing services | SE11-DEP-02 | SE11-AC-11 |
| SE01 | Capacity model: per-pool floors/ceilings for Table 5.3-R, queue-wait thresholds for TRG-WKR-LOCAL, shedding thresholds for the SE11-DEC-11 signals, replacement of ASM-SE11-03 | SE11-DEP-03 | SE11-DEC-03a; Stage 1 end |
| SE12 | Dataset classification (replaces ASM-SE11-08), retention volume V for §6.7, binding RPO/RTO, A_max/G (replaces ASM-SE11-10), backup schedule, T3 and T3-SUB policy, write-freeze enforcement, abrupt-loss integrity verification, key custody with SE17 | SE11-DEP-04 | SE11-DEC-06a; SE11-AC-07a/b/c; SE11-AC-13 |
| SE17 / SE15 | Control ids for SE11-SECREQ-01 … 08; segmentation policy between `seg.*`; key custody; T3-SUB custody; SE11-AC-08 evidence | SE11-DEP-05 | Stage 1 (host/NAS), Stage 3 (full) |
| SE19 | Execute SE11-AC-04/05/12/12b/13 and the §9 resilience tests; replace ASM-SE11-09 with measurements | SE11-DEP-06 | Stage 1–2 |
| SE20 | Telemetry integration (SE11-AC-09), maintenance windows, firmware execution, drills SE11-AC-06/07c/13/14/15, inventory upkeep, admission checklist for SE11-REQ-13/17, T3-SUB operation | SE11-DEP-07 | Stage 1 |
| SP16 | Economics input for gate G-LOCAL (ADR-01) and Step 2 of §5.3 | SE11-DEP-08 | Before any local provisioning decision |
| NT16 | External-provider and hosted-equivalent risk/SLA input for FD-EXT-AI, FD-INTERNET, N-C/M-C, T3 provider | SE11-DEP-09 | Before T3 provider and hosted-equivalent decisions |
| EL (NFR specification) | NFR ids to bind SE11-NFR-01 … 08 | SE11-DEP-10 | SE11-AC-11 |
| SE11 (own, separate tasks) | SE11-INTERFACE-CONTRACT (registers the provided contract), SE11-HARDWARE-CAPACITY-SIZING (applies Table 5.3-R/§6.7; records SE11-DEC-03a/06a) and SE11-POWER-COOLING-RACK (thermal, rack layout, PD details) | SE11-DEP-11 | Stage 1 |
| SE14 | Portable naming/addressing conventions for pools and segments (no physical design) | consultation (no contract needed) | Stage 1 |
| Qualified electrician | Circuits verification and any installation (SE11-REQ-10) | SE11-DEP-12 | Before stable-runtime baseline |

### 18.2 Provided contract — definition of record (status DEFINED-UNREGISTERED)

`SE11-CONTRACT-hardware-baseline@1` · owner SE11 · **status: DEFINED-UNREGISTERED.** The contract is defined by this section. Registration requires two artefacts that do not exist in this run: SE11's Interface Contract document (SE11-DEP-11) and EL's contract register (EL-INTERFAC-CONTRACT-GOVERNAN, SE11-DEP-02). Until both are done the contract is cited as "defined in SE11-PHYSICAL-INFRASTR-HARDWARE v3 §18.2, unregistered", and every consumer carries that status. Content per asset: the §10.1 inventory fields; class disposition, part-number evidence status, quantity status and candidate selected (§1.2, §5.3, §6.7); failure-domain ids (§9); pool ids and CPU budgets (§4) with the Table 5.3-R memory lines; volume mapping (§6.1) and the §6.1a row in force with V_min/B_max; per-class protection states and timestamps (§6.3); signalling topology S-x and restart mechanism M-x/N-x (§8.3) with B_u and R_u; the SE11-DEC-11 signal catalogue; baseline status (§17 ladder); evidence ids (§14); configuration fingerprint (§11.3). Compatibility rule: additive fields only within major version 1; any change to a disposition, mapping, budget rule, state definition or status ladder is a new major version. Consumers (EL runtime/deployment/reliability/estimate documents, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite this contract and the status they rely on; they never restate hardware facts.

### 18.3 Consumed interfaces — unmet dependencies (corrects finding 003)

No owner has published a contract id in this run (§0.1). The v2 wording "REQUESTED" with expected id patterns is withdrawn: an interface without an owner-issued contract id is an **unmet dependency**, not partial contract coverage. Each is tracked by the SE11-DEP-nn id, with the SE11 ids that depend on it and the behaviour of this document while it is unmet. No owner contract id is invented.

| Dependency | Owner | Dependent SE11 ids | Behaviour while unmet |
|---|---|---|---|
| SE11-DEP-01 register ids | PL | §0.5 crosswalk, all REQ/DEC/ADR | Seed sections cited directly; status PROV; no id attached |
| SE11-DEP-02 EL architecture review, contract registration, DoR clause, scheduler consumption of signals | EL | SE11-ADR-01 … 10, §18.2, SE11-REQ-13/17, SE11-DEC-11 | Contract DEFINED-UNREGISTERED; ADRs PROV; shedding policy unspecified (signals still published) |
| SE11-DEP-03 capacity inputs | SE01 | SE11-DEC-03a, Table 5.3-R, TRG-WKR-LOCAL, SE11-DEC-11 thresholds | Default M-A under H.1/H.3; hypothetical allocations (ASM-SE11-03) |
| SE11-DEP-04 data policy | SE12 | SE11-DEC-06a, SE11-REQ-13/17, SE11-NFR-05, §6.2–§6.3 defaults | Default N-A; provisional classes (ASM-SE11-08); A_max/G defaults (ASM-SE11-10); write-freeze enforcement unassigned |
| SE11-DEP-05 security control ids and policies | SE17 / SE15 | §13 SE11-SECREQ-01 … 08, `seg.*` policy, SE11-AC-08 | SE11-SECREQ-nn stand as requirements without control-id mapping |
| SE11-DEP-06 test execution and evidence format | SE19 | SE11-AC-04/05/12/12b/13, ASM-SE11-09 | Tests specified; not executed; defaults stand |
| SE11-DEP-07 operations integration | SE20 | SE11-AC-06/07c/09/13/14/15, §10.5, SE11-REQ-13/17 checklists | Drills specified; not scheduled or executed |
| SE11-DEP-08 economics | SP16 | G-LOCAL, §5.3 Step 2, N-C/M-C | Local-versus-hosted undecided per pool |
| SE11-DEP-09 external-dependency assessment | NT16 | FD-EXT-AI, FD-INTERNET, T3 provider, N-C/M-C | Residuals stated from the seed only |
| SE11-DEP-10 NFR ids | EL | SE11-NFR-01 … 08 | Values are proposals (ASM-SE11-06) |
| SE11-DEP-11 SE11's own sibling artefacts | SE11 | §18.2 registration, SE11-DEC-03a/06a, thermal/rack detail | Contract unregistered; candidates at default |
| SE11-DEP-12 electrical verification | Qualified electrician | SE11-REQ-10, SE11-AC-06 | No stable-runtime baseline until on file |

## 19. Criteria disposition

| Criterion | Disposition | Where / reason |
|---|---|---|
| OUT-…-AR-01 source baseline | Covered | §1.1 (Rev 1.1, BOM v2.2, sha), §1.2 (B1–B19 with class/quantity/part-number-status separation), §0.5 crosswalk |
| OUT-…-AR-02 scope and boundaries | Covered | §2 |
| OUT-…-AR-03 workload allocation | Covered | §4 (pools, CPU budgets, shared-budget membership, weighted contention vs shedding) |
| OUT-…-AR-04 compute | Covered | §5 (normalised accounting, Table 5.3-R, aggregate-only decision rule with Steps 1–3, GPU preconditions) |
| OUT-…-AR-05 storage | Covered | §6 (authoritative mapping, protection matrix §6.1a, classes, protection states §6.3, recovery split, NAS candidates) |
| OUT-…-AR-06 network | Covered | §7 (incl. NIC slot fallbacks) |
| OUT-…-AR-07 power/placement | Covered | §8 (gated signalling, per-candidate timed sequences and budgets, restart mechanisms, fail-closed) |
| OUT-…-AR-08 failure domains | Covered | §9 (incl. FD-RESTART, FD-UPS-N; copy-age-based FD-INTERNET) |
| OUT-…-AR-09 manageability | Covered | §10 |
| OUT-…-AR-10 compatibility/availability assessment | Covered | §11 — assessment performed; result "not established" for support/availability; consequence applied: part numbers deferred, classes baselined |
| OUT-…-AR-11 security | Covered | §13 (SE11-SECREQ-nn; mapping is SE11-DEP-05) |
| OUT-…-AR-12 expansion | Covered | §12 |
| OUT-…-AR-13 risks/ADRs | Covered | §16 |
| OUT-…-AR-14 validation plan | Covered | §14 |
| QC-…-AR-01 exact source version; every item dispositioned | Covered | §1.1, §1.2 (status PROVISIONAL; dispositions at class level, part numbers deferred) |
| QC-…-AR-02 one coherent physical architecture | Covered | §2.3, §4–§10 cross-referenced by pool, device, §6.1a row, segment, power-domain, candidate, failure-domain, protection-state and signal ids |
| QC-…-AR-03 compatibility and availability checked sufficiently to avoid baselining impossible or obsolete combinations | Covered **by design change; evidence-level outcome UNMET** — the check was performed to the limit of the corpus (§11.1–§11.2), found no support/availability evidence, and the baseline was reduced to specification classes with every part number deferred (SE11-DEC-14) so that no impossible or obsolete combination is baselined; closure at part-number level requires SE11-AC-01; no implementation-ready sign-off is claimed (§17) | §11.2, §11.3, §17 |
| QC-…-AR-04 no hidden SPOF, capacity limit or dependency | Covered | §9 (incl. FD-RESTART, FD-SIGNAL, FD-MGMT), §12.1 hard ceilings, §12.3, §16.4, §18.3 unmet dependencies |
| QC-…-AR-05 substitution rules preserve assumptions | Covered | §11.4 classes; SE11-REQ-12; §6.1a admissibility rules; §12.3 ESCALATE boundaries; §8.4 ordered remedies |
| QC-…-AR-06 validation evidence and affected owners explicit | Covered | §14 (owner, dependency id and gate per AC), §18 (owners, unmet dependency ids) |
| QC-…-AR-07 sign-off against the exact baseline consumed downstream | Covered | §17 (provisional sign-off bound to seed sha and the specification-class baseline; status ladder; no fingerprint claimed) |
| BND-01 … BND-04 | Covered (excluded as required) | §15 |

Required source PL-REQ-ID-REGISTER: substantive disposition **UNMET SOURCE** (SE11-DEP-01, §0.1); reported `covered` in the event only in the corpus-silence sense fixed in §0.3 (sought, absent, ASM-SE11-01, crosswalk §0.5, no id invented) — not consumed, not reconciled; closure by SE11-AC-11.
