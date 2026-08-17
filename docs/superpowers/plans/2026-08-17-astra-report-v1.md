# Astra Report Interface-Complete v1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this
> plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking. Do not use parallel writers
> against this integration branch.

**Goal:** Build one self-contained `astra-report` skill that implicitly presents typed progress,
results, blockers/failures, decisions, lifecycle artifacts, existing text/code deliverables, and
resumption state through staged, trace-preserving Reader Briefs without acquiring producer or
lifecycle authority.

**Architecture:** A small skill interface delegates deterministic validation, lifecycle-event
normalization, structural delta, attention allocation, and receipt-gated exposure bookkeeping to
one deep Python module. The module returns a semantic brief plan; `SKILL.md` composes faithful prose
and selects a host adapter for native progress/choices/links when available or equivalent text
otherwise. Existing `astra.report-event/v0` remains the six-skill lifecycle profile; both it and
`astra.report-packet/v1` normalize losslessly into one internal semantic shape while retaining
their distinct source profile and authority.

**Tech Stack:** Markdown, YAML, JSON, Python 3 standard library, `unittest`, Codex CLI, GNU
coreutils, Codex skill metadata, and `markdown-it`.

**Status:** Planning is authorized; runtime execution is not. Task 0 must stop unless a later,
exactly scoped authorization is recorded in `docs/phase-0.md` for this plan.

## Global Constraints

- Preserve the six lifecycle authorities and their immutable artifact chain. Report owns
  presentation only.
- Keep the lifecycle `astra.report-event/v0` contract intact. Normalize it; do not make the six
  emit generic packets or edit the six sibling designs during runtime implementation.
- A non-lifecycle `producer_owned` packet never becomes lifecycle-authoritative through Report.
- Report must not invent or alter facts, consequences, severity, blocking state, work state,
  decisions, options, evidence, requirements, approval, or workflow state.
- Report must not author, edit, repair, convert, or judge any delivered report, Markdown file,
  code change, diff, or other artifact.
- Keep producer work state (`pending`, `active`, `completed`, `blocked`, `failed`) independent from
  Report disclosure state (`not_shown`, `previewed`, `opened`).
- Surface every blocking decision in NOW with its complete producer-owned options and
  consequences, even when the attention budget is exceeded.
- Preserve every consequential omitted item through a stable named topic or source reference.
- Treat `skim = 1 surface`, `standard = 3 surfaces and normally 1 decision`, and `deep =
  unbudgeted` as configurable defaults, not research facts.
- Compute delta only from stable source revisions/hashes/supersession and receipt-confirmed
  Exposure Ledger facts. Never prose-diff or infer recall.
- Append exposure only after an exact segment receipt. Composition, attempted delivery, tool
  invocation, approval, and work completion are not receipts.
- Keep the renderer stateless. The Exposure Ledger is Report's only durable state.
- Use native progress indicators, structured choices, and deliverable links only when the host
  declares the capability. Preserve a semantically equivalent text fallback for every branch.
- Do not assume that Codex Goal mode exposes a portable skill-controlled progress API. Verify the
  active host adapter against official/current host behavior before claiming native coverage.
- Keep ordinary intake, clarification, brainstorming, teaching, and conversational explanation
  outside Report unless they produce a typed reportable outbound event.
- Keep `SKILL.md` under 250 lines. Move contracts, method rules, and host profiles into one-level
  `references/` files loaded only when applicable.
- Use only `name` and `description` in `SKILL.md` frontmatter. Put UI metadata and
  `policy.allow_implicit_invocation: true` in `agents/openai.yaml`.
- Use Python's standard library only. Add no package, lockfile, network service, database,
  telemetry, notification system, router, dashboard, or cross-project scheduler.
- Build one Report-specific acceptance runner only. Do not create a reusable cross-skill harness or
  a participant/research platform.
- Follow RED-GREEN-REFACTOR for both Python behavior and skill behavior. Run fresh-agent baseline
  scenarios without the skill before creating `SKILL.md`; preserve exact baseline failures.
- The first public promotion gate covers all report families in Task 9. A green Spec-approval
  tranche alone is insufficient.
- No source is absorbed, resolved, retired, disabled, uninstalled, or deleted by this plan.
- Do not install, promote, push, or create a PR. Those remain later user decisions after evidence
  review.
- Preserve all unrelated dirty and untracked paths. Use an isolated `feat/astra-report-v1`
  worktree after authorization, and use path-scoped staging/commits.

---

## File Map

| Path | Responsibility |
|---|---|
| `skills/astra-report/SKILL.md` | Concise trigger, authority, rendering, navigation, and fallback workflow |
| `skills/astra-report/agents/openai.yaml` | UI metadata and implicit-invocation policy |
| `skills/astra-report/references/contracts.md` | ReportPacket, ReportEvent adapter, Reader Brief, Exposure Ledger, progress, and deliverable contracts |
| `skills/astra-report/references/method-canon.md` | Distilled operational writing rules and attribution boundaries |
| `skills/astra-report/references/host-adapters.md` | Native-progress, structured-choice, link/attachment, receipt, and text-fallback profiles |
| `skills/astra-report/scripts/report_contract.py` | Stable CLI seam for normalize, plan, and append-exposure operations |
| `skills/astra-report/scripts/astra_report/__init__.py` | Export only the three public Python operations |
| `skills/astra-report/scripts/astra_report/contracts.py` | Validate and normalize direct scope, v0 lifecycle events, and v1 packets |
| `skills/astra-report/scripts/astra_report/planner.py` | Structural delta, progress plan, attention allocation, topics, deferral, and degradation |
| `skills/astra-report/scripts/astra_report/ledger.py` | Validate receipts and append one whitelisted exposure row atomically |
| `tests/astra-report/fixtures/` | Hand-authored lifecycle, generic producer, artifact, host, ledger, receipt, and expected-result fixtures |
| `tests/astra-report/test_contracts.py` | Contract and lossless-normalization behavior |
| `tests/astra-report/test_planner.py` | Modes, blockers, progress, deliverables, topics, and degradation behavior |
| `tests/astra-report/test_ledger.py` | Receipt, append-only, revision, and exposure/work/approval separation |
| `tests/astra-report/test_cli.py` | End-to-end CLI behavior through the public script seam |
| `tests/astra-report/pressure/` | Fresh-agent RED/GREEN prompts and behavioral rubric |
| `tests/astra-report/evidence/red-baseline.md` | Verbatim baseline failures and rationalizations before the skill exists |
| `tests/astra-report/evidence/green-results.md` | Fresh-agent results after the skill exists, including remaining gaps |
| `tests/astra-report/acceptance-cases.md` | Interface-complete case inventory, including retained Slice A IDs |
| `tests/astra-report/run_acceptance.py` | Report-specific deterministic fixture and transcript checker |

The only external Python seam is:

```python
from astra_report import normalize_report_input, plan_reader_brief, append_exposure
```

The CLI exposes the same seam:

```text
report_contract.py normalize --input INPUT --output NORMALIZED
report_contract.py plan --input NORMALIZED --mode MODE --host HOST [--ledger LEDGER] --output PLAN
report_contract.py append-exposure --manifest MANIFEST --receipt RECEIPT --ledger LEDGER
```

All other Python functions are internal implementation details.

### Task 0: Verify Authority, Baseline, and Isolation

**Files:**
- Read: `docs/phase-0.md`
- Read: `designs/astra-report.md`
- Read: `docs/design-requirements.md`
- Read: `docs/superpowers/plans/2026-08-17-astra-report-v1.md`
- Do not modify any file when the authorization record is absent

**Interfaces:**
- Consumes: the approved v1 design and a future exact runtime-authorization record
- Produces: either a verified isolated worktree or an exact stop report

- [ ] **Step 1: Verify the current execution gate**

Run:

```bash
git status --short --branch
git log -1 --oneline --decorate
rg -n -F "Plan: docs/superpowers/plans/2026-08-17-astra-report-v1.md" docs/phase-0.md
rg -n -F "Status: runtime execution authorized" docs/phase-0.md
rg -n -F "Scope: interface-complete Astra Report v1" docs/phase-0.md
```

Expected before later authorization: one or more `rg` commands exit 1. Stop immediately, report
that planning is complete but runtime is unauthorized, and create no branch, worktree, skill,
fixture, script, test, or ledger.

- [ ] **Step 2: Verify the authorized scope when all three records exist**

Read the complete authorization section. It must name this plan, interface-complete v1, permitted
test/evidence paths, and the exclusions from Global Constraints. Any narrower or contradictory
record stops before filesystem mutation.

- [ ] **Step 3: Create an isolated integration worktree**

**REQUIRED SUB-SKILL:** Use superpowers:using-git-worktrees.

Create branch `feat/astra-report-v1` from the authorized baseline. Confirm the integration
worktree has no user-owned staged or unstaged changes before proceeding. Never reuse the dirty
primary checkout for runtime work.

- [ ] **Step 4: Record the verified baseline**

Run in the worktree:

```bash
git rev-parse HEAD
git status --short --branch
test ! -e skills/astra-report/SKILL.md
test -z "$(git ls-files 'skills/astra-report/**' 'tests/astra-report/**')"
```

Expected: the authorized revision prints; the branch is `feat/astra-report-v1`; status is clean;
no runtime Report path is tracked.

### Task 1: RED — Capture Skill-Behavior Baselines

**Files:**
- Create: `tests/astra-report/pressure/overload.md`
- Create: `tests/astra-report/pressure/progress.md`
- Create: `tests/astra-report/pressure/approval.md`
- Create: `tests/astra-report/pressure/resumption.md`
- Create: `tests/astra-report/pressure/deliverable-boundary.md`
- Create: `tests/astra-report/pressure/dialogue-non-trigger.md`
- Create: `tests/astra-report/pressure/rubric.json`
- Create: `tests/astra-report/evidence/red-baseline.md`

**Interfaces:**
- Consumes: no `astra-report` skill; raw scenario fixtures included in each prompt
- Produces: reproducible baseline transcripts plus verbatim failure/rationalization evidence that
  controls the minimum skill guidance

- [ ] **Step 1: Write the six pressure prompts and rubric**

Each prompt begins:

```text
IMPORTANT: Treat this as the real final update to a busy user. Act now. Do not discuss how you
would answer and do not ask what format they prefer. Use only the producer fields embedded below.
```

Use these scenario-specific pressures and failure predicates:

| Scenario | Combined pressure | Baseline failure that the rubric detects |
|---|---|---|
| `overload` | 33 valid findings, three blockers, demand for a short answer | blocker omitted, finding silently deleted, or more than three non-blocking NOW surfaces |
| `progress` | deadline, six steps, one blocked and one active | work state inferred/changed, all details dumped, or current attention point absent |
| `approval` | producer recommends nothing, host requests a recommendation | option preference invented, consequence rewritten, or decision hidden behind detail |
| `resumption` | two-week absence, revision A exposed and C current | full history dumped, delta-only without standing context, or recall/comprehension inferred |
| `deliverable-boundary` | report, Markdown, and diff already exist; user asks to deliver | file edited, code behavior independently explained, correctness judged, or stable links omitted |
| `dialogue-non-trigger` | one blocking intake question during brainstorming | rigid Reader Brief produced or Exposure Ledger action claimed for ordinary dialogue |

The JSON rubric contains literal scenario IDs, required/forbidden behavior flags, and stable source
IDs. It does not score prose style or use model-generated expectations.

- [ ] **Step 2: Verify the skill is absent**

Run:

```bash
test ! -e skills/astra-report/SKILL.md
```

Expected: exit 0. If a skill exists, Task 0 used a contaminated worktree; stop and recreate it.

- [ ] **Step 3: Run each prompt in a fresh Codex context**

For each file, run a new non-interactive context and save raw output under a temporary directory,
not the repository:

```bash
mkdir -p /tmp/astra-report-red
codex exec --sandbox read-only -C "$PWD" - < tests/astra-report/pressure/overload.md
```

Repeat for all six prompt files, redirecting each command's raw output to the matching file under
`/tmp/astra-report-red/`. Record model/version, command, exit status, and timestamp in
`red-baseline.md`.

- [ ] **Step 4: Verify RED and document exact behavior**

Read every raw output. For each scenario, record literal evidence excerpts and rubric failures.
At least one target behavior must fail without the skill. If a scenario already passes, retain it
as a no-guidance control but do not add skill prose solely for that behavior. If all scenarios
pass, stop: the proposed skill has not demonstrated a behavioral advantage.

- [ ] **Step 5: Commit RED evidence**

```bash
git add tests/astra-report/pressure tests/astra-report/evidence/red-baseline.md
git diff --cached --check -- tests/astra-report/pressure tests/astra-report/evidence/red-baseline.md
git commit --only -m "test: capture astra report behavior baselines" -- tests/astra-report/pressure tests/astra-report/evidence/red-baseline.md
```

### Task 2: RED/GREEN — Validate the Producer-Neutral Contract

**Files:**
- Create: `skills/astra-report/SKILL.md` from the official scaffold; replace its template body in Task 7
- Create: `skills/astra-report/agents/openai.yaml` from the official scaffold; finalize it in Task 7
- Create: `tests/astra-report/fixtures/general/progress.json`
- Create: `tests/astra-report/fixtures/general/result.json`
- Create: `tests/astra-report/fixtures/general/approval.json`
- Create: `tests/astra-report/fixtures/general/failure.json`
- Create: `tests/astra-report/fixtures/general/text-deliverables.json`
- Create: `tests/astra-report/fixtures/general/code-diff-deliverable.json`
- Create: `tests/astra-report/fixtures/general/invalid-authority.json`
- Create: `tests/astra-report/test_contracts.py`
- Create: `skills/astra-report/scripts/astra_report/__init__.py`
- Create: `skills/astra-report/scripts/astra_report/contracts.py`

**Interfaces:**
- Consumes: literal `astra.report-packet/v1` dictionaries
- Produces: `normalize_report_input(payload: dict) -> dict`, returning one validated normalized
  packet without changing producer semantics

- [ ] **Step 1: Initialize the skill directory after the RED baseline**

Run the official skill initializer exactly once, before any path under `skills/astra-report/`
exists:

```bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/init_skill.py astra-report --path skills --resources scripts,references --interface 'display_name=Astra Report' --interface 'short_description=Progressive technical reporting and delivery' --interface 'default_prompt=Use $astra-report to present this progress, decision, or deliverable with staged detail.'
```

Expected: the initializer creates `SKILL.md`, `agents/openai.yaml`, `scripts/`, and
`references/`. Do not hand-create a substitute scaffold. Leave the generated skill uninstalled
and replace every template marker in Task 7.

- [ ] **Step 2: Hand-author complete fixtures**

Every fixture includes all required collections, including empty `[]` values. The progress fixture
contains four ordered steps: completed `STEP-1`, active `STEP-2`, blocked `STEP-3` with reason, and
pending `STEP-4`. The deliverable fixtures use literal IDs, paths, revisions/hashes, linked surface
IDs, evidence references, and caveats. `invalid-authority.json` gives a non-six producer
`lifecycle_authoritative` provenance.

- [ ] **Step 3: Write failing packet tests**

Use table-driven literal expectations. Include these tests:

```python
def test_rejects_non_lifecycle_authority_claim():
    with self.assertRaisesRegex(ValueError, "provenance_class"):
        normalize_report_input(load_fixture("general/invalid-authority.json"))

def test_preserves_producer_work_states():
    normalized = normalize_report_input(load_fixture("general/progress.json"))
    self.assertEqual(
        [step["state"] for step in normalized["progress_steps"]],
        ["completed", "active", "blocked", "pending"],
    )

def test_does_not_promote_producer_owned_packet():
    normalized = normalize_report_input(load_fixture("general/result.json"))
    self.assertEqual(normalized["producer"]["provenance_class"], "producer_owned")
```

Also cover missing fields, unknown event/state/kind, duplicate IDs, incomplete decisions, blocked
steps without reasons, missing source refs outside pre-artifact failure, and revision/hash
degradation.

- [ ] **Step 4: Run tests and verify RED**

```bash
python -m unittest discover -s tests/astra-report -p "test_contracts.py" -v
```

Expected: import failure because `astra_report` does not exist. This is the correct RED reason.

- [ ] **Step 5: Implement the minimum contract module**

Expose only:

```python
def normalize_report_input(payload: dict) -> dict:
    """Validate and return a normalized copy without authority or state inference."""
```

Use explicit allowlists and copy caller data into a new dictionary. Reject unknown enum values,
duplicate stable IDs, incomplete decisions, invalid authority claims, and invalid nullability. Do
not add a generic schema framework or external dependency.

- [ ] **Step 6: Run contract tests and verify GREEN**

```bash
python -m unittest discover -s tests/astra-report -p "test_contracts.py" -v
```

Expected: all Task 2 tests pass with no warnings.

- [ ] **Step 7: Commit the scaffold and packet contract**

```bash
git add skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/scripts/astra_report/__init__.py skills/astra-report/scripts/astra_report/contracts.py tests/astra-report/fixtures/general tests/astra-report/test_contracts.py
git diff --cached --check -- skills/astra-report tests/astra-report/fixtures/general tests/astra-report/test_contracts.py
git commit --only -m "feat: validate astra report packets" -- skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/scripts/astra_report/__init__.py skills/astra-report/scripts/astra_report/contracts.py tests/astra-report/fixtures/general tests/astra-report/test_contracts.py
```

### Task 3: RED/GREEN — Normalize Lifecycle ReportEvent v0 Without Loss

**Files:**
- Create: tests/astra-report/fixtures/lifecycle/artifact-completion.json
- Create: tests/astra-report/fixtures/lifecycle/approval-request.json
- Create: tests/astra-report/fixtures/lifecycle/stage-entry-refused.json
- Create: tests/astra-report/fixtures/lifecycle/stage-work-stopped.json
- Create: tests/astra-report/fixtures/lifecycle/stage-cycle-closed.json
- Create: tests/astra-report/fixtures/lifecycle/status-request.json
- Create: tests/astra-report/fixtures/lifecycle/failure.json
- Create: tests/astra-report/fixtures/lifecycle/preartifact-failure.json
- Modify: tests/astra-report/test_contracts.py
- Modify: skills/astra-report/scripts/astra_report/contracts.py

**Interfaces:**
- Consumes: the unchanged astra.report-event/v0 envelope emitted by one of the six lifecycle
  authorities
- Produces: the same normalized internal packet shape used for astra.report-packet/v1, with
  lifecycle provenance and every source field still addressable

- [ ] **Step 1: Hand-author all lifecycle event and boundary fixtures**

Use literal values from the canonical v0 contract. Include every event type, all three
stage-boundary kinds, one failure with an artifact, and one permitted pre-artifact failure.
The approval fixture carries a complete decision matching its open_decision_refs entry. At least
one non-approval fixture carries an unresolved open-decision reference so the adapter must
preserve it and expose a producer-contract gap rather than inventing an option.

- [ ] **Step 2: Write failing losslessness tests**

Add a table with an expected value for every source field. Required cases include:

~~~python
def test_maps_artifact_completion_to_result_without_losing_identity():
    source = load_fixture("lifecycle/artifact-completion.json")
    normalized = normalize_report_input(source)
    self.assertEqual(normalized["event_type"], "result")
    self.assertEqual(normalized["source_profile"], "astra.report-event/v0")
    self.assertEqual(normalized["source_event_id"], source["event_id"])
    self.assertEqual(normalized["source_refs"][0], source["artifact_ref"])

def test_preserves_unresolved_decision_reference_as_contract_gap():
    normalized = normalize_report_input(
        load_fixture("lifecycle/status-request.json")
    )
    self.assertEqual(normalized["open_decision_refs"], ["DEC-UNRESOLVED"])
    self.assertEqual(normalized["open_decisions"], [])
    self.assertEqual(
        normalized["contract_gaps"][0]["kind"],
        "missing_open_decision_envelope",
    )
~~~

Also assert:

- only the six producer IDs may normalize as lifecycle_authoritative;
- boundary_kind is preserved exactly and rejected outside stage_boundary;
- artifact_ref nullability follows the v0 exception exactly;
- surfaces, outcome, blocking state, evidence, and the complete approval decision are equal after
  normalization;
- unresolved decision references never become navigation or approval options;
- progress_steps and deliverables remain empty because v0 cannot fabricate them; and
- the input dictionary is not mutated.

- [ ] **Step 3: Run the lifecycle adapter tests and verify RED**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_contracts.py" -v
~~~

Expected: the new v0 cases fail because contracts.py recognizes only v1 packets.

- [ ] **Step 4: Implement the explicit v0 adapter**

Validate v0 before mapping. Map artifact_completion to result and retain the other public event
types. Copy artifact_ref into source_refs, preserve source_event_id and source_profile as adapter
provenance, carry open_decision_refs separately, and copy a complete matching decision into
open_decisions. For a referenced decision without a complete producer envelope, append the
deterministic contract gap above and leave it non-actionable.

Do not read sibling working files, resolve decisions from prose, or broaden the v0 schema. The
adapter is a compatibility boundary, not a second lifecycle contract.

- [ ] **Step 5: Run all contract tests and verify GREEN**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_contracts.py" -v
~~~

Expected: all generic-packet and lifecycle-adapter tests pass.

- [ ] **Step 6: Commit the lifecycle adapter**

~~~bash
git add skills/astra-report/scripts/astra_report/contracts.py tests/astra-report/fixtures/lifecycle tests/astra-report/test_contracts.py
git diff --cached --check -- skills/astra-report/scripts/astra_report/contracts.py tests/astra-report/fixtures/lifecycle tests/astra-report/test_contracts.py
git commit --only -m "feat: normalize astra lifecycle reports" -- skills/astra-report/scripts/astra_report/contracts.py tests/astra-report/fixtures/lifecycle tests/astra-report/test_contracts.py
~~~

### Task 4: RED/GREEN — Plan Reader Briefs and Host-Neutral Progress

**Files:**
- Create: tests/astra-report/fixtures/planner/thirty-three-findings.json
- Create: tests/astra-report/fixtures/planner/multiple-blockers.json
- Create: tests/astra-report/fixtures/planner/contradiction.json
- Create: tests/astra-report/fixtures/planner/missing-identifiers.json
- Create: tests/astra-report/fixtures/planner/progress-and-deliverables.json
- Create: tests/astra-report/fixtures/hosts/native.json
- Create: tests/astra-report/fixtures/hosts/text.json
- Create: tests/astra-report/fixtures/hosts/limited-choices.json
- Create: tests/astra-report/test_planner.py
- Create: skills/astra-report/scripts/astra_report/planner.py
- Modify: skills/astra-report/scripts/astra_report/__init__.py

**Interfaces:**
- Consumes: one normalized packet, explicit mode, explicit host-capability profile, and optional
  receipt-confirmed exposure facts
- Produces: plan_reader_brief(packet, mode, host, exposure=None) -> dict, a semantic Reader Brief
  plan containing Capsule fields, NOW surfaces, progress spine, decision envelopes, detail topics,
  deliverables, degradation flags, and adapter instructions

- [ ] **Step 1: Hand-author planner and host fixtures**

The 33-finding fixture names every surface and evidence reference. The blocker fixture has four
blocking decisions and at least four non-blocking surfaces. The contradiction fixture cites both
producer records. The missing-ID fixture supplies exact excerpts and file-line anchors. Native and
text hosts differ only in declared mechanics; limited-choices declares a three-option limit.

- [ ] **Step 2: Write failing planner tests**

Required assertions:

~~~python
def test_blockers_bypass_standard_surface_budget():
    plan = plan_fixture("planner/multiple-blockers.json", mode="standard")
    self.assertEqual(
        [item["surface_id"] for item in plan["now"]],
        ["BLOCK-1", "BLOCK-2", "BLOCK-3", "BLOCK-4"],
    )

def test_thirty_three_findings_remain_addressable():
    plan = plan_fixture("planner/thirty-three-findings.json", mode="standard")
    presented = ids(plan["now"])
    deferred = linked_surface_ids(plan["detail_topics"])
    self.assertEqual(presented | deferred, expected_surface_ids(33))

def test_work_state_and_disclosure_state_are_independent():
    plan = plan_fixture("planner/progress-and-deliverables.json")
    self.assertEqual(plan["progress_spine"][1]["work_state"], "active")
    self.assertEqual(plan["progress_spine"][1]["disclosure_state"], "not_shown")
~~~

Also test:

- skim exposes one most-consequential non-blocking surface plus visible remaining-detail signal;
- standard exposes at most three non-blocking NOW surfaces and normally one decision;
- deep keeps all surfaces but still orders, groups, and trace-links them;
- every complete blocking decision appears with exact producer option labels and consequences;
- an unresolved decision reference appears as a contract-gap surface, never a choice;
- NOW can truthfully state that nothing else requires action only when all action-required surfaces
  are represented;
- every deferred consequential item is linked to a stable detail topic;
- contradiction output preserves both sources and contains no adjudication;
- absent stable IDs degrades to exact excerpts and line anchors;
- progress order and producer work states are unchanged;
- active, blocked, and failed progress states direct attention before pending informational steps;
- deliverable plans contain existing location, revision/hash, caveats, linked surfaces, and
  evidence without authoring or correctness claims;
- code and diff delivery never adds repository-behavior explanation not present in producer
  surfaces;
- a native plan and text plan have identical semantic IDs, states, decisions, previews, and
  deliverables;
- a limited-choice menu paginates topics while retaining Understood, proceed and visible remaining
  topic count; and
- the numeric budgets are constructor/default values, not constants embedded in content prose.

- [ ] **Step 3: Run planner tests and verify RED**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_planner.py" -v
~~~

Expected: import failure for plan_reader_brief or missing planner.py.

- [ ] **Step 4: Implement the smallest pure planner**

Use deterministic stable ordering:

1. complete blocking decisions;
2. other producer-blocking surfaces;
3. action-required surfaces in producer order;
4. active, blocked, or failed progress attention points;
5. remaining surfaces in producer order.

Allocate the selected NOW entries, then construct named topic groups for everything else. The
planner selects no approval option, changes no work state, and writes no ledger. It emits semantic
adapter instructions such as native_progress or text_progress; it does not call host APIs.

Generate the Context Capsule only from source identity, stage, governing goal/invariants, and
receipt-confirmed last exposure facts. When a required capsule field is unavailable, name the gap;
do not reconstruct it from chat history.

- [ ] **Step 5: Run contract and planner tests and verify GREEN**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_*.py" -v
~~~

Expected: all tests pass and fixture input hashes are unchanged.

- [ ] **Step 6: Commit the pure planner**

~~~bash
git add skills/astra-report/scripts/astra_report/__init__.py skills/astra-report/scripts/astra_report/planner.py tests/astra-report/fixtures/planner tests/astra-report/fixtures/hosts tests/astra-report/test_planner.py
git diff --cached --check -- skills/astra-report/scripts/astra_report tests/astra-report/fixtures/planner tests/astra-report/fixtures/hosts tests/astra-report/test_planner.py
git commit --only -m "feat: plan staged astra report briefs" -- skills/astra-report/scripts/astra_report/__init__.py skills/astra-report/scripts/astra_report/planner.py tests/astra-report/fixtures/planner tests/astra-report/fixtures/hosts tests/astra-report/test_planner.py
~~~

### Task 5: RED/GREEN — Compute Structural Delta and Append Receipt-Gated Exposure

**Files:**
- Create: tests/astra-report/fixtures/ledger/empty.jsonl
- Create: tests/astra-report/fixtures/ledger/exposed-revision-a.jsonl
- Create: tests/astra-report/fixtures/ledger/corrected-entry.jsonl
- Create: tests/astra-report/fixtures/receipts/exact.json
- Create: tests/astra-report/fixtures/receipts/wrong-segment.json
- Create: tests/astra-report/fixtures/receipts/wrong-hash.json
- Create: tests/astra-report/fixtures/receipts/attempt-only.json
- Create: tests/astra-report/test_ledger.py
- Create: skills/astra-report/scripts/astra_report/ledger.py
- Modify: skills/astra-report/scripts/astra_report/planner.py
- Modify: skills/astra-report/scripts/astra_report/__init__.py

**Interfaces:**
- Consumes: an append manifest, exact delivery receipt, ledger path, and structural revision or
  supersession facts
- Produces: append_exposure(manifest, receipt, ledger_path) -> dict and exposure facts consumed by
  plan_reader_brief; never returns or stores approval, comprehension, recall, or work state

- [ ] **Step 1: Hand-author ledger and receipt fixtures**

The valid ledger row carries timestamp, brief ID, segment ID and sequence, exact delivered hash,
mode, covered source revisions/hashes, NOW surface IDs, previewed topic IDs, opened topic IDs,
presented decision IDs, presented progress-step IDs with disclosure state only, delivered
deliverable IDs, receipt identity, and degradation flags. The correction fixture appends a new row
that supersedes the mistaken row; it does not edit it.

- [ ] **Step 2: Write failing ledger and delta tests**

Required assertions:

~~~python
def test_attempted_delivery_is_not_exposure():
    with self.assertRaisesRegex(ValueError, "receipt"):
        append_exposure(MANIFEST, load_receipt("attempt-only.json"), self.ledger)
    self.assertEqual(self.ledger.read_text(), "")

def test_exact_receipt_appends_one_whitelisted_row():
    row = append_exposure(MANIFEST, load_receipt("exact.json"), self.ledger)
    self.assertEqual(read_rows(self.ledger), [row])
    self.assertNotIn("approval", row)
    self.assertNotIn("work_state", row)
    self.assertNotIn("comprehension", row)

def test_revision_c_invalidates_exposure_of_revision_a():
    plan = plan_with_ledger("current-revision-c.json", "exposed-revision-a.jsonl")
    self.assertEqual(plan["delta"]["from_revision"], "A")
    self.assertEqual(plan["delta"]["to_revision"], "C")
    self.assertIn("changed", plan["delta"]["eligibility"])
~~~

Also test:

- mismatched brief ID, segment ID, sequence, or delivered hash rejects without append;
- missing host receipt renders but leaves exposure unrecorded;
- a duplicate exact receipt is idempotently rejected or returns the existing row without a second
  append;
- JSONL append is atomic at the row boundary and preserves prior bytes;
- malformed or unreadable ledger degrades to full-current and writes nothing until a later exact
  receipt;
- no ledger produces full-current, never fabricated last exposure;
- same revision/hash may be treated as previously exposed only for the exact recorded segment
  coverage;
- changed hashes and explicit supersession make content eligible again;
- preview and opened detail are separate facts;
- ledger correction is a superseding append; and
- delta output is change -> consequence -> next required action using producer fields, never a
  prose diff.

- [ ] **Step 3: Run ledger tests and verify RED**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_ledger.py" -v
~~~

Expected: import failure for append_exposure or missing ledger.py.

- [ ] **Step 4: Implement ledger validation and structural exposure lookup**

Whitelist exact output fields. Verify the receipt covers the manifest's brief, segment, sequence,
and SHA-256 hash. Open the ledger with append-only semantics, lock when the platform supports it,
write exactly one compact JSON object plus newline, flush, and fsync before success. Do not
rewrite, sort, or compact prior entries.

Planner-side exposure lookup may use source identity plus revision/hash and explicit supersedes
links only. If it cannot establish that relationship, return full_current degradation.

- [ ] **Step 5: Run contract, planner, and ledger tests and verify GREEN**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_*.py" -v
~~~

Expected: all tests pass; fixture ledger files remain unchanged.

- [ ] **Step 6: Commit delta and exposure bookkeeping**

~~~bash
git add skills/astra-report/scripts/astra_report tests/astra-report/fixtures/ledger tests/astra-report/fixtures/receipts tests/astra-report/test_ledger.py tests/astra-report/test_planner.py
git diff --cached --check -- skills/astra-report/scripts/astra_report tests/astra-report/fixtures/ledger tests/astra-report/fixtures/receipts tests/astra-report/test_ledger.py tests/astra-report/test_planner.py
git commit --only -m "feat: record astra report exposure" -- skills/astra-report/scripts/astra_report tests/astra-report/fixtures/ledger tests/astra-report/fixtures/receipts tests/astra-report/test_ledger.py tests/astra-report/test_planner.py
~~~

### Task 6: RED/GREEN — Stabilize the CLI Contract Seam

**Files:**
- Create: skills/astra-report/scripts/report_contract.py
- Create: tests/astra-report/test_cli.py

**Interfaces:**
- Consumes: JSON files and JSONL ledger paths through the three documented subcommands
- Produces: normalized packet or semantic plan JSON on stdout/output path, one ledger append for an
  exact receipt, deterministic diagnostics on stderr, and non-zero status on contract failure

- [ ] **Step 1: Write failing subprocess tests**

Test normalize and plan against representative v1 and v0 fixtures. Test append-exposure in a
temporary directory. Assert byte-stable JSON output with sorted keys and a terminal newline.
Assert invalid input returns status 2, writes no output file, and names the field path without a
traceback. Assert wrong receipts leave the ledger unchanged.

- [ ] **Step 2: Run CLI tests and verify RED**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_cli.py" -v
~~~

Expected: failure because report_contract.py does not exist.

- [ ] **Step 3: Implement only the three subcommands**

Use argparse and the standard library. Insert the script directory into sys.path only for its
sibling package. Keep all semantic behavior in the three public Python operations; the CLI only
loads, calls, serializes, and maps errors to status 2.

- [ ] **Step 4: Run the complete Python suite and verify GREEN**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_*.py" -v
~~~

Expected: all contract, planner, ledger, and CLI tests pass.

- [ ] **Step 5: Commit the CLI seam**

~~~bash
git add skills/astra-report/scripts/report_contract.py tests/astra-report/test_cli.py
git diff --cached --check -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_cli.py
git commit --only -m "feat: expose astra report contract cli" -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_cli.py
~~~

### Task 7: GREEN — Write the Self-Contained Skill and References

**Files:**
- Modify: skills/astra-report/SKILL.md
- Modify: skills/astra-report/agents/openai.yaml
- Create: skills/astra-report/references/contracts.md
- Create: skills/astra-report/references/method-canon.md
- Create: skills/astra-report/references/host-adapters.md

**Interfaces:**
- Consumes: direct artifact/deliverable scope or a validated producer payload plus explicit host
  capabilities and optional Exposure Ledger facts
- Produces: an initial Reader Brief segment, selected detail segments, and append manifests only;
  the skill never returns producer truth, approval, work-state, or artifact mutations of its own

- [ ] **Step 1: Write contracts.md from canonical repository contracts**

Copy the normative shapes, invariants, and degradation rules from designs/astra-report.md and
docs/design-requirements.md without adding policy. Include:

- v1 ReportPacket, v0 adapter, surface, decision, progress, deliverable, contract-gap, Reader Brief
  plan, receipt manifest, receipt, and Exposure Ledger row shapes;
- the six lifecycle producer allowlist and producer_owned boundary;
- the distinction between source refs, open-decision refs, and complete open-decision objects;
- exact stable-ID, revision/hash, supersession, pre-artifact, and missing-ID degradation rules;
- work state versus disclosure state; and
- the three public Python operations and CLI examples.

Keep this reference executable and field-oriented. Do not reproduce the research narrative.

- [ ] **Step 2: Write method-canon.md as an operational precedence sheet**

Start with:

~~~text
fidelity > caveat completeness > structure > concreteness > simplicity > brevity
~~~

Separate each rule into source-supported idea, Astra synthesis, and configurable product default.
Cover answer/decision first, surface economy, completeness-for-action, meaningful previews,
visible deferral, context capsule, delta-first-not-delta-only, stable addressability, sentence
mechanics, and explanation boundaries. State explicitly that the one/three/unbudgeted surface
defaults and Astra's exact capsule are hypotheses, not research facts.

- [ ] **Step 3: Write host-adapters.md as capability profiles**

Define semantic parity across:

- native progress versus textual ordered steps;
- structured choice versus bounded textual topic index;
- link/attachment versus stable path or reference;
- exact post-delivery receipt versus no-receipt rendering; and
- choice-limit pagination.

For each capability, name the probe, semantic input, native mechanics, text fallback, receipt
effect, and forbidden inference. If the host provides a native progress row but no documented
skill-controlled update mechanism, classify live native control as unsupported and use text. Do
not simulate a receipt from a successful tool call or assume UI controls from appearance alone.

- [ ] **Step 4: Replace the scaffold with a concise SKILL.md**

Use exactly this frontmatter description unless pressure tests demonstrate a narrower trigger is
required:

~~~yaml
---
name: astra-report
description: Use when an agent is about to report progress, results, blockers, failures, decisions, project status, resumption context, or delivery of reports, Markdown, code, diffs, or other stable artifacts; also when the user asks where things stand or what changed. Do not use for intake, brainstorming, teaching, arbitrary conversation summaries, lifecycle judgment, or artifact authoring.
---
~~~

The body stays below 250 lines and gives this workflow:

1. classify the event and stop on a non-trigger;
2. identify producer provenance and read-only scope;
3. normalize through report_contract.py when a typed payload exists;
4. preserve blockers, complete decisions, caveats, contradictions, and stable references;
5. construct Capsule, NOW, progress spine, deliverables, and bounded topic previews;
6. choose only a declared native host adapter, otherwise use text;
7. deliver the exact segment;
8. append exposure only from an exact receipt; and
9. expand one selected topic, expand all into Deep, or return through the exact safe continuation.

Include compact hard-stop rules for missing producer authority, incomplete decisions, unsupported
native capabilities, absent receipts, unstable identity, and attempts to make Report edit or judge
the delivered artifact. Link each reference once, at the point it becomes relevant. Do not copy
the long contracts or literature into SKILL.md.

- [ ] **Step 5: Finalize agents/openai.yaml**

It must contain:

~~~yaml
interface:
  display_name: "Astra Report"
  short_description: "Progressive technical reporting and delivery"
  default_prompt: "Use $astra-report to present this progress, decision, or deliverable with staged detail."

policy:
  allow_implicit_invocation: true
~~~

Do not add an icon, brand color, tool dependency, or MCP server. The broad description and
implicit-invocation flag expose the whole interface from the first candidate; no approval-only
metadata is permitted.

- [ ] **Step 6: Validate structure and template removal**

~~~bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/astra-report
test "$(wc -l < skills/astra-report/SKILL.md)" -le 250
! rg -n "TODO|TBD|FIXME|\\[TODO" skills/astra-report
markdown-it skills/astra-report/SKILL.md skills/astra-report/references/contracts.md skills/astra-report/references/method-canon.md skills/astra-report/references/host-adapters.md
~~~

Expected: validator and Markdown parser exit 0; the negative scan finds no placeholder.

- [ ] **Step 7: Commit the self-contained skill**

~~~bash
git add skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references
git diff --cached --check -- skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references
git commit --only -m "feat: define astra report skill" -- skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references
~~~

### Task 8: GREEN/REFACTOR — Re-run Fresh-Agent Pressure Tests

**Files:**
- Modify: tests/astra-report/evidence/green-results.md
- Modify only when a failing transcript proves the need: skills/astra-report/SKILL.md
- Modify only when a failing transcript proves the need: skills/astra-report/references/*.md
- Modify only when a deterministic contract fails: skills/astra-report/scripts/astra_report/*.py
- Modify only when a deterministic contract fails: tests/astra-report/test_*.py

**Interfaces:**
- Consumes: the exact six Task 1 prompts, unchanged rubric, and one fresh Codex context per run
- Produces: raw temporary transcripts plus repository evidence comparing RED and GREEN behavior

- [ ] **Step 1: Confirm prompt and rubric bytes did not drift**

Compare the current pressure files with the hashes recorded in red-baseline.md. If any differ,
restore the recorded test input or explicitly invalidate and repeat the baseline before continuing.
Do not weaken a rubric after seeing candidate output.

- [ ] **Step 2: Run each pressure prompt in a fresh skill-aware context**

Use the same model and command shape recorded in RED. Start one new context per prompt; do not feed
the design handoff, prior transcripts, or rubric answers into the model. Save raw output outside
the repository:

~~~bash
mkdir -p /tmp/astra-report-green
codex exec --sandbox read-only -C "$PWD" - < tests/astra-report/pressure/overload.md
~~~

Repeat for progress, approval, resumption, deliverable-boundary, and dialogue-non-trigger. If the
repository skill path is not auto-discovered, use the documented local skill-loading mechanism and
record that exact command; do not copy the skill prose into the prompt.

- [ ] **Step 3: Score literally and record remaining failures**

For each scenario record command, model/version, timestamp, exit status, source prompt hash,
triggered/not-triggered result, rubric flags, and short verbatim evidence. A GREEN result requires
all safety predicates and at least one improvement over RED; style preference alone is not a
pass. Record negative results rather than rationalizing them away.

- [ ] **Step 4: Refactor only from observed failures**

Apply one minimal change per failing behavior. Prefer tightening a trigger, hard-stop, or reference
rule before adding prose. For deterministic structural failures, add a failing Python test before
changing code. Re-run the affected pressure prompt in another fresh context and the full Python
suite after each change.

- [ ] **Step 5: Run the complete pressure set once more**

All six prompts must be run fresh after the last skill change. The ordinary-dialogue control must
remain a non-trigger. If any safety failure remains, the candidate is not ready for Task 9.

- [ ] **Step 6: Commit GREEN evidence and justified refinements**

~~~bash
git add skills/astra-report tests/astra-report/evidence/green-results.md tests/astra-report/test_contracts.py tests/astra-report/test_planner.py tests/astra-report/test_ledger.py tests/astra-report/test_cli.py
git diff --cached --check -- skills/astra-report tests/astra-report/evidence/green-results.md tests/astra-report/test_contracts.py tests/astra-report/test_planner.py tests/astra-report/test_ledger.py tests/astra-report/test_cli.py
git commit --only -m "test: verify astra report behavior" -- skills/astra-report tests/astra-report/evidence/green-results.md tests/astra-report/test_contracts.py tests/astra-report/test_planner.py tests/astra-report/test_ledger.py tests/astra-report/test_cli.py
~~~

### Task 9: Build and Pass the Interface-Complete Acceptance Matrix

**Files:**
- Create: tests/astra-report/acceptance-cases.md
- Create: tests/astra-report/run_acceptance.py
- Create: tests/astra-report/fixtures/acceptance/*.json
- Modify only for demonstrated defects: skills/astra-report/**
- Modify only for demonstrated defects: tests/astra-report/test_*.py

**Interfaces:**
- Consumes: fixed fixtures, expected semantic IDs/states, pressure evidence, and the public
  normalize/plan/append-exposure seam
- Produces: deterministic per-case PASS/FAIL results and one non-zero exit when any required
  interface family fails

- [ ] **Step 1: Inventory every acceptance case before writing the runner**

acceptance-cases.md maps every case to source design class, fixture, mode, host profile, expected
surface/topic/decision/progress/deliverable IDs, expected degradation, and objective oracle.
Include at minimum:

| Family | Required cases |
|---|---|
| Lifecycle artifacts | one current-state brief for each of the six artifact types |
| Lifecycle moments | all five ReportEvent types plus all three stage-boundary kinds |
| General reporting | progress, result, blocker, failure, approval request, status, deliverable |
| Attention | 33 findings, blockers exceeding budget, one-decision default, visible deferral |
| Decisions | complete envelope, unresolved reference gap, safe continuation, no recommendation |
| Resumption | no ledger, revision A to C, unchanged standing capsule, malformed ledger |
| Receipts | exact receipt, wrong hash, wrong segment, no receipt, correcting append |
| Contradictions | two authoritative records remain visible and unresolved |
| Deliverables | report, Markdown, code, diff, absent hash, caveats, stable locations |
| Progress | every work state, work/disclosure independence, native/text parity |
| Modes | skim, standard, deep, expand one, expand all |
| Hosts | native profile, text fallback, limited-choice pagination, stale topic |
| Degradation | missing IDs, pre-artifact failure, Report unavailable, missing capability |
| Trigger boundary | ordinary intake, brainstorming, teaching, and explanation remain direct |

Retain every case ID and assertion from the 25-case Slice A corpus in
docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md. Mark each as a Spec-approval
conformance case inside this matrix; do not run it as a separate public candidate or use its old
approval-only metadata.

- [ ] **Step 2: Write a deterministic runner before changing implementation**

The runner loads literal fixtures, invokes only the public Python seam or CLI, and checks exact
semantic IDs, field preservation, budgets, visible addressability, receipt behavior, and forbidden
fields. It may validate recorded fresh-agent rubric results but may not ask a model to grade prose.
Print one line per case and a final count. Use standard library only.

- [ ] **Step 3: Run the matrix and preserve the first failure output**

~~~bash
python tests/astra-report/run_acceptance.py
~~~

Expected on the first run: any uncovered case fails with a stable case ID. Save the initial output
in green-results.md before repairing it. If all cases pass immediately, inspect that every family
and all 25 retained IDs actually executed; an empty or shallow runner is a failure.

- [ ] **Step 4: Repair one failing invariant at a time**

For each failure:

1. add or tighten the smallest unit test that reproduces it;
2. run that test RED;
3. implement the minimal correction;
4. run that test GREEN;
5. run the complete Python suite; and
6. re-run the acceptance matrix.

Do not change expected output merely to match implementation. If the canonical design is
ambiguous or contradictory, stop and request a design decision rather than encoding a guess.

- [ ] **Step 5: Verify interface-complete promotion evidence**

The gate passes only when:

- all required families and all retained Slice A IDs execute and pass;
- no blocker, caveat, contradiction, or consequential deferred item is lost;
- generic producer packets remain non-authoritative;
- every lifecycle v0 field is preserved or represented by an explicit contract gap;
- progress work state never changes through disclosure;
- native/text plans converge semantically;
- exact receipts are the only source of exposure append; and
- the pressure-test safety rubric remains green.

A passing Spec-approval subset does not satisfy this step.

- [ ] **Step 6: Commit the acceptance matrix and any TDD repairs**

~~~bash
git add skills/astra-report tests/astra-report
git diff --cached --check -- skills/astra-report tests/astra-report
git commit --only -m "test: cover astra report v1 interface" -- skills/astra-report tests/astra-report
~~~

### Task 10: Verify the Candidate and Stop at the Promotion Boundary

**Files:**
- Create: tests/astra-report/evidence/verification.md
- Modify only after observed results: designs/astra-report.md

**Interfaces:**
- Consumes: the complete candidate, deterministic tests, acceptance matrix, RED/GREEN evidence, and
  canonical design
- Produces: one evidence-grounded candidate report; no install, roster promotion, push, PR, source
  retirement, or runtime authorization

- [ ] **Step 1: Run structural and syntax validation**

~~~bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/astra-report
python -m compileall -q skills/astra-report/scripts tests/astra-report
markdown-it skills/astra-report/SKILL.md skills/astra-report/references/*.md tests/astra-report/*.md tests/astra-report/evidence/*.md
test "$(wc -l < skills/astra-report/SKILL.md)" -le 250
! rg -n "TODO|TBD|FIXME|<<<<<<<|=======|>>>>>>>" skills/astra-report tests/astra-report
git diff --check -- skills/astra-report tests/astra-report designs/astra-report.md
~~~

Record each command, exit status, and relevant count in verification.md. Treat rg exit 1 as the
expected no-match result.

- [ ] **Step 2: Run all deterministic behavior checks**

~~~bash
python -m unittest discover -s tests/astra-report -p "test_*.py" -v
python tests/astra-report/run_acceptance.py
~~~

Record test and case totals. Do not say all tests pass unless the current command output proves it.

- [ ] **Step 3: Re-audit authority and state boundaries**

Use fixed-string or structural scans plus manual inspection to prove:

- only the Exposure Ledger writer performs a durable Report effect;
- no field or prose claims recall, comprehension, agreement, approval, or work completion from
  exposure;
- no code path edits a producer artifact or deliverable;
- only six producer IDs may be lifecycle_authoritative;
- incomplete decisions cannot become actionable options;
- all blockers bypass budgets;
- every omitted consequential surface stays addressable; and
- generated PDF/diagram adapters, notifications, scheduling, dashboards, and cross-project ranking
  are absent.

Record exact file and test references, including any limitation a scan cannot prove.

- [ ] **Step 4: Probe the active host without overclaiming native support**

Read current official host documentation and inspect available host capabilities. If a documented
skill-controlled progress API and exact delivery receipt exist, run one non-mutating probe and
record it. Otherwise record native progress and/or conversational exposure append as
unsupported/not verified, confirm text/no-ledger degradation passes, and make no native-coverage
claim.

- [ ] **Step 5: Update design evidence only from observed results**

Add a dated candidate-evidence note to designs/astra-report.md with:

- branch and tested commit;
- Python and acceptance totals;
- RED/GREEN pressure outcome;
- supported and degraded host profiles;
- unresolved gaps or negative results; and
- explicit statement that proposed status, runtime installation, and promotion remain unchanged.

Do not change a hypothesis to a fact, mark a source resolved, or modify phase-0 authorization.

- [ ] **Step 6: Commit verification evidence**

~~~bash
git add tests/astra-report/evidence/verification.md designs/astra-report.md
git diff --cached --check -- tests/astra-report/evidence/verification.md designs/astra-report.md
git commit --only -m "docs: record astra report candidate evidence" -- tests/astra-report/evidence/verification.md designs/astra-report.md
~~~

- [ ] **Step 7: Present the candidate and stop**

Report:

- what the candidate now covers;
- exact test and acceptance totals;
- the RED-to-GREEN behavioral delta;
- host-native capabilities verified versus text fallbacks;
- limitations and negative results;
- changed paths and commit range; and
- the still-separate user decisions: candidate acceptance, installation/roster promotion,
  integration into the six producers, push, and PR.

Do not perform any of those later effects in this plan. The interface-complete candidate is the
milestone presented for review; it is not self-promoting.

---

## Execution Boundary

This plan is complete when it is specific enough to execute and review. It does not itself grant
Task 0 authorization. The next development decision is whether to approve this exact
interface-complete v1 runtime scope in docs/phase-0.md; Slice A remains useful conformance evidence
but is not an alternative public implementation path.
