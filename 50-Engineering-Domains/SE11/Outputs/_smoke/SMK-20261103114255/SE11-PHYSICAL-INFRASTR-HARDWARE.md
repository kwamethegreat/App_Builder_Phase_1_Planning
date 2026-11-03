---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 2
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-REQ-13, SE11-REQ-14, SE11-NFR-01, SE11-NFR-02, SE11-NFR-03, SE11-NFR-04, SE11-NFR-05, SE11-NFR-06, SE11-NFR-07, SE11-NFR-08, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-DEC-09, SE11-DEC-10, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-ADR-08, SE11-ADR-09, SE11-SECREQ-01, SE11-SECREQ-02, SE11-SECREQ-03, SE11-SECREQ-04, SE11-SECREQ-05, SE11-SECREQ-06, SE11-SECREQ-07, SE11-SECREQ-08, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-RISK-09, SE11-RISK-10, SE11-RISK-11, SE11-AC-01, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-08, SE11-AC-09, SE11-AC-10, SE11-AC-11, SE11-AC-12, SE11-AC-13, SE11-AC-14, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05, ASM-SE11-06, ASM-SE11-07, ASM-SE11-08]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v2 (revision of v1 after review findings REVIEWER-EN-SE11-PHYSICAL-001 … 009) · **Owner:** SE11 (Infrastructure, Containers & Runtime Engineering, SEED-01 §74) · **Run:** SMK-20261103114255 · **Baseline state:** PROVISIONAL (see §0 and §17)

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and reference BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite by this document id and the disposition they rely on. It selects no vendor, prices nothing and purchases nothing (§15).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`), consumed sections: hardware strategy §152–§177 (document sections 37–45, including the section-40 reference-configuration table inside §160), the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note at the end of §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231), the guardrails Appendix H (§232–§238) and the domain list §74. No BOM content is recreated from memory; every specification cited below is taken from those sections.

## 0. Document status, source availability and limitation

### 0.1 Inputs: what was available and what was not

| Input (context id) | Availability at authoring (v2) | What SE11 needed from it | Effect of absence on this document |
|---|---|---|---|
| PL-REQ-ID-REGISTER (required source) | **Unavailable** — `read_document` returned `not_found`; context block marked "missing" | Requirement / decision / constraint ids with full specification and seed section, to cite instead of raw seed sections | **Unavailable-source limitation, not inapplicability.** No register ids are cited anywhere; every statement cites the SEED-01 section directly. Reconciliation to register ids is a mandatory gate before any baseline status above PROVISIONAL (SE11-AC-11). No register id is invented. |
| PL-REQ-REGISTER-G01 … G04 (register fragments) | **Unavailable** — `not_found` (index lists 60 chars, 0 sections) | Verbatim BOM appendix | BOM read directly from SEED-01 §227–§231, which the hardware chain rule permits for SE11. |
| PM09-* (14 product documents) | **Unavailable** (all marked missing) | MVP scope, product NFRs, acceptance criteria, risks/constraints, product decision log, KPIs | Product-level targets are not reconciled. Every NFR value in §3 is an SE11 engineering proposal (ASM-SE11-06), not a product requirement. |
| NT16-* (8 vendor/dependency documents) | **Unavailable** | External-dependency and SLA requirements, exit/replacement assessment | External-provider residual risks (FD-EXT-AI, FD-INTERNET, hosted equivalents) are stated from the seed only; no vendor assessment is relied on and none is made here. |
| EL-* (26 engineering-lead documents) | **Unavailable** | System/runtime/deployment/reliability architecture, NFR specification, ADRs, interface-contract governance, estimates, sequencing, DoR/DoD | No EL decision id is cited. No EL architecture review has occurred. SE11 ADRs are provisional and may be superseded by EL. The provided contract (§18.2) is *defined* here and *proposed* for EL registration — it is not registered. |
| SP16-* (7 FinOps documents) | **Unavailable** | Cost allocation, spend guardrails, unit economics | The economic half of the seed's justification rule for local capacity (§238) cannot be evaluated; the local-versus-hosted choice therefore stays open per pool (SE11-ADR-01, gate G-LOCAL). |
| SEED-01 (seed, read on demand) | Available | Hardware strategy and BOM | Sole substantive input of this version. |

### 0.2 Decision status model

Every decision, requirement and NFR in this version carries the status **PROV** (provisional, seed-derived, not reconciled). The status **REC** (reconciled: register ids attached, EL review recorded, upstream product/NFR documents checked) can only be assigned by a later version after SE11-AC-11 passes. **No entry in v2 is REC.** Downstream documents that cite this version must cite it as `SE11-PHYSICAL-INFRASTR-HARDWARE v2 (PROVISIONAL)` and carry the same provisional status for anything derived from it (SE11-REQ-11).

### 0.3 Source disposition in the completion event

The completion-event schema admits only `covered` or `not_applicable` per required source. `covered` would falsely assert the register was consumed; this document therefore reports `not_applicable` in the mechanical sense "could not be applied because the file does not exist", and records here — as the substantive disposition — **UNAVAILABLE SOURCE / LIMITATION**: the register is required, it applies, it was not available, and the consequences are those in §0.1, §0.2, §16.6 and §17.

### 0.4 Disposition of the v1 review findings

| Finding | Correction made in v2 | Where |
|---|---|---|
| 001 source gap / unsupported consistency claim | Register and dependencies recorded as unavailable-source limitations; affected decisions identified; all decisions PROV; "no conflicts" assertion withdrawn; sign-off reduced to PROVISIONAL with reconciliation gate; no ids invented | §0, §16.6, §17, SE11-AC-11 |
| 002 memory/NAS quantities adopted without evidence; ADR-01 | 256 GB and 6×20 TB downgraded to **capacity candidates**; hypothetical reservation envelopes separated from evidence and labelled; smaller and hosted alternatives compared; decision rules defined; ADR-01 rewritten to preserve the seed's conditional local-provisioning rule (§238) | §1.2 (B4, B14), §5.3, §6.7, §16.1 ADR-01/ADR-08, SE11-DEC-03/06 |
| 003 contracts, ownership, control ids, NFR mapping | Provided contract marked PROPOSED (defined here, not registered); consumed interfaces listed as REQUESTED with owner and the id to be assigned; physical-network responsibility retained by SE11 per §74; foreign control ids replaced by SE11-SECREQ-nn proposals; quality attributes mapped to measurable SE11-NFR-nn | §3, §7.3, §13, §18 |
| 004 CPU/memory accounting and reservation mechanism | Physical cores / logical processors / guest vCPUs normalised; Hyper-V reservation controls specified; every pool has a budget or explicit shared-budget membership; contention test added | §4, §5.2, SE11-REQ-14, SE11-AC-12 |
| 005 storage mapping contradiction | One authoritative device mapping; Highest-priority VMs isolated on M2_4; deviation from the seed's literal role labels recorded as SE11-DEC-09 with Storage-QoS protection; blast radii recalculated; lane-sharing fallback analysed | §6.1, §9, SE11-ADR-09 |
| 006 UPS signalling | Signalling topology made an explicitly gated decision (no compatibility asserted); bounded state machine for every event; parametric shutdown budget with 30 % reserve against measured runtime; fail-closed commissioning outcome; signalling-path-loss and abrupt-loss drills | §8.3–§8.4, SE11-DEC-10, SE11-AC-06/13/14 |
| 007 failure domains | FD-CIRCUIT-A (healthy UPS) separated from FD-UPS-A (abrupt output loss); crash-consistency and recovery requirements stated; every domain has an accountable owner, recovery dependency, measurable target and residual disposition | §9, SE11-NFR-07 |
| 008 compatibility/availability | Recorded as **not established**; criterion QC-AR-03 reported as unmet; items retained as conditional candidates; pre-build support checks separated from commissioning tests; sign-off bound to the exact evidenced configuration fingerprint | §11, §14, §17, §19 |
| 009 T3 protection gap | Protection-activation rule: no irreplaceable dataset may exist before a verified isolated copy exists; dataset classes and provisional owner; copy interval, restore verification and residuals reconciled; T2-only recovery distinguished from T3-dependent recovery | §6.2–§6.3, §6.6, §9, SE11-REQ-13, SE11-AC-07 |

## 1. Authoritative source baseline (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01)

### 1.1 Exact version and sections consumed

| Item | Value |
|---|---|
| Seed | SEED-01, "Master Product Vision & Operating Architecture — Proposed Revision 1.1", "Expanded 2026 Baseline — Greenfield, Opportunity Intelligence, 19-Gap & Infrastructure Edition" (§0); file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| BOM version | Appendix G "Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (status note in §226; items §227.1–§227.11, §228.1–§228.3, §229.1–§229.2, §230, §231) |
| Strategy sections | §152–§154 (37.x stage boundaries, shared hardware, evidence progression), §156–§157 (38.x required logical environments, resource-reservation principle and the section-39 greenfield provisioning principle), §158–§160 (39.x no-wait/no-overbuild, evidence-driven thresholds, portability, section-40 reference configuration table), §161–§163 (40.x central node, memory, NVMe), §164–§166 (41.x NAS, UPS/electrical, rack/network and the section-42 operating model), §167–§168 (42.x layout, VMs + containers), §169–§171 (43.x workers), §172–§175 (44.x redundancy, quorum, resource classes, degradation), §176–§177 (45.x GPU) |
| Guardrails | Appendix H §232–§238 (H.1–H.7) |
| Domain boundaries | §74 (SE11 = Infrastructure, Containers & Runtime Engineering; SE12 = Database, Storage & Data; SE14 = API, Integration & Portability; SE17 = Infrastructure, Workload & Data Security; SE19 = Performance, Resilience & Specialized Validation; SE20 = SRE, Observability & Production Operations; SE01 = Core Platform & Distributed Systems) |
| Approval status of the seed | §0: "The approved v1.0 document remains authoritative until this revision is explicitly approved." The hardware baseline exists only in Rev 1.1. This document treats Rev 1.1 as the operator-supplied seed (ASM-SE11-02) and binds its provisional sign-off to that exact revision and sha (§17). |

### 1.2 Classification and engineering disposition of every BOM entry

The seed states that Appendix G "is a greenfield reference configuration, not an assertion of already-owned equipment or a mandatory topology" and that Product/Engineering "may procure, substitute, resize, or use hosted equivalents when evidence shows equal or better capability, reliability, portability, security, schedule, and economics" (§226 status note); that "local central compute, NAS, power, and worker infrastructure should be provisioned when workload evidence and economics justify it; managed/hosted equivalents remain acceptable where they better satisfy the target requirements" (§238); and that the central node "is a reference configuration rather than an inherited constraint" (§160, section 40 lead-in).

**Reading rule for the table.** A disposition below is the disposition *of the reference configuration if local provisioning of that element is justified* under gate G-LOCAL (SE11-ADR-01). It is not a decision that local provisioning is justified; that decision needs the workload and economic evidence named in §238, which is unavailable in this version (§0.1). "Quantity/count status" separates the adopted *specification class* from any *capacity figure*, which is never adopted from the maximum listed configuration (ENV-DEC-017: size from workload evidence).

| # | BOM entry (seed section) | Seed class | Engineering disposition (SE11 only) | Quantity / count status | Decision ref |
|---|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, Zen 5 homogeneous, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — virtualization extensions and IOMMU enabled; 230 W package limit is the compute line of the power budget (§8.2) | n/a (one CPU) | SE11-DEC-01 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — 157 mm < ~166 mm chassis clearance (§227.8); structural check only (§11.1) | n/a | — |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi: 4×DDR5 to 256 GB; PCI_E1 Gen5 x16 (CPU); PCI_E2 Gen3 x1; PCI_E3 Gen4 x4 (shares with M2_3); M2_1 Gen5 x4 CPU; M2_2 Gen5 x4 CPU sharing with USB4; M2_3 Gen4 x2 chipset; M2_4 Gen4 x4 chipset; 4×SATA; 5 GbE; Wi-Fi 7; BT 5.4; 2×USB4; Flash BIOS; Clear CMOS (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map verified before baseline (SE11-AC-02); Wi-Fi/Bluetooth disabled in server role; no out-of-band controller, so the management path is §10.2; BIOS/CPU support currency not established (§11.2) | n/a | SE11-DEC-02 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC, single matched kit; "step down to 5600/5200 if 4-DIMM training is unstable" (§227.4; §162 "evidence-driven sizing decision, not a fixed prerequisite") | Preferred target (class); evidence-driven (quantity) | ADOPT WITH ENGINEERING CONSTRAINT for the **specification class** (DDR5 UDIMM matched kit on the AM5 4-slot platform, EXPO with the seed's 5600/5200 fallback, non-ECC accepted and monitored, SE11-RISK-02) | **CANDIDATE.** 256 GB (4×64) is the reference *ceiling* configuration, not adopted capacity. The initial quantity is chosen by SE11-HARDWARE-CAPACITY-SIZING under the rule in §5.3 from a traceable workload/concurrency model; candidates M-A/M-B/M-C in §5.3 | SE11-DEC-03, SE11-ADR-03 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch at x2 is acceptable subject to SE11-AC-02; fallback in SE11-DEC-02 | 2 devices (roles fixed by §6.1) | SE11-DEC-02 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; seed roles "platform data / DBs / containers (M2_4)", "VM & artifact store (M2_2)" (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID (SE11-ADR-05); **role mapping deviates from the seed's literal labels**: Highest-priority VM disks move to M2_4 so that no Highest-priority pool shares a device with a Medium-priority pool (SE11-DEC-09, §6.1) | 2 devices | SE11-ADR-05, SE11-DEC-09 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build; with the 145 W optional GPU only after the measured power-budget check the seed itself requires (§227.11; §160 table "acceptable only after validating the final system power budget and headroom"); any accelerator above 145 W, dual-slot, or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3) | n/a | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance, 3×140 mm fans (§227.8) | Preferred target | ADOPT — clearance and form factor structurally compatible with B2/B3 (§11.1); GPU length 241 mm is checked in SE11-AC-02 before any GPU adoption | n/a | — |
| B9 | OS — Windows 11 Pro retail (§227.9; operating model §166) | Fixed by the operating model (§166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role; persistent services only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13.4) | n/a | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); Hyper-V virtual-switch driver support is **not established** (§11.2) and is a pre-build check (SE11-AC-01); specification-class alternative in §11.4 | 1 device | SE11-DEC-02 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell, 24 GB ECC, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition" §175; "driven by measured demand and economics" §177) | DEFER / OPTIONAL — adoption preconditions §5.5 and trigger TRG-GPU §12.2 | 0 at baseline | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T: 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock (64 GB max), 2×10GbE + 2×5GbE, 2×USB4, 4×M.2, ADM/Btrfs snapshots, per-folder AES-256, "UPS support / network UPS server" (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only (never a live datastore); admin interface on `seg.mgmt`; firmware lifecycle §10.4; UPS-signalling role gated by SE11-DEC-10 | 1 enclosure; subject to G-LOCAL (hosted object storage is the recorded equivalent for T2/T3, §6.7) | SE11-ADR-05, SE11-DEC-10 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install on TRG-NAS-MEM (§12.2) | 0 at baseline | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target (class); count tied to retention policy (§164 "according to retention policy") | ADOPT WITH ENGINEERING CONSTRAINT for the **drive class** (3.5-inch enterprise CMR, RAID 6 mandatory at ≥ 20 TB per drive, SE11-RISK-06) | **CANDIDATE.** Six drives is the reference *ceiling* array, not adopted capacity. The initial count is chosen under the rule in §6.7 from SE12's retention-volume model (unavailable); candidates N-A (4 drives), N-B (6 drives), N-C (hosted T2/T3) | SE11-DEC-06 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, line-interactive AVR, 6 battery outlets, USB HID, "automatic graceful shutdown via PowerPanel / NAS UPS service", RB1290X2 batteries (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement; shutdown budget rule SE11-REQ-06 with fail-closed outcome (§8.4); signalling integration gated (SE11-DEC-10) | 1 unit | SE11-DEC-07, SE11-DEC-10 |
| B16 | UPS (rack) — second unit ~1000 VA / 600 W pure sine, model TBD; "when a local worker rack is used" (§229.2; §165) | Candidate ("when used") | DEFER / OPTIONAL — only with a local worker rack; specification class §11.4 | 0 at baseline | SE11-DEC-08 |
| B17 | Rack — 18U; 1U 24-port switch "at least 2×10GbE"; 1U PDU; worker trays sized to measured need; 1U power-brick shelf; "no fixed initial worker count" (§230; §166) | Candidate ("If local rack infrastructure is selected", §166) | Switch: ADOPT WITH ENGINEERING CONSTRAINT by specification class (managed, VLAN-capable, ≥ 2×10GbE minimum per seed, ≥ 4×10GbE preferred, §7.2). Rack, PDU, trays, shelf: DEFER / OPTIONAL until TRG-WKR-LOCAL (§12.2) | Switch 1; rack items 0 at baseline | SE11-DEC-08, SE11-ADR-07 |
| B18 | Electrical — two separate 15 A breakers (PC+NAS UPS on one, rack UPS on the other); UPS plugged directly into wall; dedicated 20 A optional; typical ~560 W, sustained peak ~1,150–1,300 W (§231; §165) | Fixed constraint (code-regulated) | ADOPT WITH ENGINEERING CONSTRAINT — stated as a requirement for qualified professionals (SE11-REQ-10); nothing electrical is designed here | n/a | SE11-REQ-10 |
| B19 | Local worker nodes (form factor and count unspecified; pool "may be local, hosted, cloud or hybrid", §168–§171) | Optional / evidence-sized | DEFER / OPTIONAL — hosted/cloud executors first (§160 "avoid premature local-compute constraints"); local class adopted on TRG-WKR-LOCAL | 0 at baseline | SE11-ADR-01 |

**Tally (authoritative; supersedes any other count):** ADOPT ×2 (B2, B8); ADOPT WITH ENGINEERING CONSTRAINT ×13 (B1, B3, B4-class, B5, B6, B7, B9, B10, B12, B14-class, B15, B17-switch, B18); DEFER / OPTIONAL ×5 (B11, B13, B16, B17 rack/PDU/trays/shelf, B19); SUBSTITUTE ×0; ESCALATE ARCHITECTURE IMPACT ×0 at baseline (conditional REV-* triggers in §12.3). Two capacity figures (B4 quantity, B14 count) are CANDIDATES pending the sizing rules of §5.3 and §6.7. No substitution is silent: any future substitution is a new SE11-DEC entry with technical reason and impact (SE11-REQ-12).

## 2. Physical architecture scope and boundaries (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-02)

### 2.1 In scope (owned by SE11)

| Element | Content of this document |
|---|---|
| Local central compute | One central node (B1–B10) as the reference configuration; host role, slot/lane allocation, reservation mechanism (§5) |
| Worker nodes | Capability classes and placement rules for local workers if and when adopted (§4, §12); physical provisioning (trays, power, ports) when triggered |
| GPU / accelerator class | Single-slot, ≤ 145 W, PCIe x16 class; deferred (§5.5) |
| Storage / NAS | Hot NVMe tiers on the host, the durable NAS tier, and the physical mapping of every volume (§6) |
| Network switching / NICs / physical segments | 10 GbE storage/core path, 5 GbE host onboard, switch class, VLAN membership and addressing of the physical segments (§7). Physical-network engineering is SE11's: §74 places SE14 in "API, Integration & Portability Engineering", not physical networking |
| Rack / placement | 18U rack class; desk/room placement constraints (§8.5) |
| UPS / power distribution | Two power domains, UPS roles, shutdown signalling and state machine (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10.1) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10.2) |

### 2.2 Out of scope (owned elsewhere; referenced, never included)

| Concern | Owner (SEED-01 §74 unless stated) | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (chain rule) | §15 |
| Electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only |
| System, runtime, deployment and reliability architecture | EL | EL cross-references this document; EL's documents are unavailable in this version (§0.1) |
| Capacity model and growth thresholds | SE01 (capacity concern) and SE11-HARDWARE-CAPACITY-SIZING (sizing) | §5.3 and §6.7 give candidate configurations and decision rules; the sizing document applies them |
| Data policy: dataset classification, retention, backup schedule, binding RPO/RTO, key custody | SE12 (data), SE17 (security) | §6 states hardware-capable targets and a provisional default classification until SE12's document exists |
| Portability and integration constraints on how pools are addressed (DNS names, no provider-specific assumptions) | SE14 | Consulted on §4/§7 naming; owns no physical design |
| Security control catalogue and ids | SE17 (infrastructure/workload/data), SE15 (identity/crypto) | §13 lists SE11's requirements as SE11-SECREQ-nn to be mapped to owner control ids when those documents exist |
| Performance/resilience test execution | SE19 | §14 lists the tests; SE19 executes and reports |
| Operations, monitoring, maintenance windows | SE20 | §10 states telemetry and window requirements |
| Software/container/service design | existing SE11 runtime artefacts and EL | BND-03: not restated |

### 2.3 Context view (text)

```mermaid
flowchart LR
  subgraph PD_A[Power domain A: UPS-A CP1500PFCLCD on circuit A]
    HOST[Central host: Win11 Pro + Hyper-V\nVMs: Core + Data on M2_4 / Build-CI + Validation on M2_2\nM2_1 host system, M2_3 scratch]
    NAS[NAS AS6808T: RAID 6 (count = candidate)\nsnapshots, backups, evidence, archives = T2]
    SW[Managed switch: >=2x10GbE (>=4 preferred) + 1/2.5GbE access]
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
  HOST -- network shutdown command (gated) --> NAS
```

## 3. Stakeholders, concerns and quality attributes (ISO/IEC/IEEE 42010 framing)

| Stakeholder | Concern | Quality attribute (ISO/IEC 25010) | Measured by |
|---|---|---|---|
| EL | One coherent physical architecture to reference; contract to register | Compatibility, maintainability | §4–§10 cross-references; §18.2 contract definition |
| SE01 | Capacity inputs as ranges with assumptions | Capacity | §5.3, §6.7, §12 |
| SE12 | Durable tier, RAID/replication boundaries, recovery and protection rules | Reliability (recoverability, fault tolerance) | §6.3, §6.6, SE11-NFR-05, SE11-AC-07 |
| SE14 | Pools addressed portably | Portability | SE11-REQ-05 |
| SE17 / SE15 | Trusted boot, management isolation, encryption support | Security (confidentiality, integrity) | §13, SE11-AC-08 |
| SE19 | Burn-in, contention, abrupt-loss and resilience test surface | Reliability (maturity), performance efficiency | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows, shutdown drills | Maintainability (analysability), reliability | §10, SE11-NFR-04 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, ADR-01 gate G-LOCAL, §12 triggers |

**Measurable non-functional targets introduced by this document (status PROV; proposed for binding to EL-ENGINEER-NFR-SPECIFIC ids, which is unavailable; values are engineering proposals, ASM-SE11-06).**

| NFR id | Quality attribute | Target (measurable) | Verified by |
|---|---|---|---|
| SE11-NFR-01 | Performance efficiency / reservation protection | Under the §14 contention profile (Build VM at 100 % of its vCPUs, Validation VM at 100 %, background saturating, backup transfer running): Core VM synthetic API probe p95 latency ≤ 1.5 × its unloaded baseline; Data VM synthetic 4 KiB random-read p99 ≤ 2 × unloaded baseline; Highest-priority VM CPU-wait ≤ 5 % in every 60 s window; throttling order observed = background → build → validation | SE11-AC-12 |
| SE11-NFR-02 | Performance efficiency / storage path | Host↔NAS ≥ 0.7 GB/s sustained for 10 min during concurrent build-cache load; no other path degrades below 80 % of its unloaded throughput | SE11-AC-05 |
| SE11-NFR-03 | Reliability / safe shutdown | Shutdown budget B (§8.3) ≤ 0.7 × measured UPS-A runtime R at measured PD-A load; every state transition completes inside its stated bound | SE11-AC-06, SE11-AC-14 |
| SE11-NFR-04 | Maintainability / observability | 100 % of §10.3 signals exported, sample interval ≤ 60 s, retained for at least one stage | SE11-AC-09 |
| SE11-NFR-05 | Recoverability (hardware-capable; SE12 binds the product RPO/RTO) | T1→T2 snapshot interval ≤ 1 h and full replication ≤ 24 h; single-VM restore from T2 ≤ 4 h; T3 copy interval ≤ 24 h for class D-IRR; restore of any D-IRR dataset from T3 verified at every stage gate | SE11-AC-07 |
| SE11-NFR-06 | Availability (single-host) | No HA claim. Planned hardware maintenance only in declared windows; FD-HOST recovery to degraded service (hosted fallback or replacement host of the §11.4 class) ≤ 1 working day from T2/T3, assumption ASM-SE11-07 | SE11-AC-07, SE19 resilience tests |
| SE11-NFR-07 | Integrity after abrupt loss | After an abrupt power loss (FD-UPS-A drill), every VM filesystem, the host filesystem and the NAS array pass integrity checks with zero unrecoverable errors; database loss ≤ last committed transaction (SE12 verifies) | SE11-AC-13 |
| SE11-NFR-08 | Thermal/power envelope | ≥ 24 h combined stress with CPU package ≤ 230 W, all device temperatures within manufacturer limits, zero memory errors at the chosen DDR5 profile | SE11-AC-04 |

## 4. Workload-to-hardware allocation (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03)

Allocation maps workload classes to **resource pools**, never to named devices; a pool is addressed by a logical name (§160: no hard-coded host names, local paths or addresses). Pools are the unit that moves between local, hosted and customer infrastructure (§168). Every pool has either its own budget or an explicit *shared-budget membership* with a stated share (SE11-REQ-01, corrected per finding 004). Units: **LP** = logical processor of the host (32 LP = 16 physical cores × 2 SMT threads, B1); **vCPU** = virtual processor assigned to a guest (1 vCPU is scheduled onto 1 LP at a time).

| Pool | Workload class (seed §167, §169–§171, §174) | Priority (§174) | Placement in the reference configuration | CPU budget | Memory budget (candidate envelope, §5.3) | Storage device (§6.1) |
|---|---|---|---|---|---|---|
| `pool.core` | Platform core: orchestration, APIs, queues, registry/control | Highest | Linux VM "Core" | 4 vCPU; Hyper-V reserve 100 % (= 4 LP guaranteed); limit 100 %; weight 200 | Static (Dynamic Memory off): M-B envelope 32 GB / M-A envelope 24 GB | M2_4 |
| `pool.data` | Databases, search/knowledge data, caches | Highest | Linux VM "Data" | 4 vCPU; reserve 100 % (4 LP); weight 200 | Static: M-B 64 GB / M-A 32 GB | M2_4 |
| `pool.runtime` | Stable runtime of accepted stage baselines (§156, §235) | Highest | **Shared-budget member of `pool.core` and `pool.data`**: runtime namespaces inside the Core and Data VMs with separate projects, credentials, networks, data paths (§156). Share: within each VM, runtime namespaces hold cgroup `cpu.weight` ≥ 3 × the platform-control namespaces and `memory.min` ≥ 50 % of the VM's static memory (defaults; EL binds the exact values) | inherits | inherits | M2_4 |
| `pool.validate` | Integration, security validation, staging, release challenger, VP validation | High | Linux VM "Validation/Staging" | 8 vCPU; reserve 50 % (4 LP guaranteed); limit 100 %; weight 150 | Dynamic: min 16 / max 48 GB (M-B); min 12 / max 24 GB (M-A) | M2_2 |
| `pool.build` | CI runners, build cache, artifact generation | Medium | Linux VM "Build/CI" | 16 vCPU; reserve 25 % (4 LP guaranteed); limit 100 %; weight 100 | Dynamic: min 16 / max 64 GB (M-B); min 12 / max 32 GB (M-A) | M2_2 (VM disk, artifacts) + M2_3 (scratch) |
| `pool.agents` | API-based model workers | Medium | Hosted/cloud executors first. When local: **member of `pool.build` budget** as containers in the Build VM with cgroup `cpu.max` ≤ 50 % and `memory.max` ≤ 40 % of the VM | member | member | M2_2 |
| `pool.test` | Test/browser/scanning workers, synthetic users | Medium / lowest | As `pool.agents`: **member of `pool.build` budget**, `cpu.max` ≤ 50 %, `memory.max` ≤ 40 %; agents + tests together never exceed the Build VM's own ceiling | member | member | M2_2 |
| `pool.background` | Background analysis, documentation, low-priority optimisation | Lowest | **Member of `pool.build` budget**: cgroup `cpu.weight` 10 (vs 100 for build jobs), `cpu.max` ≤ 25 %, no memory guarantee; first to be shed (§175) | member | member | M2_2 |
| `pool.gpu` | Local inference, embeddings, vision, evaluation (§176) | Medium | DEFERRED — PCI_E1 when adopted (§5.5); external providers meanwhile (§160) | — | — | — |
| `pool.durable` | Backups, snapshots, release evidence, archives, mirrors (§164) | n/a | NAS T2 (+ T3 isolated copy, §6.3) | — | — | NAS |
| `pool.admin` | Host OS, Hyper-V root, WSL2 + Docker Desktop interactive use (§167) | n/a | Windows host root partition | Not reservable in Hyper-V; the root partition takes the floating LPs (§5.2); operational rule: VM reserves sum ≤ 16 LP so ≥ 16 LP float | Host OS reserve 16 GB + WSL2 cap 8 GB (`.wslconfig`) | M2_1 |

**Simultaneous accounting at baseline (corrects v1's mixed units):** vCPUs assigned to VMs = 4 + 4 + 8 + 16 = **32 vCPU on 32 LP** (1 : 1, no vCPU oversubscription at baseline; bursts happen *within* a VM's own vCPU count, not by adding vCPUs). Guaranteed LPs (sum of reserves) = 4 + 4 + 4 + 4 = **16 LP (50 %)**. Floating LPs = **16**, claimed first by the host root partition (typical need 2–4 LP, ASM-SE11-03) and then by VMs in weight order 200 : 200 : 150 : 100, which yields the deterministic throttling order background → build → validation → (never) core/data under saturation. Memory accounting is in §5.3 per candidate.

Rule SE11-REQ-01 (restated): `pool.core`, `pool.data` and `pool.runtime` reservations are hard — static memory, 100 % processor reserve, never oversubscribed; every other pool has a declared guaranteed floor and ceiling or an explicit membership share as above. Rule SE11-REQ-14: the reservation mechanism is the hypervisor's per-VM processor reserve/limit/weight and static-versus-dynamic memory controls plus in-VM cgroup shares for members; no pool relies on "best effort".

## 5. Compute architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-04)

### 5.1 Host-role requirements

| Requirement | Specification | Source |
|---|---|---|
| CPU | 16 physical cores / 32 logical processors, homogeneous cores, 64 MB L3, hardware virtualization + IOMMU enabled in firmware | B1 (§227.1); VM isolation (§168) |
| Memory | DDR5 UDIMM matched kit on four slots (board maximum 256 GB, B3); quantity per §5.3; EXPO only after the stability pass; fallback DDR5-5600/5200 as the seed directs | B4 (§227.4), §162 |
| PCIe / slots | PCI_E1 Gen5 x16 reserved for the deferred accelerator; PCI_E3 Gen4 x4 carries the 10 GbE NIC; PCI_E2 Gen3 x1 unused (insufficient for 10 GbE); 2×USB4 free for emergency storage/console | B3 (§227.3) |
| Local NVMe (4 slots, all populated) | M2_1 Gen5 x4 (CPU): 1 TB host system; M2_2 Gen5 x4 (CPU, shares with USB4): 4 TB Build/Validation VMs + artifact store; M2_3 Gen4 x2 (chipset, shares with PCI_E3): 1 TB scratch; M2_4 Gen4 x4 (chipset): 4 TB Core/Data VMs + platform data + platform container layers; total 10 TB | B5, B6 (§227.5–§227.6), §163; mapping §6.1 (SE11-DEC-09) |
| Host OS / hypervisor | Windows 11 Pro with Hyper-V; Linux VMs for all durable services; WSL2 + Docker Desktop for interactive work only | B9 (§227.9), §166–§168 |
| Firmware baseline | UEFI Secure Boot and TPM 2.0 enabled; Wi-Fi 7 / Bluetooth disabled; settings baseline in §13.1 | §13 |
| Thermal | Dual-tower air cooling 157 mm in a mesh-front mid-tower with three 140 mm intake fans; sustained 230 W CPU package (+145 W optional GPU) validated by SE11-AC-04 | B2, B8 |

### 5.2 Processor accounting and reservation mechanism (SE11-REQ-14)

| Quantity | Value | Basis |
|---|---|---|
| Physical cores | 16 | B1 |
| Logical processors (LP) available to the hypervisor | 32 | B1 (SMT) |
| vCPUs assigned to VMs | 32 (Core 4, Data 4, Validation 8, Build 16) | §4 |
| vCPU : LP ratio | 1 : 1 at baseline | no oversubscription by vCPU count |
| Guaranteed LPs (Σ processor reserve) | 16 (Core 4, Data 4, Validation 4, Build 4) | reserve % × vCPUs |
| Floating LPs | 16 | host root partition first (2–4 LP typical, ASM-SE11-03), then VMs by weight 200 : 200 : 150 : 100 |

Mechanism on the selected host platform: per-VM **processor resource controls** (virtual machine reserve %, virtual machine limit %, relative weight) and per-VM **memory controls** (static memory = hard reservation; Dynamic Memory with minimum/maximum for burst pools). Members of a shared budget (`pool.agents`, `pool.test`, `pool.background`, `pool.runtime`) are bounded inside their VM by Linux cgroup v2 `cpu.weight`, `cpu.max`, `memory.min`, `memory.max` as listed in §4. Admission: a new VM or member may be created only if (a) Σ reserves stays ≤ 16 LP, (b) Σ static memory + Σ dynamic minimums + host reserve ≤ installed memory, and (c) the pool's storage volume is already mapped in §6.1. This rule is enforced by the version-controlled VM definitions and checked in SE11-AC-03; its behaviour under saturation is verified by SE11-AC-12.

### 5.3 Memory sizing: candidates, hypothetical envelopes and decision rule (SE11-DEC-03, revised)

**Evidence status.** No measured workload exists (§0.1: EL estimates and SE01 capacity model unavailable). The envelopes below are therefore **hypothetical planning envelopes** (ASM-SE11-03) derived only from the five required logical environments (§156) and the layout (§167). They are not evidence, they do not justify any quantity, and they are replaced by the sizing document's model and by measured p95 values (§234 H.3).

| Candidate | Configuration (specification class) | Hypothetical envelope (host 16 + WSL2 8 + Core + Data + Validation min/max + Build min/max) | Fit | Scale path | Trade-off recorded |
|---|---|---|---|---|---|
| **M-A** | 2 × 64 GB matched pair = 128 GB; two slots free | 16 + 8 + 24 + 32 + (12→20) + (12→20) = floor **104 GB**, ceiling **120 GB** | Fits 128 GB with 8 GB headroom at ceiling | Add a second matched pair (re-validate stability, SE11-AC-04 memory pass; 4-DIMM training fallback per §227.4 applies) or replace the kit | Smallest justified start (§158, §238); expansion is not a "single matched kit" (§227.4) — stability must be re-proven; Data VM working set capped at 32 GB until expanded |
| **M-B** | 4 × 64 GB single matched kit = 256 GB (seed reference, board maximum) | 16 + 8 + 32 + 64 + (16→48) + (16→64) = floor **152 GB**, ceiling **232 GB** | Fits 256 GB with 24 GB headroom at ceiling | None (board maximum, hard ceiling REV-MEM) | Buys capacity the envelope does not demonstrate (§238 conflict unless the model shows it); avoids a later kit mix; 4-DIMM training risk flagged by the seed itself |
| **M-C** | Hosted/managed data services for `pool.data` (and optionally hosted validation replica); local host at M-A | M-A envelope minus the Data VM: floor **72 GB**, ceiling **88 GB** | Fits 128 GB (or 96 GB class) | Hosted elasticity | Acceptable per §238 and §160; confidential-processing boundary (§66) and economics (SP16, unavailable) decide; latency to local Core VM becomes a design input for EL |

**Decision rule (SE11-DEC-03).** Let F and C be the committed floor and ceiling produced by SE11-HARDWARE-CAPACITY-SIZING from a traceable Stage-1 workload inventory (concurrent builds, database and search working sets, validation replica size, agent/test concurrency — the inputs EL-ENGINEER-ESTIMATE-CAPACITY and SE01 own). The initial quantity is the smallest candidate whose installed capacity satisfies capacity ≥ 1.25 × F **and** capacity ≥ C + 8 GB. If the host must be built before such a model exists, the seed's H.1 ("start productively") and H.3 ("measure before resizing") apply: **M-A** is installed, unless the Stage-1 inventory already contains a single component whose working set exceeds 32 GB, in which case M-B; the choice and its basis are recorded as SE11-DEC-03a in the sizing document. **256 GB is never adopted on the strength of §5.3 alone.** Non-ECC on the central node is accepted for every candidate (SE11-ADR-03) with the ECC platform class recorded as the substitute if SE11-RISK-02 materialises.

### 5.4 Virtualization / host implications

- VM count and boundaries remain an engineering decision (§167); the four Linux VMs are the minimum that satisfies the isolation rule of §156. Merging Core and Data into one VM is permitted only if the static memory floors are preserved, both stay on M2_4, and SE17 accepts the shared blast radius.
- Highest-priority VMs (Core, Data) use static memory and 100 % processor reserve; they are never configured for dynamic over-commit (SE11-REQ-01).
- Snapshots of the Validation and Core VMs are taken before any firmware/driver change (§10.4) and replicated to `pool.durable`.
- Nothing in the VM layer may encode physical slot ids, device serials or the host name; the portability requirement §160 applies to every VM definition (SE11-REQ-05). Storage is referenced by volume label / stable identifier, not by slot.
- Per-virtual-disk IOPS controls (hypervisor storage QoS minimum/maximum) are part of the host configuration; their availability on the chosen host OS edition is confirmed in SE11-AC-03, and the fallback if unavailable is the stricter device separation of §6.1 alone (recorded in SE11-DEC-09).

### 5.5 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger TRG-GPU (§12.2: local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability, 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms measured full-load system draw plus 145 W ≤ 80 % of the 750 W PSU rating; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on the client hypervisor (device assignment or partitioning) — if none exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as a new SE11-DEC; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator or a dual-slot card is ESCALATE ARCHITECTURE IMPACT (SE11-ADR-04).

## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Authoritative physical mapping of every volume (SE11-DEC-09 / SE11-ADR-09)

This table is the single source of truth; v1's conflicting placements are withdrawn. Sizes are initial allocations (candidate envelope, ASM-SE11-03) and are thin-provisioned so that the sizing document can resize without re-mapping.

| Volume | Pool | Physical device (slot, link) | Initial allocation | Notes |
|---|---|---|---|---|
| Host OS, hypervisor, WSL2 distro disk | `pool.admin` | **M2_1** 1 TB (Gen5 x4, CPU) | whole device | T0 system; rebuildable from version-controlled host build; encrypted (§13.4) |
| Core VM system disk | `pool.core` | **M2_4** 4 TB (Gen4 x4, chipset) | 128 GB | storage-QoS minimum IOPS (defence in depth) |
| Core VM state disk (queues, registry, coordination) | `pool.core` | M2_4 | 256 GB | |
| Data VM system disk | `pool.data` | M2_4 | 64 GB | |
| Data VM database / search / cache disk | `pool.data` | M2_4 | 1.5 TB | database-consistent backups to T2 |
| Platform container image layers (Core/Data services) | `pool.core`/`pool.data` | M2_4 | 256 GB | D-REB |
| M2_4 headroom | — | M2_4 | ~1.8 TB | alert 70 %, review 85 % |
| Validation VM system + replica data disks | `pool.validate` | **M2_2** 4 TB (Gen5 x4, CPU; shares with USB4) | 64 GB + 768 GB | production-like replica; fault injection only here |
| Build VM system disk | `pool.build` | M2_2 | 64 GB | |
| Build VM container layers, agent/test workspaces | `pool.build` members | M2_2 | 512 GB | D-REB |
| Artifact store (active artifacts, served to all pools over the internal virtual switch) | `pool.build` | M2_2 | 1 TB | D-BND; archival copies to T2 |
| M2_2 headroom | — | M2_2 | ~1.6 TB | |
| Build cache / scratch | `pool.build` | **M2_3** 1 TB (Gen4 x2, chipset; shares with PCI_E3) | whole device | D-REB; first device to exhaust TBW |
| **Lane-sharing fallback** (if SE11-AC-02 shows M2_3 and PCI_E3 cannot operate together): scratch | `pool.build` | M2_2 | 512 GB virtual disk with storage-QoS **maximum** IOPS cap | Impact: Build-internal contention only (scratch, artifacts, Build VM all Medium); Highest-priority pools untouched; M2_2 headroom falls to ~1.1 TB; TBW consumption of M2_2 rises — telemetry threshold TRG-NVME-TBW applies; recorded as SE11-DEC-02 fallback |
| T2 durable | `pool.durable` | NAS RAID 6 (count per §6.7) over L1 | per §6.7 | snapshots, backups, evidence, archives, mirrors (§164) |
| T3 isolated copy | — | off-site / hosted, provider selection per NT16 (unavailable) | class D-IRR only | §6.3 |

**Why the mapping deviates from the seed's literal role labels (SE11-DEC-09).** The BOM labels M2_2 "VM & artifact store" and M2_4 "platform data / DBs / containers" (§227.6). Placing *all* VM disks on M2_2 would put the Highest-priority Core and Data system disks on the same device as Medium-priority build artifacts, violating the reservation principle (§157: reserve "storage I/O … for stable platform operation") and SE11-REQ-02. The role labels are guidance on purpose, not an isolation rule; moving the Highest-priority VM disks to M2_4 keeps M2_4 entirely Highest-priority and M2_2 entirely High/Medium. Impact: M2_4 carries both VM system disks and the database — all one priority class, protected additionally by storage-QoS minimum IOPS; M2_2 carries Validation (High) with Build (Medium), bounded by storage-QoS maximum IOPS on build/scratch disks. SE11-REQ-02 is satisfied without exception.

### 6.2 Tiers and dataset classes

| Tier | Device(s) | Role (seed) | Durability boundary | Policy owner |
|---|---|---|---|---|
| T0 system | M2_1 | Windows + WSL2 (§227.5) | Rebuildable; no unique data | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 (Gen4 x2) | Build cache / scratch (§227.5) | Disposable | SE11 |
| T1 hot, Highest | M2_4 | Core/Data VMs, platform data, DBs, platform containers | Independent volume; snapshot + replication to T2 | SE12 (data), EL (VM definitions) |
| T1 hot, High/Medium | M2_2 | Validation/Build VMs, artifact store | Independent volume; archival replication to T2 | SE12 (artifact retention) |
| T2 durable | NAS RAID 6 | Backups, snapshots, release evidence, VM/container archives, artifacts, mirrors (§164) | Dual-parity array + snapshots; "not the only backup" (§164) | SE12 |
| T3 isolated copy | Off-site / hosted, encrypted | "independent/off-site or otherwise isolated copy" for irreplaceable data (§164) | Independent of room, UPS, NAS and host | SE12 (policy), SE17 (keys) |

**Dataset classes (provisional default, ASM-SE11-08; SE12 is the classification owner and replaces this table when its document exists):**

| Class | Definition | Examples | Minimum protection |
|---|---|---|---|
| D-IRR | Irreplaceable: cannot be re-derived from any other platform data | Source repositories and IaC/configuration, non-synthetic platform databases, release-evidence packages, decision logs, inventory records, secret/key backups | T1 + T2 + **verified T3** before the dataset exists |
| D-BND | Bounded loss: re-derivable from D-IRR within an accepted window | Build artifacts, locally built images, validation results, telemetry history | T1 + T2; loss window accepted by SE12 |
| D-REB | Rebuildable from definitions or external sources | Caches, scratch, pulled container layers, VM system disks | T1 only |

### 6.3 Protection activation rule (SE11-REQ-13; corrects finding 009)

1. **Protection levels.** `PL-T2` = T1→T2 snapshot and replication verified (SE11-AC-07a). `PL-T3` = T3 mechanism commissioned and a restore from T3 verified for each D-IRR class (SE11-AC-07b).
2. **Admission rule.** A D-IRR dataset may be created on the platform only while `PL-T3` is active for its class. In `PL-T2` mode only D-BND and D-REB data may exist; the Data VM holds synthetic or rebuildable data only.
3. **Class-specific activation.** Source/configuration repositories: the T3 copy is a hosted remote at an external repository service, active before any local hardware is commissioned (§160 keeps authoritative source in version control outside any single host) — this satisfies `PL-T3` for that class from day one. Databases, release evidence, decision logs, inventory, key backups: the encrypted off-site copy mechanism must pass SE11-AC-07b before the first non-synthetic record is admitted.
4. **Interval and verification.** T3 copy interval ≤ 24 h (SE11-NFR-05); restore verification at every stage gate and after any change to the T3 mechanism or its keys.
5. **Enforcement.** SE11-AC-10 (baseline sign-off) cannot pass while any D-IRR dataset exists in `PL-T2` mode; SE20's admission checklist for the first stable-runtime baseline includes this check; EL's Definition of Ready for data-bearing services references SE11-REQ-13 (EL-ENGINEER-DEFINITI-READY unavailable — requested in §18).
6. **Residual.** Between the loss of the T3 mechanism and its restoration, no new D-IRR data is admitted (platform runs in `PL-T2` with existing D-IRR data exposed to FD-ROOM); the exposure window is logged by SE20 and bounded by SE12's policy.

### 6.4 Bandwidth / IOPS / latency assumptions (device-class figures from the BOM; measured values replace them in SE11-AC-04)

| Path | Nominal from BOM | Engineering assumption used for design |
|---|---|---|
| M2_1, M2_2, M2_4 (Gen4 x4 devices) | up to 7,300 / 6,300 MB/s (§227.5–§227.6) | Sustained mixed workload 2–4 GB/s per device; sub-millisecond latency; NVMe is not the first bottleneck |
| M2_3 (Gen4 x2 slot shared with PCI_E3) | device 7,300 MB/s; slot ≈ half of x4 | ≈ 3–3.5 GB/s ceiling; acceptable for scratch; verified in SE11-AC-02/04 |
| Host ↔ NAS over 10 GbE (L1) | 10 Gb/s ≈ 1.1–1.2 GB/s wire | 0.7–1.0 GB/s sustained for backup/artifact transfer; a 4–6 drive RAID 6 CMR array delivers on the order of 0.5–1.0 GB/s sequential and far lower random IOPS — the NAS is never used for random-IO workloads (§164) |
| Endurance | 600 TBW (1 TB), 2,400 TBW (4 TB) (§227.5–§227.6) | Scratch (M2_3) exhausts TBW first; TBW telemetry mandatory (§10.3); replacement by specification class (§11.4) |

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
| M2_2 failure (Validation + Build VMs, artifacts) | Build/validation outage; runtime continues; restore from T2 archives or rebuild from definitions; D-BND loss within SE12's accepted window | Spare NVMe |
| M2_1 failure (host OS) | All VMs stop until the host OS is rebuilt from the version-controlled host build onto a replacement device; VM disks on M2_2/M2_4 remain intact (no T2 restore needed unless they also fail) | Spare NVMe; host build definition in version control |
| M2_3 failure | Rebuild caches; no data loss | Spare NVMe or fallback mapping |
| Single NAS drive failure | No data loss; degraded; rebuild window ASM-SE11-04; replacement drive of equivalent class | Free bays allow a hot spare as an SE12 decision |
| Two concurrent NAS drive failures | No data loss (RAID 6) | — |
| Host loss (board/CPU/PSU) with intact NVMe | Move the NVMe devices to a replacement host of the §11.4 class or restore VMs to a hosted equivalent (§160, §168) | Hardware-independent definitions (SE11-REQ-05) |

**T3-dependent recoveries (valid only in `PL-T3` mode; in `PL-T2` mode no D-IRR data exists by rule, so the residual is the loss of D-BND/D-REB only):**

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| Third NAS drive failure before rebuild completes (array loss) | Restore D-IRR from T3; D-BND re-derived | Verified T3 copy |
| NAS enclosure loss | T1 continues without a local backup target (degraded, time-boxed by SE12); D-IRR protected by T3 until NAS is replaced | T3 |
| Host loss with NVMe loss, room/site loss (FD-ROOM) | Rebuild on replacement or hosted infrastructure from T3 (D-IRR) and definitions; D-BND re-derived | T3, hosted fallback |

### 6.7 Capacity headroom and NAS capacity candidates (SE11-DEC-06, revised)

| Tier | Candidate / installed | Headroom rule | Expansion path |
|---|---|---|---|
| T1 (M2_2 + M2_4) | 2 × 4 TB (fixed by B6) | Alert 70 %, architecture review 85 % (REV-STORAGE-HOT) | No free M.2 slots: larger devices of the same class (scale-up) or artifact store fronted by T2; SATA ×4 for cold tiers only |
| T2 NAS — **N-A** | 4 × 20 TB RAID 6 → 40 TB nominal, ≈ 36.4 TiB usable (derived with the seed's 80 TB → 72.8 TiB ratio, ASM-SE11-04); 4 bays free | Alert 70 %, review 80 % | Add same-class drives to free bays on TRG-NAS-CAP (online array expansion support by the NAS OS is not established — SE11-AC-01 item) |
| T2 NAS — **N-B** | 6 × 20 TB RAID 6 → ≈ 72.8 TiB usable (seed reference); 2 bays free | as above | 2 free bays |
| T2/T3 — **N-C** | Hosted object storage for T2 and/or T3 (NAS deferred or absent) | provider quota | Hosted elasticity; acceptable per §238; economics unknown (SP16 unavailable) |
| T3 | Must hold at least the D-IRR set | n/a | Provider/medium per SE12 and NT16 |

**Decision rule (SE11-DEC-06).** Let V be SE12's modelled retention volume for the first two stages (D-IRR + D-BND copies at the retention policy, including snapshot overhead). Choose N-A if V ≤ 22 TiB (≈ 60 % of N-A usable); N-B if 22 TiB < V ≤ 44 TiB; above 44 TiB the answer is REV-STORAGE (architecture revision), not simply more drives; N-C if gate G-LOCAL fails for the NAS. If the NAS must be commissioned before the model exists, **N-A** is installed (H.1/H.3) and the choice is recorded as SE11-DEC-06a in the sizing document. **Six drives are never adopted on the strength of this document alone.**

## 7. Network architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-06)

### 7.1 Physical links and roles

| Link | Speed / media | Endpoints | Role |
|---|---|---|---|
| L1 storage/core | 10GBase-T, Cat6a | Host NIC (PCI_E3) ↔ switch ↔ NAS 10 GbE port 1 | Backup, artifact, database-dump, VM-archive transfers; "network capacity appropriate to measured artifact, backup, database, and build traffic" (§166) |
| L2 management/upstream | 5 GbE onboard, Cat6a | Host onboard LAN ↔ switch | Host/VM management, upstream gateway, external-provider traffic, NAS shutdown command path (§8.3) |
| L3 NAS secondary | 10 GbE port 2 (spare), 2×5 GbE | NAS ↔ switch | Expansion: second 10 GbE consumer or link redundancy; 5 GbE for the NAS management segment |
| L4 worker links | 1 / 2.5 GbE (deferred) | Local workers ↔ switch access ports | "Worker links may be slower where sufficient" (§166) |
| L5 uplink | per upstream gateway | Switch ↔ gateway | Internet; external AI providers; hosted runners; T3 transfers |
| Wi-Fi 7 / Bluetooth | — | Host (disabled) | Not part of the architecture; disabled in firmware (§13.1) |

SE11-REQ-04: L1 sustains ≥ 0.7 GB/s host↔NAS during concurrent build-cache activity, and shared storage or control paths are not the first bottleneck during concurrent transfers (§166) — SE11-NFR-02, verified in SE11-AC-05.

### 7.2 Switching / core role

The switch (B17) is the single core: managed, VLAN-capable, at least 2×10 GbE (seed minimum, §230) with ≥ 4×10 GbE preferred so that host, NAS primary, NAS secondary and one future 10 GbE consumer fit without replacement (SE11-ADR-07); 24 access ports at ≥ 1 GbE for workers, management devices and the gateway. Until the switch is installed, an interim point-to-point 10 GbE link host↔NAS with L2 to the gateway is acceptable *placement* — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2); note that in that interim the NAS shutdown command path runs over the point-to-point link, which must then also be on PD-A.

### 7.3 Segmentation (SE11 designs the physical segments, VLAN membership and addressing; SE17 owns the security policy applied between them; SE14 is consulted for portable naming)

| Segment | Members | Purpose | Policy owner |
|---|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS software endpoint | Administrative plane; MFA-protected access (§59); no workload traffic | SE17 (SE11-SECREQ-03) |
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
| PD-A | UPS-A CyberPower CP1500PFCLCD, 1500 VA / 1000 W, line-interactive AVR, 6 battery outlets (B15) | Circuit A: separate 15 A breaker; UPS plugged directly into wall (§231) | Central host, NAS, switch (required for the shutdown command path) | ADOPT WITH ENGINEERING CONSTRAINT |
| PD-B | UPS-B ~1000 VA / 600 W pure sine, model TBD (B16) | Circuit B: second separate 15 A breaker (§231) | Rack PDU → local workers | DEFER / OPTIONAL with the rack |

Isolation rule (§165): worker/rack power is isolated from the host/NAS UPS so a worker fault or overload cannot drop the durable tier. The upstream gateway is placed on PD-A only if the measured PD-A load leaves the runtime reserve of §8.4 intact; otherwise it is powered separately (its loss during an outage is acceptable: the shutdown sequence does not depend on it).

### 8.2 Device power envelopes and circuit/load assumptions

| Device | Envelope used for planning | Source / assumption |
|---|---|---|
| Central host, no GPU | ~350–480 W peak at wall (CPU package ≤ 230 W + board/memory/4×NVMe/fans/NIC + PSU losses) | B1, B7; ASM-SE11-05, replaced by SE11-AC-06 measurement |
| Central host, with GPU | +145 W → ~500–630 W peak | B11 |
| NAS, 4–6 HDD + 2 M.2 | ~70–150 W (spin-up transient higher) | B12/B14 class; ASM-SE11-05 |
| Switch (+ gateway if on PD-A) | ~30–80 W | class estimate, ASM-SE11-05 |
| PD-A total | ~450–710 W without GPU; ~600–860 W with GPU — below the 1000 W UPS-A rating, but battery runtime at these loads is minutes: UPS-A is a controlled-shutdown device, not a ride-through supply (§165) | SE11-AC-06 verifies |
| Whole installation | Seed figures: typical ~560 W, sustained peak ~1,150–1,300 W when the rack is present (§231) | Circuit-sizing input for the electrician |

SE11-REQ-10 (qualified-professional requirement; code-regulated work is not designed here): a licensed electrician verifies that circuits A and B are separate branch circuits of adequate rating for the measured/peak loads above, that receptacles, grounding and surge arrangements meet local code, and whether the optional dedicated 20 A circuit (§231) is warranted; SE11 supplies only the load figures and the two-domain requirement.

### 8.3 Safe-shutdown signalling and state machine (SE11-DEC-07, SE11-DEC-10)

**Signalling topology — gated decision (SE11-DEC-10).** The corpus names two integration surfaces: "automatic graceful shutdown via PowerPanel / NAS UPS service" on the UPS (§229.1) and "UPS support / network UPS server" on the NAS (§228.1). It does **not** establish any protocol/client/version combination between them. SE11 therefore does not assert compatibility; it records three candidates and a gate:

| Candidate | Topology | Cross-device integration required | Status |
|---|---|---|---|
| S-1 (preferred) | UPS-A USB-HID → central host running the UPS vendor's host shutdown software; the host orchestrates VM shutdown and issues an authenticated remote shutdown command to the NAS over `seg.mgmt` | Host↔UPS: vendor software on the host OS version; host→NAS: a remote shutdown interface supported by the NAS OS | Gated by SE11-AC-01 evidence (dated vendor documentation for both interfaces at the exact versions) |
| S-2 | UPS-A USB-HID → NAS as network UPS server; host as network client | NAS server protocol ↔ a host client implementing it | Gated by SE11-AC-01 evidence |
| S-3 (protocol-agnostic fallback) | Two UPS units, each with its own USB-HID path: UPS-A → host; a second UPS of the ≥ 600 W pure-sine line-interactive class → NAS (+ switch) | None across devices | Adopted automatically if neither S-1 nor S-2 produces evidence; recorded as a new SE11-DEC (topology substitution of B15, specification class §11.4) |

No shutdown sequence is relied on until the selected candidate has passed SE11-AC-06 and SE11-AC-14.

**State machine (all candidates; parameters are defaults, replaced by measured values in SE11-AC-06).**

| State | Entry event | Actions | Bounded exit |
|---|---|---|---|
| S0 ONLINE | mains and UPS communication healthy | normal operation; UPS telemetry sampled ≤ 60 s | — |
| S1 ON-BATTERY (hold) | E1 mains loss at T0 | stop admitting new `pool.build`/`pool.background` jobs; alert SE20 | E2 mains restored before T0 + T_hold (60 s) → S0 and resume; else E3 → S2 |
| S2 SHUTDOWN-INITIATED | E3: T0 + T_hold elapsed, **or** UPS low-battery, **or** UPS runtime estimate < B, **or** E4 UPS-communication loss while in S1 (fail-safe: proceed) | (1) send NAS shutdown command, wait for acknowledgment ≤ 15 s, retry once, then proceed regardless; (2) graceful stop Build and Validation VMs in parallel, timeout 60 s then forced stop; (3) graceful stop Core VM, timeout 60 s then forced; (4) graceful stop Data VM, timeout 90 s then forced; (5) host OS shutdown ≤ 60 s. A forced stop marks the VM "unclean" so that its filesystem/database integrity check runs before services start on the next boot. **Once S2 is entered, mains restoration does not abort the sequence** (deterministic, bounded) | → S3 within B_host = 270 s of entering S2 |
| S3 HOST-OFF | host power off | NAS completes its own shutdown (S-1: on the received command; S-2: on its own low-battery threshold after waiting ≤ 60 s for client confirmation; S-3: on its own USB signal) ≤ 120 s | → S4 |
| S4 NAS-OFF | NAS off | switch remains powered until UPS exhaustion (harmless) | — |
| S5 RESTART-PENDING | E5 mains restored while S3/S4 | host firmware "restore on AC power loss = on" and NAS "power-on after AC recovery" bring both up; host UPS software checks battery charge; VM auto-start is withheld until charge ≥ 50 % (prevents a second shutdown without reserve) | → S6 |
| S6 RESTARTED | battery ≥ 50 % | VM auto-start order with delays: Data (0 s) → Core (60 s) → Validation (120 s) → Build (180 s); NAS reachable before Data VM services start; unclean VMs run integrity checks first; SE20 post-event check of backups and telemetry | → S0 |

**Communication-loss handling (E4) in detail.** Loss of host↔UPS communication while in S0: alert; if it persists > 300 s the UPS protection is declared degraded (SE20 ticket, no workload change). If mains then fails while communication is still lost, the host has no event and the outcome is an **abrupt loss** (handled as FD-UPS-A, §9) — this residual is accepted and tested (SE11-AC-14). Loss of the NAS command path (switch or NAS unreachable) in S2: proceed; NAS falls back to its own behaviour (S-2/S-3) or, in S-1, to an uncontrolled stop at UPS exhaustion — accepted residual with CoW crash-consistency and a mandatory scrub on restart (SE11-NFR-07).

**Shutdown budget (SE11-REQ-06, SE11-NFR-03).** B = T_hold (60 s) + B_host (270 s) + margin (30 s) = **360 s (6 min)** worst case, with the NAS shutdown (≤ 135 s from S2) completing in parallel inside B_host. Requirement: B ≤ 0.7 × R, where R is the measured UPS-A runtime at the measured PD-A load; therefore **R ≥ 8.6 min at measured load** for the default parameters. The 30 % reserve is held *against measured runtime*, not against the low-battery signal; the low-battery signal is only an additional trigger.

### 8.4 Fail-closed commissioning outcome

SE11-AC-06 **fails** if R < B / 0.7 at the measured load, or if any state transition exceeds its bound in the drill. Ordered remedies, each recorded as an SE11-DEC when applied: (1) remove non-essential loads from PD-A (gateway first; the switch stays while the NAS command path needs it, unless S-3 is in use); (2) shorten VM stop timeouts only with SE11-AC-13 evidence that clean stops complete within the shorter bound; (3) substitute UPS-A by a higher-runtime unit of the same specification class (§11.4); (4) if none suffices, REV-POWER (§12.3): the architecture is revised (second UPS per device, different UPS class, or hosted relocation of the affected pool). Until SE11-AC-06 passes, no stable-runtime stage baseline is accepted on this hardware (§154 evidence progression) and the platform stays in `PL-T2` mode (§6.3).

### 8.5 Placement constraints (rack / desk / room)

- Central host: tower chassis free-standing with unobstructed mesh-front intake and rear exhaust, off the floor, on PD-A; not inside the 18U rack (rack is for workers/switch/PDU per §230).
- NAS: adjacent to the host on PD-A, within Cat6a reach of the switch; 3.5-inch drives are vibration-sensitive — solid surface, never stacked on the host.
- Switch: rack-mounted when the rack exists; until then shelf-mounted next to the NAS on a PD-A battery-backed outlet.
- Rack (deferred): 18U; 17U used with a gap after every device or 12U without gaps for micro trays (§230); 1U switch, 1U PDU, 1U power-brick shelf, trays sized to the selected worker form factor; PD-B feeds the PDU.
- Room: lockable (§13.3), ambient within device operating ranges, no shared circuit with high-draw appliances (requirement to the electrician under SE11-REQ-10); thermal and rack layout detail belongs to SE11-POWER-COOLING-RACK.

## 9. Failure-domain design (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-08)

Common-mode failure domains are named explicitly so that every consuming document references them by id (SE11-REQ-11). Redundancy "must cover actual shared failure points such as network, power, storage, control plane, DNS, external AI/provider dependencies, and internet connectivity — not merely worker count" (§173). Every domain has an accountable owner, a recovery dependency, a measurable acceptance target and a residual disposition; all dispositions are PROV (§0.2).

| Domain id | What fails together | Blast radius in the reference configuration | Mitigation in this architecture | Accountable owner | Recovery dependency | Acceptance target | Residual disposition |
|---|---|---|---|---|---|---|---|
| FD-HOST | Board, CPU, memory, PSU | All four VMs, all local pools, WSL2; elastic workers lose their coordinator | Hardware-independent definitions (SE11-REQ-05); NVMe portable to a replacement host of the §11.4 class; T2/T3 copies; hosted fallback (§160, §168); queued disposable work idles rather than fails (§175) | SE11 (hardware), EL (architecture residual) | Replacement host class or hosted fallback; T2 (T3 if NVMe also lost) | SE11-NFR-06: degraded service ≤ 1 working day (ASM-SE11-07) | Accepted at Stage 1–2 by EL (unavailable — pending); REV-HA when an SLO requires survival |
| FD-NVME-M2_1 | Host system device | All VMs stop until host OS rebuilt; VM disks intact | Version-controlled host build; spare device class | SE11, SE20 | Spare NVMe; host build definition | Host rebuilt and VMs restarted without T2 restore | Accepted; same class as FD-HOST but shorter |
| FD-NVME-M2_4 | Core + Data VM disks, platform data | **Full platform outage** (control plane and data) | Device isolation (only Highest-priority); storage-QoS min IOPS; hourly snapshots to T2 | SE11, SE12 | T2 (T2-only recovery) | SE11-NFR-05: restore ≤ 4 h per VM, loss ≤ 1 h | Accepted at Stage 1–2; reviewed at REV-HA |
| FD-NVME-M2_2 | Validation + Build VM disks, artifacts | Build/validation outage; runtime continues | Isolation from M2_4; T2 archives; rebuild from definitions | SE11, SE12 | T2 or rebuild | Restore ≤ 4 h; D-BND loss within SE12 window | Accepted |
| FD-NVME-M2_3 | Scratch | Slower builds | Fallback mapping (§6.1) | SE11 | none | Cache rebuilt | None material |
| FD-WORKER | One or more workers (local or hosted) | Capacity reduction only (§172) | Multiple eligible execution targets; no critical service on one uniquely named worker (§172) | EL (placement), SE01 | none | Queue drains on remaining capacity | None material |
| FD-STORAGE | NAS enclosure / array | Backups pause; T1 keeps running; D-IRR protected only by T3 | RAID 6; snapshots; T3; T2 never a live datastore; `PL-T3` admission rule (SE11-REQ-13) | SE11 (hardware), SE12 (data) | T3 for D-IRR; replacement enclosure of the §11.4 class | No D-IRR loss; degraded window time-boxed by SE12 | Accepted only in `PL-T3` mode; in `PL-T2` mode no D-IRR data exists by rule |
| FD-SWITCH | Core switch / its uplink ports | L1, L2, L4, L5; host and NAS lose each other and the internet; VMs keep internal connectivity via the virtual switch; NAS shutdown command path lost | Interim point-to-point L1; spare NAS ports; cold-spare switch of equivalent class is an SE20 stocking decision; S-3 topology removes the command-path dependency | SE11 | Replacement switch class | Backups resume within the SE12 window after replacement; no runtime data loss | Accepted: single switch at Stage 1–2 |
| FD-CIRCUIT-A | Mains/circuit A interruption **with healthy UPS-A** | Host, NAS, switch run on battery → controlled shutdown (§8.3) | State machine S1–S6; budget SE11-REQ-06; AVR | SE11, SE20 (drills); electrician for cause (SE11-REQ-10) | none beyond UPS | SE11-NFR-03 met in SE11-AC-06; automatic restart | Accepted: outage = planned-quality downtime, no data loss beyond in-flight work |
| FD-UPS-A | **Abrupt UPS-A output loss** (UPS fault, overload trip, battery failure) or mains loss while UPS communication is lost | Host, NAS and switch lose power **simultaneously and without warning**; no shutdown energy and no signal path exist | Crash-consistency requirements: journaled guest filesystems, synchronous-commit WAL (SE12), NAS copy-on-write + scrub on restart; restart sequence S5–S6; integrity checks before services start | SE11 (hardware), SE12 (data integrity) | Spare UPS of the §11.4 class; integrity tooling | SE11-NFR-07 met in SE11-AC-13 (abrupt-loss drill) | Accepted: client-class NVMe without asserted power-loss protection (§6.5); loss bounded to last commit; REV-POWER if drills show unrecoverable corruption |
| FD-SIGNAL | UPS signalling path only (USB cable, UPS software, NAS command path) | No immediate workload impact; a later mains loss degrades to FD-UPS-A | E4 handling (§8.3); S-3 topology as fallback; telemetry alert | SE11, SE20 | none | Detected ≤ 300 s; drill SE11-AC-14 passes | Accepted with alerting |
| FD-UPS-B / FD-CIRCUIT-B | UPS-B or circuit B (deferred) | Local workers only | Isolation from PD-A (§165) | SE11 | none | Capacity reduction only | n/a until rack exists |
| FD-ROOM | Rack/room/site (fire, flood, theft) | Total local loss | T3 off-site copy; portability to hosted infrastructure (§160, §168) | SE11 (physical), SE12 (T3), EL (hosted fallback) | T3; hosted capacity | D-IRR restored from T3; service rebuilt on hosted/replacement infrastructure | Accepted only in `PL-T3` mode |
| FD-EXT-AI | External AI providers | `pool.agents` work needing external models; no offline AI until B11 adopted | Provider router/fallback and AI-dependency governance (§66, §115, §185); queued jobs resume (§175) | EL (AI/agent architecture; EL-SYSTEM-AI-AGENT unavailable) | Alternative provider per router policy | Queued work resumes without loss | Accepted by EL (pending); NT16 vendor risk unavailable |
| FD-INTERNET | Uplink / gateway | External providers, hosted runners, T3 transfers, mirrors | Local repositories/mirrors on T2 (§164); local build capacity in `pool.build`; T3 copy interval tolerates outage ≤ 24 h | SE11 (physical uplink), SE20 (operations) | Single uplink restored | Local runtime continues; T3 interval not exceeded for outages < 24 h | Accepted: single uplink at Stage 1–2 |
| FD-MGMT | Management plane (host admin path, NAS admin, switch mgmt, UPS software) | Operator cannot intervene remotely; workloads unaffected | Physical console (§10.2); `seg.mgmt` isolation; configuration in version control | SE11, SE20 | Physical presence | Console recovery procedure drilled once per stage | Accepted: no BMC on the consumer-class board (SE11-RISK-04); REV-HA if SLOs require remote recovery |

Dependency-failure behaviour summary: a local infrastructure problem must not corrupt active builds or accepted runtime state; resumable jobs, durable state and idempotent execution are required of every workload placed on these pools (§175) — EL/SE19 implement and prove this; SE11 guarantees only the physical boundaries above.

## 10. Hardware manageability / operability (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-09)

### 10.1 Inventory identity (SE11-REQ-07)

Every physical asset carries an inventory id `CSPUI-HW-<class>-<nn>` (classes: HOST, NAS, HDD, NVME, NIC, GPU, UPS, SW, RACK, PDU, WKR, CABLE) recorded in a version-controlled inventory file owned by SE11 and published through the hardware-baseline contract (§18.2). Record fields: inventory id; BOM reference (B1–B19); manufacturer part number as cited from SEED-01; serial number; firmware/BIOS/driver version at commissioning; physical position (slot id such as `M2_3`/`PCI_E3`, NAS bay, rack U); power domain (PD-A/PD-B); failure-domain ids (§9); disposition and quantity status (§1.2); pre-build evidence record id (§11.3); commissioning evidence ids (§14); warranty end; sanitisation state. Cables are labelled at both ends with the endpoint ids. The **configuration fingerprint** (§11.3) is derived from these records.

### 10.2 Remote-management capabilities where available

| Device | Out-of-band | In-band management path | Fallback |
|---|---|---|---|
| Central host | None (consumer board; no BMC/IPMI) — SE11-RISK-04 | Windows remote administration and Hyper-V management on `seg.mgmt`; MFA per §59 | Physical console in the lockable room; UEFI Flash BIOS and Clear CMOS on the rear panel (B3) |
| NAS | None | NAS OS web/remote administration on `seg.mgmt` | Front panel / USB |
| Switch | Management port if the class provides one | Management VLAN | Console port |
| UPS-A | USB-HID to the host (S-1/S-3) or NAS (S-2) | Status via the UPS software's telemetry export | Front LCD |

### 10.3 Telemetry and health status (SE11-REQ-08, SE11-NFR-04; consumed by SE20 monitoring, SE01 capacity, SE19 validation)

Mandatory signals from first power-on ("capture performance/resource telemetry from the first workloads", §160; "capture CPU, memory, I/O, network, queue time, job duration, reliability, and cost", §234): host CPU utilisation per VM and total, CPU-wait per VM, memory committed per VM and host, NVMe SMART (temperature, media errors, percentage used, TBW consumed) per device, per-virtual-disk IOPS and latency, PCIe negotiated width/speed per slot (detects degraded M2_3/PCI_E3 sharing), NIC link speed and errors, NAS array state (healthy/degraded/rebuilding), per-drive SMART, NAS volume utilisation, snapshot success, backup and T3 job success/duration/throughput, UPS state (online/on-battery/low-battery, load %, runtime estimate, battery age, communication state), host and NAS temperatures, switch port utilisation on L1/L2, protection level (`PL-T2`/`PL-T3`). Thresholds that trigger expansion or revision are in §12.

### 10.4 Firmware / BIOS / driver lifecycle (SE11-REQ-09)

- Components with a firmware lifecycle: host UEFI/BIOS (incl. CPU microcode/AGESA), NVMe firmware ×4, NIC driver/firmware, optional GPU driver, NAS OS and HDD firmware, UPS firmware and host UPS software, switch firmware.
- Update path: vendor-signed images only, checksum verified against the vendor publication, staged in a declared maintenance window (§10.5) after a successful snapshot of all VMs and a verified T2 backup; one component class per window; rollback plan recorded; post-update SE11-AC-04 smoke subset executed; firmware settings baseline re-verified (SE11-AC-08); configuration fingerprint updated.
- Ownership: SE20 schedules and executes; SE17 defines integrity controls (SE11-SECREQ-02); SE11 keeps the compatibility matrix (§11) current.

### 10.5 Maintenance windows

Hardware maintenance is performed only in a window declared to SE20's operations calendar that does not overlap a stage-gate VP validation (§174 "VP validation / release assurance"). Minimum window content: pre-checks (backup verified, snapshots taken, UPS healthy, `PL-*` state recorded), the change, post-checks (SE11-AC-04 smoke, telemetry nominal), inventory record and fingerprint updated.

## 11. Compatibility / availability assessment (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-10)

### 11.1 Structural compatibility check (from the BOM specifications themselves)

| Check | Items | Result from BOM data | Residual verification |
|---|---|---|---|
| Socket / chipset | B1 AM5 ↔ B3 AM5/X870 | Structurally compatible | BIOS version supporting the CPU: **not established** (§11.2) |
| Memory | B4 DDR5 UDIMM ↔ B3 "4× DDR5 DIMM, up to 256 GB" | Compatible at capacity; DDR5-6000 EXPO on four DIMMs is a stability-validated profile, not a guaranteed one (the seed prescribes the 5600/5200 fallback) | Exact population (2-DIMM M-A vs 4-DIMM M-B) on the board's qualified list: **not established**; stability pass SE11-AC-04 |
| Cooler | B2 157 mm ↔ B8 ~166 mm clearance; AM5 mounting included | Compatible | — |
| Form factor | B3 ATX ↔ B8 ATX/E-ATX | Compatible | — |
| PCIe lane sharing | B10 in PCI_E3 (Gen4 x4, "shares with M2_3") ↔ B5 in M2_3 (Gen4 x2) | Simultaneous operation **not established** from BOM text (sharing may mean reduced width or mutual exclusion) | SE11-AC-02 read-back; fallback mapping §6.1 |
| M2_2 ↔ USB4 sharing | B6 on M2_2 ("sharing with USB4") | USB4 unused at baseline; no conflict | Confirm USB4 use does not down-shift M2_2: SE11-AC-02 |
| PSU | B7 750 W, 12V-2x6 ↔ B1 230 W + B11 145 W + platform | Within rating for the no-GPU build; GPU build conditional on measurement (seed condition) | SE11-AC-06 |
| GPU mechanical | B11 single-slot 241 mm ↔ B8 mid-tower, PCI_E1 x16 | Expected to fit; not asserted | SE11-AC-02 before adoption |
| NAS memory | B13 DDR5-4800 ECC SO-DIMM ↔ B12 "2 slots; 64 GB max"; mixed 16 + 32 GB | Capacity compatible; mixed pair support **not established** | SE11-AC-01 (deferred item) |
| NAS drives | B14 3.5-inch SATA CMR ↔ B12 8 SATA bays | Compatible | Online RAID 6 expansion support: **not established** (SE11-AC-01) |
| Network | B10 10GBase-T ↔ B12 2×10 GbE; Cat6a supplied with NAS (§228.1) | Compatible | Switch class 10GBase-T or SFP+ with matching transceivers: SE11-AC-05 |
| UPS | B15 1000 W ↔ PD-A loads (§8.2); NEMA 5-15P ↔ 15 A circuit (§231) | Compatible; runtime unknown until measured | SE11-AC-06 |
| UPS signalling | B15 USB-HID / host software ↔ B12 network UPS server | **Not established** (§8.3) | SE11-AC-01, SE11-DEC-10 |
| OS / virtualization | B9 Windows 11 Pro ↔ Hyper-V; TPM 2.0 + Secure Boot prerequisites; Linux guest support; NIC driver for the virtual switch; per-virtual-disk IOPS controls | Hyper-V is a Pro feature; TPM/Secure Boot are install prerequisites so the platform must provide them; NIC driver and storage-QoS availability **not established** | SE11-AC-01, SE11-AC-03 |

### 11.2 Current manufacturer support and practical availability — NOT ESTABLISHED (criterion QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03 is **unmet** in this version)

The allowed corpus contains no manufacturer support statement, firmware/BIOS release information, qualified-vendor list, driver compatibility statement or market availability for any BOM item, and SE11 has no access to manufacturer publications in this run. Therefore, for every item below, the following are **not established** and are **not asserted** (BND-04): current manufacturer support status; a BIOS version supporting the CPU; the exact memory population on the board's qualified list; simultaneous PCI_E3/M2_3 operation; NIC driver support for the hypervisor virtual switch; hypervisor storage-QoS availability on the host OS edition; UPS software ↔ host OS and NAS ↔ UPS protocol compatibility; NAS online array expansion; practical availability of any part number. Consequently: (a) all B1–B17 items remain **conditional candidates** of their specification class; (b) QC-AR-03 is reported as unmet (§19) rather than covered; (c) nothing in this document is to be read as a verified buildable combination; (d) a structural comparison copied from the BOM (§11.1) is not a support check. The gap is closed only by the pre-build evidence record of §11.3, which is a separate activity from the commissioning tests of §14.

### 11.3 Pre-build support evidence record (SE11-AC-01) and configuration fingerprint

**Pre-build checks (before any build, per item; dated and attributable):** manufacturer support status; BIOS/firmware version required for the combination; memory population and profile on the qualified list; slot coexistence statement; driver/OS/hypervisor support statement; UPS software/protocol statement; availability statement. Evidence record fields: item (B-id), part number as cited, claim checked, source (publisher, document title/version, date accessed), result (confirmed / not confirmed / superseded), consequence (adopt as evidenced / substitute per §11.4 with a new SE11-DEC / defer), recorder. "Not confirmed" on any item blocks that item; a superseded item is substituted by specification class and recorded (SE11-REQ-12).

**Commissioning tests (after build, §14):** SE11-AC-02 … SE11-AC-14 measure what the built configuration actually does; they never substitute for the pre-build record.

**Configuration fingerprint.** Sign-off (§17) binds to the exact evidenced configuration: the ordered list of (B-id, part number, serial, firmware/BIOS/driver version, slot/bay position, memory population, candidate selected M-x/N-x, signalling topology S-x). Any change to the fingerprint re-opens SE11-AC-01 for the changed item and SE11-AC-10 for the baseline.

### 11.4 Alternatives by specification class (not procurement preference; preserve performance, reliability, security, portability and schedule assumptions)

| BOM item | Specification class |
|---|---|
| B1 CPU | AM5 desktop CPU, ≥ 16 physical cores, ≥ 64 MB L3, ≤ 230 W package, hardware virtualization + IOMMU |
| B3 motherboard | ATX AM5, 4×DDR5 to ≥ 256 GB, ≥ 1× PCIe x16 (CPU) + ≥ 1× PCIe x4 slot usable concurrently with ≥ 4× M.2 (≥ 2 of them x4), ≥ 2.5 GbE onboard, UEFI Secure Boot, TPM 2.0 |
| B4 memory | Matched DDR5 UDIMM kit per candidate M-A/M-B (§5.3), ≥ DDR5-5200 validated at the chosen population; ECC-capable platform class is the recorded substitute if SE11-RISK-02 materialises |
| B5/B6 NVMe | M.2 2280 PCIe 4.0 x4 (or 5.0), TLC with DRAM, ≥ 600 TBW per TB, 5-year warranty class; devices with power-loss protection are the recorded upgrade class if SE11-AC-13 shows unrecoverable corruption |
| B7 PSU | ATX 3.1 / PCIe 5.1, ≥ 750 W, Cybenetics Gold or better, native 12V-2x6, fully modular, ≥ 7-year warranty class |
| B8 case | Mid-tower ATX with mesh front, ≥ 160 mm cooler clearance, ≥ 250 mm GPU clearance |
| B10 NIC | 10GBase-T (or SFP+ with matching switch), PCIe 3.0 x4 or 4.0 x2 minimum, driver supporting the Windows Hyper-V virtual switch |
| B11 GPU | Single-slot, ≤ 145 W, ≥ 24 GB ECC VRAM, PCIe x16, 12V-2x6 or 8-pin; larger classes ESCALATE |
| B12 NAS | 8-bay SATA NAS with ECC memory, ≥ 2×10 GbE, Btrfs/ZFS-class snapshots, per-folder/volume AES-256, UPS integration (any of S-1/S-2/S-3), M.2 cache slots; hosted object storage is the equivalent for T2/T3 under G-LOCAL |
| B14 HDD | 3.5-inch enterprise CMR, 7,200 RPM, ≥ 2.5 M h MTBF, ≥ 550 TB/yr workload, 5-year warranty, ≥ 20 TB (smaller same-class drives permitted under N-A if V is small) |
| B15/B16 UPS | Pure-sine line-interactive with AVR, USB-HID, ≥ 1500 VA / 1000 W (PD-A) and ≥ 1000 VA / 600 W (PD-B or S-3 NAS unit), user-replaceable batteries; higher-runtime units of the same class are the remedy under §8.4 |
| B17 switch | Managed L2+, ≥ 2×10 GbE (≥ 4 preferred), 24× ≥ 1 GbE access, VLAN, port mirroring for SE17/SE19 |

## 12. Expansion model (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-12)

### 12.1 Planned spare capacity at baseline

| Resource | Spare at baseline | Scale path |
|---|---|---|
| Host PCIe | PCI_E1 x16 (reserved for GPU), PCI_E2 x1, 2×USB4 | Scale-up only |
| Host memory | M-A: two free slots (second matched pair, re-validation); M-B: none (board maximum) | **Hard ceiling at 256 GB** — REV-MEM |
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
| TRG-GPU | Measured external-model latency/cost/privacy case or GPU-required application testing (§176) with §5.5 preconditions met | Adopt B11 |
| TRG-MEM-EXPAND (M-A only) | Measured committed memory p95 > 80 % of installed for one stage, or a single component working set > 32 GB | Add the second matched pair (re-run SE11-AC-04 memory pass); record SE11-DEC |
| TRG-NAS-MEM | NAS memory sustained > 70 % or snapshot/backup jobs missing their window from memory pressure | Install B13 |
| TRG-NAS-CAP | T2 utilisation > 70 % | Add same-class drives to free bays (N-A → N-B) |
| TRG-NET-10G | L1 utilisation > 70 % sustained during backup windows, or a second 10 GbE consumer | Use NAS second 10 GbE / add 10 GbE ports within the switch class |
| TRG-NVME-TBW | Any NVMe > 80 % of rated TBW or media errors | Replace with same class (§11.4) |
| TRG-UPS-BATT | UPS runtime estimate at measured load < B / 0.7 | Battery replacement (RB1290X2 class, B15) or §8.4 remedies |

### 12.3 Scale-out versus scale-up boundaries and architecture-revision triggers

The central node complements, never replaces, horizontally scalable workers (§177). Scale-out (more workers, hosted executors) is the default answer to throughput; scale-up applies only to the capabilities the seed assigns to the central node — large contiguous RAM, low-latency CPU, NVMe, centralized data/control services (§161). The following require a revision of this architecture (new SE11 version plus EL review), not a hardware addition:

| Revision trigger | Why adding hardware is insufficient |
|---|---|
| REV-MEM: Highest-priority pool floors exceed 85 % of 256 GB on measured p95 | Board ceiling reached; second host, larger-memory platform class, or hosted data services (M-C) is an architectural choice |
| REV-HA: an SLO (§117) requires the control plane or Data VM to survive FD-HOST or FD-NVME-M2_4 | Needs a second failure domain and quorum design (§173) |
| REV-GPU-CLASS: accelerator > 145 W, dual-slot, or second accelerator | Exceeds PSU, slot and thermal envelope (§5.5) |
| REV-STORAGE-HOT: T1 > 85 % after device scale-up, or a random-IO workload that cannot stay on host NVMe | NAS is not a hot tier (§164) |
| REV-STORAGE: retention volume V > 44 TiB (§6.7) | Beyond the enclosure's economical RAID 6 envelope; hosted tier or second enclosure is architectural |
| REV-NET: storage/core path saturated after all 10 GbE ports used, or 25 GbE class needed | Switch and NIC class change ripples through host slots |
| REV-SITE: geographic/resilience footprint beyond one room (§226 F.20) | Hosted/hybrid footprint decision |
| REV-POWER: §8.4 remedies exhausted, PD-A measured peak within 20 % of UPS-A rating, or circuit limits reached | UPS/circuit redesign by qualified professionals; possible relocation |

## 13. Security considerations (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-11)

The owners of the control catalogue (SE17 for infrastructure/workload/data security, SE15 for identity and cryptography, §74) have not published control ids in this run (their documents are not among the available inputs, §0.1). This section therefore states SE11's hardware security **requirements** under SE11's own identifiers; each is to be mapped to the owner's control id when it exists, and no foreign id is invented. Nothing here re-derives a control design.

| Id | Requirement placed on the hardware baseline | Proposed owner for the control | Verified by |
|---|---|---|---|
| SE11-SECREQ-01 Trusted boot | UEFI Secure Boot enabled; TPM 2.0 present and enabled; boot order locked to M2_1; UEFI administrator password set; measured-boot attestation is the owner's decision | SE17 | SE11-AC-08 |
| SE11-SECREQ-02 Firmware integrity | Vendor-signed images only, checksum verified, staged in maintenance windows with snapshot + verified backup first (§10.4); firmware settings baseline (virtualization, IOMMU, Secure Boot, TPM, Wi-Fi/Bluetooth disabled) re-verified after every BIOS update | SE17 (policy), SE20 (execution) | SE11-AC-08 |
| SE11-SECREQ-03 Management-plane isolation | All management endpoints (host admin, hypervisor, NAS admin, switch, UPS software) only on `seg.mgmt`, unreachable from `seg.build`, `seg.worker`, `seg.egress`; MFA and least-privilege, short-lived credentials per §59, §112; no management interface exposed to the internet | SE17 (network policy), SE15 (identity) | SE11-AC-05, SE11-AC-08 |
| SE11-SECREQ-04 Physical and administrative access | Lockable room; host, NAS, switch and UPS inside; physical console use is a logged administrative action; segregation between hardware maintenance (SE11/SE20) and security configuration (SE17) per §112 | SE17 | SE11-AC-08 |
| SE11-SECREQ-05 Data at rest | Host full-disk encryption on M2_1 with TPM-bound keys; encryption of VM disks on M2_2/M2_4 inside the Linux VMs or by the hypervisor (hardware supports both; owner decides); NAS per-folder AES-256 (B12) for backups, evidence and archives; T3 copies encrypted before leaving the site; key custody and recovery under the owner's control | SE17, SE15 (keys) | SE11-AC-08 |
| SE11-SECREQ-06 Media sanitisation | NVMe and HDD sanitised on decommissioning/RMA; inventory record marks sanitised state | SE17 | SE11-AC-10 |
| SE11-SECREQ-07 Supply chain at receipt | Serial numbers recorded; packaging/tamper evidence inspected; firmware version read and compared with the vendor's published current version before first power-on; default credentials on NAS, switch and UPS software rotated at commissioning | SE17 | SE11-AC-01 (pre-build), SE11-AC-10 |
| SE11-SECREQ-08 Confidential-processing boundary | Private application/customer data is processed only by authorised locally hosted models or deterministic tools (§66); any local accelerator (B11) and the Data VM sit inside `seg.platform` behind the default-deny disclosure gateway on `seg.egress`; hardware telemetry export (§10.3) carries no workload content | SE17, EL | SE11-AC-05, SE11-AC-09 |

## 14. Validation / evidence plan (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-14)

Pre-build checks (AC-01, AC-11) are separate from commissioning tests (AC-02 … AC-14); commissioning never substitutes for the pre-build record (§11.3).

| AC id | Check | Pass criterion | Evidence artefact | Executing owner | Needed before |
|---|---|---|---|---|---|
| SE11-AC-01 | **Pre-build** support, compatibility and availability evidence record (§11.3) | Every B1–B17 item has a dated, attributable record for each claim in §11.3; "not confirmed" items substituted per §11.4 with a new SE11-DEC or deferred; signalling candidate S-1/S-2 evidenced or S-3 adopted; receipt check (SE11-SECREQ-07) complete | Evidence record attached to the inventory; configuration fingerprint v0 | SE11 (SE20 assists at receipt) | Any build |
| SE11-AC-11 | **Pre-build** reconciliation of this document to PL-REQ-ID-REGISTER rows and to EL/PM09/NT16/SP16 decisions once available (§0) | Every seed citation mapped to a register id; every ADR checked against EL ADRs; NFR values bound to EL/PM09 NFR ids or recorded as conflicts; status PROV → REC | Reconciliation table in SE11-PHYSICAL-INFRASTR-HARDWARE v3 | SE11, EL review | Baseline status above PROVISIONAL |
| SE11-AC-02 | Slot, lane and mechanical verification | Negotiated PCIe width/speed for M2_1–M2_4 and PCI_E3 with all devices installed; M2_3/PCI_E3 coexistence confirmed or fallback mapping invoked (SE11-DEC-02); cooler/case clearance photos; GPU mechanical check when B11 is triggered | Link-state dump; inventory photos | SE11 | Stage 1 |
| SE11-AC-03 | OS / virtualization enablement and reservation mechanism | Hyper-V operational with the four VMs at the §4 reserve/limit/weight and static/dynamic memory settings; admission rule (§5.2) encoded in version-controlled definitions; per-virtual-disk IOPS controls present or SE11-DEC-09 fallback recorded; NIC bound to the virtual switch at 10 Gb/s; Secure Boot + TPM reported enabled; GPU-to-VM path evaluated when triggered | Hypervisor and guest configuration export | SE11 with EL | Stage 1 |
| SE11-AC-04 | Burn-in and performance baseline (SE11-NFR-08) | ≥ 24 h combined CPU/memory/NVMe stress with zero memory errors at the chosen DDR5 profile (fallback 5600/5200 per B4) at the selected population M-A/M-B; thermals within limits; NVMe sequential/random, per-virtual-disk and L1 throughput recorded as the measured replacement for §6.4 | Stress logs; telemetry export; baseline table | SE19 (executes), SE11 (accepts) | Stage 1 |
| SE11-AC-05 | Network path and segmentation (SE11-NFR-02, SE11-SECREQ-03) | Host↔NAS ≥ 0.7 GB/s sustained 10 min under concurrent build-cache load; `seg.*` enforced; management plane unreachable from build/worker/egress segments | Throughput log; segmentation test log | SE11 (physical design/test), SE17 (policy), SE19 (measurement) | Stage 1 |
| SE11-AC-12 | Contention and protected-floor test (SE11-NFR-01) | Profile: Build VM 100 % CPU + heavy IO on M2_2/M2_3, Validation VM 100 %, background saturating, T1→T2 backup transfer running on L1; Core probe p95 ≤ 1.5 × baseline, Data VM random-read p99 ≤ 2 × baseline, Highest-priority CPU-wait ≤ 5 %; observed throttling order background → build → validation | Load-test report with per-VM CPU share and per-virtual-disk latency | SE19 (executes), SE11 (accepts) | Stage 1 before stable-runtime baseline |
| SE11-AC-06 | Power measurement and mains-loss drill (SE11-NFR-03; fail-closed §8.4) | Measured PD-A load (idle, typical, full stress, with/without GPU); measured runtime R at full-stress load; full mains-loss drill traverses S1 → S6 with every transition inside its bound and B ≤ 0.7 R; VMs and NAS return clean; electrician's sign-off of circuits A/B on file (SE11-REQ-10) | Power table; drill log with timestamps per state; professional sign-off reference | SE11 (measurement), SE20 (drill), qualified electrician (circuits) | Stage 1 before stable-runtime baseline |
| SE11-AC-14 | Signalling-path-loss drill (FD-SIGNAL) | (a) USB/UPS-software path removed while on mains: alert ≤ 300 s; (b) NAS command path removed during S2: host completes its sequence inside B_host and the NAS follows its own fallback; (c) communication lost then mains lost: outcome recorded as abrupt loss and handled by SE11-AC-13 | Drill log | SE20 (drill), SE11 (accepts) | Stage 1 |
| SE11-AC-13 | Abrupt-loss drill (FD-UPS-A, SE11-NFR-07) | UPS-A output removed under full contention profile; on restart every VM and host filesystem and the NAS array pass integrity checks with zero unrecoverable errors; database loss ≤ last committed transaction (SE12 verifies); scrub completes | Integrity-check logs; SE12 verification record | SE19/SE20 (drill), SE12 (data), SE11 (accepts) | Stage 1 before any D-IRR admission |
| SE11-AC-07a | T1→T2 protection (`PL-T2`) | Snapshot + replication verified; restore of a VM and a database from T2 to a clean volume within SE11-NFR-05 (SE12's binding RTO if stricter); NAS single-drive pull with rebuild time recorded (replaces ASM-SE11-04) | Restore drill log; rebuild timing | SE12 (policy), SE19/SE20 (drill) | Stage 1 |
| SE11-AC-07b | T3 protection (`PL-T3`) per D-IRR class | T3 mechanism commissioned; copy interval ≤ 24 h demonstrated; restore of each D-IRR class from T3 verified; T3 encryption and key recovery verified (SE11-SECREQ-05) | T3 inventory; restore log | SE12 (policy), SE17 (keys), SE20 (drill) | **Before the first D-IRR dataset of that class exists** (repositories: before local commissioning; databases/evidence: before non-synthetic data enters the Data VM) |
| SE11-AC-08 | Security baseline of hardware | SE11-SECREQ-01 … 08 verified against the inventory ids; default credentials rotated; encryption active where required | Owner control evidence referencing inventory ids | SE17 (SE15 for keys/identity) | Stage 1 (host, NAS); full at Stage 3 |
| SE11-AC-09 | Telemetry coverage (SE11-NFR-04) | Every §10.3 signal visible in SE20 monitoring with alert thresholds from §12.2 and the `PL-*` state | Dashboard/alert export | SE20 | Stage 1 |
| SE11-AC-10 | Inventory and baseline sign-off | Inventory complete; configuration fingerprint recorded; no D-IRR data present in `PL-T2` mode; §17 record filled with evidence ids of AC-01 … AC-14; contract record (§18.2) updated | Signed baseline record | SE11 | Before downstream consumption as "VERIFIED" |

Resilience tests beyond the above (fault injection on `pool.validate`, switch loss, NAS loss, provider loss, uplink loss) are specified and run by SE19 against the §9 domains; SE11 supplies the physical means (spare cables, drive-pull and power-cut procedures) and accepts the evidence.

## 15. Exclusions (BND-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01 … AR-04)

| Exclusion | Disposition in this document |
|---|---|
| BND-01 Purchase orders, price negotiation, vendor-selection scorecards, procurement workflow | Excluded. No prices, suppliers, order quantities or purchase approvals appear; part numbers are cited only as they appear in SEED-01 and alternatives are by specification class (§11.4). Nobody owns procurement in this chain. |
| BND-02 Project-owned acquisition dates | Excluded. Only dependency windows are referenced ("Stage 1", "before the first D-IRR dataset"); no calendar dates. |
| BND-03 Detailed software/container/service design owned by existing SE11 artefacts | Excluded. §4–§6 stop at pools, VM boundaries, hypervisor reservation controls and volume mapping; service design, images and pipelines are referenced to EL and SE11's runtime artefacts. The cgroup share defaults in §4 are budget boundaries, not service design. |
| BND-04 Unverified assumptions presented as confirmed hardware facts | Complied with. Every non-seed figure is an engineering assumption (ASM-SE11-nn) or a validation gate (SE11-AC-nn); support, compatibility and availability are explicitly **not established** (§11.2); no vendor protocol compatibility is asserted (§8.3). |

## 16. Architecture risks, decisions and ADRs (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-13)

### 16.1 Architecture decision records (all PROV, §0.2)

| ADR | Decision | Alternatives considered | Rationale |
|---|---|---|---|
| SE11-ADR-01 (rewritten) | The **candidate** physical architecture is one central node + durable NAS + elastic hosted-first worker pool. Each local element passes gate **G-LOCAL** before it is provisioned: workload evidence *and* economics justify it (§238), and no managed/hosted equivalent better satisfies the target requirements. Until G-LOCAL evidence exists (EL estimates, SE01 capacity, SP16 economics — all unavailable), every pool may be delivered locally or hosted | (a) Two-node local cluster from day one — rejected now: no measured need, violates no-overbuild (§158). (b) All-hosted — **not rejected**: it is the seed's acceptable equivalent (§238 "managed/hosted equivalents remain acceptable", §160 "must remain valid if the equivalent capacity is delivered by … hosted infrastructure, or a hybrid") and the fallback for FD-HOST/FD-ROOM; §66 favours local handling of confidential data but does not mandate local hardware | §160, §226, §238; v1's rejection of the hosted option contradicted §238 and is withdrawn |
| SE11-ADR-02 | Windows 11 Pro host with Hyper-V Linux VMs for all durable services; WSL2 for interactive use only | Bare-metal Linux hypervisor — rejected: the seed fixes the preferred operating model (§166) and retains Windows for workstation/admin use (§227.9); portability is preserved at the VM/container-definition level (§168) | §166–§168 |
| SE11-ADR-03 | Non-ECC DDR5 on the consumer AM5 platform accepted for the central node, monitored | ECC workstation/server class — recorded substitute if memory-error telemetry or data-integrity incidents attributable to memory occur (SE11-RISK-02) | §227.4; durable tier (NAS) is ECC (§228.1) |
| SE11-ADR-04 | GPU deferred; adoption gated by §5.5 and TRG-GPU; accelerator class capped at single-slot ≤ 145 W within this architecture | Adopt at first build — rejected: §175/§177 make it optional and demand-driven; external providers are the default (§160) | §175–§177 |
| SE11-ADR-05 | Host NVMe as independent volumes without RAID; NAS as durable/backup tier only; one-way replication T1 → T2 → T3 | Host NVMe mirroring — rejected (does not address FD-HOST; doubles cost); NAS as live VM datastore — rejected (§164: not a latency substitute; would make FD-STORAGE a hot-path SPOF) | §163, §164 |
| SE11-ADR-06 (revised) | UPS signalling is a **gated** selection among S-1 (preferred), S-2 and S-3 (§8.3), decided by SE11-DEC-10 on pre-build evidence; shutdown order NAS-command → Build‖Validation → Core → Data → host | v1 chose S-2 (NAS as network UPS server) without compatibility evidence — demoted to a candidate, not rejected | §165, §228.1, §229.1 |
| SE11-ADR-07 | Single managed switch, ≥ 2×10 GbE minimum (seed), ≥ 4×10 GbE preferred; interim point-to-point 10 GbE allowed as placement | Unmanaged switch — rejected (segmentation needs VLANs); dual redundant switches — rejected now (§166 "purchased incrementally from measured need") | §166, §230 |
| SE11-ADR-08 (new) | Capacity **quantities** (memory kit, NAS drive count) are candidates governed by decision rules (§5.3, §6.7) and the seed's H.1/H.3 default to the smaller configuration; the maximum listed configuration is never adopted on the strength of this document | Adopt the seed's listed quantities as given — rejected: ENV-DEC-017 ("size from workload evidence, not to the maximum listed configuration"), §162, §238 | §158, §162, §234, §238 |
| SE11-ADR-09 (new) | Storage mapping places Highest-priority VM disks on M2_4 and High/Medium VM disks + artifacts on M2_2 (§6.1), deviating from the BOM's literal role labels, with per-virtual-disk IOPS controls as defence in depth | Literal seed mapping (all VMs on M2_2) with IOPS controls only — rejected: puts Highest and Medium pools on one device, contrary to §157 and SE11-REQ-02; controls would be the sole protection | §157, §163 |

### 16.2 Decisions (SE11-DEC-nn; all PROV)

| Id | Decision | Impact |
|---|---|---|
| SE11-DEC-01 | B1 adopted with virtualization/IOMMU enabled and 230 W package limit as the compute power line | §8.2; SE11-AC-04 |
| SE11-DEC-02 | B3/B5/B10 adopted with the PCI_E3–M2_3 lane-sharing constraint; fallback scratch on M2_2 (512 GB, IOPS-capped) if mutually exclusive | §6.1; SE11-AC-02 |
| SE11-DEC-03 | B4 adopted as a specification class; quantity is a candidate (M-A/M-B/M-C) selected by the §5.3 rule in SE11-HARDWARE-CAPACITY-SIZING (recorded there as SE11-DEC-03a); 256 GB not adopted here | §5.3; SE11-RISK-02, SE11-RISK-10 |
| SE11-DEC-04 | B7 adopted; GPU power conditional on SE11-AC-06; > 145 W class escalates | §5.5; REV-GPU-CLASS |
| SE11-DEC-05 | B13 deferred to TRG-NAS-MEM | stock 16 GB ECC until telemetry justifies |
| SE11-DEC-06 | B14 adopted as a drive class with RAID 6 mandatory; count is a candidate (N-A/N-B/N-C) selected by the §6.7 rule with SE12's retention model (recorded as SE11-DEC-06a); six drives not adopted here | §6.7; SE11-RISK-06, SE11-RISK-10 |
| SE11-DEC-07 | Shutdown state machine, order and budget of §8.3 with the fail-closed outcome of §8.4 | SE11-REQ-06, SE11-NFR-03 |
| SE11-DEC-08 | Switch adopted by class now; rack/PDU/trays/UPS-B/local workers deferred to TRG-WKR-LOCAL | §7.2, §8.1, §12.2 |
| SE11-DEC-09 | Authoritative volume mapping of §6.1; Highest-priority VMs on M2_4; deviation from literal BOM role labels recorded with reason and impact; per-virtual-disk IOPS controls or, if unavailable, device separation alone | §6.1, §9 |
| SE11-DEC-10 | UPS signalling topology gated: S-1 preferred, S-2 alternative, S-3 automatic fallback; none relied on before SE11-AC-01/06/14 | §8.3; SE11-RISK-11 |

### 16.3 Requirements introduced by this document (SE11-REQ-nn; all PROV)

| Id | Requirement | Verified by |
|---|---|---|
| SE11-REQ-01 | Hard reservations (static memory, 100 % processor reserve) for `pool.core`, `pool.data`, `pool.runtime`; every other pool has a declared floor/ceiling or an explicit shared-budget membership with a stated share | SE11-AC-03, SE11-AC-12 |
| SE11-REQ-02 | No Highest-priority pool shares a physical NVMe device with a Medium-priority pool | SE11-AC-02/03 (mapping §6.1) |
| SE11-REQ-03 | T0/T1 is never the sole copy of D-IRR or D-BND data; every T1 dataset has a T2 copy; every D-IRR dataset has a verified T3 copy | SE11-AC-07a/b |
| SE11-REQ-04 | L1 sustains ≥ 0.7 GB/s host↔NAS under concurrent build-cache load; shared paths are not the first bottleneck | SE11-AC-05 |
| SE11-REQ-05 | VM/container definitions carry no physical slot ids, serials or host names (portability §160) | SE11-AC-03 review |
| SE11-REQ-06 | Shutdown budget B ≤ 0.7 × measured UPS-A runtime at measured load; every state transition bounded; fail-closed if unmet | SE11-AC-06, SE11-AC-14 |
| SE11-REQ-07 | Inventory identity scheme, record fields and configuration fingerprint (§10.1, §11.3) for every asset and cable | SE11-AC-10 |
| SE11-REQ-08 | Telemetry signals of §10.3 exported from first power-on | SE11-AC-09 |
| SE11-REQ-09 | Firmware/driver lifecycle per §10.4 with snapshot + verified backup precondition | SE11-AC-08, SE20 |
| SE11-REQ-10 | Electrical circuits A/B verified and, where needed, installed by a licensed electrician against §8.2 load figures; SE11 designs no electrical work | SE11-AC-06 sign-off reference |
| SE11-REQ-11 | Downstream documents cite this document id **with its status (PROVISIONAL in v2)**, the B-id + disposition + quantity status they rely on, and the §9 failure-domain ids | EL review |
| SE11-REQ-12 | Any substitution of a dispositioned item is recorded as a new SE11-DEC with technical reason and impact before use; silent substitution is prohibited | SE11-AC-10 |
| SE11-REQ-13 | Protection activation: no D-IRR dataset may exist unless `PL-T3` is active for its class; `PL-T2` permits D-BND/D-REB only (§6.3) | SE11-AC-07b, SE11-AC-10 |
| SE11-REQ-14 | Reservation mechanism: hypervisor processor reserve/limit/weight, static vs dynamic memory, per-virtual-disk IOPS controls, in-VM cgroup shares; admission rule of §5.2 | SE11-AC-03, SE11-AC-12 |

### 16.4 Risks

| Id | Risk | Likelihood / impact | Mitigation | Owner |
|---|---|---|---|---|
| SE11-RISK-01 | Single central host is the control-plane and data failure domain (FD-HOST, FD-NVME-M2_4) | Medium / High | SE11-REQ-05, T2/T3, hosted fallback (ADR-01), REV-HA | SE11, EL |
| SE11-RISK-02 | Non-ECC host memory → silent corruption in the Data VM | Low / High | SE11-AC-04 memory pass; database checksums and backup verification (SE12); ECC class substitute (ADR-03) | SE11, SE12 |
| SE11-RISK-03 | PCI_E3/M2_3 sharing reduces bandwidth or is mutually exclusive | Medium / Medium | SE11-AC-02; fallback mapping §6.1 | SE11 |
| SE11-RISK-04 | No out-of-band management; a hung host needs physical presence | High / Medium | Physical console; SE20 auto-restart policy; REV-HA if SLOs require | SE11, SE20 |
| SE11-RISK-05 | Support or availability of a BOM item has lapsed (BOM v2.2 is a point-in-time reference; nothing is established, §11.2) | **High** / Medium | SE11-AC-01 before any build; §11.4 classes; SE11-REQ-12 | SE11 |
| SE11-RISK-06 | Long RAID 6 rebuild at 20 TB exposes the array to a third failure | Low / High | RAID 6; T3; rebuild timing measured (AC-07a); hot-spare option | SE12, SE11 |
| SE11-RISK-07 | UPS-A runtime at measured load insufficient for the budget | Medium / High | Fail-closed §8.4 remedies; TRG-UPS-BATT | SE11, SE20 |
| SE11-RISK-08 | Seed status: Rev 1.1 "proposed" while v1.0 "remains authoritative" (§0); hardware baseline could change on approval | Low / Medium | Sign-off bound to sha and revision; change control per §151/§104 re-enters this document | SE11, PL |
| SE11-RISK-09 | Every required source and dependency was unavailable; reconciliation may change dispositions, NFRs or ADRs | **High** / Medium | All entries PROV; SE11-AC-11 gate; SE11-REQ-11 propagates provisional status | SE11, EL, PL |
| SE11-RISK-10 | Capacity candidates must be chosen before a traceable model exists; H.1/H.3 default (M-A, N-A) may be undersized for Stage 1 or the later expansion may fail stability re-validation | Medium / Medium | §5.3/§6.7 rules; TRG-MEM-EXPAND, TRG-NAS-CAP; SE11-DEC-03a/06a record basis; M-C/N-C hosted equivalents | SE11, SE01, SE12 |
| SE11-RISK-11 | No supported UPS signalling combination can be evidenced (S-1/S-2) | Medium / High | S-3 automatic fallback (two UPS, native USB each); no reliance before AC-06/14 | SE11 |

### 16.5 Assumptions (explicit, labelled; corpus silent)

| Id | Assumption | Resolution path |
|---|---|---|
| ASM-SE11-01 | PL-REQ-ID-REGISTER and fragments G01–G04 are absent; when present, their rows for §152–§177 and Appendices G/H map onto the citations here | SE11-AC-11; v3 adds register ids |
| ASM-SE11-02 | SEED-01 Rev 1.1 is the operative seed despite its "proposed" status note | PL confirms; SE11-RISK-08 |
| ASM-SE11-03 | Reservation envelopes in §4/§5.3 (floors, ceilings, host root need 2–4 LP) are hypothetical pre-measurement estimates derived from §156/§167 | Replaced by SE11-HARDWARE-CAPACITY-SIZING and measured p95 (§234) |
| ASM-SE11-04 | RAID 6 rebuild at 20 TB under concurrent load: 1–3 days; N-A usable capacity ≈ 36.4 TiB derived from the seed's 80 TB → 72.8 TiB ratio | Measured in SE11-AC-07a |
| ASM-SE11-05 | Device power envelopes in §8.2 are class estimates; the seed's ~560 W typical / 1,150–1,300 W peak remain the circuit-sizing figures | Measured in SE11-AC-06 |
| ASM-SE11-06 | SE11-NFR-01 … 08 values are engineering proposals; product NFRs (PM09) and EL NFR ids are unavailable | Bound or corrected in SE11-AC-11 |
| ASM-SE11-07 | FD-HOST recovery to degraded service ≤ 1 working day assumes a replacement host of the §11.4 class or hosted capacity is obtainable | SE20 spare/hosted readiness; SE19 resilience test |
| ASM-SE11-08 | Dataset classification D-IRR/D-BND/D-REB and examples (§6.2) are a provisional default pending SE12 | SE12 document replaces |

### 16.6 Conflicts

**Not assessable in this version; no consistency with upstream documents is asserted.** v1's statement "No approved upstream document contradicts this architecture" is withdrawn: no upstream product, EL, NT16 or SP16 document was available to check (§0.1). What SE11-AC-11 must check and where a conflict would be recorded: product NFR/acceptance targets vs SE11-NFR-01 … 08; EL runtime/deployment/reliability decisions vs ADR-01/02/05/09 and the pool model; EL contract governance vs §18.2; SE12 data policy vs §6.2–§6.3 defaults; NT16 external-dependency assessment vs FD-EXT-AI/FD-INTERNET residuals; SP16 guardrails vs gate G-LOCAL. Known internal tensions, recorded rather than hidden: (1) §6.1 deviates from the BOM's literal role labels — justified in SE11-DEC-09/ADR-09; (2) the seed's own "proposed" status — SE11-RISK-08/ASM-SE11-02.

## 17. Baseline sign-off record (QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

| Field | Value |
|---|---|
| Baseline id | SE11-HW-BASELINE-2-PROV |
| Bound to | SEED-01 Proposed Revision 1.1, Appendix G BOM v2.2, sections §74, §152–§177, §226–§238; file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| Configuration fingerprint | **None** — no evidenced configuration exists (SE11-AC-01 not performed, §11.2). The baseline is a set of dispositions by specification class plus capacity candidates, not a buildable bill |
| Dispositions | Per §1.2 tally: ADOPT ×2; ADOPT WITH ENGINEERING CONSTRAINT ×13; DEFER / OPTIONAL ×5; SUBSTITUTE ×0; ESCALATE ×0 (conditional REV-*); capacity candidates: B4 quantity (M-A/M-B/M-C), B14 count (N-A/N-B/N-C); signalling candidates S-1/S-2/S-3 |
| Status ladder | **PROVISIONAL** (this version) → RECONCILED (SE11-AC-11 passed: register ids attached, EL review recorded, conflicts resolved) → EVIDENCED (SE11-AC-01 passed: fingerprint v0 recorded) → VERIFIED (SE11-AC-02 … 14 evidence attached; SE11-AC-10 signed). Each step is recorded as a new version of this document and in the contract record (§18.2) |
| Verification state | **DISPOSITIONED — PROVISIONAL — NOT APPROVED FOR DOWNSTREAM IMPLEMENTATION.** Downstream documents may cite the dispositions, pool ids, failure-domain ids, NFR proposals and candidate rules as *provisional* (SE11-REQ-11); nothing may be built, ordered or treated as verified on this version |
| Provided contract | `SE11-CONTRACT-hardware-baseline@1` — **PROPOSED, defined in §18.2, not registered** |
| Sign-off | SE11 (author): architecture dispositions complete at PROVISIONAL status, pending SE11-AC-11 and SE11-AC-01. EL review: **not performed** (documents unavailable). SE01/SE12/SE17/SE19/SE20 inputs: requested (§18.3), none received |

## 18. Cross-domain dependencies and interface contracts

### 18.1 Dependencies by owning role

| Owning role (§74) | What is needed from / supplied to them | Artefact or contract | Needed by |
|---|---|---|---|
| EL | Reference this document (not duplicate) in system/runtime/deployment/reliability/estimate documents; bind services to pools (§4); review ADR-01 … 09; register the provided contract; accept FD-HOST/FD-EXT-AI residuals; include SE11-REQ-13 in Definition of Ready for data-bearing services | EL contract register; EL ADR record; EL DoR (all unavailable) | SE11-AC-11 |
| PL | Register ids for the cited seed sections | PL-REQ-ID-REGISTER (unavailable) | SE11-AC-11 |
| SE01 | Capacity model: F/C inputs for §5.3, queue-wait thresholds for TRG-WKR-LOCAL, replacement of ASM-SE11-03 | Requested contract (§18.3) | SE11-DEC-03a; Stage 1 end |
| SE12 | Dataset classification (replaces ASM-SE11-08), retention volume V for §6.7, binding RPO/RTO, backup schedule, T3 medium/provider policy, abrupt-loss integrity verification, key custody with SE17 | Requested contract (§18.3) | SE11-DEC-06a; SE11-AC-07a/b; SE11-AC-13 |
| SE14 | Portable naming/addressing conventions for pools and segments (no physical design) | Consultation | Stage 1 |
| SE15 / SE17 | Control ids for SE11-SECREQ-01 … 08; segmentation policy between `seg.*`; key custody; SE11-AC-08 evidence | Requested contract (§18.3) | Stage 1 (host/NAS), Stage 3 (full) |
| SE19 | Execute SE11-AC-04/05/12/13 and the §9 resilience tests | Requested contract (§18.3) | Stage 1–2 |
| SE20 | Telemetry integration (SE11-AC-09), maintenance windows, firmware execution, drills SE11-AC-06/13/14, inventory upkeep, admission checklist for SE11-REQ-13 | Requested contract (§18.3) | Stage 1 |
| SP16 | Economics input for gate G-LOCAL (ADR-01) | SP16 guardrails (unavailable) | Before any local provisioning decision |
| NT16 | External-provider and hosted-equivalent risk/SLA input for FD-EXT-AI, FD-INTERNET, N-C/M-C, T3 provider | NT16 assessments (unavailable) | Before T3 provider and hosted-equivalent decisions |
| SE11 (own) | SE11-HARDWARE-CAPACITY-SIZING (applies §5.3/§6.7 rules; records SE11-DEC-03a/06a) and SE11-POWER-COOLING-RACK (thermal, rack layout, PD details) | Sibling SE11 documents | Stage 1 |
| Qualified electrician | Circuits A/B verification and any installation (SE11-REQ-10) | Professional sign-off referenced from SE11-AC-06 | Before stable-runtime baseline |

### 18.2 Provided contract — definition of record (status PROPOSED)

`SE11-CONTRACT-hardware-baseline@1` · owner SE11 · **status: PROPOSED — defined by this section; not registered.** Registration requires SE11's Interface Contract document and EL's contract register (EL-INTERFAC-CONTRACT-GOVERNAN), neither of which is available; until registration the contract is cited as "proposed in SE11-PHYSICAL-INFRASTR-HARDWARE v2 §18.2". Content per asset: the §10.1 inventory fields; disposition, quantity status and candidate selected (§1.2, §5.3, §6.7); failure-domain ids (§9); pool ids and budgets (§4); volume mapping (§6.1); protection level `PL-*` (§6.3); signalling topology S-x (§8.3); baseline status (§17 ladder); evidence ids (§14); configuration fingerprint (§11.3). Compatibility rule: additive fields only within major version 1; any change to a disposition, mapping, budget rule or status ladder is a new major version. Consumers (EL runtime/deployment/reliability/estimate documents, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite this contract and the status they rely on; they never restate hardware facts.

### 18.3 Consumed interfaces — requested, none yet registered

No owner has published a contract id in this run (§0.1). SE11 therefore records each consumed interface as **REQUESTED**, names the owner and the expected naming pattern, and does not invent an id. Until the owner assigns the id, the dependency is **unmet** and the dependent SE11 decision stays PROV.

| Consumed interface (requested) | Owner | Expected id pattern (assigned by owner) | SE11 decision that depends on it |
|---|---|---|---|
| Capacity model inputs F/C and queue-wait thresholds | SE01 | `SE01-CONTRACT-<slug>@n` | SE11-DEC-03a, TRG-WKR-LOCAL |
| Dataset classification, retention volume V, binding RPO/RTO, T3 policy | SE12 | `SE12-CONTRACT-<slug>@n` | SE11-DEC-06a, SE11-REQ-13, SE11-NFR-05 |
| Security control ids for SE11-SECREQ-01 … 08; segmentation policy | SE17 (SE15 for identity/keys) | `SE17-CONTRACT-<slug>@n`, `SE15-CONTRACT-<slug>@n` | §13, SE11-AC-08 |
| Test execution and evidence format for SE11-AC-04/05/12/13 | SE19 | `SE19-CONTRACT-<slug>@n` | §14 |
| Telemetry ingestion, alerting, maintenance calendar, drill execution | SE20 | `SE20-CONTRACT-<slug>@n` | SE11-AC-06/09/14, §10.5 |
| NFR ids, ADR ids, contract register entry, DoR clause for SE11-REQ-13 | EL | EL register entries | §3, §16.1, §18.2 |

## 19. Criteria disposition

| Criterion | Disposition | Where / reason |
|---|---|---|
| OUT-…-AR-01 source baseline | Covered | §1.1 (Rev 1.1, BOM v2.2, sha), §1.2 (B1–B19 with class/quantity separation) |
| OUT-…-AR-02 scope and boundaries | Covered | §2 (physical network retained by SE11 per §74) |
| OUT-…-AR-03 workload allocation | Covered | §4 (pools, budgets, shared-budget membership) |
| OUT-…-AR-04 compute | Covered | §5 (normalised accounting, reservation mechanism, memory candidates and rule, GPU preconditions) |
| OUT-…-AR-05 storage | Covered | §6 (authoritative mapping, classes, protection rule, recovery split, NAS candidates) |
| OUT-…-AR-06 network | Covered | §7 |
| OUT-…-AR-07 power/placement | Covered | §8 (gated signalling, state machine, budget, fail-closed) |
| OUT-…-AR-08 failure domains | Covered | §9 (FD-CIRCUIT-A vs FD-UPS-A; owners, targets, residuals) |
| OUT-…-AR-09 manageability | Covered | §10 |
| OUT-…-AR-10 compatibility/availability assessment | Covered | §11 — the assessment is performed and its result is "not established" for support/availability; structural checks and alternatives by class recorded |
| OUT-…-AR-11 security | Covered | §13 (SE11-SECREQ-nn) |
| OUT-…-AR-12 expansion | Covered | §12 |
| OUT-…-AR-13 risks/ADRs | Covered | §16 |
| OUT-…-AR-14 validation plan | Covered | §14 |
| QC-…-AR-01 exact source version; every item dispositioned | Covered | §1.1, §1.2 (status PROVISIONAL) |
| QC-…-AR-02 one coherent physical architecture | Covered | §2.3, §4–§10 cross-referenced by pool, device, segment, power-domain, failure-domain and protection-level ids |
| QC-…-AR-03 compatibility and availability checked sufficiently | **not_applicable (recorded as UNMET)** — the allowed corpus cannot establish current support, compatibility or availability for any item (§11.2); the criterion is reported as unmet, every item stays a conditional candidate, and the baseline is PROVISIONAL with no fingerprint; closure requires SE11-AC-01 | §11.2–§11.3, §17 |
| QC-…-AR-04 no hidden SPOF, capacity limit or dependency | Covered | §9 (incl. FD-NVME-M2_1/M2_4, FD-UPS-A, FD-SIGNAL, FD-MGMT), §12.1 hard ceilings, §12.3, §16.4 |
| QC-…-AR-05 substitution rules preserve assumptions | Covered | §11.4 classes; SE11-REQ-12; §12.3 ESCALATE boundaries; §8.4 ordered remedies |
| QC-…-AR-06 validation evidence and affected owners explicit | Covered | §14 (owner and gate per AC), §18 (owners, requested contracts) |
| QC-…-AR-07 sign-off against the exact baseline consumed downstream | Covered | §17 (provisional sign-off bound to seed sha; status ladder; no fingerprint claimed) |
| BND-01 … BND-04 | Covered (excluded as required) | §15 |

Required source PL-REQ-ID-REGISTER: reported `not_applicable` in the event for the mechanical reason in §0.3; substantive disposition **UNAVAILABLE SOURCE / LIMITATION** (§0.1), closure by SE11-AC-11.
