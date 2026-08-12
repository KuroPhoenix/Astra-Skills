# Astra Report Spec-Approval Vertical Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build one non-retiring vertical slice in which a Spec-owned pending revision and approval `ReportEvent` become a faithful, plain-language Reader Brief, a receipt-confirmed delivery is appended to Report's Exposure Ledger, and the user's answer remains solely in Spec's approval record.

**Architecture:** Reconcile the seventh reporting surface into the coordinator-owned policy before creating runtime files. Implement Report as a prompt-driven skill backed by one small Python standard-library contract tool: the tool validates producer envelopes and appends a whitelisted exposure record, while the skill performs trace-preserving explanation from immutable artifacts. Exercise the Report path, the Report-unavailable producer fallback, and the answer-ownership boundary with fixed Spec fixtures; this slice does not implement the full Spec skill, a general lifecycle runtime, or a full 92-source corpus.

**Tech Stack:** Markdown, YAML, JSON, Python 3 standard library, `unittest`, Codex skill metadata, `markdown-it` validation.

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
- Treat the six-skill 15-pair consultant and final trigger-surface reconciliation as a hard external gate. The live roadmap still records it as remaining work; Tasks 1–7 may start only after a canonical committed record closes it. Task 0 may land independently.
- Runtime work also requires a new explicit choice to execute this plan. That choice authorizes only this slice and must be recorded in `docs/phase-0.md`; it does not waive any retirement or installation gate.
- This slice implements the delegated Spec approval path only. It does not implement the design's public direct-request path, and its skill metadata must not advertise direct artifact, catch-up, or project-status triggers before that path has its own behavioral case.
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
| `designs/astra-{critique,understand-code,spec,implement,test,ship}.md` | Producer-side reporting hooks and degraded fallback contracts |
| `designs/astra-report.md` | Approved Report design and implementation-evidence status |
| `docs/research/2026-08-12-astra-report-method-canon.md` | Reproducible local-book and primary-source distillation |
| `skills/astra-report/SKILL.md` | Runtime workflow and fidelity rules |
| `skills/astra-report/agents/openai.yaml` | User-facing skill metadata |
| `skills/astra-report/references/report-contracts.md` | Exact ReportEvent, Reader Brief manifest, and Exposure Ledger field contracts |
| `skills/astra-report/references/method-canon.md` | Compact operational rules traced to the research note |
| `skills/astra-report/scripts/report_contract.py` | Deterministic event validation, artifact-reference consistency checks, and append-only exposure writing |
| `tests/astra-report/fixtures/spec-pending.json` | Immutable Spec-owned pending revision for the slice |
| `tests/astra-report/fixtures/spec-approval-event.json` | Valid approval request referencing the Spec fixture |
| `tests/astra-report/fixtures/preartifact-refusal-event.json` | Valid null-artifact boundary case |
| `tests/astra-report/test_report_contract.py` | Contract and ledger unit tests |
| `tests/astra-report/evals/spec-approval-prompt.md` | Fixed dogfood invocation |
| `tests/astra-report/evals/spec-approval-fallback-prompt.md` | Fixed producer fallback case when Report is unavailable |
| `tests/astra-report/evals/render-result.schema.json` | Structured-output boundary for one slice run |
| `tests/astra-report/evals/spec-approval-rubric.md` | Slice-specific behavioral acceptance rubric |

### Task 0: Freeze the Approved Planning Baseline

**Files:**
- Modify: `designs/astra-report.md`
- Create: `docs/research/2026-08-12-astra-report-method-canon.md`
- Create: `docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md`

**Interfaces:**
- Consumes: the user's 2026-08-12 source-slice approval, the corrected local-book audit, and the two closed contract seams
- Produces: the immutable design and plan baseline used by Tasks 1–7

- [ ] **Step 1: Snapshot the pre-existing staged state**

Run:

```bash
git status --short --branch
git diff --cached --name-only
```

Expected in the current workspace: `Internship Diary.md` is already staged, `designs/astra-plan.md` has an unrelated unstaged clarification, and `.gstack/`, `.idea/`, `books/`, and `pitch/` remain outside this task. If the live list differs, record the live list and preserve it; do not clean, stash, or restage it.

- [ ] **Step 2: Validate the planning artifacts**

Run:

```bash
markdown-it designs/astra-report.md >/dev/null
markdown-it docs/research/2026-08-12-astra-report-method-canon.md >/dev/null
markdown-it docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md >/dev/null
git diff --check -- designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md
python - <<'PY'
from pathlib import Path

for name in (
    "designs/astra-report.md",
    "docs/research/2026-08-12-astra-report-method-canon.md",
    "docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md",
):
    text = Path(name).read_text(encoding="utf-8")
    assert text.count("```") % 2 == 0, name
    lines = text.splitlines()
    assert not any(
        line.startswith(("<<<<<<<", ">>>>>>>")) or line == "======="
        for line in lines
    ), name
design = Path("designs/astra-report.md").read_text(encoding="utf-8")
assert "approved source-slice statement" in design
assert "claimed`, never `resolved`" in design
assert "hidden model recall is not a reproducible dependency" in design
PY
```

Expected: all commands exit 0.

- [ ] **Step 3: Commit only the planning baseline**

```bash
git add designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md
git diff --cached --check -- designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md
git commit --only -m "docs: approve astra-report implementation plan" -- designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md
git diff --cached --name-only
```

Expected: the commit contains exactly the three named paths; the pre-existing staged `Internship Diary.md` entry remains staged.

### Task 1: Canonical Coordinator Reconciliation

**Files:**
- Modify: `docs/design-requirements.md` under section 7.11
- Modify: `docs/six-skill-source-absorption.md` under sections 1, 8, and 11
- Modify: `docs/design-roadmap.md` by adding `## 15. Amendment 8 — astra-report surface and slice sequencing` after section 14.4
- Modify: `docs/phase-0.md` under sections 8 and 9
- Modify: `docs/phase-0-ledgers.md` rows `cm-docs-and-knowledge-01`, `-02`, `-03`, `-04`, `-05`, `-07`, `-09`, and `cm-design-and-visual-21`

**Interfaces:**
- Consumes: the user-approved source-slice statement and `designs/astra-report.md` sections 4.2, 4.5, 8, and 12.4
- Produces: the canonical seven-surface roster, typed relation rule, exact source claims, and the policy precondition used by every later task

- [ ] **Step 1: Enforce the consultant and trigger reconciliation gate**

Run:

```bash
rg -n "reconcile all 15 directed.*consultant pairs|final trigger surface|remaining roadmap" docs/design-roadmap.md docs/six-skill-source-absorption.md
rg -n "15-pair.*complete|consultant-pair reconciliation.*complete|trigger-surface reconciliation.*complete" docs/design-requirements.md docs/design-roadmap.md
```

Current expected result: the first command finds unresolved work and the second finds no canonical completion record. Stop here. Resume Task 1 only after the dedicated reconciliation work replaces the remaining-work language with a committed canonical pair matrix and trigger decision record. Do not reinterpret Report's producer hooks as that reconciliation.

- [ ] **Step 2: Capture the pre-migration semantic failure**

Run:

```bash
rg -n "public interface remains exactly six|target public roster is exactly|cm-docs-and-knowledge-(01|02|03|04|05|07|09)|cm-design-and-visual-21" docs/design-requirements.md docs/six-skill-source-absorption.md docs/phase-0-ledgers.md
```

Expected: the two canonical roster documents still say exactly six; the seven documentation rows are `unclaimed`; the diagram row has no `astra-report` consumer.

- [ ] **Step 3: Amend the canonical roster and relation vocabulary**

In `docs/design-requirements.md`, preserve the exactly-six **authority** roster and add this separate surface rule:

```text
The six entries above are the complete lifecycle-authority roster. `astra-report` is an
additional directly invocable reporting surface, not a lifecycle authority: under typed
`I(reporting)`, a producer delegates rich outbound presentation while retaining content,
decision, approval, and artifact authority. No determination returns, and Report
unavailability never creates an authority failure.
```

Under section 7.11.2, define `I(reporting)` as a typed `I` relation, not a new relation letter. Add the five canonical event identifiers `artifact_completion`, `approval_request`, `stage_boundary`, `status_request`, and `failure`; require `boundary_kind` to be one of `entry_refused`, `work_stopped`, or `cycle_closed` when `event_type` is `stage_boundary`.

- [ ] **Step 4: Amend the locked absorption record without changing its denominator**

Record a dated amendment in `docs/six-skill-source-absorption.md` that quotes the approved exception and says:

```text
The 92 identifier target and six-authority allocation remain unchanged. Report receives
secondary playbook or perspective claims only for `/doc`, `document-generate`, and `rtfm`;
their registrations and primary jobs remain independent, and the five-source documentation
deferral otherwise remains locked.
```

Also record the four other secondary references (`doc-coauthoring`, `internal-comms`, `teach`, and post-MVP-only `make-pdf`) and the supplemental post-MVP `diagram` consumer. Do not add any of these to the 92 tables.

- [ ] **Step 5: Migrate the exact ledger rows**

Set the seven documentation rows to:

| Occurrence | Primary disposition/home | Secondary role | Status |
|---|---|---|---|
| `cm-docs-and-knowledge-01` | independent reference / independent | `astra-report`: explanation-structure slice; resolver gap remains | `claimed` |
| `cm-docs-and-knowledge-02` | independent reference / independent | `astra-report`: chunking and fresh-reader-testing slice | `claimed` |
| `cm-docs-and-knowledge-03` | independent reference / independent | `astra-report`: plain-language, audience, and fresh-reader slice | `claimed` |
| `cm-docs-and-knowledge-04` | independent reference / independent | `astra-report`: post-MVP delivery adapter only | `claimed` |
| `cm-docs-and-knowledge-05` | independent reference / independent | `astra-report`: status, leadership, and FAQ register slice | `claimed` |
| `cm-docs-and-knowledge-07` | independent reference / independent | `astra-report`: working-memory-aware chunking slice | `claimed` |
| `cm-docs-and-knowledge-09` | independent reference / independent | `astra-report`: consumer framing and uncertainty slice | `claimed` |

Amend `cm-design-and-visual-21` without changing its current primary disposition or `claimed` state: add `astra-report` as a supplemental, post-MVP-only consumer alongside its existing consumers.

- [ ] **Step 6: Record the post-phase-0 slice transition and roadmap amendment**

In `docs/phase-0.md`, preserve the original phase-0 exclusions as historical constraints and add a dated transition that cites the user's later execution choice. Authorize only the Spec→Report approval slice in this plan after the consultant/trigger gate; keep installation, full harness, adapters, source retirement, and deletion excluded.

Amendment 8 must record:

1. six lifecycle authorities plus one non-authoritative reporting surface;
2. the source-slice approval and ledger migration;
3. producer-contract reconciliation before runtime;
4. acceptance cases for only this Spec approval slice before implementation;
5. runner machinery pulled from the slice's demonstrated needs; and
6. corpus growth per later source-retirement request, never all 92 up front.

- [ ] **Step 7: Validate the migration**

Run:

```bash
python - <<'PY'
from pathlib import Path

ledger = Path("docs/phase-0-ledgers.md").read_text()
for row in ("01", "02", "03", "04", "05", "07", "09"):
    line = next(line for line in ledger.splitlines() if f"cm-docs-and-knowledge-{row}`" in line)
    assert "astra-report" in line and "| claimed |" in line and "| resolved |" not in line, line
diagram = next(line for line in ledger.splitlines() if "cm-design-and-visual-21`" in line)
assert "astra-report" in diagram and "| claimed |" in diagram
absorption = Path("docs/six-skill-source-absorption.md").read_text()
assert "51 already-planned source identifiers + 41 newly approved identifiers = 92" in absorption
requirements = Path("docs/design-requirements.md").read_text()
assert "I(reporting)" in requirements and "not a lifecycle authority" in requirements
phase_zero = Path("docs/phase-0.md").read_text()
assert "Spec→Report approval slice" in phase_zero
assert "installation" in phase_zero and "retirement" in phase_zero
PY
```

Expected: exit 0.

- [ ] **Step 8: Commit the coordinator migration**

```bash
git add docs/design-requirements.md docs/six-skill-source-absorption.md docs/design-roadmap.md docs/phase-0.md docs/phase-0-ledgers.md
git diff --cached --check -- docs/design-requirements.md docs/six-skill-source-absorption.md docs/design-roadmap.md docs/phase-0.md docs/phase-0-ledgers.md
git commit --only -m "docs: reconcile astra-report coordinator claims" -- docs/design-requirements.md docs/six-skill-source-absorption.md docs/design-roadmap.md docs/phase-0.md docs/phase-0-ledgers.md
```

### Task 2: Producer Reporting Contracts

**Files:**
- Modify: `designs/astra-critique.md`
- Modify: `designs/astra-understand-code.md`
- Modify: `designs/astra-spec.md`
- Modify: `designs/astra-implement.md`
- Modify: `designs/astra-test.md`
- Modify: `designs/astra-ship.md`

**Interfaces:**
- Consumes: canonical `I(reporting)` and `ReportEvent` vocabulary from Task 1
- Produces: six producer contracts; the Spec approval extension is the only one exercised at runtime in this slice

- [ ] **Step 1: Record the expected pre-amendment failure**

Run:

```bash
for file in designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md; do
  rg -q "ReportEvent" "$file" || printf 'missing ReportEvent: %s\n' "$file"
done
```

Expected: all six paths are reported missing.

- [ ] **Step 2: Add the common producer fields to all six designs**

Each authoritative artifact contract gains these exact field paths:

| Field path | Type and invariant |
|---|---|
| `reporting.supersedes_ref` | `{artifact_id: string, revision: positive integer, content_hash: sha256 digest}` or `null` |
| `reporting.surfaces` | list; empty is `[]`, never omitted |
| `reporting.surfaces[].surface_id` | stable, non-empty, producer-owned string |
| `reporting.surfaces[].claim` | non-empty artifact-grounded statement |
| `reporting.surfaces[].consequence` | non-empty impact statement assigned by the producer |
| `reporting.surfaces[].blocking` | boolean |
| `reporting.surfaces[].decision_required` | boolean |
| `reporting.surfaces[].evidence_refs` | non-empty list of stable artifact-field references |
| `reporting.open_decisions` | list; empty is `[]`, never omitted |
| `reporting.open_decisions[].decision_id` | stable, non-empty, producer-owned string |
| `reporting.open_decisions[].question` | non-empty decision question |
| `reporting.open_decisions[].options` | at least two `{option_id, label, consequence}` objects with unique, non-empty IDs and non-empty text |
| `reporting.open_decisions[].evidence_refs` | non-empty list of stable artifact-field references |
| `reporting.open_decisions[].blocking` | boolean |

Critique and Spec may map an existing supersession field instead of duplicating it. Understand Code, Implement, Test, and Ship must add an explicit field. The producer, not Report, assigns every consequence and decision.

- [ ] **Step 3: Add the common event envelope and fallback**

At the user-visible-result and approval sections of every design, require producer emission of
the following exact envelope fields. Task 3 supplies the complete concrete Spec instance.

| Field | Type and invariant |
|---|---|
| `schema_version` | literal `astra.report-event/v0` |
| `event_id` | stable, non-empty producer event identifier |
| `event_type` | one of `artifact_completion`, `approval_request`, `stage_boundary`, `status_request`, `failure` |
| `boundary_kind` | one of `entry_refused`, `work_stopped`, `cycle_closed` only for `stage_boundary`; otherwise `null` |
| `producer` | one of the six canonical lifecycle skill identifiers |
| `artifact_ref` | `{artifact_id, revision, content_hash, path}` or the narrowly permitted `null` case below |
| `artifact_ref.artifact_id` | stable, non-empty artifact identifier |
| `artifact_ref.revision` | positive integer |
| `artifact_ref.content_hash` | `sha256:` followed by exactly 64 lowercase hexadecimal characters |
| `artifact_ref.path` | repository-relative path with no `..` segment |
| `outcome` | one non-empty producer-authored sentence |
| `blocking` | boolean |
| `surface_candidates` | list using the surface shape in Step 2 |
| `open_decision_refs` | list of producer decision IDs |
| `evidence_refs` | list of stable evidence references |
| `decision` | the Step 2 decision shape for `approval_request`; otherwise `null` |

State that `artifact_ref` may replace the object with `null` only for pre-artifact `entry_refused` or `failure`. For a non-decision Report outage, emit the minimal notice. For an approval outage, present the full decision envelope directly and wait only for the user's answer.

- [ ] **Step 4: Bind the Spec approval event used by the slice**

In `designs/astra-spec.md`, require `approval_request` immediately before whole-revision approval. Its `decision.decision_id` must equal one entry in `open_decision_refs`; `decision.options` must contain every available choice with consequences; Spec alone records the answer against the exact `spec_id`, revision, and hash.

- [ ] **Step 5: Validate all six contracts**

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
    for token in ("I(reporting)", "ReportEvent", "surface_id", "consequence", "open_decisions"):
        assert token in text, (path, token)
    assert "Report owns" in text
assert "Spec alone records" in Path("designs/astra-spec.md").read_text()
PY
```

Expected: exit 0.

- [ ] **Step 6: Commit the producer contracts**

```bash
git add designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md
git diff --cached --check -- designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md
git commit --only -m "docs: define lifecycle reporting contracts" -- designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md
```

### Task 3: ReportEvent Validator and Spec Fixtures

**Files:**
- Create: `skills/astra-report/scripts/report_contract.py`
- Create: `tests/astra-report/fixtures/spec-pending.json`
- Create: `tests/astra-report/fixtures/spec-approval-event.json`
- Create: `tests/astra-report/fixtures/preartifact-refusal-event.json`
- Create: `tests/astra-report/test_report_contract.py`

**Interfaces:**
- Consumes: `astra.report-event/v0` from Task 2
- Produces: `validate_event(event: dict) -> list[str]`, `verify_artifact_ref(event: dict, root: Path) -> list[str]`, and a CLI `validate-event EVENT --root ROOT`

- [ ] **Step 1: Initialize the skill package shell**

Run before any `skills/astra-report/` file exists:

```bash
python /home/kurophoenix/.codex/skills/.system/skill-creator/scripts/init_skill.py astra-report --path skills --resources scripts,references --interface 'display_name=Astra Report' --interface 'short_description=Present Astra approvals clearly and faithfully' --interface 'default_prompt=Use $astra-report to render this delegated Astra approval event faithfully for the user.'
```

Expected: the skill directory, placeholder `SKILL.md`, and `agents/openai.yaml` are created. Keep the placeholder and metadata uncommitted until Task 5; Task 3 stages only the script and tests named in its commit step.

- [ ] **Step 2: Create the immutable Spec fixture and approval envelope**

Use `ACS-REPORT-001`, revision `1`, and the field names from `designs/astra-spec.md` section 2.5 in `spec-pending.json`: intent; observed before state; problem linked to `F-REPORT-001`; selected solution; reason selected; two rejected alternatives and their consequences; after state explicitly marked `projected`; requirements `REQ-REPORT-001` through `REQ-REPORT-004`; acceptance criteria `AC-REPORT-001` through `AC-REPORT-005`; and pending decision `DEC-SPEC-001`.

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
- for `approval_request`, require a decision object, matching open-decision reference, at least two uniquely identified options, non-empty label and consequence for every option, evidence references, and `blocking: true`;
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
git add skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/test_report_contract.py
git diff --cached --check -- skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/test_report_contract.py
git commit --only -m "feat: validate astra report events" -- skills/astra-report/scripts/report_contract.py tests/astra-report/fixtures/spec-pending.json tests/astra-report/fixtures/spec-approval-event.json tests/astra-report/fixtures/preartifact-refusal-event.json tests/astra-report/test_report_contract.py
```

### Task 4: Append-Only Exposure Ledger

**Files:**
- Modify: `skills/astra-report/scripts/report_contract.py`
- Modify: `tests/astra-report/test_report_contract.py`

**Interfaces:**
- Consumes: a validated ReportEvent and an `astra.reader-brief-manifest/v0` dictionary
- Produces: `validate_manifest(event: dict, manifest: dict) -> list[str]`, `build_exposure_entry(event: dict, manifest: dict, timestamp: str, brief_content_hash: str) -> dict`, internal `_append_exposure(path: Path, entry: dict) -> None`, `write_exposure(event: dict, manifest: dict, path: Path, timestamp: str, root: Path, delivered_brief: Path) -> list[str]`, and CLI `append-exposure EVENT MANIFEST --ledger PATH --timestamp ISO8601 --root ROOT --delivered-brief PATH`

- [ ] **Step 1: Write failing exposure tests**

Add tests that assert:

1. the first append creates one newline-terminated JSON object;
2. the second append adds a second line without changing the first;
3. the entry contains only `timestamp`, `brief_id`, `brief_content_hash`, `mode`, `event_id`, `producer`, `artifact_refs`, `surfaces`, `decisions_presented`, and `degradation_flags`;
4. answer-like input keys (`answer`, `selected_option`, `approval_state`) never appear in output;
5. an invalid event produces no ledger file; and
6. surface IDs in the manifest must exist in the event; and
7. a missing or empty delivered-brief receipt produces no ledger file.

The manifest fixture used inside the test is:

```python
manifest = {
    "schema_version": "astra.reader-brief-manifest/v0",
    "brief_id": "BRIEF-SPEC-001",
    "mode": "standard",
    "event_id": "RE-SPEC-001",
    "surfaces": {
        "now": ["SURFACE-DECISION-001"],
        "next": [],
        "deferred": ["SURFACE-AFTER-PROJECTED-001"],
    },
    "decisions_presented": ["DEC-SPEC-001"],
    "degradation_flags": [],
}
```

Add these exact methods before the module's `if __name__ == "__main__"` block:

```python
    def manifest(self) -> dict:
        return {
            "schema_version": "astra.reader-brief-manifest/v0",
            "brief_id": "BRIEF-SPEC-001",
            "mode": "standard",
            "event_id": "RE-SPEC-001",
            "surfaces": {
                "now": ["SURFACE-DECISION-001"],
                "next": [],
                "deferred": ["SURFACE-AFTER-PROJECTED-001"],
            },
            "decisions_presented": ["DEC-SPEC-001"],
            "degradation_flags": [],
        }

    def test_append_is_newline_terminated_and_preserves_prior_entry(self) -> None:
        event = self.load("spec-approval-event.json")
        with tempfile.TemporaryDirectory() as directory:
            ledger = Path(directory) / "exposure.jsonl"
            delivered = Path(directory) / "brief.md"
            delivered.write_text("delivered brief", encoding="utf-8")
            errors = report_contract.write_exposure(
                event,
                self.manifest(),
                ledger,
                "2026-08-12T12:00:00+08:00",
                ROOT,
                delivered,
            )
            self.assertEqual([], errors)
            first_bytes = ledger.read_bytes()
            self.assertTrue(first_bytes.endswith(b"\n"))

            second_manifest = self.manifest()
            second_manifest["brief_id"] = "BRIEF-SPEC-002"
            errors = report_contract.write_exposure(
                event,
                second_manifest,
                ledger,
                "2026-08-12T12:05:00+08:00",
                ROOT,
                delivered,
            )
            self.assertEqual([], errors)
            lines = ledger.read_bytes().splitlines(keepends=True)
            self.assertEqual(2, len(lines))
            self.assertEqual(first_bytes, lines[0])

    def test_exposure_entry_uses_whitelist_and_omits_answer_state(self) -> None:
        event = self.load("spec-approval-event.json")
        event["answer"] = "approve"
        manifest = self.manifest()
        manifest["selected_option"] = "approve"
        manifest["approval_state"] = "accepted"
        entry = report_contract.build_exposure_entry(
            event,
            manifest,
            "2026-08-12T12:00:00+08:00",
            "sha256:" + hashlib.sha256(b"delivered brief").hexdigest(),
        )
        self.assertEqual(
            {
                "timestamp",
                "brief_id",
                "brief_content_hash",
                "mode",
                "event_id",
                "producer",
                "artifact_refs",
                "surfaces",
                "decisions_presented",
                "degradation_flags",
            },
            set(entry),
        )
        rendered = json.dumps(entry, sort_keys=True)
        for forbidden in ("answer", "selected_option", "approval_state", '"approve"'):
            self.assertNotIn(forbidden, rendered)

    def test_unknown_manifest_surface_is_rejected(self) -> None:
        event = self.load("spec-approval-event.json")
        manifest = self.manifest()
        manifest["surfaces"]["now"] = ["SURFACE-UNKNOWN-001"]
        self.assert_has_error(
            report_contract.validate_manifest(event, manifest),
            "manifest surface SURFACE-UNKNOWN-001 is absent from the event",
        )

    def test_invalid_event_does_not_create_ledger(self) -> None:
        event = self.load("spec-approval-event.json")
        event["artifact_ref"] = None
        with tempfile.TemporaryDirectory() as directory:
            ledger = Path(directory) / "exposure.jsonl"
            delivered = Path(directory) / "brief.md"
            delivered.write_text("delivered brief", encoding="utf-8")
            errors = report_contract.write_exposure(
                event,
                self.manifest(),
                ledger,
                "2026-08-12T12:00:00+08:00",
                ROOT,
                delivered,
            )
            self.assertTrue(errors)
            self.assertFalse(ledger.exists())

    def test_missing_delivery_receipt_does_not_create_ledger(self) -> None:
        event = self.load("spec-approval-event.json")
        with tempfile.TemporaryDirectory() as directory:
            root = Path(directory)
            ledger = root / "exposure.jsonl"
            errors = report_contract.write_exposure(
                event,
                self.manifest(),
                ledger,
                "2026-08-12T12:00:00+08:00",
                ROOT,
                root / "missing-brief.md",
            )
            self.assert_has_error(errors, "delivery receipt is missing or empty")
            self.assertFalse(ledger.exists())
```

- [ ] **Step 2: Run the focused tests to verify RED**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_report_contract.py' -v
```

Expected: FAIL because `build_exposure_entry`, `write_exposure`, and `_append_exposure` are absent.

- [ ] **Step 3: Implement whitelisted construction and durable append**

`validate_manifest` must require the literal schema version, non-empty brief ID, one of the three modes, matching event ID, exactly the three surface buckets, event-owned surface IDs, event-owned presented decision IDs, and string-valued degradation flags. `build_exposure_entry` must construct a new dictionary from named fields rather than copy the input and must validate the supplied lowercase SHA-256 digest syntax. `_append_exposure` must create parent directories only for the explicit caller-provided path, serialize with sorted keys and compact separators, append exactly one line in UTF-8, flush, and call `os.fsync()` before returning. It must never edit an existing line and must be called only by `write_exposure`.

`write_exposure` and the CLI validate the event, verify its artifact reference, validate the manifest/event identity and surfaces, and require `delivered_brief` to be an existing, non-empty regular file. They hash the delivered file bytes with SHA-256, pass that digest to `build_exposure_entry`, and only then append. They return or print every error; any failure exits non-zero before opening the ledger. The receipt proves delivery to this file surface only; it is not evidence that a human read or approved the brief.

- [ ] **Step 4: Run tests to verify GREEN**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
```

Expected: all validator and append tests pass.

- [ ] **Step 5: Commit the exposure boundary**

```bash
git add skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
git diff --cached --check -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
git commit --only -m "feat: append astra report exposure records" -- skills/astra-report/scripts/report_contract.py tests/astra-report/test_report_contract.py
```

### Task 5: Prompt-Driven Astra Report Skill

**Files:**
- Create: `skills/astra-report/SKILL.md`
- Create: `skills/astra-report/agents/openai.yaml`
- Create: `skills/astra-report/references/report-contracts.md`
- Create: `skills/astra-report/references/method-canon.md`

**Interfaces:**
- Consumes: a valid delegated Spec approval ReportEvent, its exact immutable artifact, optional prior Exposure Ledger, requested mode, and user context
- Produces: a Reader Brief plus its manifest; a caller with an exact delivery receipt may pass both to `append-exposure`; no authoritative artifact mutation

- [ ] **Step 1: Replace the generated skill placeholder and confirm metadata**

Replace the generated `SKILL.md` completely in Step 4. Confirm `agents/openai.yaml` retains the three exact interface values from Task 3, quotes every string value, keeps the short description between 25 and 64 characters, and includes `$astra-report` in `default_prompt`. Preserve `scripts/report_contract.py`; remove only generated example files inside `skills/astra-report/`.

- [ ] **Step 2: Write the exact contract reference**

`references/report-contracts.md` must specify:

- the five event identifiers and three boundary kinds;
- required and conditional fields from Tasks 1–3;
- `artifact_ref` hash/path verification;
- surface and decision ownership;
- Reader Brief layer order: Capsule, NOW, NEXT, DEFERRED, Change Story when applicable, Evidence;
- manifest fields from Task 4;
- the exposure-only ledger whitelist;
- failure rules, including full decision fallback belonging to the producer when Report is unavailable.

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
4. stop on contract or hash failure and identify the producer-owned correction; never repair the event;
5. compute delta only from artifact revision/hash versus explicit prior ledger entries; absent ledger means full-state rendering with a `ledger-reset` flag;
6. allocate producer-owned blockers to NOW before budgeted FYI surfaces;
7. compose Capsule, NOW, NEXT, DEFERRED, applicable Change Story, and Evidence;
8. use plain language but retain identifiers, certainty, constraints, consequences, and all approval options;
9. state every unavailable Change Story element as missing or projected; never convert a projected after-state into an observed result;
10. show the complete approval envelope and stop for the user's answer without recording it;
11. build the manifest and request exposure append only when the caller supplies a receipt for the exact delivered brief; without a receipt, render with no ledger append; and
12. return control to the producer, which alone records the user's answer.

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

### Task 6: Spec Approval Behavioral Slice

**Files:**
- Create: `tests/astra-report/evals/spec-approval-prompt.md`
- Create: `tests/astra-report/evals/spec-approval-fallback-prompt.md`
- Create: `tests/astra-report/evals/render-result.schema.json`
- Create: `tests/astra-report/evals/spec-approval-rubric.md`
- Modify: `tests/astra-report/test_report_contract.py`

**Interfaces:**
- Consumes: the skill and fixtures from Tasks 3–5
- Produces: one reproducible dogfood case covering friendly explanation, approval fidelity, absent-data behavior, and exposure bookkeeping

- [ ] **Step 1: Write the fixed dogfood prompt**

Write exactly this task prompt; it supplies the contract but does not reveal expected prose or rubric judgments:

```markdown
Exercise the repository's Astra Report skill on one fixed approval event.

1. Read `skills/astra-report/SKILL.md` and every reference that it requires for a rich approval brief.
2. Consume `tests/astra-report/fixtures/spec-approval-event.json` in `standard` mode and read only the artifact that its `artifact_ref.path` names.
3. Follow the skill's validation and fidelity rules. Do not edit any file, do not read `books/`, do not answer the approval question, and do not invoke another lifecycle authority.
4. Return one Reader Brief and its exposure manifest. The brief is user-facing Markdown. The manifest describes what that brief presented but contains no user answer or approval state.

Return only the JSON object required by the supplied output schema. Do not wrap it in a code fence and do not add commentary outside it.
```

Use this exact `render-result.schema.json`:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "additionalProperties": false,
  "required": ["brief_markdown", "manifest"],
  "properties": {
    "brief_markdown": {
      "type": "string",
      "minLength": 1
    },
    "manifest": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "schema_version",
        "brief_id",
        "mode",
        "event_id",
        "surfaces",
        "decisions_presented",
        "degradation_flags"
      ],
      "properties": {
        "schema_version": {
          "const": "astra.reader-brief-manifest/v0"
        },
        "brief_id": {
          "type": "string",
          "minLength": 1
        },
        "mode": {
          "enum": ["skim", "standard", "deep"]
        },
        "event_id": {
          "const": "RE-SPEC-001"
        },
        "surfaces": {
          "type": "object",
          "additionalProperties": false,
          "required": ["now", "next", "deferred"],
          "properties": {
            "now": {
              "type": "array",
              "items": {"type": "string"},
              "uniqueItems": true
            },
            "next": {
              "type": "array",
              "items": {"type": "string"},
              "uniqueItems": true
            },
            "deferred": {
              "type": "array",
              "items": {"type": "string"},
              "uniqueItems": true
            }
          }
        },
        "decisions_presented": {
          "type": "array",
          "items": {"type": "string"},
          "uniqueItems": true
        },
        "degradation_flags": {
          "type": "array",
          "items": {"type": "string"},
          "uniqueItems": true
        }
      }
    }
  }
}
```

Write this exact fallback prompt in `spec-approval-fallback-prompt.md`:

```markdown
Simulate Astra Spec's degraded approval presentation when Astra Report is unavailable.

Read `tests/astra-report/fixtures/spec-approval-event.json` and the artifact it references. Do not read or invoke `skills/astra-report`; this case exercises the producer-owned fallback.

Output only a complete minimal decision envelope in plain Markdown: artifact identity, revision, and content hash; decision identity and question; every option ID, label, and producer-authored consequence; every decision evidence reference; and blocking status. Do not add Capsule, NEXT, DEFERRED, Change Story, recommendations, a user answer, or an approval state.
```

- [ ] **Step 2: Write the slice rubric**

Score these as hard pass/fail gates:

1. the approval decision appears in NOW;
2. all three option IDs and their producer-authored consequences survive;
3. Spec identity, revision, hash, requirements, acceptance, and evidence anchors remain traceable;
4. before, problem, selected fix, rationale, projected after, and both recorded alternatives are present in readable chunks;
5. projected after is never stated as observed;
6. unfamiliar terms are glossed or replaced without weakening meaning;
7. no unsupported claim, recommendation, or approval answer appears;
8. NEXT contains no blocker and DEFERRED names omitted surfaces;
9. the brief says nothing else requires attention only if the event supports that claim;
10. the resulting Exposure Ledger contains the presented decision but no answer state.
11. no Exposure Ledger append occurs without the non-empty delivered `brief.md` receipt.

Add a fallback subsection with hard gates: artifact and decision identity survive; all three options and consequences survive; both decision evidence references and blocking state survive; no Report layer, recommendation, answer, or approval state appears.

Also record soft measures: word count, reading time estimate, number of chunks, critical-decision recall, unsupported-claim count, and elapsed render time. Do not establish global thresholds from this single fixture.

- [ ] **Step 3: Add a producer-owned post-answer fixture boundary test**

Add this test method before the module's `if __name__ == "__main__"` block:

```python
    def test_producer_answer_never_enters_exposure_ledger(self) -> None:
        event = self.load("spec-approval-event.json")
        manifest = self.manifest()
        with tempfile.TemporaryDirectory() as directory:
            root = Path(directory)
            approval_path = root / "spec-approval.json"
            approval_path.write_text(
                json.dumps(
                    {
                        "decision_id": "DEC-SPEC-001",
                        "selected_option": "approve",
                        "artifact_id": "ACS-REPORT-001",
                        "revision": 1,
                        "content_hash": event["artifact_ref"]["content_hash"],
                        "decided_at": "2026-08-12T12:10:00+08:00",
                        "authority": "user",
                        "approval_state": "accepted",
                    },
                    sort_keys=True,
                ),
                encoding="utf-8",
            )
            ledger = root / "exposure.jsonl"
            delivered = root / "brief.md"
            delivered.write_text("delivered brief", encoding="utf-8")
            errors = report_contract.write_exposure(
                event,
                manifest,
                ledger,
                "2026-08-12T12:11:00+08:00",
                ROOT,
                delivered,
            )
            self.assertEqual([], errors)
            stored = ledger.read_text(encoding="utf-8")
            self.assertIn('"decisions_presented":["DEC-SPEC-001"]', stored)
            for forbidden in ("approve", "selected_option", "answer", "approval_state"):
                self.assertNotIn(forbidden, stored)
```

- [ ] **Step 4: Run the deterministic suite**

Run:

```bash
python -m unittest discover -s tests/astra-report -p 'test_*.py' -v
```

Expected: all tests pass.

- [ ] **Step 5: Run the fresh-agent dogfood case**

Run:

```bash
mkdir -p /tmp/astra-report-spec-slice
codex exec -s read-only --ephemeral -C . --output-schema tests/astra-report/evals/render-result.schema.json -o /tmp/astra-report-spec-slice/render-result.json - < tests/astra-report/evals/spec-approval-prompt.md
jq -r '.brief_markdown' /tmp/astra-report-spec-slice/render-result.json > /tmp/astra-report-spec-slice/brief.md
jq '.manifest' /tmp/astra-report-spec-slice/render-result.json > /tmp/astra-report-spec-slice/brief-manifest.json
codex exec -s read-only --ephemeral -C . -o /tmp/astra-report-spec-slice/fallback.md - < tests/astra-report/evals/spec-approval-fallback-prompt.md
```

Expected: all four commands exit 0; the schema-valid render result, extracted Reader Brief, extracted manifest, and producer fallback exist. A non-zero run or schema failure is a failed slice, not a cue to relax the output contract.

- [ ] **Step 6: Apply the rubric and append exposure**

Review `/tmp/astra-report-spec-slice/brief.md` against the Report gates and `fallback.md` against the fallback gates. Then run:

```bash
python skills/astra-report/scripts/report_contract.py append-exposure tests/astra-report/fixtures/spec-approval-event.json /tmp/astra-report-spec-slice/brief-manifest.json --ledger /tmp/astra-report-spec-slice/exposure.jsonl --timestamp 2026-08-12T00:00:00+08:00 --root . --delivered-brief /tmp/astra-report-spec-slice/brief.md
```

Expected: exit 0; exactly one ledger line; it contains `DEC-SPEC-001` but no answer or selected option. Any failed hard gate returns the task to Task 5; do not weaken the rubric.

- [ ] **Step 7: Commit the slice cases**

```bash
git add tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/render-result.schema.json tests/astra-report/evals/spec-approval-rubric.md tests/astra-report/test_report_contract.py
git diff --cached --check -- tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/render-result.schema.json tests/astra-report/evals/spec-approval-rubric.md tests/astra-report/test_report_contract.py
git commit --only -m "test: cover astra report spec approval slice" -- tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/render-result.schema.json tests/astra-report/evals/spec-approval-rubric.md tests/astra-report/test_report_contract.py
```

### Task 7: Final Reconciliation and Evidence

**Files:**
- Modify: `designs/astra-report.md`

**Interfaces:**
- Consumes: all commits and evidence from Tasks 0–6
- Produces: an honest design status and a clean implementation handoff without any retirement claim

- [ ] **Step 1: Update status from observed evidence only**

In `designs/astra-report.md`, record the exact implemented slice, test command, fixture IDs, dogfood outcome, and known limits. Keep every source row `claimed`; explicitly state that public direct invocation, full corpus, other five producer runtime slices, storage default, conversation-host delivery receipt, adapters, installation, and retirement remain unimplemented.

- [ ] **Step 2: Run repository-wide documentation validation**

Run these exact validations over the planned paths only:

```bash
markdown-it docs/design-requirements.md docs/six-skill-source-absorption.md docs/design-roadmap.md docs/phase-0.md docs/phase-0-ledgers.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md skills/astra-report/SKILL.md skills/astra-report/references/report-contracts.md skills/astra-report/references/method-canon.md tests/astra-report/evals/spec-approval-prompt.md tests/astra-report/evals/spec-approval-fallback-prompt.md tests/astra-report/evals/spec-approval-rubric.md >/dev/null
git diff --check HEAD~7 -- docs/design-requirements.md docs/six-skill-source-absorption.md docs/design-roadmap.md docs/phase-0.md docs/phase-0-ledgers.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/research/2026-08-12-astra-report-method-canon.md docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md skills/astra-report tests/astra-report
python -m json.tool tests/astra-report/fixtures/spec-pending.json >/dev/null
python -m json.tool tests/astra-report/fixtures/spec-approval-event.json >/dev/null
python -m json.tool tests/astra-report/fixtures/preartifact-refusal-event.json >/dev/null
python -m json.tool tests/astra-report/evals/render-result.schema.json >/dev/null
python - <<'PY'
from pathlib import Path

targets = [
    Path("docs/design-requirements.md"),
    Path("docs/six-skill-source-absorption.md"),
    Path("docs/design-roadmap.md"),
    Path("docs/phase-0.md"),
    Path("docs/phase-0-ledgers.md"),
    Path("designs/astra-critique.md"),
    Path("designs/astra-understand-code.md"),
    Path("designs/astra-spec.md"),
    Path("designs/astra-implement.md"),
    Path("designs/astra-test.md"),
    Path("designs/astra-ship.md"),
    Path("designs/astra-report.md"),
    Path("docs/research/2026-08-12-astra-report-method-canon.md"),
    Path("docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md"),
    Path("skills/astra-report/SKILL.md"),
    Path("skills/astra-report/references/report-contracts.md"),
    Path("skills/astra-report/references/method-canon.md"),
    Path("tests/astra-report/evals/spec-approval-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-fallback-prompt.md"),
    Path("tests/astra-report/evals/spec-approval-rubric.md"),
]
for path in targets:
    text = path.read_text(encoding="utf-8")
    lines = text.splitlines()
    assert not any(
        line.startswith(("<<<<<<<", ">>>>>>>")) or line == "======="
        for line in lines
    ), path
    assert text.count("```") % 2 == 0, path
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
git diff --name-only HEAD~8..HEAD
git ls-files books
rg -n "cm-docs-and-knowledge-(01|02|03|04|05|07|09)|cm-design-and-visual-21" docs/phase-0-ledgers.md
```

Expected: no `books/` path is tracked; unrelated pre-existing dirty paths remain untouched; only planned paths appear in the eight planning-and-implementation commits; every migrated row is `claimed`, never `resolved`.

- [ ] **Step 5: Stop before installation or publication**

Report the exact commit list, validation evidence, failed or deferred gates, and remaining dirty state. Do not install the skill, push, create a PR, implement another producer slice, or retire any source without a new explicit user instruction.
