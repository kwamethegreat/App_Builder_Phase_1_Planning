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

## 9. Failure-domain design (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-08)

Common-mode failure domains are named explicitly so that every consuming document can reference them by id. Redundancy "must cover actual shared failure points such as network, power, storage, control plane, DNS, external AI/provider dependencies, and internet connectivity — not merely worker count" (§173).

| Domain id | Failure domain | What fails together | Blast radius in the reference configuration | Mitigation in this architecture | Residual (accepted at Stage 1–2, revisited per §12.3) |
|---|---|---|---|---|---|
| FD-HOST | Central host (board, CPU, memory, PSU, NVMe) | All four VMs, `pool.core`, `pool.data`, `pool.build`, `pool.validate`, WSL2 | Platform control plane and data stop; elastic workers lose their coordinator | Hardware-independent VM/container definitions (SE11-REQ-05); T2/T3 copies; hosted executors keep queued disposable work idle rather than lost (§175) | Single host = single control-plane failure domain; no HA until a second host or hosted control plane is justified (SE11-ADR-01, SE11-RISK-01) |
| FD-WORKER | Worker pool (local or hosted) | One or more workers | Capacity reduction only (§172) | Multiple eligible execution targets per task; no critical service on one uniquely named worker (§172) | None material |
| FD-STORAGE | NAS enclosure / array | T2 durable copies; backup targets | Backups pause; T1 keeps running; recovery depends on T3 | RAID 6; snapshots; T3 isolated copy; T2 never a live datastore | Time-boxed degraded mode without local backup target |
| FD-SWITCH | Core switch / uplink | L1, L2, L4, L5 | Host and NAS lose each other and the internet; VMs on the host keep internal connectivity via the virtual switch | Interim point-to-point L1 possible; spare NAS ports; switch of equivalent class as cold spare is an SE20 decision | Single switch at Stage 1 |
| FD-UPS-A / FD-CIRCUIT-A | UPS-A or circuit A | Host, NAS, switch | Controlled shutdown (§8.3) instead of crash | Shutdown sequence SE11-DEC-07; AVR | No ride-through; outage = downtime |
| FD-UPS-B / FD-CIRCUIT-B | UPS-B or circuit B (deferred) | Local workers | Capacity reduction only | Isolation from PD-A (§165) | n/a until rack exists |
| FD-ROOM | Rack/room/site (fire, flood, theft) | Everything local | Total local loss | T3 off-site copy; portability to hosted infrastructure (§160, §168) | Rebuild time from T3 |
| FD-EXT-AI | External AI providers | `pool.agents` work needing external models | Agent throughput drops; local inference deferred (B11) | Provider router/fallback and AI-dependency governance (§66, §177); queued jobs resume (§175) | Until a local accelerator is adopted, no offline AI capability |
| FD-INTERNET | Internet uplink / gateway | External providers, hosted runners, mirrors | Same as FD-EXT-AI plus hosted-runner loss; local runtime continues | Local repositories/mirrors on T2 (§164); local build capacity in `pool.build` | Single uplink |
| FD-MGMT | Management plane (host OS admin path, NAS admin, switch mgmt, UPS service) | Ability to administer; not the workloads themselves | Operator cannot intervene remotely | Physical console access (§10.2); `seg.mgmt` isolation; configuration in version control | No out-of-band controller on the consumer-class board (SE11-RISK-04) |
| FD-NVME-M2_2 / FD-NVME-M2_4 | Single hot NVMe device | VM disks + artifacts, or platform data + containers (one of the two) | Partial availability: the other tier survives | Independent volumes (SE11-REQ-02); T2 restore | Restore time; data loss bounded by replication interval |

Dependency-failure behaviour summary: a local infrastructure problem must not corrupt active builds or accepted runtime state; resumable jobs, durable state and idempotent execution are required of every workload placed on these pools (§175) — EL/SE19 implement and prove this; SE11 only guarantees the physical boundaries above.

## 10. Hardware manageability / operability (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-09)

### 10.1 Inventory identity (SE11-REQ-07)

Every physical asset carries an inventory id `CSPUI-HW-<class>-<nn>` (classes: HOST, NAS, HDD, NVME, NIC, GPU, UPS, SW, RACK, PDU, WKR, CABLE) recorded in a version-controlled inventory file owned by SE11 and published through the hardware baseline contract (§11.4). Record fields: inventory id, BOM reference (B1–B19), manufacturer part number as cited from SEED-01, serial number, firmware/BIOS/driver version at commissioning, physical position (slot id such as `M2_3`/`PCI_E3`, NAS bay number, rack U), power domain (PD-A/PD-B), failure domain ids (§9), disposition (§1.2), commissioning evidence id (§14), warranty end. Cables are labelled at both ends with the ids of the endpoints.

### 10.2 Remote-management capabilities where available

| Device | Out-of-band | In-band management path | Fallback |
|---|---|---|---|
| Central host | None (consumer board; no BMC/IPMI) — SE11-RISK-04 | Windows remote administration on `seg.mgmt`; Hyper-V management; MFA per §59 | Physical console (keyboard/display) in the lockable room; UEFI Flash BIOS and Clear CMOS on rear panel (B3) |
| NAS | None | ADM web/SSH on `seg.mgmt` | Front panel / USB |
| Switch | Management port if the class provides one | Management VLAN | Console port |
| UPS-A | USB-HID to NAS; network UPS server | Status via NAS UPS service and telemetry export | Front LCD |

### 10.3 Telemetry and health status (SE11-REQ-08; consumed by SE20 monitoring, SE01 capacity, SE19 validation)

Mandatory signals from day one ("capture performance/resource telemetry from the first workloads", §160; "capture CPU, memory, I/O, network, queue time, job duration, reliability, and cost", §234): host CPU utilisation per VM and total, memory committed per VM, NVMe SMART (temperature, media errors, percentage used, TBW consumed) per device, PCIe link width/speed per slot (detects degraded M2_3/PCI_E3 sharing), NIC link speed and errors, NAS array state (healthy/degraded/rebuilding), per-drive SMART, NAS volume utilisation, snapshot success, backup job success/duration/throughput, UPS state (online/on-battery/low-battery, load %, runtime estimate, battery age), host and NAS temperatures, switch port utilisation on L1/L2. Thresholds that trigger expansion or revision are in §12.

### 10.4 Firmware / BIOS / driver lifecycle (SE11-REQ-09)

- Components with a firmware lifecycle: host UEFI/BIOS (incl. CPU microcode/AGESA), NVMe firmware ×4, NIC driver/firmware, optional GPU driver, NAS ADM and HDD firmware, UPS firmware, switch firmware.
- Update path: vendor-signed images only, checksum verified against the vendor publication, staged in a declared maintenance window (§10.5) after a successful snapshot of all VMs and a verified T2 backup; one component class per window; rollback plan recorded; post-update SE11-AC-04 smoke subset executed.
- Policy ownership: SE20 schedules and executes; SE17 defines the integrity controls (§13.4); SE11 keeps the compatibility matrix (§11.1) current.

### 10.5 Maintenance windows

Hardware maintenance is only performed in a window declared to SE20's operations calendar that does not overlap a stage-gate VP validation (§174 priority "VP validation / release assurance"). Minimum window content: pre-checks (backup verified, snapshots taken, UPS healthy), the change, post-checks (SE11-AC-04 smoke, telemetry nominal), inventory record updated (§10.1).

## 11. Compatibility / availability assessment (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-10)

### 11.1 Structural compatibility check (performed from the BOM specifications themselves)

| Check | Items | Result from BOM data | Residual verification |
|---|---|---|---|
| Socket / chipset | B1 AM5 ↔ B3 AM5/X870 | Compatible | BIOS version supporting the CPU: SE11-AC-01 |
| Memory | B4 4×64 GB DDR5 UDIMM ↔ B3 "4× DDR5 DIMM, up to 256 GB" | Compatible at capacity; DDR5-6000 EXPO on four DIMMs is a stability-validated profile, not a guaranteed one (seed itself prescribes the 5600/5200 fallback) | Memory stability pass: SE11-AC-04 |
| Cooler | B2 157 mm ↔ B8 ~166 mm clearance; AM5 mounting included | Compatible | — |
| Form factor | B3 ATX ↔ B8 ATX/E-ATX | Compatible | — |
| PCIe lane sharing | B10 NIC in PCI_E3 (Gen4 x4, "shares with M2_3") ↔ B5 scratch NVMe in M2_3 (Gen4 x2) | Both populated: either link may negotiate at reduced width; at Gen3/Gen4 x2 the NIC still has ≥ 10 Gb/s available, so function is preserved, bandwidth must be measured | SE11-AC-02 (link width read-back); fallback if the slots are mutually exclusive: scratch moves to a partition of M2_2 and M2_3 stays empty — recorded as SE11-DEC if invoked |
| M2_2 ↔ USB4 sharing | B6 on M2_2 (Gen5 x4, "sharing with USB4") | USB4 is unused in the baseline; no conflict | Confirm USB4 use does not down-shift M2_2: SE11-AC-02 |
| PSU | B7 750 W ATX 3.1, 12V-2x6 ↔ B1 230 W + B11 145 W + platform | Within rating with margin for the no-GPU build; GPU build conditional on measurement (seed condition) | SE11-AC-06 |
| GPU mechanical | B11 single-slot full-height 241 mm ↔ B8 mid-tower, PCI_E1 x16 | Expected to fit a mid-tower ATX chassis; not asserted as fact | SE11-AC-02 before adoption |
| NAS memory | B13 DDR5-4800 ECC SO-DIMM ↔ B12 "2 slots; 64 GB max"; mixed 16 GB + 32 GB | Capacity compatible; mixed-size pair must be on the NAS compatibility list | SE11-AC-01 (deferred item) |
| NAS drives | B14 3.5-inch SATA CMR ↔ B12 8 SATA bays | Compatible | — |
| Network | B10 10GBase-T ↔ B12 2×10GbE; Cat6a supplied with NAS (§228.1) | Compatible | Switch class must offer 10GBase-T or SFP+ with matching transceivers: SE11-AC-05 |
| UPS | B15 1000 W ↔ PD-A loads (§8.2); NEMA 5-15P input ↔ 15 A circuit (§231) | Compatible; runtime unknown until measured | SE11-AC-06 |
| OS / virtualization | B9 Windows 11 Pro ↔ Hyper-V; TPM 2.0 + Secure Boot prerequisites; Linux guest support; NIC driver for the virtual switch | Hyper-V is a Pro feature; TPM/Secure Boot are install prerequisites so they must exist on the platform | SE11-AC-01, SE11-AC-03 |

### 11.2 Current manufacturer support and practical availability

The corpus contains no market or vendor-support data, and SE11 has no tool access to manufacturer publications; therefore manufacturer support status, current firmware availability and practical availability are **not asserted as confirmed facts** (BND-04). They are baselined as a mandatory gate: SE11-AC-01 must be passed with dated evidence before the baseline in §17 is consumed as "verified". If any item fails SE11-AC-01, the specification-class alternative below applies and the substitution is logged as an SE11-DEC entry (SE11-REQ-12). This is sufficient to avoid baselining an impossible or obsolete combination because no purchase or build proceeds on an unverified item.

### 11.3 Alternatives by specification class (not procurement preference)

| BOM item | Specification class that preserves performance, reliability, security, portability and schedule assumptions |
|---|---|
| B1 CPU | AM5 desktop CPU, ≥16 physical cores, ≥64 MB L3, ≤230 W package, hardware virtualization + IOMMU |
| B3 motherboard | ATX AM5, 4×DDR5 to 256 GB, ≥1× PCIe x16 (CPU) + ≥1× PCIe x4 slot usable concurrently with ≥4× M.2 (≥2 of them x4), ≥2.5 GbE onboard, UEFI Secure Boot, TPM 2.0 |
| B4 memory | Single matched 4-DIMM DDR5 kit, 256 GB (or 192 GB if the reservation floors in §5.2 are revised down), ≥DDR5-5200 validated on four DIMMs; ECC-capable platform class is the recorded substitute if SE11-RISK-02 materialises |
| B5/B6 NVMe | M.2 2280 PCIe 4.0 x4 (or 5.0), TLC with DRAM, ≥600 TBW per TB, 5-year warranty class |
| B7 PSU | ATX 3.1 / PCIe 5.1, ≥750 W, Cybenetics Gold or better, native 12V-2x6, fully modular, ≥7-year warranty class |
| B8 case | Mid-tower ATX with mesh front, ≥160 mm cooler clearance, ≥250 mm GPU clearance |
| B10 NIC | 10GBase-T (or SFP+ with matching switch), PCIe 3.0 x4 or 4.0 x2 minimum, in-box or vendor driver supporting the Windows Hyper-V virtual switch |
| B11 GPU | Single-slot, ≤145 W, ≥24 GB ECC VRAM, PCIe x16, 12V-2x6 or 8-pin; larger classes are ESCALATE |
| B12 NAS | 8-bay SATA NAS with ECC memory, ≥2×10GbE, Btrfs/ZFS-class snapshots, per-folder/volume AES-256, network UPS server, M.2 cache slots |
| B14 HDD | 3.5-inch enterprise CMR, 7,200 RPM, ≥2.5 M h MTBF, ≥550 TB/yr workload, 5-year warranty, ≥20 TB |
| B15/B16 UPS | Pure-sine line-interactive with AVR, USB-HID, ≥1500 VA/1000 W (PD-A) and ≥1000 VA/600 W (PD-B), user-replaceable batteries |
| B17 switch | Managed L2+, ≥2×10GbE (≥4 preferred), 24× ≥1 GbE access, VLAN, port mirroring for SE17/SE19 |

### 11.4 Interface contract: hardware baseline record

`SE11-CONTRACT-hardware-baseline@1` (owner SE11; registered in SE11's Interface Contract document and later in EL's contract register) publishes, per asset: the fields of §10.1, the disposition from §1.2, the failure-domain ids from §9, the pool ids from §4 and the validation evidence ids from §14. Consumers (EL runtime/deployment/reliability/estimate documents, SE01, SE12, SE14, SE17, SE19, SE20, Stage-14 plans) cite this contract and the disposition they rely on; they never restate hardware facts.

## 12. Expansion model (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-12)

### 12.1 Planned spare capacity at baseline

| Resource | Spare at baseline | Scale path |
|---|---|---|
| Host PCIe | PCI_E1 x16 (reserved for GPU), PCI_E2 x1, 2×USB4 | Scale-up only |
| Host memory | None (256 GB is the board maximum, B3) | **Hard ceiling** — see 12.3 |
| Host NVMe slots | None (4/4 populated) | Device-capacity scale-up; SATA ×4 available for cold tiers only |
| NAS bays / M.2 | 2 bays, 4× M.2 | RAID 6 expansion; cache/metadata |
| NAS network | 1×10GbE + 2×5GbE | Second 10GbE consumer or link redundancy |
| Switch ports | all minus 2–3 at baseline | Workers, gateway, management devices |
| Rack | 18U, 12–17U usable (§230) | Worker trays, second switch, PD-B |
| Power | PD-A margin per §8.2; PD-B unused | Workers only on PD-B |
| Worker pool | Elastic: hosted/cloud executors unbounded by local hardware (§168) | Scale-out by default |

### 12.2 Evidence-driven triggers that add hardware without architecture revision (§159, §171)

| Trigger id | Signal (from §10.3 telemetry) | Action |
|---|---|---|
| TRG-WKR-LOCAL | Measured build/test queue wait p95 above the SE01-defined threshold for two consecutive stages **and** hosted-runner cost or data-privacy makes local execution preferable (§168, §171) — and the limiting factor is worker capacity, not central resources, storage, network, provider quotas or software (§171) | Adopt local worker class (B19), rack, PDU, UPS-B (B16/B17) |
| TRG-GPU | Measured external-model latency/cost/privacy case or GPU-required application testing (§176) with preconditions §5.4 met | Adopt B11 |
| TRG-NAS-MEM | NAS memory sustained > 70 % or snapshot/backup jobs missing their window due to memory pressure | Install B13 |
| TRG-NAS-CAP | T2 utilisation > 70 % | Add drives to free bays (same class as B14) |
| TRG-NET-10G | L1 utilisation > 70 % sustained during backup windows, or a second 10GbE consumer | Use NAS second 10GbE / add 10GbE ports within the switch class |
| TRG-NVME-TBW | Any NVMe > 80 % of rated TBW or media errors | Replace with same class (§11.3) |
| TRG-UPS-BATT | UPS runtime estimate below the §8.3 sequence budget + 30 % | Battery replacement (RB1290X2 class, B15) |

### 12.3 Scale-out versus scale-up boundaries and architecture-revision triggers

The central node complements, never replaces, horizontally scalable workers (§177 acceptance list). Scale-out (more workers, hosted executors) is the default answer to throughput; scale-up applies only to the capabilities the seed assigns to the central node — large contiguous RAM, low-latency CPU, NVMe, centralized data/control services (§161). The following require a revision of this architecture (new SE11 version plus EL review), not a hardware addition:

| Revision trigger | Why adding hardware is insufficient |
|---|---|
| REV-MEM: Highest-priority pool floors (§5.2) exceed 85 % of 256 GB on measured p95 | Board memory ceiling reached; a second host, a larger-memory platform class, or hosted data services is an architectural choice |
| REV-HA: an SLO (§117 governance) requires the control plane or Data VM to survive FD-HOST | Requires a second failure domain (second host or hosted control plane) and quorum design (§173) |
| REV-GPU-CLASS: accelerator > 145 W, dual-slot, or second accelerator | Exceeds PSU, slot and thermal envelope (§5.4) |
| REV-STORAGE-HOT: T1 > 85 % after device scale-up, or random-IO workload that cannot stay on host NVMe | NAS is not a hot tier (§164); needs a different storage architecture |
| REV-NET: storage/core path saturated after using all 10GbE ports, or need for 25 GbE class | Switch and NIC class change ripples through host slots |
| REV-SITE: requirement for geographic/resilience footprint beyond one room (§226 F.20) | Hosted/hybrid footprint decision |
| REV-POWER: PD-A measured peak within 20 % of UPS-A rating, or circuit limits reached | UPS/circuit redesign by qualified professionals; possible relocation |

## 13. Security considerations (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-11)

SE11 relies on controls owned by SE17 (infrastructure security) and names them by slug; SE17 assigns the control ids and the detailed design. Nothing here re-derives a control.

### 13.1 Trusted boot and firmware

- UEFI Secure Boot enabled on the host; TPM 2.0 present and enabled (Windows 11 Pro prerequisite, verified in SE11-AC-01); measured boot attestation is an SE17 decision (`SE17-CTRL-trusted-boot`).
- Firmware integrity: vendor-signed images, checksum verification, maintenance-window staging (§10.4) — `SE17-CTRL-firmware-integrity`.
- Host firmware settings baseline (virtualization, IOMMU, Secure Boot, TPM, disabled Wi-Fi/Bluetooth, boot order locked to M2_1, administrator password on UEFI) is recorded in the inventory record and re-verified after every BIOS update (SE11-AC-08).

### 13.2 Management interfaces

- All management endpoints (host admin, Hyper-V, NAS admin, switch, UPS service) live on `seg.mgmt`, unreachable from `seg.build`, `seg.worker` and `seg.egress`; access requires MFA and least-privilege, short-lived credentials per the zero-trust policy (§59, §112) — `SE17-CTRL-mgmt-plane-isolation`, `SE17-CTRL-admin-identity`.
- No management interface is exposed to the internet; remote operator access is through an SE17-approved access path only.

### 13.3 Physical and administrative access

- Lockable room; host, NAS, switch and UPS inside; chassis/NAS tamper-evident seals optional per SE17; physical console access is itself an administrative action logged by SE20 — `SE17-CTRL-physical-access`.
- Administrative segregation of duties between hardware maintenance (SE11/SE20) and security configuration (SE17) per §112.

### 13.4 Storage encryption support

- Host: Windows 11 Pro full-disk encryption on M2_1 with TPM-bound keys; encryption of VM disks on M2_2 and data volumes on M2_4 is implemented inside the Linux VMs or by the hypervisor as SE17 decides — the hardware supports both (`SE17-CTRL-data-at-rest`).
- NAS: per-folder AES-256 (B12) for backups, evidence and archives; key custody and recovery under `SE17-CTRL-key-management`; T3 copies encrypted before leaving the site.
- NVMe sanitisation on decommissioning/RMA (`SE17-CTRL-media-sanitisation`); inventory record marks sanitised state.

### 13.5 Supply-chain and security constraints

- Receipt check: serial numbers recorded, packaging/tamper evidence inspected, firmware version read and compared with the vendor's published current version before first power-on (SE11-AC-01, `SE17-CTRL-hardware-supply-chain`).
- Confidential processing constraint (§66): private application/customer data is processed only by authorised locally hosted models or deterministic tools; the physical consequence is that any local accelerator (B11) and the Data VM are inside `seg.platform` behind the default-deny disclosure gateway, and no hardware telemetry export (§10.3) carries workload content.
- No component ships with default credentials left in place; NAS, switch and UPS service credentials are rotated at commissioning (`SE17-CTRL-default-credentials`).

## 14. Validation / evidence plan (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-14)

| AC id | Check | Pass criterion | Evidence artefact | Executing owner | Needed by |
|---|---|---|---|---|---|
| SE11-AC-01 | Compatibility, support and availability gate | Every B1–B15, B17 item: current manufacturer support confirmed with dated source; firmware/BIOS version supporting the combination identified; practical availability confirmed or §11.3 alternative selected and logged as SE11-DEC; receipt check (§13.5) complete | Dated compatibility/availability record attached to the inventory record | SE11 (SE20 assists at receipt) | Before any build; Stage 1 start |
| SE11-AC-02 | Slot, lane and mechanical verification | Read-back of negotiated PCIe width/speed for M2_1–M2_4 and PCI_E3 with all devices installed; M2_3/PCI_E3 coexistence confirmed or fallback invoked; cooler/case clearance photos; GPU mechanical check when B11 is triggered | Firmware/OS link-state dump; inventory photos | SE11 | Stage 1 |
| SE11-AC-03 | OS / virtualization enablement | Hyper-V operational with four Linux VMs; NIC bound to virtual switch at 10 Gb/s; Secure Boot + TPM reported enabled; GPU-to-VM path evaluated (when triggered) | Hypervisor and guest configuration export; test log | SE11 with EL | Stage 1 |
| SE11-AC-04 | Burn-in and performance baseline | ≥ 24 h combined CPU/memory/NVMe stress with zero memory errors at the chosen DDR5 profile (fallback to 5600/5200 if any error, per B4); sustained thermals within device limits; NVMe sequential/random and L1 throughput recorded as the measured replacement for §6.2 | Stress logs, telemetry export, baseline numbers table | SE19 (executes), SE11 (accepts) | Stage 1 |
| SE11-AC-05 | Network path verification | Host↔NAS ≥ 0.7 GB/s sustained during concurrent build-cache load (SE11-REQ-04); segments `seg.*` enforced; management plane unreachable from build/worker/egress segments | Throughput test log; segmentation test log | SE14 (design), SE19 (test), SE17 (segmentation) | Stage 1 |
| SE11-AC-06 | Power and shutdown verification | Measured PD-A load (idle, typical, full stress, with/without GPU) at the UPS; UPS runtime at measured load; full mains-loss drill completes the §8.3 sequence with ≥ 30 % runtime reserve; VMs and NAS come back clean; electrician's sign-off of circuits A/B on file (SE11-REQ-10) | Power measurement table; drill log; professional sign-off reference | SE11 (measurement), SE20 (drill), qualified electrician (circuits) | Stage 1 before stable-runtime baseline |
| SE11-AC-07 | Storage durability and recovery drill | Snapshot + replication T1→T2 verified; restore of a VM and a database from T2 to a clean volume within SE12's RTO; NAS single-drive pull with rebuild time recorded (ASM-SE11-04 replaced by measurement); T3 copy existence verified for the irreplaceable set | Restore drill log; rebuild timing; T3 inventory | SE12 (policy), SE19/SE20 (drill) | Stage 2 (T3 may be "as program matures", §164, but no later than Stage 3) |
| SE11-AC-08 | Security baseline of hardware | Firmware settings baseline (§13.1) verified; management interfaces reachable only from `seg.mgmt` with MFA; disk/folder encryption active where §13.4 requires; default credentials rotated | SE17 control evidence referencing the inventory ids | SE17 | Stage 1 (host, NAS), Stage 3 (full) |
| SE11-AC-09 | Telemetry coverage | Every signal in §10.3 visible in SE20 monitoring with alert thresholds from §12.2 | Dashboard/alert export | SE20 | Stage 1 |
| SE11-AC-10 | Inventory and baseline sign-off | Inventory record complete for every asset; `SE11-CONTRACT-hardware-baseline@1` published; §17 sign-off record filled with evidence ids of AC-01…AC-09 | Signed baseline record | SE11 | Before downstream consumption as "verified" |

Resilience tests beyond the above (fault injection on `pool.validate`, switch loss, NAS loss, provider loss) are specified and run by SE19 against the failure domains in §9; SE11 supplies the physical means (spare cables, drive-pull procedure, power-cut procedure) and accepts the evidence.

## 15. Exclusions (BND-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01 … AR-04)

| Exclusion | Disposition in this document |
|---|---|
| BND-01 Purchase orders, price negotiation, vendor-selection scorecards, procurement workflow | Excluded. No prices, suppliers, order quantities or purchase approvals appear; part numbers are cited only as they appear in SEED-01 and alternatives are by specification class (§11.3). Nobody owns procurement in this chain. |
| BND-02 Project-owned acquisition dates | Excluded. Only dependency windows are referenced ("Stage 1", "before stable-runtime baseline") as the stage by which evidence is needed; no calendar dates. |
| BND-03 Detailed software/container/service design owned by existing SE11 artefacts | Excluded. §4–§5 stop at pools, VM boundaries and reservations; service design, container images and pipelines are referenced to EL and SE11's other artefacts. |
| BND-04 Unverified assumptions presented as confirmed hardware facts | Complied with. Every non-seed figure is marked as an engineering assumption (ASM-SE11-nn) or a validation gate (SE11-AC-nn); availability and support currency are explicitly not asserted (§11.2). |

## 16. Architecture risks, decisions and ADRs (OUT-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-13)

### 16.1 Architecture decision records

| ADR | Decision | Alternatives considered (rejected unless superseded by a later ADR) | Rationale |
|---|---|---|---|
| SE11-ADR-01 | One central node + durable NAS + elastic (hosted-first) worker pool; local workers deferred | (a) Two-node local cluster from day one — rejected: no measured need, violates no-overbuild (§158, §238); (b) All-hosted, no local hardware — rejected as the *only* option: seed requires local durable tier and central-node capabilities when justified (§161, §164), and confidential processing favours local data handling (§66); remains the fallback for FD-HOST/FD-ROOM | Matches §161 ("centralized … may be used when measured workloads justify it") and §168 (worker pool elastic, hybrid) |
| SE11-ADR-02 | Windows 11 Pro host with Hyper-V Linux VMs for all durable services; WSL2 for interactive only | Bare-metal Linux hypervisor — rejected: the seed fixes the preferred operating model (§166) and retains Windows for workstation/admin use (§227.9); portability is preserved at the container/VM-definition level (§168), so the host choice is not an architectural lock-in | §166, §167, §168 |
| SE11-ADR-03 | Non-ECC 256 GB DDR5 on a consumer AM5 platform accepted for the central node | Workstation/server platform with ECC — recorded as the substitute class if memory-error telemetry or data-integrity incidents attributable to memory occur (SE11-RISK-02); rejected now because the seed's reference configuration is non-ECC and the durable tier (NAS) is ECC | §227.4, §228.1; cost/schedule per §226 |
| SE11-ADR-04 | GPU deferred; adoption gated by §5.4 and TRG-GPU; accelerator class capped at single-slot ≤145 W within this architecture | Adopt GPU at first build — rejected: §175/§177 make it optional and demand-driven; external providers are the default (§160) | §175–§177 |
| SE11-ADR-05 | Host NVMe as independent volumes without RAID; NAS as durable/backup tier only; one-way replication T1→T2→T3 | Host NVMe mirroring — rejected (does not address FD-HOST; doubles cost); NAS as live VM datastore over 10GbE — rejected (§164: not a latency substitute; would make FD-STORAGE a hot-path SPOF) | §163, §164 |
| SE11-ADR-06 | UPS-A USB to NAS as network UPS server; host as network client; shutdown order Validation → Build/CI → Core → Data → host → NAS | USB to host with host as server — viable alternative; not chosen because the NAS is the last device to power down and natively offers the network UPS server role (§228.1); switchable by SE11-DEC if SE11-AC-06 shows the client mode on the host is unreliable | §165, §229.1 |
| SE11-ADR-07 | Single managed switch, ≥2×10GbE minimum (seed), ≥4×10GbE preferred; interim point-to-point 10GbE allowed as placement | Unmanaged 10GbE switch — rejected: segmentation (§7.3) needs VLANs; dual redundant switches — rejected now: not justified by measured need (§166 "purchased incrementally from measured need") | §166, §230 |

### 16.2 Decisions (SE11-DEC-nn)

| Id | Decision | Impact |
|---|---|---|
| SE11-DEC-01 | B1 adopted with virtualization/IOMMU enabled and 230 W package limit as the compute power line | Power budget §8.2; thermal validation SE11-AC-04 |
| SE11-DEC-02 | B3/B5/B10 adopted with the PCI_E3–M2_3 lane-sharing constraint; fallback scratch-on-M2_2 if mutually exclusive | SE11-AC-02; §6.2 scratch bandwidth |
| SE11-DEC-03 | B4 adopted at 256 GB as a single matched kit; justification: §5.2 floors (lower bound 192 GB) plus the seed's own stability fallback; oversize evidence feeds SE11-HARDWARE-CAPACITY-SIZING | SE11-RISK-02 monitored |
| SE11-DEC-04 | B7 adopted; GPU power conditional on SE11-AC-06; >145 W class escalates | §5.4, §12.3 REV-GPU-CLASS |
| SE11-DEC-05 | B13 deferred to TRG-NAS-MEM | Stock 16 GB ECC until telemetry justifies |
| SE11-DEC-06 | B14 adopted as 6-drive RAID 6; 4-drive start recorded as the alternative conditioned on SE12's Stage-1 retention volume | §6.5 |
| SE11-DEC-07 | Shutdown topology and sequence of §8.3 | SE11-REQ-06, SE11-AC-06 |
| SE11-DEC-08 | Switch adopted by class now; rack/PDU/trays/UPS-B/local workers deferred to TRG-WKR-LOCAL | §7.2, §8.1, §12.2 |

### 16.3 Requirements introduced by this document (SE11-REQ-nn)

| Id | Requirement | Verified by |
|---|---|---|
| SE11-REQ-01 | Hard (non-oversubscribed) reservations for `pool.core`, `pool.data`, `pool.runtime`; burst ceilings for all others | SE11-AC-03, SE01 model |
| SE11-REQ-02 | No two Highest-priority pools share a single NVMe device with a Medium-priority pool | SE11-AC-02/03 |
| SE11-REQ-03 | T0/T1 is never the sole copy of release evidence, repositories, platform databases or VM definitions; irreplaceable data has a T3 copy | SE11-AC-07 |
| SE11-REQ-04 | Storage/core path L1 sustains ≥ 0.7 GB/s host↔NAS under concurrent build-cache load; shared paths are not the first bottleneck | SE11-AC-05 |
| SE11-REQ-05 | VM/container definitions carry no physical slot ids, serials or host names (portability §160) | SE11-AC-03 review |
| SE11-REQ-06 | Safe-shutdown sequence completes within measured UPS-A runtime minus 30 % reserve | SE11-AC-06 |
| SE11-REQ-07 | Inventory identity scheme and record fields of §10.1 for every asset and cable | SE11-AC-10 |
| SE11-REQ-08 | Telemetry signals of §10.3 exported from first power-on | SE11-AC-09 |
| SE11-REQ-09 | Firmware/driver lifecycle per §10.4 with snapshot + verified backup precondition | SE11-AC-08, SE20 |
| SE11-REQ-10 | Electrical circuits A/B (two separate 15 A breakers, optional dedicated 20 A, direct-to-wall UPS) verified and, where needed, installed by a licensed electrician against the load figures of §8.2; SE11 designs no electrical work | SE11-AC-06 sign-off reference |
| SE11-REQ-11 | All downstream documents reference this document id and the disposition (B-id + disposition) they rely on, and name the §9 failure-domain ids | EL review |
| SE11-REQ-12 | Any substitution of a dispositioned item is recorded as a new SE11-DEC entry with technical reason and impact before use; silent substitution is prohibited | SE11-AC-10 |

### 16.4 Risks

| Id | Risk | Likelihood / impact | Mitigation | Owner |
|---|---|---|---|---|
| SE11-RISK-01 | Single central host is the control-plane and data failure domain (FD-HOST); hardware fault = platform outage | Medium / High | Hardware-independent definitions (SE11-REQ-05), T2/T3 copies, hosted fallback; REV-HA trigger | SE11, EL |
| SE11-RISK-02 | Non-ECC host memory → silent data corruption in Data VM | Low / High | Memory stress at commissioning (SE11-AC-04); database checksums and backup verification (SE12); ECC platform class recorded as substitute (SE11-ADR-03) | SE11, SE12 |
| SE11-RISK-03 | PCI_E3/M2_3 lane sharing reduces NIC or scratch bandwidth, or the slots are mutually exclusive | Medium / Medium | SE11-AC-02 read-back; fallback in SE11-DEC-02 | SE11 |
| SE11-RISK-04 | No out-of-band management on the consumer board; a hung host requires physical presence | High / Medium | Physical console in lockable room; watchdog-style auto-restart policy by SE20; REV-HA if unacceptable for SLOs | SE11, SE20 |
| SE11-RISK-05 | Manufacturer support or availability of a BOM item lapses before baseline (BOM v2.2 is a point-in-time reference) | Medium / Medium | SE11-AC-01 gate; §11.3 specification classes; SE11-REQ-12 | SE11 |
| SE11-RISK-06 | Long RAID 6 rebuild at 20 TB drive size exposes the array to a third failure | Low / High | RAID 6 not RAID 5; T3 copy; scrub schedule and rebuild timing measured (SE11-AC-07); hot-spare option in free bays | SE12, SE11 |
| SE11-RISK-07 | UPS-A runtime at measured load insufficient for the shutdown sequence | Medium / High | SE11-AC-06 drill; load reduction option in §8.3; battery-age telemetry | SE11, SE20 |
| SE11-RISK-08 | Seed revision status: Rev 1.1 is "proposed" while v1.0 "remains authoritative" (§0); hardware baseline could change on approval | Low / Medium | Sign-off bound to sha and revision (§17); change control per §151/§104 re-enters this document | SE11, PL |

### 16.5 Assumptions (explicit, labelled; corpus silent)

| Id | Assumption | Resolution path |
|---|---|---|
| ASM-SE11-01 | PL-REQ-ID-REGISTER and fragments G01–G04 were absent at authoring; seed sections are cited directly. When the register exists, its row ids for §152–§177 and Appendix G/H map onto the citations here without content change | Next SE11 revision adds register ids |
| ASM-SE11-02 | SEED-01 Rev 1.1 is the operative Stage-0 seed despite its "proposed" status note | PL confirms; SE11-RISK-08 |
| ASM-SE11-03 | Reservation floors/ceilings in §5.2 are pre-measurement engineering estimates derived from §156/§167 | Replaced by measured p95 after Stage 1 (§234) |
| ASM-SE11-04 | RAID 6 rebuild window for 20 TB CMR drives under concurrent load is planned at 1–3 days | Measured in SE11-AC-07 |
| ASM-SE11-05 | Device power envelopes in §8.2 (host 350–480 W no-GPU; NAS 90–150 W; switch/gateway 30–80 W) are class estimates; the seed's ~560 W typical / 1,150–1,300 W peak remain the circuit-sizing figures | Measured in SE11-AC-06 |

### 16.6 Conflicts

None. No approved upstream document contradicts this architecture; the only tension — the seed's own "proposed revision" status note (§0) versus its exclusive ownership of the hardware baseline — is recorded as SE11-RISK-08 / ASM-SE11-02 rather than as a conflict between documents.

## 17. Baseline sign-off record (QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-07)

| Field | Value |
|---|---|
| Baseline id | SE11-HW-BASELINE-1 |
| Bound to | SEED-01 Proposed Revision 1.1, Appendix G BOM v2.2, sections §152–§177, §226–§238; file sha `2d3a171d6961a8790f5a9812eeb1e3907f188242` |
| Dispositions | B1–B19 as in §1.2 (ADOPT ×2; ADOPT WITH ENGINEERING CONSTRAINT ×12 incl. switch; DEFER / OPTIONAL ×5: B11, B13, B16, rack/PDU/trays of B17, B19; SUBSTITUTE ×0; ESCALATE ×0 at baseline, conditional escalations REV-* in §12.3) |
| Verification state | **Dispositioned, pending verification**: becomes "verified" when SE11-AC-01…AC-10 evidence ids are attached. Downstream documents may cite the dispositions now and must cite the verification state they rely on |
| Published contract | `SE11-CONTRACT-hardware-baseline@1` (§11.4) |
| Sign-off | SE11 (author) — architecture complete for Stage 0; EL cross-references; SE01/SE12/SE14/SE17/SE19/SE20 supply requirements/evidence per §18 |

## 18. Cross-domain dependencies

| Owning role | What is needed from / supplied to them | Contract or artefact | Stage needed by |
|---|---|---|---|
| EL | Reference this document (not duplicate) in system/runtime/deployment/reliability/estimate documents; bind services to pools (§4); register `SE11-CONTRACT-hardware-baseline@1` | EL contract register | Stage 1 design |
| SE01 | Capacity model and thresholds for TRG-*/REV-* from §10.3 telemetry; replace §5.2 estimates | SE01 capacity document | Stage 1 end |
| SE12 | Retention volume (drives SE11-DEC-06), RPO/RTO, backup schedule, T3 provider/medium, key custody with SE17 | SE12 storage/data document | Stage 1 (T2), Stage 2–3 (T3) |
| SE14 | Addressing, VLAN design and switch configuration for `seg.*`; L1 throughput design | SE14 network document | Stage 1 |
| SE17 | Control ids for the slugs in §13; SE11-AC-08 evidence | SE17 infrastructure security document | Stage 1 (host/NAS), Stage 3 (full) |
| SE19 | Execute SE11-AC-04/05/07 tests and failure-domain resilience tests | SE19 validation evidence | Stage 1–2 |
| SE20 | Telemetry integration (SE11-AC-09), maintenance windows, firmware execution, shutdown drills, inventory upkeep | SE20 operations document | Stage 1 |
| SE11 (own) | SE11-HARDWARE-CAPACITY-SIZING (sizing model from these ranges) and SE11-POWER-COOLING-RACK (thermal, rack layout, PD details) | Sibling SE11 documents | Stage 1 |
| Qualified electrician | Circuits A/B verification and any installation (SE11-REQ-10) | Professional sign-off referenced from SE11-AC-06 | Before stable-runtime baseline |

## 19. Quality-criteria disposition

| Criterion | Disposition | Where |
|---|---|---|
| QC-SE11-PHYSICAL-INFRASTRUCTURE-HARDWARE-AR-01 exact source version; every item dispositioned | Covered | §1.1 (Rev 1.1, BOM v2.2, sha), §1.2 (B1–B19) |
| QC-…-AR-02 one coherent physical architecture | Covered | §2.3 context view; §4–§10 cross-referenced by pool, device, segment, power-domain and failure-domain ids |
| QC-…-AR-03 compatibility and availability checked sufficiently | Covered | §11.1 structural check from BOM data; §11.2 mandatory gate SE11-AC-01 with specification-class fallbacks so no impossible/obsolete combination is baselined as verified |
| QC-…-AR-04 no hidden SPOF, capacity limit or dependency | Covered | §9 failure domains incl. FD-HOST, FD-MGMT; §12.1 hard ceilings (memory, M.2 slots); §12.3 revision triggers; §16.4 risks |
| QC-…-AR-05 substitution rules preserve assumptions | Covered | §11.3 specification classes; SE11-REQ-12; §12.3 ESCALATE boundaries |
| QC-…-AR-06 validation evidence and affected owners explicit | Covered | §14 (AC-01…AC-10 with executing owner and stage), §18 |
| QC-…-AR-07 sign-off recorded against the exact baseline | Covered | §17 |

Outline criteria OUT-…-AR-01 to AR-14 are each covered by the correspondingly labelled section (§1, §2, §4, §5, §6, §7, §8, §9, §10, §11, §13, §12, §16, §14); none is not_applicable. The required source PL-REQ-ID-REGISTER is not_applicable for the reason stated in the preamble.
