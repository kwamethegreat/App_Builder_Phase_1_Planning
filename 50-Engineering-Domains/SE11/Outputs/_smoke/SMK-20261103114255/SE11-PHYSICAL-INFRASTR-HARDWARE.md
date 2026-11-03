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

## 3. Stakeholders, concerns and quality attributes (ISO/IEC/IEEE 42010 framing)

| Stakeholder | Concern | Quality attribute (ISO/IEC 25010) | Measured by |
|---|---|---|---|
| EL | One coherent physical architecture to reference | Compatibility, maintainability | §4–§10 relationships; sign-off record §17 |
| SE01 | Capacity inputs are ranges with assumptions | Capacity | §5.2, §6.5, §12 |
| SE12 | Durable tier, RAID/replication boundaries, recovery expectations | Reliability (recoverability), fault tolerance | §6.3–§6.4, SE11-AC-07 |
| SE14 | Physical ports, speeds, segments | Performance efficiency | §7, SE11-AC-05 |
| SE17 | Trusted boot, management isolation, encryption support | Security (confidentiality, integrity) | §13, SE11-AC-08 |
| SE19 | Burn-in, performance and resilience test surface | Reliability (maturity) | §14 |
| SE20 | Inventory identity, telemetry, maintenance windows | Maintainability (analysability) | §10 |
| VP / platform operator (via PL) | Provision only justified capacity; portability; no temporary architecture (§158, §160, §233, §238) | Portability, cost | §1.2 dispositions, §12 triggers |

Non-functional targets this document introduces (to be bound to NFR ids by EL/SE19): SE11-REQ-01 reservation protection (§5.2), SE11-REQ-04 storage-path bandwidth (§7.2), SE11-REQ-06 safe-shutdown time budget (§8.3), SE11-REQ-08 telemetry coverage (§10.3).

## 4. Workload-to-hardware allocation (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-03)

Allocation maps workload classes to **resource pools**, never to named devices; a pool is addressed by a logical name in configuration (§160: no hard-coded host names, local paths or addresses). Pools are the unit that moves between local, hosted and customer infrastructure (§168).

| Workload class (seed §167, §169–§171, §174) | Resource pool | Physical backing in the reference configuration | Priority class (§174) | Placement rule |
|---|---|---|---|---|
| Platform core: orchestration, APIs, queues, registry/control | `pool.core` | Linux VM "Platform Core" on host NVMe M2_4 | Highest (stable runtime) | Reserved CPU/memory; never co-scheduled with destructive tests |
| Data: databases, search/knowledge data, caches | `pool.data` | Linux VM "Data" on M2_4; backups/snapshots to NAS | Highest | Memory/IO-sensitive; largest reserved memory share |
| Build/CI: runners, build cache, artifact generation | `pool.build` | Linux VM "Build/CI" on M2_2 (VM disk) with scratch on M2_3; bursts into hosted runners | Medium | Burst into unreserved capacity; back-pressure on queue |
| Validation/staging: integration, security validation, staging, release challenger, VP validation | `pool.validate` | Linux VM "Validation/Staging" on M2_2; fault-injection targets only inside this VM | High | Preempts batch work near stage gates; destructive tests restricted here (§156) |
| Agent execution (API-based model workers) | `pool.agents` | Elastic workers: hosted/cloud executors first; local worker class when triggered (§12.2); may run as containers inside `pool.build` while small | Medium | Disposable, idempotent, capability-matched (§170) |
| Test/browser/scanning workers, synthetic users | `pool.test` | Elastic workers as above | Medium / lowest | Disposable; results persisted to NAS evidence store |
| Local AI inference, embeddings, vision, evaluation (§176) | `pool.gpu` | Deferred: host PCI_E1 GPU when adopted (§5.4); external providers meanwhile (§160, §175) | Medium | Only via the same AI-dependency governance as external models (§177) |
| Stable runtime of accepted stage baselines | `pool.runtime` | Same VMs as `pool.core`/`pool.data` with separate namespaces/projects, credentials, networks, data paths (§156) | Highest | Protected from build/test changes by VM boundary (§168) |
| Durable storage: backups, snapshots, release evidence, VM/container archives, repositories/mirrors | `pool.durable` | NAS RAID 6 volume; independent/off-site copy as program matures (§164) | n/a | Never the hot working set (§164) |
| Background analysis, documentation, low-priority optimisation | `pool.background` | Any unreserved capacity, host or workers | Lowest | Yields to all other classes; first to be shed on degradation (§175) |
| Operator/admin interactive work | `pool.admin` | Windows host + WSL2 Ubuntu + Docker Desktop (§167) | n/a | Convenience only; nothing persistent depends on WSL2 (§166) |

Rule SE11-REQ-01: every pool has a declared reservation (floor) and a burst ceiling; `pool.core`, `pool.data` and `pool.runtime` reservations are hard (never oversubscribed); all other pools share the remainder with oversubscription permitted (§157). EL's deployment documents bind services to pools; SE01's capacity model sizes pool floors from the telemetry in §10.3.

## 5. Compute architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-04)

### 5.1 Host-role requirements

| Requirement | Specification | Source |
|---|---|---|
| CPU | 16 physical cores / 32 threads, homogeneous cores, ≥64 MB L3, hardware virtualization + IOMMU enabled in firmware | B1 (§227.1); needed for Hyper-V VM isolation (§168) |
| Memory | 256 GB DDR5 installed as one matched 4-DIMM kit; EXPO profile only after stability pass; fallback DDR5-5600/5200 | B4 (§227.4), §162 |
| PCIe / slots | PCI_E1 Gen5 x16 reserved for the deferred accelerator; PCI_E3 Gen4 x4 carries the 10GbE NIC; PCI_E2 Gen3 x1 unused (insufficient for 10GbE); USB4 ×2 free for emergency storage/console | B3 (§227.3) |
| Local NVMe (4 slots, all populated) | M2_1 Gen5 x4 (CPU): 1 TB system — Windows + WSL2; M2_2 Gen5 x4 (CPU, shares with USB4): 4 TB VM disks + artifact store; M2_3 Gen4 x2 (chipset, shares with PCI_E3): 1 TB build cache/scratch; M2_4 Gen4 x4 (chipset): 4 TB platform data/DBs/containers; total 10 TB | B5, B6 (§227.5–§227.6), §163 |
| Host OS / hypervisor | Windows 11 Pro with Hyper-V; Linux VMs for all durable services; WSL2 + Docker Desktop for interactive work only | B9 (§227.9), §166–§168 |
| Firmware baseline | UEFI with Secure Boot and TPM 2.0 enabled (Windows 11 Pro prerequisite; verified in SE11-AC-01); Wi-Fi 7 / Bluetooth disabled | §13 |
| Thermal | Dual-tower air cooling 157 mm in a mesh-front mid-tower with three 140 mm intake fans; sustained 230 W CPU package + 145 W optional GPU envelope validated by burn-in (SE11-AC-04) | B2, B8 |

### 5.2 Resource-reservation constraints (ranges with assumptions; SE01 and SE11-HARDWARE-CAPACITY-SIZING refine from measurement)

| Pool / VM | vCPU reservation (floor) | vCPU ceiling | Memory floor (GB) | Memory ceiling (GB) | Assumption |
|---|---|---|---|---|---|
| Windows host + Hyper-V + WSL2/Docker Desktop | 2 physical cores | 4 | 16 | 32 | WSL2 memory capped by `.wslconfig`; host never swaps |
| Platform Core VM | 4 | 8 | 24 | 32 | Orchestrator, APIs, queues, registry |
| Data VM | 4 | 8 | 48 | 64 | Databases + search/knowledge data + caches (§167) |
| Build/CI VM | 4 (burst 12–16) | 24 (oversubscribed) | 32 | 64 | Parallel builds burst into unreserved cores |
| Validation/Staging VM | 4 | 12 | 32 | 48 | Production-like replica incl. challenger |
| Unreserved burst / local containers for agents, tests | remainder | — | remainder | — | Shed first on degradation (§175) |
| **Totals (floor)** | 18 of 32 threads reserved as floors | — | **152 GB floors; 192–240 GB at typical ceilings** | ≤ 256 GB | 256 GB leaves 16–64 GB headroom at ceiling; the 192 GB lower bound is the sizing justification in SE11-DEC-03 |

Assumptions: ASM-SE11-03 — no measured workload exists at Stage 0; the floors above come from the five required logical environments in §156 and the layout in §167, and must be replaced by measured p95 values after the first stage's telemetry (§234 H.3). Memory ceilings never exceed physical memory; the hypervisor must not be configured for dynamic over-commit of the Highest-priority pools (SE11-REQ-01).

### 5.3 Virtualization/host implications

- VM count and boundaries remain an engineering decision (§167); the four Linux VMs above are the minimum that satisfies the isolation rule of §156 (separate namespaces, credentials, networks, data paths, secrets, pipelines, budgets). Merging Core and Data into one VM is permitted only if memory floors are preserved and SE17 accepts the shared blast radius.
- VM disks live on M2_2; databases and container layers on M2_4, so that a build-cache or VM-disk saturation on one device cannot starve database IO on the other (SE11-REQ-02: no two Highest-priority pools share a single NVMe device with a Medium-priority pool).
- Snapshots of the Validation/Staging and Core VMs are taken before any firmware/driver change (§10.4) and replicated to `pool.durable`.
- Nothing in the VM layer may encode physical slot ids, device serials, or the host name; portability requirement §160 applies to every VM definition.

### 5.4 Accelerator (deferred) preconditions

The GPU (B11) stays DEFER / OPTIONAL until all of the following hold: (a) a measured trigger from §12.2 (local-inference latency/privacy/cost case or GPU-required application testing, §176); (b) SE11-AC-02 confirms PCI_E1 x16 availability, 241 mm single-slot clearance and the 12V-2x6 cable; (c) SE11-AC-06 confirms the measured full-load system draw plus 145 W stays ≤ 80 % of the 750 W PSU rating; (d) SE11-AC-03 confirms a supported path to expose the GPU to a Linux VM on client Hyper-V (device assignment or partitioning) — if no supported path exists, the fallback is a host-level local-model service exposed to VMs over the internal virtual network, recorded as an SE11-DEC entry; (e) local models are registered under the same AI-dependency governance as external models (§177). Any accelerator above 145 W, a second accelerator, or a dual-slot card is ESCALATE ARCHITECTURE IMPACT because it exceeds the PSU, slot and thermal envelope of the reference configuration (SE11-ADR-04).

## 6. Storage architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-05)

### 6.1 Tiers and roles

| Tier | Device(s) | Role (seed) | Durability boundary | Owner of policy |
|---|---|---|---|---|
| T0 system | M2_1 SN850X 1 TB | Windows + WSL2 (§227.5) | Rebuildable from version-controlled configuration; no unique data | SE20 (host build), SE17 (encryption) |
| T0 scratch | M2_3 SN850X 1 TB (Gen4 x2 link) | Build cache / scratch (§227.5) | Disposable; loss costs rebuild time only | SE11 |
| T1 hot VM/artifact | M2_2 SN850X 4 TB | VM disks + active artifact store (§227.6) | Independent volume; snapshot + nightly replication to T2 | SE12 (artifact retention), EL (VM definitions) |
| T1 hot data | M2_4 SN850X 4 TB | Platform data, databases, container layers (§227.6, §163) | Independent volume; database-consistent backups to T2 | SE12 |
| T2 durable | NAS RAID 6, 6×20 TB, ~72.8 TiB usable | Backups, snapshots, release evidence, VM/container archives, historical artifacts, repositories/mirrors, platform/application backups (§164) | Dual-parity array + Btrfs snapshots; not a substitute for NVMe latency (§164) | SE12 |
| T3 isolated copy | Off-site / immutable copy, provider or medium selected by SE12 | "Truly irreplaceable data should have an independent/off-site or otherwise isolated copy as the program matures" (§164) | Independent failure domain from the room, UPS, NAS and host | SE12 (policy), SE17 (encryption/keys) |

SE11-REQ-03: T0/T1 NVMe is never the sole copy of release evidence, repositories, platform databases or VM definitions (§163, §177 acceptance list); every T1 dataset has a T2 copy and every irreplaceable dataset has a T3 copy.

### 6.2 Bandwidth / IOPS / latency assumptions (device class figures from the BOM; measured values replace them in SE11-AC-04)

| Path | Nominal from BOM | Engineering assumption used for design |
|---|---|---|
| M2_1, M2_2, M2_4 (Gen4 x4 devices) | up to 7,300 / 6,300 MB/s read/write (§227.5–§227.6) | Sustained mixed workload 2–4 GB/s per device; sub-millisecond latency; sufficient that NVMe is not the first bottleneck |
| M2_3 (Gen4 x2 slot, shared with PCI_E3) | device 7,300 MB/s; slot ≈ half of x4 | ≈ 3–3.5 GB/s ceiling; acceptable for build cache; verified in SE11-AC-02/04 |
| Host ↔ NAS over 10GbE | 10 Gb/s link ≈ 1.1–1.2 GB/s wire | 0.7–1.0 GB/s sustained for backup/artifact transfer; 6-drive RAID 6 CMR array is expected to deliver on the order of 0.5–1.0 GB/s sequential and far lower random IOPS — the NAS is therefore never used for random-IO workloads (§164) |
| Endurance | 600 TBW (1 TB), 2,400 TBW (4 TB) (§227.5–§227.6) | Scratch drive (M2_3) is the first to exhaust TBW; TBW consumption telemetry is mandatory (§10.3); replacement by specification class in §11 |

### 6.3 RAID / replication boundaries

- Host NVMe: no RAID. Independence of M2_2 and M2_4 is the only host-level isolation; redundancy is by replication to T2, not by mirroring (SE11-ADR-05). Rationale: host-side mirroring would double NVMe cost for a tier whose durability requirement is met by snapshot + replication, and would not protect against host loss, which is the dominant failure domain (§9).
- NAS: RAID 6 across six drives, two bays free (§228.3). RAID 6 (not RAID 5) is mandatory at 20 TB drive size because a rebuild at this capacity runs for an extended window (planning assumption 1–3 days under concurrent load, ASM-SE11-04) during which a second drive loss must still be tolerated. "RAID provides drive-failure resilience but is not the only backup" (§164): Btrfs snapshots guard against logical corruption; T3 guards against array, enclosure, power or site loss.
- Replication direction is one-way T1 → T2 → T3; T2 never serves as a live datastore for VMs or databases (prevents the NAS becoming a hot-path single point of failure).

### 6.4 Recovery expectations (hardware-capable targets stated to SE12; SE12 sets the binding RPO/RTO)

| Scenario | Hardware-capable target | Dependency |
|---|---|---|
| Single NVMe failure (T1) | Restore VM/data from last T2 snapshot/backup within hours; data loss bounded by replication interval (hardware supports hourly snapshots and nightly full replication) | Spare NVMe of equivalent class (§11); SE12 schedule |
| Single NAS drive failure | No data loss; array degraded; rebuild window ASM-SE11-04; replacement drive of equivalent class inserted into a free bay or the failed bay | 2 free bays allow hot-spare adoption as an SE12 decision |
| Two concurrent NAS drive failures | No data loss (RAID 6); third failure before rebuild completes = array loss → restore from T3 | T3 copy existence (SE11-REQ-03) |
| Host loss (board/CPU/PSU) | Rebuild host from version-controlled definitions; VMs restored from T2 archives onto replacement host or hosted equivalent (§160, §168) | Hardware-independent VM/container definitions (SE11-REQ-05) |
| NAS enclosure loss | Restore durable data from T3; T1 continues operating without backup until NAS is replaced (degraded mode, time-boxed by SE12) | T3 |

### 6.5 Capacity headroom

| Tier | Installed | Headroom rule | Expansion path |
|---|---|---|---|
| T1 (M2_2 + M2_4) | 2 × 4 TB | Alert at 70 % used, architecture review at 85 % (§12.3) | No free M.2 slots: expansion = larger-capacity devices of the same class (scale-up) or moving artifact store to T2-fronted cache; recorded trigger |
| T2 NAS | ~72.8 TiB usable | Alert at 70 %, review at 80 % | 2 free bays (RAID 6 expansion) + 4× M.2 slots for cache/metadata; the recorded smaller alternative is a 4-drive RAID 6 start (~36 TiB usable) with the remaining two drives added when SE12's retention model demands it — chosen only if SE12's Stage-1 retention volume is < 15 TiB (SE11-DEC-06) |
| T3 | n/a | Must hold at least the irreplaceable subset defined by SE12 | Provider/medium selection by SE12 |

## 7. Network architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-06)

### 7.1 Physical links and roles

| Link | Speed / media | Endpoints | Role |
|---|---|---|---|
| L1 storage/core | 10GBase-T, Cat6a | Host NIC (PCI_E3) ↔ switch ↔ NAS 10GbE port 1 | Backup, artifact, database-dump, VM-archive transfers; "network capacity appropriate to measured artifact, backup, database, and build traffic" (§166) |
| L2 management/upstream | 5 GbE onboard, Cat6a | Host onboard LAN ↔ switch | Host/VM management, upstream gateway, internet/external-provider traffic |
| L3 NAS secondary | 10GbE port 2 (spare), 2×5GbE | NAS ↔ switch | Expansion: second 10GbE for a future second consumer or link redundancy; 5GbE for NAS management segment |
| L4 worker links | 1 / 2.5 GbE (deferred) | Local workers ↔ switch access ports | "Worker links may be slower where sufficient" (§166) |
| L5 uplink | per upstream gateway | Switch ↔ gateway | Internet; external AI providers; hosted runners |
| Wi-Fi 7 / Bluetooth | — | Host (disabled) | Not part of the architecture; disabled in firmware (§13) |

SE11-REQ-04: the storage/core path L1 must sustain ≥ 0.7 GB/s host↔NAS during concurrent build-cache activity, and shared storage or control paths must not be the first bottleneck during concurrent transfers (§166) — verified in SE11-AC-05.

### 7.2 Switching / core role

The switch (B17) is the single core: managed, VLAN-capable, at least 2×10GbE (seed minimum, §230) with ≥ 4×10GbE preferred so that host, NAS primary, NAS secondary and one future 10GbE consumer fit without replacement (SE11-ADR-07); 24× 1/2.5GbE access ports for workers, management devices and the gateway. Until the switch is installed, an interim point-to-point 10GbE link host↔NAS with L2 to the gateway is acceptable placement — not architecture — because all addressing is by DNS name and VLAN membership is a configuration attribute (§233 H.2).

### 7.3 Segmentation (names only; SE14 designs addressing and policy, SE17 the rules)

| Segment | Members | Purpose |
|---|---|---|
| `seg.mgmt` | Host management interface, NAS admin, switch management, UPS network service | Administrative plane; MFA-protected access (§59); no workload traffic |
| `seg.storage` | Host 10GbE, NAS 10GbE | Backup/artifact traffic only; not routed to workers |
| `seg.platform` | Core VM, Data VM, runtime namespaces | Stable runtime east-west |
| `seg.build` | Build/CI VM, Validation/Staging VM, local containers | Build/test east-west; fault injection confined here |
| `seg.worker` | Local workers (deferred), hosted-runner VPN/egress | Disposable execution |
| `seg.egress` | Gateway-facing | Default-deny disclosure gateway for external model inputs (§66) sits on this boundary |

### 7.4 East-west traffic and bottleneck avoidance

- Build artifacts move Build/CI VM → artifact store (M2_2) over the host-internal virtual switch (no physical hop); only archival copies cross L1 to the NAS, scheduled outside peak build windows (SE20).
- Database backups cross L1 at off-peak; restore drills (§14) measure actual throughput to replace the assumptions in §6.2.
- Worker-to-core control traffic is small; worker artifact pulls are served from the host artifact store, not the NAS.

### 7.5 Expansion ports / headroom

Free after baseline: NAS 1×10GbE + 2×5GbE; host 2×USB4 (usable for emergency 10GbE/NVMe adapters), switch access ports per §7.2. Trigger for a second switch or a 10GbE-dense core is in §12.2.

## 8. Physical power / placement architecture (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

### 8.1 Power domains

| Domain | UPS | Circuit (requirement, not design) | Loads | Status |
|---|---|---|---|---|
| PD-A | UPS-A CyberPower CP1500PFCLCD, 1500 VA / 1000 W, line-interactive AVR, 6 battery-backed outlets (B15) | Circuit A: separate 15 A breaker; UPS plugged directly into wall (§231) | Central host, NAS, switch (critical network), gateway if co-located | ADOPT WITH ENGINEERING CONSTRAINT |
| PD-B | UPS-B ~1000 VA / 600 W pure sine, model TBD (B16) | Circuit B: second separate 15 A breaker (§231) | Rack PDU → local workers | DEFER / OPTIONAL with the rack |

Isolation rule (§165): worker/rack power is isolated from the host/NAS UPS so a worker fault or overload cannot drop the durable tier.

### 8.2 Device power envelopes and circuit/load assumptions

| Device | Envelope used for planning | Source / assumption |
|---|---|---|
| Central host, no GPU | ~350–480 W peak at wall (CPU package ≤ 230 W + board/memory/4×NVMe/fans/NIC + PSU losses) | B1, B7; engineering estimate ASM-SE11-05, replaced by SE11-AC-06 measurement |
| Central host, with GPU | +145 W → ~500–630 W peak | B11 |
| NAS, 6 HDD + 2 M.2 | ~90–150 W (spin-up transient higher) | B12/B14 class; ASM-SE11-05 |
| Switch + gateway | ~30–80 W | class estimate |
| PD-A total | ~470–710 W without GPU; ~620–860 W with GPU — below the 1000 W UPS-A rating in both cases, but runtime at these loads is minutes, so the UPS is a controlled-shutdown device, not a ride-through supply (§165) | SE11-AC-06 verifies |
| Whole installation | Seed planning figures: typical ~560 W, sustained peak ~1,150–1,300 W when the rack is present (§231) | To be measured; retained as the circuit-sizing input for the electrician |

SE11-REQ-10 (qualified-professional requirement, code-regulated work not designed here): a licensed electrician verifies that circuits A and B are separate branch circuits of adequate rating for the measured/peak loads above, that receptacles, grounding and surge arrangements meet local code, and whether the optional dedicated 20 A circuit (§231) is warranted; SE11 supplies only the load figures and the two-domain requirement.

### 8.3 Safe-shutdown dependencies (SE11-DEC-07)

Topology: UPS-A USB-HID is connected to the NAS, whose UPS service acts as the network UPS server (B12: "UPS support / network UPS server"); the Windows host runs the matching network UPS client; VMs receive the shutdown signal from the host. Ordering on mains loss:

1. T+0 s: on-battery event broadcast; `pool.background` and `pool.build` batch work paused (§175).
2. T+60 s (if mains not restored): host initiates orderly VM shutdown Validation → Build/CI → Core → Data (Data last so dependants drain first); local workers (if any, on PD-B) are drained by their own UPS client.
3. T+240 s or UPS "low battery", whichever first: host shuts down; the NAS continues to hold the network until the host confirms off, then shuts itself down on its low-battery threshold.
4. SE11-REQ-06: the whole sequence must complete inside the measured UPS-A runtime at the measured PD-A load minus a 30 % reserve (SE11-AC-06); if it cannot, the load on PD-A is reduced (move switch/gateway to a separate small UPS) rather than the sequence shortened.

The host must never depend on the NAS for its own shutdown path beyond the signal (no boot or shutdown dependency on NAS-hosted storage).

### 8.4 Placement constraints (rack / desk / room)

- Central host: tower chassis placed free-standing with unobstructed mesh front intake and rear exhaust, off the floor, on PD-A; not inside the 18U rack (rack is for workers/switch/PDU per §230).
- NAS: adjacent to the host on PD-A, within Cat6a reach of the switch; 6×3.5-inch drives make it vibration-sensitive — solid surface, not stacked on the host.
- Switch: rack-mounted when the rack exists; until then shelf-mounted next to the NAS, on PD-A battery-backed outlet.
- Rack (deferred): 18U; 17U used with a gap after every device or 12U without gaps for micro trays (§230); 1U switch, 1U PDU, 1U power-brick shelf, worker trays sized to the selected worker form factor; PD-B feeds the PDU.
- Room: lockable (§13.3), ambient within the device classes' operating range, no shared circuit with high-draw appliances (requirement to the electrician under SE11-REQ-10); the detailed thermal and rack layout belongs to SE11-POWER-COOLING-RACK.
