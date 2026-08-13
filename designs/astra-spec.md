# Astra Spec — phase-0 design

**Date:** 2026-08-03 · **Authoritative drafting-tranche position:** 3 of 8 ·
**Status:** `proposed`

**Six-skill reconciliation:** 2026-08-11 · surviving public home for solution selection and the
complete approved change contract; `astra-plan` is superseded historical evidence

> **Authority.** `docs/design-requirements.md` is the sole per-skill design contract;
> `docs/phase-0.md` owns phase scope and coordinator authority; the current user instruction fixes
> the public drafting tranche and its order. This document proposes one design. It does not
> implement a skill, edit either global ledger, install or remove a source, file an issue, create a
> design document outside this file, invoke another workflow, or authorize retirement.
>
> **Certainty.** **O** = observed directly in an inspected body, registration, or bundle; **I** =
> inferred or proposed and still requiring reconciliation or later comparison; **U** = unavailable.
> Proposed Astra behavior is never presented as observed runtime behavior.
>
> **Conformance.** Sections 1–10 map one-to-one and in order onto
> `docs/design-requirements.md` sections 7.1–7.10. Section 11 applies the six-skill contract in
> requirements section 7.11 and has normative precedence over conflicting pre-reconciliation
> wording. Every assigned body and its directly relevant registration or bundle was inspected in
> full. All originals remain installed.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-spec` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhood | Plan & spec: `cm-plan-and-spec-01`, `05`, `06`, and `07` |
| User job | **When I have vague, partial, revised, or finding-backed intent, I want one approved change specification that selects the solution and defines every required outcome, without repository delivery planning or mutation.** |
| Accepts Critique handoff | **yes** — for `specification-gap-or-ambiguity` and any user-selected in-scope finding requiring a change contract; section 11 governs the reconciled intake |
| Six-skill role | Absorbs Plan's solution-facing authority; exact repository delivery planning transfers to `astra-implement` |

The reconciled outcome is one **Approved Change Specification**, or an honestly non-approved
draft with fielded blockers. Clarification, evidence grounding, solution alternatives, selected
direction, semantic ordering, staged decisions, acceptance criteria, conditional branches,
revision, and optional artifact delivery are behaviors that lead to that outcome. They do not
turn Spec into a repository delivery planner, project mutator, reviewer, tester, publisher, or
workflow dispatcher.

**Personal value is explicit.** The user selected `astra-spec` as the third peer in this exact
public tranche: `astra-critique`, `astra-understand-code`, `astra-spec`, `astra-plan`,
`astra-implement`, `astra-test`, `astra-debug`, and `astra-ship`. That direct selection establishes
`now` priority for the design. The user also requires approval state to remain machine-visible so
Plan cannot infer acceptance from a document's existence, tone, issue label, or prior conversation.

The tranche is flat. No peer invokes another implicitly. Context, Guard, Delegate, Automate,
Incident, and Deploy remain deferred general-purpose concerns and appear only as manual or external
bridges in sections 7 and 8. They are not public peers, internal modules, or absorbed capabilities.

One label-based assignment does not survive source inspection unchanged: `sdd` is a workflow-state
navigator, not a specification author. This design proposes that it remain an independently
invocable reference. Its useful persistent-spec and backward-flow principles inform revision mode,
but its command routing, installation, initialization, checklist mutation, and delivery advice do
not enter the Spec interface.

---

## 2. Interface and scope

### 2.1 Requests that should trigger it

- “Turn this idea into an accepted specification.”
- “Help me work out what this feature should do before we plan it.”
- “Clarify the actors, outcomes, boundaries, edge behavior, and acceptance criteria.”
- “Synthesize the decisions in this conversation into a spec,” when enough evidence already exists.
- “Revise the accepted spec because production evidence exposed a requirements gap.”
- “Make these requirements observable and testable without choosing the implementation sequence.”
- “Prepare a backlog-ready intent artifact,” with any issue or design-document delivery treated as a
  separately authorized effect.
- A user-selected Critique handoff whose problem class and compact payload pass section 7.3.

### 2.2 Nearby requests that should not trigger it

| Request | Owner or current bridge | Why Spec stops |
|---|---|---|
| “Explain what this code currently does” | `astra-understand-code` | Existing behavior is evidence for intent, not intent authority |
| “Attack this spec or compare independent reviewer judgments” | `astra-critique` | Review and adversarial judgment are separate from authorship |
| “Turn the approved change spec into exact repository work” | `astra-implement` | Files, symbols, task graph, commands, rollback procedures, agents, worktrees, and commit/PR boundaries belong downstream |
| “Change the project” | `astra-implement` | Source, configuration, migration, and production mutation are forbidden here |
| “Build or run the proof” | `astra-test` | Spec defines accepted behavior; Test creates and executes evidence |
| “Find the cause of this failure” | `astra-critique diagnose` | Causal judgment may inform remediation mode, but Spec does not run a causal investigation |
| “Commit, push, file a PR, merge, release, or deploy” | `astra-ship` for VCS/publication; Deploy stays external | Acceptance conveys no publication or deployment authority |
| “Tell me the next speckit command” | retained `/sdd` reference | Workflow navigation is a separate user job and may carry source-specific effects |
| “Dispatch an agent to implement this” | explicit external Delegate bridge | Specification acceptance is not dispatch authority |

### 2.3 Conceptual input

One invocation accepts a bounded **Specification Context** with these caller-visible facts:

1. `intent_input`: the user's request, conversation, Critique capsule, or revision request;
2. `evidence_inputs`: optional referenced artifacts from Understand Code, Test, Debug, stakeholder
   material, existing product behavior, contracts, ADRs, or prior specification revisions;
3. `authority_context`: who may decide intent, scope, acceptance criteria, and final acceptance;
4. `artifact_context`: repository, product, API, feature, issue, or other bounded subject;
5. `requested_mode`: `discover`, `synthesize`, `remediate`, or `revise`, or permission to
   recommend one;
6. `effect_authority`: explicit allow/deny values for local-document delivery, issue delivery,
   external review, browser/visual delivery, and any other persistent or remote effect; and
7. `constraints`: user-supplied time, compatibility, regulatory, policy, language, accessibility,
   or other product constraints.

Missing evidence is not silently converted into intent. Missing intent is not inferred from current
code. Missing authority is a blocker for acceptance, even when a plausible draft can be produced.

### 2.4 Small public interface and result

The future module exposes one conceptual operation:

```text
specify(Specification Context) -> Specification Result
```

`Specification Result` is either:

- an **Accepted Specification**, whose approval invariants below all hold;
- a `draft` or `changes_requested` specification with explicit unresolved decisions; or
- a `blocked` result naming the missing authority, evidence, or prerequisite.

The invocation and the fielded artifact contract in section 2.5 are the module's external
interface. Question pacing, evidence reconciliation, alternative generation, section rendering,
schema checking, issue formatting, and visual presentation stay behind internal seams. The module
is deep because those behaviors provide substantial leverage while the caller sees one operation
and one artifact family.

### 2.5 Accepted Specification artifact, field for field

The artifact is conceptual in phase 0, but its fields are not optional prose conventions. A later
candidate must serialize an equivalent contract and validate the same invariants. Unless a row says
otherwise, a field is required; an empty collection is represented as `[]`, not omitted.

#### 2.5.1 Identity, lifecycle, and approval

| Field path | Type / allowed values | Meaning and invariant |
|---|---|---|
| `schema_version` | non-empty string | Version of this artifact contract |
| `spec_id` | stable non-empty string | Identity shared by all revisions of one specification |
| `revision` | positive integer | Increments whenever accepted meaning or acceptance criteria change |
| `content_hash` | digest string over canonical meaning-bearing fields | Binds approval and downstream use to exact intent/scope/behavior/constraint/decision/evidence/readiness values. Canonicalization excludes `content_hash`, `approval`, `delivery`, lifecycle state/timestamps, and other mutable bookkeeping, which are validated separately |
| `title` | non-empty string | User-recognizable subject, not an implementation task title |
| `subject_ref` | string or `null` | Repository, product, API, issue, or prior-art reference; `null` is explicit |
| `supersedes_revision` | integer or `null` | Immediately superseded revision; cannot equal `revision` |
| `revision_reason` | non-empty string | Why this revision exists, including production-feedback or Critique origin |
| `lifecycle.state` | `draft`, `reviewing`, `accepted`, `changes_requested`, `rejected`, `superseded`, `blocked` | Explicit artifact state; only `accepted` is Plan-consumable |
| `lifecycle.created_at` | timestamp | Artifact creation time |
| `lifecycle.updated_at` | timestamp | Time these exact bytes or equivalent field values were produced |
| `approval.state` | `not_requested`, `pending`, `accepted`, `changes_requested`, `rejected`, `superseded` | Explicit user-owned decision state; never inferred |
| `approval.decider` | user/stakeholder identity or `null` | The authority who actually decided; an agent is not valid acceptance authority |
| `approval.approved_revision` | integer or `null` | Must equal `revision` when `approval.state = accepted`; otherwise `null` |
| `approval.approved_content_hash` | digest string or `null` | Must equal `content_hash` when accepted; prevents same-revision field drift |
| `approval.decided_at` | timestamp or `null` | When the explicit decision occurred |
| `approval.decision_ref` | conversation/event reference or `null` | Traceable evidence of the explicit decision, not a paraphrased tone judgment |
| `approval.authority_scope` | non-empty list drawn from `intent`, `scope`, `requirements`, `acceptance`, `whole_revision` | Must contain `whole_revision` plus every meaning-bearing area changed in this revision |
| `approval.section_decisions` | list of `{section_id, state, decider, decision_ref}` where `state` is `accepted`, `changes_requested`, or `rejected` | Staged approvals; useful evidence but not a substitute for whole-revision acceptance |

#### 2.5.2 Intent and product outcomes

| Field path | Type | Meaning |
|---|---|---|
| `intent.problem` | non-empty string | User or stakeholder problem in outcome language |
| `intent.affected_actors` | list of `{actor_id, description}` | People or systems whose behavior or outcome changes |
| `intent.desired_outcomes` | list of `{outcome_id, actor_ids, statement}` | What becomes true for those actors |
| `intent.why_now` | string or `null` | Timing rationale; explicit `null` is allowed |
| `intent.success_measures` | list of `{measure_id, outcome_ids, observable, target, observation_window}` | Product-level success, distinct from implementation telemetry selection |
| `intent.non_goals` | list of strings | Outcomes this specification intentionally does not pursue |

#### 2.5.3 Scope, assumptions, and evidence-backed current state

| Field path | Type | Meaning |
|---|---|---|
| `scope.in_scope` | list of `{scope_id, statement, rationale}` | Included behavior or user-visible area |
| `scope.out_of_scope` | list of `{scope_id, statement, rationale}` | Explicit exclusion, not an implied omission |
| `scope.constraints` | list of `{constraint_id, kind, statement, source_ref}` | Compatibility, policy, legal, time, platform, or other binding constraint |
| `scope.assumptions` | list of `{assumption_id, statement, certainty, evidence_refs, validation_owner}` where `certainty` is `observed`, `inferred`, or `unavailable` | Non-facts remain visible and owned |
| `scope.dependencies` | list of `{dependency_id, kind, required_state, owner, availability}` where `kind` is `product`, `policy`, `external_system`, `stakeholder`, or `evidence`, and `availability` is `available`, `unavailable`, or `unknown` | Product/external prerequisites, not an implementation package list |
| `current_state.observed_behavior` | list of `{observation_id, statement, evidence_refs, certainty}` | Existing behavior supported by evidence; intent does not overwrite it |
| `current_state.invariants` | list of `{invariant_id, statement, evidence_refs}` | Existing contract or architecture facts that constrain the desired behavior |
| `current_state.known_gaps` | list of `{gap_id, statement, consequence}` | Missing evidence or unresolved mismatch |

`certainty` is `observed`, `inferred`, or `unavailable`; it is independent of the document-level
**O/I/U** labels used for this phase-0 design.

#### 2.5.4 Behavior and acceptance contract

| Field path | Type | Meaning |
|---|---|---|
| `behavior.scenarios` | list of `{scenario_id, actor_ids, preconditions, trigger, expected_sequence, terminal_state}` | User/system journeys without implementation sequencing |
| `behavior.requirements` | list of `{requirement_id, kind, statement, rationale, source_refs}` | `kind` is `functional`, `quality`, `policy`, `compatibility`, or `data` |
| `behavior.acceptance_criteria` | list described below | Observable criteria mapped to requirements |
| `behavior.negative_cases` | list of `{case_id, trigger, required_response, forbidden_response, requirement_ids}` | Failure and forbidden behavior are first-class |
| `behavior.permissions_and_roles` | list of `{rule_id, actor_id, allowed, denied, condition}` | Explicit authorization behavior where relevant |
| `behavior.data_and_contract_rules` | list of `{rule_id, subject, required_behavior, compatibility, evidence_refs}` | Product/API/data semantics, not storage or migration tasks |
| `behavior.accessibility_and_localization` | list of `{rule_id, jurisdiction, required_behavior}` | Explicit cross-cutting behavior when applicable |

Every `behavior.acceptance_criteria[]` item has exactly these fields:

| Field | Type | Rule |
|---|---|---|
| `criterion_id` | stable non-empty string | Unique within the specification |
| `requirement_ids` | non-empty list | Every criterion traces to at least one requirement |
| `actor_or_system` | non-empty string | Observer or affected party |
| `preconditions` | list of strings | Explicit starting state; empty is allowed |
| `trigger` | non-empty string | Action or event |
| `observable_outcome` | non-empty string | Externally visible result, not a private implementation detail |
| `failure_or_negative_case` | string or `null` | Required failure behavior when relevant |
| `measure` | string or `null` | What is measured when a threshold exists |
| `threshold` | string or number or `null` | Accepted boundary; cannot exist without `measure` |
| `evidence_method_class` | `test`, `inspection`, `measurement`, `stakeholder_confirmation`, or `external_verification` | Class of later proof; Spec does not execute it |

#### 2.5.5 Decisions, alternatives, and technical constraints

| Field path | Type | Meaning |
|---|---|---|
| `decisions.alternatives` | list of `{alternative_id, summary, benefits, costs, risks, disposition, decision_ref}` where `disposition` is `selected`, `rejected`, `deferred`, or `open` | Preserves real alternatives and user rulings |
| `decisions.selected_direction` | `{alternative_id, rationale, decision_ref}` or `null` | Product/design direction, not an executable plan |
| `decisions.user_rulings` | list of `{decision_id, question, answer, authority, decision_ref, affected_fields}` | Every material user-owned decision is traceable |
| `technical_constraints.modules` | list of `{module_ref, observed_role, evidence_refs}` | Existing modules touched by behavior, not files-to-edit |
| `technical_constraints.interfaces` | list of `{interface_ref, invariant, compatibility, evidence_refs}` | Existing interface facts and required compatibility |
| `technical_constraints.seams` | list of `{seam_ref, reason, evidence_refs}` | Existing or required testing/integration seams without task decomposition |
| `technical_constraints.adapters` | list of `{adapter_ref, external_system, constraint, evidence_refs}` | Existing external adaptation facts, not a selected implementation stack |
| `technical_constraints.forbidden_prescriptions` | fixed list | Must include `task_order`, `files_to_change`, `implementation_commands`, `effort_estimates`, and `rollout_steps` |

The module/interface/seam/adapter vocabulary is deliberate. A specification may constrain an
existing interface or require an observable seam. It may not turn those constraints into Plan's
execution graph or Implement's file list.

#### 2.5.6 Evidence, uncertainty, downstream readiness, and delivery

| Field path | Type | Meaning and invariant |
|---|---|---|
| `evidence.items` | list of `{evidence_id, source_kind, source_ref, claim, certainty, captured_at}` where `source_kind` is `user`, `stakeholder`, `repository`, `contract`, `understand_packet`, `test_packet`, `debug_packet`, or `external_observation`, and `certainty` is `observed`, `inferred`, or `unavailable` | Traceable support for current-state and constraint claims |
| `evidence.conflicts` | list of `{conflict_id, evidence_refs, description, ruling_ref}` | Conflicting evidence remains visible; a ruling is optional until resolved |
| `uncertainty.open_questions` | list of `{question_id, question, owner, blocking, affected_fields}` | No question disappears because a draft reads fluently |
| `uncertainty.unavailable_inputs` | list of `{input_id, description, consequence, fallback}` | Missing prerequisite and degradation record |
| `readiness.plan_state` | `ready` or `blocked` | `ready` is valid only under the acceptance gate below |
| `readiness.blocking_question_ids` | list of IDs | Must be empty for `ready` |
| `readiness.nonblocking_question_ids` | list of IDs | Accepted uncertainty Plan must preserve, not silently resolve |
| `readiness.required_plan_inputs` | list of strings | Inputs Plan must still obtain; cannot include unresolved product decisions when `ready` |
| `readiness.acceptance_map` | list of `{requirement_id, criterion_ids}` | Complete requirement-to-criterion mapping |
| `delivery.mode` | `none`, `local_document`, or `issue` | Delivery is optional and never confers acceptance |
| `delivery.authorized` | boolean | Explicit authority for the selected effect |
| `delivery.destination_ref` | string or `null` | Path/issue URL when attempted |
| `delivery.result` | `not_attempted`, `succeeded`, `failed`, or `partial` | Effect outcome independent of artifact lifecycle |
| `delivery.failure` | string or `null` | Exact visible failure or degradation |
| `delivery.observed_at` | timestamp or `null` | Time external state was last verified |

#### 2.5.7 The non-inference acceptance gate

Plan may consume the artifact only when all of these are true:

1. `lifecycle.state == accepted`;
2. `approval.state == accepted`;
3. `approval.approved_revision == revision`;
4. `approval.approved_content_hash == content_hash`;
5. `approval.decider` is non-null and has the required `approval.authority_scope`, including
   `whole_revision`;
6. `approval.decision_ref` is non-null;
7. `readiness.plan_state == ready`;
8. `readiness.blocking_question_ids == []`;
9. every requirement appears in `readiness.acceptance_map`; and
10. no referenced `uncertainty.open_questions[]` item with `blocking: true` remains unresolved.

Section-by-section assent, a `ready-for-agent` label, a filed issue, a committed design document, a
passing external review score, or the phrase “looks good” outside a traceable whole-revision
decision does not satisfy this gate. A revision invalidates prior acceptance until the same gate
passes for the new `revision`. Delivery failure does not revoke an otherwise accepted artifact;
delivery success does not accept a draft.

### 2.6 Effect authority and non-goals

Spec may inspect bounded project evidence read-only. With separate explicit authority it may later
write the specification to one local destination or file one issue through an adapter at the
delivery seam. Each effect is opt-in, individually recorded, and failure-visible.

Spec does **not**:

- write or change production code, tests, configuration, migrations, plans, tasks, CI, or deploy
  state;
- create a branch, worktree, commit, stash, PR, release, or deployment;
- install or update a CLI, plugin, skill, package, issue-tracker setup, or speckit state;
- dispatch an implementation or review agent;
- invoke Plan, Implement, Test, Debug, Critique, or Ship;
- decide a user-owned ambiguity, auto-accept a revision, or treat tool pre-approval as user
  authority;
- prescribe task order, exact implementation commands, effort estimates, rollout steps, or a
  files-to-change list;
- mutate issue labels or remote artifacts without explicit destination and effect authority;
- turn optional browser/visual delivery into a prerequisite for textual specification; or
- absorb the retained `sdd` navigator or any deferred general-purpose concern.

### 2.7 Decisions that remain with the user

The user or identified stakeholder authority owns problem framing when evidence conflicts; included
and excluded outcomes; selection among material alternatives; acceptable risk and compatibility;
every product requirement and acceptance criterion; whether a draft is accepted; whether a
revision supersedes the accepted version; whether Critique starts; whether Plan starts; and every
local, remote, browser, external-review, or dispatch effect. The module may recommend, ask, record,
and stop. It cannot inherit authority from an `allowed-tools` list, implicit-invocation setting,
issue label, source default, or prior acceptance of a different revision.

---

## 3. Source evidence and proposed ledger changes

All assigned bodies and their directly relevant declarations, generation inputs, and bundled files
were inspected in full on 2026-08-03. Hashes identify the inspected bytes; clean Git revisions
identify all listed files inside those repositories.

### 3.1 Occurrence inspection record

| Occurrence / source | Component type and live location | Invocation / availability | Complete declaration or registration | Immutable provenance |
|---|---|---|---|---|
| `cm-plan-and-spec-01` / `superpowers:brainstorming` | skill in installed `superpowers` Codex plugin cache at `~/.codex/plugins/cache/openai-curated-remote/superpowers/6.2.0/skills/brainstorming/` | `superpowers:brainstorming`; live (**O**) | `name: brainstorming`; description requires use before creative work and says it explores intent, requirements, and design before implementation. OpenAI metadata contains only `display_name: Brainstorming` and `short_description: Explore intent, requirements, and design before implementation`; no per-skill policy field. Plugin manifest version is `6.2.0`; plugin capabilities are `Interactive`, `Read`, and `Write` (**O**) | plugin manifest `b271065c5e90`; skill `4a54a4858b99`; remote registration id `plugins~Plugin_60aea7460bd4819199fd97a9553a5e12` |
| `cm-plan-and-spec-05` / `spec` | generated skill; `~/.claude/skills/spec/SKILL.md` symlink → `~/.claude/skills/gstack/spec/SKILL.md`; authoritative template is sibling `SKILL.md.tmpl` | `/spec`; live (**O**) | `name: spec`; `version: 0.1.0`; full description names issue filing and optional agent spawn; `allowed-tools: Bash, Read, Grep, Glob, AskUserQuestion`; six exact natural-language triggers; no invocation-disable field (**O**) | clean gstack revision `a3259400a366593e0c909dd9ac3e59752efd2488`; package version `1.60.1.0`; generated `7ad290d73bb3`; template `26b366c256f7` |
| `cm-plan-and-spec-06` / `to-spec` | skill; `~/.claude/skills/to-spec` symlink → `~/.agents/skills/to-spec/` | `/to-spec`; live; user-only (**O**) | `name: to-spec`; description says synthesize the current conversation and publish it to the project issue tracker without interview; `disable-model-invocation: true`; OpenAI metadata `To Spec` / `Turn a conversation into a spec` and `policy.allow_implicit_invocation: false` (**O**) | skill `267638edd513`; metadata `1c5b4d1e3d8e` |
| `cm-plan-and-spec-07` / `sdd` | skill; `~/.claude/skills/sdd` symlink → `monster-prompt/claude/skills/sdd/` | `/sdd`, `/sdd update`, `/sdd upgrade`; live (**O**) | `name: sdd`; `effort: low`; long description declares workflow navigation/status and update triggers; no tool, invocation-disable, hook, or agent declaration. The inspected marketplace manifest registers only `loop-goal`, not `sdd`, so this occurrence is a personal symlink rather than a marketplace registration (**O**) | clean `monster-prompt` revision `6abccfa5f83a82f2bff309228b956323a11e4d2a`; skill `652a1039fe72`; marketplace manifest `8992866835bd` |

`allowed-tools` and plugin capability lists are host pre-approval metadata. They are not proof of
user authority for any effect.

#### 3.1.1 Complete declaration values

The compact evidence table does not replace exact registration evidence. These are the complete
skill declaration values and directly relevant invocation metadata observed in the inspected
bytes:

```yaml
# superpowers:brainstorming SKILL.md
name: brainstorming
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation."
# agents/openai.yaml
interface:
  display_name: Brainstorming
  short_description: Explore intent, requirements, and design before implementation
# no policy field
# plugin registration relevant to this occurrence
plugin_name: superpowers
plugin_version: 6.2.0
skills_path: ./skills/
hooks: {}
capabilities: [Interactive, Read, Write]
remote_plugin_id: plugins~Plugin_60aea7460bd4819199fd97a9553a5e12
```

```yaml
# live generated spec SKILL.md
name: spec
version: 0.1.0
description: Turn vague intent into a precise, executable spec in five phases. (gstack)
allowed-tools: [Bash, Read, Grep, Glob, AskUserQuestion]
triggers:
  - spec this out
  - file an issue
  - write up a ticket
  - turn this into an issue
  - make this a github issue
  - turn this into a backlog item
# generated body section "When to invoke this skill" restores this remainder:
# Files the issue, optionally spawns a Claude Code agent in a fresh worktree, and lets /ship close the source issue on merge. Use when asked to "spec this out", "file an issue", "write up a ticket", "make this a GitHub issue", or "turn this into a backlog item".
```

```yaml
# to-spec SKILL.md
name: to-spec
description: Turn the current conversation into a spec and publish it to the project issue tracker — no interview, just synthesis of what you've already discussed.
disable-model-invocation: true
# agents/openai.yaml
interface:
  display_name: To Spec
  short_description: Turn a conversation into a spec
policy:
  allow_implicit_invocation: false
```

```yaml
# sdd SKILL.md
name: sdd
effort: low
description: "SDD workflow navigator — tells you which speckit step to run next. Use whenever the user types /sdd, asks 'what's next', 'where am I in speckit', 'which speckit command', 'SDD status', or seems unsure about the spec-driven development workflow order. Also use when the user just finished a speckit step and needs guidance on what comes next. Even a simple '?' or 'next step' in a speckit context should trigger this. Also triggers on '/sdd update', '/sdd upgrade', or 'update speckit' to update the specify CLI."
# no tools, hooks, invocation-disable field, agent declaration, or OpenAI metadata
# repository marketplace manifest has no sdd entry
```

### 3.2 Full-body and bundle evidence

| Source | Observed behavior, authority, effects, prerequisites, and failures |
|---|---|
| `superpowers:brainstorming` | Enforces a hard no-implementation gate; explores project context; asks one question at a time; presents two or three approaches; obtains staged section approval; writes a design document; performs an inline self-review; asks the user to review the written document; and terminates by invoking `superpowers:writing-plans`. Its native checklist also commits the design document. A just-in-time visual companion is optional and user-approved. The companion needs Node and a browser, starts a keyed local HTTP/WebSocket server, writes session HTML/event files under `.superpowers/brainstorm/` or `/tmp`, may open a browser, and has telemetry/remote-asset paths. Missing browser/Node or declined visual use must degrade to text. The bundled reviewer prompt remains a distinct support artifact even though the current skill instructs an inline quick review. (**O**) |
| `spec` | Runs a five-phase interrogation: why; scope; code-evidence/technical questions; draft review; quality/redaction; then filing. It can deduplicate with GitHub, dispatch a Codex quality reviewer, enforce fail-closed secret/PII redaction, file a GitHub issue, write a local archive, opt that archive into artifacts sync, and by default outside plan mode spawn `claude -p` in a new worktree. Flags include `--dedupe`/`--no-dedupe`, `--no-gate`, `--audit`, `--execute`, `--no-execute`/`--file-only`, `--plan-file`, and `--sync-archive`. `--no-gate` does not disable redaction. It depends on gstack binaries/config, shell tools, Git, optional `gh`/`glab`, Bun for redaction, Codex for the quality gate, and Claude/worktree support for spawn. Missing optional tools have source-specific skip/stop behavior; redaction HIGH findings block persistence. Its template asks for exact implementation detail, dependency graphs, effort, rollback, and task-ready precision that cross the Astra Spec/Plan seam. (**O**) |
| `to-spec` | Synthesizes existing conversation and codebase context without an interview; uses domain glossary and ADR vocabulary; chooses high existing test seams; then says to check those seams with the user, which conflicts with “no interview.” It writes a PRD-like issue with problem, solution, long user stories, implementation decisions, testing decisions, out-of-scope, and notes; publishes to the configured tracker; and applies `ready-for-agent`. It requires external tracker and triage vocabulary and otherwise directs the user to `/setup-matt-pocock-skills`. It declares no fallback for tracker or label failure. The issue and label are remote effects, not prose formatting. (**O**) |
| `sdd` | Declares itself read-only and says never to modify files, but `/sdd update` installs `specify-cli` from GitHub, missing `.specify/` triggers `specify init`, and checklist evaluation writes checkbox/evidence changes. It inspects constitution/spec/plan/tasks/checklist state, treats specifications as persistent source of truth, preserves `[NEEDS CLARIFICATION]`, supports backward flow after implementation evidence, and recommends `/speckit.*` commands. It also depends on speckit registrations, Specify CLI, Git/project artifact layout, Jira URLs and Jira MCP for Specify/Clarify, and optional external skills for API design/review, BDD, local debug, and scored review. Its command navigator, automatic checklist decisions, and install/init effects are a separate job from authoring an Accepted Specification. (**O**) |

No available body is an alias or delegating stub. The `spec` live entry is a symlink to generated
bytes, but that is one occurrence with a generated delivery path, not a second source. The
authoritative gstack template contains two literal `{{PREAMBLE}}` tokens: one intended placeholder
and one in prose explaining `GSTACK_PLAN_MODE`. The generator expands both, so the 2,359-line live
output contains two byte-identical 767-line preamble regions (**O**, exact comparison succeeded).
The duplicate is a generation defect, not independently authored Spec behavior.

#### 3.2.1 Inspected bundle index

| Bundle | Files inspected in full and immutable anchors |
|---|---|
| Brainstorming | plugin manifest `b271065c5e90`; remote-install record `c36744fde190`; `SKILL.md` `4a54a4858b99`; `agents/openai.yaml` `90585d2a0928`; reviewer prompt `95a0a195de9d`; visual companion `60cbad29b9dd`; `frame-template.html` `6a8a4e58bd6a`; `helper.js` `43c6d69954a4`; `server.cjs` `2d2961ea8d11`; `start-server.sh` `a4e5ae84275b`; `stop-server.sh` `0b5ccbbd57f6` |
| gstack `spec` | Clean revision `a3259400a366593e0c909dd9ac3e59752efd2488` anchors generated body, authoritative template, package registration, full generator, resolver registry/types, PREAMBLE composition and every consumed generator, selected model overlay, redaction resolver and canonical pattern taxonomy. Key hashes: package `9980b37cd19b`; generator `cd62a5046ee6`; registry `9e07dfe5a4ec`; PREAMBLE root `d6e6e2f5cd68`; redaction resolver `70c1d1ccf351`; taxonomy `2f8f7314ad5e`; Claude overlay `b975643f22bd` |
| `to-spec` | `SKILL.md` `267638edd513`; `agents/openai.yaml` `1c5b4d1e3d8e`; no scripts, agents, references, hooks, or other bundle files found (**O**) |
| `sdd` | Clean revision `6abccfa5f83a82f2bff309228b956323a11e4d2a` anchors the sole `SKILL.md` and its repository marketplace manifest; no local scripts, agents, references, or OpenAI metadata in the skill bundle (**O**) |

### 3.3 Disposition and contribution

| Occurrence | Proposed disposition and home | Contribution to this design | Preserved separate behavior or secondary role |
|---|---|---|---|
| `superpowers:brainstorming` | proposed Astra design → `astra-spec` | **Protocol, Playbook, Machinery, Authority**: question-at-a-time discovery, alternatives, staged approval, hard pre-implementation stop, scalable design presentation | Visual companion is an optional delivery adapter. Design-doc write, commit, reviewer support artifact, and terminal Plan invocation remain separately authorized/manual until fidelity is proved; no implicit Plan start |
| `spec` | proposed Astra design → `astra-spec` | **Protocol, Playbook, Jurisdiction, Machinery**: rigorous intent interrogation, brownfield evidence, acceptance precision, scope control, revision-quality and redaction ideas | GitHub dedupe/issue, archive/artifacts sync, Codex reviewer, worktree, stash, and spawned agent are separate external effects. Plan owns executable detail; Implement owns mutation; Ship owns final publication/VCS |
| `to-spec` | proposed Astra design → `astra-spec` | **Protocol, Playbook, Jurisdiction**: fast synthesis of already-settled conversation, domain vocabulary, user-story and testing-decision capture | Issue filing, `ready-for-agent`, and setup prerequisite remain an explicit issue-delivery adapter/manual bridge. Its “no interview” rule cannot bypass acceptance or unresolved blockers |
| `sdd` | independent reference → retained independent | **Reference, Playbook**: persistent versioned specification, fielded clarification markers, evidence-driven revision and backward flow | Entire workflow navigator remains independently invocable. Install/update/init, command recommendation, checklist mutation, Jira-specific rules, and external skill routing are not absorbed |

The proposed `sdd` split is evidence-based, not a rename preference. A request to author accepted
intent and a request to report the next command can occur at different times, have different
outputs, and require incompatible effect policies. Absorbing the latter would broaden the public
interface and create an unearned Automate/Delegate surface.

### 3.4 Exact proposed collision-ledger changes

Only the phase-0 coordinator may apply these rows. The four current rows are `unassigned` and
`unclaimed`; this design proposes `claimed`, never `resolved`.

| Occurrence ID | Proposed primary disposition | Proposed primary home | Proposed secondary roles | Proposed claim state | Evidence |
|---|---|---|---|---|---|
| `cm-plan-and-spec-01` | proposed Astra design | `astra-spec` | `astra-plan`: provenance of the source's terminal writing-plans edge only; `astra-critique`: external review support remains separate | `claimed` | this design §§3.1–5.2 and complete Brainstorming bundle hashes |
| `cm-plan-and-spec-05` | proposed Astra design | `astra-spec` | `astra-plan`: executable-detail split; `astra-implement`: spawned-agent effect excluded from Spec; `astra-ship`: issue-close/archive provenance; `astra-critique`: independent evaluator behavior | `claimed` | this design §§3.1–5.6 and clean generated-source pipeline revision |
| `cm-plan-and-spec-06` | proposed Astra design | `astra-spec` | issue delivery remains an explicit external adapter; no agent or peer invocation | `claimed` | this design §§3.1–5.5 and complete two-file bundle hashes |
| `cm-plan-and-spec-07` | independent reference | retained independent | `astra-spec`: consumes persistent-spec and backward-revision principles only | `claimed` | this design §§3.1–5.7 and clean `monster-prompt` revision |

### 3.5 Exact proposed reference-and-cleanup-ledger change

Because `sdd` is proposed as an independently retained reference consumed by this design, the
coordinator should add this row if the primary split is accepted. The global ledger and user retain
`keep` / `defer` / `exclude` authority; this document does not set it to `keep`.

| Source ID | Component type | Location | Availability | Disposition | Reason | Consuming designs | Evidence |
|---|---|---|---|---|---|---|---|
| `sdd` | skill | `~/.claude/skills/sdd` → `monster-prompt/claude/skills/sdd/` | live | `unassigned` | Recommend keep pending user decision: its workflow-status outcome and command/effect policy are not owned by Spec; Spec consumes only the persistent-spec and backward-revision reference slice | `astra-spec` | this design §§3.1–3.3; clean revision `6abccfa5f83a82f2bff309228b956323a11e4d2a`; skill `652a1039fe72` |

No other reference-and-cleanup-ledger change is proposed. The issue trackers, browser, Node, Git,
Codex, Claude, gstack binaries, Specify CLI, Jira MCP, and source-linked documentation are external
prerequisites or tools, not independently consumed live reference entries under that ledger.

---

## 4. Collision analysis

### 4.1 Why the sources appeared duplicative

All four use the word “spec,” operate before or around implementation, read project context, and
try to reduce ambiguity. Brainstorming produces an approved design; `spec` produces a backlog issue;
`to-spec` produces a PRD-like issue; `sdd` treats a spec as the controlling artifact in a larger
workflow. Labels alone therefore suggest one generic “make a spec” command.

### 4.2 Behavior genuinely shared

The three authoring sources share a smaller kernel:

```text
intent/evidence → explicit decisions → bounded desired behavior → acceptance artifact
```

They all preserve some combination of problem, user outcome, scope, constraints, decisions, and
testing/acceptance thought. Brainstorming and `spec` both interrogate ambiguity; `to-spec` and
`spec` both package backlog-ready content; Brainstorming and `to-spec` both scale detail to known
context. That shared behavior supports one deep Spec module.

`sdd` shares the artifact's importance and revision semantics, but not the authoring job. It is a
consumer/navigator of a broader artifact hierarchy. That is a reference relation, not shared core.

### 4.3 Aliases and shallow delegation

None of the four occurrences is a delegating stub. `~/.claude/skills/spec/SKILL.md` is a symlink to
the generated gstack file, and `to-spec`/`sdd` are directory symlinks to their installed bodies;
these are delivery aliases for the same occurrence. The Brainstorming skill's terminal instruction
to invoke `superpowers:writing-plans` is a real cross-workflow edge, not proof that writing-plans is
part of Brainstorming or Spec.

### 4.4 Apparent duplicates that are different jobs

| Behavior | Why it remains distinct |
|---|---|
| Brainstorming visual companion | It externalizes a visual decision through a local browser adapter; textual questioning is still complete without it |
| `spec` Codex quality gate and Brainstorming reviewer support | Independent judgment is reviewer behavior. It cannot be flattened into “self-review” or silently absorbed by Spec |
| GitHub issue, local archive, design document, label, and commit | These are different delivery/effect adapters with different authorization and failure semantics |
| `spec` fresh-worktree agent spawn | This is Delegate/Implement machinery and changes external/project state; it is not specification authorship |
| `sdd` dashboard and command recommendation | Its result is “where the workflow is and what command comes next,” not an Accepted Specification |
| `sdd` update/init/checklist paths | They install or mutate state despite the source's read-only declaration; they require their own authority and failure handling |
| Plan-ready technical decomposition | Exact task order, files, commands, effort, and rollout are Plan's job even when a source includes them in a ticket template |

### 4.5 Instruction conflicts that must remain visible

1. **Interview versus synthesis.** Brainstorming and `spec` require iterative questioning;
   `to-spec` says no interview but later requires user seam confirmation. Proposed resolution:
   `synthesize` may skip discovery questions only when all acceptance-blocking fields are already
   grounded; it still needs an explicit whole-revision acceptance decision.
2. **Section approval versus whole-revision approval.** Brainstorming stages approval by section;
   issue sources can publish without a fielded revision gate. Proposed resolution: preserve staged
   decisions as evidence, then require the section 2.5.7 whole-revision gate.
3. **Authorship versus planning.** `spec` asks for implementation sequence, file-level work,
   dependencies, effort, and rollback; `to-spec` includes implementation decisions; `sdd` routes to
   Plan/Tasks. Proposed resolution: retain technical constraints and test seams, exclude executable
   decomposition from the Spec artifact.
4. **Read-only claim versus mutation.** `sdd` says never modify, then installs, initializes, and
   rewrites checklists. Proposed resolution: retain it independently and make the safe manual bridge
   stop before every effect unless separately authorized.
5. **Automatic downstream action versus user authority.** Brainstorming invokes writing-plans;
   gstack `spec` defaults to agent spawn outside plan mode; issue sources publish/label. Proposed
   resolution: no implicit invocation and no effect without an explicit per-effect gate.
6. **External review versus authorship.** `spec` dispatches Codex and Brainstorming bundles a
   reviewer prompt. Proposed resolution: external review remains a separately authorized adapter or
   user-mediated Critique workflow, never hidden inside Spec.
7. **Generated versus authored authority.** The live gstack output duplicates the common preamble;
   the template and resolver pipeline are authoritative maintenance sources. Generated duplication
   cannot count as distinct preserved behavior or an advantage.

### 4.6 Why one coherent deep module is plausible

The three authoring sources vary mainly in how much intent is already known and how the artifact is
delivered. Their shared invariant is stronger than their delivery differences: desired behavior and
acceptance authority must be explicit before downstream planning. One interface can route among
`discover`, `synthesize`, and `revise`, while internal adapters preserve questions, visuals, local
documents, and issues. The caller does not need to understand source provenance or pipeline flags.

This is one module, not a universal planning runtime. The retained `sdd` split and the hard Plan
seam prevent breadth from masquerading as depth.

### 4.7 Declared positive advantage

**Advantage class: decision integrity under mixed ambiguity and brownfield evidence.** The proposed
module should outperform the strongest single source on cases where user intent is incomplete,
existing behavior constrains the answer, acceptance criteria must be observable, and an explicit
acceptance decision must survive later revision.

A positive win requires all of the following on at least one fixed combination class:

- higher recall of material intent/scope/acceptance decisions than the best source oracle;
- equal or better supported-claim precision and no increase in invented requirements;
- a field-complete artifact whose approval state cannot be mistaken by Plan;
- preservation of source-unique clarification, synthesis, and delivery behavior; and
- zero unauthorized issue, document, commit, agent, peer, browser, install, or project effects.

Convenience, one command name, a longer document, or matching the oracle's final recommendation is
not a positive advantage.

---

## 5. Preserved distinctions

### 5.1 Discovery is not synthesis

`discover` preserves Brainstorming's question-at-a-time cadence, `spec`'s pressure against
ambiguity, and explicit purpose/constraints/success exploration. `synthesize` preserves `to-spec`'s
valuable no-redundant-interview behavior when conversation evidence is already sufficient. A
candidate must decide from artifact completeness, not user patience: it may recommend synthesis,
but a blocking gap returns the workflow to one focused question or produces a non-accepted draft.

This distinction matters when the same terse prompt follows either a rich design conversation or no
prior context. Treating both identically either wastes the first case or invents the second.

### 5.2 Alternatives and staged approval

Brainstorming's two-or-three alternatives and section-scaled presentation survive. The future module
must expose meaningful trade-offs before locking a product/design direction, and it must preserve
every user ruling. Staged section approval reduces review load, but only the whole-revision gate can
set `approval.state: accepted`.

This matters when the user accepts scope but rejects the proposed failure behavior. A flat “approved”
flag would erase the distinction and let downstream work proceed on a revision the user did not
accept.

### 5.3 Accepted intent is not an executable plan

`spec` and `to-spec` contain useful technical evidence, seam selection, compatibility concerns, and
testing decisions. Those survive as `technical_constraints`, acceptance criteria, and
`evidence_method_class`. Exact files, implementation steps, dependency order, estimates, commands,
worktree instructions, and rollout/rollback sequences do not. Plan must derive them from the
accepted artifact and current project state.

This matters when an issue remains product-correct but its originally guessed file path or build
sequence becomes stale.

### 5.4 Approval authority and revision semantics

Brainstorming's user approval gate and `sdd`'s persistent source-of-truth principle survive as the
fielded lifecycle/approval contract. A new revision supersedes but does not inherit acceptance.
Issue state, label, review score, design-doc commit, or completed section reviews remain evidence or
delivery facts only.

This matters when production feedback changes one negative case after Plan has already consumed
revision 3. Revision 4 is `draft` until explicitly accepted, and Plan can detect that mechanically.

### 5.5 Local-document, issue, and visual delivery

These are adapters at two real internal seams, not generic prose:

- a **persistent-delivery seam** has at least two actual adapters: local design/spec document and
  issue tracker;
- a **presentation seam** has textual rendering and the optional Brainstorming browser/visual
  adapter.

Each adapter preserves destination, authorization, bytes sent or written, result, and failure.
Issue filing and `ready-for-agent` labeling are separate remote operations. A local archive and a
project design document are separate writes. A design-doc commit is a separate VCS effect and stays
outside Spec. Visual session files, browser launch, and local server lifetime remain visible.

This matters when the user accepts the artifact but denies remote publication, or authorizes an
issue but not a label.

### 5.6 Independent review and agent delivery shapes

The Brainstorming reviewer prompt, gstack Codex quality gate, and gstack spawned Claude agent are
not reduced to “review carefully” or “someone can implement it.” They preserve distinct execution
contexts, dependencies, payloads, failures, and effects:

- external review may be requested separately or approximated through a user-mediated Critique
  workflow, but Spec itself does not judge its own artifact as an independent reviewer;
- a quality score cannot confer acceptance;
- a spawned worktree agent is a Delegate/Implement effect and never starts from Spec implicitly;
- missing Codex/Claude/worktree support is reported, not silently simulated by the authoring
  context.

This matters when a draft scores highly but the user has not accepted a scope trade-off, and when
the issue is filed successfully but agent spawn fails.

### 5.7 Persistent specification and backward flow

The `sdd` source contributes a durable reference principle: implementation, Test, Debug, or
production evidence may reveal that an accepted requirement is incomplete or wrong; the
specification is revised first, then downstream artifacts are reconsidered. Its exact command
dashboard, Jira mandate, constitution workflow, checklist auto-evaluation, score thresholds, and
external-skill routing remain with retained `/sdd`.

This matters when the implementation works as planned but contradicts a newly observed user need.
Spec revises intent; Debug does not redefine the requirement and Plan does not patch it silently.

### 5.8 Prerequisites, authority, and failure behavior

| Preserved source distinction | Later candidate obligation |
|---|---|
| Project/repository may be absent | Ask for bounded artifact evidence or produce an explicitly evidence-limited draft; never invent current state |
| User/stakeholder authority may be absent | Draft may exist, but acceptance is blocked and `decider` remains `null` |
| Node/browser unavailable or visual declined | Continue textually and record visual adapter unavailable/declined |
| Tracker/label/credentials/network unavailable | Preserve the accepted artifact, report delivery failure, do not fabricate an issue URL or label |
| Codex/redaction runtime unavailable | External review may degrade only as authorized; secret-safety failure follows a fail-closed policy before any authorized remote publication |
| `gh`, Git, worktree, or Claude unavailable | No dedupe/spawn simulation; core Spec outcome remains independent |
| Speckit/Jira/Specify unavailable | `/sdd` bridge stops with its missing prerequisite; Astra Spec does not install or imitate it |
| Evidence conflicts with stated intent | Record both, ask the correct authority, and preserve the ruling reference |
| User rejects or requests changes | Artifact remains `rejected` or `changes_requested`; no downstream readiness |

---

## 6. Proposed skill design

### 6.1 Deep module and small interface

The architecture hypothesis is one deep `astra-spec` module with one external interface: accept a
Specification Context and return a Specification Result. Its depth comes from reconciling evidence,
interview state, alternatives, authority, acceptance criteria, revision history, and optional
delivery behind that interface.

The interface includes these promises:

- **invariant:** accepted intent and approval are revision-bound and fielded;
- **error contract:** missing evidence, authority, or delivery prerequisites are named with their
  consequence and never converted into success;
- **configuration:** discovery/synthesis/revision mode and effect authority are caller-visible;
- **performance expectation:** simple synthesis should not inherit full discovery ceremony, while
  ambiguity must not be skipped to reduce latency; and
- **test surface:** artifact fields, gate invariants, source-unique behavior, and zero unauthorized
  effects are observable without inspecting internal prompts.

### 6.2 Internal modules

| Internal module | Responsibility | What it must not own |
|---|---|---|
| Intake and authority classifier | Normalize intent, evidence, requested mode, decider authority, prior revision, and effect grants | Product decisions or downstream workflow starts |
| Evidence-grounding module | Consume supplied Understand/Test/Debug artifacts; separate observed, inferred, unavailable, and conflicting claims | Repository explanation, testing, or diagnosis as an independent job |
| Clarification module | Ask one material question at a time and track blocking gaps | Auto-deciding a user-owned ambiguity |
| Alternatives module | Generate two or three materially distinct directions with trade-offs and recommendation | Treating recommendation as acceptance |
| Specification compiler | Populate the exact artifact contract, including negative cases and acceptance map | Task order, files-to-change, commands, estimates, or rollout |
| Decision and approval module | Record section decisions; present the whole revision; validate explicit acceptance authority | Inferring approval from prose, issue state, or source defaults |
| Revision module | Compare prior accepted revision with new evidence; mark supersession and invalidate stale acceptance | Quietly mutating the accepted artifact in place |
| Delivery coordinator | Invoke only authorized local-document, issue, or visual adapters and record their results | Commits, labels without authority, agent spawn, or peer invocation |
| Contract validator | Check schema, traceability, blocking questions, acceptance mapping, forbidden prescriptions, and delivery/approval independence | Substituting a quality score for the user decision |

These are responsibilities behind one interface, not public child skills. No shared Astra module is
proposed: this design alone cannot prove reuse.

### 6.3 Modes and stopping rules

| Mode | Use | Preserved source value | Stop condition |
|---|---|---|---|
| `discover` | Vague, conflicting, or materially incomplete intent | Brainstorming dialogue, alternatives, staged presentation; `spec` interrogation | Stop on each user decision; stop before acceptance if authority or blocking evidence is absent |
| `synthesize` | Prior conversation already resolves all material questions | `to-spec` speed, domain vocabulary, no redundant interview | Fall back to one focused clarification or emit a non-accepted draft when a blocking field is missing |
| `revise` | Accepted spec is challenged by new user, Test, Debug, production, or Critique evidence | `sdd` persistent truth/backward flow; revision-bound approval | Never inherit acceptance; stop until changed revision is reviewed and explicitly accepted |

Delivery is not a fourth authoring mode. It is a post-artifact adapter choice and can fail without
changing the artifact's intent state.

### 6.4 Information flow

```text
Specification Context
        │
        ▼
intake + authority classification
        │
        ▼
evidence grounding ── conflict/unavailable ──► field gap and consequence
        │
        ▼
mode selection: discover | synthesize | revise
        │
        ├─ discover ─► focused questions ─► alternatives ─► staged decisions
        ├─ synthesize ─────────────────────► decision inventory
        └─ revise ─► prior-revision diff ──► changed-decision inventory
        │
        ▼
Specification compiler
        │
        ▼
contract validator ── failure ─► draft / changes_requested / blocked
        │
        ▼
whole-revision user acceptance gate
        │
        ├─ not accepted ─► fielded non-accepted result
        └─ accepted ─────► Accepted Specification
                               │
                               └─ optional authorized delivery adapter
```

No arrow invokes another Astra peer. Peer artifacts enter only when the user supplies them; peer
workflow starts occur only after this module stops and the user acts.

### 6.5 Internal seams and adapters

The evidence justifies these internal seams:

1. **Evidence-input seam.** Understand Code, Test, Debug, stakeholder, and existing-contract
   packets vary in shape but must yield claims, anchors, certainty, and conflicts. Adapters normalize
   them without granting their originating peer invocation authority.
2. **Persistent-delivery seam.** Local-document and issue-tracker adapters are two real variants.
   They share bytes, authority, destination, result, and failure fields while preserving their
   different effects.
3. **Presentation seam.** Text and optional visual/browser delivery are two real variants. Text is
   always sufficient; visual delivery never changes decision authority.
4. **External-review seam.** Brainstorming support review and gstack Codex evaluation establish
   source variation, but the seam remains external to the Spec core. A later candidate may offer a
   separately authorized adapter or user-mediated Critique suggestion; it may not call itself
   independent.

One hypothetical issue tracker does not justify a universal tracker framework. The interface is
only the fields required by the observed local-document and issue variants; additional adapters
need later evidence.

### 6.6 Approval, effect, and artifact invariants

- Only the identified authority may set `approval.state: accepted`.
- Section decisions never imply whole-revision acceptance.
- Any meaning-changing revision invalidates prior acceptance.
- Acceptance and delivery are independent state dimensions.
- Plan readiness is computed from field invariants, not from document style or external labels.
- The bytes or structured fields shown for acceptance are the same revision recorded as accepted.
- The bytes sent to an authorized remote destination are the accepted or explicitly requested draft
  bytes after required redaction; re-rendering after review must trigger revalidation.
- Every externally visible effect has an individual allow/deny decision. A grant for an issue does
  not grant a label, commit, archive sync, reviewer, browser, worktree, or agent.
- Tool availability and pre-approval do not widen effect authority.
- A failed effect leaves enough information for manual recovery and never fabricates success.

### 6.7 Uncertainty, degradation, and errors

The module returns named errors rather than generic refusal:

| Error class | Required result |
|---|---|
| `missing_intent_authority` | Draft allowed; acceptance blocked; exact authority needed is named |
| `blocking_ambiguity` | Ask one focused question when interactive, otherwise return `blocked` with affected fields |
| `evidence_conflict` | Preserve both claims and anchors; route ruling to the correct user/stakeholder authority |
| `unsupported_current_state` | Mark claim inferred/unavailable; do not elevate it into a requirement |
| `acceptance_unobservable` | Keep draft non-ready and name criterion needing an observable outcome/measure |
| `stale_approval` | Set new revision non-accepted and preserve prior accepted revision reference |
| `delivery_unauthorized` | Do not call adapter; return accepted/draft artifact with `delivery.result: not_attempted` |
| `delivery_unavailable` | Preserve artifact; record prerequisite and exact failure; offer manual copy only |
| `external_review_unavailable` | Skip only with explicit authority or stop that optional path; never invent a score |
| `redaction_blocked` | Prevent remote/persistent sink for the affected bytes until the user edits at source |
| `peer_unavailable` | Retain artifact and suggested manual next step; never redirect to another peer |

### 6.8 Hypotheses still requiring comparison

- Whether one mode router preserves source-specific pacing better than explicit user-selected modes.
- Whether section-by-section approval plus one whole-revision gate is enough, or whether high-risk
  specifications need an additional authority-scope confirmation.
- Whether the exact artifact has too many fields for small changes and needs a lossless compact
  rendering while preserving the same structured contract.
- Whether external review should remain only a manual bridge or become an optional adapter after
  Critique profile reconciliation.
- Whether visual presentation improves material decision recall enough to justify its dependency
  and effect surface.
- Whether issue and local-document adapters share enough behavior for one delivery seam without
  hiding source-specific labels, archives, or path rules.

---

## 7. Dependencies and delivery shape

### 7.1 Separate dependencies by category

| Dependency category | Dependency | Relationship to future Spec | Failure / authority rule |
|---|---|---|---|
| In-process | artifact compiler, gate validator, question state, alternative and revision logic | Internal modules behind the public interface | Candidate must be self-contained before any source retirement |
| Local-substitutable | repository read/search; Git history; local rendering; redaction engine | Read through bounded adapters; alternatives may substitute if equivalent evidence is visible | Missing tools reduce evidence or delivery, never acceptance authority |
| Local-substitutable | Node, local HTTP/WebSocket server, browser opener, temp/project visual files | Optional Brainstorming visual adapter only | Explicit opt-in; text fallback; no silent project write |
| Remote-owned through a port | GitHub or configured issue tracker, labels, dedupe search | Optional issue-delivery adapter | Separate authorization for issue and label; return verified URL/result or exact failure |
| Remote-owned through a port | external Codex/Claude reviewer | Optional external-review bridge, not Spec judgment | Explicit dispatch authority; unavailable reviewer never becomes simulated self-review |
| True external | user/stakeholder acceptance authority | Supplies decisions and whole-revision acceptance | Cannot be mocked or inferred in production behavior |
| True external | stakeholder documents, Jira tickets, production observations | Evidence inputs through an evidence adapter | Provenance/certainty required; source absence remains visible |
| Separate source runtime | gstack preamble/binaries/config, Bun, `gh`/`glab`, Claude CLI/worktrees | Needed only by exact `/spec` bridge | Not absorbed into public Spec core; source-specific effects remain visible |
| Separate source runtime | Specify CLI, speckit skills, Jira MCP, `/sdd` artifact layout | Needed only by retained `/sdd` bridge | Never auto-install/init from Spec |

### 7.2 Relation vocabulary

- **R — roster relation:** ownership, trigger, or authority boundary; no artifact use implied.
- **I — information relation:** one peer's artifact/capability is consumed after the user supplies or
  authorizes it; no workflow invocation implied.
- **H — handoff relation:** a user-mediated suggestion/capsule names the next peer; the destination
  remains uninvoked.
- **P — provenance relation:** source overlap or source-native routing that must be reconciled; it is
  not permission to reproduce the edge.

### 7.3 Precise relations with all seven peers

| Peer | Exact R / I / H / P relation | Minimum information crossing | Who starts the next workflow | If unavailable |
|---|---|---|---|---|
| `astra-critique` | **R:** Critique judges; Spec authors accepted intent. **I:** Critique may inspect a user-supplied spec. **H inbound:** only `specification-gap-or-ambiguity`. **P:** assigned sources contain separate reviewer behavior | H uses Critique common envelope plus the two destination-only fields below; no solution or success criteria | User chooses zero or one Critique route, then separately starts Spec; Spec never starts Critique | Critique report/candidate remains; Spec may be invoked manually with the common problem facts, but no fabricated capsule |
| `astra-understand-code` | **R:** Understand reports existing behavior; Spec decides desired behavior. **I inbound:** observed modules/flows, interfaces, seams, invariants, compatibility constraints, anchors, certainty, and gaps | Understanding artifact/ref, relevant claim IDs, evidence anchors, certainty/conflicts | User starts Understand and later supplies its result to Spec | Spec marks current-state evidence unavailable/inferred or blocks the affected decision; it does not invoke Understand |
| `astra-plan` | **R:** Plan owns executable decomposition and planning approval. **I outbound:** only an artifact passing section 2.5.7. **P:** Brainstorming terminal writing-plans and `sdd` Plan phase | Entire Accepted Specification identity/revision, approval record, intent, scope, requirements, criteria, technical constraints, uncertainty, and acceptance map | User starts Plan after Spec stops | Accepted artifact remains useful; Spec names Plan unavailable/manual planning prerequisite and does not broaden itself |
| `astra-implement` | **R only at runtime:** Implement mutates from an approved Plan; no direct Spec workflow edge. **P:** gstack agent spawn and `sdd` Implement phase are source effects excluded here | No direct packet. The approved Plan may carry the accepted `spec_id`/`revision` and acceptance map | User starts Implement under its own approval gate | Spec does nothing; no direct fallback or agent dispatch |
| `astra-test` | **R:** Test proves but does not decide behavior. **I outbound:** accepted requirements, criteria, negative cases, compatibility, evidence-method classes. **I inbound:** contract/server disagreement or test evidence that challenges intent. **P:** source templates include testing decisions | Spec→Test: accepted `spec_id`/`revision`, criterion IDs and expected behavior. Test→Spec: evidence packet/ref, affected criterion IDs, observed mismatch, certainty | User starts either workflow and supplies the artifact | Spec keeps acceptance contract; unavailable proof is a readiness/dependency fact, not permission to weaken criteria |
| `astra-debug` | **R:** Debug diagnoses; Spec revises desired behavior. **I inbound:** diagnosed cause/evidence showing requirement ambiguity or mismatch | Debug evidence ref, affected requirement/criterion IDs if known, observed-versus-expected distinction, certainty | User starts Debug, then chooses whether Spec revision begins | Existing spec remains; unresolved causal claim is recorded as inferred/unavailable, not rewritten as intent |
| `astra-ship` | **R:** Ship owns commit/PR/publication; Spec owns no VCS effect. **I outbound, optional:** accepted spec identity, approval record, acceptance map, and delivery refs for traceability. **P:** gstack issue-close integration and `sdd` Issues/PR phase | `spec_id`, accepted `revision`, `approval.decision_ref`, requirement/criterion map, existing issue ref; no command or release instruction | User starts Ship under Ship's own gate | Specification and local delivery remain; no PR, close, commit, or release is attempted |

No relation above is implicit invocation. `I` is artifact-mediated; `H` is user-mediated; `P` records
source history; `R` preserves ownership.

#### Critique destination profile owned by Spec

**Accepted problem class:** `specification-gap-or-ambiguity` — a surviving Critique finding shows
that desired behavior, scope, acceptance, or revision authority is missing, ambiguous,
contradictory, unobservable, or stale. Critique may identify the problem but cannot author the
replacement requirement or acceptance criterion.

Critique's common envelope already carries `destination_skill`, `why_this_skill`, `invocation`,
`artifact`, `agenda`, `problem_statement`, `finding_ids`, `evidence`, `observed_impact`,
`affected_scope`, `constraints`, `open_decisions`, `prerequisites`, and `context_gaps`. The
`destination_payload` for Spec must contain **only**:

| Spec-only field | Allowed values / meaning |
|---|---|
| `specification_area` | `intent`, `scope`, `requirement`, `acceptance`, or `approval_revision` |
| `gap_kind` | `missing`, `ambiguous`, `conflicting`, `unobservable`, or `stale_authority` |

Those fields classify the destination's work; they do not repeat the common problem, evidence,
scope, constraints, decisions, prerequisites, or context. They contain no proposed remedy,
implementation direction, tool choice, or Critique-authored success criterion. The user selects
zero or one immediate route. Unselected routes remain in the Critique report. A missing or
inconsistent reconciled profile prevents capsule emission and never narrows Critique's review
scope.

### 7.4 Delivery shape and self-containment

The proposed final package is one public `SKILL.md`-equivalent interface plus directly selected,
one-level references for the artifact schema, mode playbooks, and delivery adapter contracts if
later token evidence justifies them. No nested public skills or recursive support-file chaining are
proposed. Internal adapters are selected by mode and explicit authority, not discovered as peer
skills.

Final self-containment requires re-expressing every retained authoring protocol and delivery
contract needed by the candidate. Reading installed Brainstorming, gstack, or `to-spec` bodies at
runtime would make a reference convener, not a final candidate. The retained `sdd` reference is
different: it remains independently invocable and is not a hidden runtime dependency for normal
Spec behavior. Its principles can be re-expressed only to the degree accepted by the later
reference/retirement decision.

### 7.5 Deferred general-purpose concerns as manual/external bridges only

| Deferred concern | Honest boundary for this design |
|---|---|
| Context | User supplies conversation/repository/evidence refs; current source-specific local context stores remain external |
| Guard | Host/sandbox/redaction tools may protect effects, but Spec's effect invariants remain explicit and no Guard peer is implemented |
| Delegate | gstack agent spawn and reviewer dispatch remain external and separately authorized; no delegation module exists here |
| Automate | Speckit command routing, issue labels, and source-native pipelines remain manual/external; Spec does not auto-chain them |
| Incident | Operational evidence may enter through Debug/Test artifacts; incident coordination remains external |
| Deploy | Deployment constraints may appear in accepted intent, but deployment execution remains external and uninvoked |

### 7.6 Provenance relations that require coordinator reconciliation

- Brainstorming's terminal writing-plans edge is **P** to Plan, not an `H` or invocation contract.
- gstack `spec`'s agent spawn is **P** to Implement/Delegate behavior and must not become a direct
  Spec→Implement edge.
- gstack `spec`'s issue-close-on-merge behavior is **P** to Ship; Ship's own design decides whether
  it consumes issue refs.
- `spec` and Brainstorming independent review behavior is **P** to Critique, but does not prove
  Critique equivalence or authorize automatic Critique invocation.
- `to-spec` and `spec` testing sections are **P** to Test; accepted criteria cross as `I`, while
  test construction remains separate.
- Retained `sdd` names several workflow commands; those are source-native routes, not Astra edges.

---

## 8. Manual bridge

No current source emits the exact section 2.5 artifact or enforces its non-inference gate. The safest
current bridge is explicit normalization around one selected source, not a chain that silently
inherits every source effect.

### 8.1 Choose one source-native authoring path

1. **Ambiguous or exploratory intent:** invoke `superpowers:brainstorming`. Tell it up front:
   “Produce the approved specification content only; use my chosen destination if I authorize one;
   do not commit; stop before invoking writing-plans.” The source still performs its dialogue and
   staged approval. If a visual question genuinely benefits, separately approve the visual
   companion; otherwise stay textual.
2. **Already-rich conversation:** invoke `/to-spec` only after explicitly authorizing the named
   issue tracker and `ready-for-agent` label. If no tracker vocabulary is configured, stop rather
   than invoke setup implicitly. Although the source says “no interview,” answer its seam-confirmation
   question; unresolved acceptance gaps remain blockers.
3. **Backlog interrogation with GitHub delivery:** only after authorizing issue creation and local
   archive, invoke `/spec --no-execute --no-gate --no-dedupe`. This avoids agent spawn, Codex review,
   and dedupe search; redaction still runs and issue/archive effects remain. Decline any unrelated
   one-time gstack routing, commit, browser, sync, or configuration effect unless separately wanted.
   If external Codex review is desired, omit `--no-gate` only after granting that dispatch.

Do not run all three by default. Select the source whose home jurisdiction matches the input; extra
runs add conflicting policy and effects, not automatically better specification.

### 8.2 Normalize the result and obtain explicit acceptance

After the chosen source returns:

1. Manually map its output into every field in section 2.5, using empty lists and explicit `null`
   rather than omission.
2. Remove task order, files-to-change, implementation commands, effort, rollout, and other Plan
   content while retaining evidence-backed technical constraints.
3. Mark unsupported current-state claims as inferred or unavailable.
4. Ask the authorized user to review the exact revision and answer an explicit whole-revision
   accept / request-changes / reject decision.
5. Record the decision reference, accepted revision, blocking questions, and acceptance map.
6. Stop. The user may then manually start Plan, Critique, Test, or another peer.

### 8.3 Retained SDD navigator bridge

For a project already using speckit, invoke `/sdd` with the explicit instruction:

> Report status and the next source-native command only. If installation, update, `specify init`,
> checklist generation/evaluation, file writes, or any external skill is required, stop and report
> the prerequisite; do not perform it.

Never use `/sdd update` or `/sdd upgrade` as part of the Spec bridge. If `/speckit.*`, Specify CLI,
`.specify/`, Jira input, or Jira MCP is missing, report that source prerequisite. The user may
authorize the independent source workflow separately. `/sdd` can identify that a spec should be
revised; it does not produce or accept the Astra artifact.

### 8.4 What the bridge cannot approximate

- One artifact schema with revision-bound approval and Plan-readable non-inference gates.
- A clean separation between accepted intent and every source's executable-detail preferences.
- Uniform per-effect authority across local document, issue, label, archive, browser, reviewer,
  worktree, and agent paths.
- Self-contained preservation of all three authoring protocols without reading originals.
- Automated evidence normalization from Understand Code, Test, or Debug packets.
- A reconciled Critique destination profile enforced at runtime.
- Proven positive advantage over the best source oracle.

---

## 9. Deferred implementation and validation

Phase 0 builds none of the systems, corpus, adapters, wrappers, or harness below.

### 9.1 Declared advantage and three comparison systems

| System | Definition | Eligible as final? |
|---|---|---|
| Source oracle | The preselected strongest unchanged authoring source for each corpus case; retained `/sdd` is the oracle only for its independent navigator jurisdiction | No; baseline only |
| Reference convener | A temporary wrapper that selects/coordinates unchanged authoring sources, normalizes their results into section 2.5, and enforces explicit effect/acceptance gates | No; breaks when originals are removed and is not self-contained |
| Self-contained candidate | Re-expresses the validated authoring protocols, artifact contract, authority rules, degradation, and authorized delivery adapters without reading installed authoring sources | Yes, only after every gate passes; retained `/sdd` remains independent unless the user later changes that disposition |

The declared advantage is decision integrity under mixed ambiguity and brownfield evidence. A
reference-convener win tests whether coordination/schema normalization helps. A later candidate
loss isolates an internalization failure rather than disproving the source combination.

### 9.2 Fixed corpus

The corpus must be frozen before comparison and include:

| Corpus class | Required cases |
|---|---|
| Brainstorming home | Vague greenfield behavior; small “obvious” change hiding one material assumption; visual state/flow choice where text and optional visual presentation can diverge |
| gstack `spec` home | Brownfield backlog item requiring repository evidence; issue-ready security/privacy constraint; audit/cleanup-shaped request; exact redaction sink case |
| `to-spec` home | Rich prior conversation with all decisions present; rich conversation with one hidden acceptance blocker; domain-glossary/ADR constraint |
| retained `sdd` home | Speckit project at Specify/Clarify/Plan boundary; production evidence requiring backward flow; missing speckit/Specify/Jira prerequisite; no authoring score assigned to this independent job |
| Claimed advantage combinations | Vague intent plus brownfield constraints; conversation plus conflicting current behavior; accepted revision challenged by Test/Debug/production evidence; accepted artifact with denied remote delivery |
| Expected divergence | User intent conflicts with current behavior; source recommends issue/label but user denies; external review score conflicts with user ruling; staged sections accepted but whole revision rejected; revision changed after acceptance |
| Expected convergence controls | Fully specified low-risk change with observable criteria; issue-ready change where all effects are authorized; no-op revision where evidence does not change intent |
| Prerequisite/effect failures | No repository; unavailable stakeholder authority; no Node/browser; no tracker/network/credentials; absent Codex/Bun/Claude/Git support; redaction HIGH finding; delivery succeeds but label fails; missing speckit/Jira |

Each source's home cases must include at least one successful path and one source-native degradation
or failure path. The corpus must preserve cases where the correct output is a non-accepted draft or
no effect.

### 9.3 Method and measures

Run the source oracle, reference convener, and self-contained candidate on identical intent,
evidence, prior revision, authority, and effect grants. Repeat deterministic-looking cases at least
three times to detect model variance. Randomize system order. Blind evaluators to system identity;
use multiple evaluators for subjective measures and adjudicate against a pre-written decision key.

Measure at least:

- material intent/scope/acceptance-decision recall;
- critical acceptance-criterion and negative-case recall;
- supported-claim precision and unsupported-claim rate;
- requirement-to-criterion traceability and artifact-schema completeness;
- source-unique supported questions, alternatives, decisions, and delivery behavior;
- invented requirement count and Plan-content leakage;
- approval false-positive rate, stale-revision acceptance rate, and Plan-readiness false positives;
- actionability for the user while remaining non-executable for Plan purposes;
- duplicate/noise load and redundant-question rate;
- mode, evidence-input, delivery-adapter, and Critique-route accuracy;
- unauthorized effect count, including issues, labels, files, commits, browser/server, reviewers,
  worktrees, agents, installs, peer starts, and external calls;
- degradation fidelity and fabricated-success count;
- reviewer agreement, user decision reversals after reading, cost, context tokens, and latency; and
- for retained `/sdd`, status/next-command accuracy and zero unauthorized mutation, scored
  separately from authoring advantage.

Matching a final recommendation is insufficient if a source-unique question, staged decision,
effect distinction, or informative conflict disappeared.

### 9.4 Gates and failure consequences

| Gate | Pass requirement | Consequence of failure |
|---|---|---|
| Home-jurisdiction non-regression | On every authoring source's home cases, candidate meets the source oracle on critical decision/criterion recall, supported precision, authority fidelity, and source-unique behavior within predeclared margins | Narrow or reject the merger/mode; source remains installed and not retirement-eligible |
| Coordination value | Reference convener beats the source oracle on at least one declared combination class for decision/criterion recall and artifact/approval integrity, with no material precision or authority loss | Reject the combined architecture; a unified name alone has no value |
| Positive advantage | Self-contained candidate also beats the best source oracle on at least one declared combination class and produces zero unauthorized effects | Withdraw the better-output claim or narrow the interface to non-regressing behavior |
| Internalization fidelity | Candidate matches the reference convener on source-unique questions, alternatives, decision records, artifact fields, delivery distinctions, degradation, and informative divergence | Rework extraction; no source retirement |
| Approval and peer-contract integrity | Zero false accepted revisions; zero Plan-ready artifacts that fail section 2.5.7; Critique capsules contain only reconciled common envelope plus the two Spec fields | Block implementation/roster reconciliation for the affected interface |
| Effect and delivery integrity | Zero unauthorized effect; every partial/failed effect is accurate and recoverable; acceptance remains independent | Remove or redesign the adapter; preserve original source |
| Retained-reference boundary | Candidate does not simulate `/sdd`, install/init speckit, mutate checklists, or convert source-native commands into implicit Astra edges | Keep `sdd` entirely outside the candidate and revise relation claims |

### 9.5 Source-specific retirement gates

No source becomes retirement-eligible in phase 0. Later, in addition to the common gates:

| Source | Additional gate before any retirement proposal |
|---|---|
| `superpowers:brainstorming` | Preserve question cadence, small-change hard gate, alternatives, staged presentation/approval, textual degradation, optional visual offer timing and delivery, inline review distinction, and explicit stop before Plan. Decide with the user whether design-doc commit and reviewer support artifact are preserved, reassigned, or intentionally dropped |
| `spec` | Preserve rigorous interrogation, brownfield evidence, scope discipline, quality/redaction behavior, every supported flag/degradation selected for Astra, issue/archive effect fidelity, and generated-template provenance. Agent spawn, worktree/stash, gstack onboarding/config, external Codex review, and Ship issue-close behavior require explicit preserve/reassign/drop decisions; none may disappear silently |
| `to-spec` | Preserve fast conversation synthesis, domain/ADR vocabulary, seam confirmation, full issue template value, tracker/label effects and failures, implicit-invocation prohibition, and setup prerequisite behavior or an explicit user-approved replacement/exclusion |
| `sdd` | Not retirement-eligible through this design because it is proposed retained independent. Any future proposal must separately preserve its workflow dashboard, backward routing, speckit/Jira/constitution/checklist semantics, commands, install/update/init effects, contradictions, and user-approved disposition |

All originals remain installed during design, corpus construction, comparison, tuning, and user
review. Only the user may approve retirement after source-specific characterization,
home-non-regression, positive advantage, internalization fidelity, dependency/effect checks, and
delivery-shape fidelity pass.

---

## 10. Provenance and open questions

### 10.1 Inspection summary

Inspected in full on 2026-08-03:

- `docs/design-requirements.md` and `docs/phase-0.md`;
- the Plan & spec, relation-vocabulary, Critique-topology, generated-source, and exact-tranche parts
  of `docs/design-roadmap.md`;
- assigned rows and reference-ledger schema/state in `docs/phase-0-ledgers.md`;
- relevant inventory, collision, plugin, and delivery sections in `README.md`;
- current `designs/astra-understand-code.md` and `designs/astra-test.md`;
- Spec/Plan/Implement/Test/Critique boundaries in `designs/astra-implement.md` and
  `designs/astra-critique.md`, including Critique's exact common envelope;
- the Codebase Design `SKILL.md` and `DEEPENING.md`, which supplied the
  module/interface/seam/adapter and dependency vocabulary used here;
- the complete Brainstorming skill bundle and installed plugin/remote registration;
- the full generated and authored gstack `spec` source, every placeholder it consumes, full
  generation/registration path, selected model overlay, and redaction taxonomy;
- the complete two-file `to-spec` bundle; and
- the complete `sdd` body, symlink delivery, marketplace registration boundary, and clean source
  repository provenance.

### 10.2 Immutable source-artifact index

| Source artifact | Immutable anchor |
|---|---|
| Superpowers plugin manifest | SHA-256 `b271065c5e906e73757b7f9c26f7c57bb662ee47a31ed479dc32fb253729a25c` |
| Brainstorming skill | SHA-256 `4a54a4858b99807f3155ed1614b2f116e35ea5c1b788e793f565dd837fd3891f` |
| Brainstorming metadata | SHA-256 `90585d2a09289aaff7eba1271596e8500c7328437b94839f2d39699a41689195` |
| Brainstorming reviewer prompt | SHA-256 `95a0a195de9d984be2fffa95bab16fc8c563bc296a9cfc5e9c29cb3ece0d7457` |
| Brainstorming visual guide | SHA-256 `60cbad29b9dd7eaf08da020e301c498a72230b2e13c1813fa967a135ffcc1d71` |
| Brainstorming scripts | `frame-template.html` `6a8a4e58bd6a`; `helper.js` `43c6d69954a4`; `server.cjs` `2d2961ea8d11`; `start-server.sh` `a4e5ae84275b`; `stop-server.sh` `0b5ccbbd57f6` |
| gstack repository | clean Git revision `a3259400a366593e0c909dd9ac3e59752efd2488` |
| gstack Spec generated / template | SHA-256 `7ad290d73bb3a2556963b80fc22d6ea7322045356be6e0fc858f6e3b271bbcc9` / `26b366c256f73336b0254d354f8971b24183060827ea43a260616b02b6191e0e` |
| gstack generator / resolver roots | generator `cd62a5046ee6`; registry `9e07dfe5a4ec`; PREAMBLE `d6e6e2f5cd68`; redaction `70c1d1ccf351`; patterns `2f8f7314ad5e` |
| `to-spec` skill / metadata | SHA-256 `267638edd513b5918de626ad5605d261952abb7428cb308869c663ca924e93e7` / `1c5b4d1e3d8e52287ef19cc2742fdbbfae1914ac75d33af3e4c8174f08cc55bb` |
| `sdd` repository / skill | clean revision `6abccfa5f83a82f2bff309228b956323a11e4d2a`; SHA-256 `652a1039fe72cb705841e7e7e4b58d0c981e77dbf2abb1d7b7bd887b935134cc` |
| `sdd` repository marketplace manifest | SHA-256 `8992866835bd21e2e213de359b51e29885f6217236a425f020a1e1acd7921780` |

### 10.3 Provenance caveats and observed source defects

- The installed Superpowers cache exposes version and a remote plugin id but no local Git history.
  Full file hashes, not an inferred upstream commit, anchor the inspected bundle (**O**).
- The current gstack repository is clean at the recorded revision, and the authoritative template
  plus every consumed generation input was inspected. The live generated file contains an exact
  duplicate PREAMBLE expansion caused by a placeholder token in explanatory prose (**O**). Any line
  anchor into generated bytes is unsafe without the recorded hash.
- `to-spec` has no repository-level revision in its installed personal bundle. Its two file hashes
  are the available immutable provenance (**O**).
- `sdd` is clean at the recorded `monster-prompt` revision, but the repository marketplace manifest
  does not register it. Its availability depends on the observed personal symlink (**O**).
- `sdd`'s read-only declaration conflicts with observed update/init/checklist-write instructions;
  authority resolution is a design prerequisite, not a documentation nit (**O**).
- No runtime characterization, corpus run, comparison system, or user disposition has occurred in
  phase 0 (**O** for absence in this work; future performance remains **U**).

### 10.4 Provisional decisions

- One deep authoring module with `discover`, `synthesize`, and `revise` modes is the smallest
  plausible interface (**I**).
- The exact Accepted Specification contract and non-inference gate in section 2.5 are proposed as
  the Spec→Plan information seam (**I**).
- `sdd` should remain an independent reference rather than be merged into the public Spec job
  (**I**, coordinator and user reconciliation required).
- Local-document and issue delivery justify one persistent-delivery seam with two real adapters;
  visual delivery justifies a separate text/visual presentation seam (**I**).
- Independent review and spawned agents remain external/manual rather than internal Spec modules
  (**I**).
- Critique handoff acceptance is `yes` only for the named problem class and two-field payload
  (**I**, coordinator must reconcile both designs).

### 10.5 Open authority and design questions

| Open question | Consequence if unresolved |
|---|---|
| Who may accept a specification when several stakeholders have partial authority? | `approval.authority_scope` cannot be validated; artifact remains non-accepted |
| Is a typed chat approval event enough for `decision_ref`, or must high-risk specs use a signed/external record? | Plan cannot implement one uniform acceptance gate across risk classes |
| Which fields may remain nonblocking in an accepted artifact? | Candidate may either over-block planning or let Plan infer product decisions |
| May issue creation and label application share one user grant? | Issue adapter risks unauthorized label mutation; default must remain separate grants |
| Should remote redaction be part of core delivery or an external Guard bridge? | Issue delivery cannot be retirement-safe until fail-closed behavior and dependency ownership are settled |
| Does visual presentation improve critical decision recall enough to retain? | Browser/server adapter remains source-specific and original stays installed |
| Should external review be a Spec adapter or only a user-mediated Critique route? | Reviewer prompt/Codex gate cannot be declared preserved or retired |
| Does the user accept `sdd` as retained independent and want a new reference-ledger row? | Collision and reference ledger proposals remain provisional |
| Which gstack source effects are intentional product value versus common preamble baggage? | `spec` cannot pass source-specific retirement fidelity |
| What compact rendering preserves every artifact field for small changes? | Interface may be correct but too costly or noisy; comparison must test lossless compaction |

### 10.6 Coordinator reconciliation required

The coordinator must reconcile:

1. the four collision-ledger proposals and the new retained-reference proposal;
2. the exact Spec/Plan ownership split and field-for-field artifact contract;
3. Understand Code, Test, Debug, and Ship information payloads against their peer designs;
4. the Critique problem class and two-field destination profile without duplicating common-envelope
   fields;
5. every **P** source edge so source-native commands do not become implicit Astra invocation; and
6. the exact eight-peer roster, with no deferred general-purpose concern promoted or absorbed.

Until that reconciliation, this design is `proposed`; every ledger row remains unresolved; every
original remains installed; and no source is eligible for retirement.

---

## 11. Six-skill reconciliation amendment

This section merges Plan's solution-facing authority into Spec while leaving repository delivery
planning with Implement. It fixes the surviving contract before the remaining relevant source
inventory is absorbed. Sections 1–10 retain their source evidence and validation obligations;
where their eight-peer terminology, `Accepted Specification` name, or Spec/Plan boundary
conflicts with this section, this section governs.

### 11.1 Public operation and modes

The one public operation is reconciled as:

```text
specify(Change Context) -> Specification Result
```

It supports four modes:

| Mode | Use | Required authority behavior |
|---|---|---|
| `discover` | Develop vague or greenfield intent | Ask one material question at a time and expose solution-significant choices |
| `synthesize` | Compile already-resolved intent | Avoid redundant questioning while preserving evidence and approval identity |
| `remediate` | Select and specify fixes for Critique findings | Dispose every in-scope Finding ID and consult Critique before approval |
| `revise` | Supersede an approved Specification after new evidence | Preserve prior revision identity, explain the change, and obtain fresh whole-revision approval |

The merged workflow is:

1. classify input authority, mode, artifact identities, and effect limits;
2. ground current state in supplied Critique, Understand Code, Test, repository, and historical
   Debug evidence without converting evidence into intent;
3. ask one material question at a time;
4. develop two or three viable solutions and recommend one;
5. obtain user decisions on solution-significant tradeoffs;
6. compile the complete Approved Change Specification draft;
7. invoke Understand Code's persistent consultant when the draft directly relies on an
   Understanding Report;
8. repair Understand Code `drift` inside the active draft or stop on `authority_gap`;
9. invoke Critique's persistent consultant when Critique authority is present;
10. repair Critique `drift` inside the active draft or stop on `authority_gap`;
11. present the complete revision for explicit whole-revision user approval; and
12. return an approved, draft, changes-requested, or fielded blocked result.

The conditional Understand Code gate receives the exact report and draft identities, revisions,
and hashes; the exact current-state claims the draft relies on; and any changed repository
evidence. It occurs after the complete draft and before the Critique gate so both determinations
bind the same proposed revision. Understand Code judges only whether the current-state
interpretation remains supported. Spec owns any in-authority draft repair; a stale, contradicted,
or too-narrow report returns `authority_gap` and stops approval. If the user continues, a new
immutable Specification cycle must use a new report or remove the reliance and independently
ground the affected fact.

Spec also exposes a narrow read-only `consult` mode to downstream peers. It checks whether a
roadmap, executed branch, Test packet, or publication claim remains inside the exact approved
behavior, constraints, freedoms, and conditional branches. It returns `pass`, `drift`, or
`authority_gap`; it cannot mutate the downstream artifact, approve it, or create a new branch.

### 11.2 Merged authority boundary

| Retained or absorbed by Spec | Transferred to Implement |
|---|---|
| Selected solution and rejected alternatives | Exact files, symbols, and repository baseline |
| Target behavior and interfaces | Concrete implementation and diagnostic tasks |
| Scope, non-goals, constraints, and invariants | Task dependency graph and repository delivery phases |
| Compatibility and semantic migration strategy | Exact commands, working directories, and evidence capture steps |
| Required semantic ordering | Execution mode, bounded agent assignments, and worktree choice |
| Positive, negative, and failure acceptance cases | Atomic commit boundaries and PR partitions |
| Finding-to-requirement traceability and explicit dispositions | Concrete stop, recovery, and rollback procedures |
| Approved conditional outcomes and implementation freedoms | Mutation progress, branch selection, checkpoint state, and execution evidence |

Spec may require `expand -> migrate -> contract`, but it must not choose which files or commits
realize those semantics. Repository task order, exact paths, implementation commands, agent
dispatch, effort estimates, worktree operations, commit sequencing, and rollback commands remain
forbidden prescriptions in the Approved Change Specification.

### 11.3 Approved Change Specification

The reconciled artifact name is **Approved Change Specification**. The section 2.5 Accepted
Specification fields remain the starting schema rather than discarded work. A later schema
revision must make these additions and renamings explicit:

- replace Plan-facing readiness language with Implement-facing delivery readiness;
- accept immutable Finding Set references instead of treating historical Debug packets as a
  separate public authority;
- add a complete list of `{finding_id, disposition, requirement_ids, criterion_ids}` for every
  in-scope Critique finding;
- represent required semantic ordering independently from repository task ordering;
- represent approved conditional branches with their hypothesis state, permitted outcome,
  constraints, acceptance criteria, and indeterminate behavior;
- distinguish required implementation freedoms from prohibited behavior; and
- retain immutable identity, content hash, approval record, inbound consultant determinations,
  evidence conflicts, open questions, rejected alternatives, and non-inference acceptance gates.

For critique-driven work, no in-scope finding may disappear. Each is `resolved-by-change`,
`accepted-risk`, `rejected-with-evidence`, `duplicate-of`, or `out-of-scope-with-owner`, with the
user-owned decisions recorded where required. Every `resolved-by-change` finding maps to at least
one requirement and observable acceptance criterion. The Critique consultant checks finding and
causal-obligation coverage; it does not select the solution.

Approval binds one exact Specification revision and content hash. A changed selected solution,
scope, required behavior, semantic order, criterion, constraint, branch, or freedom invalidates
the prior approval. Delivery metadata cannot silently change meaning-bearing fields.

### 11.4 Forward-only branch authority

Remediation may begin while causal evidence is incomplete only when the Specification contains a
closed decision envelope. For every live hypothesis it states what outcome is allowed if the
hypothesis is supported, contradicted, or remains indeterminate. Implement may execute only the
branch whose evidence is accepted by the Critique consultant and whose outcome is authorized by
the Spec consultant.

Evidence already represented by that envelope proceeds without returning to Spec. Evidence
outside every branch, evidence invalidating a Finding Set, or a new user-owned tradeoff returns
`authority_gap`. The active consultant cannot revise the Specification; a new approved revision
and immutable change cycle are required if the user continues.

### 11.5 Plan source preservation and deferred absorption

`astra-plan` is a superseded historical design. Its inspected sources, exact artifact reasoning,
dependency and effect analysis, fixtures, projections, and source-specific retirement gates
remain inputs to a later Spec/Implement source-allocation pass. This amendment does not yet:

- reassign or resolve any Plan collision row;
- decide source by source whether behavior becomes Spec-internal, Implement-internal, a retained
  reference, an adapter, or an excluded duplicate;
- claim preservation of Plan's complete authoring, execution, ticketing, tuning, or Wayfinder
  behavior; or
- build the consultant runtime, artifact schema, corpus, reference convener, or self-contained
  candidate.

The surviving Spec is therefore authority-complete for this policy checkpoint but deliberately
not yet fully fleshed out from all relevant sources.

## 12. 92-component source-expansion amendment

The user-approved census, source hashes, cross-stack equivalence evidence, and retirement gates
live in `docs/six-skill-source-absorption.md`. This design adopts ten new primary identifiers:
`feature-dev:feature-dev`, `feature-dev:code-architect`, `sdd`, `design-api`, `design-db`,
`mcp-builder`, `skill-creator`, `skill-creator:skill-creator`, `writing-great-skills`, and
`superpowers:writing-skills`.

Their material behavior becomes six internal specification profiles behind the Approved Change
Specification interface: feature development, lifecycle-state projection, API design, database
design, MCP design, and skill-artifact design. A profile may add domain fields and a separate
advisor context, but it must preserve selected and rejected alternatives, user-owned tradeoffs,
state transitions, interfaces, migrations, acceptance cases, provenance, missing prerequisites,
and source-specific failure behavior. `sdd` may project repository artifact state and the next
valid lifecycle entry; it does not create a seventh authority or grant setup/update effects.

`feature-dev:code-architect` remains a separately invocable advisor delivery shape. It may propose
architecture options but cannot select or approve them. Likewise, skill-scoped analyzers,
comparators, and graders inform the skill-artifact profile without approving the specification.
Only the user approves the complete specification revision.

OpenAPI documents, DDL and migration scripts, MCP server code, `SKILL.md` files, fixtures, and
evaluation programs are durable repository artifacts. Spec states their required behavior and
acceptance criteria; Implement owns writing them according to an approved Roadmap, and Test owns
independent evidence. No source-native generator crosses those boundaries merely because it was
bundled with a design workflow.

This amendment revises the Plan-source allocation proposed in section 11.5 but does not update or
resolve the coordinator ledger. No runtime profile, generated artifact, corpus, harness,
installation, publication, or retirement is created here.

## 13. Shared trigger and reporting amendment

This section and `docs/design-requirements.md` sections 7.11.6–7.11.7 supersede earlier
trigger-bearing Plan and Debug destinations without rewriting their historical evidence.
Explicit invocation never waives prerequisites. Implicit routing uses the exact rule
**earliest missing authority**. A compound request stops at this artifact or approval boundary;
later public workflows are listed but not invoked. `Understood, proceed` returns control only and
cannot start a public peer.

### 13.1 Public-entry partition

Greenfield intent may begin directly at Spec; Critique participates only when Finding or causal
authority genuinely belongs to the active cycle. A known Finding without an Approved Change
Specification enters Spec. Exact repository tasks, delivery ordering, and mutation remain
Implement authority.

“Turn this into an issue” enters Spec only when “this” is intent or specification content and the
separate issue-writing effect is authorized. The generic roadmap-to-ticket projection remains unowned.
A compound request stops after explicit whole-revision Specification approval;
Implement remains a non-invoked prospective stage until the user starts it.

### 13.2 Specification reporting map and approval

The Approved Change Specification maps its existing `supersedes_revision` plus the explicitly
referenced prior `spec_id` and `content_hash` to `reporting.supersedes_ref`; a missing prior hash
cannot be inferred. It adds `reporting.surfaces` and `reporting.open_decisions`, grounded in exact
requirements, criteria, decisions, alternatives, evidence, gaps, and approval state.

Spec emits a producer-owned `ReportEvent` at `artifact_completion`, `approval_request`,
`stage_boundary`, `status_request`, and `failure`. The `approval_request` occurs immediately before
whole-revision approval and carries every option ID, label, Spec-authored consequence, evidence
reference, and blocking state. The complete envelope is never hidden behind optional detail. If
Report is unavailable, Spec presents that envelope itself; other moments use the shared minimal
unavailable notice. `I(reporting)` changes presentation only. Spec alone records the answer
against the exact Specification revision and content hash.
