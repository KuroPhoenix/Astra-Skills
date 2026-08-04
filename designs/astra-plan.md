# Astra Plan — phase-0 design

> Status: **proposed design only**. This document does not install, generate,
> validate, retire, rename, invoke, or modify any skill, agent, hook, tracker,
> project file, or ledger. Every ledger entry below is a proposal for later
> coordinator reconciliation.

This is the phase-0 design for public flat peer **4. `astra-plan`** in the
fixed public tranche:

1. `astra-critique`
2. `astra-understand-code`
3. `astra-spec`
4. `astra-plan`
5. `astra-implement`
6. `astra-test`
7. `astra-debug`
8. `astra-ship`

The design uses the repository's exact evidence labels:

- **O — observed:** present in a body, referenced bundle file, registration,
  manifest, or current peer design that was inspected.
- **I — inferred:** a phase-0 design conclusion that still needs comparison or
  coordinator agreement.
- **U — unavailable/unknown:** bytes, runtime behavior, authority, or a peer
  contract was unavailable or unresolved.

The design also uses `module`, `interface`, `implementation`, `depth`, `seam`,
`adapter`, `leverage`, and `locality` in the sense defined by the inspected
`codebase-design` guidance. A seam is a real place where implementations meet;
an adapter exists only where at least two observed delivery shapes justify an
interface. “Boundary” below means ownership or effect authority, not an
invented software interface.

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-plan` |
| Status | `proposed` |
| Priority | `now` for completing this phase-0 design contract; implementation remains later and gated |
| Candidate neighborhood | Plan & spec: `cm-plan-and-spec-02`, `08`, `09`, `10`, and `11` |
| User job | **When I want to turn an explicitly accepted Spec into a complete, implementation-ready Plan whose exact work, ordering, interfaces, verification, effects, stops, rollback, and handoff can be reviewed before anyone changes the project.** |
| Accepts Critique handoff | **conditional**, for the user-selected `execution-plan-defect` problem class and compact payload in §7.2 |

**One job:** the table's user job has one outcome—an executable Plan artifact.
Its task graph, verification matrix, effect ledger, and handoff are parts of
that result, not independent jobs.

**Personal value — explicit.** The user selected `astra-plan` as the fourth
peer in an exact eight-peer public design tranche and supplied its accepted
Spec/Implement/Test/Understand/Critique authority contract. That is direct
evidence that an approval-safe, implementation-ready Plan is valuable for the
user's project development and makes this design a `now` priority. The claimed
quality advantage of combining source behavior is still **I** and requires
section 9; no usage count is used to predetermine the architecture.

**Phase-0 classification:** public flat peer; design only; not implemented or
validated.

**Primary users:** a user who has accepted a Spec and wants an executable plan,
or a downstream implementer who needs an explicitly approved plan.

**Core authority:** analysis and artifact rendering in the conversation only.
The core may inspect user-authorized, read-only project evidence. It has zero
authority to write a plan file, edit the project, create or update issues,
change tuning state, create tasks, dispatch agents, execute a step, run a test,
diagnose a failure, critique a result, commit, or ship.

**Approval rule:** “executable” means sufficiently concrete to execute; it does
not mean authorized for execution. A newly rendered Plan has `status: draft`
and `approval.state: unapproved`. Only an explicit user decision can attach an
approval record. `astra-plan` never infers approval from acceptance of the
upstream Spec, silence, continued conversation, a ticket, a saved file, or an
execution request.

**Source status:** all five assigned originals remain installed. Phase 0 makes
no validation, replacement, or retirement claim.

**Deferred general-purpose names:** Context, Guard, Delegate, Automate,
Incident, and Deploy are not public or absorbed peers in this tranche. Where
one of those concerns is needed, this design names an honest user-mediated or
external prerequisite; it does not invent a peer.

## 2. Interface and scope

### 2.1 Requests that should trigger it

- “Turn this accepted spec into an implementation plan.”
- “Produce exact tasks, dependencies, paths, interfaces, and verification for
  this approved change.”
- “Plan this wide migration using expand–migrate–contract steps.”
- “Make the plan buildable by another implementer, but do not implement it.”
- “Create a plan revision for this accepted change in constraints.”
- “Render a draft ticket projection from this approved plan without publishing
  tickets.”

The trigger is not the word “plan”; it is the combination of an accepted Spec,
available implementation evidence, and a request for an executable work
artifact.

### 2.2 Nearby requests that should not trigger it

- Deciding the product intent, requirements, success criteria, or acceptance
  examples belongs to `astra-spec`.
- Locating code, explaining architecture, or selecting a technical design
  belongs to `astra-understand-code`; the retained Architect agent remains
  there.
- Changing files, updating progress state, creating commits, or coordinating
  implementers belongs to `astra-implement` or an explicitly authorized
  external workflow.
- Constructing or running tests, collecting evidence, and final verification
  belongs to `astra-test`.
- Explaining a failure's cause belongs to `astra-debug`.
- Judging a plan or implementation belongs to `astra-critique`.
- Landing, publishing, releasing, or deploying belongs to `astra-ship` or an
  explicit external workflow.
- Mapping unresolved intent into decision tickets belongs to retained
  `wayfinder`; it happens before Spec acceptance, not inside Plan.
- Changing question preferences or developer-profile state belongs to retained
  `plan-tune`.

If the request still contains a blocking product or architecture decision,
`astra-plan` stops and identifies that decision. It does not decide it under
the guise of a planning assumption.

### 2.3 Small public interface

The conceptual interface is deliberately small:

```text
plan(
  accepted_spec,
  read_only_project_context,
  optional_understand_evidence,
  optional_test_strategy,
  optional_accepted_debug_evidence,
  explicit_presentation_preferences
) -> draft_executable_plan | blocked_plan_report
```

The interface has one operation and two terminal result kinds. Modes,
decomposition strategies, graph construction, renderers, and source-derived
checks remain implementation details inside the module.

`read_only_project_context` names the repository/artifact, exact revision,
dirty state, and relevant generated contracts available for inspection. It is a
Plan input, not a hidden field added to the accepted Spec. Missing context is
matched against `readiness.required_plan_inputs` and may produce a blocked
result.

`explicit_presentation_preferences` are values supplied in this request. The
module does not read `plan-tune` state, question logs, profiles, or hooks.

### 2.4 Proposed accepted-Spec input contract

The concurrently drafted `astra-spec` design is now available. This Plan input
proposal adopts its entire section-2.5 field set and non-inference gate rather
than inventing a second schema. The contract remains coordinator-provisional,
but the two drafts are field-aligned as of 2026-08-03. Unless stated otherwise,
each field is required and an empty collection is `[]`, not omission.

**Identity, lifecycle, and approval**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `schema_version` | non-empty string | Must be a reconciled supported schema version. |
| `spec_id` | stable non-empty string | Root of requirement and Plan traceability across revisions. |
| `revision` | positive integer | Binds this Plan to one Spec revision. |
| `content_hash` | digest over canonical meaning-bearing fields | Plan verifies the approval-bound hash before use and records it in `spec_ref`. |
| `title` | non-empty string | User-recognizable subject; never converted into a task title by itself. |
| `subject_ref` | string or explicit `null` | Context locator only; not proof of current project bytes. |
| `supersedes_revision` | integer or `null` | Lets Plan invalidate an older Plan whose Spec was superseded. |
| `revision_reason` | non-empty string | Preserves why replanning may be necessary. |
| `lifecycle.state` | `draft`, `reviewing`, `accepted`, `changes_requested`, `rejected`, `superseded`, or `blocked` | Only `accepted` is consumable. |
| `lifecycle.created_at` | timestamp | Provenance, not acceptance. |
| `lifecycle.updated_at` | timestamp | Helps detect stale supplied bytes; not acceptance. |
| `approval.state` | `not_requested`, `pending`, `accepted`, `changes_requested`, `rejected`, or `superseded` | Must be `accepted`; never inferred. |
| `approval.decider` | user/stakeholder identity or `null` | Must be non-null and authorized; an agent is not acceptance authority. |
| `approval.approved_revision` | integer or `null` | Must equal `revision`. |
| `approval.approved_content_hash` | digest or `null` | Must equal `content_hash`. |
| `approval.decided_at` | timestamp or `null` | Spec-decision evidence; does not approve Plan. |
| `approval.decision_ref` | conversation/event ref or `null` | Must be non-null and is carried into `spec_ref`. |
| `approval.authority_scope` | non-empty list drawn from `intent`, `scope`, `requirements`, `acceptance`, `whole_revision` | Must contain `whole_revision` and every meaning-bearing changed area. |
| `approval.section_decisions` | list of `{ section_id, state, decider, decision_ref }` | Preserved as staged evidence; never substitutes for whole-revision acceptance. |

**Intent and product outcomes**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `intent.problem` | non-empty outcome-language string | Plan operationalizes but does not rewrite the problem. |
| `intent.affected_actors` | list of `{ actor_id, description }` | Connects tasks and verification to affected parties/systems. |
| `intent.desired_outcomes` | list of `{ outcome_id, actor_ids, statement }` | Forms the Plan's outcome trace; not implementation steps. |
| `intent.why_now` | string or explicit `null` | Preserved rationale; not automatic scheduling authority. |
| `intent.success_measures` | list of `{ measure_id, outcome_ids, observable, target, observation_window }` | Becomes measurement/evidence obligations without selecting telemetry implementation. |
| `intent.non_goals` | list of strings | Negative scope check on every task and projection. |

**Scope, assumptions, dependencies, and current state**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `scope.in_scope` | list of `{ scope_id, statement, rationale }` | Upper limit of work. |
| `scope.out_of_scope` | list of `{ scope_id, statement, rationale }` | Explicit task exclusion. |
| `scope.constraints` | list of `{ constraint_id, kind, statement, source_ref }` | Binding compatibility/policy/legal/time/platform constraints; Plan cannot waive them. |
| `scope.assumptions` | list of `{ assumption_id, statement, certainty, evidence_refs, validation_owner }` | Blocking uncertainty stops; accepted non-blocking uncertainty remains visible and owned. |
| `scope.dependencies` | list of `{ dependency_id, kind, required_state, owner, availability }` | Product/policy/external-system/stakeholder/evidence prerequisites, distinct from package/task dependencies. |
| `current_state.observed_behavior` | list of `{ observation_id, statement, evidence_refs, certainty }` | Reconciled against the exact read-only project snapshot. |
| `current_state.invariants` | list of `{ invariant_id, statement, evidence_refs }` | Constrains module/interface/seam and compatibility planning. |
| `current_state.known_gaps` | list of `{ gap_id, statement, consequence }` | Becomes a visible stop, Plan gap, or explicit evidence task; never guessed away. |

Spec-local certainty values remain `observed`, `inferred`, or `unavailable` and
are distinct from this design's O/I/U evidence labels.

**Behavior and acceptance**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `behavior.scenarios` | list of `{ scenario_id, actor_ids, preconditions, trigger, expected_sequence, terminal_state }` | Maps desired journeys to implementation and integration tasks without treating product sequence as task order. |
| `behavior.requirements` | list of `{ requirement_id, kind, statement, rationale, source_refs }`, with kind `functional`, `quality`, `policy`, `compatibility`, or `data` | Every requirement maps to a task and verification or an explicit non-code disposition. |
| `behavior.acceptance_criteria` | list of the exact criterion shape below | Primary requirement-to-verification contract. |
| `behavior.negative_cases` | list of `{ case_id, trigger, required_response, forbidden_response, requirement_ids }` | Drives failure-path tasks and tests. |
| `behavior.permissions_and_roles` | list of `{ rule_id, actor_id, allowed, denied, condition }` | Preserves product authorization semantics without granting Plan effects. |
| `behavior.data_and_contract_rules` | list of `{ rule_id, subject, required_behavior, compatibility, evidence_refs }` | Feeds data/API compatibility and migration obligations. |
| `behavior.accessibility_and_localization` | list of `{ rule_id, jurisdiction, required_behavior }` | Receives explicit tasks/evidence where applicable. |

Every `behavior.acceptance_criteria[]` item is consumed field for field:

| Criterion field | Required shape | Plan use |
|---|---|---|
| `criterion_id` | stable non-empty string | Verification identity. |
| `requirement_ids` | non-empty list | Traceability edge to accepted requirements. |
| `actor_or_system` | non-empty string | Observer/evidence owner context. |
| `preconditions` | list of strings | Task and verification preconditions. |
| `trigger` | non-empty string | Planned test/action trigger, not task authorization. |
| `observable_outcome` | non-empty string | Expected result. |
| `failure_or_negative_case` | string or `null` | Failure-path obligation. |
| `measure` | string or `null` | Measurement obligation when present. |
| `threshold` | string, number, or `null`; cannot exist without `measure` | Exact gate, not an estimate. |
| `evidence_method_class` | `test`, `inspection`, `measurement`, `stakeholder_confirmation`, or `external_verification` | Routes the proof obligation without invoking its owner. |

**Decisions and technical constraints**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `decisions.alternatives` | list of `{ alternative_id, summary, benefits, costs, risks, disposition, decision_ref }` | Only selected/accepted rulings constrain Plan; open/deferred items remain visible and may block. |
| `decisions.selected_direction` | `{ alternative_id, rationale, decision_ref }` or `null` | Product/design direction, not executable decomposition. |
| `decisions.user_rulings` | list of `{ decision_id, question, answer, authority, decision_ref, affected_fields }` | Preserves every material user decision and prevents Plan from relitigating it. |
| `technical_constraints.modules` | list of `{ module_ref, observed_role, evidence_refs }` | Starting module map; exact paths still require current project evidence. |
| `technical_constraints.interfaces` | list of `{ interface_ref, invariant, compatibility, evidence_refs }` | Accepted interface and compatibility constraints. |
| `technical_constraints.seams` | list of `{ seam_ref, reason, evidence_refs }` | Accepted integration/test seam constraints, not a selected implementation sequence. |
| `technical_constraints.adapters` | list of `{ adapter_ref, external_system, constraint, evidence_refs }` | Existing external adaptation facts; Plan does not invent an adapter from one hypothetical variation. |
| `technical_constraints.forbidden_prescriptions` | fixed list containing `task_order`, `files_to_change`, `implementation_commands`, `effort_estimates`, `rollout_steps` | Confirms these are absent from Spec and must be derived by Plan from accepted intent plus current project evidence. |

**Evidence, uncertainty, readiness, and delivery**

| Spec field path | Required shape | Plan interpretation |
|---|---|---|
| `evidence.items` | list of `{ evidence_id, source_kind, source_ref, claim, certainty, captured_at }` | Attributed support; stale or unavailable claims cannot justify exact paths/interfaces. |
| `evidence.conflicts` | list of `{ conflict_id, evidence_refs, description, ruling_ref }` | An unruly blocking conflict stops; Plan never silently chooses a source. |
| `uncertainty.open_questions` | list of `{ question_id, question, owner, blocking, affected_fields }` | Blocking items stop; accepted non-blocking items remain in Plan gaps/stops. |
| `uncertainty.unavailable_inputs` | list of `{ input_id, description, consequence, fallback }` | Matched to current Plan inputs and degraded honestly. |
| `readiness.plan_state` | `ready` or `blocked` | Must be `ready`. |
| `readiness.blocking_question_ids` | list of IDs | Must be `[]`. |
| `readiness.nonblocking_question_ids` | list of IDs | Carried into Plan gaps, assumptions, and change policy. |
| `readiness.required_plan_inputs` | list of strings | Exact additional read-only context/evidence Plan must obtain; cannot contain unresolved product decisions when ready. |
| `readiness.acceptance_map` | list of `{ requirement_id, criterion_ids }` | Must cover every requirement and seeds Plan traceability. |
| `delivery.mode` | `none`, `local_document`, or `issue` | Spec delivery fact only. |
| `delivery.authorized` | boolean | Does not authorize Plan or Implement effects. |
| `delivery.destination_ref` | string or `null` | Provenance locator only. |
| `delivery.result` | `not_attempted`, `succeeded`, `failed`, or `partial` | Independent of acceptance. |
| `delivery.failure` | string or `null` | Preserved context; does not force Plan delivery. |
| `delivery.observed_at` | timestamp or `null` | Freshness evidence for external delivery only. |

Plan consumes the artifact only when the Spec non-inference gate passes exactly:

1. `lifecycle.state == accepted`;
2. `approval.state == accepted`;
3. `approval.approved_revision == revision`;
4. `approval.approved_content_hash == content_hash`;
5. `approval.decider` is non-null and `approval.authority_scope` contains
   `whole_revision` plus every changed meaning-bearing area;
6. `approval.decision_ref` is non-null;
7. `readiness.plan_state == ready`;
8. `readiness.blocking_question_ids == []`;
9. every requirement appears in `readiness.acceptance_map`; and
10. no referenced `uncertainty.open_questions[]` item with `blocking: true`
    remains unresolved.

Section decisions, issue/label state, document commits, delivery success,
external review, or informal “looks good” prose do not satisfy this gate. A new
Spec `revision` and `content_hash` invalidate prior Plan approval. Spec delivery
failure does not revoke an otherwise accepted artifact, and delivery success
does not accept a draft. Separate `read_only_project_context` must still satisfy
`readiness.required_plan_inputs`; otherwise Plan returns
`blocked_plan_report`.

### 2.5 Optional evidence contracts

Optional evidence is user-supplied. `astra-plan` does not invoke another peer
to obtain it.

**Accepted Understand Code evidence** follows the inspected peer design and
must contain: repository and revision; relevant paths and symbols; the accepted
module/interface/seam choice; invariants; constraints; rejected alternatives;
and known gaps. An Architect blueprint is accepted only when it arrives through
that evidence with attribution and explicit user acceptance. Plan never owns or
invokes the Architect agent.

**Test strategy or evidence** may contain: accepted behavior and snapshot;
test modes and framework; changed test artifacts; seams; exact commands,
working directories, environment prerequisites, and expected exit or result;
red/green/mutation evidence where it already exists; evidence gates; gaps; and
cleanup state. Plan may carry and order those obligations. It does not claim the
commands passed, invent evidence, or invoke `astra-test`.

**Accepted Debug evidence** is optional only for a repair-plan request. It must
identify the diagnosed cause, evidence, affected contract, remediation
constraint, and user acceptance of the diagnosis. Raw symptoms do not become a
diagnosis inside Plan.

### 2.6 Proposed executable-Plan output contract

This is the field-for-field **proposal for reconciliation with
`astra-implement`**. The canonical artifact is data; Markdown views are
renderings, not separate authorities.

| Field | Required shape | Invariant |
|---|---|---|
| `schema` | literal `astra.plan.executable/v0` | Unknown schemas stop downstream execution. |
| `plan_id` | stable non-empty identifier | Does not change across a pure rendering change. |
| `plan_version` | immutable version identifier | Any task, scope, effect, verification, or dependency change increments it. |
| `status` | `draft`, `approved`, or `superseded` | New output is always `draft`. |
| `approval` | `{ state, decision_id, actor, decided_at, approved_version, approved_effect_scope }`; null decision fields while unapproved | An approval applies to exactly one version and effect scope. |
| `spec_ref` | `{ spec_id, revision, content_hash, approval: { decision_ref, decider, decided_at, authority_scope } }` | Complete upstream identity and revision-bound acceptance trace using the Spec field names. |
| `goal` | exact accepted goal plus a non-normative execution summary | Summary cannot change intent. |
| `baseline` | `{ repository, base_revision, branch_or_detached, worktree, dirty_state, preexisting_changes, relevant_paths, generated_contract_refs }` | All path/interface claims and mutation protections are relative to this snapshot. |
| `scope` | `{ in_scope, out_of_scope, requirement_refs }` | No task may escape it. |
| `planning_inputs` | list of `{ kind, artifact_ref, version_or_revision, accepted_by, claim_scope }` | Distinguishes accepted evidence from unsupported context. |
| `architecture_constraints` | list of `{ id, module, interface, seam, invariant, source_ref }` | Uses accepted technical evidence; Plan does not choose a new architecture. |
| `execution_policy` | `{ allowed_effects, forbidden_effects, mutation_scope, network_policy, install_policy, commit_policy, worktree_policy, issue_policy, live_system_policy }` | Every effect is denied unless explicitly allowed later by the user. Plan records policy; it does not exercise it. |
| `execution_decision` | `{ state, mode, segment_map, worktree_approval, checkpoint_commit_approval, decision_ref }`, where `state` is `undecided` or `accepted` and mode is `sequential`, `task-dispatch`, `mixed`, or `null` | User-owned Implement routing. A new draft is undecided; no source default or Plan recommendation sets acceptance. |
| `phases` | ordered list of `{ phase_id, title, outcome, entry_gate, task_ids, exit_gate }` | A phase is a dependency/verification grouping, not runtime progress state. |
| `tasks` | ordered list of the exact task shape below | Each task must be independently reviewable and have a demonstrable result. |
| `dependency_edges` | list of `{ from_task, to_task, kind, rationale }` where `kind` is `blocks`, `requires-interface`, `requires-evidence`, or `serialization-only` | Every ordering constraint has a reason; parallelism is never inferred from numbering. |
| `verification_matrix` | list of `{ obligation_id, requirement_refs, task_refs, method, command_ref_or_review, expected_result, evidence_owner }` | Covers every requirement and NFR or states why it is non-verifiable in this plan. |
| `effect_ledger` | list of `{ effect_id, task_ref, target, effect_kind, reversibility, authorization_needed }` | Makes writes, installs, network calls, commits, tracker actions, and live effects visible before approval. |
| `global_stops` | list of `{ stop_id, condition, evidence_to_report, decision_owner }` | Stops are executable conditions, not “use judgment.” |
| `rollback` | list of `{ rollback_id, trigger, affected_task_refs, procedure, limits, evidence }` | No claim of reversibility without a procedure and limit. |
| `handoff` | exact downstream shape below | Lets Implement reject an incomplete or unauthorized plan. |
| `projections` | optional `{ phase_summary, ticket_draft }` | Pure views only; no file or tracker publication. |
| `traceability` | list of `{ requirement_ref, task_refs, verification_refs, risk_refs }` | No orphan requirement or orphan task. |
| `gaps` | list of `{ gap_id, certainty, impact, blocking, owner, next_decision }` | Unknowns stay visible. |
| `change_policy` | `{ changes_requiring_spec_reacceptance, changes_requiring_plan_reapproval, progress_state_owner }` | Progress belongs to Implement; Plan revisions never rewrite history. |

Every `tasks[]` item contains:

| Task field | Required content |
|---|---|
| `task_id`, `title`, `outcome` | Stable identity and one demonstrable outcome. |
| `requirement_refs` | Exact accepted requirements covered. |
| `dependencies` and `parallel_safety` | Task IDs plus the shared files, interfaces, state, or evidence that make parallel work safe or unsafe. |
| `preconditions` | Snapshot, prior artifacts, decisions, tool availability, and clean/dirty-state requirements. |
| `files` | Exact path entries with operation `create`, `modify`, `move`, or `delete`; stable symbols or ranges when known; deletions require explicit accepted scope. |
| `interfaces` | Consumed and produced module interfaces, schema/API changes, compatibility rule, and seam affected. |
| `steps` | Ordered, concrete implementation actions; no “wire it up,” TODO, ellipsis, or hidden research. Code fragments appear only when derivable and materially disambiguating. |
| `test_cycle` | Required red/green/refactor or other accepted strategy, including who owns missing construction. |
| `verification` | Exact commands or review procedures, each with working directory, prerequisites/environment, expected result, failure interpretation, and evidence to retain. |
| `acceptance` | Observable task-level criteria linked to requirement IDs. |
| `effects` | Allowed target, effect class, reversibility, and separate authorization needed. |
| `stops` | Conditions that prevent beginning or continuing this task. |
| `rollback` | Task-local recovery or explicit “irreversible” with escalation owner. |
| `handoff` | Artifacts, evidence, unresolved gaps, and next task or peer recipient after user mediation. |
| `checkpoint_policy` | Whether a checkpoint would help and what it contains; never commit authorization. |

The `handoff` object contains: `recipient: astra-implement`; exact
`plan_id/version`; Spec reference; Plan approval record; ordered and parallel
task sets; allowed and forbidden mutation scope; acceptance criteria;
verification commands and Test artifact refs; stop and rollback rules; branch,
detached/worktree, dirty-state, pre-existing-change, and base context; unresolved
non-blocking gaps; the accepted/undecided execution decision; and separate
worktree/checkpoint-commit approvals. Implement must stop if any required field
is missing, contradictory, stale, or unapproved.

### 2.7 User-visible result and blocked result

The normal result is one draft executable Plan with three adjacent items:

1. a short scope and authority header;
2. the canonical task, dependency, verification, effect, stop, rollback, and
   handoff content;
3. a separate approval request that names the exact version and effect scope.

Optional `phase_summary` and `ticket_draft` projections may accompany the same
artifact. They cannot contain facts absent from the canonical Plan.

Execution mode, worktree use, and checkpoint-commit policy are separate
user-owned decisions. Plan may present those choices after the Plan is accepted,
but recording a choice neither executes the Plan nor authorizes unrelated
effects.

A `blocked_plan_report` contains: accepted Spec reference; the exact missing or
contradictory evidence; why it prevents exact planning; the owner of the next
decision; safe read-only evidence that could unblock it; and the unchanged
effect policy. It contains no guessed implementation sequence.

### 2.8 Non-goals and decisions retained by the user

`astra-plan` does not:

- decide intent, accept a Spec, choose a product requirement, or waive scope;
- select an architecture when no user-accepted technical decision exists;
- write or edit a project or plan file;
- create, update, label, assign, block, or close a ticket or issue;
- create tasks, update progress checkboxes, maintain execution summaries, or
  adapt a live plan after work starts;
- execute, dispatch implementers or agents, test, debug, critique, commit,
  release, deploy, or ship;
- read or mutate question preferences, psychographic profiles, logs, API
  credentials, or gbrain state;
- treat a source plugin's broad tool declaration as Plan authority.

The user retains Spec and Plan acceptance, mutation/effect authorization,
execution mode, worktree and commit policy, tracker publication, live-system
access, choice among conflicting technical alternatives, plan revision after
execution begins, and source retirement.

## 3. Source evidence and proposed ledger changes

### 3.1 Assigned occurrence inspection record

**Inspection date for every row and immutable anchor below: 2026-08-03.** All
five assigned skill bodies were available. The only partial body-linked
artifact was planb's observed `examples.md`, whose own bytes end in a truncation
marker.

Observed live locations and registration aliases:

- `writing-plans`:
  `/home/kurophoenix/.codex/plugins/cache/openai-curated-remote/superpowers/6.2.0/skills/writing-plans/`
  plus the Superpowers plugin manifest and installed registry entry;
- `planb`: `/home/kurophoenix/.claude/skills/planb` →
  `/mnt/c/Users/kurop/Desktop/University/Intern/monster-prompt/claude/skills/planb`;
- `plan-tune`: `/home/kurophoenix/.claude/skills/plan-tune/SKILL.md` → the
  generated Gstack `plan-tune/SKILL.md`, with body-linked binaries under
  `/home/kurophoenix/.claude/skills/gstack/bin/` and registered Claude hooks;
- `wayfinder`: `/home/kurophoenix/.claude/skills/wayfinder` →
  `/home/kurophoenix/.agents/skills/wayfinder`;
- `to-tickets`: `/home/kurophoenix/.claude/skills/to-tickets` →
  `/home/kurophoenix/.agents/skills/to-tickets`.

| Collision row | Source | Component and invocation | Inspected body and directly relevant delivery | Authority/effects and dependencies | Failure behavior | Certainty |
|---|---|---|---|---|---|---|
| `cm-plan-and-spec-02` | `superpowers:writing-plans` | Skill; explicit `/superpowers:writing-plans`, with metadata also permitting description-based discovery | Full `SKILL.md`; full reviewer prompt; full OpenAI metadata; Codex plugin manifest; installed plugin registry entry and enabled setting | Reads spec/code and prescribes a Markdown plan, exact files/code/tests, self-review, and an execution choice. Default save location is `docs/superpowers/plans/...`. Bundle reviewer text calls for a reviewer agent, while the main body says self-review without a subagent. Requires the Superpowers bundle and project evidence. | Stops on unclear scope by asking; can produce placeholders or wrong paths if evidence is weak. Source-internal reviewer contradiction is unresolved. Broad plugin capabilities are not Plan permission. | O |
| `cm-plan-and-spec-08` | `planb` | Skill; explicit `/planb`; live Claude registration is a symlink into `monster-prompt` | Full `SKILL.md`, `examples.md`, `references/format.md`, `references/parallel-execution.md`, and `references/task-tracking.md`; source marketplace manifest inspected and does not register Plan B | Mixed plan-authoring and execution system: goal confirmation, phases, tasks, acceptance criteria, dependency/parallel structure, plan file, Claude tasks, dispatch, progress updates, advisor calls, validation, adaptation, skip/abort/auto-fix. Depends on task tooling, agents, plan files, and a shared worktree during execution. | Can mutate plan/progress state and execute beyond Plan authority. The observed `examples.md` ends with a literal truncation marker. Its no-code planning rule conflicts with writing-plans' code-rich rule. | O |
| `cm-plan-and-spec-09` | `plan-tune` | Stateful skill plus hooks and local binaries; explicit `/plan-tune` or declared trigger phrases; no `disable-model-invocation` field observed | Full generated skill and source template; version; relevant AskUserQuestion hook registrations and shell shims; full question preference, question log, developer profile, distill, and apply binaries | Reads/writes `~/.gstack` tuning, logs, profiles, proposals, consent and sync state; can call Anthropic for distillation, publish to gbrain, and in broader gstack setup affect project guidance. Requires Bun/gstack, optional API key/billing and gbrain. It is not a plan author. | Must respect one-way-door questions and user-origin trust. Generated text says a three-per-day rate cap, while the inspected distill binary says no rate cap. Stateful/privacy behavior cannot be collapsed into Plan. | O |
| `cm-plan-and-spec-10` | `wayfinder` | Skill; explicit `/wayfinder`; `disable-model-invocation: true`; Claude registration is a symlink to the cross-agent source | Full `SKILL.md` and full OpenAI metadata | Maps unresolved intent as a root issue plus decision tickets; uses tracker-native blocking, labels, assignment, claims, research/prototype/grilling tasks, agents, and one-ticket-per-session progress. Defaults to local Markdown only when no tracker exists. | Requires an issue tracker or explicit local fallback and may create/update/assign/close issues or dispatch research. It solves pre-Spec decision fog, not implementation planning. | O |
| `cm-plan-and-spec-11` | `to-tickets` | Skill; explicit `/to-tickets`; `disable-model-invocation: true`; Claude registration is a symlink to the cross-agent source | Full `SKILL.md` and full OpenAI metadata | Decomposes a plan/spec/conversation into tracer tickets, blocking edges, and expand–migrate–contract slices; presents a draft, then publishes local `.scratch/.../issues/*.md` files or real tracker issues after approval. May inspect code, ADRs, and glossary. | Publication mutates files or a remote tracker. Its ticket view intentionally avoids fragile exact paths and implementation detail, which conflicts with Implement's canonical intake if used as the only Plan. | O |

No listed `agents/openai.yaml` file declares an executable retained agent. Those
files are interface metadata. The only assigned source with agent behavior is
`planb`'s runtime dispatch protocol; that behavior is in the skill, not a
separate agent component.

### 3.2 Declarations and non-skill delivery shapes

The observed declarations are preserved because discovery and delivery shape
are part of the occurrence, not incidental prose:

| Source | Observed declaration | Registration and invocation consequence | Certainty |
|---|---|---|---|
| `writing-plans` | `name: writing-plans`; description: “Use when you have a spec or requirements for a multi-step task, before touching code.” OpenAI metadata declares display name “Writing Plans” and short description “Turn specs into detailed multi-step implementation plans.” | Installed inside Superpowers 6.2.0 with an enabled plugin registry entry. The skill announces itself and is available as `/superpowers:writing-plans`; its description also supports skill selection. | O |
| `planb` | `name: planb`; `effort: high`; description: “Create and execute structured project plans with phases, tasks, and acceptance criteria. Supports interactive execution, multiple validation types, and automated progress tracking. Plans are action-oriented without code examples.” | Live Claude path is a personal symlink. The inspected source marketplace manifest registers `loop-goal`, not `planb`; therefore the live symlink/frontmatter, not that marketplace entry, is the observed declaration path. Explicit invocation is `/planb`. | O |
| `plan-tune` | `name: plan-tune`; `preamble-tier: 2`; `version: 1.0.0`; description: “Self-tuning question sensitivity + developer psychographic for gstack (v1: observational). (gstack)”; triggers `tune questions`, `stop asking me that`, `too many questions`, `show my profile`, `show my vibe`, `developer profile`, `turn off question tuning`; allowed tools Bash, Read, Write, Edit, AskUserQuestion, Glob, Grep. | Generated live skill is linked to Gstack source. It is available through `/plan-tune` and trigger phrases; no implicit-invocation prohibition was observed. Declared tools describe source delivery, not Plan authority. | O |
| `wayfinder` | `name: wayfinder`; description: “Plan a huge chunk of work — more than one agent session can hold — as a shared map of decision tickets on your issue tracker, and resolve them one at a time until the way to the destination is clear.”; `disable-model-invocation: true`. OpenAI metadata declares display name “Wayfinder,” short description “Map a large effort as decision tickets,” and `allow_implicit_invocation: false`. | Cross-agent source is exposed to Claude by symlink; explicit invocation is `/wayfinder`. | O |
| `to-tickets` | `name: to-tickets`; description: “Break a plan, spec, or the current conversation into a set of tracer-bullet tickets, each declaring its blocking edges, published to the configured tracker — edges as text in one file per ticket locally, or native blocking links on a real tracker.”; `disable-model-invocation: true`. OpenAI metadata declares display name “To Tickets,” short description “Split a plan into tracer-bullet tickets,” and `allow_implicit_invocation: false`. | Cross-agent source is exposed to Claude by symlink; explicit invocation is `/to-tickets`. | O |

The directly relevant Superpowers plugin manifest was also read completely. Its
declaration is recorded compactly rather than treating its broad plugin fields
as Plan permission:

```yaml
name: superpowers
version: 6.2.0
description: "An agentic skills framework & software development methodology that works: planning, TDD, debugging, and collaboration workflows."
author: { name: Jesse Vincent, email: jesse@fsck.com, url: https://github.com/obra }
homepage: https://github.com/obra/superpowers
repository: https://github.com/obra/superpowers
license: MIT
skills: ./skills/
hooks: {}
keywords: [brainstorming, subagent-driven-development, skills, planning, tdd, debugging, code-review, workflow]
interface:
  displayName: Superpowers
  developerName: Jesse Vincent
  shortDescription: "A dev methodology for agents"
  longDescription: "Use Superpowers to guide agent work through brainstorming, implementation planning, test-driven development, systematic debugging, parallel execution, code review, and finish-the-branch workflows."
  category: Developer Tools
  capabilities: [Interactive, Read, Write]
  brandColor: "#F59E0B"
  brandColorDark: "#F59E0B"
  logo: ./.codex-plugin/assets/logo.png
  composerIcon: ./.codex-plugin/assets/composer-icon.svg
  websiteURL: https://github.com/obra/superpowers
  privacyPolicyURL: https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement
  termsOfServiceURL: https://docs.github.com/en/site-policy/github-terms/github-terms-of-service
  defaultPrompt:
    - "I've got an idea for something I'd like to build."
    - "Let's add a feature to this project."
```

Those fields describe the bundle, not the authority of the `writing-plans`
occurrence or future Plan. **O**

The non-skill shapes and source-native commands also remain explicit:

- `writing-plans` ships a reviewer prompt, OpenAI interface metadata, plugin
  manifests, and an installed/enabled registry record in addition to its skill
  body. It references `superpowers:using-git-worktrees` for execution context
  and sends completed plans toward `superpowers:subagent-driven-development`
  or `superpowers:executing-plans`. The metadata is not a reviewer agent and
  neither that routing nor the reviewer prompt is automatic Plan authority.
  **O**
- `planb` defines a Markdown plan file, phase/task/acceptance checkbox state,
  `TaskCreate`/`TaskUpdate`/`TaskList`/`TaskGet` records with blocking edges,
  `AskUserQuestion` gates, optional `advisor()` calls, general-purpose Agent
  calls for parallel batches in the shared working directory, validation
  summaries, phase reviews, adaptations, and live task-status updates. Those
  command/state/agent shapes remain outside Plan even where its authoring
  schema learns from them. **O**
- `plan-tune` registers a PreToolUse AskUserQuestion preference hook and
  PostToolUse question-log/error-fallback hooks. Its observed command surface
  includes `gstack-question-preference --check|--write|--stats`,
  `gstack-question-log <json>`,
  `gstack-developer-profile --read|--profile|--vibe|--gap`,
  `gstack-distill-free-text --status|--background`, and
  `gstack-distill-apply --list|--proposal N`. These commands operate on local
  tuning/profile/log/proposal state and, in some paths, external services; none
  is a Plan adapter. **O**
- `wayfinder` delivers a tracker root issue labelled `wayfinder:map`, child
  decision issues, native blocking edges, names/links, assignment and claims,
  frontier/fog/out-of-scope state, and optional agent-backed research or
  prototypes. Its local-Markdown fallback is still a write. **O**
- `to-tickets` delivers one local `.scratch/<slug>/issues/*.md` file per ticket
  with textual edges, or real tracker tickets with native blocking, labels, and
  publication state. It directs the user to `/setup-matt-pocock-skills` when
  tracker and triage-label vocabulary is missing and ordinarily applies the
  `ready-for-agent` label. Draft projection, tracker setup, and publication are
  different effects. **O**

### 3.3 Disposition and preserved contribution

| Source | Proposed disposition and primary home | Contribution categories | Contribution to `astra-plan` | Behavior deliberately outside `astra-plan` | Retirement implication |
|---|---|---|---|---|---|
| `superpowers:writing-plans` | **proposed Astra design**; primary home `astra-plan` | Machinery, Protocol, Playbook, Jurisdiction, Prerequisite | Scope check; exact file/interface map; small concrete actions; test-first/verification detail; expected results; placeholder and type-consistency self-review. | Saving under `docs/...`, commits, reviewer-agent dispatch, and choosing an execution workflow. | Not eligible until the reviewer contradiction and all save/commit/dispatch semantics have a tested, explicitly authorized home or approved deletion. |
| `planb` | **proposed Astra design for authoring slice**; primary home `astra-plan`; mixed execution slice remains installed and **Separate** from Plan | Machinery, Protocol, Playbook, Jurisdiction, Prerequisite, Separate | Goal confirmation; phase/task hierarchy; typed acceptance criteria; dependency and parallel-safety reasoning; action-oriented no-code summary projection; validation and adaptation fields. | Plan-file writes, Claude task creation, subagent dispatch, task execution, progress tracking, phase reviews, advisor calls, automatic fixes, and live adaptation. | The occurrence cannot be retired merely because authoring behavior is internalized. Mixed execution/tracking behavior needs another owner, non-regression proof, or user-approved deletion. The truncated example must be recovered or explicitly accepted as unavailable. |
| `plan-tune` | **retained independent**; primary home remains retained `plan-tune` | Separate, Machinery, Protocol, Prerequisite, Reference | No runtime dependency. Plan may honor a preference explicitly supplied in the current request. | All preference/profile/log/hook/distillation/consent/sync/gbrain behavior. | Not a Plan retirement candidate. Its stateful bundle and observed rate-cap contradiction require their own design. |
| `wayfinder` | **retained independent**; primary home remains retained `wayfinder` | Separate, Machinery, Protocol, Playbook, Jurisdiction, Prerequisite | At most, Plan consumes a user-approved closed-decision/map snapshot already reflected in the accepted Spec. | Intent discovery, issue-map ownership, issue mutations, assignee claims, agents, and one-ticket-per-session workflow. | Not a Plan retirement candidate. The current Spec draft does not define a Wayfinder input; coordinator reconciliation must decide whether such a map is accepted evidence. |
| `to-tickets` | **proposed Astra design for pure decomposition and projection**; primary home `astra-plan`; publisher delivery remains installed | Machinery, Protocol, Playbook, Jurisdiction, Prerequisite | Tracer vertical slices, demoable fresh-context tickets, blocking edges, prefactoring, and expand–migrate–contract sequencing; draft ticket projection. | Local issue files, remote issue creation, labels, assignment, tracker edges, and all publication. | Whole-source retirement is blocked until publisher delivery is preserved elsewhere with explicit effect authority, or the user approves its deletion. |

No assigned source contributes an independent Plan **Perspective** on current
evidence. The code-rich/no-code disagreement changes representation and
playbook, not who owns the decision or what recommendation policy has standing.
That classification is **I** and must be challenged by divergence cases in §9.2.

### 3.4 Exact proposed collision-ledger changes

These rows are not applied here. The roadmap allocation was treated as an
investigation candidate, not a predetermined merger: full-body evidence is why
Plan Tune and Wayfinder remain independent and why planb/To Tickets are only
partially internalized.

| Row | Proposed status | Proposed primary home | Proposed secondary role | Evidence point and unresolved authority |
|---|---|---|---|---|
| `cm-plan-and-spec-02` | `claimed` | `astra-plan` | `astra-implement` consumes only the approved Plan artifact, never this source | Exact-path/action/verification authoring is Plan behavior. Save, commit, execution-choice, and reviewer-agent authority remain unresolved. |
| `cm-plan-and-spec-08` | `claimed` | `astra-plan` for plan-authoring behavior | `astra-implement` must reconcile, not inherit, execution/tracking semantics | Authoring and execution are inseparable in the source occurrence. Claim does not mean absorbed or retirement-ready. |
| `cm-plan-and-spec-09` | `retained independent` | retained `plan-tune` | none for Plan; explicit user-supplied preferences are ordinary input | Separate job, state, hooks, binaries, API effects, and privacy/consent authority. |
| `cm-plan-and-spec-10` | `retained independent` | retained `wayfinder` | candidate upstream evidence for `astra-spec`; current Spec draft is silent, so coordinator decision remains pending | It resolves decision fog and mutates a tracker. Plan accepts only the resulting accepted Spec, not live Wayfinder state. |
| `cm-plan-and-spec-11` | `claimed` | `astra-plan` for decomposition and draft projection | explicit external publisher after a separate user decision | Tracker/local publication remains unowned by Plan and blocks full source retirement. |

There is no proposed reference-ledger or cleanup-ledger insertion. These are
live collision occurrences with distinct delivery and effect semantics, not
mere references or junk. The inspected `codebase-design` guidance supplies the
document's architectural vocabulary but is neither a future runtime dependency
nor an occurrence in the assigned phase-0 reference ledger, so this design does
not invent a `consuming_designs` row for it.

### 3.5 Authority facts that must survive condensation

- A default file path in a source is not permission to write it.
- A requested implementation plan is not permission to execute it.
- A Plan approval is not permission for commits, worktrees, installs, network
  calls, tracker publication, or live-system effects unless the exact effect
  scope is separately accepted.
- Ticket breakdown approval is not ticket publication approval.
- An issue assignment is not implementation dispatch authority.
- A question preference is not approval of a one-way effect.
- A source's `allowed-tools`, plugin manifest capabilities, or hook registration
  is observed delivery metadata, not authority inherited by `astra-plan`.
- A plan revision after execution begins cannot silently rewrite the approved
  historical plan or Implement's progress state.

## 4. Collision analysis

### 4.1 Why the five entries looked duplicative

All five can appear near the word “plan.” Three can generate structured work
items, two use issue-like graphs, and two ask or remember user choices. At title
level they can look like competing plan makers.

The full bodies show four different jobs:

1. `writing-plans` authors code-rich execution instructions.
2. `planb` combines authoring with an execution and progress-control runtime.
3. `plan-tune` manages question and developer-profile state.
4. `wayfinder` resolves intent and decision fog through an issue map.
5. `to-tickets` projects accepted work into publishable tracker units.

Only the authoring slice of 1 and 2 and the pure decomposition slice of 5
belong in Plan.

### 4.2 Genuine shared behavior

The Plan-relevant sources share:

- a goal or accepted source artifact before decomposition;
- explicit phases, tasks, acceptance checks, and dependencies;
- work units small enough for review or a fresh execution context;
- verification or validation attached to work rather than left implicit;
- a user checkpoint before execution or publication;
- a need to expose assumptions, gaps, and sequencing rationale.

This common behavior supports one coherent module. It does not erase the
different output detail, state, and effect authorities.

### 4.3 Aliases and shallow delegation

The live `planb`, Wayfinder, and To Tickets Claude paths are registration
symlinks to the same inspected bodies. They are aliases, not extra source
occurrences or independent behavior. Plan Tune's generated live file and source
template are two delivery stages of one occurrence; the hooks and binaries are
non-skill components of that occurrence.

No assigned skill is merely a shallow delegation stub. `planb` does dispatch
agents during execution, but it also carries its own authoring, validation,
state, and failure protocol; calling it a delegator would lose behavior.
Writing Plans' reviewer prompt is auxiliary bundle material, not a second skill
or automatic agent. Wayfinder's research agents are optional behavior inside a
different decision-mapping job. These shapes remain explicit rather than being
counted as Plan perspectives.

### 4.4 Conflicts and defects that remain visible

| Tension | Design treatment |
|---|---|
| `writing-plans` demands exact paths, code snippets where useful, 2–5 minute actions, and frequent commits; `planb` says plans should be action-oriented without code examples and uses broader phases/tasks. | The canonical artifact contains exact implementation facts and never treats a commit suggestion as authorization. A pure `phase_summary` adapter may render the same artifact without code. The views cannot diverge. Task size is judged by reviewability, one outcome, and verification—not a rigid clock. |
| `writing-plans` main body asks for self-review without a subagent; its bundled reviewer prompt asks to dispatch a plan-document reviewer. | Core Plan uses deterministic self-review. No hidden reviewer is dispatched. Whether a separate Critique review is requested remains a user decision. |
| `planb` creates tasks, dispatches agents, updates checkboxes, executes validations, and adapts the plan. | Those are execution-state behaviors. Plan emits an immutable version and change policy; Implement owns progress, and the user mediates revision. |
| `to-tickets` omits fragile file-path/implementation detail while Implement needs exact paths and interfaces. | The canonical Plan remains exact. A ticket projection intentionally references canonical task IDs and stable outcomes rather than becoming the sole execution artifact. |
| `plan-tune` generated instructions declare a three-per-day distill cap, but the inspected binary says no rate cap. | The contradiction is recorded and excluded from Plan. No retirement or behavior claim is made. |
| `planb/examples.md` ends with `[395 more lines]`. | The example corpus is observably incomplete. It cannot support a fidelity or retirement claim. |

### 4.5 Apparent duplicates that are separate jobs

**Wayfinder versus Plan:** Wayfinder asks “which decision do we need to make?”
and maintains an issue graph while intent is unresolved. Plan asks “what exact
implementation work realizes this accepted decision?” If a Wayfinder map still
has blocking fog, there is no accepted Spec and Plan stops.

**Plan Tune versus Plan:** Plan Tune governs whether and how questions are
asked, with durable state, hooks, consent, telemetry, and optional external API
effects. Plan may receive a preference, but it must not become the preference
system.

**Tickets versus Plan:** a tracker is a delivery channel and coordination
system. A canonical Plan is an implementation contract. Ticket projection can
be internalized; publication remains an external effect.

**Plan versus Implement:** Plan describes and obtains separate approval for
work. Implement performs approved effects and owns progress evidence. A Plan
must never make itself “more executable” by crossing that seam.

### 4.6 Why one deep public module is plausible

The module's depth comes from hiding a substantial, coherent transformation
behind one operation:

```text
accepted intent + accepted technical evidence + test obligations
    -> validated implementation model
    -> dependency-safe, effect-explicit, verifiable tasks
    -> one canonical Plan plus lossless projections
```

Callers do not choose a source, manage its conflicting formats, reconcile
requirements with files and interfaces, or hand-construct a dependency and
verification graph. That is leverage. Locality is preserved because every
requirement, task, dependency, effect, stop, rollback, and verification claim
is represented once in the canonical artifact and rendered through adapters.

The module stays coherent because it stops at the approval/execution seam. It
does not absorb decision mapping, tuning state, runtime coordination, testing,
diagnosis, critique, or shipping.

### 4.7 Declared positive advantage

The candidate should beat the best single source on **cross-representation
implementation planning**: a change that simultaneously needs exact
paths/interfaces/actions, phase and dependency structure, verification and
effect authority, rollback/stops, and a lossless ticket projection—especially a
wide expand–migrate–contract refactor.

The advantage is not “more detail.” It is catching critical dependency,
interface, verification, effect, rollback, and handoff omissions while keeping
the plan in accepted scope and exposing conflicts between rich implementation
detail and fresh-context ticket delivery. That claim remains hypothetical until
section 9 passes.

## 5. Preserved distinctions

### 5.1 Exact implementation view versus no-code phase view

The canonical Plan is rich enough for Implement. `implementation_plan` renders
exact paths, interfaces, steps, and commands. `phase_summary` renders outcomes,
tasks, dependency/parallel structure, acceptance, and gates without code
fragments. The no-code view is useful for review but cannot replace canonical
facts or authorize work.

### 5.2 Static plan version versus execution state

Plan versions are immutable. Checkboxes, current phase/task, task summaries,
validation results, adaptations, skips, aborts, and auto-fixes are runtime
state. Plan may prescribe the fields Implement must report; it does not own or
update them.

If execution evidence requires a Plan change, the user chooses whether to stop,
request a new Plan version, return to Spec, or continue within an already
approved tolerance. A revision cites the superseded version and never rewrites
its history.

### 5.3 Canonical task versus tracer-ticket projection

A canonical task may reference exact paths and interface detail. A ticket draft
optimizes for a fresh context, one demoable vertical slice, decision rationale,
blocking edges, and stable links back to the Plan. The projection may omit
fragile detail only when it links to the canonical field; it may not invent,
merge, or drop acceptance and effect constraints.

Wide changes preserve `expand`, one or more independently verifiable `migrate`
batches, and `contract`. Contract cannot unblock until migration evidence and
compatibility gates pass.

### 5.4 Test strategy versus test execution

Plan records where a test belongs, the expected failing and passing evidence,
exact commands when known, and which peer or executor owns missing evidence.
Only Test constructs/runs the test and judges its evidence. A command copied
from Test is an obligation, not a passing result.

### 5.5 Architecture evidence versus architecture choice

Plan consumes an accepted module/interface/seam choice. It may detect that the
choice is incomplete for execution and stop. It does not invoke Architect,
promote Architect to a public peer, or choose a new architecture. Architect
remains a retained agent under `astra-understand-code`.

### 5.6 Planning preferences versus tuning state

Conciseness, view choice, or grouping preferences explicitly supplied by the
user can affect rendering. Durable preferences, never/always-ask rules,
one-way-door safeguards, profiles, logs, distillation, consent, and sync remain
inside `plan-tune`. Plan never silently queries or writes them.

### 5.7 Plan review versus Plan construction

Plan performs mechanical and semantic self-checks against its accepted inputs.
It does not judge the Plan with an independent critic voice. If Critique is
requested, the user supplies the Plan to `astra-critique` and may later return
one selected handoff. No automatic review loop exists.

### 5.8 Project artifact versus conversation result

Writing `docs/superpowers/plans/...`, `plans/.../plan.md`, or any other project
path is a project mutation. Core Plan returns the artifact in the conversation
and may suggest a destination. Saving it requires a separate, explicit manual
action with its own allowed path and overwrite policy.

## 6. Proposed skill design

### 6.1 Deep module and implementation outline

`astra-plan` is one public module with one operation. Its proposed internal
implementation contains:

1. **Intake validator** — validates Spec schema, separate acceptance records,
   blocking decisions, project snapshot, and optional evidence provenance.
2. **Evidence reconciler** — joins requirements to accepted code/interface/test
   evidence without converting gaps into assumptions.
3. **Implementation mapper** — builds the exact file, symbol, module,
   interface, seam, compatibility, and generated-contract map.
4. **Work decomposer** — creates one-outcome tasks and phased vertical slices;
   applies expand–migrate–contract where compatibility requires it.
5. **Dependency planner** — builds typed edges and proves or rejects proposed
   parallel work using shared files, interfaces, state, and evidence.
6. **Verification planner** — maps requirements and NFRs to test cycles,
   commands/reviews, expected results, and evidence owners.
7. **Effect and recovery planner** — records allowed/forbidden effects,
   authorization gates, stops, rollback procedures, and irreversibility.
8. **Handoff compiler** — emits the exact Implement intake and detects stale,
   missing, contradictory, or unauthorized fields.
9. **Projection adapters** — render implementation-plan, phase-summary, and
   ticket-draft views from one canonical artifact.
10. **Self-reviewer** — checks traceability, buildability, placeholders,
    consistency, unsupported authority, path/interface evidence, and projection
    loss without dispatching a peer or agent.

The internal modules are not public modes and should not become skills.

### 6.2 Information flow and stopping rules

```text
explicit user request
  -> accepted-Spec validation
      -> STOP: acceptance, scope, or blocking decision defect
  -> optional evidence validation
      -> STOP: exact planning would require an unsupported architecture/path
  -> canonical implementation model
  -> task + dependency + verification + effect + recovery graphs
      -> STOP: cycle, uncovered requirement, unauthorized effect, or no rollback decision
  -> handoff compilation
      -> STOP: Implement intake incomplete
  -> deterministic self-review
      -> STOP: placeholder, contradiction, orphan, or projection loss
  -> draft executable Plan
  -> separate user approval decision
      -> approved Plan artifact OR unchanged draft
```

The module degrades only by returning a blocked report or omitting an optional
projection. It does not degrade exact paths into guesses, approval into an
inference, or verification into “run tests.”

### 6.3 Real seams and adapters

**Accepted-artifact seam:** the public input interface separates Spec's
accepted intent from Plan's implementation transformation. The observed
downstream Implement design supplies a second side of the output seam. Both
contracts require coordinator reconciliation before implementation.

**Evidence seam:** repository/code, Understand, Test, and accepted Debug
evidence enter as immutable, attributed artifacts. This is not a peer-invocation
port.

**Projection interface:**

```text
render(canonical_plan) -> view
```

It has three justified adapters: implementation-plan Markdown, no-code phase
summary, and tracer-ticket draft. All three observed delivery shapes are
present in assigned sources. The interface has a losslessness test: every
omitted detail must remain reachable by stable canonical references, and no
adapter may invent authority or publish its result.

There is deliberately no issue-tracker adapter, agent-dispatch adapter, test
runner adapter, or plan-file writer adapter. One assigned source for each kind
does not justify making those effects part of the module, and the core has no
authority to use them.

### 6.4 Dependency categories

| Category | Proposed dependency | Treatment |
|---|---|---|
| In-process | schema validation, traceability graph, dependency graph, effect ledger, self-review, renderers | Candidate-owned implementation; deterministic and testable without originals. |
| Local but substitutable | read-only repository search, VCS snapshot inspection, language-aware symbol/interface lookup | Accessed through narrow read interfaces; absence yields a blocked exact-path claim, not a fabricated one. |
| Remote-owned | issue trackers, gbrain, Anthropic distillation API, remote agent/task systems | Not runtime dependencies of Plan. They remain only in explicit manual/external bridges. |
| True external | user acceptance, user effect authorization, repository bytes/revision, generated/protobuf/API contracts, installed build/test tools | Must be supplied or inspected with provenance. Plan cannot replace their authority. |

### 6.5 Invariants

- One accepted requirement maps to at least one task and verification
  obligation, or to an explicit non-code disposition.
- One task maps to accepted scope and a demonstrable outcome.
- One ordering constraint maps to a typed dependency edge and rationale.
- Parallel tasks share no unmediated file, interface, state, or evidence owner.
- Exact paths and interfaces cite the project snapshot or are marked unknown.
- Every effect is denied unless separately allowed; suggestions are not
  permissions.
- Every risky or irreversible task has a stop and recovery/escalation rule.
- No draft carries Plan approval; no Plan approval carries execution progress.
- Projections cannot introduce or lose normative facts.
- The module calls no peer and performs no project or external mutation.

### 6.6 Self-review protocol

Before returning a draft, the candidate checks:

1. accepted Spec completeness and version identity;
2. requirement, acceptance-example, risk, and NFR coverage;
3. exact file, symbol, interface, seam, compatibility, and generated-contract
   references against the named snapshot;
4. dependency cycles, false parallelism, and missing integration order;
5. concrete steps without placeholders, TODOs, ellipses, or hidden research;
6. verification working directories, prerequisites, expected results, and
   evidence owners;
7. all writes, network calls, installs, commits, tracker, and live effects in
   the effect ledger;
8. actionable stops, rollback limits, and user-owned decisions;
9. exact Implement handoff completeness;
10. zero inferred approval, zero execution/ticket/plan-file authority, zero
    peer invocation, and projection consistency.

Self-review repairs only representational defects within accepted scope. A
missing requirement, architecture decision, risk acceptance, or effect
authority becomes a blocked result.

## 7. Dependencies and delivery shape

### 7.1 Precise relations with all seven public peers

`R`, `I`, `H`, and `P` retain the roadmap meanings: roster reconciliation,
future information/capability flow, user-selected Critique problem handoff, and
provenance/external-behavior dependency. They do not imply peer invocation.

| Peer | R | I | H | P | Minimum information crossing the relation | Who starts | If unavailable | Prohibition |
|---|---|---|---|---|---|---|---|---|
| `astra-critique` | Yes: distinguish construction from judgment. | User may supply the draft/approved Plan to Critique; Plan consumes no Critique output except a selected H envelope. | Inbound only, after Critique emits its report and the user selects the Plan route. | Current common-envelope and Plan destination-profile design are provenance dependencies. | Common H envelope plus the compact payload in §7.2. | User alone starts Critique and selects zero or one returned route. | No H occurs; Plan may still self-review and return a draft, clearly uncritiqued. | No automatic review loop, critic dispatch, direct fix, or remedy authored by Critique. |
| `astra-understand-code` | Yes: locate/explain/design evidence precedes implementation planning. | Inbound optional accepted evidence: repository/revision, paths/symbols, accepted module/interface/seam choice, invariants, constraints, rejected alternatives, gaps. | None. | Inspected peer contract; retained Architect provenance remains under that peer. | The exact evidence fields listed at left, with user acceptance. | User supplies existing evidence or separately starts Understand. | Plan uses equivalent user-supplied evidence; if exact mapping needs missing evidence, it returns blocked rather than invoking Understand. | No invocation of Understand or Architect; no architecture choice by Plan. |
| `astra-spec` | Yes: Spec owns “what”; Plan owns executable “how.” | Inbound required accepted-Spec artifact in §2.4. | None. | Inspected Spec sources include a terminal writing-plans edge and an `sdd` Plan phase; reconciliation must prevent either from becoming implicit invocation. | Full field-aligned Accepted Specification: identity/revision/hash, lifecycle/approval, intent, scope/current state, behavior/criteria, decisions/technical constraints, evidence/uncertainty, readiness/acceptance map, and delivery facts. | User accepts Spec and separately starts Plan. | A supplied artifact passing §2.4 remains consumable if the Spec runtime is unavailable; without one, Plan blocks. Raw requirements or a Wayfinder map are never silently promoted. | No intent decision, requirement rewrite, scope waiver, or inferred acceptance. |
| `astra-implement` | Yes: Plan describes; Implement mutates and tracks progress. | Outbound only through the user: an approved Plan artifact and exact handoff in §2.6. | None. | Inspected current Implement design; final schema reconciliation remains pending. | Plan ID/version, Spec ref, approval, tasks/order/dependencies, effects/scope, acceptance, verification/Test refs, stops, rollback, baseline, gaps, user decisions. | User approves an exact Plan version and separately starts Implement. | The approved artifact is retained; no task executes and Plan does not substitute as executor. | No execution, task dispatch, progress update, commit, or automatic plan rewrite. |
| `astra-test` | Yes: Plan orders evidence obligations; Test owns construction/execution/judgment. | Inbound optional strategy/evidence; outbound through user as task seams, test artifacts, commands, prerequisites, and evidence gates. | None. | Inspected current Test design. | Accepted snapshot/behavior, modes/framework, artifacts/seams, exact commands with cwd/env/expected result, evidence state, gaps and cleanup. | User supplies evidence or separately starts Test. | Plan records a Test-owned gap; if methodology is needed to make the Plan exact, it blocks, otherwise it retains the unresolved evidence owner. | No Test invocation and no claim that a planned command passed. |
| `astra-debug` | Yes: a repair Plan can start only after diagnosis is owned elsewhere. | Inbound optional, user-accepted diagnosis for a repair-plan request. | None. | Debug peer contract is currently unavailable; payload is provisional. | Cause, evidence, affected contract, remediation constraint, diagnosis acceptance, unresolved uncertainty. | User accepts a diagnosis and separately starts repair planning. | Repair planning blocks when cause is a prerequisite; Plan does not diagnose from symptoms. | No diagnosis from symptoms and no Debug invocation. |
| `astra-ship` | Yes: approved Plan is upstream context, but Ship follows verified Implement output. | No required direct I edge. The canonical route is Plan → user → Implement → user → Ship; Ship may receive the Plan ref within Implement's handoff. | None. | Ship peer contract is currently unavailable. | No direct Plan payload is proposed beyond a Plan reference carried by Implement. | User starts Ship only after the required Implement/Test evidence exists. | Plan is unaffected; the later landing/publication/deployment workflow stops. | No commit, publish, release, deploy, or claim of ship readiness. |

### 7.2 Critique handoff acceptance

**Accepts Critique handoff: conditional.** The owned post-critique problem class
is `execution-plan-defect`; the conditions are explicit user selection, a valid
common envelope, and the compact destination-only payload below.

Critique owns the common envelope. Plan must not repeat its artifact, agenda,
problem statement, finding IDs/evidence, observed impact/affected scope,
constraints/open decisions, prerequisites, or context gaps inside the
destination payload.

The compact Plan-only destination payload is exactly:

```yaml
problem_class: execution-plan-defect
plan_lifecycle_state: draft-before-approval | approved-not-started | approved-in-progress
plan_dimension: intake | file-interface-map | decomposition | dependency-graph | verification | effect-authority | stop-rollback | implement-handoff | projection-fidelity
```

Acceptance rules:

1. Critique has already emitted its report with all candidate routes retained.
2. The user selected zero or one route and explicitly selected `astra-plan`.
3. The common envelope is present and the destination payload contains no
   remedy, new success criterion, implementation sequence, tool choice, or
   duplicated common-envelope evidence.
4. The envelope identifies an accepted Spec and the Plan version being
   questioned through its common artifact/context fields.
5. `approved-in-progress` never authorizes Plan to mutate the live plan or
   Implement state; Plan can only render a revision proposal and request a user
   decision.

Malformed or unselected handoffs stop with a compact reason. Plan neither
silently expands the payload nor asks Critique to repair it.

### 7.3 Retained Architect and source coordination

Architect remains a retained agent beneath `astra-understand-code`. Plan may
consume a user-approved blueprint only through the Understand evidence seam.
The blueprint's authorship, revision, accepted constraints, and known gaps must
remain visible. Plan never invokes, supervises, or claims Architect.

The assigned source originals also are not runtime dependencies of the future
candidate. During phase-0 validation they form comparison systems. A future
candidate must work self-contained once inputs are supplied; otherwise it is a
convener rather than a condensed module.

### 7.4 Deferred general-purpose concerns

Context, Guard, Delegate, Automate, Incident, and Deploy are not peers or
absorbed modules. Their honest treatments are:

- context: explicit accepted artifacts, snapshot, provenance, and gaps in the
  Plan input;
- guard: effect policy, stops, rollback, and separate user authorization;
- delegate/automate: execution choices recorded for the user and Implement,
  never performed by Plan;
- incident: accepted Debug evidence or an external incident record, never a
  Plan-owned diagnosis;
- deploy: an external/Ship-owned effect appearing in Plan only as forbidden or
  separately authorized downstream scope.

## 8. Manual bridge

The bridge exists because phase 0 has no implemented `astra-plan`. These are
manual, source-native invocations with outer authority envelopes. They are not
claims that the source natively enforces every restriction.

### 8.1 Code-rich draft through writing-plans

```text
/superpowers:writing-plans

Use the attached explicitly accepted Spec and accepted read-only code evidence.
Return the complete plan draft in this conversation only. Do not write or edit
files, commit, dispatch a reviewer or implementer, execute, test, create tasks,
or choose an execution workflow. Mark unsupported paths/interfaces as blocking
gaps. Treat every commit suggestion as non-authorizing. Stop after self-review
and the draft; ask separately for Plan approval.
```

This best approximates exact path/action/test detail, but it does not supply the
canonical effect ledger, dependency typing, or ticket-projection guarantees
without explicit manual normalization.

### 8.2 Phase/dependency draft through planb

```text
/planb

Planning-only containment. Confirm the accepted goal, then return a phase/task
draft with acceptance criteria, dependencies, parallel-safety rationale, and
validation obligations in this conversation. Do not create or edit a plan
file, create Claude tasks, dispatch agents, execute a task, run validation,
update progress, call advisors, skip/abort/auto-fix, or adapt runtime state.
Stop before execution setup and request Plan approval separately.
```

Because `planb` is a mixed author-and-execute source, any sign that it cannot
honor the containment is a stop, not permission to proceed.

### 8.3 Draft ticket projection through to-tickets

```text
/to-tickets <approved-plan-artifact>

Draft-only projection. Use the exact approved Plan version and return numbered
tracer-ticket drafts and blocking edges in this conversation. Preserve Plan
task IDs, acceptance, effect constraints, and expand–migrate–contract order.
Stop after the breakdown review and before publication. Do not write .scratch
files or create/update/label/assign/link/close any tracker issue. Ticket
breakdown approval is not publication approval.
```

If the user later wants publication, they must explicitly invoke the source
again or use a tracker workflow, name the destination, approve the exact
effects and overwrite/duplicate policy, and accept that this is outside Plan.

### 8.4 Separate retained-source bridges

If intent is unresolved, use `/wayfinder` explicitly before Spec acceptance;
its issue effects and agents require their own user authorization. Return the
closed, user-approved decisions to Spec, not directly to Plan as new intent.

Use `/plan-tune` only for question-preference/profile work. It is never a Plan
prerequisite, and Plan should not read its local state implicitly.

If an Architect blueprint is needed, the user routes the request through
`astra-understand-code`'s current manual/retained-Agent path, approves the
result, and supplies it to Plan. Plan does not launch Architect.

### 8.5 What the manual bridge cannot prove

The bridge cannot prove self-containment, exact cross-source normalization,
lossless projections, zero hidden writes, authority compliance, lower cost, or
positive advantage. It also cannot make the mixed originals retirement-safe.
Those are section-9 validation questions.

## 9. Deferred implementation and validation

No test, benchmark, source retirement, installation, or candidate generation is
performed in phase 0.

### 9.1 Three comparison systems

1. **Source oracle:** choose the best single relevant source for each prompt:
   `writing-plans` for exact implementation detail, planb's authoring slice for
   phased/dependency structure, or `to-tickets` for pure decomposition. Retained
   `wayfinder` and `plan-tune` are not forced into Plan prompts. Selection is
   fixed before any system output is seen.
2. **Reference convener:** coordinate unchanged originals under draft-only
   containment, then manually reconcile their outputs into the proposed
   canonical schema. It must log every source call, contradiction, omitted
   field, manual decision, and attempted effect.
3. **Self-contained candidate:** use only the accepted artifacts and its own
   implementation. It may not read or invoke the originals, their prompts,
   planb runtime, tracker publishers, Plan Tune state, or retained agents.

The same accepted inputs, project snapshot, effect policy, time budget, and
output schema apply to all three systems.

### 9.2 Fixed corpus

**Home cases**

1. A small multi-file feature with an accepted Spec, exact code snapshot,
   generated interface, test-first requirement, and no external effects.
2. A phased feature whose tasks have real dependency and parallel-safety
   constraints, plus acceptance criteria of automated, tool, and human-review
   kinds.
3. An approved change needing fresh-context tracer tickets but no tracker
   publication.
4. A wide refactor requiring expand–migrate batches–contract, compatibility
   gates, rollback, and cross-interface verification.

**Positive-advantage cases**

5. A cross-cutting feature spanning exact code paths, module interfaces,
   dependency-safe parallel tasks, red/green commands, reversible and
   irreversible effects, and an Implement handoff.
6. A wide migration where the best single source either loses implementation
   precision or loses the ticket-level delivery shape.

**Divergence cases**

7. Code-rich instructions versus a requested no-code summary.
8. Source-recommended frequent commits with `commit_policy: forbidden`.
9. A planb-style request to update checkboxes or auto-fix during execution.
10. A ticket request whose stable outcome conflicts with a fragile file-path
    detail.
11. A bundled reviewer-agent suggestion where the user authorized no agents.

**Convergence/control cases**

12. A trivial, single-file accepted change with one verification command where
    all systems should produce essentially the same plan.

**Prerequisite and failure cases**

13. Missing or non-accepted Spec; Spec approval reused as Plan approval.
14. Blocking open decision or unwaived assumption.
15. Repository/revision unavailable, dirty-state conflict, stale path, or
    generated contract not inspected.
16. Missing architecture decision needed to name an interface or seam.
17. Missing Test strategy where the Spec requires a framework-specific gate.
18. Dependency cycle or false parallelism through a shared file/interface.
19. Tracker unavailable or publication unauthorized; this may block only the
    external publisher, never the pure Plan or ticket draft.
20. Critique H payload that repeats common-envelope fields or prescribes a fix.

### 9.3 Measures

Run paired comparisons on identical immutable artifacts. Use at least three
trials for nondeterministic systems; randomize system and output order; blind
reviewers to system/source identity; keep prompts, budgets, tools, project
snapshot, and effect policy fixed; and adjudicate disagreements without showing
the expected source answer first.

For each system, capture:

- critical recall and precision for requirements, exact tasks, paths, module
  interfaces, seams, dependencies, acceptance, verification, effects, stops,
  rollback, and handoff fields;
- supported-claim precision, unsupported-claim rate, and source-unique supported
  findings or planning moves retained;
- orphan requirement/task/verification counts;
- unsupported path, command, architecture, risk, or approval assumptions;
- dependency-cycle and false-parallelism defects;
- buildability by a fresh implementer without asking a hidden design question;
- scope expansion, duplicate work, and representational noise;
- routing accuracy when choosing a source oracle, stopping for Spec/Understand/
  Test/Debug evidence, or identifying a separate publisher/execution job;
- command validity: working directory, prerequisites, expected result, and
  failure interpretation;
- projection fidelity and expand–migrate–contract ordering;
- user correction count and severity-weighted critical omissions;
- zero inferred Plan approval, project writes, plan-file writes, issue effects,
  peer/agent invocations, execution, commits, and live effects;
- latency, token/tool cost, source calls, and manual reconciliation time.

Evaluation requires blinded human review plus deterministic schema,
traceability, graph, placeholder, effect, and projection checks. Source names
are hidden from reviewers. A critical omission includes a scope escape,
unapproved effect, missing compatibility gate, unsafe parallel edge, false
verification claim, missing stop/rollback for irreversible work, or unusable
Implement handoff.

### 9.4 Gates and failure consequences

**Characterization gate:** every preserved source behavior, delivery shape,
authority, prerequisite, failure, state, agent, hook, command, and external
effect has an observed test or an explicit approved exclusion.

**Home non-regression gate:** the candidate is no worse than the source oracle
on every home case and has no new critical omission.

**Positive-advantage gate:** on both advantage cases, the candidate has a
materially lower severity-weighted critical-omission rate than the best single
source, while staying within agreed latency/cost and scope-expansion thresholds.
“Looks more complete” is not enough.

**Coordination gate:** the reference convener must preserve source-unique
behavior and informative disagreements while honoring the common authority
contract. If it cannot reconcile the sources without scope expansion or hidden
effects, reject or narrow the combined architecture.

**Internalization-fidelity gate:** the self-contained candidate matches or
beats the reference convener's correctness, source-unique supported planning
moves, delivery fidelity, and authority behavior without hidden source
dependence or manual normalization. A convener win followed by a candidate loss
blocks internalization and every retirement claim, even if final task titles
look similar. Any missing behavior requires explicit user-approved deletion.

**Authority gate:** across the full corpus, counts for inferred approval,
project/external mutation, source/peer/agent invocation, execution, publication,
commit, and live effect are all zero.

**Interface gate:** Spec input and Implement output schemas reconcile with those
peer designs; Test/Understand evidence remains optional and user-mediated;
Critique's common envelope is not repeated.

**Self-containment gate:** originals can be removed from the test environment
without changing candidate behavior. Source prompt leakage is checked.

**Retirement gate:** characterization, home non-regression, positive advantage,
coordination, internalization fidelity, authority, interface, self-containment, immutable
provenance, rollback, and explicit user approval all pass for each occurrence.

Failure keeps the original installed and the ledger occurrence unresolved. A
single critical authority violation fails the candidate regardless of average
quality. No partial authoring success permits retirement of a mixed source's
execution or publisher behavior.

Gate-specific consequences are not interchangeable:

- failed characterization expands the evidence/corpus and blocks a fidelity
  claim;
- failed home non-regression rejects the candidate for that jurisdiction or
  narrows the proposed merger;
- failed positive advantage removes the claimed reason to merge and defaults to
  retaining/routing the strongest applicable source behavior;
- failed coordination rejects or narrows the combined architecture;
- failed internalization fidelity leaves, at most, a validation convener and
  blocks self-contained implementation and retirement;
- failed authority, interface, or self-containment blocks candidate release;
- failed source-specific retirement keeps that occurrence installed even if
  the candidate is useful elsewhere.

### 9.5 Source-specific retirement gates

**`superpowers:writing-plans`:** preserve scope validation, exact file/interface
map, concrete steps, useful disambiguating code, test-first/verification detail,
expected results, and placeholder/type self-review. Resolve the main-body versus
reviewer-prompt contradiction. Saving, commits, execution choices, and review
dispatch need an explicitly authorized owner or approved deletion.

**`planb`:** preserve goal confirmation, phase/task/acceptance structure,
dependency and parallel safety, validation kinds, concise no-code view, and
adaptation schema. Separately characterize plan-file writes, Claude task shapes,
agents, execution, progress tracking, phase reviews, advisors, skip/abort,
auto-fix, and adaptation. Recover or explicitly accept the truncated example.

**`plan-tune`:** outside Plan retirement scope. Any later design must preserve
question preference semantics, one-way-door safeguards, logs, profile model,
consent, hooks, binaries, distillation/API behavior, gbrain/sync, privacy, and
failure behavior, and resolve the observed rate-cap contradiction.

**`wayfinder`:** outside Plan retirement scope. Any later design must preserve
root map and decision-ticket schema, native blocking, labels, claims,
assignments, issue effects, research/prototype/grilling/agent shapes, fallback
delivery, and one-ticket-per-session behavior.

**`to-tickets`:** preserve tracer vertical slices, fresh-context/demoable
criteria, prefactoring, wide-refactor expansion/migration/contraction,
dependency edges, and user breakdown review. Full retirement additionally
requires a separately authorized, tested replacement for local and real-tracker
publication, or explicit user approval to delete those delivery shapes.

## 10. Provenance and open questions

### 10.1 Inspection summary

The following were read completely for this design:

- repository authorities `docs/design-requirements.md` and `docs/phase-0.md`;
- Plan/spec and R/I/H/P sections of `docs/design-roadmap.md`, including the
  fixed roster, Plan map, Critique route, allocation, and Architect retention;
- assigned collision-ledger rows in `docs/phase-0-ledgers.md`;
- full `designs/astra-understand-code.md` and `designs/astra-test.md`;
- the newly available `designs/astra-spec.md` Plan-facing artifact contract,
  accepted-intent distinction, relation row, and open contract questions from
  snapshot SHA-256
  `6ec61e19ec2af793a2bece1ccc1402b4d9190c822f329aa938be0e218b5163c6`;
- Plan-facing intake/handoff/effect sections of `designs/astra-implement.md` and
  Critique's common-envelope/Plan-route sections of
  `designs/astra-critique.md`;
- full `codebase-design/SKILL.md` and `DEEPENING.md`;
- every assigned source body and the directly relevant body-linked references,
  manifests, metadata, symlink/marketplace or hook registration, and stateful
  binaries listed in §3.1 and §10.2.

Peer-design snapshot hashes at inspection were: Spec
`6ec61e19ec2af793a2bece1ccc1402b4d9190c822f329aa938be0e218b5163c6`,
Understand Code
`152143af484c843dfa180ed5184914cea0295ce48e33b574edf2074eef719cda`,
Test `59525a1de2ee699585d4fd93e15baaf86bff61506c2d3381a4cc9feed26b7a5f`,
Implement
`2aac0600c1547e2fb4b812f8aff44bc43c4a4d54ece96715e55e4a88a5cff6ee`,
and Critique
`2fc22bad57b18a97668fa76d7c387728dcac8a423119d1c7f1191e09b6031f7d`.
They are mutable peer proposals, not immutable source occurrences; a hash change
requires relation reconciliation before implementation.

No current source was invoked. Inspection was read-only. No unavailable peer
contract or uninspected shared runtime is represented as observed behavior.

### 10.2 Immutable source-artifact index

| Source | Immutable inspected anchor | SHA-256 or revision | Certainty |
|---|---|---|---|
| `writing-plans` | cached Superpowers 6.2.0 `skills/writing-plans/SKILL.md` | `72190c88b2b5a67a96b91d66aa72b9161913e10e8769da3f28a226f4cc7b99d0` | O |
| `writing-plans` | `plan-document-reviewer-prompt.md` | `aa728b96aad603c8be28875a4305637f6c984aa81ffcadcb13e743202fa2a0c7` | O |
| `writing-plans` | `agents/openai.yaml` | `de6a2f3d9de78d9c5027512ab1abab998f9acbef70960ecdbad525f4dce2e1bb` | O |
| `writing-plans` | Codex plugin manifest | `b271065c5e906e73757b7f9c26f7c57bb662ee47a31ed479dc32fb253729a25c` | O |
| `writing-plans` | installed plugin registry | Superpowers `6.2.0`, git commit `eafe962b18f6c5dc70fb7c8cc7e83e61f4cdde06`; installed `2026-03-31`, updated `2026-07-27` | O |
| `planb` | symlink target `monster-prompt/claude/skills/planb/SKILL.md` | `41cb523aee7a7f513eacc28fe14f19088ae763edd97468e0505313bc2ea344b8`; repository revision `6abccfa5f83a82f2bff309228b956323a11e4d2a` | O |
| `planb` | `examples.md` | `25dd7f9cba311472eb77649be48f769e30c3f2468326042dc581106523fc1e2f` | O |
| `planb` | `references/format.md` | `c30d85e2f9b09d09b7377ccb35e992fc28fbad8bdc71b74ac5d57a9e3548db96` | O |
| `planb` | `references/parallel-execution.md` | `3e4fd4c5122cca1f851cf3856807ad55a3e34ae602a154ae933d0aaaa22c72d3` | O |
| `planb` | `references/task-tracking.md` | `7865d2f945e8144a24aa45097385425f907b3262bd095e9cb75066e57a0087a5` | O |
| `planb` | source `.claude-plugin/marketplace.json` (observed not to register Plan B) | `8992866835bd21e2e213de359b51e29885f6217236a425f020a1e1acd7921780` | O |
| `plan-tune` | generated Gstack 1.60.1.0 `plan-tune/SKILL.md` | `2e6ed969370e9a31a017d97644658ce1e5906bbb6023e5a37ce0af08b6b5e3cb`; source repository revision `a3259400a366593e0c909dd9ac3e59752efd2488` | O |
| `plan-tune` | source `SKILL.md.tmpl` and Gstack `VERSION` | `54551fbd340c25db44a3eead7f93a865a714f94da9e944198224aef941a3b588`; version-file hash `a05442e1220521c44bac111462a2a311da807c141cbefba49249f2e8599f44bb` | O |
| `plan-tune` | registered question-preference, question-log, and AUQ-error-fallback hook shims | `608d228537f83074eb9ef7a9d64052cd43fd01623d08c04450b9815f2b4bbd75`; `a8dae5b30d44cf599e893eb052784a9d78681359f9b0635ca4f5bf823d6b23e2`; `fce153204a040294b4f9877a04a187b626ff625ae12737f8c07888f68473e727` | O |
| `plan-tune` | Claude settings registration snapshot | `0e553d6e5eb95b9fc5b63b5f65e15d22bbfef538558e3bb66eea6c6ce27eed1a` | O |
| `plan-tune` | `gstack-question-preference` | `fd3ea37045fb0e049bdf98871e3795a29707f9b7eb8edc3bf09802d8ae87a621` | O |
| `plan-tune` | `gstack-question-log` | `2555dd32376118ddedc98bd9d75d5594411c6643d00c787b58fb89188715261c` | O |
| `plan-tune` | `gstack-developer-profile` | `2529dcd929c6248fd756846b3b61e66b622fb3b6ce22addd8791fd29f6f186ca` | O |
| `plan-tune` | `gstack-distill-free-text` | `5d5188aa855037d9a66c86b33c42c5e75dc89a642f6dc13ed0b9413e66b0b451` | O |
| `plan-tune` | `gstack-distill-apply` | `de27ef9805c4e244f7d0b9932710752932d8bf4e7b5d1849a630c324983b811b` | O |
| `wayfinder` | cross-agent `SKILL.md` | `257e40665b28ae959ffdcb97d7a72b074360f4a3d201bd84786505308546e434` | O |
| `wayfinder` | `agents/openai.yaml` | `88bc81a11a6d52ac67aeaa76b8b619e387020d47c5133a4dd4927fd15c4ad073` | O |
| `to-tickets` | cross-agent `SKILL.md` | `5ecdf1d4df8a360ed39df21a2347f97ba177afd449a577da4f6b6ea8e1ebb808` | O |
| `to-tickets` | `agents/openai.yaml` | `21bc6215fffcd7614e9f772bb1760e87cc5fc7dcc707e7d282bc9414267a6090` | O |

Hashes identify inspected bytes, not trust or future availability. The
cross-agent Wayfinder and To Tickets directories exposed no repository revision
in the inspected registration, so their byte hashes are the current immutable
anchors. Plan Tune depends on additional shared Gstack implementation not
claimed as absorbed; only the directly relevant registered shims and binaries
were used to establish its separate-job/state/effect disposition.

### 10.3 Provisional decisions

- One deep `astra-plan` module owns accepted-Spec-to-executable-Plan
  transformation and pure projections. **I**
- `writing-plans`, planb's authoring slice, and `to-tickets`' pure decomposition
  are proposed inputs to the design, not runtime dependencies. **I**
- `plan-tune` and `wayfinder` remain independent. **I**, grounded in observed
  distinct jobs/effects.
- Plan emits conversation artifacts only; all project-file and tracker writes
  remain separately authorized manual/external effects. **I**
- Plan consumes accepted Understand/Test/Debug evidence without invoking peers;
  Architect remains under Understand. **I**
- The canonical artifact is code-rich and exact; no-code phase and ticket views
  are lossless projections. **I**
- Critique supplies only a user-selected problem handoff; it does not enter an
  automatic repair loop. **I**

### 10.4 Open authority and design questions

1. **Spec reconciliation — blocking before implementation:** the current Spec
   and Plan drafts now share the complete field set and ten-part non-inference
   gate. The coordinator must still fix the concrete `schema_version`, canonical
   hash serialization, which nonblocking questions may survive acceptance, and
   how `readiness.required_plan_inputs` binds a later repository snapshot. Until
   those choices are reconciled, the contract remains **I**, not implemented.
   The Spec row's shorthand that Plan “owns planning approval” must also be
   normalized to mean that Plan carries and presents the gate; only the user
   owns the approval decision.
2. **Implement reconciliation — blocking before implementation:** will
   `astra-implement` accept the exact Plan schema and immutable-version rule,
   and which fields belong in its own progress state rather than the Plan? **U**
3. **Plan-file authority:** should a later non-core adapter be allowed to save a
   Plan after a second explicit user authorization, or must saving always remain
   external? Core Plan has no write authority either way. **U**
4. **Commit representation:** should `checkpoint_policy` remain advisory, or be
   removed entirely to avoid confusing source commit suggestions with
   execution authority? **U**
5. **Plan detail policy:** when exact code is safely derivable, is it normative
   Plan content or only a disambiguating example? Validation must compare both
   fidelity and staleness. **U**
6. **Mixed planb ownership:** which future module owns planb's task creation,
   agents, progress, phase reviews, advisors, and live adaptation, and is any of
   it appropriate for `astra-implement`? Claiming the authoring slice does not
   answer this. **U**
7. **Ticket publisher ownership:** what explicit adapter or external workflow
   preserves local and real-tracker publication, native blocking, labels, and
   duplicate handling? It cannot be Plan core. **U**
8. **Wayfinder-to-Spec relation:** may Spec accept a closed Wayfinder map as
   evidence, and what proves the decisions—not merely tickets—were accepted?
   **U**
9. **Debug repair input:** what exact accepted diagnosis artifact will the
   future Debug design expose? The current proposal is provisional. **U**
10. **Ship trace:** should Ship receive a Plan reference only through
    Implement, or will it define a direct informational relation without making
    Plan a ship-readiness authority? **U**
11. **Plan Tune inconsistency:** is distillation actually rate-capped, and which
    generated/source/runtime authority wins? This does not block Plan but blocks
    any Plan Tune retirement claim. **U**
12. **Reviewer contradiction:** is the writing-plans reviewer prompt normative,
    optional bundle support, or stale? No Plan implementation may infer agent
    authority while this remains unresolved. **U**
13. **Truncated planb example:** are the omitted example bytes recoverable, or
    should the source be characterized from the observed partial artifact? **U**
14. **Projection loss threshold:** which omissions are allowed in phase-summary
    and ticket views while remaining lossless through canonical references?
    This needs corpus evidence. **U**

### 10.5 Coordinator reconciliation required

Before any implementation work, the coordinator must reconcile:

- all five proposed ledger dispositions and secondary roles;
- the accepted-Spec input with `astra-spec`;
- the executable-Plan output and progress-state seam with `astra-implement`;
- Test, Understand, Debug, Critique, and Ship information relations;
- mixed planb execution ownership and To Tickets publisher ownership;
- the zero-write core authority and any future explicitly authorized saving
  adapter;
- source-specific characterization and retirement gates.

Until then, this document is an evidence-backed architectural hypothesis, not a
replacement instruction.
