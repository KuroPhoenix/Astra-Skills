# Astra Report slice A — acceptance-case design

| Field | Value |
|---|---|
| Date | 2026-08-13 |
| Status | Approved acceptance-case design; plan and ledger reconciliations not yet applied |
| Decision owner | User |
| Scope | Absorption item 4 (roadmap 14.4 item 2) for one non-retiring vertical slice |
| Evidence | [`designs/astra-report.md`](../../../designs/astra-report.md) §§4.1.1, 4.5, 7.2–7.5, 11.2–11.5, 12.4 |
| Governing policy | [`docs/design-requirements.md`](../../design-requirements.md) §§7.11.6–7.11.7 |

## 1. Decision

Slice A is the **delegated Spec-approval path**: a Spec-owned pending revision and its approval
`ReportEvent` become a staged Reader Brief; a receipt-confirmed delivery appends to Report's
Exposure Ledger; and the user's answer remains solely in Spec's approval record.

The slice evidence in this design consists of **behavioral acceptance cases and drift-risk oracle
captures only**. It organizes those cases by **contract conformance** — three groups matching the
three contracts the slice crosses — and admits only cases that settle **mechanically**, against
artifact fields, ledger rows, and event envelopes. The separately authorized plan and ledger edits
reconcile existing records; they are not additional slice evidence or item-5 implementation.

The user selected item-4-only scope, mechanical-only pass criteria, and contract-conformance
structure on 2026-08-13, then directed that the superseded plan and the coordinator ledger also be
reconciled so the slice's statements and claims cohere.

### 1.1 Authorization

This design authorizes exactly three independently committed work products:

1. this acceptance-case specification and the source-anchored oracle capture in §3–§6;
2. a coherence reconciliation of
   [`docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md`](../plans/2026-08-12-astra-report-spec-approval-slice.md);
   and
3. one ledger-reconciliation commit containing the eight row changes already enumerated in
   `designs/astra-report.md` §4.5, the corresponding §12.4 item 3 status flip, and the historical
   hash-pin supersession note required by §8.1 of this design.

It authorizes **no** runtime skill, evaluation harness, corpus runner, installation, source
retirement, push, PR, or item-5 implementation. Every source keeps its current registration and
every migrated collision row remains `claimed`, never `resolved`.

**Ledger editing authority.** [`docs/phase-0.md`](../../phase-0.md) §1 names the Codex primary
agent the current phase-0 coordinator and **the sole editor of `docs/phase-0-ledgers.md`**; §5
repeats that design agents do not edit that file. §1 also records that the user remains the
approval authority for job boundaries, exclusions, priorities, the final roster, and every later
retirement decision — a list that does not itself name ledger edits — and it defines the transfer
mechanism: **a handoff changes the named assignee in that ledger before another agent edits it.**

The user directed this reconciliation on 2026-08-13. That direction is the recorded authorization
and is scoped to the §4.5 rows and their two exact dependent records named above; it grants no
standing ledger-editing authority for any other row or later change. Because §1 routes ledger
writes through the named assignee rather than through approval alone, the reconciliation commit
must either record a handoff naming the executing agent or be applied by the coordinator. The
current executing agent is the named Codex primary agent (`/root`), so the coordinator route
applies and no handoff is needed. The eight row changes are transcription of an already-approved
specification, not a new content decision.

## 2. Why this slice is non-retiring

Report absorbs no primary source identifier. Its six oracle sources — `/doc`, `doc-coauthoring`,
`internal-comms`, `document-generate`, `teach`, `rtfm` — all hold `independent reference`
disposition under `designs/astra-report.md` §4.5. Capturing their behavior changes no disposition
and proposes no retirement. `designs/astra-report.md` §11.5 already records **no retirement in
this tranche**, so no source-specific retirement gate is created or required here.

## 3. Case selection

`designs/astra-report.md` §11.2 enumerates 35 fixed corpus classes. That corpus is sized for an
eventual retirement comparison against six documentation oracles. This slice selects the subset
that (a) binds to the Spec-approval path and (b) settles without a human or model judge.

**Selected: 16 classes → 25 cases.** Classes 4, 5, 9, 13, 19, 20, 25, 26, 28, 29, 30, 31, 32, 33,
34, 35. Coverage is full for 14 classes and deliberately partial for classes 30 and 35; neither
partial is reported as full-class satisfaction.

**Excluded: 19 classes.** Classes 1, 2, 3, 6, 7, 8, 10, 11, 12, 14, 15, 16, 17, 18, 21, 22, 23,
24, 27 fail at least one selection filter: some exercise a different artifact, failure, resumption,
or full-chain path; others require register, clarity, density, attribution, or layer-1-completeness
judgment. `designs/astra-report.md` §11.3 requires blinded, order-randomized evaluation for the
subjective subset. That is evaluation machinery, and absorption item 4 forbids designing a
reusable harness up front. All 19 defer undiminished; exclusion here is not a claim that every one
is subjective.

**Classes 30 and 35 are bounded partials.** For class 30, "names its section" is mechanical while
"states the section's recorded conclusion and significance" is a judgment. It is admitted with a
**structural proxy** defined in §5. For class 35, the negative text-fallback branch is mechanical,
but the canonical `v0` producer contract names no approval-preference field; §5.1 prevents this
slice from inventing one. Each partial catches executable drift without claiming the full class.

## 4. Contract groups

### 4.1 Group 1 — `ReportEvent` envelope and producer authority

Ground truth: the producer's authoritative artifact plus the field tables in
`docs/design-requirements.md` §7.11.7.

| Case | Class | Passes when |
|---|---|---|
| C4 | 4 | The rendered approval preserves the exact artifact identity, revision, and hash; `decision_id`; `question`; every `option_id`, `label`, and `consequence`; non-empty `evidence_refs`; and `blocking` state |
| C9a | 9 | Report unavailable at a non-decision moment: the producer emits artifact and event identity, one non-empty outcome sentence, blocking state, and an unavailable flag — and nothing further |
| C9b | 9 | Report unavailable at an `approval_request`: the producer presents its own complete decision envelope, never a reduced one |
| C13a | 13 | An attempted re-grade leaves every producer grade byte-for-byte unchanged and returns an explicit authority refusal |
| C13b | 13 | An attempted authoritative-artifact edit leaves the artifact byte-for-byte unchanged and returns an explicit authority refusal |
| C13c | 13 | An attempted automatic Critique start produces no invocation or effect record and returns control to the user |
| C19a | 19 | `artifact_ref: null` is accepted for a pre-artifact `entry_refused` or `failure` carrying a stable producer event ID and evidence or failure anchors |
| C19b | 19 | `artifact_completion` with `artifact_ref: null` is rejected |
| C35b | 35 | Under the canonical `v0` decision shape, which has no producer-preference field, a host-mandated approval recommendation forces text fallback and marks no approval option recommended |

### 4.2 Group 2 — Exposure Ledger integrity

Ground truth: ledger rows plus artifact revision and content hash.

| Case | Class | Passes when |
|---|---|---|
| C20 | 20 | After the user answers, the ledger holds exactly one presentation row for the decision, and no answer, selected option, or approval state |
| C25 | 25 | An artifact revised without an approval-state change becomes unexposed, and the brief does not describe it as unapproved |
| C26 | 26 | Delivery without a confirmed non-empty receipt appends zero rows, and the artifact revision remains unbriefed on the next run |
| C28 | 28 | The delta derives from artifact revision and hash plus ledger ground truth, never from a "commits since last review" style selector |
| C32a | 32 | Every delivered preview records exposure level `preview`; only a selected, receipt-confirmed body records `detail` |
| C32b | 32 | Menu selection and approval state never appear in any ledger row |

### 4.3 Group 3 — Disclosure and menu behavior

Ground truth: the rendered brief structure against `designs/astra-report.md` §§7.2–7.5.

| Case | Class | Passes when |
|---|---|---|
| C5 | 5 | With four producer-owned blocking surfaces under the standard three-surface cap, all four render in NOW; no blocker is omitted |
| C29a | 29 | The initial segment contains the Capsule, materially complete NOW content, and topic previews — and zero unopened topic bodies |
| C29b | 29 | Selecting one topic reveals only that topic's body |
| C30 | 30 | Every preview satisfies the §5 structural proxy |
| C31 | 31 | Structured-choice and text-index renderings agree on topic IDs, order, previews, continuation meaning, and returned detail; no host-specific visual placement is required |
| C33a | 33 | `Understood, proceed` returns control inside an already-authorized workflow |
| C33b | 33 | `Understood, proceed` cannot approve, reject, or waive a decision, and cannot grant a new effect |
| C33c | 33 | `Understood, proceed` cannot start the next public lifecycle skill |
| C34 | 34 | Under host panel limits, every topic remains name-addressable, every page retains `Understood, proceed`, and no topic or caveat disappears between pages |
| C35a | 35 | When one topic alone links to a producer surface with both `blocking: true` and `decision_required: true`, while every other topic links only to false values, a host-required navigation recommendation names only that topic; renderer prose cannot override it |

## 5. The class-30 structural proxy

A topic preview passes when all four hold:

1. non-empty;
2. at most two sentences;
3. names a section present in the rendered brief; and
4. contains either a stable linked surface/evidence ID or one contiguous phrase of at least two
   words copied from the linked producer `claim` or `consequence` after the exact section label is
   removed. A preview containing only navigation instruction (for example "click to see more" or
   "select this option") therefore fails mechanically.

A host restricted to one sentence receives a faithful compressed preview, and the same four rules
apply to the compressed form. This proxy does not establish that a preview states its section's
recorded conclusion and significance; that judgment defers with the other 19 classes.

### 5.1 The class-35 producer-preference boundary

`docs/design-requirements.md` §7.11.7 defines an approval option as exactly
`{option_id, label, consequence}` and defines no producer-owned preference field. Therefore this
slice can settle the unsupported-recommendation fallback mechanically, but it cannot create the
positive "producer recorded that preference" fixture without changing the canonical contract.

The positive branch is **blocked, not passed**. A later amendment may name a producer-owned field
and then add a positive fixture. Until then, neither the acceptance record nor the reconciled plan
may invent `recommended`, infer preference from option order, or treat Spec's selected solution as
a recommendation about the user's approval answer.

## 6. Drift-risk oracle captures

Absorption item 4 says **capture** oracle behavior. This slice captures; it does not compare. The
capture is instruction-level evidence: exact source bytes and supporting bodies are pinned, and
the behavior most likely to drift is recorded against one approval-shaped stimulus. A generated
model answer is not treated as a stable oracle because sampling would make the supposedly
mechanical baseline nondeterministic.

The capture fixes this stimulus profile: a long pending-Spec approval brief with immutable artifact
identity, revision, and hash; one referenced graded Finding; one blocking three-option decision;
six supporting sections; a selected solution and rejected alternatives; a project-status
paragraph; unfamiliar technical terms; one material caveat; and one explicitly unverified
interface claim. Item 4 fixes the profile and source obligations, not a runnable fixture. Item 5
must pin the concrete fixture bytes before its first run and may not remove or add a profile
category without creating a new capture revision.

| Source | Pinned evidence | Captured behavior under the fixed stimulus | Primary drift risk |
|---|---|---|---|
| `/doc` | 199-line entry, SHA-256 prefix `684db9d1ef2e` | Enforce audience-appropriate register, run the three-level anti-slop scan, and apply a fresh-reader test | Fluent prose hides confidence or structure defects |
| `doc-coauthoring` | 375-line entry, `2e47d78846fa` | Preserve the three-stage protocol and refine the long brief section by section | One-shot summary skips chunk protocol and reader questions |
| `internal-comms` | 32-line entry, `067b7587a344`, plus the four §4.1.2 example hashes | Preserve status and leadership-update shapes rather than flattening every section into one register | Status shape disappears into generic documentation prose |
| `document-generate` | Generated entry `3d97c417c753`; authored template `83ce891719d1` at gstack `a3259400a366593e0c909dd9ac3e59752efd2488` / `1.60.1.0` | Keep explanation understanding-oriented and make the rationale answer why the selected solution is this way | Procedure or reference dump replaces explanation |
| `teach` | 140-line entry, `6d2dbe5e0308` | Bound chunks to working memory and preserve progressive explanation | Dense approval context arrives as one oversized block |
| `rtfm` | 360-line entry, `909197c58116` | Frame interface-facing change from the consumer's when-and-why perspective and disclose the unverified claim | Implementation detail displaces consumer consequence or uncertainty vanishes |

The hash prefixes and line anchors are the exact house-style pins recorded in
`designs/astra-report.md` §§4.1–4.1.2. Generated gstack bytes remain runtime-fidelity evidence only
and are never the sole oracle. The `document-generate` resolver and generator-registration gap in
§4.1.2 remains open and must be restated with any comparison. These captures establish no
absorption, advantage, or retirement claim.

## 7. Plan reconciliation

`docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md` has three coherence
defects against the current record.

**D1 — the external gate statement is false.** Line 27 states that the trigger-surface
reconciliation "remains remaining work" and gates Tasks 1–7. Roadmap amendment 9 closed it in
commit `be6249e`. The constraint becomes a satisfied precondition citing that revision.

**D2 — Tasks 1 and 2 are substantially complete.** `designs/astra-report.md` §12.4 records items
1, 2, 4, 5, and 6 as **Complete, 2026-08-13**: the roster amendment, the `I(reporting)` typing
convention, the four reporting hooks on all six sibling designs, the delegation clauses, and
Report's inclusion in the trigger-surface reconciliation. Only item 3 remains `Pending`. Task 1
therefore narrows to the ledger rows in §8, and Task 2 is satisfied.

**D3 — Tasks 3–6 predate the 2026-08-13 interaction contract.** Task 3 gains the class-35 negative
fallback fixture and explicitly blocks the positive producer-preference branch described in §5.1;
it does not invent a recommendation flag. Task 4's ledger schema gains `preview` and `detail`
exposure levels; Task 5 gains staged segments and structured-choice/text-index convergence; Task 6
adopts the 25 cases of §4, including the bounded class-30 and class-35 partials.

The revised plan's status becomes **reconciled; awaiting explicit execution authorization**. This
preserves the plan's own rule that runtime work requires a separate recorded choice. Reconciliation
establishes coherence, never permission.

## 8. Ledger reconciliation

Apply the eight row changes exactly as `designs/astra-report.md` §4.5 specifies — seven
`unclaimed` → `claimed` secondary-role claims plus the `diagram` secondary-consumer amendment —
then flip §12.4 item 3 from `Pending` to `Complete`.

| Occurrence | Change |
|---|---|
| `cm-docs-and-knowledge-02` `doc-coauthoring` | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-05` `internal-comms` | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-07` `teach` | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-04` `make-pdf` | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-03` `/doc` | `unclaimed` → `claimed`; lock exception approved in §4.2 |
| `cm-docs-and-knowledge-01` `document-generate` | `unclaimed` → `claimed`; lock exception approved in §4.2; the §4.1.2 resolver gap must still close before resolution |
| `cm-docs-and-knowledge-09` `rtfm` | `unclaimed` → `claimed`; lock exception approved in §4.2 |
| `cm-design-and-visual-21` `diagram` | stays `claimed`; add `astra-report` as post-MVP supplemental-delivery consumer |

Rows become `claimed`, never `resolved`. None joins the locked 92. The three lock exceptions
change claim ownership only and leave all five deferred documentation sources outside the 92
target.

### 8.1 Superseded hash pin

`docs/superpowers/plans/2026-08-13-six-skill-trigger-surface-amendments.md` pins the ledger's
SHA-256 at `3f2babefc8f178fab9b77c36738e516530a5426abcdb69c261365a167fe9d15a` in two places
(lines 129 and 634) as a frozen-baseline check. This reconciliation legitimately changes that
file, so both pins become stale.

The reconciliation must record the post-change SHA-256 and mark the prior pin **superseded as of
2026-08-13 by this authorized ledger change**. The prior pin remains valid evidence for the
trigger-surface tranche it verified; it is not deleted.

## 9. Degradation handling

A slice with unrunnable cases degrades silently into a slice that always passes. Three rules
prevent that:

1. A case whose fixture is missing is **blocked**, never passed.
2. A host without structured-choice support runs only the text-index half of C31. That is a
   **recorded limitation**, not a pass.
3. An oracle source unavailable at its pinned source bytes is captured as a **gap with its
   consequence**, never substituted with a nearby version.

Governing rule: **any case that cannot fail is not a case.** It is removed or rewritten.

## 10. Deliberately left open

| Open item | Where it is recorded |
|---|---|
| Exposure Ledger file format, storage location, brief identity scheme | `designs/astra-report.md` §12.2 |
| Whether the §7.5 budget defaults suit this user | `designs/astra-report.md` §12.3 question 2 |
| Whether intake dialogue appends to the ledger — currently no | `designs/astra-report.md` §12.3 question 1 |
| The public direct-request runtime path and its direct-exposure ledger schema | `designs/astra-report.md` §12.2; needs its own behavioral slice |
| The 19 excluded cross-path and judged classes | §3 of this design |

## 11. Delivery

Three separate commits, each independently reviewable and matching §1.1:

1. this acceptance-case design and oracle-capture record;
2. the existing implementation-plan reconciliation; and
3. the ledger reconciliation: the eight rows, `designs/astra-report.md` §12.4 item 3, and the §8.1
   historical hash-pin supersession note.

The user's staged `Internship Diary.md` and unstaged `designs/astra-plan.md` are preserved
untouched. Each commit uses path-scoped staging and verifies those unrelated entries afterward.
No push and no PR.
