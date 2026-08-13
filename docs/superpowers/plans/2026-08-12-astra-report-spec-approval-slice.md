# Astra Report Spec-Approval Vertical Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build one non-retiring vertical slice in which a Spec-owned pending revision and approval `ReportEvent` become a faithful, plain-language Reader Brief, a receipt-confirmed delivery is appended to Report's Exposure Ledger, and the user's answer remains solely in Spec's approval record.

**Architecture:** The six-authority plus reporting-surface policy and all six producer contracts are already canonical at `be6249e`; this plan consumes that existing seam rather than rebuilding it. Implement Report as a prompt-driven skill backed by one small Python standard-library contract tool: the tool validates producer envelopes, verifies revision exposure, and appends one whitelisted record per receipt-confirmed segment, while the skill performs trace-preserving staged explanation from immutable artifacts. Exercise only the delegated Spec-approval path with the 25 mechanical Slice A cases; this slice does not implement the full Spec skill, public direct-request Report, a general lifecycle runtime, a reusable harness, or the full 92-source corpus.

**Tech Stack:** Markdown, YAML, JSON, Python 3 standard library, `unittest`, Codex CLI, `jq`, GNU coreutils, Codex skill metadata, `markdown-it` validation.

**Status:** Reconciled on 2026-08-13 against the approved Slice A design at commit `44d1f16`; runtime execution is not authorized. Tasks 3–7 may begin only after the separately authorized coordinator-ledger reconciliation lands and the user makes a new explicit runtime-execution choice recorded in `docs/phase-0.md`.

## Global Constraints

- Preserve the lifecycle authority path `astra-critique -> astra-spec -> astra-implement -> astra-test -> astra-ship`; Report owns presentation, never lifecycle judgment.
- Keep all migrated collision rows `claimed`, never `resolved`; no source is absorbed, retired, disabled, uninstalled, or moved into the locked 92-source target by this slice.
- Preserve output-only delegation: the six lifecycle authorities remain directly invocable; rich skill-to-user output uses typed `I(reporting)`.
- Report must never invent, repair, approve, reject, waive, or mutate authoritative artifact content.
- An approval request must preserve the decision identity, every option and producer-assigned consequence, evidence references, and blocking state.
- The Exposure Ledger records presentation only. It must not record an answer, selected option, or approval state.
- `artifact_ref` is non-null whenever an authoritative artifact exists. It may be null only for a pre-artifact refusal or failure carrying a stable producer event identity and evidence or failure anchors.
- The local files under `books/` are research inputs only: do not edit, stage, commit, package, or require them at runtime.
- Carry only distilled, attributed method rules into `skills/astra-report/references/method-canon.md`; do not reproduce source prose.
- Use Python's standard library only. Do not add package, lockfile, network, service, database, telemetry, router, adapter, or shared runtime dependencies.
- Require an explicit Exposure Ledger path from the caller in this slice; do not select a permanent project-wide default before the open storage decision is resolved.
- Require a caller-confirmed, non-empty delivered-brief path before appending exposure. Composition alone is not exposure; a chat host without a receipt renders without appending and may repeat the revision later.
- Text conversation is the only delivery surface. PDF and diagram delivery remain post-MVP and unimplemented.
- Limit evaluation infrastructure to the Spec approval fixtures in this plan. Do not build a universal runner or the full source-retirement corpus.
- Treat the 15-pair consultant and final trigger-surface gate as satisfied by roadmap amendments 8 and 9, culminating in commit `be6249e`. Verify that commit as an ancestor; do not redo those amendments.
- Treat the coordinator ledger as a separate documentation prerequisite. Before runtime, the seven Report secondary-role rows must be `claimed`, the `diagram` consumer amendment must be present, `designs/astra-report.md` §12.4 item 3 must be complete, and the trigger-plan ledger hash must carry an explicit historical-supersession record.
- Runtime work also requires a new explicit choice to execute this plan. That choice authorizes only this slice and must be recorded in `docs/phase-0.md`; it does not waive any retirement or installation gate.
- This slice implements the delegated Spec approval path only. It does not implement the design's public direct-request path, and its skill metadata must not advertise direct artifact, catch-up, or project-status triggers before that path has its own behavioral case.
- Use the 25 unique case IDs and 16 selected corpus classes in `docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md` §§3–5. Class 30 is only the named structural proxy. Class 35's producer-preference-positive branch is blocked because `astra.report-event/v0` has no preference field; never invent `recommended` or infer it from option order.
- Every delivered initial or detail segment receives its own manifest, exact receipt, and Exposure Ledger row. A preview is always `preview` exposure; only a selected, receipt-confirmed body is `detail` exposure.
- Keep every acceptance check deterministic. A missing fixture or unavailable host branch is `blocked` or a recorded limitation, never `pass`; no prose-quality judge or blinded-evaluation machinery belongs in this slice.
- Preserve all unrelated dirty and untracked paths. Stage only the exact paths named by each task.
- Each commit must contain one reviewable functionality and pass a path-scoped `git diff --cached --check` that lists the task's exact paths before creation.
- The worktree begins with user-owned staged and unstaged changes. Snapshot the pre-existing index, use `git commit --only` with the task's exact paths for every commit, and verify those unrelated entries remain staged afterward.

---

## File Map

| Path | Responsibility |
|---|---|
| `docs/design-requirements.md` | Canonical roster, typed `I(reporting)`, and common `ReportEvent` rules |
| `docs/six-skill-source-absorption.md` | Locked-record amendment for Report's approved secondary slices without changing the 92 count |
| `docs/design-roadmap.md` | Coordinator roadmap amendment and vertical-slice sequencing |
| `docs/phase-0.md` | Historical phase-0 boundary plus the explicitly authorized post-phase-0 slice transition |
| `docs/phase-0-ledgers.md` | Seven secondary claims plus the existing `diagram` row amendment; all remain claimed |
| `docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md` | Approved 25-case Slice A contract and drift-risk oracle capture |
| `designs/astra-{critique,understand-code,spec,implement,test,ship}.md` | Producer-side reporting hooks and degraded fallback contracts |
| `designs/astra-report.md` | Approved Report design and implementation-evidence status |
| `docs/research/2026-08-12-astra-report-method-canon.md` | Reproducible local-book and primary-source distillation |
| `skills/astra-report/SKILL.md` | Runtime workflow and fidelity rules |
| `skills/astra-report/agents/openai.yaml` | User-facing skill metadata |
| `skills/astra-report/references/report-contracts.md` | Exact ReportEvent, Reader Brief manifest, and Exposure Ledger field contracts |
| `skills/astra-report/references/method-canon.md` | Compact operational rules traced to the research note |
| `skills/astra-report/scripts/report_contract.py` | Deterministic event validation, artifact-reference consistency checks, and append-only exposure writing |
| `tests/astra-report/fixtures/spec-pending.json` | Immutable Spec-owned pending revision for the slice |
| `tests/astra-report/fixtures/spec-pending-revision-2.json` | Same pending approval state on a new, unexposed artifact revision |
| `tests/astra-report/fixtures/spec-approval-event.json` | Valid approval request referencing the Spec fixture |
| `tests/astra-report/fixtures/spec-revised-event.json` | Approval request for the unexposed revision-2 fixture |
| `tests/astra-report/fixtures/preartifact-refusal-event.json` | Valid null-artifact boundary case |
| `tests/astra-report/fixtures/preartifact-failure-event.json` | Valid null-artifact pre-artifact failure case |
| `tests/astra-report/fixtures/spec-status-event.json` | Non-decision producer-fallback fixture |
| `tests/astra-report/fixtures/spec-over-budget-event.json` | Four-blocker attention-budget fixture |
| `tests/astra-report/test_report_contract.py` | Contract and ledger unit tests |
| `tests/astra-report/evals/spec-approval-prompt.md` | Fixed dogfood invocation |
| `tests/astra-report/evals/spec-approval-text-index-prompt.md` | Same initial segment under the text-index host branch |
| `tests/astra-report/evals/spec-approval-detail-prompt.md` | Structured-host fixed topic selection and selected-only detail segment |
| `tests/astra-report/evals/spec-approval-text-index-detail-prompt.md` | Text-index fixed topic selection and semantically identical detail segment |
| `tests/astra-report/evals/spec-over-budget-prompt.md` | Four-blocker render under the standard three-surface cap |
| `tests/astra-report/evals/spec-revised-prompt.md` | Revision-2 exposure-state render without approval inference |
| `tests/astra-report/evals/spec-approval-fallback-prompt.md` | Fixed producer fallback case when Report is unavailable |
| `tests/astra-report/evals/spec-status-fallback-prompt.md` | Fixed non-decision producer fallback case |
| `tests/astra-report/evals/render-result.schema.json` | Structured-output contract for an initial or detail segment run |
| `tests/astra-report/evals/spec-approval-cases.md` | Exact C4–C35 case-to-evidence matrix; no subjective rubric |
| `tests/astra-report/verify_slice_a.py` | Slice-specific mechanical verifier; not a reusable corpus harness |

### Task 0: Verify the Approved Baseline and Runtime Gate

**Files:**
- Read: `docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md`
- Read: `docs/design-roadmap.md`
- Read: `docs/phase-0.md`

**Interfaces:**
- Consumes: approved Slice A design commit `44d1f16`, canonical trigger commit `be6249e`, and a later explicit runtime-execution record
- Produces: a fail-closed execution preflight; no repository mutation

- [ ] **Step 1: Snapshot and preserve the live workspace state**

Run:

```bash
git status --short --branch
git diff --cached --name-only
git diff --name-only
```

Expected: record the live output. Preserve every pre-existing staged, unstaged, and untracked path. Do not clean, stash, restage, or infer that a path is disposable.

- [ ] **Step 2: Verify the approved design and canonical trigger record**

Run:

```bash
git merge-base --is-ancestor 44d1f16 HEAD
git merge-base --is-ancestor be6249e HEAD
markdown-it docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md >/dev/null
python - <<'PY'
from pathlib import Path

spec = Path("docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md").read_text()
for token in (
    "Selected: 16 classes → 25 cases",
    "Classes 30 and 35 are bounded partials",
    "class-35 producer-preference boundary",
    "authorizes **no** runtime skill",
):
    assert token in spec, token
roadmap = Path("docs/design-roadmap.md").read_text()
assert "Section 14.4 item 1 is complete" in roadmap
PY
```

Expected: every command exits 0. A missing ancestor or token means the authority source drifted; stop and reconcile the design rather than weakening this check.

- [ ] **Step 3: Enforce the separate runtime-authorization gate**

Before creating any path under `skills/astra-report/` or `tests/astra-report/`, require a later governance commit in `docs/phase-0.md` containing all of these exact statements:

```text
Spec-to-Report Slice A runtime execution authorized.
Scope is only the delegated Spec approval path in the reconciled implementation plan.
Installation, public direct-request Report, reusable harness extraction, source retirement,
deletion, push, and PR remain unauthorized.
```

Run:

```bash
python - <<'PY'
from pathlib import Path

text = Path("docs/phase-0.md").read_text()
required = (
    "Spec-to-Report Slice A runtime execution authorized.",
    "Scope is only the delegated Spec approval path in the reconciled implementation plan.",
    "Installation, public direct-request Report, reusable harness extraction, source retirement,",
    "deletion, push, and PR remain unauthorized.",
)
missing = [token for token in required if token not in text]
assert not missing, "runtime authorization absent; stop before Task 3: " + repr(missing)
PY
```

Expected before a new user execution choice: non-zero with `runtime authorization absent`; stop. Design approval and documentation reconciliation are not substitutes.

### Task 1: Verify the Coordinator Reconciliation

**Files:**
- Read: `docs/phase-0-ledgers.md`
- Read: `designs/astra-report.md`
- Read: `docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md`

**Interfaces:**
- Consumes: the separately committed coordinator-ledger reconciliation authorized by the Slice A design
- Produces: exact source-claim and hash-provenance evidence for Task 3; no repository mutation

- [ ] **Step 1: Verify the eight exact ledger occurrences**

Run:

```bash
python - <<'PY'
from pathlib import Path

ledger = Path("docs/phase-0-ledgers.md").read_text().splitlines()
expected = {
    "cm-docs-and-knowledge-01": "explanation-quadrant structure slice",
    "cm-docs-and-knowledge-02": "chunking and fresh-reader-testing playbook slice",
    "cm-docs-and-knowledge-03": "plain-language, audience-targeting, and fresh-reader-test slice",
    "cm-docs-and-knowledge-04": "post-MVP delivery adapter",
    "cm-docs-and-knowledge-05": "status/leadership/FAQ register slice",
    "cm-docs-and-knowledge-07": "working-memory chunk-sizing slice",
    "cm-docs-and-knowledge-09": "consumer-framing and uncertainty-disclosure slice",
}
for occurrence, role in expected.items():
    line = next(row for row in ledger if f"`{occurrence}`" in row)
    assert "| independent reference | independent |" in line, line
    assert f"`astra-report`: {role}" in line, line
    assert "| claimed |" in line and "| resolved |" not in line, line
diagram = next(row for row in ledger if "`cm-design-and-visual-21`" in row)
assert "`astra-report`: post-MVP supplemental-delivery consumer" in diagram, diagram
assert "| claimed |" in diagram and "| resolved |" not in diagram, diagram
PY
```

Expected: exit 0; all seven documentation occurrences are claimed independent references and `diagram` retains its prior home while adding only the post-MVP Report consumer.

- [ ] **Step 2: Verify the dependent completion and hash-provenance records**

Run:

```bash
python - <<'PY'
from hashlib import sha256
from pathlib import Path

report = Path("designs/astra-report.md").read_text()
assert "3. **Complete, 2026-08-13.** Apply the section 4.5 row changes" in report
plan = Path("docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md").read_text()
old = "3f2babefc8f178fab9b77c36738e516530a5426abcdb69c261365a167fe9d15a"
current = sha256(Path("docs/phase-0-ledgers.md").read_bytes()).hexdigest()
assert old in plan
assert "historical baseline superseded by the authorized Slice A ledger reconciliation" in plan
assert current in plan, current
PY
```

Expected: exit 0. The old digest remains as evidence for the trigger tranche; the current digest is separately recorded and never retroactively substituted into the old expected-output block.

### Task 2: Verify the Existing Producer Interface

**Files:**
- Read: `docs/design-requirements.md`
- Read: `designs/astra-{critique,understand-code,spec,implement,test,ship}.md`

**Interfaces:**
- Consumes: canonical `I(reporting)` and `astra.report-event/v0` already landed at `be6249e`
- Produces: the immutable producer interface consumed by Task 3; no repository mutation

- [ ] **Step 1: Verify all six producer contracts without reapplying them**

Run:

```bash
python - <<'PY'
from pathlib import Path

files = [
    Path("designs/astra-critique.md"),
    Path("designs/astra-understand-code.md"),
    Path("designs/astra-spec.md"),
    Path("designs/astra-implement.md"),
    Path("designs/astra-test.md"),
    Path("designs/astra-ship.md"),
]
for path in files:
    text = path.read_text()
    for token in (
        "I(reporting)",
        "ReportEvent",
        "reporting.surfaces",
        "consequence",
        "reporting.open_decisions",
    ):
        assert token in text, (path, token)
requirements = Path("docs/design-requirements.md").read_text()
for token in (
    "Literal `astra.report-event/v0`",
    "`{option_id, label, consequence}`",
    "Only the producer",
    "records the user's answer",
):
    assert token in requirements, token
spec = Path("designs/astra-spec.md").read_text()
assert "Spec alone records the answer" in spec
PY
```

Expected: exit 0. Do not edit or recommit these seven canonical files in this slice.

- [ ] **Step 2: Pin the class-35 schema limit**

The `v0` approval option is exactly `{option_id, label, consequence}`. Task 3 must reject an added `recommended` key; Task 5 must use text fallback when a host demands an approval recommendation. A future positive producer-preference branch requires a separately approved schema amendment and is `blocked`, never silently passed, in this slice.

### Task 3: ReportEvent Validator and Spec Fixtures

**Files:**
- Create: `skills/astra-report/scripts/report_contract.py`
- Create: `tests/astra-report/fixtures/spec-pending.json`
- Create: `tests/astra-report/fixtures/spec-approval-event.json`
- Create: `tests/astra-report/fixtures/preartifact-refusal-event.json`
- Create: `tests/astra-report/fixtures/preartifact-failure-event.json`
- Create: `tests/astra-report/test_report_contract.py`

**Interfaces:**
- Consumes: the already-canonical `astra.report-event/v0` verified by Task 2
- Produces: `validate_event(event: dict) -> list[str]`, `verify_artifact_ref(event: dict, root: Path) -> list[str]`, and a CLI `validate-event EVENT --root ROOT`

- [ ] **Step 1: Initialize the skill package shell**

Run before any `skills/astra-report/` file exists:

```bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/init_skill.py astra-report --path skills --resources scripts,references --interface 'display_name=Astra Report' --interface 'short_description=Present Astra approvals clearly and faithfully' --interface 'default_prompt=Use $astra-report to render this delegated Astra approval event faithfully for the user.'
```

Expected: the skill directory, placeholder `SKILL.md`, and `agents/openai.yaml` are created. Keep the placeholder and metadata uncommitted until Task 5; Task 3 stages only the script and tests named in its commit step.

- [ ] **Step 2: Create the immutable Spec fixture and approval envelope**

Use `ACS-REPORT-001`, revision `1`, and the field names from `designs/astra-spec.md` section 2.5 in `spec-pending.json`: intent; observed before state; problem linked to evidence item `F-REPORT-001`; selected solution; reason selected; two rejected alternatives and their consequences; after state explicitly marked `projected`; requirements `REQ-REPORT-001` through `REQ-REPORT-004`; acceptance criteria `AC-REPORT-001` through `AC-REPORT-005`; and pending decision `DEC-SPEC-001`.

The fixture is the concrete revision of the approved §6 stimulus profile. It must contain six addressable source sections — `intent`, `current_state`, `decisions`, `behavior`, `evidence_and_uncertainty`, and `readiness` — plus all of these exact drift probes:

| Probe | Exact fixture content |
|---|---|
| Graded finding | `evidence.items[]` contains exactly `{evidence_id: F-REPORT-001, source_kind: contract, source_ref: F-REPORT-001, claim: "Grade blocking. Observation: Raw lifecycle artifacts preserve authority but overload the approval surface. Evidence ref: USER-REPORT-001.", certainty: observed, captured_at: 2026-08-13T00:00:00+08:00}`; the grade is producer text, not an invented Spec-schema field |
| Project-status statement | `Specification revision 1 is reviewing and blocked only on DEC-SPEC-001.` |
| Unfamiliar term | `I(reporting)` with artifact-grounded definition `output-only use of Report's rendering capability while Spec retains decision authority` |
| Material caveat | `A written segment file is the only receipt supported by this slice.` |
| Explicitly unverified claim | `Conversation-host receipt integration is unavailable and remains unverified.` |

Do not add a `recommended` field anywhere. The selected design direction is historical Spec content; it is not a recommendation about how the user should answer `DEC-SPEC-001`.

For this fixture only, calculate the producer-owned hash by removing the root fields `content_hash`, `approval`, `delivery`, and `lifecycle`, then serializing the remaining object with sorted keys, UTF-8, `ensure_ascii=False`, and separators `(',', ':')`. Run this read-only command after creating the fixture with `content_hash: null`:

```bash
python - <<'PY'
import hashlib
import json
from pathlib import Path

path = Path("tests/astra-report/fixtures/spec-pending.json")
artifact = json.loads(path.read_text(encoding="utf-8"))
meaning = {
    key: value
    for key, value in artifact.items()
    if key not in {"content_hash", "approval", "delivery", "lifecycle"}
}
canonical = json.dumps(
    meaning,
    ensure_ascii=False,
    separators=(",", ":"),
    sort_keys=True,
).encode("utf-8")
print("sha256:" + hashlib.sha256(canonical).hexdigest())
PY
```

Replace the fixture's `null` with the printed value and copy that value unchanged into `spec-approval-event.json`. Add a fixture test that repeats this calculation. This is test provenance, not a Report algorithm: production Report validates identity/revision/hash equality against producer fields and does not redefine or recompute Spec's hash.

Use these exact meaning-bearing values; fill the remaining required section 2.5 collections with explicit `[]` and nullable fields with explicit `null`:

| Field | Exact value |
|---|---|
| `title` | `Delegate Astra approval reporting` |
| `intent.problem` | `The lifecycle artifacts preserve authority and evidence, but their raw form makes approval slow and difficult to review.` |
| `intent.desired_outcomes[0].statement` | `Projected after: the user receives one faithful, readable approval brief while Spec remains the only owner of the decision and answer.` |
| `current_state.observed_behavior[0].statement` | `Before: each lifecycle skill presents its own artifact directly in its native structure.` |
| `current_state.observed_behavior[1].statement` | `Problem: the user must reconstruct outcome, rationale, alternatives, consequences, and the approval ask across dense fields.` |
| `current_state.observed_behavior[1].evidence_refs` | `["F-REPORT-001"]` |
| selected `decisions.alternatives[]` summary | `Add a non-authoritative Report surface downstream of the six lifecycle authorities.` |
| selected-direction rationale | `This keeps lifecycle authority with Spec while centralizing only human-facing explanation and exposure bookkeeping.` |
| rejected alternative 1 | `Keep rich reporting inside all six skills`; consequence: `Presentation logic and user context remain duplicated across six contracts.` |
| rejected alternative 2 | `Make Report the input orchestrator`; consequence: `Report would gain routing and intake authority beyond the approved output-only boundary.` |
| `REQ-REPORT-001` | `Report must preserve every producer-owned identity, certainty, caveat, consequence, and evidence reference.` |
| `REQ-REPORT-002` | `Report must explain the artifact in plain, scannable chunks without inventing content.` |
| `REQ-REPORT-003` | `An approval brief must present every option and its producer-assigned consequence before asking for a decision.` |
| `REQ-REPORT-004` | `The Exposure Ledger must record presentation and must not record the user's answer or approval state.` |
| `AC-REPORT-001` | A field-by-field comparison finds no changed identity, certainty, caveat, consequence, or evidence reference. |
| `AC-REPORT-002` | A fresh reader can identify before, problem, selected fix, rationale, projected after, and both rejected alternatives from labeled chunks. |
| `AC-REPORT-003` | `DEC-SPEC-001` renders all three options and consequences in NOW. |
| `AC-REPORT-004` | The appended exposure record contains `DEC-SPEC-001` and contains no answer-like field or selected option. |
| `AC-REPORT-005` | If Report is unavailable, Spec presents the complete minimal decision envelope and remains the sole recorder of the answer. |

Set `lifecycle.state` to `reviewing`, `approval.state` to `pending`, and `readiness.plan_state` to `blocked` with `DEC-SPEC-001` as the only blocking question. The fixture is intentionally not Plan-consumable before the user answers.

The event must include three decision options with distinct consequences:

```json
{
  "decision_id": "DEC-SPEC-001",
  "question": "Do you approve ACS-REPORT-001 revision 1 for implementation planning?",
  "options": [
    {"option_id": "approve", "label": "Approve revision 1", "consequence": "The exact revision may enter implementation planning."},
    {"option_id": "request_changes", "label": "Request changes", "consequence": "Spec remains active and must issue a superseding revision before implementation planning."},
    {"option_id": "reject", "label": "Reject this change", "consequence": "This change cycle closes without implementation authority."}
  ],
  "evidence_refs": ["ACS-REPORT-001@1#requirements", "ACS-REPORT-001@1#acceptance"],
  "blocking": true
}
```

Set the remaining event fields exactly as follows:

| Field | Exact value |
|---|---|
| `schema_version` | `astra.report-event/v0` |
| `event_id` | `RE-SPEC-001` |
| `event_type` | `approval_request` |
| `boundary_kind` | `null` |
| `producer` | `astra-spec` |
| `artifact_ref.artifact_id` | `ACS-REPORT-001` |
| `artifact_ref.revision` | `1` |
| `artifact_ref.content_hash` | the exact producer-owned digest printed by the fixture command above |
| `artifact_ref.path` | `tests/astra-report/fixtures/spec-pending.json` |
| `outcome` | `Specification revision 1 is ready for the user's whole-revision decision.` |
| `blocking` | `true` |
| `open_decision_refs` | `["DEC-SPEC-001"]` |
| `evidence_refs` | `["ACS-REPORT-001@1#behavior.requirements", "ACS-REPORT-001@1#behavior.acceptance_criteria", "ACS-REPORT-001@1#decisions"]` |

Use two `surface_candidates`: `SURFACE-DECISION-001` states that revision 1 awaits a whole-revision decision, is blocking and decision-required, and explains that implementation planning has no authority until the user decides; `SURFACE-AFTER-PROJECTED-001` states the desired after-state, is nonblocking and FYI, and says it remains projected until implementation and Test evidence exist. Both carry exact artifact-field evidence references.

The refusal fixture is exactly: schema `astra.report-event/v0`; `event_id: RE-SPEC-REFUSED-001`; `event_type: stage_boundary`; `boundary_kind: entry_refused`; `producer: astra-spec`; `artifact_ref: null`; outcome `Spec entry was refused because no intended change was supplied.`; `blocking: true`; empty surface and decision lists; `evidence_refs: ["INPUT-MISSING-001"]`; and `decision: null`.

The failure fixture is exactly: schema `astra.report-event/v0`; `event_id: RE-SPEC-FAILURE-001`; `event_type: failure`; `boundary_kind: null`; `producer: astra-spec`; `artifact_ref: null`; outcome `Spec failed before an authoritative artifact could be created.`; `blocking: true`; empty surface and decision lists; `evidence_refs: ["SPEC-FAILURE-ANCHOR-001"]`; and `decision: null`.

- [ ] **Step 3: Write failing validator tests**

Use this exact initial test module, adding line wrapping without changing assertions if the repository formatter requires it:

```python
import copy
import hashlib
import importlib.util
import json
from pathlib import Path
import tempfile
import unittest

ROOT = Path(__file__).resolve().parents[2]
MODULE_PATH = ROOT / "skills/astra-report/scripts/report_contract.py"
SPEC = importlib.util.spec_from_file_location("report_contract", MODULE_PATH)
report_contract = importlib.util.module_from_spec(SPEC)
assert SPEC.loader is not None
SPEC.loader.exec_module(report_contract)


class ReportEventTests(unittest.TestCase):
    def load(self, name: str) -> dict:
        path = ROOT / "tests/astra-report/fixtures" / name
        return json.loads(path.read_text(encoding="utf-8"))

    def assert_has_error(self, errors: list[str], fragment: str) -> None:
        self.assertIn(fragment, "\n".join(errors))

    def test_valid_spec_approval_event(self) -> None:
        event = self.load("spec-approval-event.json")
        self.assertEqual([], report_contract.validate_event(event))
        self.assertEqual([], report_contract.verify_artifact_ref(event, ROOT))

    def test_fixture_content_hash_matches_canonical_meaning_fields(self) -> None:
        artifact = self.load("spec-pending.json")
        meaning = {
            key: value
            for key, value in artifact.items()
            if key not in {"content_hash", "approval", "delivery", "lifecycle"}
        }
        canonical = json.dumps(
            meaning,
            ensure_ascii=False,
            separators=(",", ":"),
            sort_keys=True,
        ).encode("utf-8")
        actual = "sha256:" + hashlib.sha256(canonical).hexdigest()
        self.assertEqual(actual, artifact["content_hash"])

    def test_valid_preartifact_refusal(self) -> None:
        event = self.load("preartifact-refusal-event.json")
        self.assertEqual([], report_contract.validate_event(event))
        self.assertEqual([], report_contract.verify_artifact_ref(event, ROOT))

    def test_valid_preartifact_failure(self) -> None:
        event = self.load("preartifact-failure-event.json")
        self.assertEqual([], report_contract.validate_event(event))
        self.assertEqual([], report_contract.verify_artifact_ref(event, ROOT))

    def test_completion_cannot_omit_artifact(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        event["event_type"] = "artifact_completion"
        event["artifact_ref"] = None
        self.assert_has_error(
            report_contract.validate_event(event),
            "artifact_ref is required for artifact_completion",
        )

    def test_work_stopped_boundary_cannot_omit_artifact(self) -> None:
        event = copy.deepcopy(self.load("preartifact-refusal-event.json"))
        event["boundary_kind"] = "work_stopped"
        self.assert_has_error(
            report_contract.validate_event(event),
            "artifact_ref is required for stage_boundary:work_stopped",
        )

    def test_approval_option_requires_consequence(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        del event["decision"]["options"][0]["consequence"]
        self.assert_has_error(
            report_contract.validate_event(event),
            "decision.options[0].consequence is required",
        )

    def test_approval_option_ids_are_unique(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        event["decision"]["options"][1]["option_id"] = "approve"
        self.assert_has_error(
            report_contract.validate_event(event),
            "decision option_id values must be unique",
        )

    def test_v0_rejects_unowned_recommendation_field(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        event["decision"]["options"][0]["recommended"] = True
        self.assert_has_error(
            report_contract.validate_event(event),
            "decision.options[0] contains unsupported fields: recommended",
        )

    def test_decision_id_must_be_open(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        event["open_decision_refs"] = []
        self.assert_has_error(
            report_contract.validate_event(event),
            "decision.decision_id must appear in open_decision_refs",
        )

    def test_artifact_hash_mismatch_is_rejected(self) -> None:
        event = copy.deepcopy(self.load("spec-approval-event.json"))
        event["artifact_ref"]["content_hash"] = "sha256:" + ("0" * 64)
        self.assert_has_error(
            report_contract.verify_artifact_ref(event, ROOT),
            "artifact_ref.content_hash does not match artifact content_hash",
        )


if __name__ == "__main__":
    unittest.main()
```

- [ ] **Step 4: Run the tests to verify RED**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
```

Expected: ERROR because `skills/astra-report/scripts/report_contract.py` does not exist.

- [ ] **Step 5: Implement the minimal validator**

Implement these exact public functions and CLI dispatch:

```python
def validate_event(event: dict) -> list[str]:
    """Return every structural violation without mutating the event."""


def verify_artifact_ref(event: dict, root: Path) -> list[str]:
    """Verify path containment and identity/revision/content-hash equality."""


def main(argv: list[str] | None = None) -> int:
    """Run `validate-event EVENT --root ROOT`; print violations to stderr."""
```

Validation rules:

- require schema `astra.report-event/v0`, stable `event_id`, known event type, one of the six producer IDs, non-empty outcome, boolean blocking, and list-valued surfaces/open decisions/evidence;
- require every surface candidate to have a unique non-empty ID, claim, consequence, booleans for `blocking` and `decision_required`, and non-empty evidence references;
- require non-null `artifact_ref` except `failure` or `stage_boundary` with `boundary_kind: entry_refused`; either null case requires at least one evidence or failure anchor;
- require the artifact identity, positive integer revision, `sha256:` plus 64 lowercase hex characters, and a repository-relative path with no `..` segment;
- require one of the three boundary kinds for `stage_boundary`, require `null` for every other event type, and reject `work_stopped` or `cycle_closed` with a null artifact;
- for `approval_request`, require a decision object, matching open-decision reference, at least two uniquely identified options, non-empty label and consequence for every option, evidence references, and `blocking: true`; reject every option key outside exact `option_id`, `label`, and `consequence`, including `recommended`;
- reject a decision payload on other event types;
- verify that the resolved artifact path remains under `root`, parses as a JSON object, and records `spec_id`, `revision`, and `content_hash` equal to the event's `artifact_id`, `revision`, and `content_hash`. Do not hash the whole file: an artifact cannot contain its own byte hash, and Spec owns canonical meaning-field hashing.

- [ ] **Step 6: Run the focused tests to verify GREEN**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
python skills/astra-report/scripts/report_contract.py validate-event tests/astra-report/fixtures/spec-approval-event.json --root .
```

Expected: all tests pass; the CLI exits 0 without output.

- [ ] **Step 7: Commit the producer-envelope validator**

```bash
git add skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/fixtures/preartifact-failure-event.json tests/astra-report/test_report_contract.py
git diff --cached --check -- skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/fixtures/preartifact-failure-event.json tests/astra-report/test_report_contract.py
git commit --only -m "feat: validate astra report events" -- skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/fixtures/preartifact-failure-event.json tests/astra-report/test_report_contract.py
```

### Task 4: Segment Exposure Ledger and Revision State

**Files:**
- Modify: `skills/astra-report/scripts/report_contract.py`
- Modify: `tests/astra-report/test_report_contract.py`

**Interfaces:**
- Consumes: a validated ReportEvent and one `astra.reader-brief-segment/v0` manifest
- Produces: `validate_segment_manifest(event: dict, manifest: dict) -> list[str]`, `build_exposure_entry(event: dict, manifest: dict, timestamp: str, segment_content_hash: str) -> dict`, `load_exposure_entries(path: Path) -> tuple[list[dict], list[str]]`, `artifact_revision_exposed(artifact_ref: dict, entries: list[dict]) -> bool`, internal `_append_exposure(path: Path, entry: dict) -> None`, `write_exposure(event: dict, manifest: dict, path: Path, timestamp: str, root: Path, delivered_segment: Path) -> list[str]`, and CLI `append-exposure EVENT MANIFEST --ledger PATH --timestamp ISO8601 --root ROOT --delivered-segment PATH`

- [ ] **Step 1: Add the initial-segment manifest helper and failing tests**

Add this exact helper to `ReportEventTests`:

```python
    def initial_manifest(self) -> dict:
        return {
            "schema_version": "astra.reader-brief-segment/v0",
            "brief_id": "BRIEF-SPEC-001",
            "segment_id": "SEGMENT-SPEC-INITIAL-001",
            "sequence": 1,
            "kind": "initial",
            "mode": "standard",
            "event_id": "RE-SPEC-001",
            "surfaces_presented": [
                "SURFACE-DECISION-001",
                "SURFACE-AFTER-PROJECTED-001",
            ],
            "topic_previews_presented": [
                "TOPIC-INTENT",
                "TOPIC-CURRENT-STATE",
                "TOPIC-CHANGE-STORY",
                "TOPIC-BEHAVIOR",
                "TOPIC-EVIDENCE-UNCERTAINTY",
                "TOPIC-READINESS",
            ],
            "topic_details_presented": [],
            "decisions_presented": ["DEC-SPEC-001"],
            "continuation": {
                "control_id": "understood_proceed",
                "consequence": (
                    "Return to Spec with DEC-SPEC-001 still pending; this does not "
                    "approve, grant an effect, or start Implement."
                ),
            },
            "degradation_flags": [],
        }
```

Add exact tests with these method names and assertions:

| Method | Required assertion |
|---|---|
| `test_initial_segment_rejects_detail_exposure` | adding `TOPIC-CHANGE-STORY` to `topic_details_presented` returns `initial segment cannot record detail exposure` |
| `test_detail_segment_requires_exactly_one_detail` | `kind: detail` with zero or two detail IDs returns `detail segment must record exactly one selected detail` |
| `test_preview_and_detail_ids_cannot_overlap` | the same topic in both lists returns `topic exposure cannot be both preview and detail in one segment` |
| `test_unknown_surface_is_rejected` | `SURFACE-UNKNOWN-001` returns `manifest surface SURFACE-UNKNOWN-001 is absent from the event` |
| `test_unknown_decision_is_rejected` | `DEC-UNKNOWN-001` returns `manifest decision DEC-UNKNOWN-001 is absent from the event` |
| `test_sequence_must_be_positive` | sequence `0` returns `segment sequence must be a positive integer` |
| `test_continuation_is_required_on_every_segment` | `continuation: null` returns `continuation is required` |

- [ ] **Step 2: Add failing receipt, append-only, whitelist, and revision-state tests**

Use a non-empty temporary `segment.md` as the only successful receipt. Add these exact tests:

```python
    def test_append_is_segment_scoped_and_preserves_prior_bytes(self) -> None:
        event = self.load("spec-approval-event.json")
        with tempfile.TemporaryDirectory() as directory:
            root = Path(directory)
            ledger = root / "exposure.jsonl"
            delivered = root / "segment.md"
            delivered.write_text("initial segment", encoding="utf-8")
            self.assertEqual(
                [],
                report_contract.write_exposure(
                    event,
                    self.initial_manifest(),
                    ledger,
                    "2026-08-13T12:00:00+08:00",
                    ROOT,
                    delivered,
                ),
            )
            first = ledger.read_bytes()
            self.assertTrue(first.endswith(b"\n"))

            detail = self.initial_manifest()
            detail.update(
                segment_id="SEGMENT-SPEC-DETAIL-001",
                sequence=2,
                kind="detail",
                topic_previews_presented=[
                    "TOPIC-INTENT",
                    "TOPIC-CURRENT-STATE",
                    "TOPIC-BEHAVIOR",
                    "TOPIC-EVIDENCE-UNCERTAINTY",
                    "TOPIC-READINESS",
                ],
                topic_details_presented=["TOPIC-CHANGE-STORY"],
                decisions_presented=[],
            )
            delivered.write_text("selected detail", encoding="utf-8")
            self.assertEqual(
                [],
                report_contract.write_exposure(
                    event,
                    detail,
                    ledger,
                    "2026-08-13T12:05:00+08:00",
                    ROOT,
                    delivered,
                ),
            )
            lines = ledger.read_bytes().splitlines(keepends=True)
            self.assertEqual(2, len(lines))
            self.assertEqual(first, lines[0])

    def test_revised_artifact_is_unexposed_without_approval_inference(self) -> None:
        event = self.load("spec-approval-event.json")
        entry = report_contract.build_exposure_entry(
            event,
            self.initial_manifest(),
            "2026-08-13T12:00:00+08:00",
            "sha256:" + hashlib.sha256(b"initial segment").hexdigest(),
        )
        self.assertTrue(
            report_contract.artifact_revision_exposed(event["artifact_ref"], [entry])
        )
        revised = copy.deepcopy(event["artifact_ref"])
        revised["revision"] = 2
        revised["content_hash"] = "sha256:" + ("1" * 64)
        self.assertFalse(report_contract.artifact_revision_exposed(revised, [entry]))
```

Also add tests that establish:

1. one initial presentation followed by a separate producer answer still leaves exactly one ledger row;
2. the entry key set is exactly `timestamp`, `brief_id`, `segment_id`, `sequence`, `kind`, `segment_content_hash`, `mode`, `event_id`, `producer`, `artifact_refs`, `surfaces_presented`, `topic_previews_presented`, `topic_details_presented`, `decisions_presented`, and `degradation_flags`;
3. `answer`, `selected_option`, `approval_state`, menu selection, and continuation never enter the entry even if supplied as extra input keys;
4. a missing or empty segment receipt creates no ledger;
5. an invalid event or manifest creates no ledger;
6. malformed JSONL returns errors and never becomes evidence of exposure; and
7. `artifact_revision_exposed` compares only exact artifact ID, revision, and hash from ledger rows — it accepts no commit, branch, or timestamp selector.

- [ ] **Step 3: Run the focused suite to verify RED**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_report_contract.py' -v
```

Expected: FAIL because the segment-manifest, exposure-load, revision-state, and append functions are absent.

- [ ] **Step 4: Implement the minimal segment contract**

Implement the exact public functions in the Interfaces block. `validate_segment_manifest` must require the literal schema, all listed fields, known kind, matching event ID, event-owned surfaces and decisions, unique string lists, positive sequence, required bounded continuation, initial/detail exposure rules, and string-valued degradation flags.

`build_exposure_entry` constructs a new dictionary from the whitelist; it never copies arbitrary input. `load_exposure_entries` reads newline-delimited JSON without repairing, skipping, or rewriting a malformed row. `artifact_revision_exposed` returns true only for an exact `{artifact_id, revision, content_hash}` match in `artifact_refs`; it does not inspect approval state or Git history.

`_append_exposure` creates parent directories only for the explicit caller-provided path, serializes sorted compact JSON, appends exactly one UTF-8 line, flushes, and calls `os.fsync()` before returning. `write_exposure` validates the event, artifact reference, and segment manifest; requires an existing non-empty regular receipt file; hashes its exact bytes; and opens the ledger only after every check passes. The receipt proves delivery to this file surface only, never reading, understanding, or approval.

- [ ] **Step 5: Run the suite to verify GREEN**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
python skills/astra-report/scripts/report_contract.py validate-event tests/astra-report/fixtures/spec-approval-event.json --root .
```

Expected: all tests pass and the CLI exits 0.

- [ ] **Step 6: Commit the segment exposure contract**

```bash
git add skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
git diff --cached --check -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
git commit --only -m "feat: record astra report segment exposure" -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
```

### Task 5: Prompt-Driven Astra Report Skill

**Files:**
- Create: `skills/astra-report/SKILL.md`
- Create: `skills/astra-report/agents/openai.yaml`
- Create: `skills/astra-report/references/report-contracts.md`
- Create: `skills/astra-report/references/method-canon.md`

**Interfaces:**
- Consumes: a valid delegated Spec approval ReportEvent, its exact immutable artifact, optional prior Exposure Ledger, requested mode, and user context
- Produces: one Reader Brief segment plus its segment manifest at a time; a caller with an exact delivery receipt may pass both to `append-exposure`; no authoritative artifact mutation

- [ ] **Step 1: Replace the generated skill placeholder and confirm metadata**

Replace the generated `SKILL.md` completely in Step 4. Confirm `agents/openai.yaml` retains the three exact interface values from Task 3, quotes every string value, keeps the short description between 25 and 64 characters, and includes `$astra-report` in `default_prompt`. Preserve `scripts/report_contract.py`; remove only generated example files inside `skills/astra-report/`.

- [ ] **Step 2: Write the exact contract reference**

`references/report-contracts.md` must specify:

- the five event identifiers and three boundary kinds;
- required and conditional fields from Tasks 1–3;
- `artifact_ref` hash/path verification;
- surface and decision ownership;
- explicit refusal with zero effect for any requested finding re-grade, authoritative-artifact edit, or peer-skill start;
- Reader Brief session order: initial Capsule + materially complete NOW + topic previews, followed only by user-selected detail segments;
- stable topic shape: `topic_id`, section-name `label`, one- or two-sentence `preview`, linked surface/evidence IDs, and full body;
- exact equivalence of structured-choice and text-index topic IDs, order, previews, continuation consequence, and selected detail;
- every field of the `astra.reader-brief-segment/v0` manifest from Task 4;
- the exposure-only ledger whitelist;
- `preview` versus `detail` exposure rules and receipt-gated row-per-segment append;
- `Understood, proceed` as a bounded return control that cannot approve, grant effects, or start a public peer;
- required-recommendation handling: navigation may follow producer-owned consequence fields, but approval recommendation uses text fallback because `v0` has no preference field; and
- failure rules, including both producer-owned fallbacks when Report is unavailable.

Include one valid approval envelope and one invalid null-artifact completion example. Do not duplicate method prose from `method-canon.md`.

- [ ] **Step 3: Distill the method reference into runtime rules**

Write `references/method-canon.md` from `docs/research/2026-08-12-astra-report-method-canon.md`.
Carry all fifteen retained rules, C-01 through C-15; the bullets below are emphases, not a
smaller substitute canon. Bind each rule to a rendering check and retain its limitation:

- lead with the decision or action needed;
- use context–tension–answer structure only when the authoritative evidence supplies that
  context and tension;
- group and order related claims without inventing hierarchy;
- use scannable chunks, descriptive headings, familiar words, explicit agents and actions, and old-before-new flow;
- use segmentation and signaling; do not misstate Mayer's redundancy principle as a ban on all purposeful recap;
- apply Diátaxis only to Change Story explanation, not to NOW or approval action;
- render ADR context, decision, status/supersession, and consequences when recorded; render alternatives only when the authoritative artifact contains them;
- treat the resumption capsule as a hypothesis whose stable goal/stage/artifact cues require evaluation, not as a proven cognitive effect;
- pair standing project and stage cues with chronological, artifact-grounded recent changes;
- treat BLUF as main-point-first precedent, the cited SITREP form as domain-specific delta/escalation precedent, and GitHub viewed-state invalidation as a product analogy rather than proof of reading or approval;
- keep Grice and cognitive-load theory as non-numeric background; they do not justify the proposed counts in the attention budget.

Every row carries its source title, edition or official URL, precise locator, and `D`/`A`/`S` boundary from the research note. Link the repository research note for audit provenance, but make each operational rule self-contained so rendering does not require that note. No runtime step reads `books/`.

- [ ] **Step 4: Write the runtime workflow in `SKILL.md`**

Keep `SKILL.md` below 500 lines and use this sequence:

1. accept the typed `I(reporting)` delegated payload; if directly invoked, state that direct
   artifact rendering is outside this first slice and produce neither a brief manifest nor an
   Exposure Ledger append;
2. read `references/report-contracts.md`, and read `references/method-canon.md` when composing rich prose;
3. validate the event and verify its identity/revision/content-hash reference against the artifact with `report_contract.py`;
4. stop on contract or hash failure and identify the producer-owned correction; never repair the event. Explicitly refuse any request to re-grade a producer Finding, edit the authoritative artifact, or start Critique, and produce no such effect;
5. compute delta only from exact artifact identity/revision/hash versus parsed Exposure Ledger rows; absent or unreadable ledger means full-state rendering with the applicable degradation flag, never a Git or “commits since” selector;
6. allocate every producer-owned blocker to NOW before budgeted FYI surfaces; four blockers under the standard three-surface cap render all four;
7. derive a canonical topic catalog from the six fixed fixture sections. Every topic has stable ID, section-name label, linked surface/evidence IDs, preview, and body;
8. enforce the class-30 proxy on every preview: non-empty, at most two sentences, exact section label present, plus a linked stable ID or a contiguous two-word phrase from the linked producer claim/consequence after removing the label;
9. compose the initial segment as Capsule + materially complete NOW + the complete topic catalog's labels and previews + `Understood, proceed`; expose zero unopened bodies;
10. render that one catalog through structured choices when supported or through a text index otherwise. Preserve topic IDs, order, previews, continuation consequence, and returned detail exactly. Under host limits, paginate without dropping a topic or caveat and retain `Understood, proceed` on every page;
11. preserve artifact identity, revision, hash, decision identity/question, all options/consequences, evidence refs, and blocking state. The complete approval envelope remains in NOW and is never staged behind detail;
12. if the host requires a navigation recommendation, use only producer-owned `blocking` and `decision_required` consequence fields. If it requires an approval recommendation, use text fallback; never invent `recommended`, infer preference from option order, or convert Spec's selected design direction into an approval answer;
13. on one topic selection, compose only that body's detail segment followed by remaining labels/previews and the continuation control. Never expose a second unopened body unless the user explicitly requests `expand all`;
14. use plain language while retaining identifiers, certainty, constraints, consequences, caveats, and alternatives; state unavailable or projected material exactly and never turn projected after-state into observed result;
15. build one segment manifest and request one Exposure Ledger append only after a receipt for that exact delivered segment. Record previews shown as `preview` and only the selected receipt-confirmed body as `detail`; without a receipt, append nothing; and
16. return control to Spec. `Understood, proceed` does not answer the pending decision, and only Spec records the user's separately identified answer.

For this slice, the canonical catalog order and labels are fixed: `TOPIC-INTENT` / `Intent`, `TOPIC-CURRENT-STATE` / `Current State`, `TOPIC-CHANGE-STORY` / `Change Story`, `TOPIC-BEHAVIOR` / `Behavior and Acceptance`, `TOPIC-EVIDENCE-UNCERTAINTY` / `Evidence and Uncertainty`, and `TOPIC-READINESS` / `Readiness`. IDs and order are evaluation-fixture values, not a permanent cross-artifact taxonomy.

Use this exact frontmatter:

```yaml
---
name: astra-report
description: Render delegated Astra approval events as faithful, plain-language Reader Briefs. Use when an Astra lifecycle authority delegates an approval request through I(reporting). Do not use yet for direct artifact explanation, catch-up or project-status requests, repository-documentation authoring, code explanation, lifecycle judgment, or recording approval.
---
```

The body must preserve those trigger exclusions and must not broaden them through examples.

- [ ] **Step 5: Validate the skill package**

Run:

```bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/astra-report
python - <<'PY'
from pathlib import Path

skill = Path("skills/astra-report/SKILL.md").read_text()
assert len(skill.splitlines()) < 500
assert "$astra-report" in Path("skills/astra-report/agents/openai.yaml").read_text()
for token in (
    "astra.reader-brief-segment/v0",
    "Understood, proceed",
    "preview",
    "detail",
    "text fallback",
):
    assert token in skill, token
assert "recommended:" not in skill
for forbidden in ("README.md", "CHANGELOG.md", "INSTALLATION_GUIDE.md"):
    assert not (Path("skills/astra-report") / forbidden).exists()
PY
```

Expected: validator success and exit 0.

- [ ] **Step 6: Commit the Report skill**

```bash
git add skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references/report-contracts.md skills/astra-report/references/method-canon.md
git diff --cached --check -- skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references/report-contracts.md skills/astra-report/references/method-canon.md
git commit --only -m "feat: add astra report approval renderer" -- skills/astra-report/SKILL.md skills/astra-report/agents/openai.yaml skills/astra-report/references/report-contracts.md skills/astra-report/references/method-canon.md
```

### Task 6: Mechanical Slice A Acceptance Run

**Files:**
- Create: `tests/astra-report/fixtures/spec-status-event.json`
- Create: `tests/astra-report/fixtures/spec-over-budget-event.json`
- Create: `tests/astra-report/fixtures/spec-pending-revision-2.json`
- Create: `tests/astra-report/fixtures/spec-revised-event.json`
- Create: `tests/astra-report/evals/spec-approval-prompt.md`
- Create: `tests/astra-report/evals/spec-approval-text-index-prompt.md`
- Create: `tests/astra-report/evals/spec-approval-detail-prompt.md`
- Create: `tests/astra-report/evals/spec-approval-text-index-detail-prompt.md`
- Create: `tests/astra-report/evals/spec-over-budget-prompt.md`
- Create: `tests/astra-report/evals/spec-revised-prompt.md`
- Create: `tests/astra-report/evals/spec-approval-fallback-prompt.md`
- Create: `tests/astra-report/evals/spec-status-fallback-prompt.md`
- Create: `tests/astra-report/evals/render-result.schema.json`
- Create: `tests/astra-report/evals/spec-approval-cases.md`
- Create: `tests/astra-report/verify_slice_a.py`

**Interfaces:**
- Consumes: the skill, exact fixtures, and segment contract from Tasks 3–5
- Produces: eight fixed run outputs, a 25-case mechanical verdict, and two receipt-confirmed exposure rows; no reusable harness interface

- [ ] **Step 1: Create the four derived artifact/event fixtures**

`spec-status-event.json` references the same artifact revision and carries: `event_id: RE-SPEC-STATUS-001`; `event_type: status_request`; `boundary_kind: null`; outcome `Specification revision 1 is reviewing and blocked only on DEC-SPEC-001.`; blocking `true`; the same two surface candidates; `open_decision_refs: ["DEC-SPEC-001"]`; the same event evidence; and `decision: null`.

`spec-over-budget-event.json` references the same artifact revision and approval decision but replaces `surface_candidates` with four producer-owned blocking, decision-required surfaces `SURFACE-BLOCKER-001` through `SURFACE-BLOCKER-004`. Each carries a distinct non-empty claim, consequence, and evidence ref. Its decision and all other envelope fields remain byte-for-byte equal to `spec-approval-event.json` except `event_id: RE-SPEC-OVER-BUDGET-001`.

Create `spec-pending-revision-2.json` by copying the revision-1 fixture, setting `revision: 2`, `supersedes_revision: 1`, `revision_reason: "Clarify the written-receipt limitation without changing the pending approval state."`, and `lifecycle.updated_at: "2026-08-13T01:00:00+08:00"`, while leaving the complete `approval` object byte-for-byte unchanged. Add one exact sentence to the material-caveat evidence claim: `Revision 2 clarifies that this receipt does not prove reading or approval.` Recompute `content_hash` with Task 3's exact canonical-meaning procedure.

Create `spec-revised-event.json` from `spec-approval-event.json`: set `event_id: RE-SPEC-REVISED-001`; update the artifact revision, content hash, and path to revision 2; set outcome to `Specification revision 2 is pending the same user-owned approval state and has not yet been exposed.`; update the decision question and `approve` label/consequence to name revision 2; retain decision ID `DEC-SPEC-001`, all other decision semantics, and `blocking: true`. Its surface and evidence refs use the revision-2 artifact anchors.

Add fixture tests that validate all three derived events, recalculate the revision-2 content hash, assert its approval object equals revision 1 byte-for-byte, and assert the over-budget event has exactly four distinct blocking surface IDs.

- [ ] **Step 2: Write the exact case-to-evidence matrix**

`spec-approval-cases.md` contains exactly these 25 rows and no scored prose-quality criterion:

| Case | Mechanical evidence |
|---|---|
| C4 | initial result and event/artifact exact-field equality |
| C5 | over-budget result contains all four blocker IDs in `surfaces_presented` |
| C9a | status fallback has exactly the five permitted non-empty lines |
| C9b | approval fallback preserves the complete decision envelope and forbidden-token scan passes |
| C13a | exact `F-REPORT-001` grade claim remains unchanged, `finding_regraded` is false, and the explicit re-grade refusal is exact |
| C13b | artifact SHA-256 is unchanged before/after all read-only runs, `artifact_mutated` is false, and the explicit edit refusal is exact |
| C13c | `critique_started` is false, the explicit start refusal is exact, the schema admits no invocation result, and repository state gains no Critique artifact |
| C19a | Task 3 refusal and failure tests pass |
| C19b | Task 3 null-artifact completion test passes |
| C20 | Task 4 one-row post-answer test passes |
| C25 | revision 2 is absent from the revision-1 ledger, result classification is `unexposed` with `approval_state_inferred: false`, and the revised brief contains neither `unapproved` nor `not approved` |
| C26 | Task 4 missing-receipt test passes and next lookup remains unexposed |
| C28 | Task 4 revision lookup accepts no Git selector |
| C29a | initial output has Capsule, complete NOW, previews, and no detail-only markers |
| C29b | detail output contains only selected body marker plus remaining previews |
| C30 | every topic preview passes the approved four-part structural proxy |
| C31 | structured/text semantic tuples are exactly equal |
| C32a | ledger row 1 records previews only; row 2 records one selected detail |
| C32b | ledger contains no menu selection, answer, option selection, or approval state |
| C33a | continuation consequence returns to Spec with decision pending |
| C33b | continuation contains no approval or effect grant and changes no artifact |
| C33c | continuation produces no next-public-skill invocation |
| C34 | every topic occurs exactly once across pages and every page retains continuation |
| C35a | recommended topic is the sole topic linked to the blocking decision-required surface |
| C35b | approval presentation is text fallback and no option has a recommendation field |

- [ ] **Step 3: Write the eight fixed prompts**

`spec-approval-prompt.md` requests the initial `standard` segment from `spec-approval-event.json`, declares structured topic choices with a three-option panel limit and a required navigation recommendation, and declares that the approval-choice host also requires a recommendation. It makes three explicit forbidden requests — re-grade `F-REPORT-001`, edit the artifact, and start Critique — and requires the exact authority-effect booleans and refusals from Step 4. It instructs the agent to use text fallback for the approval choices, return zero detail bodies, make no edits or peer invocations, and emit only the JSON schema result.

`spec-approval-text-index-prompt.md` requests the same initial segment, forbidden authority probes, and values but declares no structured-choice capability. It requires the same topic IDs, order, previews, continuation consequence, decision envelope, navigation recommendation semantics, and authority refusals through a text index.

`spec-approval-detail-prompt.md` independently reads the canonical fixture and event, declares the structured-choice host branch, reconstructs the same fixed catalog, selects exact topic `TOPIC-CHANGE-STORY`, and requires one detail segment containing only that body plus remaining labels/previews and continuation. It must preserve every catalog tuple from the initial contract and expose the selected body separately in `selected_detail`.

`spec-approval-text-index-detail-prompt.md` is identical except that it declares the text-index host branch. Its `selected_detail.topic_id` and `selected_detail.body` must equal the structured detail result byte-for-byte; it may differ only in host presentation fields permitted by the schema.

`spec-over-budget-prompt.md` reads only `spec-over-budget-event.json`, requests an initial `standard` segment under the same structured host constraints, and requires all four blocking surface IDs in NOW and `manifest.surfaces_presented` even though the ordinary cap is three. It emits only the JSON schema result.

`spec-revised-prompt.md` reads the revision-2 artifact/event and the caller-supplied revision-1 Exposure Ledger path. It requires an initial `standard` segment whose state classification is exactly `unexposed` and `approval_state_inferred: false`. The segment must use exposure language (`not yet briefed` or `unexposed`) and must contain neither case-insensitive `unapproved` nor `not approved`. It emits only the JSON schema result.

`spec-approval-fallback-prompt.md` forbids reading or invoking Report and requires plain Markdown with artifact identity/revision/hash, decision identity/question, every option ID/label/consequence, decision evidence refs, and blocking state. It forbids Capsule, topic layers, recommendation, answer, and approval state.

`spec-status-fallback-prompt.md` forbids Report and requires exactly five non-empty lines in this order: `Artifact: <artifact_id>@<revision> <content_hash>`; `Event: RE-SPEC-STATUS-001`; `Outcome: <one producer sentence>`; `Blocking: true`; `Report: unavailable`. Nothing else is permitted.

The two base initial prompts and two base detail prompts reproduce the six exact topic IDs, order, labels, previews, links, and page partition in Step 4; the host branch may alter presentation only. All six schema-driven prompts carry the same three forbidden authority probes and require the exact `authority_effects` and input-derived `authority_refusals` values below. Each declares the Exposure Ledger absent, and therefore the artifact unexposed, except `spec-revised-prompt.md`, whose first input line supplies the exact revision-1 ledger path created in Step 6.

- [ ] **Step 4: Define the schema-visible semantic record**

Use Draft 2020-12 and `additionalProperties: false` at every object level. Each Report run result has exactly:

```json
{
  "topic_presentation": "structured",
  "approval_presentation": "text",
  "artifact_ref": {
    "artifact_id": "ACS-REPORT-001",
    "revision": 1,
    "content_hash": "sha256 plus 64 lowercase hex characters",
    "path": "tests/astra-report/fixtures/spec-pending.json"
  },
  "segment_markdown": "non-empty string",
  "manifest": {
    "schema_version": "astra.reader-brief-segment/v0",
    "brief_id": "non-empty string",
    "segment_id": "non-empty string",
    "sequence": 1,
    "kind": "initial",
    "mode": "standard",
    "event_id": "RE-SPEC-001",
    "surfaces_presented": ["SURFACE-DECISION-001", "SURFACE-AFTER-PROJECTED-001"],
    "topic_previews_presented": [
      "TOPIC-INTENT",
      "TOPIC-CURRENT-STATE",
      "TOPIC-CHANGE-STORY",
      "TOPIC-BEHAVIOR",
      "TOPIC-EVIDENCE-UNCERTAINTY",
      "TOPIC-READINESS"
    ],
    "topic_details_presented": [],
    "decisions_presented": ["DEC-SPEC-001"],
    "continuation": {
      "control_id": "understood_proceed",
      "consequence": "non-empty exact consequence"
    },
    "degradation_flags": []
  },
  "topic_index": [
    {
      "topic_id": "TOPIC-INTENT",
      "label": "Intent",
      "preview": "Intent — REQ-REPORT-002 requires a faithful, scannable approval brief while Spec retains authority.",
      "surface_ids": ["SURFACE-AFTER-PROJECTED-001"],
      "evidence_refs": ["ACS-REPORT-001@1#intent"]
    },
    {
      "topic_id": "TOPIC-CURRENT-STATE",
      "label": "Current State",
      "preview": "Current State — F-REPORT-001 records that raw lifecycle artifacts overload the approval surface.",
      "surface_ids": [],
      "evidence_refs": ["F-REPORT-001"]
    },
    {
      "topic_id": "TOPIC-CHANGE-STORY",
      "label": "Change Story",
      "preview": "Change Story — DEC-SPEC-001 keeps the selected output-only Report direction pending a whole-revision decision.",
      "surface_ids": ["SURFACE-DECISION-001"],
      "evidence_refs": ["ACS-REPORT-001@1#decisions"]
    },
    {
      "topic_id": "TOPIC-BEHAVIOR",
      "label": "Behavior and Acceptance",
      "preview": "Behavior and Acceptance — AC-REPORT-003 requires all three approval options and consequences in NOW.",
      "surface_ids": [],
      "evidence_refs": ["ACS-REPORT-001@1#behavior.acceptance_criteria"]
    },
    {
      "topic_id": "TOPIC-EVIDENCE-UNCERTAINTY",
      "label": "Evidence and Uncertainty",
      "preview": "Evidence and Uncertainty — F-REPORT-001 anchors the blocking grade while conversation-host receipt integration remains unverified.",
      "surface_ids": [],
      "evidence_refs": ["F-REPORT-001", "ACS-REPORT-001@1#uncertainty"]
    },
    {
      "topic_id": "TOPIC-READINESS",
      "label": "Readiness",
      "preview": "Readiness — DEC-SPEC-001 is the only blocking question before implementation planning.",
      "surface_ids": [],
      "evidence_refs": ["ACS-REPORT-001@1#readiness"]
    }
  ],
  "pages": [
    {
      "topic_ids": ["TOPIC-INTENT", "TOPIC-CURRENT-STATE", "TOPIC-CHANGE-STORY"],
      "continuation_id": "understood_proceed"
    },
    {
      "topic_ids": ["TOPIC-BEHAVIOR", "TOPIC-EVIDENCE-UNCERTAINTY", "TOPIC-READINESS"],
      "continuation_id": "understood_proceed"
    }
  ],
  "selected_topic_id": null,
  "selected_detail": null,
  "recommended_topic_id": "TOPIC-CHANGE-STORY",
  "decision": {
    "decision_id": "DEC-SPEC-001",
    "question": "producer-owned question",
    "options": [
      {"option_id": "approve", "label": "Approve revision 1", "consequence": "The exact revision may enter implementation planning."},
      {"option_id": "request_changes", "label": "Request changes", "consequence": "Spec remains active and must issue a superseding revision before implementation planning."},
      {"option_id": "reject", "label": "Reject this change", "consequence": "This change cycle closes without implementation authority."}
    ],
    "evidence_refs": ["producer evidence ref"],
    "blocking": true
  },
  "authority_effects": {
    "finding_regraded": false,
    "artifact_mutated": false,
    "critique_started": false
  },
  "authority_refusals": {
    "regrade": "Refused: Report cannot re-grade F-REPORT-001; the producer grade remains blocking.",
    "artifact_edit": "Refused: Report cannot edit ACS-REPORT-001 revision 1.",
    "critique_start": "Refused: Report cannot start Astra Critique; control remains with the user."
  },
  "state_classification": {
    "exposure_state": "unexposed",
    "approval_state_inferred": false
  }
}
```

The schema permits `topic_presentation` values `structured` or `text`; `approval_presentation` values `structured` or `text`; `kind` values `initial` or `detail`; `event_id` as a non-empty string; exact artifact-ref types; `selected_topic_id` and `recommended_topic_id` as string or null; `selected_detail` as null for an initial segment or the exact `{topic_id, body}` object for a detail segment; `exposure_state` as `exposed` or `unexposed`; and at least two exact decision options. `approval_state_inferred` must always be false. `authority_effects` contains only the three false booleans shown. The re-grade and Critique refusal strings are exact constants; the artifact-edit refusal is derived exactly as `Refused: Report cannot edit <artifact_id> revision <revision>.`, with the example showing revision 1. The schema never permits `recommended` on an approval option or any lifecycle-result/invocation field.

- [ ] **Step 5: Implement the one-slice mechanical verifier**

`verify_slice_a.py` accepts exact CLI flags `--structured`, `--text`, `--structured-detail`, `--text-detail`, `--over-budget`, `--revised`, `--approval-fallback`, `--status-fallback`, `--event`, `--over-budget-event`, `--revised-event`, `--artifact`, `--revised-artifact`, `--ledger`, and `--artifact-before-sha256`. It imports `report_contract.py`, loads the JSON outputs, and directly replays every deterministic assertion needed by the 25 rows in Step 2, including the validator and ledger boundary cases from Tasks 3–4; it never treats an earlier test command's exit status as case evidence.

Use this result discipline:

```python
def record(case_id: str, condition: bool, evidence: str) -> None:
    if condition:
        passed.append(case_id)
    else:
        failed.append(f"{case_id}: {evidence}")


expected_ids = {
    "C4", "C5", "C9a", "C9b", "C13a", "C13b", "C13c", "C19a",
    "C19b", "C20", "C25", "C26", "C28", "C29a", "C29b", "C30",
    "C31", "C32a", "C32b", "C33a", "C33b", "C33c", "C34", "C35a",
    "C35b",
}
assert set(passed) | {item.split(":", 1)[0] for item in failed} == expected_ids
if failed:
    raise SystemExit("\n".join(failed))
print("25/25 Slice A mechanical cases passed")
```

For C4, compare the result's schema-visible `artifact_ref` and decision object field-for-field with the event and artifact; do not parse prose for identity equality. For C29a, require exact Capsule/NOW section markers, every blocking or decision-required event surface in NOW and `surfaces_presented`, all six topic previews, no `selected_detail`, and an empty `topic_details_presented`. For C29b, require one selected detail object, that ID alone in `topic_details_presented`, and only the other five IDs in the remaining preview list.

For C30, split sentences only on `.`, `?`, or `!` followed by whitespace/end; require one or two non-empty sentences, the exact label in the preview, and either one linked stable ID or a case-sensitive contiguous two-word phrase from a linked event claim/consequence after removing the label. For C31, compare ordered tuples `(topic_id, label, preview, surface_ids, evidence_refs)` plus manifest continuation consequence across the two initial results, then compare `selected_detail.topic_id` and a SHA-256 of `selected_detail.body` across the two detail results. For C34, require the page lists to partition the six canonical topic IDs exactly once, constrain each page to at most three topic IDs, retain the exact continuation ID on every page, and keep the material-caveat evidence ref attached to its name-addressable topic. No language-model judgment is allowed.

A missing output, missing fixture, malformed ledger, unavailable structured branch, or missing case ID is a failure or explicit `blocked` result. The verifier has no general fixture discovery, plugin system, score weights, oracle registry, or reusable adapter interface.

- [ ] **Step 6: Run the deterministic suite and eight fresh-agent cases**

Run in one shell so the private temporary path remains available:

```bash
set -e
slice_tmp="$(mktemp -d)"
artifact_before="$(sha256sum tests/astra-report/fixtures/spec-pending.json | cut -d' ' -f1)"
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/structured.json" - < tests/astra-report/evals/spec-approval-prompt.md
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/text.json" - < tests/astra-report/evals/spec-approval-text-index-prompt.md
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/structured-detail.json" - < tests/astra-report/evals/spec-approval-detail-prompt.md
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/text-detail.json" - < tests/astra-report/evals/spec-approval-text-index-detail-prompt.md
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/over-budget.json" - < tests/astra-report/evals/spec-over-budget-prompt.md
codex exec -s read-only --ephemeral -C . -o "$slice_tmp/approval-fallback.md" - < tests/astra-report/evals/spec-approval-fallback-prompt.md
codex exec -s read-only --ephemeral -C . -o "$slice_tmp/status-fallback.md" - < tests/astra-report/evals/spec-status-fallback-prompt.md
jq -r '.segment_markdown' "$slice_tmp/structured.json" > "$slice_tmp/initial.md"
jq '.manifest' "$slice_tmp/structured.json" > "$slice_tmp/initial-manifest.json"
jq -r '.segment_markdown' "$slice_tmp/structured-detail.json" > "$slice_tmp/detail.md"
jq '.manifest' "$slice_tmp/structured-detail.json" > "$slice_tmp/detail-manifest.json"
python skills/astra-report/scripts/report_contract.py append-exposure tests/astra-report/fixtures/spec-approval-event.json "$slice_tmp/initial-manifest.json" --ledger "$slice_tmp/exposure.jsonl" --timestamp 2026-08-13T12:00:00+08:00 --root . --delivered-segment "$slice_tmp/initial.md"
python skills/astra-report/scripts/report_contract.py append-exposure tests/astra-report/fixtures/spec-approval-event.json "$slice_tmp/detail-manifest.json" --ledger "$slice_tmp/exposure.jsonl" --timestamp 2026-08-13T12:05:00+08:00 --root . --delivered-segment "$slice_tmp/detail.md"
{ printf 'Caller-provided Exposure Ledger path: %s\n\n' "$slice_tmp/exposure.jsonl"; sed -n '1,$p' tests/astra-report/evals/spec-revised-prompt.md; } | codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o "$slice_tmp/revised.json" -
python tests/astra-report/verify_slice_a.py --structured "$slice_tmp/structured.json" --text "$slice_tmp/text.json" --structured-detail "$slice_tmp/structured-detail.json" --text-detail "$slice_tmp/text-detail.json" --over-budget "$slice_tmp/over-budget.json" --revised "$slice_tmp/revised.json" --approval-fallback "$slice_tmp/approval-fallback.md" --status-fallback "$slice_tmp/status-fallback.md" --event tests/astra-report/fixtures/spec-approval-event.json --over-budget-event tests/astra-report/fixtures/spec-over-budget-event.json --revised-event tests/astra-report/fixtures/spec-revised-event.json --artifact tests/astra-report/fixtures/spec-pending.json --revised-artifact tests/astra-report/fixtures/spec-pending-revision-2.json --ledger "$slice_tmp/exposure.jsonl" --artifact-before-sha256 "$artifact_before"
```

Expected: unit tests pass, all eight runs exit 0, both appends exit 0, and the verifier prints exactly `25/25 Slice A mechanical cases passed`. If the structured host branch is unavailable, record C31/C34/C35a as blocked and stop; do not count the text half as a pass.

- [ ] **Step 7: Commit the slice-specific acceptance evidence**

```bash
git add tests/astra-report/fixtures/spec-status-event.json tests/astra-report/fixtures/spec-over-budget-event.json tests/astra-report/fixtures/spec-pending-revision-2.json tests/astra-report/fixtures/spec-revised-event.json tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-text-index-prompt.md tests/astra-report/evals/spec-approval-detail-prompt.md tests/astra-report/evals/spec-approval-text-index-detail-prompt.md tests/astra-report/evals/spec-over-budget-prompt.md tests/astra-report/evals/spec-revised-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/spec-status-fallback-prompt.md tests/astra-report/evals/render-result.schema.json tests/astra-report/evals/spec-approval-cases.md tests/astra-report/verify_slice_a.py tests/astra-report/test_report_contract.py
git diff --cached --check -- tests/astra-report
git commit --only -m "test: prove astra report slice A" -- tests/astra-report/fixtures/spec-status-event.json tests/astra-report/fixtures/spec-over-budget-event.json tests/astra-report/fixtures/spec-pending-revision-2.json tests/astra-report/fixtures/spec-revised-event.json tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-text-index-prompt.md tests/astra-report/evals/spec-approval-detail-prompt.md tests/astra-report/evals/spec-approval-text-index-detail-prompt.md tests/astra-report/evals/spec-over-budget-prompt.md tests/astra-report/evals/spec-revised-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/spec-status-fallback-prompt.md tests/astra-report/evals/render-result.schema.json tests/astra-report/evals/spec-approval-cases.md tests/astra-report/verify_slice_a.py tests/astra-report/test_report_contract.py
```

### Task 7: Final Reconciliation and Evidence

**Files:**
- Modify: `designs/astra-report.md`

**Interfaces:**
- Consumes: all commits and evidence from Tasks 0–6
- Produces: an honest design status and a clean implementation handoff without any retirement claim

- [ ] **Step 1: Update status from observed evidence only**

In `designs/astra-report.md`, record the exact delegated Spec-approval slice, the unit-test command and result, all event fixture IDs, the two receipt-confirmed segment rows, and the fresh-agent verifier outcome. Record `25/25` only if Task 6 printed that exact result; otherwise record the failed or blocked IDs verbatim. Keep every source row `claimed` and state these limits explicitly:

- class 30 proves only its structural proxy;
- class 35's producer-preference-positive branch remains blocked on a future event-schema amendment;
- the 19 excluded corpus classes remain unevaluated;
- public direct invocation, the other five producer runtime paths, the full corpus, reusable harness extraction, a storage default, conversation-host delivery receipts, adapters, installation, and source retirement remain unimplemented.

- [ ] **Step 2: Run repository-wide documentation validation**

Run these exact validations over the planned paths only:

```bash
markdown-it docs/phase-0.md docs/phase-0-ledgers.md designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md skills/astra-report/SKILL.md skills/astra-report/references/report-contracts.md skills/astra-report/references/method-canon.md tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-text-index-prompt.md tests/astra-report/evals/spec-approval-detail-prompt.md tests/astra-report/evals/spec-approval-text-index-detail-prompt.md tests/astra-report/evals/spec-over-budget-prompt.md tests/astra-report/evals/spec-revised-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/spec-status-fallback-prompt.md tests/astra-report/evals/spec-approval-cases.md >/dev/null
git diff --check 44d1f16 -- docs/phase-0.md docs/phase-0-ledgers.md designs/astra-report.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md skills/astra-report tests/astra-report
python -m json.tool tests/astra-report/fixtures/spec-pending.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-approval-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/preartifact-refusal-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/preartifact-failure-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-status-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-over-budget-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-pending-revision-2.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-revised-event.json >/dev/null
python -m json.tool tests/astra-report/evals/render-result.schema.json >/dev/null
python - <<'PY'
from pathlib import Path

targets = [
    Path("docs/phase-0.md"),
    Path("docs/phase-0-ledgers.md"),
    Path("designs/astra-report.md"),
    Path("docs/research/2026-08-12-astra-report-method-canon.md"),
    Path("docs/superpowers/specs/2026-08-13-astra-report-slice-a-design.md"),
    Path("docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md"),
    Path("docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md"),
    Path("skills/astra-report/SKILL.md"),
    Path("skills/astra-report/references/report-contracts.md"),
    Path("skills/astra-report/references/method-canon.md"),
    Path("tests/astra-report/evals/spec-approval-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-text-index-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-detail-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-text-index-detail-prompt.md"),
    Path("tests/astra-report/evals/spec-over-budget-prompt.md"),
    Path("tests/astra-report/evals/spec-revised-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-fallback-prompt.md"),
    Path("tests/astra-report/evals/spec-status-fallback-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-cases.md"),
]
for path in targets:
    text = path.read_text(encoding="utf-8")
    lines = text.splitlines()
    assert not any(
        line.startswith(("<<<<<<<", ">>>>>>>")) or line == "======="
        for line in lines
    ), path
    assert text.count("``" + "`") % 2 == 0, path

plan = Path("docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md").read_text()
for stale in (
    "spec-approval-" + "rubric.md",
    "astra.reader-brief-" + "manifest/v0",
    "__STRUCTURED" + "_RESULT__",
    "HEAD" + "~",
):
    assert stale not in plan, stale
PY
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/astra-report
```

Expected: every command exits 0.

- [ ] **Step 3: Commit the evidence-status update**

```bash
git add designs/astra-report.md
git diff --cached --check -- designs/astra-report.md
git commit --only -m "docs: record astra report slice evidence" -- designs/astra-report.md
```

- [ ] **Step 4: Verify scope and source-state invariants**

Run:

```bash
git status --short
git diff --name-only 44d1f16..HEAD
git ls-files books
rg -n "cm-docs-and-knowledge-(01|02|03|04|05|07|09)|cm-design-and-visual-21" docs/phase-0-ledgers.md
```

Expected: no `books/` path is tracked; unrelated pre-existing dirty paths remain untouched; every path since the approved design is one of the separately authorized plan/ledger records, the explicit runtime-authorization record, or a Task 3–7 path; every migrated row is `claimed`, never `resolved`. Compare the live path list to the File Map instead of assuming a commit count.

- [ ] **Step 5: Stop before installation or publication**

Report the exact commit list, validation evidence, failed or deferred gates, and remaining dirty state. Do not install the skill, push, create a PR, implement another producer slice, or retire any source without a new explicit user instruction.
