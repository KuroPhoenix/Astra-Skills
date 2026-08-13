# Six-Skill Trigger-Surface Canonical Amendments Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make the approved prerequisite-aware trigger surface and output-only Report relation canonical across policy, all six lifecycle designs, and the two coordinator records.

**Architecture:** `docs/design-requirements.md` becomes the sole normative routing and reporting-contract source. Each lifecycle design adds one precedence-bearing local amendment that maps its authority, ambiguous phrases, artifact reporting fields, and five Report events onto that policy; Report and the coordinator documents record completion without gaining lifecycle authority. Because a partial graph would leave contradictory public routes, all canonical edits land in one documentation commit after path-scoped checkpoints.

**Tech Stack:** Markdown, Git, `rg`, `markdown-it`, POSIX shell checks, Python 3 standard-library semantic assertions.

## Global Constraints

- Preserve exactly six lifecycle authorities: `astra-critique`, `astra-understand-code`, `astra-spec`, `astra-implement`, `astra-test`, and `astra-ship`.
- Preserve `astra-report` as one additional directly invocable, non-authoritative reporting surface; it owns presentation only.
- Route by requested authoritative result and current artifact state. A bare word, source name, or final verb is never sufficient routing evidence.
- Explicit invocation enters the named surface but never waives its artifact, authority, evidence, approval, or effect prerequisites.
- A compound request starts only the earliest missing authority. Later requested outcomes remain visible, non-invoked stages that the user starts individually.
- Internal modes, artifact presence, `C`, `I`, `H`, and `I(reporting)` never start another public workflow.
- Preserve the 15-pair consultant topology already committed in `4d59e42`; this tranche changes triggers and reporting, not pair direction.
- Preserve the 2026-08-13 staged Report contract in `42b3405`: Standard mode exposes Capsule/NOW and previews first, not all detail bodies.
- Keep the older Report runtime plan explicitly non-executable until a separate revision adopts multi-segment preview/detail exposure and conditional structured choices.
- Change no source allocation, `docs/phase-0-ledgers.md` row, claim/resolution state, runtime skill, schema implementation, corpus runner, harness, installation, source retirement, or docs-only lifecycle decision.
- Preserve historical Plan/Debug evidence in earlier sections. New precedence-bearing amendments replace only active public destinations.
- Preserve all unrelated staged, unstaged, and untracked work. Use exact-path checks and one `git commit --only`; never use `git add -A`.
- Create one atomic documentation commit for the ten canonical files. Do not push or create a PR in this plan.

---

## File Responsibility Map

| File | Responsibility in this tranche |
|---|---|
| `docs/design-requirements.md` | Normative roster, trigger classifier, collision partitions, relation boundary, producer reporting fields, and `ReportEvent` envelope |
| `designs/astra-critique.md` | Review/diagnose partition, earliest-authority behavior, Finding Set reporting mapping |
| `designs/astra-understand-code.md` | Explicit technical-design gate, repository-state boundary, Understanding Report reporting mapping |
| `designs/astra-spec.md` | Greenfield/remediation intent routing, issue-effect boundary, Specification reporting mapping |
| `designs/astra-implement.md` | Missing-authority and unknown-cause replacements, shippable-test and implementation-commit ownership, delivery reporting mapping |
| `designs/astra-test.md` | Reproduction-versus-cause and evidence-versus-shippable-test boundary, Test packet reporting mapping |
| `designs/astra-ship.md` | Landing-conflict and publication-commit boundary, Ship prerequisite behavior, Publication Record reporting mapping |
| `designs/astra-report.md` | Trigger reconciliation completion, direct artifact-state boundary, output-only continuation, remaining coordinator work |
| `docs/design-roadmap.md` | Amendment 9 completion record and next governed work item |
| `docs/six-skill-source-absorption.md` | Six-authority/one-reporting-surface wording and completion of locked item 3 |

## Canonical Interfaces

### Public authority classifier

```text
optional current-state explanation: Understand Code
finding or cause: Critique
intended change: Spec
repository delivery: Implement
independent evidence: Test
publication: Ship
artifact/project-state explanation: Report (non-authoritative)
```

### Producer reporting fields

Every authoritative lifecycle artifact exposes:

| Field path | Type and invariant |
|---|---|
| `reporting.supersedes_ref` | `{artifact_id, revision, content_hash}` or `null`; Critique and Spec may map their existing supersession field |
| `reporting.surfaces` | list, empty as `[]`, never omitted |
| `reporting.surfaces[].surface_id` | stable non-empty producer-owned ID |
| `reporting.surfaces[].claim` | non-empty artifact-grounded statement |
| `reporting.surfaces[].consequence` | non-empty producer-assigned impact statement |
| `reporting.surfaces[].blocking` | boolean |
| `reporting.surfaces[].decision_required` | boolean |
| `reporting.surfaces[].evidence_refs` | non-empty stable artifact-field references |
| `reporting.open_decisions` | list, empty as `[]`, never omitted |
| `reporting.open_decisions[].decision_id` | stable non-empty producer-owned ID |
| `reporting.open_decisions[].question` | non-empty producer-owned question |
| `reporting.open_decisions[].options` | at least two unique `{option_id, label, consequence}` objects |
| `reporting.open_decisions[].evidence_refs` | non-empty stable artifact-field references |
| `reporting.open_decisions[].blocking` | boolean |

Every reporting moment emits this envelope:

| Field | Type and invariant |
|---|---|
| `schema_version` | literal `astra.report-event/v0` |
| `event_id` | stable non-empty producer event ID |
| `event_type` | `artifact_completion`, `approval_request`, `stage_boundary`, `status_request`, or `failure` |
| `boundary_kind` | `entry_refused`, `work_stopped`, or `cycle_closed` for `stage_boundary`; otherwise `null` |
| `producer` | one of the six lifecycle identifiers |
| `artifact_ref` | `{artifact_id, revision, content_hash, path}`; may be `null` only for pre-artifact `entry_refused` or `failure` with stable anchors |
| `outcome` | one non-empty producer-authored sentence |
| `blocking` | boolean |
| `surface_candidates` | producer-owned surfaces using the artifact shape above |
| `open_decision_refs` | producer decision IDs |
| `evidence_refs` | stable evidence references |
| `decision` | complete matching open-decision object for `approval_request`; otherwise `null` |

Report unavailable at a non-decision moment yields only artifact/event identity, one-sentence outcome, blocking state, and an unavailable flag. At an approval request, the producer presents the complete decision envelope itself. Report failure never changes lifecycle authority.

---

### Task 0: Freeze and Verify the Execution Baseline

**Files:**
- Read: `docs/superpowers/specs/2026-08-12-six-skill-trigger-surface-design.md`
- Read: `docs/research/2026-08-12-six-skill-trigger-surface-reconciliation.md`
- Read: `designs/astra-report.md`
- Read: `docs/phase-0-ledgers.md`

**Interfaces:**
- Consumes: approved design `21d89ff`, staged-disclosure amendment `42b3405`, and pair reconciliation `4d59e42`
- Produces: a verified immutable baseline and explicit pre-existing workspace snapshot; no repository edit

- [ ] **Step 1: Verify the approved design inputs are unchanged**

Run:

```bash
git merge-base --is-ancestor 4d59e42 HEAD
git merge-base --is-ancestor 21d89ff HEAD
git merge-base --is-ancestor 42b3405 HEAD
sha256sum docs/superpowers/specs/2026-08-12-six-skill-trigger-surface-design.md docs/research/2026-08-12-six-skill-trigger-surface-reconciliation.md designs/astra-report.md docs/phase-0-ledgers.md
```

Expected hashes:

```text
43d372f134b61c48aa36ca93248ca12f95e79fa689f999f36f890d11166070ab  docs/superpowers/specs/2026-08-12-six-skill-trigger-surface-design.md
d3d042f6d1573b5e00042bf51249ce78f354cb74bd879981b930ff96ef8a239f  docs/research/2026-08-12-six-skill-trigger-surface-reconciliation.md
453c3da3931b175eee1414acf9d2a19fab6d06518620e929721d0746f03d163c  designs/astra-report.md
3f2babefc8f178fab9b77c36738e516530a5426abcdb69c261365a167fe9d15a  docs/phase-0-ledgers.md
```

Stop and reconcile the changed authority source if any hash differs. Do not mechanically update the expected hash.

- [ ] **Step 2: Snapshot the unrelated workspace state visibly**

Run:

```bash
git status --short --branch
git diff --cached --name-status
git diff --name-status -- designs/astra-plan.md
```

Expected at plan-writing time: the staged `Internship Diary.md`, unstaged `designs/astra-plan.md`, and untracked `.gstack/`, `.idea/`, `books/`, and `pitch/` remain outside the tranche. If the user's state has evolved, preserve the live state rather than forcing this historical list.

- [ ] **Step 3: Confirm the canonical gap still exists**

Run:

```bash
rg -n "final shared trigger surface remains (open|the next coordinator task)" docs/design-roadmap.md docs/six-skill-source-absorption.md
for file in designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md; do
  rg -q "ReportEvent" "$file" || printf 'missing ReportEvent: %s\n' "$file"
done
```

Expected: roadmap and absorption still declare the trigger half open; all six lifecycle designs are reported missing `ReportEvent`. If the gap is already closed, review the intervening commit rather than applying this plan twice.

### Task 1: Make Routing and Reporting Normative

**Files:**
- Modify: `docs/design-requirements.md:427-565`
- Modify: `docs/design-requirements.md` after section 7.11.5

**Interfaces:**
- Consumes: approved authority matrix, compound-request ruling, relation semantics, and Report producer contract
- Produces: normative sections 7.11.6 and 7.11.7 consumed by every local design amendment

- [ ] **Step 1: Record the expected policy failure**

Run:

```bash
for token in "earliest missing authority" "I(reporting)" "astra.report-event/v0" "Review this failure" "Understood, proceed"; do
  rg -F "$token" docs/design-requirements.md || printf 'missing policy token: %s\n' "$token"
done
```

Expected: each token is missing before the amendment.

- [ ] **Step 2: Correct the roster wording without changing authority count**

Replace “The target public roster is exactly” with “The lifecycle-authority roster is exactly” and retain the same six bullets. Immediately after them add:

```text
`astra-report` is an additional directly invocable reporting surface, not a seventh lifecycle
authority. The six retain user-to-skill intake and approval authority. Under typed
`I(reporting)`, they delegate rich outbound presentation to Report, which returns no lifecycle
determination and starts no peer workflow.
```

Do not add Report to the six-row lifecycle-authority table.

- [ ] **Step 3: Clarify `I(reporting)` inside the relation vocabulary**

In section 7.11.2, expand the `I` bullet so ordinary `I` still means artifact/capability consumption and add this typed clarification:

```text
`I(reporting)` is output-only presentation consumption. The producer owns facts, consequences,
options, evidence, blocking state, and the returned user decision; Report owns organization,
density, language, staged disclosure, and evidence links. No `pass`, `drift`, or `authority_gap`
returns. It is neither a public peer invocation nor an `H` handoff.
```

- [ ] **Step 4: Add section 7.11.6, “Shared public trigger surface”**

Insert the seven-row classifier from this plan’s “Public authority classifier” with columns `Requested result`, `Owner`, `Required state`, and `Result`. Use these exact selection rules beneath it:

1. Explicit invocation enters the named surface but enforces every prerequisite.
2. Implicit routing chooses the earliest missing authority required for the requested outcome.
3. One focused question is required when two routes materially change authority, writable scope, effects, evidence, or cost.
4. Only one public workflow runs. Required `C` checks occur inside it; `I`, `H`, and `I(reporting)` do not start peers.
5. Compound requests retain later outcomes as prospective stages and stop at every artifact or approval boundary.
6. The user starts each later public workflow. A Report continuation control cannot do so.

Close the rule with this explicit invariant: **there is no automatic public peer invocation**.
Internal modes, artifact presence, `C`, `I`, `H`, `I(reporting)`, detail selection, and
`Understood, proceed` may expose or return control to an eligible workflow, but cannot start it.

Add this collision table exactly:

| Request | Canonical partition |
|---|---|
| “Explain this” | Repository/code state -> Understand Code; lifecycle artifact/change state -> Report |
| “Is this architecture right?” | Judge a choice -> Critique; explain current structure/read-only options -> Understand Code; select desired direction -> Spec |
| “Why did this test fail?” / “does it fail?” | Establish cause -> Critique `diagnose`; reproduce/check pinned revision -> Test |
| “Review this failure” | Cause question -> Critique `diagnose`; evidence/artifact-quality question -> Critique `review`; ask once if the choice changes evidence or cost |
| “Fix this bug” | Cause/finding absent -> Critique; finding present but approved change absent -> Spec; exact Specification approved -> Implement |
| “Write tests” | Evidence-only/uncommitted artifact -> Test; shippable durable test -> Spec if not required, then Implement Roadmap task; Test independently verifies |
| “Review and ship this” | Critique first for a new judgment; clean review later crosses only as evidence and grants no publication authority |
| “Commit this” | Approved implementation commit -> Implement; authorized version/changelog publication commit, push, or PR -> Ship |
| “Resolve merge conflicts” | Ship during landing; Implement only for approved Roadmap base synchronization; otherwise stop for scope/authority |
| “Root cause analysis” | Critique `diagnose`; live-outage stabilization remains external `firefighting` |
| “Where are we?” | Artifact/project state -> Report; publication authorization or queue state -> Ship Status |
| “Turn this into an issue” | Spec only for intent/specification projection with separately authorized issue effects; generic roadmap-to-ticket projection remains unowned |
| “Explain, fix, test, and ship” | Earliest missing authority; later outcomes remain non-invoked user-started stages |

State that this table supersedes active Plan/Debug routes while preserving historical evidence.

- [ ] **Step 5: Add section 7.11.7, “Producer reporting contract”**

Copy the two field tables from this plan’s “Producer reporting fields” into the policy. Bind the five event types to artifact completion, approval request, stage boundary, explicit status request, and failure/degradation. Require non-null `artifact_ref` whenever an artifact exists; a null reference is allowed only for a pre-artifact refusal or failure with a stable producer event ID and evidence/failure anchors.

Add the two Report-unavailable fallbacks from the canonical interface block. State that the full decision envelope is never staged behind optional detail and only the producer records the user's answer.

- [ ] **Step 6: Validate the policy in isolation**

Run:

```bash
markdown-it docs/design-requirements.md >/dev/null
git diff --check -- docs/design-requirements.md
for token in "earliest missing authority" "I(reporting)" "astra.report-event/v0" "Review this failure" "Understood, proceed"; do
  rg -Fq "$token" docs/design-requirements.md
done
python3 - <<'PY'
from pathlib import Path
import re

text = Path("docs/design-requirements.md").read_text(encoding="utf-8")
authority = text.split("#### 7.11.1 Lifecycle authority", 1)[1].split("#### 7.11.2", 1)[0]
authority_rows = re.findall(r"^\| `(astra-[^`]+)` \|", authority, flags=re.MULTILINE)
assert authority_rows == [
    "astra-critique",
    "astra-understand-code",
    "astra-spec",
    "astra-implement",
    "astra-test",
    "astra-ship",
], authority_rows

trigger = text.split("#### 7.11.6 Shared public trigger surface", 1)[1].split("#### 7.11.7", 1)[0]
for identifier in authority_rows + ["astra-report"]:
    assert trigger.count(f"`{identifier}`") >= 1, identifier
assert trigger.count("`astra-report`") == 1
PY
```

Expected: exit 0. Do not commit yet; the policy is not safe to land without reciprocal local amendments.

### Task 2: Reconcile Explanation, Judgment, and Intent Triggers

**Files:**
- Modify: `designs/astra-critique.md` before Appendix A
- Modify: `designs/astra-understand-code.md` after section 12
- Modify: `designs/astra-spec.md` after section 12

**Interfaces:**
- Consumes: normative sections 7.11.6–7.11.7
- Produces: reciprocal public-entry and reporting mappings for current state, findings/causes, and intended change

Every section added in this task must include the same direct/compound-entry contract, using the
exact phrases needed by the shared checks: explicit invocation never waives prerequisites;
implicit routing uses the **earliest missing authority**; a compound request stops at this
artifact or approval boundary with later public workflows listed but not invoked; and
`Understood, proceed` returns control only and cannot start a public peer.

- [ ] **Step 1: Add Critique section 13, “Shared trigger and reporting amendment”**

Record that section 13 and policy 7.11.6 supersede earlier trigger-bearing Plan/Debug destinations without rewriting historical source evidence. Add these binding rules:

- `review` owns artifact/decision quality; `diagnose` owns why an observed failure occurs.
- “Review this failure” routes to `diagnose` for a causal question and `review` for evidence/artifact quality; ask one focused mode question only when the distinction changes evidence or cost.
- “Fix this bug” enters Critique only when cause/finding authority is missing. Critique stops with findings and never selects or applies the fix.
- Exact Critique invocation never grants mutation, instrumentation, solution selection, or Spec authority.
- A compound request completes Critique only, then exposes Spec as a non-invoked prospective stage.

Map the Finding Set to the canonical `reporting.*` fields. Reuse its existing supersession field for `reporting.supersedes_ref`. Require all five Report events and both unavailable fallbacks; Critique alone owns every claim/consequence and any returned approval record.

- [ ] **Step 2: Add Understand Code section 13, “Shared trigger and reporting amendment”**

Add these binding rules:

- Locate, trace, explain, and bounded current-state mapping route here; artifact-chain status routes to Report.
- `technical-design` remains explicit-only and is never inferred from architecture wording.
- “Is this architecture right?” routes to Critique for judgment, Understand for current structure/read-only alternatives, and Spec for selected target direction.
- Understand may offer the eligible next authority but never starts it. Direct invocation changes none of these gates.

Add `reporting.supersedes_ref` explicitly to the Understanding Report and map its reportable surfaces/open decisions. Require all five Report events and fallbacks. `I(reporting)` must not be confused with Understand's conditional downstream `C` mode.

- [ ] **Step 3: Add Spec section 13, “Shared trigger and reporting amendment”**

Add these binding rules:

- Greenfield intent may begin directly at Spec; Critique is required only when finding/cause authority genuinely participates.
- A known finding without an Approved Change Specification routes to Spec; exact repository tasks remain Implement authority.
- “Turn this into an issue” is Spec only when “this” is intent/specification and the separate issue-writing effect is authorized. Generic roadmap-to-ticket projection remains unowned.
- A compound request stops after whole-revision Specification approval; Implement remains non-invoked until the user starts it.

Map the Specification's existing supersession field to `reporting.supersedes_ref`; add surfaces and open decisions. Require `approval_request` immediately before whole-revision approval, with all option IDs, labels, producer consequences, evidence, and blocking state. Require the other four Report events and both fallbacks. Spec alone records the answer against the exact Specification revision/hash.

- [ ] **Step 4: Validate the three authority amendments**

Run:

```bash
for file in designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md; do
  markdown-it "$file" >/dev/null
  for token in "earliest missing authority" "I(reporting)" "ReportEvent" "reporting.surfaces" "reporting.open_decisions" "Understood, proceed"; do
    rg -Fq "$token" "$file"
  done
done
git diff --check -- designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md
rg -Fq 'Review this failure' designs/astra-critique.md
rg -Fq 'technical-design' designs/astra-understand-code.md
rg -Fq 'generic roadmap-to-ticket projection remains unowned' designs/astra-spec.md
```

Expected: exit 0. Keep the three files uncommitted until every downstream reciprocal amendment exists.

### Task 3: Reconcile Delivery, Evidence, and Publication Triggers

**Files:**
- Modify: `designs/astra-implement.md` after section 12
- Modify: `designs/astra-test.md` after section 12
- Modify: `designs/astra-ship.md` after section 12

**Interfaces:**
- Consumes: normative sections 7.11.6–7.11.7 and the approved local authority boundaries
- Produces: reciprocal public-entry and reporting mappings for repository mutation, independent evidence, and publication

Every section added in this task must include the same direct/compound-entry contract, using the
exact phrases needed by the shared checks: explicit invocation never waives prerequisites;
implicit routing uses the **earliest missing authority**; a compound request stops at this
artifact or approval boundary with later public workflows listed but not invoked; and
`Understood, proceed` returns control only and cannot start a public peer.

- [ ] **Step 1: Add Implement section 13, “Shared trigger and reporting amendment”**

Add these binding rules:

- Missing Approved Change Specification routes to Spec without starting it; missing/stale Roadmap approval stops before mutation.
- Unknown cause routes to Critique `diagnose`, replacing active Debug destinations. A delivery-roadmap defect still inside the approved Specification is repaired by a newly approved Roadmap revision owned by Implement; a changed outcome returns upstream.
- Durable tests, fixtures, configuration, and test documentation intended to ship with the active functionality are Implement Roadmap tasks. Separately authorized Test artifacts remain uncommitted evidence until a later approved cycle incorporates them.
- Implement owns approved implementation commits. It does not own push, PR, merge, or publication metadata except as historical source evidence.
- Compound requests stop after the approved delivery scope; Test and Ship remain user-started.

Add `reporting.supersedes_ref` to both Roadmap and Execution Ledger reporting contracts, or state the exact per-artifact mapping if one field is shared. Add surfaces/open decisions and all five Report events/fallbacks. Report may present Roadmap approval, but Implement alone records that answer.

- [ ] **Step 2: Add Test section 13, “Shared trigger and reporting amendment”**

Add these binding rules:

- “Does it fail at this revision?”, accepted-behavior test construction, BDD execution, framework setup within authority, and fresh evidence route to Test.
- “Why did it fail?” routes to Critique `diagnose`; Test preserves observation without inventing cause.
- Evidence-only or explicitly uncommitted test artifacts may be Test-owned. A durable artifact intended for publication follows Spec/Implement as stated in policy 7.11.6.
- A genuine failed or blocking-inconclusive packet starts no repair workflow; it exposes Critique as a prospective user-started stage.

Add explicit Test Evidence Packet `reporting.supersedes_ref`, surfaces/open decisions, all five Report events, and fallbacks. Test alone owns evidence claims and packet completion.

- [ ] **Step 3: Add Ship section 13, “Shared trigger and reporting amendment”**

Add these binding rules:

- Direct Ship entry may show status with missing prerequisites, but cannot publish without the complete current chain, Test evidence, and exact effect authority.
- Merge-conflict work belongs to Ship only during landing preparation; Implement owns it only when an approved Roadmap names base synchronization. Otherwise stop for scope/authority.
- Implement commits stay Implement-owned. Ship owns only separately authorized publication metadata commits and publication effects.
- “Review and ship” begins at Critique when new judgment is requested; review evidence never grants publication authority.
- Any code, behavior, evidence, or unknown-cause defect exposes the eligible earlier authority without invoking it.

Add explicit Publication Record `reporting.supersedes_ref`, surfaces/open decisions, all five Report events, and fallbacks. Ship alone records effect authorization and publication result.

- [ ] **Step 4: Validate the three downstream amendments**

Run:

```bash
for file in designs/astra-implement.md designs/astra-test.md designs/astra-ship.md; do
  markdown-it "$file" >/dev/null
  for token in "earliest missing authority" "I(reporting)" "ReportEvent" "reporting.supersedes_ref" "reporting.surfaces" "reporting.open_decisions" "Understood, proceed"; do
    rg -Fq "$token" "$file"
  done
done
git diff --check -- designs/astra-implement.md designs/astra-test.md designs/astra-ship.md
rg -Fq 'Separately authorized Test artifacts remain uncommitted evidence' designs/astra-implement.md
rg -Fq 'Why did it fail?' designs/astra-test.md
rg -Fq 'approved Roadmap names base synchronization' designs/astra-ship.md
```

Expected: exit 0. Do not commit the downstream half separately.

### Task 4: Close Report and Coordinator Reconciliation

**Files:**
- Modify: `designs/astra-report.md:5-13`
- Modify: `designs/astra-report.md:964-984`
- Modify: `designs/astra-report.md` after section 12.4
- Modify: `docs/design-roadmap.md:1-60`
- Modify: `docs/design-roadmap.md` after section 15
- Modify: `docs/six-skill-source-absorption.md:1-25`
- Modify: `docs/six-skill-source-absorption.md:403-415`

**Interfaces:**
- Consumes: all seven reconciled public surfaces and the completed 15-pair record
- Produces: an append-only coordinator completion record; no ledger or runtime state

- [ ] **Step 1: Record Report's completed trigger boundary**

Change Report's status so trigger and producer-contract reconciliation are complete while source-ledger migration, runtime-plan revision, implementation, and retirement gates remain pending. In section 12.4 mark items 1, 2, 4, 5, and 6 completed by this canonical tranche; keep item 3 pending and every row `claimed`, never `resolved`.

Append section 13, “Shared trigger-surface reconciliation result,” containing:

- direct Report requests own only recorded artifact/project-state explanation;
- repository/code-state explanation remains Understand Code;
- Report remains outside the six-authority classifier and cannot mediate input or orchestrate stages;
- detail selection and `Understood, proceed` obey the staged contract but cannot start the next public skill;
- the five `I(reporting)` moments and producer fallbacks are now canonical; and
- the older Report implementation plan remains non-executable until separately revised for staged segments.

- [ ] **Step 2: Append roadmap Amendment 9 without duplicating the normative tables**

Update the snapshot to 2026-08-13 and the status to say consultant pairs and the final trigger surface are reconciled; source internalization and runtime remain deferred. Add the Amendment 9 summary near Amendments 7–8 and change the current-roadmap rule to sections 14–16.

Append section 16, “Amendment 9 — final shared trigger surface reconciled.” Link both:

- `research/2026-08-12-six-skill-trigger-surface-reconciliation.md`; and
- `superpowers/specs/2026-08-12-six-skill-trigger-surface-design.md`.

Record approach B by name—authority-result and artifact-state routing—and cite
`docs/design-requirements.md` sections 7.11.6–7.11.7 as normative rather than copying their
tables. State that section 14.4 item 1 is now complete. Record the user-approved slice-first
resequencing in section 14.4: select one non-retiring vertical slice; write only that slice's
behavioral acceptance cases and capture drift-risk oracle behavior; implement and dogfood the
slice while letting the minimum runner mechanics emerge from demonstrated needs; and extract a
reusable corpus or harness only after repeated needs justify stable seams. The full 92-source
corpus remains a preservation/retirement obligation, not a prerequisite for the first slice.
Reiterate that no runtime, corpus runner, reusable harness, ledger, installation, deletion,
retirement, push, or PR follows from this documentation tranche.

- [ ] **Step 3: Close locked absorption item 3 without changing the 92 denominator**

Change the top roster wording to “six lifecycle authorities” and add one sentence that Report is an additional non-authoritative reporting surface whose approved secondary slices do not join or change the 92-source target.

In section 11.1 record that roadmap Amendment 9 and the trigger audit complete the trigger half,
so locked item 3 is complete in full. Replace the old item-4-before-item-5 ordering with the same
user-approved slice-first sequence: select one non-retiring slice and write only its acceptance
cases plus drift-risk oracle captures; implement and dogfood it while minimum runner mechanics
emerge; then widen the corpus or extract reusable harness structure only from demonstrated needs.
Keep source-specific preservation and retirement gates last. State explicitly that this changes
section 11's open-work ordering, which the allocation lock did not freeze; it changes no locked
allocation, source denominator, or ledger state.

- [ ] **Step 4: Validate coordinator agreement**

Run:

```bash
markdown-it designs/astra-report.md >/dev/null
markdown-it docs/design-roadmap.md >/dev/null
markdown-it docs/six-skill-source-absorption.md >/dev/null
git diff --check -- designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md
rg -Fq 'final trigger surface are reconciled' docs/design-roadmap.md
rg -Fq 'item 3 is complete' docs/six-skill-source-absorption.md
rg -Fq 'older Report implementation plan remains non-executable' designs/astra-report.md
for file in docs/design-roadmap.md docs/six-skill-source-absorption.md; do
  rg -Fq 'non-retiring vertical slice' "$file"
  rg -Fq 'behavioral acceptance cases' "$file"
  rg -Fq 'reusable harness' "$file"
done
test "$(rg -c '51 already-planned source identifiers + 41 newly approved identifiers = 92' docs/six-skill-source-absorption.md)" = 1
```

Expected: exit 0. Do not edit `docs/phase-0-ledgers.md` to make the completion claim.

### Task 5: Verify and Commit the Atomic Documentation Tranche

**Files:**
- Modify: `docs/design-requirements.md`
- Modify: `designs/astra-critique.md`
- Modify: `designs/astra-understand-code.md`
- Modify: `designs/astra-spec.md`
- Modify: `designs/astra-implement.md`
- Modify: `designs/astra-test.md`
- Modify: `designs/astra-ship.md`
- Modify: `designs/astra-report.md`
- Modify: `docs/design-roadmap.md`
- Modify: `docs/six-skill-source-absorption.md`

**Interfaces:**
- Consumes: all policy, local, reporting, and coordinator amendments
- Produces: one self-consistent canonical trigger-surface commit

- [ ] **Step 1: Parse every intended Markdown file and verify whitespace**

Run:

```bash
for file in docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md; do
  markdown-it "$file" >/dev/null
done
git diff --check -- docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md
```

Expected: exit 0 and no output from `git diff --check`.

- [ ] **Step 2: Run structural and semantic policy checks**

Run:

```bash
python3 - <<'PY'
from pathlib import Path

policy = Path("docs/design-requirements.md").read_text(encoding="utf-8")
assert "The lifecycle-authority roster is exactly" in policy
authority_ids = (
    "astra-critique",
    "astra-understand-code",
    "astra-spec",
    "astra-implement",
    "astra-test",
    "astra-ship",
)
for skill in authority_ids:
    assert skill in policy
authority = policy.split("#### 7.11.1 Lifecycle authority", 1)[1].split("#### 7.11.2", 1)[0]
authority_rows = [line.split("`")[1] for line in authority.splitlines() if line.startswith("| `astra-")]
assert authority_rows == list(authority_ids), authority_rows
trigger = policy.split("#### 7.11.6 Shared public trigger surface", 1)[1].split("#### 7.11.7", 1)[0]
assert trigger.count("`astra-report`") == 1
for token in (
    "additional directly invocable reporting surface",
    "earliest missing authority",
    "no automatic public peer",
    "I(reporting)",
    "astra.report-event/v0",
    "Review this failure",
    "Explain, fix, test, and ship",
):
    assert token in policy, token

designs = [
    Path("designs/astra-critique.md"),
    Path("designs/astra-understand-code.md"),
    Path("designs/astra-spec.md"),
    Path("designs/astra-implement.md"),
    Path("designs/astra-test.md"),
    Path("designs/astra-ship.md"),
]
events = (
    "artifact_completion",
    "approval_request",
    "stage_boundary",
    "status_request",
    "failure",
)
for path in designs:
    text = path.read_text(encoding="utf-8")
    for token in (
        "Shared trigger and reporting amendment",
        "I(reporting)",
        "ReportEvent",
        "reporting.supersedes_ref",
        "reporting.surfaces",
        "reporting.open_decisions",
        "earliest missing authority",
        "Understood, proceed",
    ) + events:
        assert token in text, (path, token)

report = Path("designs/astra-report.md").read_text(encoding="utf-8")
for token in (
    "one- or two-sentence preview",
    "preview` exposure",
    "`detail` exposure",
    "Understood, proceed",
    "non-executable",
):
    assert token in report, token

roadmap = Path("docs/design-roadmap.md").read_text(encoding="utf-8")
absorption = Path("docs/six-skill-source-absorption.md").read_text(encoding="utf-8")
assert "Amendment 9" in roadmap
assert "item 3 is complete" in absorption
assert "51 already-planned source identifiers + 41 newly approved identifiers = 92" in absorption
for text in (roadmap, absorption):
    assert "non-retiring vertical slice" in text
    assert "behavioral acceptance cases" in text
    assert "reusable harness" in text
PY
```

Expected: exit 0.

- [ ] **Step 3: Check fences, conflict markers, and prohibited scope**

Run:

```bash
for file in docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md; do
  awk '/^```/{n++} END{if (n % 2) exit 1}' "$file"
done
if rg -n '^(<<<<<<<|=======|>>>>>>>)' docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md; then exit 1; fi
test "$(sha256sum docs/phase-0-ledgers.md | cut -d' ' -f1)" = "3f2babefc8f178fab9b77c36738e516530a5426abcdb69c261365a167fe9d15a"
git diff --name-only | rg -v '^(docs/design-requirements\.md|designs/astra-(critique|understand-code|spec|implement|test|ship|report)\.md|docs/design-roadmap\.md|docs/six-skill-source-absorption\.md|designs/astra-plan\.md)$' && exit 1 || true
```

Expected: balanced fences, no conflict markers, unchanged coordinator ledger, and no newly modified path outside the ten intended files plus the pre-existing `designs/astra-plan.md`.

- [ ] **Step 4: Stage exactly the ten canonical files and inspect the index**

Run:

```bash
git add -- docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md
git diff --cached --check -- docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md
git diff --cached --name-status
```

Expected: the ten intended paths plus the user's pre-existing staged `Internship Diary.md`. Do not unstage or alter that file.

- [ ] **Step 5: Commit only the atomic trigger tranche**

Run:

```bash
git commit --only -m "docs: reconcile six-skill trigger surface" -- docs/design-requirements.md designs/astra-critique.md designs/astra-understand-code.md designs/astra-spec.md designs/astra-implement.md designs/astra-test.md designs/astra-ship.md designs/astra-report.md docs/design-roadmap.md docs/six-skill-source-absorption.md
```

Expected: one commit containing exactly the ten named paths. No push or PR.

- [ ] **Step 6: Verify the committed result and preserved user state**

Run:

```bash
git diff-tree --no-commit-id --name-only -r HEAD | sort
git diff HEAD^ HEAD --check
git status --short --branch
git diff --cached --name-status
```

Expected commit paths:

```text
designs/astra-critique.md
designs/astra-implement.md
designs/astra-report.md
designs/astra-ship.md
designs/astra-spec.md
designs/astra-test.md
designs/astra-understand-code.md
docs/design-requirements.md
docs/design-roadmap.md
docs/six-skill-source-absorption.md
```

The unrelated staged diary, unstaged `designs/astra-plan.md`, and untracked directories remain
outside the commit. The next governed work is selecting one non-retiring vertical slice and
writing only its acceptance cases plus drift-risk oracle captures. No reusable harness is designed
up front; minimum runner mechanics emerge during slice implementation, and the stale Report
runtime plan must be revised before Report can be selected for execution.
