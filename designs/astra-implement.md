# Astra Implement — phase-0 design

**Date:** 2026-08-03, revised 2026-08-04 against four completed peer contracts · **Wave:** 3 ·
**Status:** `proposed`

**Six-skill reconciliation:** 2026-08-11 · owns immutable repository delivery-roadmap approval,
execution, atomic implementation commits, and the Execution Ledger

> **Authority.** `docs/design-requirements.md` governs this document; `docs/phase-0.md` owns
> phase scope and the global ledgers; `docs/design-roadmap.md` supplies the provisional roster and
> relations. The restored drafting handoff narrows the initial public tranche and the authority
> boundaries applied here. This is one per-skill design. It is not an implemented skill, changes no
> ledger, installs or removes nothing, and authorizes no source retirement.
>
> **Conformance.** Sections 1–10 map one-to-one and in order onto
> `docs/design-requirements.md` sections 7.1–7.10. Section 11 applies the six-skill contract in
> requirements section 7.11 and has normative precedence over conflicting pre-reconciliation
> Plan intake, checkpoint-commit, final-commit, or eight-peer wording. Section 9's comparison
> systems and source-specific gates remain evidence obligations.
>
> **Peer reconciliation, 2026-08-04.** The 2026-08-03 draft was written before any sibling contract
> existed, so its peer profiles were one-sided. Four are now complete —
> [`astra-spec`](astra-spec.md), [`astra-plan`](astra-plan.md), [`astra-test`](astra-test.md), and
> [`astra-understand-code`](astra-understand-code.md) — and each names `astra-implement` in its own
> relation table and ledger proposals. This revision adopts their side of every shared seam, replaces
> this document's private relation vocabulary with the roadmap vocabulary all four use, and answers
> the reconciliation obligations they left standing. Sections 2.3, 2.4, 3.4, 4.5, 5.5, 5.9, 7.2, 7.4,
> 8.3, 9.3, 9.4, 9.6, and 10 carry the changes. The pass also reread the already-published
> [`astra-critique`](astra-critique.md) contract and corrected section 7.4's destination payload
> against it. Only `astra-debug` and `astra-ship` remain unwritten, so those two relation rows stay
> provisional from this side only.
>
> **Certainty labels.** **O** = observed in an inspected artifact; **I** = inferred and still
> needing confirmation; **U** = unavailable.
>
> **Notation — `SDD` is not `sdd`.** Throughout this document, **SDD** abbreviates
> `superpowers:subagent-driven-development` (`cm-plan-and-spec-04`), an assigned occurrence of this
> design. It is **not** the live standalone skill `sdd` (`cm-plan-and-spec-07`), a speckit workflow
> navigator whose own description opens "SDD workflow navigator" and which is assigned to
> [`astra-spec`](astra-spec.md) §§3.1, 8.3. The two artifacts share no bytes, no home, and no
> disposition. The collision matters here because the `sdd` navigator sequences a speckit **Implement
> phase**, which `astra-spec` §7.3 records as a **P** relation to this design; section 7.2 accepts
> that provenance leg and section 8.3 states why no bridge routes through it.
>
> **Coordinator gap.** All seven collision-map rows assigned to this drafting pass remain
> `unclaimed` and `unassigned` in `docs/phase-0-ledgers.md` (**O**). Section 3.3 proposes the exact
> reconciliations, but only the phase-0 coordinator may apply them. The gap is reported rather than
> repaired here because the ledger already contains unrelated user work.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-implement` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhoods | Plan & spec (primary); mutation-oriented Code review cleanup (secondary) |
| User job | **When I want an Approved Change Specification mapped onto an exact, approved repository delivery roadmap and then executed as verified atomic commits without changing required behavior or publishing them.** |
| Critique handoff acceptance | **conditional** — see section 7.4 |
| Six-skill role | Produces and obtains approval for the immutable Delivery Roadmap, executes it, and records the separate Execution Ledger |

**The job expresses one outcome.** An approved repository delivery roadmap, atomic project
changes, focused verification evidence, and the final Test handoff are consecutive parts of
delivering one Approved Change Specification. Selecting the solution, changing required behavior,
independent acceptance, and publication remain different jobs with different owners.

**Name and promise.** `astra-implement` is intentionally a verb with a hard prerequisite: one
Approved Change Specification. It does not mean "take any software request to completion."
`astra-spec` decides *what* is required; Implement inspects the repository, plans and obtains
approval for *how this repository will deliver it*, then performs only those authorized
mutations; `astra-test` owns independent verification; `astra-critique` preserves finding and
causal authority; and `astra-ship` owns publication. These are flat peers.

The historical drafting tranche contained eight peers. The reconciled public stack contains
`astra-critique`, `astra-understand-code`, `astra-spec`, `astra-implement`, `astra-test`, and
`astra-ship`; Plan and Debug remain superseded source evidence. Context, Guard, Delegate,
Automate, Deploy, Incident, and other later roster candidates are not introduced by this design.

**Personal value: explicit.** The user selected `astra-implement` as one of exactly eight skills in
the initial public tranche and supplied a dedicated drafting handoff. The immediate value is
authority-safe execution: the user can approve a plan once, receive verified code changes, and know
that checkpoint commits, arbitrary delegation, and shipping did not appear merely because a source
workflow bundled them. `now` applies to completing this phase-0 contract; a runtime candidate remains
downstream of approved Plan and Test contracts and section 9's comparison gates.

---

## 2. Interface and scope

### 2.1 Requests that should trigger it

- "Plan delivery for and implement this Approved Change Specification."
- "Continue the next task in this approved Delivery Roadmap," when its immutable identity,
  Execution Ledger, and working base are available.
- "Implement this approved remediation specification," including its Finding IDs and conditional
  diagnostic branches.
- "Refine the code changed by this task without changing behavior," only when that cleanup is in the
  approved task or is a supported internal-review finding.

The intake can name one task or many. The number of tasks affects execution mode, not ownership.

### 2.2 Nearby requests that should not

| Request | Correct owner or prerequisite | Why it is outside Implement |
|---|---|---|
| "Build me feature X" with no approved change contract | `astra-spec` | Discovery, solution selection, required behavior, and acceptance precede delivery planning |
| "How does this subsystem work?" | `astra-understand-code` | Explanation and technical mapping are not mutation |
| "Why is this failing?" | `astra-critique diagnose` | Critique owns causal findings; Implement may execute only approved diagnostic branches |
| "Design the test strategy / bootstrap the suite" | `astra-test` | Test methodology and suite design are distinct authority |
| "Review this diff" or "simplify whatever I changed" without bounded authorization | `astra-critique` or a new plan | Review is read-only; open-ended cleanup silently expands scope |
| "Push, open a PR, merge, release, deploy, or publication cleanup" | `astra-ship` | These are publication or integration effects; Implement owns its approved atomic implementation commits |
| "Deploy this" or "handle the incident" | manual/external prerequisite; deferred peers | Deploy and Incident are outside the initial tranche |
| "Delegate this arbitrary job" | manual user coordination; general `astra-delegate` is deferred | Implement may dispatch only its own bounded task roles |

### 2.3 Required intake contract

An invocation must supply or make resolvable:

1. an **Approved Change Specification** identity, revision, content hash, and approval record;
2. its Finding IDs, requirements, acceptance criteria, semantic ordering, constraints,
   implementation freedoms, and conditional branches;
3. the repository and authorization needed to inspect its live baseline, including branch,
   worktree, dirty state, and protected pre-existing changes;
4. any user-supplied delivery constraints, including effect limits, language boundaries, PR
   dependencies, and line-count exceptions already decided;
5. the required Critique, Spec, and conditional Understand consultant artifacts and availability;
6. the authority to run read-only discovery and planning commands needed to make exact repository
   claims; and
7. an explicit acknowledgment that no mutation or implementation commit occurs before the user
   approves one immutable Delivery Roadmap version and its effect scope.

If items 1–3 are absent or stale, Implement stops before delivery planning. If an exact roadmap
would require a new solution, requirement, acceptance criterion, semantic branch, or test-policy
decision, it returns the gap to the owning authority rather than manufacturing it. After planning,
missing roadmap approval stops before mutation.

#### 2.3.1 Historical binding to the executable-Plan schema

The remainder of this subsection preserves the former eight-peer Plan/Implement mapping as source
evidence. Section 11 replaces it as the active six-skill intake contract; it is not a second
runtime entrance.

`astra-plan` section 2.6 now defines that intake field for field as `astra.plan.executable/v0`, and
its section 10.4 question 2 asks — as a blocking pre-implementation question — whether Implement
accepts the exact schema and the immutable-version rule. **This design accepts both**, with the
mapping below. The prose items above are retained as the human-readable statement of the same
requirement; where the two differ, the Plan field name governs.

| Intake item | Consumed `astra.plan.executable/v0` fields | Implement's stop condition |
|---|---|---|
| 1. Approved plan reference and approval state | `schema`, `plan_id`, `plan_version`, `status`, `approval` | `schema` unrecognized, `status` not `approved`, `approval.approved_version` ≠ `plan_version`, or the mutation about to occur falls outside `approval.approved_effect_scope` |
| 2. Tasks, acceptance, order | `tasks[]`, `phases`, `dependency_edges`, `traceability` | An orphan task or requirement, or a dependency edge whose `kind` and `rationale` do not justify the ordering Implement is asked to break |
| 3. Mutation scope and forbidden effects | `scope`, `execution_policy`, `effect_ledger`, `tasks[].effects` | A required effect is absent from `execution_policy.allowed_effects`; every effect is denied by default |
| 4. Working base | `baseline` | `baseline.base_revision`, `dirty_state`, or `preexisting_changes` no longer match the live tree |
| 5. Verification | `verification_matrix`, `tasks[].verification`, `tasks[].test_cycle` | An obligation has no `command_ref_or_review`, or its `evidence_owner` is Test and no Test artifact was supplied |
| 6. Execution decision | `execution_decision` | `state` is `undecided`, or `mode` is `null`; Implement never promotes its own recommendation to an acceptance |
| 7. Isolation and checkpoint authority | `execution_decision.worktree_approval`, `execution_decision.checkpoint_commit_approval` | Task-dispatch or mixed mode is accepted without both approvals |

Three consequences follow from Plan's invariants and are binding here:

- **Immutable version.** Plan increments `plan_version` on any task, scope, effect, verification, or
  dependency change, and an approval applies to exactly one version and effect scope. Implement
  therefore pins the exact `plan_version` at intake, re-checks it before each task, and stops on
  drift rather than continuing against a superseded plan. It never edits the artifact to resolve
  the mismatch.
- **`checkpoint_policy` is advisory.** Plan states that `tasks[].checkpoint_policy` is "never commit
  authorization" (**O**). Implement reads it as a hint about checkpoint content only; the authority
  comes from `execution_decision.checkpoint_commit_approval` and section 6.5.
- **Non-blocking gaps stay visible.** `gaps[]` entries whose `blocking` flag is false are carried
  into the section 2.4 handoff unchanged. Implement does not close, resolve, or silently drop a Plan
  gap.

#### 2.3.2 Progress state belongs to Implement

Plan's `change_policy.progress_state_owner` names Implement, and Plan's own section 7.1 forbids it
to perform any "progress update" (**O**). This design accepts that ownership and answers the second
half of Plan's question 2 — which fields are *not* Plan's — as follows. Implement's plan ledger
(section 6.2) owns, and the Plan artifact never records:

per-task state (`DONE`, `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, `BLOCKED`); the mode actually used
for each segment; recorded task `BASE`/`HEAD`; checkpoint commit identifiers; verification runs with
their exact commands, outcomes, and evidence; internal review findings, repair rounds, and
dispositions; deviations and the user decisions that authorized them; the resume cursor after an
interruption; and the live dirty-state delta against `baseline`.

This state is reported in the section 2.4 handoff. It is never written back into the Plan artifact,
because a revision after execution begins cannot rewrite the approved historical plan
(`astra-plan` section 3.5). If the user wants the plan changed, Plan issues a new `plan_version`
and the user re-approves it; Implement then re-enters intake against that version.

### 2.4 User-visible result

The result is an **Approved Delivery Roadmap**, its separate **Execution Ledger**, verified atomic
implementation commits, any explicitly reported uncommitted blocked/incomplete residue, focused
verification evidence, and a revision-bound Test handoff—not a shipped change. Together they
contain:

- the exact Specification identity/revision/hash, Roadmap identity/version/hash, and live baseline;
- completed, skipped, changed, and blocked task states;
- files changed and a concise behavioral summary;
- the exact verification commands, outcomes, and relevant failure evidence;
- deviations from the plan and the user decisions that authorized them;
- internal-review findings and their disposition;
- every atomic implementation commit identifier and its task, requirement, and focused-check refs;
- remaining risks or external prerequisites; and
- the current branch/worktree state for an independent Test invocation.

The delivered revision plus its Execution Ledger is the primary implementation result. The
handoff must never imply that unrun checks passed, that focused implementation checks replace
independent Test evidence, or that Ship has started.

### 2.5 Non-goals

- Discovering or specifying a feature, selecting its solution, or revising an Approved Change
  Specification.
- General-purpose delegation or parallel swarming.
- Owning testing methodology, broad test-suite creation, or a health dashboard.
- Owning causal judgment; Critique's consultant evaluates diagnostic evidence on approved branches.
- Acting as the public, independent Critique surface.
- Changelog/version publication work, push, PR creation, merge, release, deploy, or publication
  cleanup. Implement does own the atomic implementation commits authorized by its Roadmap.
- Editing global Astra ledgers or retiring an original source during phase 0.

### 2.6 Decisions that remain with the user

The user approves the immutable Delivery Roadmap, mutation and commit scope, execution mode,
worktree use, any line-count exception, and PR dependency structure; resolves authority gaps;
accepts or rejects proposed repartitioning; decides whether failed or unavailable evidence permits
anything further; and decides whether to start Test or Ship afterward. A source workflow's bundled
tail never substitutes for those choices.

---

## 3. Source evidence

### 3.1 Inspection record

Inspected 2026-08-03. The Superpowers sources are from package release `6.2.0`; the gstack Health
template is at clean commit `a3259400a366593e0c909dd9ac3e59752efd2488`, release `1.60.1.0`.
Hashes are full SHA-256 unless shortened in prose.

**Assigned occurrence sources.** Inspection does not imply absorption.

| Ledger row and source | Delivery and inspected declaration | Material observed behavior | Availability / provenance |
|---|---|---|---|
| `cm-plan-and-spec-03` — `superpowers:executing-plans` | Skill, 64 lines; `c4c3d8b628c51114cd165fb8246fe02744cd8be180032328391252e653028d9b` | Requires a written plan, isolated workspace, critical preflight, exact task steps and verification; stops on blockers; sends completion into `finishing-a-development-branch` (`L3`, `L18–38`, `L40–64`) | **O**; plugin manifest reports `6.2.0` |
| `cm-plan-and-spec-04` — `superpowers:subagent-driven-development` | Skill plus three prompt files and three shell helpers; main file 503 lines; `349a08ad8b59b19b86c13a7d2f34a1a38719bf88257004a863eefefa8d9f9e40` | Fresh implementer per task, serial task dispatch, per-task commits, spec-and-quality review, five-round bounded repair, plan-scoped recovery ledger, final branch review, then finish/cleanup (`L8`, `L17`, `L56–106`, `L136`, `L238–423`) | **O**; plugin manifest reports `6.2.0` |
| `cm-plan-and-spec-12` — `implement` | Standalone skill, 15 lines; `6d3fd9e83b8f36e5213854779db49b256a457a7ebb4a503e53fa7dcff696adc3` | Takes a spec/ticket set, uses TDD at pre-agreed seams, runs focused and final checks, invokes code review, then unconditionally commits the current branch (`L2–15`) | **O**; `disable-model-invocation: true`; no version declaration inspected |
| `cm-plan-and-spec-15` — `feature-dev:feature-dev` | Command, 125 lines; `652e5d6264fd253fcb70c2f84de986a88d77109a02410aacd90230a6ab4bf557`; bundled with three agent declarations | Seven phases span discovery, code exploration, clarifying questions, parallel architecture options, user architecture approval, implementation, three quality reviews, and summary (`L20–119`) | **O** body; plugin manifest has no version and cache path is `unknown`; README's `1.0.0` claim is not manifest provenance |
| `cm-code-review-10` — `simplify` | Live Claude harness built-in; no path, manifest, or body in the inspected source inventory | The name suggests cleanup, but behavior, authority, delivery shape, and host-version pin cannot be verified | **U**; ledger and repository inventory explicitly mark bytes unavailable |
| `cm-code-review-11` — `code-simplifier` | Separate agent, 52 lines; `2a51e8d210580d9f66ac2ed1226c41f9374565fc275da30d7bb95f65c2cc87bb` | Proactively mutates recently modified code for clarity while preserving behavior; it normally acts without a new request (`L3`, `L9–11`, `L45–52`) | **O**; plugin manifest reports `1.0.0` |
| `cm-code-review-12` — `health` | Generated skill, 1,076 lines; authored template 320 lines, `faf103f39b2a3e42192b476ec09778ab9300942ed12ae1f832a9018c4ec19b9d` | Detects and runs project quality tools sequentially, computes a dashboard and trends, and has a hard gate never to fix findings; writes gstack history and may update Health Stack configuration (`template L35`, `L108–134`, `L229+`) | **O**; gstack generator/template provenance inspected |

**Live locator, invocation, availability, and declaration record.** Paths are the inspected live
locations, not proposed Astra package paths.

| Source | Live location | Current invocation / delivery | Availability and inspected declaration |
|---|---|---|---|
| `superpowers:executing-plans` | `~/.codex/plugins/cache/openai-curated-remote/superpowers/6.2.0/skills/executing-plans/SKILL.md` | `/superpowers:executing-plans <approved-plan>` | **O:** live skill; frontmatter declares `name: executing-plans` and written-plan execution; `agents/openai.yaml` supplies display metadata |
| `superpowers:subagent-driven-development` | `~/.codex/plugins/cache/openai-curated-remote/superpowers/6.2.0/skills/subagent-driven-development/` | `/superpowers:subagent-driven-development <approved-plan>`; skill dispatches separate agents and uses bundled scripts | **O:** live skill bundle; frontmatter declares plan execution with independent tasks in the current session |
| `implement` | `~/.agents/skills/implement/SKILL.md` | `/implement <spec-or-tickets>` | **O:** live skill; `disable-model-invocation: true` and OpenAI metadata sets implicit invocation false |
| `feature-dev:feature-dev` | `~/.claude/plugins/cache/claude-plugins-official/feature-dev/unknown/commands/feature-dev.md` | `/feature-dev:feature-dev [feature description]`; command launches bundled agents | **O:** live command; frontmatter declares guided feature development and optional argument; manifest declares command/agent bundle but no version |
| `simplify` | Claude harness built-in; no filesystem location | **U:** exact syntax and dispatch declaration were not available in the inspected bytes | **U:** listed live in repository inventory, but body, manifest, version, component declaration, and behavior are unavailable |
| `code-simplifier` | `~/.claude/plugins/cache/claude-plugins-official/code-simplifier/1.0.0/agents/code-simplifier.md` | host-dispatched `code-simplifier` agent; no user slash command declared | **O:** live separate agent; frontmatter declares `model: opus` and behavior-preserving simplification |
| `health` | active `~/.claude/skills/health/SKILL.md` resolves to `~/.claude/skills/gstack/health/SKILL.md` | `/health` | **O:** live generated skill; authored template declares `preamble-tier: 2`, `version: 1.0.0`, triggers, and Bash/Read/Write/Edit/Glob/Grep/AskUserQuestion tools |
| `cm-codebase-comprehension-03` — `codebase-design` reference | active `~/.claude/skills/codebase-design/SKILL.md` resolves to `~/.agents/skills/codebase-design/SKILL.md` | `/codebase-design` or explicit skill selection upstream | **O:** live retained skill; frontmatter declares deep-module design vocabulary |

**Bundled and supporting bodies inspected.**

| Bundle | Inspected bodies | Finding that affects this design |
|---|---|---|
| Subagent-driven development | `implementer-prompt.md` (142 lines, `94660161…`), `task-reviewer-prompt.md` (185, `e3b4a1bf…`), `re-review-prompt.md` (106, `e1d8e0e6…`), `review-package` (46, `fac3d4bd…`), `sdd-workspace` (40, `95a09d9d…`), `task-brief` (41, `d6954ef…`) | Implementer and reviewer are intentionally separate contexts; the reviewer is read-only and receives file artifacts, not controller history. Review ranges use the recorded task base, not `HEAD~1`, preserving multi-commit tasks. |
| Superpowers boundaries | `requesting-code-review/SKILL.md`, its `code-reviewer.md`, `using-git-worktrees/SKILL.md`, and `finishing-a-development-branch/SKILL.md` | Isolation and review are implementation prerequisites; finish owns merge/push/keep/cleanup choices. Astra assigns that finish tail to Ship rather than hiding it inside Implement. |
| Feature Dev | `code-explorer.md` (51 lines, `3b277703…`), `code-architect.md` (34, `c50fb08d…`), `code-reviewer.md` (46, `a7df173b…`), manifest and README | The command is a multi-role bundle, not an Implement alias. Agents are separate delivery shapes. Architecture choice and independent review belong outside Implement. |
| Retained technical-design reference | `codebase-design/SKILL.md` (114 lines, `a8d50abac5a4018f60e1d911d4b6f4e36454ca14d6c390c0695a578c7de65dad`) plus `DEEPENING.md` and `DESIGN-IT-TWICE.md` | Its deep-module vocabulary may constrain an approved plan, but Implement must not invoke it to reopen architecture. The existing ledger already retains it independently with Implement as a consumer. |

Two source-quality caveats are observed rather than normalized away:

1. all three SDD helper files currently have mode `0644`. `task-brief` and `review-package` attempt
   to execute `sdd-workspace` directly when no explicit output path is supplied, so their documented
   default path is not invocation-safe in the inspected installation (**O**); section 8 gives a
   non-mutating `bash` bridge;
2. Health's authored example runs `tsc --noEmit 2>&1 | tail -50` and then records `$?` without
   establishing `pipefail`, so the example can record `tail`'s status rather than the type checker's
   status (**O**). Health evidence is advisory until this protocol is characterized.

### 3.2 Disposition and contribution

| Source | Proposed disposition | Condensation categories | Contribution or reason |
|---|---|---|---|
| `superpowers:executing-plans` | proposed Astra design → `astra-implement` | **Protocol, Playbook, Prerequisite** | Sequential plan preflight, exact step execution, verification, isolation, and stop discipline |
| `superpowers:subagent-driven-development` | proposed Astra design → `astra-implement` | **Machinery, Protocol, Playbook, Prerequisite** | Bounded task-dispatch mode, plan-scoped recovery state, task review, repair loop, separate agents, and review packages |
| `implement` | proposed Astra design → `astra-implement` | **Protocol, Playbook** | Thin spec/ticket intake and regular focused/final verification; unconditional current-branch commit is rejected |
| `feature-dev:feature-dev` | **defer primary disposition** pending peer reconciliation | **Protocol, Jurisdiction, Separate** | Only phase 5 is Implement behavior. Phases 1–4 belong across Spec, Understand Code, and Plan; phase 6 is independent Critique; flattening the command would violate both jurisdiction and delivery shape. |
| `simplify` | **defer** | **Exclude** from the current candidate | Source bytes and declaration are unavailable; no absorption or preservation claim is supportable |
| `code-simplifier` | proposed Astra design → `astra-implement`, preserving the agent shape | **Playbook, Prerequisite** | Optional, bounded post-task refiner after explicit plan authorization or a supported internal finding; never autonomous over arbitrary recent work |
| `health` | **independent reference** | **Reference, Playbook, Separate** | Its user outcome is a report-only quality dashboard, not approved-plan mutation. Implement may consume a named report as advisory evidence. |
| `codebase-design` | no change: retained independent reference | **Reference, Playbook** | Implement consumes constraints already accepted into the plan; it does not own technical design |

### 3.3 Proposed ledger changes

These are paste-ready coordinator proposals, not applied changes:

| Occurrence | Proposed primary disposition | Proposed primary home | Proposed secondary role | Proposed claim status | Proposed evidence |
|---|---|---|---|---|---|
| `cm-plan-and-spec-03` | proposed Astra design | `astra-implement` | — | `claimed` by phase-0 coordinator | this design §§3.1–3.2, executing-plans full hash |
| `cm-plan-and-spec-04` | proposed Astra design | `astra-implement` | — | `claimed` by phase-0 coordinator | this design §§3.1–3.2, SDD bundle hashes |
| `cm-plan-and-spec-12` | proposed Astra design | `astra-implement` | — | `claimed` by phase-0 coordinator | this design §§3.1–3.2, standalone skill and metadata hashes |
| `cm-plan-and-spec-15` | defer | `unassigned` | phase 5 candidate for `astra-implement`; other phases require Spec / Understand Code / Plan / Critique reconciliation | `claimed` by phase-0 coordinator as a cross-peer item | this design §§3.1–3.2, command/agent/manifest hashes and version gap |
| `cm-code-review-10` | defer | `unassigned` | — | `claimed` by phase-0 coordinator as provenance-deferred | this design §§3.1–3.2, explicit **U** record |
| `cm-code-review-11` | proposed Astra design | `astra-implement` | separate internal refiner delivery shape | `claimed` by phase-0 coordinator | this design §§3.1–3.2, agent and manifest hashes |
| `cm-code-review-12` | independent reference | `retained independent` | `astra-implement` may consume a report | `claimed` by phase-0 coordinator | this design §§3.1–3.2, authored/generated/generator provenance |

If the Health disposition is accepted, add a reference/cleanup row for the live `health` skill with
`astra-implement` as a consumer and **user disposition pending**. Do not change the existing
`codebase-design` row; it already names `astra-implement` as a consumer. Do not add Feature Dev to
the reference ledger until the cross-peer disposition is decided.

Verified no-change occurrence: `cm-codebase-comprehension-03` has primary disposition
`independent reference`, primary home `retained independent`, secondary consumers
`astra-understand-code` and `astra-implement`, and reservation `claimed` (**O**). Its corresponding
reference-ledger row already contains both consumers, so this design proposes no duplicate update.

### 3.4 Occurrences owned by peers that name this design

The seven rows above are the only ledger changes *this* design proposes. Separately, four completed
peer contracts assign `astra-implement` a secondary role or a provenance leg on occurrences they
own. Those rows belong to the owning peer; what follows is this design's explicit acceptance,
qualification, or refusal, recorded so the coordinator can reconcile both sides against one page.

| Occurrence / source | Primary home | Role the peer assigns to `astra-implement` | This design's response |
|---|---|---|---|
| `cm-testing-01` / `tdd` | `astra-test` | Production-green half of TDD, artifact-mediated only | **Accepted.** Implement performs the minimal production change that turns a supplied red into green, inside an approved task. It does not confirm seams, author tests, or own the loop |
| `cm-testing-02` / `superpowers:test-driven-development` | `astra-test` | Production deletion, edit, and refactor effects, artifact-mediated only | **Accepted with the section 5.6 limit.** These are production-code effects only; test artifacts remain Test's. Refactor occurs only where the approved task or a supported internal finding authorizes it, with behavior locked by the task's checks |
| `cm-testing-05` / `nextjs-test` | `astra-test` | Production-change/fix half of the source loop | **Accepted with a narrowing.** `astra-test` records that the source "prefers fixing implementation on failure" (**O**). Implement repairs only when cause and fix are inside the approved task; otherwise section 6.7 stops or routes to Debug |
| `cm-testing-07` / `superpowers:verification-before-completion` | `astra-test` | May consume the required proving commands | **Accepted.** Its fresh-full-output rule strengthens the section 5.7 no-false-green invariant. `astra-test` classes reverting a production fix to obtain a red proof as external/manual or peer-owned; Implement performs such a revert only under an approved task or explicit user direction, never to manufacture evidence |
| `cm-plan-and-spec-02` / `superpowers:writing-plans` | `astra-plan` | Consumes only the approved Plan artifact, never this source | **Accepted.** Implement claims no writing-plans behavior. Section 8.1's bridge invokes `executing-plans`, not `writing-plans` |
| `cm-plan-and-spec-08` / `planb` | `astra-plan` (authoring slice) | Must **reconcile, not inherit,** execution and tracking semantics | **Answered in section 5.9.** Of nine execution and tracking behaviors, Implement claims two, refuses six, and claims one — phase review — only in a narrow sense. Five of the six refusals leave the behavior with no owner anywhere in the roster. It proposes no ledger change on this row |
| `cm-plan-and-spec-05` / `spec` | `astra-spec` | Spawned-agent effect excluded from Spec | **Accepted as exclusion, not as a claim.** Implement does not claim the gstack fresh-worktree agent spawn either. It remains unowned; see section 10.4 |
| `cm-plan-and-spec-07` / `sdd` | retained independent | None; `astra-spec` is the sole consuming design | **No consumer claim.** Implement records only the **P** relation covering the speckit Implement phase (section 7.2) and routes no bridge through it (section 8.3) |
| `cm-codebase-comprehension-03` / `codebase-design` | retained independent | Consuming design alongside `astra-understand-code` | **Accepted, unchanged.** Already verified above; no duplicate update proposed |

No peer proposes `astra-implement` as the primary home of an occurrence outside section 3.3, and this
design requests none. Acceptance here is evidence for the coordinator, not a second claim on a row
another design owns.

---

## 4. Collision analysis

### 4.1 Why these sources looked duplicative

`executing-plans`, SDD, `implement`, and Feature Dev phase 5 all mutate code from some description of
desired work. SDD, `implement`, Feature Dev, and Health all mention tests or review. `simplify`,
`code-simplifier`, and Health appeared together in the Code review neighborhood. Those are lexical
and lifecycle overlaps; they do not establish one public job.

### 4.2 What behavior is genuinely shared

The three primary execution sources share a small kernel: accept authorized work, make changes,
verify them, and report. `executing-plans` supplies plan fidelity and stop rules; SDD supplies durable
task state and role-separated review; the thin `implement` skill confirms regular focused checks and
a final suite. That kernel is coherent enough for one public Implement interface.

### 4.3 Aliases and shallow delegation

None of the inspected sources is a safe alias for another:

- `implement` is thin but adds an unconditional current-branch commit, which changes authority;
- SDD is not merely executing-plans with agents: it adds persisted plan-scoped artifacts, task-base
  review ranges, reviewer conflict handling, a five-round repair protocol, and per-task commits;
- `code-simplifier` is a proactive mutating agent, not a read-only reviewer;
- Health shares generated gstack chassis with other gstack skills, but its authored behavior is a
  dashboard, so chassis duplication is not merger value;
- Feature Dev is a user-facing lifecycle command whose phases cross four peer jurisdictions.

Astra Implement may internally dispatch implementer, task-reviewer, re-reviewer, and scoped-refiner
roles. That is not an alias to general Delegate and not authority to dispatch arbitrary jobs.

### 4.4 Apparent duplicates that are different jobs

| Source behavior | Distinct job |
|---|---|
| Feature Dev discovery, questions, architecture variants, and user selection | Spec / Understand Code / Plan, before approved-plan execution |
| Feature Dev's three post-implementation reviewers | Independent artifact judgment, belonging to Critique rather than the mutating controller |
| Health | Report on repository quality and trend history without fixing it |
| `codebase-design` | Vocabulary and comparison methods for choosing module boundaries |
| `finishing-a-development-branch` | Integration decision, push/PR, and cleanup, mapped to Ship |
| `simplify` | Unknown until source bytes and host provenance are available |

### 4.5 Conflicts that require an authority decision

1. The thin `implement` source says to commit the current branch; Astra allows checkpoint commits
   only in a user-approved isolated branch/worktree and only when task-dispatch mechanics require
   them.
2. SDD and executing-plans automatically continue into cleanup and/or branch finishing; Astra stops
   at an implementation handoff because Ship owns the tail.
3. `code-simplifier` is proactive by default; Astra makes it explicit and bounded to the current
   approved task.
4. Feature Dev can begin from vague intent and select architecture; Astra requires the accepted plan
   before mutation.
5. SDD's reviewer may identify a plan defect; Astra must return any plan-versus-finding conflict to
   the user rather than letting the controller or reviewer rewrite the plan.
6. Health is report-only and writes its own configuration/history; it cannot be re-described as an
   internal, side-effect-free verification adapter.
7. `planb` — owned by `astra-plan` as `cm-plan-and-spec-08` — mixes plan authoring with execution:
   it writes the plan file, creates host tasks, dispatches agents into a **shared** worktree, updates
   progress in place, runs phase reviews and advisor calls, and performs skip, abort, auto-fix, and
   live adaptation (**O**, `astra-plan` sections 3.1 and 3.3). Its bundled
   `references/parallel-execution.md` and shared-worktree dependency contradict both SDD's explicit
   one-implementer-at-a-time rule and this design's isolated-worktree requirement. `astra-plan`
   claims only the authoring slice and instructs this design to **reconcile, not inherit** the rest;
   section 5.9 is that reconciliation.
8. The `sdd` navigator sequences a speckit **Implement phase** (**O**, `astra-spec` sections 3.1 and
   7.3). It is proposed as a retained independent reference whose only consuming design is
   `astra-spec`. Its phase ordering therefore never becomes an entry point into this design; an
   approved Plan is the sole entry point, and section 8.3 routes no bridge through `/sdd`.

### 4.6 Why this is one coherent module

The module owns one irreversible transition: **approved plan → verified working-tree changes**. Plan
intake, task state, mutation, required verification, implementation-local review, and handoff all
serve that transition. Discovery, design, independent critique, final integration, publication, and
operation occur on different sides of the boundary and remain separate.

### 4.7 Declared positive advantage

**Advantage class: mixed-topology approved plans under constrained authority.** Some plans contain a
tightly coupled sequence that one executor should carry in context and other tasks independent
enough to benefit from fresh implementers and isolated review. The proposed skill maintains one
plan ledger while selecting sequential or task-dispatch mode per approved segment, then stops before
shipping. No inspected original combines mixed-mode recovery state with this commit/Ship authority
split (**I**, to be validated).

The claimed advantage is **coordination reliability and authority containment**, not superior coding
judgment. Against the strongest applicable original, the candidate should produce fewer skipped or
duplicated requirements after mode changes or context loss, preserve complete multi-commit task
review ranges, and cause zero unapproved commits or Ship effects. Optional scoped simplification is a
secondary hypothesis, not the reason the merger exists.

---

## 5. Preserved distinctions

### 5.1 Plan preflight versus execution

`executing-plans` critically reviews the plan before starting and stops on gaps, unclear
instructions, blockers, or repeated verification failures (**O**). Astra preserves that preflight.
It may identify a concern; it may not repair the plan by inference. Once preflight passes, task steps
and acceptance checks remain binding until the user approves a change.

### 5.2 Sequential and task-dispatch modes

Sequential mode preserves one executor's context for coupled work and does not require checkpoint
commits. Task-dispatch mode preserves SDD's fresh implementer per task, serial dispatch, separate
read-only task review, recorded task base, bounded repair loop, and recovery ledger. "Fresh per task"
does not mean parallel implementers; SDD explicitly forbids multiple implementers at once (**O**).

### 5.3 Internal roles and public Critique

An internal task reviewer checks one completed task against its approved brief and code-quality
criteria so defects do not cascade. It is an implementation-local gate and may initiate bounded
repairs. `astra-critique` remains a public, independent, read-only judgment surface with a
user-mediated handoff. Implement does not absorb it merely because Feature Dev and SDD contain
reviewer agents.

### 5.4 Checkpoint commits and final commits

SDD's per-task commits make durable recovery and exact review packages possible, including tasks
with multiple commits (**O**). Preserve them only in task-dispatch mode, only in a user-approved
isolated branch/worktree, and label them checkpoints. Sequential mode leaves normal working changes
uncommitted. Implement never rebases, squashes, writes a changelog, pushes, opens a PR, merges,
deletes a branch, or removes a worktree. Ship owns every finalization choice.

### 5.5 Verification and Test ownership

Implement executes the verification strategy named by the approved plan or Test artifact. It
preserves focused checks during work, the specified final suite, exact command/outcome evidence, and
TDD evidence at pre-agreed seams when the plan requires it. It does not invent project-wide testing
methodology, claim an unavailable suite passed, or turn Health's score into acceptance. A missing
strategy is an upstream gap, not permission to improvise one silently.

The split runs in both directions. `astra-test` assigns Implement the production half of the TDD
loop — the minimal change that turns a supplied red into green, plus production deletion, edit, and
refactor effects — and keeps test artifacts, seams, and adequacy judgment for itself (section 3.4).
Implement therefore owes Test a **return snapshot**: the changed base, the production scope actually
touched, focused-check results, and any required check it did not run. That return is user-mediated
and creates no invocation edge in either direction; section 7.2 records the full loop.

### 5.6 Function-preserving cleanup

`code-simplifier` contributes a distinct refiner role: improve clarity and consistency while
preserving behavior. Its separate-agent delivery shape and behavior-preservation invariant survive.
Its proactive scope does not. Astra dispatches it only for the current task, only after behavior is
covered by the task's acceptance checks, and only when the approved plan or a supported internal
finding authorizes cleanup. The same checks run afterward.

### 5.7 Failure states and evidence integrity

Preserve SDD's `DONE`, `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, and `BLOCKED` distinctions; the
five-round maximum for implementation-local repair; reviewer statements such as "cannot verify from
diff" as uncertainty rather than pass evidence; and exact base-to-head review packages. Preserve the
sequential source's earlier stop condition when a blocker makes further mutation unsafe.

### 5.8 Delivery shape and unavailable behavior

Implementer, task reviewer, re-reviewer, and scoped refiner remain separate agent contexts in
task-dispatch mode. Helper scripts remain scripts. A command bundle such as Feature Dev is not
flattened into prose. The unavailable `simplify` built-in remains provenance-deferred; Astra neither
claims its behavior nor claims to preserve it.

### 5.9 `planb` execution and tracking — reconciled, not inherited

`astra-plan` claims `planb`'s authoring slice and leaves this standing instruction on
`cm-plan-and-spec-08`: "`astra-implement` must reconcile, not inherit, execution/tracking
semantics." Its section 10.4 question 6 restates the same gap and warns that claiming the authoring
slice does not answer it. This section is the answer.

**What this section is not.** `planb` is not an assigned occurrence of this design and its bytes were
inspected by `astra-plan`, not here. Every statement below is a **jurisdiction** decision about the
behavior class, not a preservation claim over inspected behavior. Nothing here makes `planb`
retirement-eligible, and `astra-plan` separately records that its `examples.md` ends in a truncation
marker, so part of the source is not yet fully characterized (**O**).

| `planb` execution/tracking behavior | Implement's position | Basis |
|---|---|---|
| Task execution | **Claimed, as a behavior class.** Approved plan → verified working-tree changes is exactly this module's transition | Section 4.6 |
| Progress tracking | **Claimed, with a different medium.** Plan's `change_policy.progress_state_owner` names Implement, and section 2.3.2 enumerates the fields. Implement holds progress in its own ledger and reports it in the handoff | Section 2.3.2, `astra-plan` section 2.6 |
| Phase reviews | **Partially claimed, unsettled.** Implement will evaluate a `phases[].exit_gate` before advancing a segment. It does not claim `planb`'s phase-review agent shape or that review's authority to re-plan. Granularity — per task here, per phase there — must be compared against the source body before this is settled | Sections 5.3, 6.6; this design's section 10.4 question 7 |
| Plan-file writes | **Refused.** `plan_version` is immutable and a post-execution revision cannot rewrite the approved historical plan. Implement writes only ignored scratch artifacts | Section 6.5, `astra-plan` section 3.5 |
| Host task creation | **Refused.** Creating tracked host tasks is a separate delivery shape with its own effect surface. Implement's task state is internal and reported, not published | Sections 2.5, 6.5 |
| General subagent dispatch | **Refused.** Implement dispatches exactly four bounded roles — implementer, task reviewer, re-reviewer, scoped refiner — one mutating task at a time. `planb`'s general dispatch into a **shared** worktree is neither those roles nor a safe isolation model | Sections 4.3, 5.2, 6.2, 7.3 |
| Advisor calls | **Refused.** An advisory-agent facility is a general delegation surface. It belongs to the deferred Delegate concern, not to a bounded executor | Sections 2.5, 7.3 |
| Automatic fixes and skip/abort | **Refused as automatic behavior.** Repair happens only for a supported finding whose cause and fix are inside the approved task, under the bounded five-round protocol. Skipping or aborting a task is a user decision, recorded as a task state | Sections 6.6, 6.7 |
| Live plan adaptation | **Refused.** Implement may report that a plan is defective; it may not repair the plan by inference. Conflicts return to the user, who may obtain a new `plan_version` | Sections 5.1, 6.7 |

**What remains unowned.** Host task creation, advisor calls, general subagent dispatch, plan-file
writes, and live adaptation now have no proposed owner anywhere in the roster. That is the honest
state, not an oversight: `astra-plan` refused them, this design refuses them, and Delegate and
Automate are outside the initial tranche. `astra-plan`'s section 9.5 retirement gate already requires
each to be separately characterized, and `planb` cannot become retirement-eligible until they have a
tested, explicitly authorized home or the user approves deleting the delivery shape. This design
proposes no ledger change on that row.

---

## 6. Proposed skill design

### 6.1 Public shape

One public skill accepts an approved implementation plan and produces verified working-tree changes
plus an implementation handoff. Its interface is shallow: plan reference, allowed scope, execution
mode, and authority flags. Role prompts, task briefs, review packages, and recovery records are
internal artifacts rather than new public skills.

### 6.2 Internal modules

| Module | Responsibility | Explicit non-authority |
|---|---|---|
| Intake gate | Validate plan approval, tasks, scope, base, verification, and dirty-state preservation | Cannot approve or rewrite the plan |
| Plan ledger | Record every task, dependency, mode, base/head, verification, review, and concern | Cannot mark work complete without evidence |
| Mode selector | Choose sequential or task-dispatch per approved segment from section 6.3 | Cannot select a commit-producing mode without user approval |
| Sequential executor | Perform coupled tasks in order and run their checks | Cannot create checkpoint commits by default |
| Task dispatcher | Prepare bounded task briefs and dispatch one fresh implementer at a time | Cannot perform arbitrary delegation or parallel mutation |
| Evidence collector | Capture exact commands, results, and relevant logs | Cannot convert skipped/unavailable into passed |
| Task reviewer | Read-only spec-compliance and quality review of the recorded range | Cannot mutate or overrule the approved plan |
| Repair coordinator | Dispatch bounded repairs and scoped re-review, maximum five rounds | Controller does not fix code itself in dispatch mode |
| Scoped refiner | Optional behavior-preserving cleanup within the task | Cannot roam over all recently modified code |
| Handoff renderer | Produce the section 2.4 implementation handoff | Cannot invoke Ship or claim publication |

### 6.3 Mode selection

| Condition | Mode |
|---|---|
| Tasks share mutable state, require continuous context, or cannot be reviewed as independent ranges | sequential |
| Tasks have explicit boundaries and acceptance checks; separate agents are available; the user approved an isolated worktree and checkpoint commits | task-dispatch |
| Plan has both kinds and declares safe segment boundaries | mixed: one shared ledger, sequential execution within coupled segments, serial task dispatch for independent tasks |
| Agent capability is unavailable or checkpoint commits are not authorized | degrade to sequential; do not simulate task dispatch |
| Required isolation is absent for task-dispatch mode | stop and request the missing authority/workspace; do not commit in place |

The selector may recommend a mode, but mode-changing authority stays with the user. Mixed mode never
runs concurrent implementers and never changes mode inside a task.

### 6.4 Execution state machine

```text
approved plan
  → intake and dirty-state snapshot
  → critical plan preflight
  → user-resolved concerns
  → mode/segment selection
  → task brief
  → mutate
  → required verification
  → internal task review
  → bounded repair + re-review, or user decision on conflict
  → record task state
  → next task
  → final whole-plan verification/review
  → implementation handoff
  → stop
```

At every arrow, preserved pre-existing changes remain out of scope unless the plan expressly includes
them. A task that cannot be separated from unrelated dirty work stops rather than overwriting it.

### 6.5 Commit and effect authority

| Effect | Sequential | Task dispatch | Owner after Implement |
|---|---:|---:|---|
| Mutate plan-authorized project files | yes | yes, through bounded implementers | — |
| Write ignored plan/review scratch artifacts | optional | yes | Ship owns cleanup; Implement reports the path and leaves it in place |
| Create checkpoint commits | no | yes, only with prior isolated-worktree approval | — |
| Amend/squash/reorder final history | no | no | Ship |
| Changelog/version bump | no | no | Ship |
| Push/PR/merge/release/deploy | no | no | Ship or a later operational peer |
| Delete branch/worktree/source | no | no | explicit user-directed workflow only |

### 6.6 Review and repair protocol

For each dispatch-mode task, record `BASE` before implementation and `HEAD` after all implementer
commits. Review the entire `BASE..HEAD` range. Findings are evidence-backed and severity-calibrated.
Supported implementation findings enter a five-round maximum: rounds 1–3 may resume the implementer;
rounds 4–5 use a fresh implementer if available. Each repair gets a scoped re-review. A finding that
conflicts with the plan stops for the user. Residual load-bearing findings after round 5 yield
`BLOCKED`; non-load-bearing parked findings require explicit user acceptance.

Sequential mode may use the same review criteria without fabricating a commit range: review the
plan-scoped working diff against the captured base and pre-existing dirty snapshot. It does not create
commits merely to fit the dispatch protocol.

### 6.7 Degradation and stop behavior

| Condition | Behavior |
|---|---|
| Plan approval, scope, or acceptance checks are ambiguous | stop before mutation; request Plan/user resolution |
| Unknown root cause blocks the plan | stop and offer a destination-only Debug handoff |
| Required test tooling is missing | record exact failure; ask whether Test/Plan should amend the strategy |
| A verification fails once | investigate within the approved task; repair only if the cause and fix are in scope |
| Verification fails repeatedly or exposes a plan defect | stop; do not force through |
| Reviewer and plan conflict | return both claims and evidence to the user |
| Task agent unavailable | degrade to sequential if safe; otherwise `BLOCKED` |
| Scratch helper fails | use the manual bridge in section 8 or degrade to sequential; do not alter installed sources during phase 0 |
| No safe separation from pre-existing changes | stop and identify the overlapping files |
| Final checks are not green | return incomplete/blocked handoff; never say "implemented successfully" |

### 6.8 Architectural hypotheses

The public approved-plan boundary is settled for this draft; the following internals remain
hypotheses until section 9 runs:

- whether one ledger can safely span sequential and checkpoint-commit segments without producing an
  ambiguous handoff;
- whether mode selection should occur per plan, per dependency-connected segment, or only through an
  explicit Plan annotation;
- whether five repair rounds is the right invariant outside the source's native workflow;
- whether scoped `code-simplifier` dispatch adds measurable value beyond the task reviewer; and
- whether ignored in-tree scratch artifacts are the correct recovery medium for a self-contained
  candidate.

No shared Astra adapter or universal orchestration runtime is proposed. These seams are local to
Implement and correspond to observed variation between at least two execution sources.

---

## 7. Dependencies and delivery shape

### 7.1 External components that remain separate

- A git repository and, for task dispatch, a user-approved isolated branch/worktree.
- Project-native build, typecheck, lint, and test tools named by the plan/Test artifact.
- Separate implementer and reviewer agent contexts when dispatch mode is available.
- Script artifacts for plan-scoped scratch state and review packages; these are implementation aids,
  not public peer invocations.
- `codebase-design` as a retained independent reference already consumed upstream by Plan or
  Understand Code; Implement sees only accepted constraints.
- Health as a proposed independent reference. Its dashboard may inform a user decision but is not a
  hidden acceptance gate.

No server, hook, background runtime, or credential is observed as a home prerequisite. If a later
plan requires one, it is an external plan prerequisite with its own availability and authority gate;
Implement does not absorb it.

The deferred public skills Context, Guard, Delegate, Automate, Deploy, and Incident are not runtime
dependencies. Until their contracts exist, section 7.3 supplies manual prerequisites.

### 7.2 Flat-peer relations

**Relation vocabulary — corrected 2026-08-04.** The 2026-08-03 draft defined `R` as "consume an
artifact" and reserved `I` for the Ship boundary. That is a private vocabulary, and it collides with
the one all four completed peers use: `astra-spec` section 7.2, `astra-test` section 7.2,
`astra-understand-code` section 7.2, and `astra-plan` section 7.1 all carry the roadmap meanings.
Under the old letters, this design and its peers described the *same* edges with *swapped* codes,
which would have made the coordinator's reconciliation unreadable. This design now uses the roadmap
vocabulary:

- **R — roster relation:** ownership, trigger, or authority boundary. No artifact use is implied.
- **I — information relation:** a peer's artifact or capability is consumed after the user supplies
  or authorizes it. No workflow invocation is implied.
- **H — handoff relation:** Critique's zero-or-one user-selected problem capsule naming a
  destination. Reserved for Critique alone.
- **P — provenance relation:** source overlap or source-native routing that must be reconciled. It
  is not permission to reproduce the edge.

| Peer | Exact R / I / H / P relation and direction | Minimum information crossing the boundary | Who starts / unavailable behavior | Prohibition |
|---|---|---|---|---|
| `astra-spec` | **R:** Spec decides desired behavior; Implement mutates only from an approved Plan. No direct workflow edge in either direction. **P:** gstack `spec`'s fresh-worktree agent spawn and the `sdd` navigator's speckit Implement phase are source-native routes into implementation | No direct packet. The approved Plan carries `spec_ref` — `spec_id`, `revision`, `content_hash`, and the approval trace | User starts Implement under its own approval gate. If Spec is unavailable, Implement is unaffected while the Plan's `spec_ref` is complete | No requirement authorship, no agent spawn, no `/sdd`-driven entry, and neither **P** route may become a Spec → Implement edge |
| `astra-plan` | **R:** Plan describes; Implement mutates and owns progress. **I inbound, required:** the `astra.plan.executable/v0` artifact and its `handoff` object bearing `recipient: astra-implement` | Section 2.3.1's field mapping in full, plus the section 2.3.2 progress-state split | User approves an exact `plan_version` and separately starts Implement. If Plan is unavailable, a supplied artifact passing section 2.3.1 remains consumable; otherwise Implement stops | No plan authoring or editing, no acceptance of an `undecided` `execution_decision`, no execution against a superseded version, no Plan invocation |
| `astra-understand-code` | **R:** project-read-only explanation versus mutation authority. **I inbound, conditional:** Understand → Implement **directly only when an approved plan already owns the change**; otherwise the evidence must arrive through Plan | Code map, observed invariants, affected interfaces/seams, evidence anchors, accepted constraints, unresolved risks | User supplies the approved plan and starts Implement. If unavailable, no mutation occurs; Implement proceeds only where the plan is self-sufficient | No invocation; no use of an Understand artifact to widen scope past the approved plan; no reopening of architecture |
| `astra-test` | **R:** test-artifact authority versus production mutation. **I, bidirectional and user-mediated in both directions:** Test → Implement supplies red/failing evidence and required commands; **Implement → Test supplies the changed snapshot for green and final evidence.** `astra-test` section 7.3 states this is a visible loop, explicitly **not H**, and neither peer invokes the other | **Inbound:** accepted behavior; test IDs/files; seam; exact red/failing command and output; expected green; allowed production scope if already approved; snapshot/base. **Outbound:** changed snapshot and base, files changed, the production scope actually touched, focused-check results, and any required check Implement did not run | User starts each half. If Test is unavailable or its strategy is incomplete, Implement stops rather than inventing methodology. If Implement is unavailable, Test returns red evidence and stops | No test authoring or methodology invention; no editing test artifacts outside an approved task; no claim that an unrun check passed; no invocation in either direction |
| `astra-debug` | **I outbound, user-mediated** — corrected from the draft's `H`, since H is Critique's alone. Implement → user → Debug supplies a reproduction/evidence packet; Debug → user → Implement may return an accepted diagnosis the user converts into an approved bounded plan | Failing command and reproduction, relevant logs, last-known-good state, worktree/base, attempted in-scope fixes, and mutation constraints | User decides whether Debug starts. If unavailable, mark the plan task `BLOCKED` with evidence | No diagnosis from symptoms, no remediation without an approved plan, no invocation. The Debug contract does not exist, so this payload is provisional from this side only |
| `astra-critique` | **R:** implementation-local review versus public independent judgment. **H inbound, conditional:** Critique → user → Implement with section 7.4's `approved-code-remediation` capsule | Section 7.4's destination-only payload plus Critique's common envelope | User selects zero or one route. A missing or inconsistent profile remains a reconciliation gap, not a guessed payload | Implement never emits an internal reviewer result as public Critique and never invokes Critique |
| `astra-ship` | **R:** implementation handoff versus finalization and publication authority. **I outbound, user-mediated; never H:** Implement → user → Ship. `astra-plan` section 7.1 records the canonical route as Plan → user → Implement → user → Ship, with the Plan reference carried inside Implement's handoff | Section 2.4 handoff: task state, diff/files, checkpoints, verification evidence, findings, risks, and branch/worktree/base | User alone starts Ship. If unavailable or not selected, preserve and report current state | No commit shaping, changelog, version bump, push, PR, merge, release, deploy, cleanup, or Ship invocation |

**No row authorizes Implement to invoke a peer workflow.** The `astra-plan`, `astra-test`,
`astra-understand-code`, and `astra-spec` rows are now reconciled against the completed peer
contracts and match their side. The `astra-critique` row is reconciled differently: that contract
exists, and its section on destination profiles makes **this design** authoritative for the problem
class and payload it accepts, so what remains pending is the coordinator's reconciled snapshot, not
the peer's contract. Only the `astra-debug` and `astra-ship` rows are this design's proposed side
alone, because those two contracts do not exist yet; no absent peer contract is fabricated here.

### 7.3 Manual prerequisites for deferred peers

| Deferred concern | Manual prerequisite now |
|---|---|
| Context | Provide the approved plan, current task/ledger state, base/head, worktree path, dirty-state snapshot, and prior verification/review evidence at invocation or resume |
| Guard | State writable roots, forbidden files/effects, destructive-action rules, and whether checkpoint commits are authorized; host safety rules still apply |
| Delegate | The Implement controller may dispatch only the task implementer/reviewer/refiner roles defined here, one mutating task at a time; every other delegation returns to the user |
| Automate | Repeated execution remains manual; Implement does not create schedules, hooks, or background jobs |
| Deploy / Incident | Treat live environment access and operational actions as external; stop at the verified code handoff |

### 7.4 Critique handoff acceptance

**Accepts Critique handoff: conditional.** The owned problem class is **code remediation against a
user-approved plan**. Critique's report must retain all actionable findings and routes. The user may
select zero or one immediate capsule. Implement accepts that capsule only when it includes or
references an approved bounded remediation plan; otherwise Plan remains the destination and
Implement does not improvise the remedy.

**Payload corrected 2026-08-04.** The 2026-08-03 draft listed nine fields. Six of them —
`target_state`, `finding`, `expected_behavior`, `mutation_scope`, `evidence`, and `constraints` —
either duplicate Critique's common envelope or ask Critique to author something it is forbidden to
author. `astra-critique`'s problem/solution boundary states that a handoff "must not contain a
proposed design, remedy, implementation sequence, tool choice, or Critique-authored success
criteria" (**O**), and `expected_behavior` is precisely a success criterion. `astra-spec`,
`astra-plan`, and `astra-test` all converged on a compact two-or-three-field destination payload for
the same reason. This design now matches that pattern.

Critique owns the common envelope: `artifact`, `agenda`, `problem_statement`, `finding_ids`,
`evidence`, `observed_impact`, `affected_scope`, `constraints`, `open_decisions`, `prerequisites`,
and `context_gaps`. Implement must not restate any of them. The destination-only payload is exactly:

| Implement-only field | Allowed values / meaning |
|---|---|
| `problem_class` | Literal `approved-code-remediation` |
| `defect_locus` | Where the surviving finding lives: `production-code`, `task-scope`, `verification-evidence`, or `checkpoint-integrity`. Classification only |
| `remediation_authority` | Whether an approved bounded remediation plan already covers this defect: `approved-plan-exists`, `plan-required`, or `unknown` |

Acceptance rules:

1. Critique has already emitted its report with every candidate route retained.
2. The user selected zero or one route and explicitly selected `astra-implement`.
3. `remediation_authority` is `approved-plan-exists`, **and** the user supplies the plan reference
   and approval at invocation. Critique never authors, names, or approves that plan.
4. `plan-required` and `unknown` route to `astra-plan`, not here. Implement does not improvise the
   remedy, and a capsule alone never becomes mutation authority.
5. The payload contains no remedy, implementation sequence, tool choice, acceptance criterion, or
   duplicated common-envelope evidence. Everything the old table asked Critique for —
   target state, mutation scope, verification commands, expected behavior — arrives instead through
   the section 2.3 intake contract, from the approved Plan.

The handoff is always user-mediated. Critique never invokes Implement, and Implement does not send an
internal reviewer result back as if it were public Critique.

### 7.5 Ship handoff

Implement's section 2.4 artifact is sufficient for the user to start Ship without replaying the
implementation session. It records whether checkpoints exist, whether the tree is clean, exact test
evidence, unresolved findings, and the base/branch/worktree. Ship independently decides final commit
shape, changelog/version work, push, PR, merge, and cleanup. If no Ship invocation occurs, Implement
leaves state in place and reports it.

---

## 8. Manual bridge

No Astra runtime artifact is created in phase 0. The following current-source bridges approximate
the proposed behavior while keeping originals installed.

### 8.1 Sequential bridge

1. Manually create or select an isolated worktree when the plan's risk requires it; record all
   pre-existing changes.
2. Invoke the current source with the approved plan:

   ```text
   /superpowers:executing-plans path/to/approved-plan.md
   ```

3. Add an explicit session instruction: **execute tasks and verifications only; do not invoke
   `finishing-a-development-branch`, commit, push, merge, or clean up; return the Implement handoff.**
4. If the source tries to enter its required finishing tail, stop it and render section 2.4 instead.

This bridge is not equivalent to the candidate: the installed source declares the finish transition
mandatory, so authority containment depends on the manual instruction.

### 8.2 Task-dispatch bridge

Use only after the user approves an isolated branch/worktree and checkpoint commits:

```text
/superpowers:subagent-driven-development path/to/approved-plan.md
```

Add the same authority instruction, strengthened to **stop after final review and before deleting the
plan scratch workspace or invoking `finishing-a-development-branch`**. Preserve one implementer at a
time, the task reviewer, five-round limit, and exact task base. The current helper modes require this
invocation-safe shell sequence when manually generating artifacts:

```bash
SDD_SCRIPTS=/home/kurophoenix/.codex/plugins/cache/openai-curated-remote/superpowers/6.2.0/skills/subagent-driven-development/scripts
SDD_DIR=$(bash "$SDD_SCRIPTS/sdd-workspace" path/to/approved-plan.md)
bash "$SDD_SCRIPTS/task-brief" path/to/approved-plan.md 1 "$SDD_DIR/task-1-brief.md"
bash "$SDD_SCRIPTS/review-package" path/to/approved-plan.md BASE_SHA HEAD_SHA "$SDD_DIR/review-BASE..HEAD.diff"
```

Supplying explicit output paths is necessary in the inspected installation because the two helper
scripts otherwise execute non-executable `sdd-workspace` directly. This is a current manual bridge,
not a proposed permanent path or permission change.

### 8.3 Thin and secondary bridges

- `/implement` approximates thin execution from a spec/ticket set, but its unconditional current-
  branch commit violates this design. Use it only where an outer controller can stop before line 15
  and where an approved plan supplies the missing authority fields.
- The `code-simplifier` agent may be dispatched with an exact task diff, allowed files, behavior-
  preservation checks, and a prohibition on unrelated recent code. Never invoke its default
  proactive scope.
- `/health` remains a separate report-only invocation. Treat its output as advisory, and verify raw
  tool exit statuses independently until the pipeline example is corrected or characterized.
- `feature-dev:feature-dev` has no safe Implement-only entry point: invoking the command starts at
  discovery. Its phase 5 can be used as evidence, not as a standalone manual adapter.
- `/sdd` — the speckit workflow navigator, not SDD — is **not** part of any Implement bridge. It is
  `astra-spec`'s retained reference, and `astra-spec` section 8.3 already bounds it to reporting
  status and the next source-native command. Even though it sequences a speckit Implement phase,
  routing through it would make a navigator's phase ordering the entry point instead of an approved
  Plan. Sections 8.1 and 8.2 are the only execution bridges.

---

## 9. Deferred implementation and validation

No source removal, packaging, permission tuning, or implementation occurs in this phase. Later work
must compare three systems with originals still installed.

### 9.1 Declared advantage class

The primary comparison class is an approved plan containing both coupled and independent tasks,
with at least one session interruption or context restoration and with Ship authority withheld. The
candidate wins only if mixed-mode coordination improves task traceability or recovery while matching
the best original's home behavior and causing no authority expansion. A code-simplification subset
tests the secondary refiner hypothesis separately.

### 9.2 The three comparison systems

1. **Source oracle.** Preselect the strongest applicable original before seeing its output:
   `executing-plans` for coupled sequential work; SDD for independent task-dispatch work; thin
   `implement` for a small accepted ticket set; `code-simplifier` for already-authorized cleanup.
   Feature Dev and Health remain separate-oracle references for their own jobs. `simplify` cannot be
   an oracle until its bytes and version are available.
2. **Reference convener.** One temporary authority shim selects unchanged originals per approved
   plan segment, carries a shared ledger, constrains `code-simplifier`, and intercepts every
   finish/Ship transition. This isolates coordination value while preserving source bodies.
3. **Self-contained candidate.** The eventual Astra artifact internalizes the supported behavior and
   runs without reading or invoking the superseded originals. Retained references remain external by
   design.

### 9.3 Fixed corpus

The corpus must distinguish the checklist's five case families rather than treating all failures as
one score:

| Case family | Required comparison |
|---|---|
| Home jurisdiction | Sequential, task-dispatch, thin-ticket, and scoped-cleanup cases test each claimed source contribution on its strongest native job |
| Advantage | Mixed-topology and interruption/resume cases test the declared coordination win |
| Divergence | Plan/reviewer conflict, out-of-scope cleanup, dirty-file overlap, and withheld-commit cases test whether source protocols remain visibly different |
| Partial internalization | Every source slice this design **rejects rather than absorbs** gets its own case. A merger that quietly re-acquires a rejected slice under pressure has not preserved the boundary it claimed |
| Convergence | A simple plan executable by multiple originals tests whether all systems reach the same accepted behavior without invented distinctions |
| Prerequisite failure | Missing plan approval, isolation, agents, tests, tools, source bytes, or publication authority tests explicit stop/degradation behavior |

Include at least:

- a one-task accepted ticket and a tightly coupled multi-task plan;
- an independent multi-task plan with a task producing multiple checkpoint commits;
- a mixed coupled/independent plan with a compaction or resume between segments;
- an unrelated dirty working tree and a task overlapping one pre-existing modified file;
- a plan gap, an ambiguous instruction, and a reviewer finding that contradicts the plan;
- focused-test failure, repeated final-suite failure, and missing test tooling;
- agent unavailability, no isolated worktree, and checkpoint-commit authority withheld;
- a clarity cleanup with behavior-locking tests and one without adequate tests;
- an SDD helper invocation using default outputs in the current `0644` installation;
- a Health run where the left side of a pipeline fails but `tail` succeeds;
- vague Feature Dev intent that must route upstream rather than mutate;
- Critique capsules with and without an approved remediation plan; and
- a completed implementation where push, PR, merge, and cleanup authority are withheld.

**Partial-internalization cases.** Six of this design's seven sources are only partly absorbed, and
one peer-owned source carries a standing reconciliation instruction. Each rejected slice needs a case
that actively invites the candidate to re-acquire it:

- a request to commit the current branch the way thin `implement` does, with no isolated worktree and
  no checkpoint authority;
- a completed plan at the point where `executing-plans` treats the transition into
  `finishing-a-development-branch` as mandatory;
- an SDD run that reaches final review, testing whether the candidate stops before deleting the plan
  scratch workspace and before the finish tail;
- a `code-simplifier` dispatch offered over all recently modified code, including files outside the
  approved task;
- a Health run whose dashboard is then offered as an acceptance gate;
- vague Feature Dev intent offered as an Implement entry point, and a Feature Dev phase-6 reviewer
  result offered as public Critique;
- a `planb`-style request to update plan-file checkboxes or auto-fix during execution — the
  Implement-side mirror of `astra-plan` section 9.2 case 9;
- a `planb`-style request to dispatch parallel agents into a shared worktree, testing whether the
  candidate degrades to serial dispatch in isolation or stops;
- a `/sdd`-sequenced speckit implement phase offered as the entry point instead of an approved Plan;
- a Test-supplied green step whose production fix lies outside the approved task scope, testing
  whether the candidate inherits `nextjs-test`'s "prefer fixing implementation" preference;
- a plan re-issued mid-execution so the pinned `plan_version` goes stale; and
- a plan whose `execution_decision.state` is `undecided`, offered with a plausible mode
  recommendation.

### 9.4 Method and measures

Freeze plans, repositories, base revisions, dirty-state fixtures, user decisions, tool versions, and
expected acceptance checks. Run paired systems on identical artifacts and repeat trials where agent
or reviewer behavior can vary. Blind system identity and randomize presentation order for every
subjective review-quality or maintainability judgment; the candidate never grades itself. Record:

- plan-requirement recall and acceptance-criterion pass rate;
- critical plan-decision and implementation-defect recall;
- supported-finding precision, unsupported-finding rate, and source-unique supported findings;
- finding actionability, duplicate/noise load, and correct routing of out-of-scope problems;
- completed, skipped, duplicated, or out-of-order tasks;
- resume accuracy after interruption;
- correctness of task base/head and multi-commit review coverage;
- focused and final verification results, including false-green evidence;
- supported review findings resolved and unsupported findings introduced;
- behavior preservation after cleanup;
- out-of-scope files touched and pre-existing changes altered;
- unapproved commits, branch moves, pushes, PRs, merges, cleanup, or peer invocation;
- user interrupts required for real ambiguity versus avoidable prompts;
- rejected-slice re-acquisition rate across the partial-internalization cases;
- completeness of the return snapshot owed to Test, and of the `plan_version` staleness check;
- handoff completeness and accuracy; and
- wall time, token/tool cost, and reviewer rounds as secondary measures.

### 9.5 Gates and consequences

| Gate | Pass condition | Failure consequence |
|---|---|---|
| Characterization | Every claimed source behavior and source-specific failure is reproduced or explicitly rejected with evidence | Correct the design; no candidate implementation |
| Home-jurisdiction non-regression | Candidate matches the source oracle on plan fidelity, required checks, blocker handling, and applicable review quality | Split the regressing mode or retain its original |
| Positive coordination advantage | On the mixed/resume class, candidate beats the preselected source oracle on traceability/recovery with no worse acceptance or authority score | Retain separate sources or reduce the skill to routing; do not claim merger advantage |
| Internalization fidelity | Self-contained candidate matches the successful reference convener without reading/invoking superseded originals | Keep the convener/originals; candidate is not self-contained |
| Authority containment | Zero out-of-scope mutation, unauthorized checkpoint/final commit, Ship effect, arbitrary delegation, or silent plan rewrite | Hard fail; redesign authority gates |
| Delivery-shape fidelity | Dispatch mode keeps implementer/reviewer/refiner contexts separate and sequential mode works without pretending agents ran | Preserve components or split the design |
| Review/evidence integrity | Complete ranges, no false-green checks, uncertainty reported, and plan conflicts reach the user | Fix the evidence protocol before any rollout |
| Cleanup advantage | Authorized refiner improves agreed clarity measures while all behavior checks remain green and no unrelated file changes | Drop the refiner from Implement; retain the agent independently |
| Source-specific retirement | For each source, behavior, authority, prerequisites/dependencies, component delivery shape, degradation, provenance, internalization, and explicit user approval all pass; an unavailable source fails by definition | That original remains installed; no deletion or disablement |

Health and Feature Dev cannot fail Implement's home gate because this design does not claim their
whole jobs. They do have boundary tests: Implement must refuse to absorb their report/discovery
surfaces. Section 9.6 expands the final row above into per-source gates.

### 9.6 Source-specific retirement gates

`docs/design-requirements.md` section 7.9 requires a per-source retirement gate covering behavior,
authority, dependencies, delivery shape, degradation, and user approval, and all four completed peers
expand it into a section of its own. The single generic row in section 9.5 was not enough, because
this design internalizes most sources only in part. The pattern applied below is: **name the rejected
slice, give it a corpus case, and let it block retirement until it has an owner.** A slice with no
owner is not a slice that has been eliminated.

**`superpowers:executing-plans`:** preserve critical plan preflight and its stop-on-gap behavior,
exact step execution, required verification, the isolation prerequisite, and the earlier stop when a
blocker makes further mutation unsafe. Its mandatory transition into `finishing-a-development-branch`
is **rejected, not internalized**; that tail is assigned to Ship, whose contract does not yet exist.
Retirement therefore requires a written and tested `astra-ship` owner for the finish, merge, push,
and cleanup decision, or explicit user approval to drop the behavior. Provenance is complete at
plugin `6.2.0`.

**`superpowers:subagent-driven-development`:** preserve the fresh implementer per task, serial
dispatch with no concurrent implementers, per-task commits, the recorded task base and complete
`BASE..HEAD` review ranges including multi-commit tasks, the read-only reviewer that receives file
artifacts rather than controller history, five-round bounded repair, the four task states, and the
plan-scoped recovery ledger. **Rejected slices:** the finish/cleanup tail and the scratch-workspace
deletion. Its three helper scripts are a delivery shape — preserve them as scripts or prove an
equivalent internal seam. The observed `0644` mode defect must be reproduced or explicitly rejected
with evidence, never silently normalized. Retirement additionally requires the Ship owner named
above.

**`implement`:** preserve the thin spec/ticket intake, TDD at pre-agreed seams, regular focused
checks, and the final suite. **Rejected slices:** the unconditional current-branch commit, and the
direct invocation of code review, which this design splits into an internal task reviewer and public
Critique. Retirement requires either a tested Ship-owned commit path or explicit user approval to
delete the unconditional-commit behavior. No version declaration was inspected, so provenance is
incomplete on its own terms.

**`code-simplifier`:** preserve behavior-preserving clarity and consistency refinement and the
separate-agent delivery shape. **Rejected slice:** its proactive default scope over all recently
modified code. Retirement requires the section 9.5 cleanup-advantage gate to pass, evidence that
bounded dispatch loses no source-unique refinement quality, and preservation of the declared
`model: opus` or an approved substitute. Provenance is complete at plugin `1.0.0`.

**`feature-dev:feature-dev`:** outside Implement's retirement scope. Only phase 5 is Implement
behavior; phases 1–4 and 6 belong to Spec, Understand Code, Plan, and Critique. It cannot count
toward any peer's internalization gate until that cross-peer allocation is agreed, and its manifest
carries no version and an `unknown` cache path, so it fails provenance independently of any
behavioral finding.

**`health`:** outside Implement's retirement scope; proposed as an independent reference. Any later
design must preserve sequential tool detection and execution, the dashboard and trend history, the
hard never-fix gate, gstack history writes, and Health Stack configuration updates, and must resolve
the observed missing-`pipefail` example before its recorded exit statuses can be trusted as evidence.

**`simplify`:** cannot be gated at all. Bytes, manifest, path, declaration, and host-version pin are
unavailable, so it fails the retirement gate by definition. It stays excluded from candidate behavior
and from source-oracle comparison until it is inspectable.

**`codebase-design`:** outside Implement's retirement scope. It is a retained independent reference
consumed upstream, and this design proposes no change to its disposition.

**`planb` — peer-owned, recorded for completeness:** `astra-plan` owns this retirement gate. Section
5.9 records which execution and tracking behaviors Implement claims, refuses, and leaves unowned.
Because the refused behaviors still have no owner anywhere in the roster, nothing in this design
advances `planb` toward retirement, and this design proposes no ledger change on that row.

---

## 10. Provenance and open questions

### 10.1 Provenance summary

| Source family | Provenance state |
|---|---|
| Superpowers execution/review/worktree/finish | **O:** versioned plugin cache `6.2.0`; primary and directly referenced bodies inspected |
| Standalone `implement` | **O:** live body and invocation policy inspected; version unavailable |
| Feature Dev | **O:** command, agents, manifest, and README inspected; manifest version absent and cache directory `unknown` |
| Code Simplifier | **O:** versioned plugin cache `1.0.0`; agent and manifest inspected |
| Health | **O:** authored template, generated skill, generator registration/resolvers, clean commit, and gstack version inspected |
| `simplify` built-in | **U:** no body, manifest, path, or stable host-version pin available |
| `codebase-design` reference | **O:** live skill and both directly referenced method files inspected |

**Immutable source-artifact index.** This index covers inspected source bodies and declaration or
generation artifacts. Governing Astra documents are current working authority, not merger sources.

- Superpowers package manifest:
  `b271065c5e906e73757b7f9c26f7c57bb662ee47a31ed479dc32fb253729a25c`.
  `executing-plans`: skill
  `c4c3d8b628c51114cd165fb8246fe02744cd8be180032328391252e653028d9b`, metadata
  `c9884a11c9c4721b838ad0b526590efdf677065fb20af0ac3b2bd2ea55cf8786`.
- SDD: skill `349a08ad8b59b19b86c13a7d2f34a1a38719bf88257004a863eefefa8d9f9e40`;
  implementer prompt `946601616a6f76ab3f165ef98377390968f1ec124ecef87422bc3553404e0332`;
  task-reviewer prompt `e3b4a1bfe7cd55ed0459e5ca9cdddb6ff086c345b99e9097036db6a18545729e`;
  re-review prompt `e1d8e0e65e58ccde6dc920843da9148d23e65aeb0f8932bcc30be1341a703c4c`;
  `review-package` `fac3d4bd7f94369e8037b9ead2a8a502dca6ab333902b560b9455dbb3c450ebe`;
  `sdd-workspace` `95a09d9d3983ad1aafd093ca72b4587946dea885c6e302caa02a779a2f911c31`;
  `task-brief` `d6954ef7841c7da3d77373e6ff5118b3f2f2e998606fd95d33e6527851bce044`;
  metadata `58ef494a996998f2a486a0764b769bdf02e9c148b050b38603dbcdb364ae2771`.
- Supporting Superpowers boundaries: requesting-review skill
  `d71cc01ba56d2325cf8af5f7c11837819b63ecd57de0bfdb812f7f3ff7751df8`;
  reviewer prompt `b2f2ec7596925fe52dac158fdfbca19b3a7d779d619c481e6706a6c0001662d3`;
  worktree skill `8cfb86f121269e8f7f12361e6795c4f6738828340e28964c9229d365666c9edd`;
  finishing skill `d0ac8360ed9d59121776ef95c84bcb38e9747de0d7ae7e227dca81e437593b9b`.
- Thin Implement: skill
  `6d3fd9e83b8f36e5213854779db49b256a457a7ebb4a503e53fa7dcff696adc3`;
  metadata `8970a8596ade0c28ab427f41a4ea242d6bdf6186c59ebf55e1238dbecaab79dc`.
- Feature Dev: command
  `652e5d6264fd253fcb70c2f84de986a88d77109a02410aacd90230a6ab4bf557`;
  explorer `3b277703de7458988ec3b8021c716f79f642e174950ed332629310f68322029a`;
  architect `c50fb08d59a4bbd19660860626a049e44cf1a2b0c1cf782e6c7a99ba7e71b0c3`;
  reviewer `a7df173bf77a00da5584c6401a1061524fdbe477b6fef5dd496d4c7a9113c78c`;
  manifest `66e5b7724eae5bc5b24f18fafe4c425ba3763c543218ba1c68dcc22c589a99d9`;
  README `8dca1b27e026cab4b8bb8118709935b08fc27d2911efd9e1061b9836b534fbc1`.
- Code Simplifier: agent
  `2a51e8d210580d9f66ac2ed1226c41f9374565fc275da30d7bb95f65c2cc87bb`;
  manifest `f18fb26b2f03e95ad165a4333c73ecd292da18e74d2b89d89bd9848839f8d0e7`.
- Health at gstack commit `a3259400a366593e0c909dd9ac3e59752efd2488`: authored template
  `faf103f39b2a3e42192b476ec09778ab9300942ed12ae1f832a9018c4ec19b9d`;
  generated skill `505867059a06664334fb2ae1218b3deb814c8e7b42c837a626c3a062543611c8`;
  package declaration `9980b37cd19ba457ac713bdd96e67ea3242700c9c1f4e195832af34472736550`;
  version file `a05442e1220521c44bac111462a2a311da807c141cbefba49249f2e8599f44bb`;
  generator `cd62a5046ee68c5e65e55b3566615f7effbb2d845a946f2720eee7832fce38ef`;
  resolver registry `9e07dfe5a4ecc700fcb074f4ebf93493e369412e1f07831889d97ff284565e8d`;
  preamble resolver `d6e6e2f5cd68d2b414b667d09ecdc1c48770e1be3371859f6739edad971b3ea1`;
  utility resolver `9f71ca8edea748dae8fd0568202f5a661c4ed89e68f93aa7aa04219b012e8fe1`.
- Codebase Design reference: skill
  `a8d50abac5a4018f60e1d911d4b6f4e36454ca14d6c390c0695a578c7de65dad`;
  `DEEPENING.md` `125e6b77413ad2bc7cf7a772bc74336d580a50f9e797db2178ed133d62333d06`;
  `DESIGN-IT-TWICE.md` `21c3264953bd30ee87b181a3ccaf0e70649f461e5ffd7dc654acee4ba1788b31`;
  metadata `edebc9e4fcfe102114012575eaa9600b9b5fd08c311664f389c36e7bc717740f`.

### 10.2 Evidence gaps

- The built-in `simplify` behavior and host-version provenance are unavailable.
- No self-contained Astra runtime candidate, manifest, permission declaration, or installed path
  exists; phase 0 intentionally defers them.
- The Feature Dev manifest does not corroborate the README's version string.
- Five sibling contracts now exist — Spec, Plan, Test, Understand Code, and Critique — and sections
  2.3, 3.4, 5.5, 5.9, 7.2, and 7.4 are reconciled against them. `astra-debug` and `astra-ship` are
  still unwritten, so those two relation rows remain provisional from this side only. Ship's absence
  is load-bearing: three retirement gates in section 9.6 depend on a Ship owner that does not yet
  exist.
- `planb` was inspected by `astra-plan`, not here. Section 5.9 is a jurisdiction decision over the
  behavior class, not a preservation claim over inspected bytes, and `astra-plan` records that the
  source's `examples.md` ends in a truncation marker.
- The current SDD helper-file mode and Health pipeline behavior have been inspected statically but not
  mutated or executed during this documentation-only pass.

### 10.3 Provisional decisions

- The public intake requires an approved plan; Feature Dev's pre-approval phases do not move the
  boundary.
- Task dispatch is bounded implementation machinery, not the deferred general Delegate skill.
- Checkpoint commits belong only to task-dispatch mode in a user-approved isolated branch/worktree.
- Ship owns final commit shape and every publication/integration/cleanup effect.
- Internal task review does not absorb public Critique.
- Health remains independent and `simplify` remains deferred unless later evidence changes their
  dispositions.
- Originals remain installed. No preservation or retirement claim is made for unavailable behavior.
- `astra.plan.executable/v0` is accepted as the intake schema, including the immutable-version rule;
  progress state is Implement's and is never written back into the Plan artifact (sections 2.3.1,
  2.3.2).
- The roadmap R/I/H/P vocabulary replaces this design's earlier private one, and `H` is reserved for
  Critique alone (section 7.2).
- Of `planb`'s nine execution and tracking behaviors, two are claimed, six are refused, and one —
  phase review — is claimed only in the narrow `phases[].exit_gate` sense (section 5.9).

### 10.4 Open questions

1. Should Feature Dev remain a retained lifecycle command, or can its phases be allocated across
   Spec, Understand Code, Plan, Implement, and Critique after all five peer contracts exist?
   **Consequence:** it stays deferred and cannot count toward any peer's internalization gate until
   that allocation is agreed.
2. Should Health be retained permanently as a standalone dashboard, or assigned primarily to a later
   QA/Test neighborhood while Implement remains only a consumer? **Consequence:** Implement treats
   Health as advisory external evidence and makes no retirement claim in either case.
3. What stable path and host-version evidence will make the `simplify` built-in inspectable?
   **Consequence:** its row remains deferred, excluded from candidate behavior and source-oracle
   comparisons.
4. Should a mixed plan permit checkpoint commits only for dispatch segments, producing a partially
   committed tree, or should any mixed plan run wholly sequential until Ship? The comparison corpus
   must measure handoff clarity before choosing. **Consequence:** the runtime candidate cannot enable
   mixed mode until the handoff and recovery invariant is selected.
5. Should the five-round repair limit remain fixed across task risk levels, or be plan-configurable
   without weakening the stop gate? **Consequence:** preserve the observed fixed limit in the
   reference convener and do not expose a tuning field until evidence supports it.
6. Who owns the `planb` execution behaviors that section 5.9 refuses — plan-file writes, host task
   creation, general subagent dispatch, advisor calls, and live adaptation? This is the
   Implement-side half of `astra-plan`'s open question 6, and neither design can close it alone.
   **Consequence:** those behaviors stay unowned, `planb` stays ineligible for retirement, and no
   design may quietly re-acquire them to make the row resolvable.
7. Is the correct review granularity per task, per phase, or both? SDD reviews per task; `planb`
   reviews per phase; Plan's schema carries a `phases[].exit_gate` that implies a phase-boundary
   check. **Consequence:** section 5.9 claims only the exit-gate evaluation, and the phase-review
   agent shape stays unclaimed until the `planb` body is compared against SDD's task reviewer.
8. Who owns gstack `spec`'s fresh-worktree agent spawn? `astra-spec` excludes it, and this design
   declines it. **Consequence:** it remains an unowned source effect recorded as **P** in section
   7.2, and neither design's retirement claim may count it as preserved.

### 10.5 Coordinator reconciliation still required

The phase-0 coordinator must reserve and reconcile the seven rows in section 3.3, decide the
cross-peer Feature Dev disposition, and add Health to the reference ledger if its independent status
is accepted. Five further items arise from the 2026-08-04 peer pass:

- record this design's acceptance of `astra.plan.executable/v0` and the progress-state split as the
  reconciled answer to `astra-plan` open question 2, which that design marks blocking before
  implementation;
- record the nine acceptances in section 3.4 against the peer-owned rows that assert them, so both
  sides of each secondary role are visible on one page;
- snapshot section 7.4's corrected `approved-code-remediation` profile as the canonical Implement
  destination contract, which `astra-critique` explicitly defers to this design;
- carry the section 7.2 vocabulary correction into any earlier notes that quoted the old letters; and
- log the unowned residue — `planb`'s five refused behaviors, the gstack agent spawn, and the Ship
  tail that three section 9.6 gates depend on — as roster-level gaps rather than per-design ones.

This design deliberately leaves `docs/design-roadmap.md` and `docs/phase-0-ledgers.md` untouched. No
claim here becomes global allocation authority until those coordinator edits occur.

---

## 11. Six-skill reconciliation amendment

This section absorbs repository delivery planning while preserving Spec's change authority,
Critique's finding and causal authority, Test's independent evidence authority, and Ship's
publication authority. It replaces the active Plan intake, optional-checkpoint, uncommitted-
sequential-mode, and Ship-final-shaping rules in sections 1–10. Those sections remain source and
validation evidence rather than a second runtime contract.

### 11.1 One invocation, two consecutive stages

Implement owns:

1. produce and obtain approval for an immutable repository Delivery Roadmap; and
2. execute exactly that approved Roadmap while recording a separate Execution Ledger.

Before Roadmap approval, Implement may inspect the live repository and run authorized read-only
discovery commands. It may not mutate the target, create an implementation commit, or treat a
draft Roadmap as authority. The user approves the exact Roadmap version and hash, mutation scope,
execution mode, worktree use, commit authority, and PR partition before execution begins.

The Approved Delivery Roadmap must contain:

- pinned Approved Change Specification revision/hash and every applicable Finding ID;
- live repository baseline, branch/worktree state, dirty state, and protected pre-existing
  changes;
- exact files, symbols, interfaces, generated contracts, tasks, and typed dependency ordering;
- repository phases implementing Spec's required semantic order;
- conditional diagnostic branches authorized by the Specification;
- exact verification commands, working directories, prerequisites, expected evidence, and
  evidence owners;
- allowed effects, forbidden effects, stop conditions, recovery procedures, and rollback limits;
- execution mode and bounded agent assignments;
- one logically indivisible intent and focused validation gate for every atomic commit;
- one-functionality PR scope, authored-line estimate, language partition, and any explicit stack
  dependency; and
- required Critique, Spec, and conditional Understand consultant checkpoints.

The Roadmap never selects a different solution, changes a requirement, weakens a criterion,
invents a semantic branch, or resolves a user-owned tradeoff. A repository fact that makes the
approved solution impossible is an `authority_gap`, not permission to reinterpret the
Specification.

### 11.2 Consultant gates and forward-only branches

One persistent Critique consultant and one persistent Spec consultant participate whenever their
authority is present. An Understand Code consultant also participates when the Roadmap directly
relies on an Understanding Report. They receive immutable artifact references rather than reading
sideways into peer files.

Before Roadmap approval:

- Critique checks Finding-ID coverage, causal proof obligations, instrumentation needs, and
  diagnostic branch completeness;
- Spec checks requirements, acceptance criteria, constraints, semantic ordering,
  implementation freedoms, and branch authorization; and
- Understand Code, when applicable, checks that repository claims have not drifted beyond its
  report.

During execution, the Critique consultant evaluates diagnostic evidence and causal claims. The
Spec consultant confirms which already approved branch that evidence permits. Evidence inside the
decision envelope proceeds without an upstream restart or renewed approval. Evidence outside it,
an invalidated finding, stale artifact identity, or a new user-owned decision returns
`authority_gap` and stops mutation.

At final implementation verification, the same consultants check the delivered revision and
Execution Ledger against their preserved authority. `drift` may be repaired only when the repair
is already a named Roadmap task or approved branch. Consultants never mutate, approve, or widen
the Roadmap.

Implement exposes its own narrow read-only `consult` mode to Test and Ship. It validates delivered
scope, task and commit coverage, language partitioning, and Execution Ledger accuracy and returns
`pass`, `drift`, or `authority_gap`. It cannot declare Test evidence sufficient or authorize
publication.

### 11.3 Execution Ledger and deviation rules

The Approved Delivery Roadmap is immutable. The Execution Ledger separately records:

- Roadmap identity/version/hash and the observed baseline;
- task state, dependency releases, mode and assigned executor;
- exact pre- and post-task revisions and dirty-state deltas;
- diagnostic evidence, consultant determinations, and selected approved branch;
- commands, working directories, outputs, failures, and focused verification results;
- changed files, generated-output accounting, authored-line counts, and protected user changes;
- atomic commit IDs and their requirement, criterion, task, and evidence references;
- deviations, whether they remain inside approved implementation freedom, and user decisions;
- unselected branches, parked work, residual instrumentation, risks, and resume cursor; and
- final revision identity and Test handoff.

A represented condition selects a branch; it does not rewrite the Roadmap. A mechanical execution
detail may vary only inside an explicit Specification freedom and Roadmap effect boundary and is
recorded as a deviation. Any new task, file class, functionality, language partition, semantic
outcome, required effect, or commit purpose outside the Roadmap stops for a new approved Roadmap or
an upstream authority cycle as appropriate.

Focused implementation checks prove only that an atomic task is ready to commit. They do not
replace Test's independent verification against the pinned delivered revision.

### 11.4 Atomic commit policy

Every implementation commit must be:

- one logically indivisible change;
- complete with the tests and durable documentation necessary for that change;
- free of unrelated cleanup, metadata, or user-owned work;
- verified by its named focused checks before creation;
- independently understandable and safely revertible; and
- created immediately after that atomic change is verified.

This policy applies in sequential, task-dispatch, and mixed execution. Roadmap approval is the
bounded commit authority; a separate ad hoc approval is not required for each commit already named
there. Agent dispatch and worktree creation still require their exact approved effects. Implement
records and protects pre-existing staged, unstaged, and untracked changes and never folds them into
an atomic commit merely because they share the checkout.

The historical rule that sequential mode normally leaves work uncommitted is superseded. The
historical distinction between a checkpoint and a final-quality implementation commit is also
superseded: every Implement commit must meet the atomic contract when created. Implement never
pushes, opens a PR, merges, releases, deploys, or rewrites atomic history for cosmetic shaping.

### 11.5 Narrow PR roadmap policy

Each planned PR must serve exactly one functionality, feature, or bug fix. Implement targets no
more than 400–500 authored changed lines. If the realized work would grow beyond that target, it
stops and repartitions before adding more scope. Exceeding 500 authored lines requires explicit
justification and user approval.

Changes in different implementation languages go into separate PRs even when they support the
same larger feature. The Roadmap names their dependency order or stacking relationship. Tests and
durable documentation may accompany only the functionality they directly support. Generated
output is counted and reported separately and cannot conceal the authored line total.

Critique and Spec consultants check that this partition retains complete Finding and requirement
coverage. Ship later verifies realized scope, language separation, authored-line count, base,
ancestry, conflicts, and fresh evidence before publication.

### 11.6 Deferred source absorption

The superseded Plan design's inspected sources now require source-by-source allocation between
Spec, Implement, retained references, adapters, and exclusions. This amendment does not claim that
allocation, change a ledger row, or resolve the Implement design's existing source gaps. In
particular, task publication, tuning, general delegation, live adaptation, Health, unavailable
`simplify`, and source-native Ship tails remain open source-specific decisions.

No runtime skill, consultant process, harness, schema, corpus, reference convener,
self-contained candidate, push, PR, or source retirement is created here. Implement is
policy-grounded but deliberately not yet fully fleshed out from every relevant source.
