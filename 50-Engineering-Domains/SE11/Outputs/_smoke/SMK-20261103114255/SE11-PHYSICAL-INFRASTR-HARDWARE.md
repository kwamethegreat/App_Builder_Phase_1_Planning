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
