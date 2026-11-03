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
