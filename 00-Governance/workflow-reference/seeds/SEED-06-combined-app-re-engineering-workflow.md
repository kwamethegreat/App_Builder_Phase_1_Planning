---
id: SEED-06
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "Combined App Re-Engineering Workflow.md"
---

# Combined App Re-Engineering Workflow

Oct 30, 2026 · @Kwame Vision

## Overview

The combined approach reproduces a large app on desktop, web and mobile in 1–3 weeks by pairing static analysis (REA plus disassembler bridges) with an automated exploration harness (Playwright, Appium, emulators, AI vision). Static analysis tells the harness what exists; the harness tells static analysis what runs. The same harness later verifies the clone against the original.

It produces four things: an evidence corpus (traffic, traces, screenshots, accessibility trees), a synthesized spec (API contracts, state machines, data models, UI spec, architecture graph), a working clone built from a shared core with thin platform shells, and a measurable equivalence score with a list of remaining divergences.

It is for teams rebuilding their own legacy apps, building interoperable replacements, preserving software, or doing authorized research. It assumes the one-time factory in Phase 0 already exists; the 1–3 week clock starts at Phase 1.

&#91;embedded content: combined pipeline · 6 phases, 2 feedback loops\]

The inventory tells exploration what to reach; execution traces tell static analysis what to decompile; the exploration harness runs unchanged against the clone in verification.

## Phase 0: One-time factory build (before any app)

The 1–3 week timeline is only possible because none of this is built during the engagement. Budget 6–10 weeks of engineering once; every component exists today as open source or commercial tooling and needs integration, not invention.

| Component | What it does | Built from |
| --- | --- | --- |
| Static inventory tooling | Extracts routes, screens, strings, endpoints, feature flags, analytics events, entitlements, linked SDKs from bundles, APKs, IPAs and binaries | REA, Ghidra MCP or IDA/Binary Ninja MCP, jadx, source-map and bundle unpackers, Hopper or class-dump for iOS |
| Exploration harness | Launches the original on all three platforms, drives it toward inventory targets, recovers from unexpected states | Playwright, Appium + UiAutomator2, XCUITest, Android Emulator, iOS Simulator, vision-capable model, Temporal or Argo for orchestration |
| Instrumented capture | Records traffic, execution traces, screenshots, accessibility trees and video per step | mitmproxy, Frida, Chrome DevTools Protocol, coverage tooling, FFmpeg, S3-compatible storage |
| Contract synthesizer | Turns the corpus into OpenAPI specs, stateful contracts, state machines and data models | Agent pipeline over the corpus; property-based test generators (Hypothesis, fast-check, Schemathesis) |
| Architecture graph | Single source of truth for modules, types, endpoints, decisions; agents read and write it | Graph database or structured repo; REA evidence records as the seed format |
| Replay server | Serves the recorded corpus so client work never waits on backend | mitmproxy replay, WireMock, Prism or a custom replay service |
| Capability library | Pre-tested adapters for the \~30 native capabilities (push, secure storage, biometrics, camera, files, background tasks, deep links, IAP, permissions) | Flutter, React Native, Kotlin Multiplatform or Tauri plugins, wrapped behind one interface |
| Substitution table | Maps proprietary SDKs to open or self-serve equivalents with adapters ready | Analytics, crash reporting, maps, auth, media, ads replacements |
| Divergence agent | Generates inputs to maximize disagreement between original and clone; files each as a reproducible ticket | Same harness, fuzzing strategies, accessibility-tree and traffic diffing |
| Device farm | Runs every commit on real iOS, Android, Windows, macOS and browsers | BrowserStack, Firebase Test Lab, AWS Device Farm or self-hosted |

Acceptance for the factory: run it end to end on one known mid-sized app you own the source for, and confirm the clone passes 95 percent of recorded sessions in under two weeks. Until that passes, the engagement timelines in this doc do not apply.

## Phase 1: Intake and static inventory (days 1–2)

By the end of day 2 you have a complete list of what the app contains, including things the UI never shows, and a classification that sets the timeline.

1. Collect all three builds (web bundle, desktop installer, Android APK, iOS IPA) plus any public API docs, changelogs and store listings.
2. Run the legal and scope check from the go/no-go checklist. Stop here if it fails.
3. Mine leaked structure first, before any decompilation: source maps, readable JS names, Electron asar contents, Android class names, Objective-C runtime metadata, Swift symbols, string tables, localization files, analytics event names, entitlements and manifest permissions. For most consumer apps this recovers 70–90 percent of the architecture.
4. Cross-platform triangulation: match features across the three builds by shared strings, endpoints and control-flow shape. Names that survive in one build label the stripped version in another.
5. Decompile only what leaked structure did not explain, using REA for breadth and Ghidra, IDA or Binary Ninja via MCP for native depth.
6. Embed and cluster functions into modules (by strings referenced, APIs called, call-graph neighborhood). Agents name the \~200 clusters, not the 50,000 functions.
7. Write the inventory into the architecture graph: every screen, route, endpoint, feature flag, state, native capability and third-party SDK, each with its evidence.
8. Classify the app and lock the plan:
   - Client-heavy (offline tools, editors, games): full 1–3 week path applies.
   - Conventional backend (CRUD, sync, auth, payments): 2–3 weeks; backend track runs in parallel.
   - Hidden server intelligence (ranking, matching, risk scoring): shell in 1–3 weeks, substitute logic for the hidden parts, flag it as non-identical.
   - Hardened (obfuscation, anti-tamper, cert pinning): expect decompilation to contribute less and exploration to carry more; add 20–40 percent to the estimate.

Outputs: inventory in the graph, SDK list for the substitution table, capability list for the capability library, exploration target list for Phase 2, app class and locked estimate.

## Phase 2: Inventory-guided exploration and instrumented capture (days 2–5, continues in background)

Exploration is coverage-driven, not blind: the harness is handed the Phase 1 inventory as a target list and reports what it reached and what it could not. This is the single change that turns the attached harness from a screenshot tool into a re-engineering input.

1. Provision isolated environments per platform: headless browsers in containers, Android emulators with virtualization, iOS simulators on macOS workers, desktop VMs with virtual displays. Seed test accounts and data.
2. Attach instrumentation before launch: mitmproxy or DevTools for traffic, Frida or coverage hooks for execution traces, accessibility-tree dumps and screenshots at every step, video per session.
3. Run deterministic scripts first for known flows (login, onboarding, core actions). Cheap, repeatable, and they produce the first golden sessions within hours.
4. Run the AI-driven explorer against the target list: reach each inventoried screen, trigger each analytics event, hit each endpoint, exercise each state. The explorer gets a score, not a vibe: targets reached over targets inventoried.
5. Convert every successful AI exploration into a deterministic replay script. AI discovers once; scripts replay forever.
6. Parallelize across hundreds of sessions with randomized data, roles and device profiles to surface variants (empty states, errors, permissions denied, slow network, offline).
7. Feed execution traces back to Phase 1: functions that ran under a feature are decompiled and annotated; functions that never ran are deprioritized.
8. Explicitly log unreachable targets (needs real hardware, CAPTCHA, admin role, paid tier) and decide per item: provision access, substitute, or scope out.

Coverage expectations by day 5: 85–95 percent of inventoried screens reached for conventional apps, 60–80 percent for hardened or hardware-dependent apps. The unreached list is a scoped decision, not an unknown.

Outputs: traffic corpus, execution traces, screenshot and accessibility-tree corpus, replay scripts, coverage report, unreached-target decisions.

## Phase 3: Contract and architecture synthesis (days 4–7, overlaps Phase 2)

The output of this phase is the spec the build is held to. Two independent sources, code and observed behavior, are reconciled, and every disagreement between them becomes a task rather than a guess.

1. API contracts: from the traffic corpus, generate OpenAPI specs plus stateful contracts (preconditions, transitions, idempotency, ordering, error cases). Express them as property-based tests so they are executable, not prose.
2. State machines and data models: from traces plus decompiled hot paths, recover client-side state, persistence schema, sync and conflict rules, caching and retry behavior.
3. UI spec: from accessibility trees and screenshots, produce per-screen specs with exact copy, component hierarchy, layout, transitions and responsive behavior across the three platforms.
4. Cross-check: states implied by code but never observed, and behaviors observed but not found in code, are listed and investigated. Typical findings are feature flags, A/B variants and dead code.
5. Define equivalence tiers up front: pixel-level for flagship screens, structural (accessibility tree) for most screens, functional (traffic and state) for background behavior. This is where you stop chasing differences nobody can perceive.
6. Decompose into modules with contracts between them, so each build agent works on one module with only its own and its neighbors' contracts in context.
7. Commit everything to the architecture graph. An architect agent owns it from here and rejects any merge that contradicts it.

Outputs: executable API contracts, state machines, data models, UI spec, equivalence tiers, module decomposition, populated architecture graph.

## Phase 4: Build (days 5–15)

The app is built once as a shared core with thin platform shells, against the replay server, with the capability library and substitution table doing the platform and third-party work. Three parallel tracks run from day 5.

**Core track.** All business logic, state, networking and persistence in one cross-platform core (Kotlin Multiplatform, Rust, Dart or TypeScript depending on the original's shape). Each module is assigned to a build agent with its contract, its neighbors' contracts and the relevant evidence. Merges are gated by the architect agent against the graph and by the module's contract tests.

**Shell track.** Web, desktop and mobile shells generated from the UI spec and wired to the core. Native capabilities come from the pre-built library, limited to the capability list from Phase 1. Every commit runs on the device farm.

**Backend track.** Only for conventional-backend apps. Day 5 the replay server is live and clients never wait on it. The real backend is built to the Phase 3 contracts, with the traffic corpus as its acceptance suite. Hidden server intelligence is replaced with a documented substitute and flagged in the equivalence report.

Build rules that keep the clock honest:

- No reverse engineering of third-party SDKs. Known SDK means known interface; substitute from the table and move on.
- No feature is built that is not in the inventory, and no inventoried feature is built without evidence attached.
- Scope by observed usage: endpoints and states the exploration runs hit get built; the long tail gets a faithful stub.
- Context is reconstructed from the graph per task; no agent session is expected to last longer than a day.
- A first playable build on all three platforms exists by day 8, however incomplete, so Phase 5 has something to diff.

Outputs: shared core, three shells, backend or replay configuration, all under contract tests, running on the device farm.

## Phase 5: Continuous differential verification (day 8 to ship)

Verification is a running process that starts the day a build exists, not a phase at the end. The harness that explored the original is reused unchanged against the clone, so this phase costs almost no new build effort.

1. Replay every recorded session from Phase 2 against the clone on every commit. Diff accessibility trees (not pixels) and traffic. Pixel diffs run only on the flagship screens defined in the equivalence tiers.
2. The divergence agent runs continuously: it generates inputs intended to make clone and original disagree, and files each divergence as a ticket with a reproduction script. Divergences found per day is the leading indicator; it should peak around day 9–10 and trend toward zero.
3. Triage each divergence against the tiers: must-fix (flagship pixel, any functional), should-fix (structural on a major screen), accept (imperceptible or scoped out). Accepted ones are listed in the final report, never hidden.
4. Regress the golden corpus on every fix. Session pass rate is the progress bar.
5. Run the contract suite against the real backend as it comes online, then switch replay sessions from the replay server to the real backend and re-diff.
6. Final sweep on real devices across OS versions and form factors from the device farm.

Exit criteria for shipping: 95 percent or more of recorded sessions passing at their tier, zero open must-fix divergences, all accepted divergences documented with reason, contract suite green against the real backend.

Outputs: equivalence report with pass rate per tier and per platform, divergence log, accepted-difference list, reproduction scripts for everything still open.

## Phase 6: Delivery, parallel gates and handoff

A working app on all three platforms is delivered inside the window; public store availability may trail by days and is handled by a track that starts on day 1 and never touches code.

**Day-1 paperwork track:** developer accounts, bundle IDs, certificates and provisioning, domains and TLS, payment-processor applications, every third-party API key. Use only vendors with self-serve onboarding or accounts you already hold.

**Week-1 placeholder submission:** submit a minimal real build to both stores to flush out review issues (privacy labels, metadata, age rating, screenshots) while the app is still being built. Resubmission is faster than first review.

**Distribution that does not gate:** web and desktop ship the moment they pass. Mobile goes out through TestFlight, internal testing tracks or enterprise distribution before store approval lands.

**Handoff package:**

- Source for core, shells and backend, with the architecture graph exported as documentation
- Equivalence report, divergence log and accepted-difference list
- The replay scripts and golden corpus, so the owner can keep verifying after changes
- SDK substitution record and licensing notes for every third-party component
- Unreached-target decisions from Phase 2, so nobody rediscovers them later

## Progress metrics and schedule

The combined approach gives a real progress number, which neither approach has on its own. Four metrics are reported daily; the first two are the denominator that blind exploration lacks.

| Metric | Definition | Day 5 target | Day 10 target | Ship target |
| --- | --- | --- | --- | --- |
| Inventory coverage (%) | Inventoried screens, endpoints, states reached by the harness | 85–95 | 95+ | 95+ or scoped |
| Trace understanding (%) | Executed functions assigned to a named module with evidence | 60 | 90 | 95+ |
| Session pass rate (%) | Recorded sessions passing at their equivalence tier against the clone | 0 (no build yet) | 60–75 | 95+ |
| Open must-fix divergences | Count filed by the divergence agent and not yet closed | n/a | peak (20–60 typical) | 0 |

&#91;embedded content: engagement schedule · 6 tracks, 2 milestones\]

Static analysis, exploration and synthesis overlap in week one; build starts day 5 against the replay server; verification starts the day the first build exists and runs to the ship gate. Large apps stretch build and verification to day 28.

## Benefits over either approach alone

Each half fixes the other's defining weakness: static analysis gives exploration a denominator, and exploration tells static analysis which code matters. The harness is built once and used twice, for discovery and for verification.

| Benefit | Harness alone | REA + workarounds alone | Combined |
| --- | --- | --- | --- |
| Logic and data-model accuracy | Low to medium; internals are guessed from outputs | High | High |
| UI and UX fidelity | High | Medium | High |
| Coverage confidence | None; you cannot know what you did not see | Partial; code shows what exists but not what runs | Measurable: targets reached over targets inventoried |
| Decompilation effort | None | Whole binary, or guessed hot paths | Only traced, executed code |
| Hardened apps | Works but shallow | Slowed by obfuscation | Works; exploration carries the load where code is opaque |
| Verification cost | Manual | Divergence agent to be built | Same harness, near-zero extra build |
| Progress visibility | None | Weak | Daily metrics with a real denominator |
| Agent drift on long tasks | Not applicable | High risk | Low; graph plus coverage metric give an objective signal |
| Hidden states (flags, error paths, roles) | Invisible | Visible | Visible and then exercised |

The one place the combination loses is small apps, where it is more machinery than the job needs. A lite profile (bundle scan plus harness, no traces, no graph) covers those.

## Expectations and limits by app class

"Near-identical" means identical on the paths users actually take, at the equivalence tier defined for each screen, with every accepted difference written down. It never means byte-identical, and it never includes server-side logic that was not observable.

| App class | Example | Timeline (all three platforms) | Expected pass rate at ship | What will not be identical |
| --- | --- | --- | --- | --- |
| Small, client-heavy | Utility, single-feature tool | 3–7 days (lite profile) | 97+ | Nothing material |
| Small, with backend | Simple CRUD app | 1–2 weeks | 95+ | Backend internals; rebuilt to contract |
| Medium, conventional backend | Productivity app with auth, sync, payments | 2–3 weeks | 95+ | Third-party SDK behavior where substituted; long-tail states stubbed |
| Large, conventional backend | Content, media, productivity suite | 2–4 weeks | 93–96 | Same as above plus scoped-out unreached targets |
| Large, hidden server intelligence | Marketplace, social feed, fintech | 2–3 weeks to shell; longer for behavior | 85–92 | Ranking, matching, risk and pricing logic replaced with documented substitutes |
| Hardened | DRM, anti-tamper, heavy obfuscation | Add 20–40 percent to the class above | 5–10 points lower | Whatever the harness could not reach and the binary would not yield |
| Subtle-correctness | Collaborative editing, financial reconciliation | Shell in window; equivalence takes weeks longer | 80–90 at window end | Conflict resolution and reconciliation edge cases until the divergence agent converges |

Other expectations to set with stakeholders:

- The first week produces no visible app. It produces evidence and a spec. Stakeholders expecting screens on day 3 will be disappointed; day 8 is the first playable build.
- Divergences peak mid-engagement by design. A rising count around day 9–10 means the divergence agent is working, not that the build is failing.
- Store approval is outside the window. The deliverable is a working, distributable app; public listing follows.
- Real hardware surfaces quirks that simulators hide. Budget the final two days for device-farm findings.
- The estimate is locked at the end of Phase 1, not before. Anything quoted earlier is a range for the app class, not a commitment.

## Roles, tooling stack and cost model

A three-week engagement runs with three to four people and a fleet of agents; humans own decisions, verification judgment and anything legal, while agents own volume.

| Role | Owns | Time |
| --- | --- | --- |
| Lead engineer / architect | App classification, equivalence tiers, architecture graph sign-off, merge vetoes, final report | Full time |
| RE and dynamic-analysis engineer | Static inventory, decompilation of hot paths, Frida and traffic instrumentation, unreached-target decisions | Full time, front-loaded |
| Platform engineer | Shells, capability library wiring, device-farm triage, store submissions | Full time, back-loaded |
| Operations / paperwork (part time) | Accounts, certificates, vendor onboarding, placeholder submissions | 25 percent |
| Agents | Exploration, clustering and naming, contract synthesis, module implementation, divergence generation, regression triage | Continuous |

**Stack (all available today):** REA (rea-agents) for breadth; Ghidra, IDA Pro or Binary Ninja with their MCP bridges for native depth; jadx for Android; Hopper or class-dump for iOS; Playwright, Appium with UiAutomator2 and XCUITest, Android Emulator, iOS Simulator; mitmproxy, Frida, Chrome DevTools Protocol; Temporal or Argo Workflows; a vision-capable model API; OpenCV and Airtest for canvas and game surfaces; Hypothesis, fast-check or Schemathesis for contracts; a graph database or structured repo for the architecture graph; Kotlin Multiplatform, Flutter, React Native or Tauri for the shared core; BrowserStack, Firebase Test Lab or AWS Device Farm; S3-compatible storage; PostgreSQL and Grafana for metrics.

**Cost per engagement (excluding the one-time factory), approximate, USD:**

| Line | Medium app | Large app |
| --- | --- | --- |
| Agent and vision-model usage | 3,000–8,000 | 8,000–25,000 |
| Emulator, VM and device-farm compute | 1,000–3,000 | 3,000–8,000 |
| Tool licenses (IDA, Binary Ninja, Hopper, device farm) | 1,000–3,000 | 1,000–3,000 |
| Third-party service substitutes (first month) | 500–2,000 | 1,000–5,000 |
| People (3.25 FTE for 3 weeks, loaded) | 45,000–75,000 | 45,000–90,000 |

People dominate. The factory's purpose is to keep them at 3–4 regardless of app size; without it the large-app line is a multiple of that.

**One-time factory:** 6–10 weeks for two to three engineers, roughly 100,000–250,000 USD loaded, amortized across every engagement after the first.

## Risks, legal considerations and go/no-go checklist

The technical risks are bounded by the metrics above; the legal and ethical risks are not, and they are checked before any build is downloaded.

**Legal considerations (not legal advice; confirm with counsel for your jurisdiction):**

- Reverse engineering for interoperability, security research and preservation is treated differently from reproducing a competitor's product for commercial release. The purpose shapes what is defensible.
- EULAs and terms of service often prohibit reverse engineering and automated access. Automated exploration at scale against a live service may breach terms, rate limits or anti-abuse rules even where decompilation is permitted.
- Copyright covers code and assets; trade secrets may cover non-public server logic; patents may cover specific methods; trademarks cover names and branding. A clone that substitutes its own code, assets and brand avoids some of these and none of them automatically.
- Third-party SDKs carry their own licenses and cannot be redistributed by analyzing them.
- Keep evidence records. Structured, dated evidence of what was observed and how is both a quality control and a defensibility measure.

**Technical risks and mitigations:**

| Risk | Signal | Mitigation |
| --- | --- | --- |
| Backend logic invisible | Many endpoints with responses that cannot be derived from inputs | Classify as hidden-intelligence in Phase 1; substitute and flag; do not promise identical |
| Exploration stalls | Inventory coverage flat under 70 percent by day 4 | Provision access (roles, tiers, hardware); convert to scoped-out decisions; do not extend blindly |
| Agent drift | Merges rejected by architect agent rising; contradictory modules | Shorten agent task scope; reconstruct context from graph; add contract tests |
| Divergences not converging | Must-fix count flat after day 14 | Re-tier (some are structural, not functional); isolate to one module; accept and document if imperceptible |
| Simulator-only validation | Device-farm failures late | Device farm from day 5, not day 18 |
| Vendor gates | Any API key or account pending after week 1 | Swap to a self-serve vendor from the substitution table |

**Go/no-go checklist (complete before Phase 1):**

- [ ] Purpose documented and reviewed by counsel (own legacy app, interoperability, preservation, authorized research, or other with sign-off)
- [ ] Terms of service and EULA reviewed for the target; automated-access limits understood
- [ ] Builds for all three platforms obtained legitimately
- [ ] Test accounts and data that do not touch real users or production data of others
- [ ] Factory acceptance test passed on a reference app within the last 90 days
- [ ] App class and estimate range agreed as a range, with the locked estimate due at end of Phase 1
- [ ] Equivalence tiers and accepted-difference policy agreed in principle
- [ ] Day-1 paperwork track staffed and started
