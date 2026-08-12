# Six-skill trigger-surface design

| Field | Value |
|---|---|
| Date | 2026-08-12 |
| Status | Approved design; canonical amendments not yet applied |
| Decision owner | User |
| Evidence | `docs/research/2026-08-12-six-skill-trigger-surface-reconciliation.md` |

## 1. Decision

The final public surface has **six directly invocable lifecycle authorities plus one
non-authoritative reporting surface**:

```text
Understand Code (optional current-state explanation)
Critique -> Spec -> Implement -> Test -> Ship

All six --I(reporting)--> Report --presentation--> user
```

Requests route by the authoritative result sought and the artifacts already approved, not by a
bare keyword, a historical source command, or the final verb in a compound request.

A compound request authorizes the desired end state, but it does not authorize automatic
lifecycle chaining. The initial request enters the earliest missing authority. After that skill
completes and any required approval is recorded, it may present the next prospective stage, but
only the user starts the next public workflow.

The user approved this rule on 2026-08-12 after comparing it with final-verb routing and automatic
orchestrator alternatives.

## 2. Scope

This design closes the shared trigger half of the six-skill coordinator reconciliation. It covers:

- positive, conditional, and negative public triggers for all six lifecycle skills;
- direct invocation, prerequisites, ambiguity, and compound requests;
- the boundary between public invocation and `C`, `I`, `H`, and `I(reporting)` relations;
- the public seam between Test evidence construction and Implement-owned shippable tests;
- stale active routes that still name superseded Plan or Debug peers;
- Report's approved output-only role where it affects public routing; and
- the documentation amendments and semantic checks needed to make the surface canonical.

It does not authorize a runtime router, automatic orchestration, source-ledger changes, corpus or
harness construction, skill installation, source retirement, or the deferred docs-only lifecycle.

## 3. Routing model

### 3.1 Authority matrix

| Requested authoritative result | Owner | Required state | Result |
|---|---|---|---|
| Explain current repository behavior or structure without changing it | `astra-understand-code` | Bounded code/repository scope; explicit request for `technical-design` when applicable | Current-state Code Report |
| Judge an artifact or establish why an observed failure occurs | `astra-critique` | Reviewable artifact or observed failure evidence | Finding Set or causal finding |
| Decide intended behavior, selected solution, and acceptance | `astra-spec` | User intent, or accepted findings for remediation; Critique is not mandatory for greenfield intent | Approved Change Specification |
| Plan and execute exact repository delivery | `astra-implement` | Current Approved Change Specification and effect authority | Approved Delivery Roadmap, Execution Ledger, atomic implementation commits |
| Construct or run independent proof at a pinned revision | `astra-test` | Accepted behavior, target snapshot, and effect boundary | Test Evidence Packet |
| Prepare and perform publication effects | `astra-ship` | Complete current artifact chain, passing evidence, and explicit effect authority | Publication Record |
| Explain recorded lifecycle artifacts, progress, decisions, or blockers | `astra-report` | Recorded producer artifacts or a producer-owned `ReportEvent` | Human-readable rendering; no lifecycle determination |

Understand Code is optional. The normal change path begins at Critique when a problem or cause must
be established, or at Spec for greenfield intent whose desired behavior is the open question.

### 3.2 Selection algorithm

1. Identify the authoritative result the user wants.
2. Inspect the recorded artifact state needed for that result.
3. If the user names a skill explicitly, enter that surface but enforce all of its prerequisites.
4. Otherwise choose the earliest missing authority needed for the requested outcome.
5. If two choices would materially change authority, writable scope, external effects, evidence,
   or cost, ask one focused question. Do not guess.
6. Run only that public workflow. Required `C` checks may occur within it.
7. At a reporting moment, pass a producer-owned `ReportEvent` through `I(reporting)`.
8. Stop at the artifact or approval boundary. Present later requested stages as non-invoked next
   steps; the user starts each one.

Explicit invocation is routing evidence, not a prerequisite waiver. For example, a direct Ship
request without current Test evidence may return status and the missing-evidence prerequisite, but
it cannot publish.

### 3.3 Relation boundaries

| Mechanism | May start a public peer workflow? | Binding behavior |
|---|---:|---|
| User direct request | Yes, one | Enters the selected surface subject to its gates |
| Internal mode | No | Chooses behavior after one public owner is selected |
| Artifact presence | No | Satisfies or blocks intake; may activate a required consultation |
| `C` | No | Active downstream owner requests an upstream authority check returning `pass`, `drift`, or `authority_gap` |
| `I` | No | Carries an artifact or capability without invoking judgment |
| `H` | No | Critique emits zero or one user-selected problem capsule; destination remains uninvoked |
| `I(reporting)` | No | Producer delegates presentation while retaining content and approval authority |

Broad sibling language such as "never invoke another peer" must mean "never invoke another peer's
public workflow." Required `C` consultation and output-only `I(reporting)` are typed exceptions,
not hidden lifecycle starts.

## 4. Collision decisions

| Request | Canonical route |
|---|---|
| "Explain this" | Repository/code state -> Understand Code. Artifact-chain/change state -> Report. |
| "Is this architecture right?" | Judge a choice -> Critique. Explain current structure or read-only options -> Understand Code. Select desired direction -> Spec. |
| "Why did this test fail?" | Establish cause -> Critique `diagnose`. Reproduce/check at a pinned revision -> Test. |
| "Review this failure" | Causal question -> Critique `diagnose`. Evidence/artifact-quality question -> Critique `review`. Ask once if the distinction changes evidence or cost. |
| "Fix this bug" | Cause/finding absent -> Critique. Finding present but change contract absent -> Spec. Exact Specification approved -> Implement. |
| "Write tests" | Evidence-only or explicitly uncommitted artifact -> Test. Shippable durable test for the active functionality -> Spec if not required yet, then Implement as an approved Roadmap task; Test independently verifies it. |
| "Review and ship this" | Critique first when a new judgment is requested. A clean review crosses later only as evidence; it grants no publication authority. |
| "Commit this" | Approved implementation commit -> Implement. Authorized version/changelog publication commit, push, or PR -> Ship. |
| "Resolve merge conflicts" | Ship during landing preparation. Implement only when an approved Roadmap owns base synchronization. Otherwise stop for scope and authority. |
| "Root cause analysis" | Critique `diagnose`. Live-outage stabilization remains external `firefighting`. |
| "Where are we?" | Artifact/project state -> Report. Publication authorization or queue state -> Ship Status. |
| "Turn this into an issue" | Spec only for intent/specification projection with separately authorized issue effects. Generic roadmap-to-ticket projection remains unowned. |
| "Explain, fix, test, and ship" | Enter the earliest missing authority; retain later outcomes as prospective, user-started stages. |

These partitions take precedence over stale trigger-bearing prose that sends work to the superseded
Plan or Debug peers.

## 5. Reporting flow

The six lifecycle skills remain directly invocable control surfaces. Report is directly invocable
only for recorded artifact/project-state explanation and is delegated presentation at five moments:

1. authoritative-artifact completion;
2. approval request;
3. stage boundary;
4. explicit status request; and
5. failure or degradation announcement.

The producer owns the facts, available choices, consequences, evidence, blocking state, and the
user's returned decision. Report may change organization, density, language, and explanation, but
may not add claims, select an option, return a consultant determination, start a peer, or record an
approval.

If Report is unavailable, ordinary moments degrade to the producer's minimal identity/outcome/
blocking notice. Approval requests degrade to the producer's complete minimal decision envelope so
presentation failure never hides options or consequences.

## 6. Failure behavior

| Condition | Required response |
|---|---|
| Named skill lacks a prerequisite | Refuse the prohibited work, identify the exact missing/stale artifact or authority, and name the eligible prior skill without starting it |
| Implicit request has one owner | Route to that owner |
| Two routes materially differ | Ask one focused question; preserve both interpretations until answered |
| Compound request crosses a gate | Complete only the current stage, report the next prospective stage, and stop |
| Requested work is outside the six | Name the external jurisdiction; do not stretch a nearby skill |
| Historical Plan/Debug destination appears | Apply the active replacement: Spec for missing change authority, Implement for delivery-roadmap defects, Critique `diagnose` for unknown cause |
| Report unavailable | Use the applicable degraded producer fallback; never block lifecycle progress solely on rendering |

## 7. Canonical amendment set

The implementation plan must make one atomic documentation tranche with explicit-path staging:

1. `docs/design-requirements.md` — distinguish the six lifecycle authorities from Report; add the
   authority matrix, selection algorithm, ambiguity fallback, relation boundary, compound rule,
   collision partitions, and `I(reporting)` clarification.
2. The six lifecycle designs — add precedence-bearing trigger amendments adopting direct-entry
   gates, user-mediated continuation, the five `ReportEvent` moments, approval fallback, and each
   skill-specific collision repair.
3. `designs/astra-report.md` — record the trigger reconciliation as complete without changing its
   authority or resolving its remaining coordinator/implementation tasks.
4. `docs/design-roadmap.md` — append a coordinator amendment that supersedes the historical
   eight-peer trigger decisions and marks the final trigger surface complete.
5. `docs/six-skill-source-absorption.md` — mark the trigger half of item 3 complete without changing
   allocation, ledger, runtime, harness, installation, or retirement state.

The implementation must not stage or alter the pre-existing `Internship Diary.md`,
`designs/astra-plan.md`, `.gstack/`, `.idea/`, `books/`, or `pitch/` state.

## 8. Verification design

Documentation validation must prove:

- Markdown parses and fences, tables, links, whitespace, and conflict markers are clean;
- exactly six lifecycle authority rows and one non-authoritative Report row exist;
- every collision row in section 4 has one canonical partition;
- active trigger rules contain no Plan or Debug public destination;
- explicit invocation cannot waive prerequisites;
- compound requests cannot auto-chain public workflows;
- `C`, `I`, `H`, and `I(reporting)` remain distinct;
- Critique's review/diagnose fallback is explicit;
- Test evidence-only artifacts do not bypass Implement ownership of shippable durable tests;
- Ship owns merge-conflict work only under landing authority, except approved Implement base-sync;
- all six designs expose the same five reporting moments and safe approval fallback; and
- roadmap and absorption completion claims agree while ledgers remain unchanged.

Behavioral corpus and runtime conformance tests remain part of the later vertical-slice plan. This
tranche defines the contract they will test; it does not build their runner or fixtures.

## 9. Acceptance criteria

This design is implemented when a reader can route every positive, negative, ambiguous, and
compound case without consulting historical Plan/Debug authority; no route silently gains
mutation or publication permission; each lifecycle transition remains user-controlled; Report can
render every approved reporting moment without owning lifecycle content; and the coordinator docs
unambiguously mark both halves of item 3 complete while preserving all deferred work.
