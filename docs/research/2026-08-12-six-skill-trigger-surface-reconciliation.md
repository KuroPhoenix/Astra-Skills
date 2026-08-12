# Six-skill trigger-surface reconciliation

**Date:** 2026-08-12

**Scope:** the six coding-lifecycle authority surfaces, plus `astra-report` only where its
approved direct-request and `I(reporting)` boundaries affect routing

**Status:** propose-only coordinator research; no amendment in this record is applied, and this
record grants no runtime, ledger, installation, publication, or retirement authority

## 1. Verdict

The six lifecycle jobs are separable by the authoritative result the user is asking for:

```text
Understand Code (optional current-state explanation)
Critique -> Spec -> Implement -> Test -> Ship
finding/cause -> intended change -> repository delivery -> independent evidence -> publication
```

This is a **routing order**, not an automatic pipeline. Understand Code remains optional and
read-only; the normal change path begins at Critique, or at Spec for greenfield intent
(`docs/design-requirements.md:440-462`). The final surface should route to the earliest missing
authority needed for the requested outcome, let that one skill stop with its artifact, and require
the user to start each later public workflow.

`astra-report` does not become a seventh lifecycle authority or an orchestrator. The approved
shape is **six directly invocable lifecycle control surfaces plus one non-authoritative reporting
surface**: user-to-skill input remains direct, while rich skill-to-user output is rendered through
Report (`designs/astra-report.md:34-64`, `:545-566`). This wording resolves the present collision
between the policy's exactly-six roster and Report's approved existence; it does not change the six
authority owners.

## 2. What a trigger is—and is not

| Surface | Routing consequence | Source |
|---|---|---|
| Public job trigger | Starts exactly one authority-owning skill because the requested result is in its jurisdiction | `docs/design-requirements.md:455-486` |
| Explicit direct invocation | Enters the named control surface, but never waives its intake, effect, evidence, or approval gates; an invalid entry refuses and names the prerequisite | `designs/astra-report.md:55-64`; each design's section 2 |
| Internal mode | Selects behavior after one public owner is chosen; it is not another public skill | Critique `designs/astra-critique.md:949-968`; Spec `designs/astra-spec.md:1195-1227`; Test `designs/astra-test.md:429-445`; Ship `designs/astra-ship.md:565-571` |
| Artifact presence | Satisfies or blocks intake and may activate a consultant; it never starts a peer workflow by itself | `docs/design-requirements.md:464-479`, `:554-565` |
| `C` consultation | The already-active downstream owner invokes an upstream read-only authority check; the only results are `pass`, `drift`, or `authority_gap` | `docs/design-requirements.md:496-565` |
| `I` | Carries an artifact or capability without invoking a peer's judgment or public workflow | `docs/design-requirements.md:501-510` |
| `H` | Critique emits zero or one user-selected problem capsule; the destination remains uninvoked | `docs/design-requirements.md:501-504`; `designs/astra-critique.md:554-587`, `:610-614` |
| `I(reporting)` | The producer delegates presentation, not content authority; no determination returns and no workflow starts | `designs/astra-report.md:555-589` |
| Reporting moment | Artifact completion, approval request, stage boundary, explicit status request, or failure/degradation announcement; it triggers rendering only | `designs/astra-report.md:568-616` |

Approval direction remains asymmetric: Report presents a producer-owned request; the user's answer
returns directly to the producing skill and is recorded only in its authoritative artifact
(`designs/astra-report.md:591-613`).

## 3. Complete public trigger inventory

### 3.1 `astra-understand-code`

**Positive jobs:** locate a declaration/call; trace a request, data, or state flow; explain a
subsystem; map modules, interfaces, seams, adapters, invariants, and surprises; prepare bounded
current-state evidence; or, only on explicit request or an accepted Critique architecture problem,
give read-only technical-design advice (`designs/astra-understand-code.md:52-82`, `:500-511`).

**Conditional entrances:** `technical-design` is never inferred. `auto` may choose only `locate`,
`trace`, or `explain`, must disclose escalation, and asks when scope or cost would materially change
the answer. The `architecture-or-technical-design` `H` profile is accepted, but the user starts the
skill (`:68-70`, `:133-140`, `:638-667`). Its `consult` mode is not a public trigger; it activates
only when an already-active downstream artifact directly relies on its report (`:1085-1111`).

**Non-triggers:** adversarial judgment; deciding desired behavior; delivery planning or mutation;
test strategy; causal diagnosis; publication; deployment or incident work (`:84-96`).

### 3.2 `astra-critique`

**Positive jobs:** review an artifact or decision for evidence-backed problems; attack an approach;
judge a diff, plan, specification, architecture, infrastructure change, prompt, instruction file, or
running interface; diagnose an observed deterministic, intermittent, performance, resource, or
environment-difference failure; establish a root cause (`designs/astra-critique.md:62-69`,
`:949-968`).

**Conditional entrances:** `review` owns quality/judgment; `diagnose` owns causal establishment;
`consult` is only an internal downstream `C` entry. Factual conflicts are evidence-checked;
normative conflicts and incompatible route classifications remain user decisions. A missing lens or
destination profile stays explicit and never redirects to a convenient peer (`:513-535`,
`:610-614`, `:1002-1017`).

**Non-triggers:** merely checking whether tests pass; `cso`'s independent security-audit job;
explaining code; mutation, instrumentation, or repair; solution selection; implementation planning;
success-criterion authorship (`:71-80`, `:100-109`).

**Missing fallback:** “review this failure” can mean artifact judgment or causal investigation. The
canonical rule should be: observed-failure **why** question -> `diagnose`; artifact/decision-quality
question -> `review`; when that choice changes evidence or cost materially, ask one focused mode
question.

### 3.3 `astra-spec`

**Positive jobs:** discover vague or greenfield intent; synthesize already-resolved intent; clarify
actors, outcomes, scope, edge behavior, and acceptance; make requirements observable; select and
specify remediation for Critique findings; revise an approved Specification; optionally project the
result to an issue when that exact effect is authorized (`designs/astra-spec.md:66-76`,
`:1195-1227`).

**Conditional entrances:** `discover`, `synthesize`, `remediate`, and `revise` select authoring
behavior after Spec owns the request. The `specification-gap-or-ambiguity` `H` profile is accepted.
Blocking ambiguity gets one focused question or a fielded non-approved result. Required Understand
or Critique consultation occurs inside the active invocation and starts no peer workflow
(`:783-800`, `:858-880`, `:1221-1241`).

**Non-triggers:** current-code explanation; adversarial review; exact repository task/commit work;
project mutation; test construction/execution; causal diagnosis; publication or deployment;
generic workflow navigation or arbitrary agent dispatch (`:78-90`).

### 3.4 `astra-implement`

**Positive jobs:** from an Approved Change Specification, inspect the repository, produce and obtain
approval for an exact Delivery Roadmap, execute it as atomic commits, resume its next task from the
Execution Ledger, or perform already-authorized behavior-preserving cleanup
(`designs/astra-implement.md:92-102`, `:1206-1238`).

**Conditional entrances:** absent or stale Specification, baseline, authority, or roadmap approval
stops before mutation. Sequential execution is the safe fallback when dispatch machinery is
unavailable; missing required isolation blocks dispatch. Upstream `C` gates run inside Implement;
its own `consult` mode is exposed only to Test and Ship (`:117-137`, `:573-584`, `:1240-1270`).

**Non-triggers:** an unapproved feature request; current-state explanation; unknown-cause diagnosis;
test-strategy ownership; unbounded review/cleanup; push, PR, merge, release, deployment, or incident
work (`:104-115`).

### 3.5 `astra-test`

**Positive jobs:** construct or update evidence artifacts against accepted behavior; work test-first
at agreed seams; apply Behave, Spock, Next.js, or Bats playbooks; bootstrap bounded test
infrastructure when explicitly authorized; run tests; determine whether they pass at a pinned
revision; collect fresh completion or regression evidence (`designs/astra-test.md:62-75`).

**Conditional entrances:** accepted behavior, target snapshot, and writable/effect boundaries are
required. Explicit compatible framework requests win; materially valid policy ambiguity goes to the
user. The `test-evidence-gap` `H` profile is accepted. Test may name Implement, Critique, or Ship but
never starts them (`:90-109`, `:447-495`, `:552-573`).

**Non-triggers:** defining product behavior; code explanation or architecture choice; delivery
planning; production-code repair; causal diagnosis; independent quality judgment; publication or
exploratory QA without an accepted assertion (`:77-88`).

### 3.6 `astra-ship`

**Positive jobs:** with verified changes, show publication status; plan publication; verify and
publish one narrow PR; land or leave a branch; write an authorized version/changelog change;
resolve conflicts that arise while preparing this change-set to land; or clean up provenance-owned
workspace state after landing (`designs/astra-ship.md:74-85`, `:565-571`).

**Conditional entrances:** absent effect authority permits read-only status and an authorization
request only. Missing or stale evidence and failing checks block effects. Ambiguous merge intent is
returned as explicit choices. The `publication-defect` `H` profile is accepted, but every remedy
still needs its own effect authorization (`:102-140`, `:656-673`, `:738-768`).

**Non-triggers:** feature, production-code, or test authorship; review or diagnosis; deploy/canary;
general documentation; worktree creation; unscoped branch cleanup (`:87-100`).

### 3.7 `astra-report`, outside lifecycle authority

**Direct positive jobs:** catch up on project/artifact state; explain a Finding Set, Specification,
Test packet, or other chain artifact; enumerate open decisions or blockers. **Delegated positive
events:** the five reporting moments in section 2 (`designs/astra-report.md:138-188`, `:568-589`).

**Non-triggers:** explain repository code; write durable documentation; summarize conversation;
adjudicate findings or contradictions; deployment changelogs, retrospectives, meetings, or other
independent communication artifacts (`:158-170`). Report never starts, schedules, interrupts, or
approves a lifecycle workflow (`:196-213`).

## 4. Collision and ambiguity decisions

| Ambiguous request | Canonical partition |
|---|---|
| “Explain this” | Repository/code state -> Understand Code. Lifecycle artifact/change state -> Report. |
| “Is this architecture right?” | Judge the current/proposed choice -> Critique. Explain current structure or compare read-only deepening options -> Understand Code. Select target behavior/direction -> Spec. |
| “Why did this test fail?” / “does it fail?” | Establish cause -> Critique `diagnose`. Reproduce/check at a pinned revision -> Test. |
| “Fix this bug” | Cause/finding absent -> Critique. Finding exists but approved change contract absent -> Spec. Exact Specification approved -> Implement. |
| “Write tests” | Evidence-only or explicitly uncommitted Test artifact -> Test. A durable test intended to ship with the active functionality -> Spec if not required yet, then Implement as a Roadmap task; Test independently verifies it. This closes the collision between Test's write scope and its active normal-path rule (`designs/astra-test.md:138-156`, `:951-970`). |
| “Review and ship this” | Critique first if a new judgment is requested; a clean review crosses later as `I`, never `H` or publication authority (`designs/astra-ship.md:724-730`, `:758-768`). |
| “Commit this” | An approved implementation commit -> Implement. Separately authorized version/changelog publication commit, push, or PR -> Ship (`designs/astra-implement.md:1296-1316`; `designs/astra-ship.md:1310-1320`). |
| “Resolve merge conflicts” | Ship only inside landing preparation. Implement only when an approved Roadmap owns base synchronization. Otherwise stop for scope/authority; the old roadmap already identified the unowned middle (`docs/design-roadmap.md:1901-1904`). |
| “Root cause analysis” | Critique `diagnose`. Live-outage stabilization/incident communication remains external `firefighting`, not another coding skill (`docs/six-skill-source-absorption.md:175-185`, `:261-265`). |
| “What is blocking / where are we?” | Artifact-chain/project status -> Report. Publication scope, authorization, or queue state -> Ship Status. An active producer may receive the question directly but delegates its rich answer through `I(reporting)`. |
| “Turn this into an issue” | Spec only when “this” is intent/specification and the issue effect is explicitly authorized. No current six-skill contract owns generic roadmap-to-ticket projection. |
| “Explain, fix, test, and ship” | Start the earliest explicitly requested or missing authority. Preserve later requested outcomes as prospective follow-ups; after each artifact/report, the user starts the next skill. Never route by the final verb or pre-authorize later effects. |

## 5. Live inconsistencies to close

1. **Report migration is unapplied.** Policy still declares exactly six public roster members, and
   no sibling design contains `I(reporting)` or `ReportEvent`, while the approved Report design
   requires the roster wording, reporting hooks, and output delegation
   (`docs/design-requirements.md:427-438`; `designs/astra-report.md:618-643`, `:845-865`).
2. **Superseded destinations remain in trigger-bearing historical prose.** Plan and Debug are no
   longer public peers (`docs/design-requirements.md:436-438`), yet Implement's old `plan-required`
   handoff names Plan and its failure fallback names Debug (`designs/astra-implement.md:634-645`,
   `:735-776`); Understand and Ship retain comparable old routes
   (`designs/astra-understand-code.md:661-673`; `designs/astra-ship.md:758-768`). The active
   replacements are Spec for missing change
   authority, Implement for delivery-roadmap defects, and Critique `diagnose` for unknown cause.
3. **Test/Implement durable-test ownership is not stated at the public trigger seam.** Section 4's
   partition must become normative so a Test write does not bypass the Roadmap/atomic-commit chain.
4. **No canonical ambiguity fallback exists.** The designs locally ask or stop, but policy does not
   yet say when the shared router must ask rather than choose.
5. **Compound requests have no lifecycle rule.** Without one, a final verb can bypass missing
   authority or a source-native workflow can silently auto-chain peers.
6. **Roadmap section 13.4 is historical, not a usable six-skill surface.** It still names Plan,
   Debug, and Incident and leaves merge-conflict ownership open (`docs/design-roadmap.md:1886-1904`).

## 6. Closure approaches

### A. Bare-phrase or final-verb routing — rejected

Route on words such as “test,” “fix,” “RCA,” or “ship,” preferring the last requested action.
This is cheap, but the same words select different authorities based on artifact state, causal
certainty, effect scope, and whether the result is intended to ship. It would recreate the
collisions in section 4 and permit prerequisite bypass.

### B. Authority-result and artifact-state routing — recommended

Use the six rows in `docs/design-requirements.md:455-462` as the classifier. Explicit invocation
enters the named surface but fails closed on unmet prerequisites. Implicit routing selects the
earliest missing authority whose artifact is required for the requested outcome. When two choices
would materially change authority, writable scope, effects, evidence, or cost, ask one focused
question. A producer may present the next prospective step through Report, but only the user starts
that public workflow.

This approach preserves direct invocation, every approval gate, the `H`/`I`/`C` distinctions, and
the output-only Report decision without creating an orchestrator.

### C. Report or a lifecycle controller auto-chains the six — rejected

Treat a compound request as blanket authority to run the whole stack. This reduces ceremony, but
contradicts Report's non-orchestrator boundary, the flat-peer/no-implicit-invocation contracts, and
stage-specific approval/effect ownership (`designs/astra-report.md:55-64`, `:196-205`;
`docs/design-requirements.md:472-479`, `:506-510`). It also turns missing artifacts into hidden
control flow instead of explicit user decisions.

## 7. Exact amendment scope if approach B is approved

1. **`docs/design-requirements.md` §7.11:** preserve exactly six lifecycle authorities; add the
   one-line “plus one non-authoritative reporting surface” distinction; add one canonical trigger
   table using section 4's partitions; define direct invocation, earliest-missing-authority routing,
   one-question ambiguity fallback, compound-request continuation, and “no automatic public peer
   chaining.” Clarify that required `C` and `I(reporting)` are not public-workflow invocation.
2. **All six designs:** add a precedence-bearing trigger amendment rather than rewriting source
   evidence. Each amendment adopts the canonical direct-entry/non-trigger rule, user-mediated next
   step, five ReportEvents, complete approval envelope, and degraded Report fallback.
3. **Skill-specific repairs:** Critique gets the review/diagnose fallback; Spec owns missing
   remediation-change authority and only intent-to-issue projection; Implement replaces Plan/Debug
   destinations and states its durable-test/implementation-commit scope; Test states the
   evidence-only versus shippable-test partition; Ship states landing-only conflict ownership and
   publication-only commit scope; Understand preserves its explicit technical-design gate.
4. **`designs/astra-report.md`:** no authority redesign. Mark trigger reconciliation complete only
   after the policy/sibling wording lands; leave its other coordinator and implementation tasks
   separately open.
5. **`docs/design-roadmap.md`:** append one coordinator amendment recording approach B and mark
   roadmap §14.4 item 1 complete. Keep §13.4 as superseded historical evidence rather than editing
   old eight-skill decisions in place.
6. **`docs/six-skill-source-absorption.md` §11.1:** mark the trigger half of item 3 complete. Change
   no allocation, ledger state, runtime, harness, installation, or retirement claim.

## 8. Explicit deferrals

This audit does not design router code, trigger metadata/frontmatter, a universal runtime,
consultant execution, Report implementation, schemas, corpus, behavioral harness, adapters,
installation, source retirement, or a docs-only lifecycle. It changes no source allocation or
ledger state. Runtime conformance belongs to the later vertical slice and behavioral corpus.

## 9. Provenance

Full SHA-256 values pin the exact workspace bytes inspected. Line anchors above refer to these
bytes. Repository baseline: `4d59e42803f6d8b1a0a37dfeb53a5112c567cb58`.

| Role | File | SHA-256 |
|---|---|---|
| Governing policy | `docs/design-requirements.md` | `ae40429d5420c4b24df306aeacb3973b624344dafecb5437f3a1eebbf645920a` |
| Coordinator roadmap | `docs/design-roadmap.md` | `ed3878062b66f95594d595a4c84b56f2a660d7ebd6868ea18bc892b6278f9c40` |
| Absorption boundary | `docs/six-skill-source-absorption.md` | `29df249cdedf1afd1c2df7c460d8c4ed22df62b3e7e2d50c60a59591ca073ed9` |
| Lifecycle authority | `designs/astra-critique.md` | `3d08b780b7ebe48bb1bae6ade0bc75d25f390919356c0bc7a821381e9fb56aaa` |
| Lifecycle authority | `designs/astra-understand-code.md` | `cce0deb5a103d4fe765bb64fd2fdb893fd59624f0577a7619e200ebab6185675` |
| Lifecycle authority | `designs/astra-spec.md` | `51e0ace851a70997903d392b129a0911834e59ce9af0b06aeb8b82284f8355b5` |
| Lifecycle authority | `designs/astra-implement.md` | `38c7fb294b1de2df677e2beea9aecda42d6d31cdd558ae7bd098a2f3b6317842` |
| Lifecycle authority | `designs/astra-test.md` | `8ba726c9acb00adecff7a54810501c96086d4b974f1dc62295e9fcc3e09af665` |
| Lifecycle authority | `designs/astra-ship.md` | `af264431beeb4c1de5c41b7d27ece1ff15a3b868a0b526cdfe75df09e492804e` |
| Reporting boundary only | `designs/astra-report.md` | `5428716aa0ca089298c2d30ef853863a4573f96c1cbe8b1beefd4c32f6632110` |
