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

