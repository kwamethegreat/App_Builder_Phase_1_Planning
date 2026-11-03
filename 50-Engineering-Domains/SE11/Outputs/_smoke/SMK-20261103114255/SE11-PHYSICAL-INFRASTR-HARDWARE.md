---
id: SE11-PHYSICAL-INFRASTR-HARDWARE
version: 1
status: complete
owner: SE11
based_on: [SEED-01]
requirements: [SE11-REQ-01, SE11-REQ-02, SE11-REQ-03, SE11-REQ-04, SE11-REQ-05, SE11-REQ-06, SE11-REQ-07, SE11-REQ-08, SE11-REQ-09, SE11-REQ-10, SE11-REQ-11, SE11-REQ-12, SE11-DEC-01, SE11-DEC-02, SE11-DEC-03, SE11-DEC-04, SE11-DEC-05, SE11-DEC-06, SE11-DEC-07, SE11-DEC-08, SE11-ADR-01, SE11-ADR-02, SE11-ADR-03, SE11-ADR-04, SE11-ADR-05, SE11-ADR-06, SE11-ADR-07, SE11-RISK-01, SE11-RISK-02, SE11-RISK-03, SE11-RISK-04, SE11-RISK-05, SE11-RISK-06, SE11-RISK-07, SE11-RISK-08, SE11-AC-01, SE11-AC-02, SE11-AC-03, SE11-AC-04, SE11-AC-05, SE11-AC-06, SE11-AC-07, SE11-AC-08, SE11-AC-09, SE11-AC-10, ASM-SE11-01, ASM-SE11-02, ASM-SE11-03, ASM-SE11-04, ASM-SE11-05]
---

# Physical Infrastructure and Hardware Architecture

**Document id:** SE11-PHYSICAL-INFRASTR-HARDWARE v1 · **Owner:** SE11 (Physical Infrastructure & Hardware) · **Stage:** 0 · **Run:** SMK-20261103114255

**Purpose.** This is the single engineering disposition of the Master Product Vision hardware strategy and BOM. It turns the seed's reference configuration into one coherent physical architecture (compute, storage, network, power/placement, management, failure domains), records every BOM item's disposition, and defines the validation evidence that downstream owners (EL, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) rely on by citing this document id and the disposition they consume. It does not select vendors, price, or purchase (see §15 Exclusions).

**Source baseline (hardware planning chain, ENV-DEC-017).** SEED-01 "CSPUI — Master Product Vision & Operating Architecture — Proposed Revision 1.1, Expanded 2026 Baseline" (repository sha `2d3a171d6961a8790f5a9812eeb1e3907f188242`), hardware strategy sections §152–§177 (document sections 37–45) and the BOM "Appendix G. Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (§226 status note, §227 G.1, §228 G.2, §229 G.3, §230 G.4, §231 G.5) plus Appendix H guardrails (§232–§238). No BOM content is recreated from memory; every specification cited below is taken from those sections.

**Required source disposition — PL-REQ-ID-REGISTER: not_applicable.** The Master Requirement ID Register (`10-Product-Lead/PL/Outputs/PL-REQ-ID-REGISTER.md`) and its fragments PL-REQ-REGISTER-G01..G04 are not present in the repository at authoring time (`read_document` returned `not_found` for all five paths); SEED-01 is therefore consumed directly for every hardware fact, as the hardware chain rule allows for SE11, and register-id reconciliation is recorded as ASM-SE11-01 (see §16).

## 1. Authoritative source baseline (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01)

### 1.1 Exact version and sections consumed

| Item | Value |
|---|---|
| Seed | SEED-01, Proposed Revision 1.1, "Expanded 2026 Baseline — Greenfield, Opportunity Intelligence, 19-Gap & Infrastructure Edition" (§0) |
| BOM version | Appendix G "Reference Greenfield Infrastructure BOM — Optional Baseline (v2.2)" (§226 status note; items §227–§231) |
| Strategy sections | §152–§154 (37.x four-stage/shared-hardware), §156–§157 (38.x environments, resource reservation), §158–§160 (39.x no-wait/no-overbuild, capacity thresholds, portability, section 40 reference configuration table), §161–§163 (40.x central node, memory, NVMe), §164–§166 (41.x NAS, UPS/electrical, rack/network), §167–§168 (42.x VMs + containers), §169–§171 (43.x worker pool), §172–§175 (44.x redundancy, quorum, resource classes, graceful degradation), §176–§177 (45.x GPU) |
| Guardrails | Appendix H §232–§238 (H.1–H.7) |
| Approval status | §0: "The approved v1.0 document remains authoritative until this revision is explicitly approved." The hardware baseline exists only in Rev 1.1; this document treats Rev 1.1 as the operator-supplied Stage-0 seed (ASM-SE11-02) and binds its sign-off to that exact revision and sha (§17). |

### 1.2 Classification of every BOM entry

The seed itself states that Appendix G "is a greenfield reference configuration, not an assertion of already-owned equipment or a mandatory topology" and that Product/Engineering "may procure, substitute, resize, or use hosted equivalents when evidence shows equal or better capability, reliability, portability, security, schedule, and economics" (§226). Classification therefore separates what is fixed by the vision from what is a preferred target, optional, or subject to engineering validation.

| # | BOM entry (seed section) | Seed class | Engineering disposition (SE11 only) | Decision ref |
|---|---|---|---|---|
| B1 | CPU — AMD Ryzen 9 9950X, 16C/32T, AM5, 24 PCIe 5.0 lanes, 170 W TDP / ~230 W package (§227.1) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — virtualization extensions (SVM/IOMMU) enabled; 230 W package limit is the compute line in the power budget (§8) | SE11-DEC-01 |
| B2 | CPU cooler — Thermalright Phantom Spirit 120 EVO, 157 mm (§227.2) | Preferred target | ADOPT — 157 mm < ~166 mm chassis clearance (§227.8) | — |
| B3 | Motherboard — MSI MAG X870 Tomahawk WiFi, 4×DDR5 to 256 GB, PCI_E1 Gen5 x16, PCI_E2 Gen3 x1, PCI_E3 Gen4 x4 (shares with M2_3), 4×M.2, 5 GbE, Wi-Fi 7/BT 5.4, 2×USB4 (§227.3) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — lane-sharing map validated before baseline (SE11-AC-02); Wi-Fi/Bluetooth disabled in the server role; no out-of-band controller, so management path is defined in §10 | SE11-DEC-02 |
| B4 | Memory — G.Skill Flare X5 4×64 GB DDR5-6000 CL36 EXPO, non-ECC (§227.4; §162) | Preferred target, "evidence-driven sizing decision, not a fixed prerequisite" (§162) | ADOPT WITH ENGINEERING CONSTRAINT — 256 GB justified by the concurrent-environment reservation plan in §5.2 (lower bound 192 GB) and by the single-matched-kit rule; EXPO only after stability pass, fallback 5600/5200 as the seed directs; non-ECC risk accepted and monitored (SE11-RISK-02) | SE11-DEC-03, SE11-ADR-03 |
| B5 | 2× WD_BLACK SN850X 1 TB, PCIe 4.0 x4, 600 TBW; roles system (M2_1), scratch (M2_3) (§227.5) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — M2_3 is a Gen4 x2 chipset slot shared with PCI_E3; scratch runs at x2 (acceptable for cache/scratch) subject to SE11-AC-02 | SE11-DEC-02 |
| B6 | 2× WD_BLACK SN850X 4 TB, PCIe 4.0 x4, 2,400 TBW; roles platform data/DBs/containers (M2_4), VM & artifact store (M2_2) (§227.6; §163) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — two independent volumes, no host RAID; durability comes from NAS snapshots/backup, "local NVMe is never the sole copy of important data" (§163) | SE11-ADR-05 |
| B7 | PSU — Corsair RM750e 750 W ATX 3.1, native 12V-2x6 (§227.7) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — adequate for the no-GPU build and for the 145 W optional GPU only after the measured power-budget check the seed requires (§227.11, §160 table); any accelerator class above 145 W or a second accelerator is ESCALATE ARCHITECTURE IMPACT (§12.3) | SE11-DEC-04 |
| B8 | Case — Fractal Design Meshify 3 Black Solid, mid-tower ATX/E-ATX, ~166 mm cooler clearance (§227.8) | Preferred target | ADOPT — clearance and ATX form factor verified against B2/B3; GPU length 241 mm is validated in SE11-AC-02 before any GPU adoption | — |
| B9 | OS — Windows 11 Pro retail (§227.9; §166) | Fixed constraint (operating model §166: "Windows host + Hyper-V Linux VMs + Docker containers for durable services") | ADOPT WITH ENGINEERING CONSTRAINT — Hyper-V role enabled; persistent platform services run only in Linux VMs, never solely in WSL2 (§166); host disk encryption required (§13) | SE11-ADR-02 |
| B10 | 10 GbE NIC — ASUS XG-C100C V2, 10GBase-T, PCIe 3.0 x4, installed in PCI_E3 (§227.10) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — shares chipset lanes with M2_3 (B5); Hyper-V virtual-switch driver support is a baseline check (SE11-AC-03); specification-class alternative recorded in §11 | SE11-DEC-02 |
| B11 | GPU (optional) — NVIDIA RTX PRO 4000 Blackwell 24 GB, 145 W, single-slot, 241 mm, PCIe 5.0 x16 (§227.11; §175–§177) | Optional ("optional at initial acquisition", §175; "driven by measured demand and economics", §177) | DEFER / OPTIONAL — adoption triggers and preconditions in §5.4 and §12 | SE11-ADR-04 |
| B12 | NAS — Asustor Lockerstor 8 Gen3 AS6808T, 8 bays, Ryzen Embedded V3C14, 16 GB DDR5 ECC stock, 2×10GbE + 2×5GbE, 4×M.2, Btrfs snapshots, per-folder AES-256, UPS/network-UPS support (§228.1; §164) | Preferred target; role fixed by §164 ("durable backup/storage tier, not a substitute for central NVMe latency") | ADOPT WITH ENGINEERING CONSTRAINT — durable/backup tier only; admin interface on the management segment; firmware lifecycle per §10 | SE11-ADR-05 |
| B13 | NAS memory — Kingston Server Premier 32 GB DDR5-4800 ECC SO-DIMM → 48 GB total (§228.2) | Preferred target | DEFER / OPTIONAL — stock 16 GB ECC serves the backup/snapshot role; install when NAS memory telemetry shows sustained pressure (trigger in §12.2) | SE11-DEC-05 |
| B14 | NAS drives — 6× Toshiba MG10 20 TB CMR enterprise, RAID 6 → 80 TB nominal / ~72.8 TiB usable, 2 bays free (§228.3; §164) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — RAID 6 (dual parity) is mandatory at this drive capacity; retention policy input comes from SE12; a 4-drive RAID 6 start is the recorded smaller alternative (§6.5) | SE11-DEC-06 |
| B15 | UPS (PC + NAS) — CyberPower CP1500PFCLCD 1500 VA / 1000 W pure sine, USB HID, PowerPanel / NAS UPS service (§229.1; §165) | Preferred target | ADOPT WITH ENGINEERING CONSTRAINT — load ≤ 1000 W verified by measurement (SE11-AC-06); shutdown topology SE11-DEC-07 | SE11-DEC-07 |
| B16 | UPS (rack) — second unit ~1000 VA / 600 W pure sine, model TBD (§229.2; §165) | Candidate subject to validation ("when used") | DEFER / OPTIONAL — required only when a local worker rack exists; specification class in §11 | SE11-DEC-08 |
| B17 | Rack — 18U, 1U 24-port switch with ≥2×10GbE, 1U PDU, worker trays sized to measured need, 1U power-brick shelf, modest headroom (§230; §166) | Candidate subject to validation ("If local rack infrastructure is selected", §166; "no fixed initial worker count", §230) | Switch: ADOPT WITH ENGINEERING CONSTRAINT (managed, VLAN-capable, ≥2×10GbE minimum per seed, ≥4×10GbE preferred; §7). Rack, PDU, trays, shelf: DEFER / OPTIONAL until the local-worker trigger in §12.2 | SE11-DEC-08, SE11-ADR-07 |
| B18 | Electrical — two separate 15 A breakers (PC+NAS UPS on one, rack UPS on the other), UPS plugged directly into wall, dedicated 20 A optional; typical ~560 W, sustained peak ~1,150–1,300 W (§231; §165) | Fixed constraint (code-regulated) | ADOPT WITH ENGINEERING CONSTRAINT — stated as a requirement for qualified professionals (SE11-REQ-10); not designed here | SE11-REQ-10 |
| B19 | Local worker nodes (form factor and count unspecified; elastic pool may be local, hosted, cloud or hybrid, §168–§171) | Optional / evidence-sized | DEFER / OPTIONAL — hosted/cloud executors first; local worker class adopted on the queueing/utilization trigger in §12.2 | SE11-ADR-01 |

No item is dispositioned SUBSTITUTE in this version; every substitution rule that would apply if an item fails availability or compatibility validation is recorded by specification class in §11, and any future substitution is logged as a new SE11-DEC entry with reason and impact (SE11-REQ-12).

## 2. Physical architecture scope and boundaries (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-02)

### 2.1 In scope (owned by SE11)

| Element | Content of this document |
|---|---|
| Local central compute | One central node (B1–B10) as the reference configuration; its host role, slot/lane allocation, reservation constraints (§5) |
| Worker nodes | Capability classes and placement rules for local workers if and when adopted (§4, §12); physical provisioning (trays, power, ports) when triggered |
| GPU / accelerator class | Single-slot, ≤145 W, PCIe x16 class; deferred (§5.4) |
| Storage / NAS | Hot NVMe tiers on the host and the durable NAS tier (§6) |
| Network switching / NICs | 10 GbE storage/core path, 5 GbE host onboard, switch class, segmentation (§7) |
| Rack / placement | 18U rack class, desk/room placement constraints (§8) |
| UPS / power distribution | Two power domains, UPS roles, shutdown dependencies (§8) |
| Cabling | Cat6a for 10GBase-T paths; labelled per inventory id (§10) |
| Out-of-band / management | Management path given the absence of a BMC on the consumer-class board (§10) |

### 2.2 Out of scope (owned elsewhere; referenced, not included)

| Concern | Owner | How this document relates |
|---|---|---|
| Purchase orders, pricing, vendor scorecards, procurement workflow | nobody (excluded by chain rule) | §15 Exclusions |
| Facilities: electrical circuit design, breaker work, code compliance | Qualified electrical professionals | SE11-REQ-10 states the requirement only |
| System architecture, deployment topology | EL | EL cross-references this document instead of duplicating it |
| Capacity model and growth thresholds | SE01 (capacity); SE11-HARDWARE-CAPACITY-SIZING (SE11) | Sizing ranges here are inputs; the sizing document carries the model |
| Storage/data policy: retention, backup schedule, RPO/RTO, encryption key management | SE12 (data), SE17 (security) | §6 states hardware-capable targets as requirements to those owners |
| Network/integration design beyond physical ports and segments | SE14 | §7 states physical constraints and segment names |
| Infrastructure security controls | SE17 | §13 names the control slugs SE11 relies on; SE17 owns their ids |
| Performance/resilience validation execution | SE19 | §14 lists the tests; SE19 executes and reports evidence |
| Operations, monitoring, maintenance windows | SE20 | §10 states telemetry and window requirements |
| Software/container/service design | existing SE11 artefacts and EL | BND-03: not restated here |

### 2.3 Context view (text)

```mermaid
flowchart LR
  subgraph PD_A[Power domain A: UPS-A CP1500PFCLCD on circuit A]
    HOST[Central host: Win11 Pro + Hyper-V\nLinux VMs: Core / Data / Build-CI / Validation-Staging\nNVMe M2_1 sys, M2_3 scratch, M2_2 VM+artifact, M2_4 platform data]
    NAS[NAS AS6808T: RAID6 6x20TB\nsnapshots, backups, evidence, archives]
    SW[Managed switch: >=2x10GbE (>=4 preferred) + 1/2.5GbE access]
  end
  subgraph PD_B[Power domain B: rack UPS-B on circuit B — DEFERRED]
    RACK[18U rack: PDU, worker trays — DEFERRED]
    WK[Local workers — DEFERRED]
  end
  HOST -- 10GbE storage/backup path --> SW
  NAS -- 10GbE --> SW
  HOST -- 5GbE onboard: management + upstream --> SW
  SW -- uplink --> GW[Upstream gateway / internet]
  GW --> EXT[External AI providers, hosted runners, cloud workers]
  WK -. 1/2.5GbE worker links .-> SW
  UPS_A[UPS-A USB-HID] -- shutdown signal --> NAS
  NAS -- network UPS server --> HOST
```
