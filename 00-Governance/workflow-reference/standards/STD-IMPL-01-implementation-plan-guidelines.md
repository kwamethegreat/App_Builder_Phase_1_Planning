---
id: STD-IMPL-01
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "LOOP-GUIDELINES.md"
---

# LOOP-GUIDELINES.md — replicating the perpetual build loop for a new application

**Written 2026-09-27 from the App Builder project's loop as it stood at batch 75 (plan step 1186 pending; batch 74's escalation unrecovered — `state.json` reads `next: 74`).** Every mechanism below carries three things: what it is, the failure it exists to prevent (batch and finding cited), and the command that proves it is working in the new environment. Text quoted from the gathered files is verbatim; prose around it is the author's. Anything the gathered output did not cover is marked `[UNVERIFIED — needs <command>]`. Target platform: native Linux.

**Generic vs specific, stated once:** "GENERIC" means transfer unchanged; "SPECIFIC" means it encoded the App Builder's plan, contract or domain and must be re-authored. Each section says which.

## Manifest of parts

| § | Section | Status |
|---|---|---|
| 1 | Read this first | this file |
| 2 | Prerequisites and host setup | this file |
| 3 | Repository skeleton | this file |
| 4 | How to author the implementation plan | this file |
| 5 | The loop | this file |
| 6 | The advisor | this file |
| 7 | Claude Code guardrails | this file |
| 8 | Session conventions | this file |
| 9 | Human-gate posture | this file |
| 10 | Operating procedures | this file |
| 11 | Pitfall register | this file |
| 12 | Day-one checklist | this file |
| 13 | What is not settled | this file |

---

## 1. Read this first

### 1.1 The system in one page

An externally authored, step-indexed implementation plan (thirteen parts, steps 1001–2470 in the source project) drives two Git repositories that share a pinned contract wheel. A driver script launches one headless Claude Code session per **batch**; the session executes a **span** of plan steps, runs four quality gates in the foreground, writes a report, and stops unmerged. A deterministic checker (`complete.py`) verifies mechanics and classifies the diff against a **human-merge list**. A single model call (`advise.py`, with a pinned brief as its system prompt) rules the routine judgment, decides PROCEED / ESCALATE / HALT / PART_END, and writes the next prompt. On PROCEED with a mergeable classification, the driver runs the human's own merge script under standing order. Everything on the human-merge list stops the loop for a person; a growing set of **exemptions with mechanical proofs** takes classes of change off that list without removing the list.

Observed cadence at batch 75: 50–100 minutes per batch (session 30–70 min, gates 17–25 min, advisor ~2 min); one batch cost $19.59 in API spend (`sessions/batch-74.json: total_cost_usd`). Part 02's back half: 22 steps in 15 batches with five stops, four forced by the list and one chosen.

### 1.2 The division of labor — an invariant

| Role | Who | Does | **Never does** |
|---|---|---|---|
| Builder | one headless session per batch: `claude -p "<prompt>" --permission-mode bypassPermissions --output-format json`, cwd = control plane, `ANTHROPIC_API_KEY` unset | executes the span; records, findings, STATUS entries, per-step commits; runs gates; writes the report; pre-reads the next span | merge, push, mirror, launch `claude`, edit `~/.claude`, read `.env`, write the project root, write the kill file or `loop.conf`, write under `.loop/` other than its own report |
| Advisor | `scripts/loop/advise.py`: one API call, brief = `docs/ADVISOR-PROMPT.md`, default model `claude-sonnet-5` (`LOOP_ADVISOR_MODEL` / `--model`) | reads report + mechanics; rules routine judgment; decides; tables questions; writes the next prompt | build, merge, edit files, resolve a halted session's question, tune a ruling to make a red go green |
| Decider | the human plus an advisory chat thread | rules the novel: escalations, brief amendments, precedent, part boundaries, digest review | run commands (the human does) |
| Human | you | `.env`, `~/.claude/`, `~/bin/`, the API-key file, placing and landing plan authorities, the root `plan/`, the merge (by your own script), credits | — |

The rules file states the driver-side half structurally: *"the loop's scripts never invoke `make merge`, `git push`, `claude`, or write under the host's hook directory — asserted structurally, argv- and literal-derived, by `tests/structural/test_loop_scripts_hold_no_merge_push_or_claude.py` in the control plane, planted both directions."*

### 1.3 The halt bar, quoted (brief §5)

> A batch halts on: a decision with no precedent; an immutable artefact that would be got wrong (migrations, contract schemas, committed hashes, plan pins, host-guard references); or a correctness defect. NOT on a finding that can be logged, a defect that can be fixed, or a guard whose scope can be narrowed. The bar drifts wider on its own; hold it narrow.
>
> Your escalation bar is the same bar, read for the next span: an escalation is a halt the next session would otherwise have to make. If the next session, holding your ruling, would not halt — because the ruling gives it a precedent or a reading to record — then you do not escalate; you rule.

Failure this prevents: batches 41–42 stopped four times on routine judgment (three of them with a direct precedent) before A11 rewrote §4. A wide bar costs a stop per batch; a narrow bar with digest review costs one batch of revertible branch work per wrong marginal call.

---

## 2. Prerequisites and host setup (native Linux)

Ordered. Each row: what, why, check.

| # | Item | Why (failure prevented) | Check |
|---|---|---|---|
| 1 | Two repository checkouts as siblings under one parent (`<parent>/<cp>`, `<parent>/<ws>`); `step-open.sh` and `find-sibling.sh` walk up to four parents to find the twin; `AGENT_LOOP_CONTROL_PLANE_ROOT` / `AGENT_LOOP_WORKSPACE_ROOT` override | asymmetric execution (one repo branched, the other not) — `step-open.sh` header | `make -C <cp> step-open` prints both repos |
| 2 | `git` with `origin` and a `gitea` mirror remote; `make merge` = `check ci-local commit-lint` → ff-merge → `git push origin main` → `scripts/mirror-push.sh main` → `scripts/gitea-post-status.sh success check` → branch delete | a mirror that silently never received a push (batch 146–149 ledger entry: the workspace mirror sat 36 commits stale while every merge "succeeded") | `git -C <cp> remote -v`; `mirror-push.sh` fails on a reachable mirror that did not receive the push `[UNVERIFIED — needs cat scripts/mirror-push.sh]` |
| 3 | `uv` (0.11.x at the source project); `hatchling` pinned exact in both `[build-system]` (finding 284) | a wheel rebuild that changes bytes because the backend moved on an unrelated `uv sync` | `uv --version`; `grep hatchling <cp>/pyproject.toml <cp>/contract/pyproject.toml` |
| 4 | **`uv --no-config` for every scratch install** | finding 324: `[tool.uv] find-links` discovered from the working directory shadowed the scratch `--find-links`; a planted stale install installed the current wheel twice | any scratch drive prints the installed `BUNDLE_SHA256` *before* asserting |
| 5 | Docker + Compose, `--project-name` per repo; Postgres for scratch databases; `act` for `make ci-local` | two checkouts addressing the same compose project; `ci-local` runs under `act` as root (batch 224 root-skip lesson) | `docker compose version`; `act --version` |
| 6 | `jq` — the host guard exits 2 (blocks everything) without it | fail-closed by design: `GUARD BROKEN: jq missing, refusing to allow unchecked` | `command -v jq` |
| 7 | `~/.claude/settings.json` with the hooks stanza and permissions (§7.1), `~/.claude/hooks/guard.sh` + `show-commit.sh` executable, installed by `infra/host-guards/install.sh` from the tracked reference | finding 313: a guard that is correct, wired and never invoked | `tail -n 3 ~/.claude/guard-invocations.log` fresh after any tool call; `uv run pytest tests/unit/test_host_guard_parity.py` |
| 8 | `~/bin/loop.sh`, `~/bin/merge-and-sweep.sh`, `~/bin/loop-preflight.sh` (mode 755), `~/bin/loop.conf` (**mode 600** — it holds the ntfy token; the source machine had it at 644 until batch 58) | — | `ls -l ~/bin/loop.conf` |
| 9 | `~/.config/agent-loop/anthropic-api-key` (600); read only inside `advise()` in `loop.sh`: `advise () { ANTHROPIC_API_KEY="$(cat "$API_KEY_FILE")" python3 "$CP/scripts/loop/advise.py" "$@"; }`; sessions run `env -u ANTHROPIC_API_KEY claude -p …` | the session uses the Claude Code login, never the key; the key touches one process | `env \| grep -c ANTHROPIC_API_KEY` in a session shell → 0 |
| 10 | **Automatic credit reload** on the Anthropic console, threshold above one night's spend (~$50–80 at $3–20/batch) | batch 59: `terminal_reason: api_error` 89 seconds in — the only stop in the run the loop could not have avoided | console setting; usage alert email |
| 11 | `tmux` for the driver; ntfy topic + token in `loop.conf` | a closed terminal kills a bare `loop.sh`; notifications reach a phone | `tmux ls`; `loop-preflight.sh` step 6 posts `loop: preflight` |
| 12 | Node only in the workspace (commitlint); **the control plane takes no npm dependency** (supply-chain: it brokers credentials and owns guards) | `test_control_plane_stays_node_free.py` | `ls <cp>/package.json` → absent |

GENERIC: all of it. SPECIFIC: the compose service set, the repo names in `find_sibling`.

---

## 3. Repository skeleton

### 3.1 Two repositories, one contract

| Piece | Location | Mechanism |
|---|---|---|
| Control plane (CP) | `<parent>/<cp>/` | orchestrator, DB, contract package, guards, plan documents, loop tooling under `scripts/loop/` |
| Workspace (WS) | `<parent>/<ws>/` | runner side; mirrored tests; own STATUS; own gates |
| Contract wheel | `<cp>/contract/` (source), `contract-wheelhouse/` in **both** repos (committed, byte-identical, swept) | `make contract-build`: generate models → golden fixtures → `bundle_hash.py` → `uv build --wheel --offline` → copy to sibling → `cmp` → reinstall (`uv sync --dev --reinstall-package agent-loop-contract`); the WS must reinstall itself |
| `contract.lock` | repo root, both repos, byte-identical | `{"version": "0.1.0", "bundle_sha256": "sha256:<64 hex>"}` — one digest over `schemas/`, `openapi/`, `fixtures/golden/` |
| Pin test | `tests/contract/test_contract_pin.py` (mirrored) | installed `BUNDLE_SHA256` == this repo's lock (local staleness); cross-repo agreement is the parity sweep's (`contract.lock` is at `.`, which is swept) |
| Wheel currency | `tests/unit/test_contract_wheel_is_current.py` (CP) | parses the Makefile's own `uv build … --offline` line, rebuilds into scratch, byte-compares to the committed wheel |
| Tree→lock edge | `tests/unit/test_contract_lock_pins_the_tree.py` (CP, step 1177) | recomputes the manifest over the three trees via the package's own `hashing.manifest`/`bundle_hash` and holds it equal to the lock |

Lock discipline (E-13): every schema change moves `contract.lock` in both repos **in the same commit pair**, scratch-built and byte-compared before belief. Forty-seven movements in Part 02, identical digest sequences in both repos (batch 70). SPECIFIC: the schema families. GENERIC: the triangle of tests.

### 3.2 Mirrors and parity

`tests/unit/test_shared_config_parity.py` (WS) holds the shared `[tool.ruff]`, `[tool.mypy]`, `[tool.pytest.ini_options]` blocks identical modulo package name, `MIRRORED_PATHS` byte-identical, `SWEPT_DIRECTORIES` (including `.` and `contract-wheelhouse`) identical, with one-sided rows declared for CP-only tests. Locates the sibling by env var, then ancestor search, else **skips with a reason** (never a silent pass). `[UNVERIFIED — needs sed -n '40,120p' <ws>/tests/unit/test_shared_config_parity.py for the exact constants]`

`docs/CROSS_REPO_CLAUDE.md` is byte-mirrored in both repos and parity-gated; an edit is a both-repo commit pair and a human-merge stop.

### 3.3 The pins

`tests/unit/test_plan_citations.py` in **both** repos carries (line numbers from the source project):

```
ROADMAP_SHA256 = "<64 hex>"          # the roadmap
ADDENDA_SHA256 = "<64 hex>"          # the addenda
HANDOFF_SHA256 = "<64 hex>"          # the handoff
ADVISOR_PROMPT_SHA256 = "<64 hex>"   # the brief (moves under A10; NOT a human-merge item)
PLAN_SHA256 = {                      # every file under docs/plan/, key = docs/plan-relative path
    "ACCOMMODATION-REGISTER.tsv": ("<64 hex>"),
    "DISPOSITION-REGISTER.tsv": ("<64 hex>"),
    ...
}
```

`loopcore.plan_mapping` parses the literal: entries `"key": "hex"` or `"key": ("hex")`, ending at the first bare `}`; comments carry no quoted 64-hex. A pin movement is any `+`/`-` line matching `^[+-](?!\+\+|--).*"[0-9a-f]{64}"` in that file (`_PIN_LINE`); the advisor pin's line is split off by `ADVISOR_PIN_LINE`. Re-pin comments beside each entry record the step and reason (the 1163/1168/1173/1174 form). GENERIC.

### 3.4 Documentation surfaces every mechanism reads

| Path | Purpose | Read by |
|---|---|---|
| `docs/STATUS.md` (both) | one entry per batch, `  **Batch N**` heading (`_BATCH_HEADING = r"^  \*\*Batch [^*]+\*\*"`), `- **Current step:** NNNN` (`_CURRENT_STEP`) | advise.py (`current_step`, `latest_batch_entry`), the deferred register's test |
| `docs/BATCH-FINDINGS.md` (CP only — the WS has none) | `## Finding NNN — …` | advise.py (`findings_tail`, 5 entries / 40 000 chars) |
| `docs/recon/NNN-<slug>.md` | records; opens with a fenced `bash` block of the command run | `test_recon_records_carry_their_command.py` |
| `docs/gates/PHASE-Pnn-{A,B}-<slug>.md` | phase gate pairs | `test_gate_documents_pair.py`; A26 |
| `docs/plan/` | landed plan (§4) | `PLAN_SHA256`; `complete.py` |
| `docs/DEFERRED-ESCALATIONS.md` | the tabled-questions register (§6.4) | advise.py, digest.py, its own test |
| `docs/DECISIONS/NNNN-*.md` + `README.md` index | ADRs; `scripts/new-adr.sh` allocates; `ADR_RENUMBERED` maps plan-named numbers to allocated ones | `test_adr_index_matches_the_records.py` |
| `.loop/` (CP, gitignored — `loop-preflight.sh` step 2 checks `^\.loop` in `.gitignore`) | `state.json`, `prompts/`, `reports/`, `verdicts/`, `merges/`, `sessions/`, `digest-running.md`, `DIGEST-through-N.md`, `STOP`, `MERGE-APPROVED-N` | the driver |

---

## 4. How to author the implementation plan

The next conversation starts here. Everything in this section is enforced by a script or test in the source project; the plan must be conformant *before* it is landed, because the landing pins its bytes.

### 4.1 Part and step structure

- One file per part: `PLAN-PART-NN-<slug>.md`. Steps are level-3 headings matching `STEP_RE = ^### (\d+)\. `\[([a-z.]+)\]` (.+?)$` — number, backticked tag, title.
- Per-step fields, each a bullet `- <field>: <value>`, parsed by `FIELD_RE = ^- (produces|depends_on|verify|risk|covers|disposition|host): (.*)$`. **All seven are required** (self-check: `missing field`).
- `risk:` is `yes` or `no`. `host:` is one of `any | current | current-degraded | new-required`, optionally followed by ` — <note>`; a `current-degraded` host must name an `RCAP-nn` re-capture obligation.
- `depends_on:` names earlier steps that exist in an authored part (self-check: `depends_on N exists in no authored part`; `not numerically earlier`).
- **The `flag` column never appears in the prose** (`flag must not appear in the authority`). It is the one judgment the prose cannot yield and lives in the pinned generator's `FLAGS` map (`docs/plan/derive-plan-shards.py`): `impl` (pure construction), `decision` (the advisor rules it unless it meets an escalation class), `unsure` (density uncertainty). A1/A21: `unsure` *"neither closes a span nor requires a pre-issued ruling"*. `[UNVERIFIED — flag semantics for the shard's consumer of `decision` steps: needs grep -n 'decision' <cp>/scripts/loop/loopcore.py]`
- Steps are numbered contiguously across parts (the source plan: 1001–2470, Part 07 starting exactly at Part 06's last step + 1). The self-check refuses `range mismatch`.
- `produces:` paths are stated as `` `CP/<path>` `` / `` `WS/<path>` `` in backticks. **A register the step writes must be named exactly as `` `CP/docs/plan/<NAME>.tsv` ``** — `_PRODUCES_REGISTER = r"`CP/docs/plan/([^`/\s]+\.tsv)`"` is what A28 reads; a register named through an elided prefix is not named (rules file: *"a produces cell naming a register only through an elided `.../` prefix does not name it here — the file stays the human's"*).

### 4.2 Risk tagging is span sizing

A `risk: yes` step closes its batch (inclusive). The evidence:

| Part | Steps | risk: yes | Batches (observed or projected) |
|---|---|---|---|
| 02 | 100 | 34 | 52 batches (observed, batches 18–70) |
| 03 | 120 | 63 | ~96 spans at minimum (batch 71 inventory: 12 multi-step, 84 single) |
| 07 | 70 | 41 (59%) | ≥ 41 batches |

Guidance: tag `risk: yes` only where a wrong execution would be irreversible or expensive (a schema on the wire with a corpus, a migration, a pin, a guard narrowing). A risk tag on a step whose artefact is revertible branch work buys nothing — per-batch merging already bounds the blast radius to one batch — and costs a full batch (~70 min, ~$10–20). Aim for 25–35% risk density; 59% roughly doubles the part's calendar time. A gate pair, a plan landing, a pin movement and a guard re-sync are solo regardless of their tag (§4.4), so tagging them `risk: yes` is redundant.

### 4.3 The solo list (rules file, loop discipline, verbatim)

> A session executes exactly one batch — the §10.2 span the shard allows, ending at the first `risk: yes` step (inclusive) or before any solo-list step (decision flag, plan landing, guard re-sync, phase gate, pinned-hash movement, contract-lock cutover; an `unsure` flag is density uncertainty (A1): it neither closes a span nor requires a pre-issued ruling; a `decision` flag is solo.)

Note the distinction the source project learned at batch 72: **solo ≠ human-merge**. A28 made register steps self-land but they still run as one-step batches (a batch, not a stop). A `contract.lock` movement is *not* on the solo list (the batch-46 precedent, restated at every lock-moving batch) — an early advisor verdict (batch 50) wrongly called 1152 "a pinned-hash movement" and was corrected by the session.

### 4.4 Authoring rules with their erratum text

| Rule | Erratum / finding | Text to obey |
|---|---|---|
| `covers:` enumerates identifiers, never ranges | E-09 | *"A `covers:` field **may not contain a range**. Identifiers are enumerated. The coverage shard generator refuses a field containing a range notation … A range in a `covers:` field is a count beside a list in disguise."* The generator refuses `…` or `...` in `covers`. The source plan had 23 such ranges across Parts 08–12, fixed on the root with a 20-line expander before those parts could be parity-proven. |
| The lock moves per schema step, not once at the part's publication step | E-13 (finding 301) | *"each schema-bearing step moves the lock in-batch; 1177 verifies the lock's history"* — write publication steps as verification, never as "move the lock". |
| Built vocabularies win over a source document's DDL | E-14 (finding 302); ADR 0014 | *"the built set is migration-proven and live … A-02's principle — the existing schema's forms win over the handoff's DDL — applies at the vocabulary level"*. Do not author a plan step that transcribes a vocabulary the codebase already pins differently; say "anchor the built vocabulary". |
| Counts are derived from lists, never written beside them | E-18 (finding 140's class) | *"'six' is a count beside a list … No member is added to satisfy the arithmetic."* Never write "the N tools/tables/guards" in a verify clause; write "membership against the named set, the count computed". |
| Registers the plan directs sessions to write are **derived** | A25 → A28 → A30 (batches 56–74) | see §4.6 |
| A step names its record number | record numbering | plan-named record numbers collide with the live sequence (the `049` → `140` form, eleven times); write "the next free record number" or none. Files under `docs/recon/` are numbered by the sequence, never by the plan. |
| Nominal paths | the filename/tag nominal precedent (§6 of the brief) | a plan path that collides with the built layout is nominal; the built convention governs and the mapping is recorded (`schemas/<family>/<name>.schema.json` for the plan's flat `schemas/<name>.json`; in-wheel `conformance/`; the flat golden corpus). Write plan paths loosely or in the built convention; do not fight it in verify clauses. |
| A verify clause must be executable from held sources | A20, finding 321 | *"a deferral premised on the plan's NOMINAL … path — never tracked and never to be — so it would have skipped forever"* — a verify clause that premises on a path must premise on the path as built. |

### 4.5 `covers`, records and citations

- `covers:` identifiers are the coverage universe (RQ-nn, RC-nn, NC-nn, OV-nn, X-n, `Part 00 §n.n`, `handoff §n.n`). `derive-plan-coverage.py` re-derives the coverage shard from every step's `covers:` at test time; *"a hand-added identifier present in no step's `covers:` field is refused by name."*
- Every citation of a step, test, record or section in any tracked prose is checked: `test_plan_citations.py` (steps), `test_test_citations.py` (test identifiers — *"a test name in prose is a claim that a mechanism exists"*), the addendum-citation guard, the record-command guard. Phantom citations were 6 in 111 on the first sweep. Plan prose that names a test names an obligation the step must discharge under that exact name — or the step must record the rename.

### 4.6 Design registers as derived from day one (the A25/A28/A30 lesson)

The source project discovered at batch 56 that three Part 02 steps edit `INCORPORATED-BY-REFERENCE.tsv` under `PLAN_SHA256` — three forced stops — and exempted that one file (A25, batch 58). At batch 71 it found eighteen Part 03 steps write under `docs/plan/`, sixteen human-merge by construction, and generalised to any produces-named `*.tsv` (A28, batch 72). At batch 74 it found a register (`MIGRATION-GUARD-COVERAGE.tsv`) that is re-derived by every migration step without any of those steps naming it — 43 stops — and added derived registers (A30, batch 75). Each discovery cost a rules-file stop and a tooling batch.

For the new plan, decide at authoring time, per plan-side register:

| Kind | Definition | Self-lands when (complete.py) | Plan authoring requirement |
|---|---|---|---|
| **Produces-named** (A28) | a `docs/plan/*.tsv` a step writes as its own product | only that file changed under `docs/plan/`; header unchanged; no row removed; every added/changed row cites a step inside the span (`_STEP_TOKEN = (?<![\w.])(\d{4})(?!\w)(?!\.\d)` — four digits, not a section number); pin moved in both repos to the landed bytes; no other pin moved; nothing else on the list moved | every writing step's `produces:` names `` `CP/docs/plan/<NAME>.tsv` ``; every row carries its step number |
| **Derived** (A30) | a register that is a function of a source tree and re-derived whenever that tree changes | declared in the rules file under `### Derived registers (A30)` as `register\|source tree\|deriving test`; the batch changed the source tree; the deriving test is present and the gates green; header unchanged; pin moved in both; nothing else moved | the creating step's verify clause states the derivation and names the deriving test; **the rules file's table is authored at genesis with every derived register the plan will create**, so no step later meets A30 as a discovery |
| **Human's** | plan text, the shards, `PLAN-CARRY.md`, `PLAN-MANIFEST.md`, `ERRATA.md`, any `docs/plan/*.md` | never | write these into part-boundary steps only (the carry rewrite and re-pin, `1179`'s form) |

`[UNVERIFIED — A30's implementation as built in batch 75: needs sed -n on loopcore.py after batch 75 lands]`

### 4.7 The index shard is a derived artefact

- `docs/plan/index/part-NN.tsv`, pipe-delimited `step|tag|flag|risk|produces|depends_on|verify`, produced by the pinned `docs/plan/derive-plan-shards.py` and re-derived by `scripts/derive-plan-index.py` (the flag copied through), the two held equal row-for-row by `test_plan_index_parity.py` — *"two implementations of one derivation are acceptable **only as a checksum**"*. Coverage and hardware shards are derived at landing (`derive-plan-coverage.py`, `derive-plan-hardware.py`; the hardware shard's gate is `test_recapture_obligations_are_bound.py`).
- Generator CLI: `python3 derive-plan-shards.py <part-file> <NN> <lo> <hi> <out-dir>`; writes `<out>/index/part-NN.tsv`, `<out>/coverage/part-NN.tsv`, `<out>/hardware/part-NN.tsv`; its self-check reads prior parts' index shards from `<out>/index/` for cross-part `depends_on`, so **seed the scratch out-dir with a copy of the plan root**, and delete the part's own shard from the scratch before running so a BYTE-IDENTICAL verdict can only come from a fresh write (the source project's first parity run reported identity against its own seeded copy — a false positive).

### 4.8 Placing and proving a part (Linux)

```bash
ROOT=<project-root>/plan                         # the human's authoring copy, outside both repos
# 1. place PLAN-PART-NN-<slug>.md and index/part-NN.tsv (from wherever authored)
# 2. line endings and shape
file "$ROOT"/PLAN-PART-NN-*.md "$ROOT"/index/part-NN.tsv | grep -c CRLF        # 0
wc -l "$ROOT"/index/part-NN.tsv                                              # steps + 1
awk -F'|' 'NR>1{print $3}' "$ROOT/index/part-NN.tsv" | sort | uniq -c        # flag distribution
awk -F'|' 'NR>1{print $4}' "$ROOT/index/part-NN.tsv" | sort | uniq -c        # risk density
awk -F'|' 'NR>1{print $1}' "$ROOT/index/part-NN.tsv" | sort -n | sed -n '1p;$p'  # contiguous with the previous part
# 3. parity, fresh write only
SCRATCH=$(mktemp -d); cp -r "$ROOT"/. "$SCRATCH"/; rm -f "$SCRATCH/index/part-NN.tsv" "$SCRATCH/coverage/part-NN.tsv"
python3 "$SCRATCH/derive-plan-shards.py" "$SCRATCH/PLAN-PART-NN-<slug>.md" NN <lo> <hi> "$SCRATCH"; echo "exit $?"   # 0, no SELF-CHECK FAILURES
cmp "$SCRATCH/index/part-NN.tsv" "$ROOT/index/part-NN.tsv" && echo BYTE-IDENTICAL
```

An exit 1 names the defect (E-09 ranges, missing fields, bad host class, unknown `depends_on`). Fix on the root; nothing is pinned until landing.

### 4.9 Landing under A27 — the part's first batch

Verbatim from A27: *"A part's landing (root → docs/plan/ byte-identically with its index shard, the coverage and hardware shards derived by the repo-side scripts and byte-agreed with the pinned generator in scratch, every file pinned in both repositories in one commit pair, the manifest's part row updated; record 045's form, the 1072/1073 shard precedents) is the first batch's opening act and a human-merge stop."* The same batch carries the part's **class-(2) inventory** (every type, vocabulary, grammar or member the produces/verify clauses require that no held source defines, with candidate readings and the A20 clause covering each, plus the phase-gate, register and plan-event steps) so the decider rules the whole part at that one stop.

Failure prevented: finding 303 — landing Part 03 ahead of execution tripped `test_every_current_degraded_shard_row_names_a_held_obligation[03]` because a row named `RCAP-02` before step 1200 registered it; the first landing (batch 20) was reverted. A27's rule: a guard whose premise is "held by an executed step" admits the row *premised on the registering step, failing closed at the batch that executes it without registering*. The same shape hit the carry gate at batch 71 (a landed-not-carried part). **Author every guard over plan-side registers with the landed-but-unexecuted premise from the start.**

### 4.10 What the plan must say so events land as solos

- **Phase gate pairs**: a step whose `produces:` is exactly `CP/docs/gates/PHASE-Pnn-A-<slug>.md` and `-B-<slug>.md` (`GATE_PAIR_NAME = ^PHASE-(P\d{2})-([AB])-([a-z-]+)\.md$` — lowercase slug, hyphens only); verify: *"every test this phase produced passes, each recorded with its command; Half B names each mechanism observed REFUSING … and states what adjacent case it does not cover"*. Under A26 it self-lands; it is still solo.
- **Guard re-syncs** (`infra/host-guards/`): human-merge, solo, never exempted.
- **Pin movements** other than a register's: solo and human-merge (the carry rewrite and re-pin at the part's close, the landing).
- **The part close**: one step for the carry rewrite + manifest + re-pin (`1179`'s form: regenerate shards expecting byte-identical, rewrite the carry from a build script, generalise the carry gate, move `PLAN_SHA256` for exactly the changed files), then the final gate pair (PART_END).

GENERIC: §4.1–4.10 entirely, with the identifier prefixes (RQ/RC/NC/OV/X) SPECIFIC.

---

## 5. The loop

### 5.1 `state.json` and the iteration

`state.json` = `{"next": "<N>", "awaiting_human_merge": "" | "<N>", "pending_tip_cp": "<sha>"}`. The driver's loop (from `loop.sh`, verbatim structure):

```
while true:
  STOP file present → notify, exit 0
  BATCHES_RUN ≥ MAX_BATCHES or hours ≥ MAX_HOURS → exit 0
  awaiting_human_merge non-empty → notify "run --resume after merging", exit 0
  N = next; require prompts/batch-N.md (else exit 1)
  ( cd CP && env -u ANTHROPIC_API_KEY claude -p "$(cat prompt)" --permission-mode bypassPermissions --output-format json ) > sessions/batch-N.json
  report missing/empty → notify "produced no report — stopping", exit 1        ← hardening owed (§5.6)
  complete.py → verdicts/batch-N-complete.json; exit ∉ {0,3} → exit 2
  advise → verdicts/batch-N.json; append digest_line to digest-running.md
  PART_END → exit 0; ESCALATE|HALT → exit 2 (nothing merged, A6)
  exit 3 → set awaiting_human_merge=N, pending_tip_cp=HEAD; exit 0
  merge_and_advance: MERGE-APPROVED-N marker → merge-and-sweep.sh → (on failure: advise --classify-merge-failure, retry once if TRANSIENT and < 2 fails) → next_prompt → prompts/batch-(N+1).md → next=N+1 → digest every DIGEST_EVERY (6) or on "PHASE GATE" in the report
```

Modes: `--bootstrap` (advisor over the last report on file, writes the first prompt), `--resume` (verifies `pending_tip_cp` is an ancestor of `main`, runs `merge-and-sweep.sh` silently, writes `merges/batch-N.txt` = "human merge of batch N verified on main", advisor `--post-merge`, next prompt, clears the flag, continues), `--dry-merge N` (exercises `merge_and_advance` against scratch state/prompt paths with a synthetic PROCEED), plain `run`.

`merge-and-sweep.sh`: CP then WS, each `make merge` into `~/merge-logs/merge-<name>-<stamp>.log`, refusing a dirty tree, requiring a `Deleted branch` line; then a branch sweep and an **ancestor unwind** (deletes any branch whose tip is on `main`; aborts on one that is not). Skips a repo already on `main`.

### 5.2 `complete.py` — the mechanics (from its docstring, numbered assertions)

1–5: all four quiet-gate logs green by content (`_COUNT_LINE = \b\d+ (?:passed|xfailed)\b`; `_MAKE_ERROR`; `Job succeeded`/`_JOB_FAILED` for ci-local); each gate's `.gate-logs/<gate>.started` stamp at or after the final commit in **both** repositories; both trees clean; report line 1 `STATUS: COMPLETE`; line 2 `HUMAN_MERGE: (yes|no) — <reason>` (`_HUMAN_MERGE_LINE`) agreeing with the independent classification (`classify_human_merge` over both repos: `HUMAN_MERGE_PREFIXES`, `HUMAN_MERGE_EXACT`, and every pin movement except the advisor pin's — `[UNVERIFIED — the constants' values: needs grep -n -A6 'HUMAN_MERGE_PREFIXES\|HUMAN_MERGE_EXACT' loopcore.py]`).
6 (A10): a moved brief or advisor pin → the landed copy byte-identical to the root and the pin naming its digest, else exit 1 naming both digests.
7 (A25→A28): register self-landing, hits split off when every condition is met.
8 (A26): gate-pair self-landing, composed after 7.

Exit codes: `EXIT_MERGEABLE = 0`, `EXIT_NOT_COMPLETE = 1`, `EXIT_HUMAN_MERGE = 3`. Unmet exemption conditions are appended to `reasons` as `register self-landing (A28) not earned: …` / `gate pair self-landing (A26) not earned: …`.

### 5.3 The human-merge list

Rules file, verbatim: *"Any change under `infra/host-guards/`, **including settings-reference re-syncs** …; the pinned plan documents under `docs/plan/` (landings and re-landings); any `PLAN_SHA256`, `ROADMAP_SHA256` or scalar pin movement in either repository's `tests/unit/test_plan_citations.py` **except `ADVISOR_PROMPT_SHA256`**; … [A28 and A26 exceptions] … and this file."* Phase-gate pairs under `docs/gates/` were on it until A26.

### 5.4 Every exemption

| Amendment | What self-lands | Exact conditions (complete.py) | Planted proofs (test_loop_complete.py) |
|---|---|---|---|
| **A10** (batch 45) | `docs/ADVISOR-PROMPT.md` + `ADVISOR_PROMPT_SHA256` | landed file byte-identical to the root `plan/ADVISOR-PROMPT.md` (found beside the repositories or via `AGENT_LOOP_ROOT_BRIEF`); the moved pin == sha256 of the landed bytes in each repo; a root that cannot be found → exit 1 | byte-identical landing → 0; one byte changed → refused naming both digests; pin to a foreign digest → refused; no root → refused; a batch not touching the brief never consults the root; other pins beside the brief still stop |
| **A25→A28** (58→72) | produces-named `docs/plan/*.tsv` registers | (1) every `docs/plan/` change is a top-level `.tsv` named in the span's steps' `produces` (span from the report H1 via `report_span`; produces from the **landed** index shard at HEAD; a step with no shard row names nothing); status `A` or `M` only; the WS changes nothing under `docs/plan/`; (2,3) header unchanged, no row removed (keyed by first cell), every added/changed row cites a four-digit step inside the span; (4,5) the mapping entry for exactly those registers moved/added in both repos to `sha256_of(landed)` and no other entry moved; (6) no other human-merge hit | all-five-met → 0; multi-step span admits any span step; second plan document beside it → 3; pin in one repo only → 3; row citing outside the span → 3; row citing no step (`§5.6`, `10.4`, `v1.1` are not steps) → 3; header changed / row removed → 3; second entry moving / wrong digest → 3; unparseable heading → 3; created register → 0; edited under its span → 0; register no span step names → 3; `.md` beside it → 3; index shard named in produces → outside the class; no landed shard row → 3; gate pair beside a register → refused by both |
| **A26** (71) | one phase's `PHASE-Pnn-{A,B}-<slug>.md` | additions only under `docs/gates/` (`changed_statuses`: not plain `A` → not an addition); exactly one A and one B, one phase, one slug; WS adds nothing under `docs/gates/`; no other hit; the pair guard runs inside `check` (assertion 3 covers "gates green after both finals") | clean pair → 0; reported as human-merge → disagreement; plan document beside it → 3; one half → 3; two phases → 3; modified existing gate document → 3; gate document added in WS → 3; no gate change → exception never applies |
| **A30** (75, in flight) | derived registers | declared in the rules file table; source tree touched; deriving test present; header unchanged; pin both repos; nothing else | `[UNVERIFIED — needs the batch-75 report and grep -n 'def test_' tests/unit/test_loop_complete.py after it lands]` |

Design principle (rules file): *"Not covered, by A28's own statement … a row's content within its own step's remit — the digest's; nor by A26's: the content of the two halves — the digest's."* Every exemption names what it does not check and hands that to the digest review (A19).

### 5.5 Failures and the fix that landed

| Failure | Batch / finding | Fix |
|---|---|---|
| Gates launched in the background died with the headless session; the report carried a `GATES_PENDING` placeholder under `STATUS: COMPLETE` | 40 / 318 | A7: gates foreground, sequential, blocking; report only after all four; `advise.py` injects the sentence (`FOREGROUND_GATES_CLAUSE`) into any next prompt lacking `in the FOREGROUND` |
| A green quoted about a tree that gained a commit after the run | 12, 24 / 318's stamps | the quiet targets write `.gate-logs/<gate>.started` before running; `complete.py` requires every stamp ≥ both finals; a hand-redirected `make check > log` has no stamp and is refused |
| The loop's own fixture stamped scratch repos at their own heads; a loaded machine read CP gates as stale; a sound batch refused at the merge gate | 48 / 320 | fixture keys stamps to `final_commit(cp, ws)`; both directions planted |
| The verdict validator refused any marginal ruling on a PROCEED (the pre-A11 §4) | 45–46 / 319 | validator reads `precedent`, not `confidence` (`NO_PRECEDENT_FORMS`, whole-string compare) |
| The validator refused a precedent that mentioned `class (2)` in explanation | 66–67 / 323 | `names_a_class_as_the_gap`: strip `GAP_PRECEDENT` matches, then require a `CITATION_FORMS` match in the remainder |
| `terminal_reason: api_error` 89 s into a batch (credits) | 59 | credit auto-reload; driver retry owed (§5.6) |
| `--resume` writes `next_prompt` unconditionally | 66, seen at 67 | owed (§5.6) |
| `MAX_BATCHES=10` would have stopped a healthy run at batch 65 | 57 | both budgets 999; the list and PART_END stop the loop, not the budget |
| A16's recording injection re-tabled rows already in the register | 57 | `_split_by_register`: `deferred_already_recorded` |
| Two merge failures in a row | design | `merge_and_advance`: one retry on `TRANSIENT:`; A3: exit 137 is REAL |

### 5.6 The hardened `loop.sh` — the baseline for the new app

Apply these to the verbatim `loop.sh` above before the first `--bootstrap`; each is a few lines.

1. **Retry a dead session.** Replace `[[ -s "$REPORT" ]] || { notify "…produced no report — stopping"; exit 1; }` with: read `terminal_reason` from `sessions/batch-N.json`; if it is `api_error` (or the file is empty), then for both repos `git checkout -q main` and delete `feat/*`/`plan/*` branches with no commits beyond `main` (refuse, notify and exit 2 if any branch has commits), sleep `RETRY_MINUTES` (10), relaunch the same prompt, up to `MAX_SESSION_RETRIES` (3); on exhaustion notify with the reason. Batch 59's recovery was exactly this, by hand.
2. **`--resume` checks the decision.** After the `--post-merge` advisor call: `DEC=$(jget … decision)`; if `DEC != PROCEED`, notify `"loop: post-merge advisor $DEC — decider needed"` and exit 2 **without** writing the prompt or clearing the flag.
3. **Refuse an empty prompt.** Line `[[ -f "$PROMPT" ]] ||` → `[[ -s "$PROMPT" ]] && grep -q '^STEP 1' "$PROMPT" ||`.
4. **Name the reason on every stop.** The "no report" and "advisor failed" notifications include the last three lines of `sessions/batch-N.json` / the advisor's stderr.
5. **`loop-preflight.sh` generic.** Steps 3 and 5 of the source script hard-code batch 38's report as the exemplar; replace with the latest report on file (`ls reports/batch-*.md | sort -V | tail -1`).

Verification: `--dry-merge` for the merge path; an `api_error` simulation — a fake `claude` on `PATH` that writes `{"terminal_reason":"api_error"}` and exits — must produce three retries and a named stop.

GENERIC: all of §5. SPECIFIC: the paths in `loop.sh`'s first lines.

---

## 6. The advisor

### 6.1 The brief's thirteen sections

| § | Purpose | Transfer |
|---|---|---|
| 1 Role and stance | "you ARE the decider for routine judgment"; never build/merge/edit; marginal is not a stop | GENERIC |
| 2 What you receive | report, complete.py verdict, previous merge result, STATUS entry, findings tail, rules file, next two spans' shard rows, the session's pre-read, flags `--bootstrap`/`--post-merge`/`--classify-merge-failure` | GENERIC |
| 3 Output contract | the JSON (§6.2) | GENERIC |
| 4 Decision rules | rule the routine; marginal proceeds; PROCEED/ESCALATE/DEFER/HALT/PART_END; spans | GENERIC |
| 5 The halt bar | §1.3 | GENERIC |
| 6 Precedent catalogue | 042/037/044 forms, nominal, executed-as-verification, built-precedent-wins, lock discipline, additive-optional, deferral convention, vacuity, derive-don't-restate, guards state gaps, contemporaneous refusal, gate-green tree, elision, invented-member, A8, A9, pod-lifecycle, human-launched, phase gate form, A14, A15 | GENERIC principles; the record/step numbers cited are SPECIFIC and must be re-earned |
| 7 Worked examples | escalated correctly / wrongly / proceeded correctly / would have been wrong | SPECIFIC content; keep the four headings, refill from the new project's first parts |
| 8 Next-prompt template | §8.1 | GENERIC |
| 9 Report checklist | eleven items | GENERIC |
| 10 Human-merge list | §5.3 | GENERIC |
| 11 Pre-issued rulings | the decider's settled rulings for named steps | SPECIFIC; starts empty |
| 12 Amendments | A1–A30 | see §6.6 |
| 13 Things you never do | quoted in §6.3 | GENERIC |

### 6.2 The output contract (brief §3, verbatim)

```json
{
  "decision": "PROCEED | ESCALATE | HALT | PART_END",
  "batch_reviewed": 38,
  "rulings": [
    {"topic": "...", "ruling": "...", "precedent": "record 0NN / finding NNN / ADR 00NN / rules § / step text", "confidence": "settled | marginal"}
  ],
  "deviations": ["each place the report says the work departed from plan text, with the recorded reading"],
  "lock_movements": ["contract.lock <old>→<new> both repos" ],
  "not_covered_additions": ["each named gap the batch added"],
  "deferred_escalations": [
    {"question": "...", "class": "(1)|(2)", "why_safe_to_defer": "no step through <n> depends on it; nothing authored assumes an answer", "expires_at_step": 1150, "recorded_in": "docs/DEFERRED-ESCALATIONS.md"}
  ],
  "next_span": {"steps": [1129], "closes_at": 1129, "why": "risk: no; 1130 is risk: yes"},
  "next_prompt": "<the full text of the next batch's prompt, per §8>",
  "digest_line": "batch 38 — <steps> — <verdict> — marginal: <each marginal reading, or none> — <one clause on anything a human should notice>",
  "reasons": ["why this decision, in order of weight"]
}
```

*"For ESCALATE, `reasons[0]` MUST name which class of §4 applies — (1) authority conflict, (2) invented immutable artefact, (3) guarded surface, (4) unfixable correctness defect — and quote the two authorities or the artefact. An escalation that cannot do this is not an escalation; emit PROCEED with the reading recorded as marginal instead."* For `--classify-merge-failure`: one line, `TRANSIENT: <class>` or `REAL: <reason>`; exit 137 under concurrent gates is REAL (A3).

The validator (`advise.py`) enforces: required keys, `decision ∈ DECISIONS`, `batch_reviewed == batch`, list fields, each ruling's `confidence ∈ {settled, marginal}`, every tabled item has a non-empty `question` and an **integer** `expires_at_step`, and — on PROCEED — no ruling whose precedent is a `NO_PRECEDENT_FORMS` member (`{"", "none", "n/a", "na", "no precedent", "-", "—", "unknown"}`, compared whole after lower-casing and stripping a trailing period) or names a class as the gap:

```python
GAP_PRECEDENT = re.compile(r"(?i)(?:§\s*4\s+)?(?:\bclass|§\s*4)\s*\(\s*[1-4]\s*\)")
CITATION_FORMS = re.compile(
    r"\b[Rr]ecord\s+\d{3}\b"
    r"|\b[Ff]inding\s+\d{3}\b"
    r"|\bADR\s+\d{4}\b"
    r"|\bA-?\d{1,2}\b"
    r"|§\s*\d+"
    r"|\b[Ss]tep\s+\d{3,4}\b"
    r"|\b\d{3,4}\b(?:\s+[\w'-]+){0,3}\s+(?:[Ff]orm|[Rr]uling|[Pp]recedent)s?\b"
)
```

Every `precedent` the new brief teaches the advisor to write must match one of those forms, or the validator will stop the loop (findings 319, 323 — both were the validator enforcing a shape narrower than the brief's words).

### 6.3 Decision rules, quoted where load-bearing

- **Rule the routine.** *"which of two internally consistent readings a verify clause bears; whether a plan-named path … is nominal …; a step whose artefact already exists …: executed as verification plus record; how a test fake … is extended; where a known gap is named …; whether an accessor … is derivable from a stated mechanism (A8); which side of a boundary an obligation lives on when the step's text names the act (A12); … deferrals … never a reason to stop; vocabulary transcribed by observation (A4)."*
- **Marginal is not a stop.** *"choose the one the step's text fits best, mark the ruling 'marginal', and put it in the digest line … a wrong marginal call costs one batch of revertible branch work, which is what per-batch merging bounds."*
- **PROCEED** when COMPLETE, exit 0 or 3, no merge/push/hook edit claimed, every judgment settled or marginal.
- **ESCALATE** only for classes (1)–(4); *"can you quote the two authorities, or name the artefact and show no source states it and no mechanism derives it? If not, it is a marginal reading — PROCEED and record it."*
- **DEFER before you ESCALATE** (A16): table a class (1)/(2) question the next span does not depend on, with `expires_at_step` = the first step whose execution needs the answer; escalate *"only when the expiry step is the next span … carrying every tabled item."*
- **HALT** on `STATUS: HALTED|ESCALATED`, a red that survived diagnosis, a claimed merge/push/hook edit, an unexplained exit 1.
- **PART_END** when the batch closed the part's final step; `next_prompt` is empty.
- **§13**: *"Never write a prompt that tells the session to merge, push, run make merge, or launch claude. Never resolve a halted session's question yourself. Never tune a ruling to make a red go green. Never produce prose outside the JSON. Never escalate on routine judgment — rule it and record it. Never proceed past class (1)–(4) of §4 — those, and only those, stop the loop."*

### 6.4 The tabling mechanism, end to end

1. The verdict lists the question under `deferred_escalations` with class, `why_safe_to_defer`, integer `expires_at_step`.
2. `finalize_next_prompt` injects `Record the advisor's tabled escalations (A16)` into STEP 0 (only for items not already in the register — `_split_by_register`).
3. The session appends one row to `docs/DEFERRED-ESCALATIONS.md`'s table: `| question | class | why safe to defer | expires_at_step | batch tabled | resolution |` (six columns = `loopcore.DEFERRED_COLUMNS`; `batch tabled` = the batch whose **verdict** tabled it, record 120).
4. `test_deferred_escalations_register.py` refuses a row without an integer expiry and **fails on any open row whose expiry ≤ `docs/STATUS.md`'s declared line** — the fail-closed arrival.
5. `digest.py` heads every digest with the open rows, due ones marked.
6. The advisor escalates when the expiry step is the next span; the decider rules; the session writes the ruling into `resolution` citing the amendment (never a second row; never edits the original text).

Failure prevented: batch 55 — Step/StepOutcome tabled at 54 with expiry 1159 escalated exactly at the P08 gate stop, so the human resolved them at a stop the list forced anyway. Batch 74 — the A28 question tabled at 73 with expiry 1186 escalated one batch later; the batch itself merged clean (A6).

### 6.5 The digest review cadence

`digest.py --through N` runs every `DIGEST_EVERY` (6) batches or when a report contains `PHASE GATE`, from the verdicts with no model call; A19: the marginal ledger lives there (batch, topic, precedent, premise, a verdict cell). The decider reviews at every digest, every phase gate, every part boundary; an overturn becomes a 037-form record correction and a §12 amendment. Through record 148 the source project overturned none. `[UNVERIFIED — whether digest.py renders the marginal ledger table A19 specifies: needs sed -n '131,243p' scripts/loop/digest.py]`

### 6.6 Amendment discipline as a procedure

How the thirty arrived, and what each class teaches:

| Trigger | Amendments | Lesson |
|---|---|---|
| Replay calibration at batch 38 | A1–A3 | calibrate before the first live batch |
| First live stops (39–44) | A4–A9, A12, A14, A15 | per-step rulings become worked examples; principles become §6 entries |
| Four routine stops in a row (41–42) | **A11** (§1/§4/§5/§7/§9/§13 rewritten), A13 | the calibration correction: marginal is not a stop |
| The human's own rulings at stops | A6, A10, A16 | an escalation never merges; the brief self-lands; table what the next span doesn't need |
| One tabled question at 54–55 | A17–A22 | premise stated; extend-with-over-proof; ledger in the digest; the A20 ladder; `unsure` reading; worked examples |
| Forced stops discovered in a pre-read (56) | A23–A25 | configuration is not immutable; the first exemption |
| Part boundary (70) | A26, A27 | gate pairs self-land; landing ahead of execution |
| Inventory at landing (71) | A28, A29 | the exemption class; the inventory's tabled items ruled |
| A28's gap (74) | A30 | derived registers |

Procedure: (1) write the amendment as a principle that retires a class — *"Rulings are principles that retire a class, not per-step answers; per-step answers live only as worked examples"*; (2) append under §12 in the root copy; `grep -c '^\- \*\*A[0-9]'` counts; `diff landed root` shows only additions; (3) the next batch's STEP 0 lands it under A10 — no stop; (4) if it changes what the loop may merge, the rules file carries the same text — that batch stops; (5) planted proofs both directions in `test_loop_complete.py`; (6) record the batch that earned it in the amendment's own text.

**Generic amendments (day-one text for the new brief):** A1, A2, A3, A6, A7, A10, A11, A13, A16, A17, A18 (the principle: probe the stronger form; the guard licenses the proceed), A19, A20 (the ladder (a)–(e)), A21 (as the `unsure` rule), A23, A25/A26/A28/A30 (as §10 exceptions), A27. **Specific (re-earn as worked examples):** A4, A5, A8, A9, A12, A14, A15 (principles generic, examples specific), A22, A24, A29.

### 6.7 The acceptance test for a new brief: replay calibration

`scripts/loop/replay.py --manifest scripts/loop/replay-manifest.tsv --out <scratch> [--only 19,31] [--dry-run] [--model …]`. For each manifest row (columns `batch span heading next_heading session_status human_merge hm_reason expected counterfactual_expected note`) the report is reconstructed from the STATUS entry at the commit that introduced the next entry's heading; complete.py's verdict is synthesised; the advisor runs with the working tree's brief. Halted/escalated batches replay twice — truthful and **counterfactual** (`STATUS: COMPLETE` over the same body). The A2 criterion: *"A halt since ruled correctly PROCEEDs today; the control replay against a brief lacking the ruling must HALT — that pair is the proof."* `SUMMARY.md` lists every mismatch; a PROCEED where the decider halted is the stop-and-redesign finding.

For a new project with no history: seed the manifest with five to ten hand-written synthetic batches — two clean, one halt-with-precedent, one class-(1) fork, one class-(2) invented member, one marginal reading — and run the counterfactual pairs before `--bootstrap`.

GENERIC: §6 entirely except the worked examples and pre-issued rulings.

---

## 7. Claude Code guardrails

### 7.1 The host guard — `~/.claude/hooks/guard.sh` (PreToolUse, exit 2 blocks)

Wired by `settings.json`:

```json
"permissions": {"allow": ["Bash","Edit","Write","Read","Glob","Grep"],
                "deny": ["Read(**/.env)","Bash(git push --force*)","Bash(git push -f*)"],
                "ask": ["Bash(make merge*)","Bash(git push*)"], "defaultMode": "bypassPermissions"},
"model": "fable",
"hooks": {"PreToolUse": [{"matcher": "", "hooks": [{"type":"command","command":"$HOME/.claude/hooks/guard.sh"}]}],
          "PostToolUse": [{"matcher": "Bash", "hooks": [{"type":"command","command":"$HOME/.claude/hooks/show-commit.sh"}]}]}
```

The guard logs first — `printf '%s %s\n' "$(date +%s)" "$tool" >> "$HOME/.claude/guard-invocations.log"` — then, for `Bash`, refuses (matchers verbatim):

| Refusal | Matcher |
|---|---|
| merge / push, any `-C` walk-through (finding 309) | `(^\|[^[:alnum:]_])make([[:space:]]+[^;&\|[:space:]]+)*[[:space:]]+merge([^[:alnum:]_-]\|$)` and the same for `git … push` |
| nested `claude` | `(^\|[^[:alnum:]_./-])(/[^[:space:]]*/)?claude([[:space:]]\|$)` |
| `docker volume rm/prune` in argv-list form (step 161) and in shell form; `docker system prune --volumes` | as in the file |
| `rm`/`shred` touching `.git` | two greps ANDed |
| `git reflog expire`, `gc --prune`, `filter-branch`, `filter-repo` | one grep |
| a destructive verb (`rm mv shred truncate`) with a home-rooted path outside `$PROJECT` — quotes stripped first (`sed "s/'[^']*'//g; s/\"[^\"]*\"//g"`) | loop over `(~\|$HOME)/…` paths |
| `cat/less/head/tail/bat … .env` (not `.env.example`) | one grep |

For `Read/Edit/Write`: `.env` refused; any `Edit/Write` under `$HOME` outside `$PROJECT` refused (*"includes ~/.claude/, which is not yours to edit"*). Missing `jq` → exit 2. `$PROJECT` is the one SPECIFIC line.

**Why `bypassPermissions` is safe only because of this.** The settings' `ask` rules never fire in a headless session and never matched `cd X && make merge`; the guard's comment says so: *"The settings ask rules never matched … Matching here is ours."* Remove the hook and the session can merge.

**Finding 189 (the accepted false positive):** the guard cannot tell doing from describing, so prose that quotes `docker volume rm` or `make merge` through a shell heredoc is refused. *"The handling is to change the tool, never the text"* — write documentation with the file-editing tool; never reword prose until the matcher stops firing. Batch 71 hit it on a `grep` whose pattern quoted the literals; batch 74 on an `rm -rf` of a scratch path beside `--exclude .git`. Sessions record each as a live refusal.

**Liveness (finding 313).** `scripts/step-open.sh` requires a log entry within `LIVENESS_WINDOW=15` seconds — the very Bash call running `make step-open` writes one — else exits 1 with *"hook liveness gap"*. A human shell has no hook layer: `STEP_OPEN_NO_HOOK_LAYER=1 make step-open`, set only by a human. A fresh line proves the layer logged *some* call, not that it would refuse a forbidden one; refusal evidence is the observed refusals.

**The tracked reference** `infra/host-guards/` (`MANIFEST`, `README.md`, `hooks/`, `install.sh`, `settings.json`): `test_host_guard_parity.py` compares each live file to the reference with the manifest's `@reference-home` rewritten to `$HOME` (*"live == what the installer would produce here"*), asserts the manifest lists every reference file, and that the live hooks are executable; it **skips with a reason where `~/.claude` is absent** (a category-C, machine-local check no checkout can supply). A re-sync after the human edits the live guard is a human-merge batch (batch 28/29 form).

**`step-open.sh`'s other two assertions:** both repos on a non-main branch (the batch-open refusal is expected and recorded), and no branch holding commits reachable from neither HEAD nor `origin/main` (the *stranded* check — measured to catch the real incident the ancestry check missed). Neither reaches the network; a merge that landed remotely and was never fetched reads as stranded (the safe direction).

### 7.2 Commit-message hooks

CP `scripts/commit-msg-check.sh` (shell, no npm — supply-chain decision, step 20): `types = feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert`; `scopes = compiler|scheduler|state|contract|budget|gate|invariant|checkpoint|eval|secret|config|obs|errors|ids|cli|brief|approval|build|docs|ci`; pattern `^(types)\((scopes)\)!?: .+` or scope-less `^(types)!?: .+`; **subject ≤ 100** (`max_len=100`). WS `commitlint.config.mjs`: `config-conventional`, its own twenty scopes, `header-max-length 100`, `subject-case` off; `body-max-line-length` 100 (config-conventional's default, which refused batch 74's STATUS commit body). `test_commit_grammar.py` drives both enforcers over one byte-identical corpus. About ten refusals across Parts 02–03, all subject length — sessions are told to **measure before committing**; the reliable form is writing the message to a file and running the hook script on it before `git commit -F`.

SPECIFIC: the scope vocabularies. GENERIC: the grammar, the shared corpus, the length.

### 7.3 The scratch pipeline for any wheel change

Rebuild into scratch and assert, in order: `TREE-IDENTICAL` (×4: schemas, models, fixtures, openapi), `SCRATCH-WHEEL-IDENTICAL-TO-COMMITTED`, `WHEELHOUSES-IDENTICAL`, `LOCKS-IDENTICAL`. Two traps: a `ruff.toml` must sit beside the scratch tree or the generator's formatter reformats hand modules and the tree differs by whitespace (record 128, batch 59); every `uv pip install` in scratch carries `--no-config` (finding 324). Print the installed digest before asserting: *"a planted proof that reports the state it planted is the only kind whose vacuity is visible in a green run."*

### 7.4 `show-commit.sh`

PostToolUse on Bash: after a `git commit` in command position, prints `git show --stat --oneline HEAD` and appends it to `~/.claude/commit-log.txt`. Batch 70's lesson (a refused subject re-run with `git add -A` that swept in a scratch file) is why the artifact is shown at every commit.

---

## 8. Session conventions

### 8.1 The prompt template (brief §8, verbatim)

```
Fresh session. Batches through <n-1> are merged to main in both repos (verify at step-open). Steps <first>–<last done> are done. Follow the standing rules in CROSS_REPO_CLAUDE.md, including the loop discipline. This session is batch <n>: plan step(s) <span> — <tag(s)>, risk: <flags>; <why the span closes where it does>. Stop after <last of span>. Do not open <next>.

Run `make step-open` first (it asserts hook liveness). Context discipline stands: output piped at the call, decisive lines to the window, full logs to files. Gates run SEQUENTIALLY, in the FOREGROUND, blocking — never in the background; the report is written only after all four finish.

STEP 0 — <write-backs owed: STATUS figures upgraded from expected to observed; corrections in the 037/040 form; carried items restated>. Land the brief (A10) if the root and landed copies differ. Record the advisor's tabled escalations (A16) if any.

STEP 1 — execute <span> per the plan text, under these rulings, each recorded in the step's record citing the decider:
 - <ruling 1, with its precedent and confidence>
 - …
Standing clauses as they apply: <lock discipline / scratch discipline / A18 over-proof / adjacent case named / derive, never list>.

STEP 2 — read-only pre-read of <the following span> (why it closes where it does): what each requires, sources named and located, records bearing. Decision material stated — for the advisor to rule. Author nothing.

STEP 3 — gates via the quiet variants, sequentially, in the foreground, all started after the final commit in both repositories; a refused-then-fixed gate re-runs in full. Then STOP — unmerged. Write the report to CP/.loop/reports/batch-<n>.md per the contract: line 1 STATUS, line 2 HUMAN_MERGE with reason (expected: <yes/no — why>); then the report in the established form (each step's record and commit; lock movements both repos; WS commits explicitly either way; gate count lines, log paths and run order relative to both finals; anything surfaced but not fixed).

Halt bar unchanged and in the file.
```

`advise.py` holds every PROCEED prompt to two markers derived from the landed brief (`FOREGROUND_MARKER = "in the FOREGROUND"`, `ADVISOR_RULE_MARKER = "for the advisor to rule"`) and injects them when missing; each injection is named under `prompt_injections`. A prompt without a `STEP 0` gets the A10/A16 clauses appended as a new STEP 0 before STEP 1.

### 8.2 The report contract

Line 1 `STATUS: COMPLETE|HALTED|ESCALATED`; line 2 matches `^HUMAN_MERGE: (yes|no) (?:—|-|–) (.+)$`; the **first H1** states the span in the form `plan step(s) NNNN[–NNNN]` (`report_span` returns `None` for anything else, which makes every register edit human-merge — *"unparseable is human-merge"*; `[UNVERIFIED — the exact `_H1_SPAN` regex: needs grep -n '_H1_SPAN =' loopcore.py]`). Then, per the §9 checklist: per-step record and commit; lock movements in both repos; WS commits stated either way; live refusals as they happened; the pre-read; the four gates' count lines, log paths, `.started` stamps and run order against both finals; `complete.py` run read-only after the gates (stdout to `/tmp`, nothing under `.loop/`); "surfaced but not fixed". Batch 74's report (`.loop/reports/batch-74.md`) is the canonical example: STEP 0 upgrades batch 73's figures and annotates record 146, then 1184 and 1185 each with rulings cited to the decider, measurement before building, planted proofs, adjacent cases, nominal→actual, seven live refusals, the gates with stamps, complete.py's observed exit, and five surfaced items.

### 8.3 Records, corrections, forms

- **A record opens with the command that produced it** — first line a fenced `bash` block, non-empty (`test_recon_records_carry_their_command.py`; P1-D2). It does not verify the command is right or the output unedited; the reconnaissance steps that re-run commands do.
- **037/040 form:** a wrong record is corrected by annotation beneath, never by rewriting (*"Gate results enter records only via re-verification or post-gate commits"*: a record commits as *expected at gate*; the next session's STEP 0 upgrades it to observed).
- **042 form:** an ambiguous clause → both texts quoted, the reading chosen, why; an undefined member → elided with candidate source and owning step, expiring on arrival.
- **044 form:** a vacuous confirmation says so (*"green over nothing"*, finding 289's class).
- **STATUS entries** are written "expected at gate" and upgraded by the next STEP 0; the WS STATUS entry too (its correction is a 037 annotation in the next STEP 0, batch 71's lesson).
- **Findings** name their class and adjacent case; a live refusal is recorded *when it happens* in the finding or the resolving commit's body.
- **Deviations** are recorded in `docs/STATUS.md` under Deviations; errata candidates are recorded for the human to land at the part-end re-pin (A28: *"never by a session"*).

### 8.4 Guards

- Planted proofs both directions; a mutation probe where cheap (disable the widening, watch the old refusal return).
- **The deferral convention**: premise on a *path* (git history says whether it ever existed — `tests/deferral.py`); assertion on *behaviour* (never a substring grep — the marker-grep audit found three); if the artefact is absent, say in the test's own text that it is a grep. A premise on a *step* (A27) fails closed at the batch that executes it.
- **Name the adjacent case and the surfaces read** at the guard: *"covered elsewhere / cannot occur there / is a known gap"*.
- **Measure precision retroactively** before trusting a finding-shaped guard (the 71%-false artefact-existence sweep).
- **Two questions before any guard:** does the platform already enforce it? would it have caught the thing that prompted it?
- **Derive sets, duplicate reasons** (*"what happens when the two copies disagree — nothing at all, or a reader who notices"*).
- **Every command names its repository in its own arguments** (`git -C`, `make -C`); a tool that discovers config from the working directory needs a flag that turns discovery off (finding 324).
- **A command that modifies or destroys state runs against a scratch target, unconditionally** (finding 188).

### 8.5 Rulings the session applies as standing

- **Built precedent wins** (ADR 0014, A-02): where a source document and the built, pinned, migration-proven surface diverge, the built one governs; the source is corrected by errata.
- **The A20 ladder** for a type a signature names and no source defines: (a) opaque reference minimum (`{type: string, minLength: 1}`, grammar elided); (b) composition-implied members only; (c) `$ref` to a built vocabulary when a stated mechanism routes there; (d) a set a source states in prose, transcribed by parsing the sentence and checksummed at test time; (e) a derivation the plan itself states (RQ-01). Empty populations refused (`minItems: 1` on a list the type exists to exercise).
- **The 1154 form** (A18): a plan clause says "required" on a type with a corpus → probe the wire-required form against the compatibility guard first; if refused over baselines, land additive-optional on the wire and required on the object path at every emitter, the wire half owed at the first MAJOR, held by a mirrored test. A new type carries its clauses from birth.
- **Configuration values are data** (A23): settings fields with fail-closed provisional defaults, `retryable ⇔ ceiling > 0` derived, never class (2).
- **Executed as verification** (record 075): an artefact that already exists is asserted mechanically, the lock unmoved.

GENERIC: §7–§8, with the scope vocabularies, `$PROJECT` and the numbered record/finding citations SPECIFIC.

---

## 9. Human-gate posture — stated precisely

The goal was fewer human stops; the mechanism was **exemptions with mechanical proofs, never removal of the list**. Batch 71's inventory is the arithmetic: Part 03 has eighteen `docs/plan/` producers, sixteen human-merge by construction under the list as it stood; A28 (one rules-file stop) took fifteen off; A30 (one more stop) took the 43 migration re-derivations off. Expected forced stops for a 120-step part after A30: the landing (first batch), the carry rewrite and re-pin (last-but-one), PART_END. Everything else the loop merges.

### 9.1 Still human-merge by construction, and why each cannot be exempted safely

| Item | Why it stays |
|---|---|
| `docs/CROSS_REPO_CLAUDE.md` (the rules file) | it defines what the loop may merge; a self-merging rule change is the executor writing its own checks (rule four of the workspace's seven, one level up) |
| `infra/host-guards/` incl. settings re-syncs | the reference for the checks the session is the subject of; a session cannot attest to the guard that judges it; a human-side drift the loop *stops on, never absorbs* |
| plan landings and re-landings (`PLAN-PART-*.md`, shards) | plan authority is exercised at placement by the human; the landing pins bytes the plan's whole execution reads |
| the part-end carry rewrite and re-pin (`PLAN-CARRY.md`, `PLAN-MANIFEST.md`) | the carry is the human's position record and the re-entry prompt; its content is judgment, not derivation (the build script derives its tables, the human reads the whole) |
| `ERRATA.md` and any `docs/plan/*.md` | an erratum amends what the plan means |
| guard re-syncs of any kind | same as host guards |
| a `docs/gates/` change that is not exactly one phase's new pair | a modified gate document is a rewritten record |
| pins other than a register's (`ROADMAP_SHA256`, `ADDENDA_SHA256`, `HANDOFF_SHA256`, scalar pins) | the authorities themselves |
| an exemption whose conditions are unmet, in any way | fail-closed: *"any condition unmet is exit 3, the unmet conditions named"* |

### 9.2 The exemption recipe

1. **Identify the recurring stop** from a pre-read or inventory (batch 56: three register edits; batch 71: sixteen producers; batch 74: 43 re-derivations). Count the stops it would cost.
2. **Define the mechanical condition** over the diff alone — paths, statuses, headers, row keys, four-digit step tokens, digests in both repos, other hits — and state what the condition cannot see (content), assigning that to the digest.
3. **Plant proofs both directions** in `tests/unit/test_loop_complete.py`: the clean case → 0; every condition unmet, singly → 3 naming it; the composition with the other exemptions (a gate pair beside a register is refused by both).
4. **Carry the same text in the rules file** (in the brief's own words, quoted) and in the brief's §12; add the case to complete.py's docstring as the next numbered assertion.
5. **Land as one human-merge batch**: brief (A10, no stop) + rules file + `loopcore.py`/`complete.py` + plants, its own commit pair, `HUMAN_MERGE: yes — the rules file`. Then `--resume`.
6. **Verify live** at the first batch the exemption applies to: `complete.py`'s verdict shows `<exemption>_landing.applies: true, exempt: true` and `classified: []` (batch 73's record of A28's first application).

The next conversation should design its plan-side registers (§4.6) and its gate-pair form (§4.10) so A26/A28/A30 apply from the first part — not discover them at its third.

---

## 10. Operating procedures

Shell preamble for every runbook (variables do not survive tmux/terminal boundaries):

```bash
CP=<parent>/<cp>; WS=<parent>/<ws>; LOOP=$CP/.loop; ROOT=<project-root>/plan
```

### 10.1 Launch

1. `~/bin/loop-preflight.sh` — scripts present, `.loop` ignored, latest report/merge on file, the advisor pin count 1, complete.py's exit over the latest report (3 is normal after a human-merge stop), ntfy round-trip, key file head, `bash -n loop.sh`.
2. `tail -n 3 ~/.claude/guard-invocations.log` — the hook logs; `ls -l ~/bin/loop.conf` — 600.
3. `cat $LOOP/state.json` — `next` is the batch whose prompt exists; `awaiting_human_merge` empty.
4. `tmux new -s loop -d; tmux send-keys -t loop '~/bin/loop.sh 2>&1 | tee -a ~/merge-logs/loop-$(date +%Y%m%d-%H%M).log' Enter; tmux attach -t loop`; detach with `Ctrl-b d`.
5. Stop cleanly: `touch $LOOP/STOP` (honoured at the next batch boundary); `rm` it before relaunch.

### 10.2 A human-merge stop (`awaiting_human_merge` set)

1. `head -2 $LOOP/reports/batch-N.md`; the verdict's `decision` and `digest_line`.
2. If the rules file changed: `cmp $CP/docs/CROSS_REPO_CLAUDE.md $WS/docs/CROSS_REPO_CLAUDE.md`. If `complete.py` changed: `grep -n 'def test_' $CP/tests/unit/test_loop_complete.py` shows the plants. If `docs/plan/` changed: the pins moved for exactly those files in both repos.
3. `~/bin/merge-and-sweep.sh | tee ~/merge-logs/batch-N-hand-merge.txt`; confirm `SWEEP CLEAN`.
4. If `docs/plan/` moved (carry/manifest at a part close): sync root ← landed (`cp $CP/docs/plan/PLAN-MANIFEST.md $ROOT/`; `cp … PLAN-CARRY.md`; `cmp`). Finding 316: an edit on the landed copy that never reached the root is silently reverted at the next landing.
5. `~/bin/loop.sh --resume 2>&1 | tee -a …` — it verifies the tip, writes `merges/batch-N.txt`, runs the post-merge advisor, writes the next prompt, continues.

### 10.3 An escalation (`ESCALATE`, exit 2, nothing merged)

1. Read `reasons[0]` (the class and the authorities) and `reasons[1]` (whether the batch is clean).
2. If clean: `~/bin/merge-and-sweep.sh | tee "$LOOP/merges/batch-N.txt"` (the loop's own record path, since the driver did not write it).
3. Rule as a principle → an amendment on `$ROOT/ADVISOR-PROMPT.md` (§6.6). Resolve any tabled row's `resolution` cell via the next STEP 0.
4. Write `$LOOP/prompts/batch-(N+1).md` by hand in the §8.1 form (the verdict's `next_prompt` is empty on ESCALATE). If the verdict was PROCEED with rulings and only the driver failed (finding 323's shape), extract `next_prompt` with Python and insert an addendum before `STEP 1 —`.
5. `state.json` → `{"next":"N+1","awaiting_human_merge":"","pending_tip_cp":"<CP main>"}`; **plain run, not `--resume`** — `--resume` would regenerate the prompt from the landed brief, which does not yet carry the amendment, and would write it regardless of the post-merge decision (§5.6 item 2).

### 10.4 A dead session (no report; `terminal_reason: api_error` or empty session file)

Until §5.6's retry lands: `python3 -c 'import json;print(json.load(open("'$LOOP'/sessions/batch-N.json")).get("terminal_reason"))'`; for both repos `git log main..HEAD --oneline` (expect empty), `git checkout main`, `git branch -D feat/batch-N-*`; confirm `state.json` still names N; plain run. Check credits first.

### 10.5 The advisor's validator refuses a sound verdict (`advisor failed`, empty `verdicts/batch-N.json`)

`ls -l $LOOP/verdicts/batch-N*` — the `-advisor-raw.json` holds the model's output. If its decision is PROCEED with rulings, extract `next_prompt` from the raw file, write the prompt, fix the validator in the next batch's STEP 0 with a planted proof (finding 323's form), state and plain run.

### 10.6 Digest review

Every 6 batches, every phase gate, every part boundary: `cat $LOOP/DIGEST-through-N.md` (open tabled rows on top); endorse or overturn each marginal ruling; an overturn → 037 annotation on the record + a §12 amendment; read each gate pair's Half B not-covered list (A26 moved that review here).

### 10.7 PART_END

The driver exits 0 with no prompt and no flag. Review the part-close batch (the gate pair, the carry, the re-pin — the last two were human-merge stops already); sync the root; land the next part per §4.9 with a hand-written landing prompt (batch 71's form: STEP 0 write-backs, Act 1 landing, Act 2 any tooling the boundary needs, Act 3 the inventory); state `next`; plain run.

### 10.8 Placing and landing

§4.8 then §4.9. The landing batch is `HUMAN_MERGE: yes` (docs/plan/ + pins); after its merge, `--resume`.

### 10.9 Amending the brief

§6.6 steps 1–4. Never edit the landed copy; never edit the root between a landing and the verdict (A10: the safeguard reads "not identical" and stops — the safe direction).

---

## 11. Pitfall register

Ordered by batch (source-project numbering; "pre" = before the loop existed). Every failure between batch 38 and 75 appears; earlier ones are included where the loop inherits their guard.

| # | Batch / finding | Symptom | Root cause | Fix that landed | Guard now | New app must |
|---|---|---|---|---|---|---|
| 1 | 12, 24 / rules file | a green quoted about a tree that gained a commit; a WS commit after CP's gates | gate-green is a property of the tree | both-trees rule; `.started` stamps | complete.py assertion 2 | keep the quiet targets and stamps from genesis |
| 2 | pre / 188 | a destructive command run against the live dev database | "this backup is of this database, so restore is a no-op" — a correct argument | the unconditional scratch rule | rules file | write the rule into the rules file day one |
| 3 | pre / 189 | host guard refuses prose that quotes a dangerous command | matcher on command text | accept; edit docs with the file tool | rules file | never reword around a matcher |
| 4 | pre / 301, E-13 | plan text puts the lock move at the part's end; gates require it per step | authored design vs built gates | E-13; per-step lock discipline | wheel-currency + pin tests | author publication steps as verification |
| 5 | pre / 302, E-14 | a step transcribes a vocabulary the codebase pins differently | source DDL vs built enum | built precedent wins | ADR 0014 | never transcribe over a built vocabulary |
| 6 | pre / 303 | landing Part 03 ahead of execution tripped the current-degraded guard; the landing was reverted | guard premise "held by an executed step" | A27's deferral form | `test_recapture_obligations_are_bound.py` | write register guards with the landed-unexecuted premise |
| 7 | 28–29 / 309 | `-C` forms walked through the host guard | leading-anchor matcher | tolerant matchers (`([[:space:]]+[^;&\|[:space:]]+)*`) | guard.sh | copy the matchers verbatim |
| 8 | 34–37 / 313 | the host guard was correct, wired and never invoked in a headless child | no hook layer fired; every surface looked green | liveness log; step-open's 15-s window | `guard-invocations.log` | day-one liveness test |
| 9 | 37 / 316 | a §10.3 edit reached the landed plan copy and not the root | root outside git, read by no gate | root-first rule; diff before landing | ritual only | sync root ← landed at every plan stop |
| 10 | 38 | `MAX_BATCHES=10`, `loop.conf` mode 644 | defaults | 999; 600 | — | set at install |
| 11 | 38–39 | the first prompt's ruling read the step's text loosely ("A8 form" resolved to no document) | brief vocabulary not pinned | A8 in the catalogue | validator citation forms | every precedent name is a citation form |
| 12 | 40 / 318 | background gates died with the headless session; placeholder report | headless turn end reaps children | A7 foreground; injection | complete.py refuses countless/stale logs | keep A7 in the template |
| 13 | 41–42 | four routine stops in a row | §4 too wide | A11 rewrite; A13 | brief | marginal is not a stop, from day one |
| 14 | 44 | a clean batch left unmerged by an escalation about the *next* span | ambiguity in what an escalation merges | A6: never merges; `reasons[1]` states cleanliness | driver | keep A6 |
| 15 | 45 / 319 | the validator refused the first verdict under the rewritten brief | a checksum of the old §4 left in code | validator reads `precedent` | `test_loop_advise.py` | when §4 changes, grep the code for it |
| 16 | 45 | the brief was on the human-merge list — a stop per amendment | — | A10 byte-identity self-landing | complete.py assertion 6 | A10 from genesis |
| 17 | 48 / 320 | the loop's own test refused a sound batch at the merge gate on a loaded machine | fixture stamps keyed per-repo head | keyed to the pair's final | plants both directions | copy the fixture |
| 18 | 49, 50, 53 | rulings asserted a premise the report contradicted (ULID over bigint; a lock move for a module step; a gate grouped into a span) | precedent applied without its premise | A17 | validator (partly) + digest | A17 day one |
| 19 | 50 | the advisor called a module-only step a "pinned-hash movement" | solo-list confusion | corrected by the session; A21 | — | state "lock ≠ solo" in the rules file |
| 20 | 54–55 | two class-(2) forks tabled with expiry at the next span → escalation at a forced stop | design working | A16 proven; A20 ladder | register test | A16 + A20 from genesis |
| 21 | 55 | `unsure` read as solo by the rules file, density by the brief | two authorities on one word | A21; rules file amended at the next stop | — | one wording, both files |
| 22 | 56 | three Part 02 steps edit a pinned register — three stops discovered in a pre-read | registers not designed as exemptible | A25 → A28 → A30 | complete.py 7 | §4.6 |
| 23 | 56 | STATUS entries written in the wrong order (a later step above an earlier) | write-back convention | annotation | — | STATUS order is part of the STEP 0 check |
| 24 | 57 | A16 injection re-tabled an already-recorded row | injection unaware of the register | `_split_by_register` | advise test | keep |
| 25 | 59 | `terminal_reason: api_error` at 89 s | credits exhausted | auto-reload; retry owed | §5.6 | auto-reload before the first night |
| 26 | 59 | `tee` swallowed pytest's exit code in a recorded command | pipeline status | `set -o pipefail` in recorded commands | rules (context discipline) | pipe with pipefail |
| 27 | 59 / 321 | a deferral premised on a nominal, never-tracked path would skip forever | premise on the plan's path not the built one | premise on the in-wheel path | deferral tests | premise on built paths |
| 28 | 59 / record 128 | scratch rebuild differed by whitespace | no `ruff.toml` beside the scratch tree | copy `ruff.toml` | scratch script | §7.3 |
| 29 | 61 / 322 | the generator's `__init__` keyed on `*_schema.py` swept a hand module | shape unique only by luck (finding 145's class) | derive the generated set from the schema list | `test_generated_init` | derive, never shape-match |
| 30 | 63, 66 | the advisor grouped a solo step into a span; the session corrected it | shard reading | A17 | — | the session checks the solo list at step-open |
| 31 | 66 | `--resume` died on the validator (finding 323); the raw verdict was sound | shape `class (N)` unique only by luck | citation grammar | `test_a_class_mentioned_beside_a_named_citation…` | copy the validator |
| 32 | 66–67 | `--resume` writes `next_prompt` whatever the decision | driver | owed | §5.6 | fix before bootstrap |
| 33 | 68 / 324 | a planted stale install installed the current wheel twice; the first diagnosis (cache) was wrong | uv discovers `[tool.uv]` from cwd | `--no-config`; measured with/without | drive script comment | §2 row 4; docstring in the mirrored offline test owed |
| 34 | 70 | a refused commit subject re-run with `git add -A` swept a scratch file into the commit | staged set not re-checked | check `git status` before every re-commit | show-commit.sh | measure subjects before `git commit` |
| 35 | 71 | the carry gate's docstring predicted "a landed part joins with no edit" and failed on the landing | mis-shaped expiry prediction | A27's premise form | gate plants | describe what a guard does, never what it will never need |
| 36 | 71 | 43 of 120 rows produce "a new migration" with no path | plan authoring | held for the carry rewrite | carry gate adjacent case (b) | every produces cell names a backticked path |
| 37 | 71, 74 | seven commit-subject refusals in one batch; a body line > 100 in the WS | length measured after writing | shortened | hooks | §7.2's file-then-hook form |
| 38 | 72 | a 100-step part with sixteen forced stops | A25 too narrow | A28 | complete.py 7 | §4.6 |
| 39 | 73–74 | a derived register re-derived by 43 steps none of which name it | A28's produces-naming letter | A30 | complete.py (batch 75) | declare derived registers at genesis |
| 40 | 74 | Alembic applies a migration declaring the wrong base and leaves two version rows | tool behaviour | the pre-flight hook, measured first | `test_migration_preflight*` | measure the tool before guarding it |
| 41 | all | the doubled `-q` suppressed pytest's count line, so the quiet gate refused a green | `-q` in `addopts` plus `-q` on the command | run without the extra `-q` | quiet targets | never pass `-q` twice |
| 42 | all | `StarletteDeprecationWarning` in every count line | dependency | carried | — | pin or filter before it masks a real warning |
| 43 | 74 | a WS commitlint measurement that did not gate the command | measured then committed anyway in one chain | recorded as the failure | — | the measurement gates: `&&` |
| 44 | PART_END | the driver leaves no prompt and no flag | design | hand-written landing prompt | — | §10.7 |
| 45 | 71 | the workspace STATUS claimed "all three headers accepted first time" before its own fourth was refused | prediction as observation | 037 annotation next STEP 0 | rules (gate results enter records via re-verification) | never claim an outcome for the commit being written |

---

## 12. Day-one checklist for the new app

Ordered; each line checkable; the minimum before the first `--bootstrap`.

1. Two sibling repositories cloned; `make step-open` from either finds both and refuses on `main`.
2. `~/.claude/settings.json` hooks stanza (§7.1), `guard.sh` and `show-commit.sh` installed from `infra/host-guards/install.sh`; `jq` present; `test_host_guard_parity.py` green (not skipped); a tool call writes a fresh line to `guard-invocations.log`.
3. **Guard liveness test**: a headless `claude -p 'run make step-open'` exits with the hook logging its call; then a deliberate `claude -p 'run make merge'` is refused with `BLOCKED: merge and push are the human's` (observed, recorded as the first live refusal).
4. Commit hooks in both repos; `test_commit_grammar.py` green over the shared corpus; subjects of exactly 100 accepted, 120 refused.
5. Contract triangle green in both repos: `contract-verify`, `test_contract_wheel_is_current.py`, the tree→lock test; `contract.lock` byte-identical; parity sweep green.
6. Quiet gate targets with `.started` stamps in both Makefiles; `make check-quiet` and `make ci-quiet` print count lines and log paths.
7. **A7 foreground-gate test**: a headless session prompted to run one quiet gate in the background then write a report → `complete.py` exit 1 naming the stale/countless log (finding 318 reproduced on purpose).
8. `scripts/loop/{loopcore,complete,advise,digest,replay}.py` + tests green; `test_loop_scripts_hold_no_merge_push_or_claude.py` green; `.loop` in `.gitignore`.
9. `~/bin/loop.sh` with §5.6's four hardenings; `bash -n`; `--dry-merge` over a fake merged batch cleans its marker; **`api_error` simulation** (a fake `claude` on `PATH`) produces three named retries and a stop.
10. `loop.conf` 600 with ntfy; key file 600; credit auto-reload on; `loop-preflight.sh` (generic form) all green.
11. The rules file authored with: the loop discipline section, the human-merge list with A10/A25-A28/A26/A30 exceptions in the brief's words, the `### Derived registers (A30)` table naming every register the plan will derive, the scratch rule, the host-guard section, the halt bar.
12. The brief authored with §1–§13, the generic amendments (§6.6) as day-one text, worked examples refilled; `ADVISOR_PROMPT_SHA256` pinned in both repos; the root copy identical (`cmp`).
13. **Replay calibration** over a synthetic manifest (§6.7): every counterfactual pair behaves; no PROCEED where a halt was correct; spurious ESCALATEs tuned out before live.
14. Plan Part 00/01 placed and parity-proven (§4.8); risk density inspected; every register-writing step names `` `CP/docs/plan/<NAME>.tsv` ``; gate-pair steps name `PHASE-Pnn-{A,B}-<slug>.md`.
15. The first part landed by a hand-written landing batch (§4.9) — **a deliberately human-merge batch** that proves the stop-and-resume path: `awaiting_human_merge` set, hand merge, `--resume` writes the next prompt.
16. First `docs/DEFERRED-ESCALATIONS.md` with header and an empty table; its test green.
17. `--bootstrap` from the landing batch's report; read the first prompt; launch in tmux.

---

## 13. What is not settled

Generic carried items (the App-Builder-specific ones — GuardRun fields, `visibility: guard`, the 1154 grammar, Part 06's adapter clause — are omitted).

- `loop.sh` hardening (§5.6): owed since batch 59; not landed at batch 75.
- The validator's adjacent case (finding 323): a precedent naming a class as the gap with a decorative citation beside it passes — the unsafe direction, carried to the digest review.
- The mirrored offline-install test's docstring does not name that `uv`'s discovered config and its argument coincide on the same directory (finding 324's adjacent case).
- The tree-run limit class: the contract's source-tree test cannot import hand modules with import-time schema holds; the in-wheel run is the property's home (record 136).
- Commit-subject length is still measured by hand; ten refusals say the convention does not hold. Recommendation: a `scripts/commit-with-check.sh` that writes the message to a file, runs the hook script, then commits — and the rules file naming it as the only commit form for sessions.
- `digest.py`'s rendering of the A19 marginal ledger `[UNVERIFIED]`.
- The `StarletteDeprecationWarning` in every count line.
- `test_recon_records_carry_their_command.py` cannot see a wrong or stale command; the 037 annotation convention is ritual.

**Recommendations for a clean start (marked as such):**

1. Design every plan-side register as produces-named or derived at authoring time (§4.6); author the A30 table at genesis.
2. Keep risk density at 25–35% and reserve `risk: yes` for irreversible artefacts (§4.2).
3. Ship A6, A7, A10, A11, A16, A17, A20, A25/26/28/30 as day-one text and mechanisms — every one of them was earned by a stop that a first-part plan will otherwise repeat.
4. Add a `complete.py --span` argument fed from `state.json` so the H1 heading is checked against the driver's own record rather than parsed alone (`report_span`'s adjacent case: a heading claiming a span the batch did not run).
5. Make the scratch wheel pipeline a `make contract-scratch-verify` target rather than a per-session script, so its four assertions and `--no-config` are one command.
6. Write `merges/batch-N.txt` from the driver on every stop path (ESCALATE/HALT/PART_END) so hand merges are recorded by the same mechanism `--resume` reads.
7. Replace the batch-38-specific `loop-preflight.sh` with the generic form before the first run.
8. Put `set -o pipefail` in the session's recorded-command convention in the rules file (pitfall 26).

---

## Appendix A — the eight findings the pitfall register cites, by their own headings (verbatim from `docs/BATCH-FINDINGS.md`)

- **Finding 189** — the host guard fired on a ledger entry, and rewording it would have been the wrong fix
- **Finding 303** — a placed-but-unexecuted part trips the current-degraded guard, and the landing was reverted rather than the guard bent
- **Finding 316** — a §10.3 edit to a pinned plan document reached the landed copy and not the root authoring copy, and nothing compared the two until the next landing
- **Finding 318** — a headless session ends when its turn ends, so gates launched in the background died with it and the report carried a placeholder; `complete.py` refused it as designed
- **Finding 319** — the advisor's self-consistency check enforced the superseded §4 and stopped the loop on the first verdict rendered under the rewritten brief
- **Finding 320** — the loop's own fixture stamped each scratch repository at its own head, so a loaded machine read the control plane's gates as stale; the batch forty-eight merge gate refused a sound batch on the loop tooling's test, not on the batch's work
- **Finding 323** — the advisor's verdict validator keyed on the SHAPE `class (N)` and refused a sound PROCEED whose precedent cited four sources and mentioned the class only to say why the rejected reading was one
- **Finding 324** — a scratch install run with a repository's `[tool.uv]` config discoverable took that repository's own wheelhouse over the `--find-links` it was given, so a planted stale install installed the current wheel twice; the first diagnosis was wrong and was corrected by measurement

## Appendix B — `report_span`, verbatim (the H1 rule every register exemption depends on)

```python
def report_span(body: str) -> tuple[int, int] | None:
    """The batch's span from the report's FIRST H1 line, or None when it states none.

    None is the fail-closed answer: a heading the pattern cannot read leaves every register
    edit on the human-merge list (A25's "unparseable is human-merge"). Adjacent case, named: a
    heading stating a span the batch did not actually run is admitted — the span is what the
    session claims; the advisor reads the report against the shard, and the digest review is
    where a claimed span is checked against the work.
    """
    for line in body.splitlines():
        if line.startswith("# "):
            match = _H1_SPAN.search(line)
            if not match:
                return None
            low = int(match.group(1))
            high = int(match.group(2)) if match.group(2) else low
            return (low, high) if low <= high else None
    return None
```

`classify_human_merge` (verbatim structure): every changed path against `HUMAN_MERGE_PREFIXES` and `HUMAN_MERGE_EXACT`, then every pin line in the pin holder except the one `ADVISOR_PIN_LINE` matches, each hit carrying its moved digest so `complete.py` can split off exactly one register entry's movement. The two constants' values were not in the gathered output: `[UNVERIFIED — needs grep -n -A8 'HUMAN_MERGE_PREFIXES =\|HUMAN_MERGE_EXACT =' <cp>/scripts/loop/loopcore.py]`.
