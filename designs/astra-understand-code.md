# Astra Understand Code — phase-0 design

**Date:** 2026-08-03 · **Public tranche position:** 2 of 8 · **Status:** `proposed`

> **Authority.** `docs/design-requirements.md` is the sole per-skill contract;
> `docs/phase-0.md` owns phase scope and global accounting; the current user instruction fixes the
> public drafting tranche. This design changes no ledger, installs or removes nothing, and grants
> no source-retirement authority.
>
> **Certainty.** **O** = observed in an inspected artifact; **I** = inferred and still requiring
> confirmation; **U** = unavailable. Proposed Astra behavior is explicitly described as a proposal
> or hypothesis rather than as observed runtime behavior.
>
> **Conformance.** Sections 1–10 map one-to-one and in order to
> `docs/design-requirements.md` sections 7.1–7.10. Phase 0 is prose only. Every original remains
> installed.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-understand-code` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhoods | Codebase comprehension; one retained-agent seam from Plan & spec |
| User job | **When I want to understand how a codebase behavior works well enough to make a technical decision without changing the project.** |
| Accepts Critique handoff | **yes**, for the bounded problem class in section 7.3 |

This is one outcome: an evidence-backed working model of existing code. Locating a symbol, tracing a
flow, explaining a subsystem, and exposing the technical-design consequences of that model are
different depths of the same inquiry. Optional improvement advice is a read-only interpretation of
the established model; it is not a second mutation or planning job.

**Personal value — explicit.** The user selected `astra-understand-code` as the second peer in an
exact eight-peer public drafting tranche. That makes the design itself a `now` priority. The stated
scope also protects a recurring project-development need: learn unfamiliar code before Spec, Plan,
Implement, Test, or Debug acts on it. Usage supports but does not decide priority: `code-tracing`
recorded 11 July invocations, all agent-fired (**O**, README “Actual working set”).

The authoritative public tranche, and no substitute roster, is `astra-critique`,
`astra-understand-code`, `astra-spec`, `astra-plan`, `astra-implement`, `astra-test`,
`astra-debug`, and `astra-ship`. They are flat peers. Context, Guard, Delegate, Automate, Incident,
and Deploy are deferred general-purpose peers and appear here only as honest manual or external
bridges.

---

## 2. Interface and scope

### 2.1 Small public interface

Conceptually, the future module accepts three caller-visible facts:

1. a bounded codebase question;
2. the repository, revision, or supplied artifact context in which the question should be
   answered; and
3. an optional explicit mode when the caller needs `locate`, `trace`, `explain`, or
   `technical-design` behavior rather than safe automatic selection.

Its result is one **understanding report** whose detail varies by mode but whose claims remain tied
to paths, symbols, revisions, and stated uncertainty. The invocation and these behavioral promises
are the module's external interface. Search strategy, agent fan-out, reconciliation, diagrams, and
technical-design vocabulary stay in the implementation behind that seam.

`technical-design` is never selected implicitly. The source contributing that mode disables model
invocation in both its Claude declaration and OpenAI metadata (**O**); a future candidate must
preserve the explicit-user gate even if explanation remains model-invocable.

### 2.2 Requests that should trigger it

- “Where is this method declared or called?”
- “Trace this request from the entry point to persistence.”
- “How does authentication, billing, rendering, or another subsystem work?”
- “Map the modules, interfaces, seams, adapters, data flow, invariants, and surprising behavior in
  this area.”
- “Given how this subsystem works, where are the evidence-backed deepening opportunities?” when the
  user explicitly requests read-only technical-design advice.
- “Prepare the code evidence an architect, spec author, planner, implementer, tester, debugger, or
  critic would need,” without starting that other workflow.

### 2.3 Nearby requests that should not trigger it

| Request | Owner or bridge | Reason |
|---|---|---|
| “Attack this architecture or diff and tell me what is wrong” | `astra-critique` | Adversarial judgment and independent code/architecture lenses are Critique's job |
| “Decide what product behavior should exist” | `astra-spec` | Intent and acceptance behavior are not facts about existing code |
| “Turn this decision into executable tasks” | `astra-plan` | Task decomposition and approval state are downstream |
| “Make or refactor the change” | `astra-implement` | Project mutation is forbidden here |
| “Design or execute the test strategy” | `astra-test` | This peer may explain existing tests but does not own testing methodology |
| “Why is this failing?” where cause is unknown | `astra-debug` | Causal diagnosis uses a failure-first loop; Understand supplies a map at most |
| “Commit, push, open a PR, merge, or publish” | `astra-ship` | VCS finalization and publication are effects outside this interface |
| “Choose one complete feature architecture and implementation blueprint for me” | retained `feature-dev:code-architect` agent | Decisive blueprint authority and separate agent delivery remain independent |
| “Deploy this” or “stabilize an outage” | external/manual Deploy or Incident bridge | Those deferred peers are neither implemented nor absorbed here |

### 2.4 Accepted input and user-visible result

Accepted context may be a repository or bounded path set; a revision, diff, symbol, feature, event,
or runtime flow; the user's question and known constraints; and optional existing evidence such as
logs, tests, a specification, an ADR, or `CONTEXT.md`. The skill may inspect the project read-only.
It does not require every optional artifact to exist.

The report contains only the sections useful for the selected depth:

- a hit list for `locate`;
- a call/data/state trace for `trace`;
- overview, key concepts, flow, file map, gotchas, and open questions for `explain`; or
- the explanation plus current-architecture friction, dependency categories, candidate deepening
  opportunities, trade-offs, and a recommendation for `technical-design`.

Every factual conclusion distinguishes observed evidence from inference. An absent or ambiguous
edge remains a named gap. A design recommendation distinguishes the current fact, the pressure it
responds to, and the proposed choice.

### 2.5 Non-goals and forbidden effects

- Editing project source, configuration, `CONTEXT.md`, ADRs, tests, plans, or documentation.
- Creating commits, branches, worktrees, tickets, schedules, deployments, or persistent state.
- Treating a search hit as proof of behavior, or turning a locate request into an unsolicited
  whole-subsystem analysis.
- Running an internal critic panel, adjudicating a Critique report, or silently invoking any peer.
- Absorbing `codebase-design` or the retained `feature-dev:code-architect` agent.
- Presenting technical-design advice as an approved plan or implementation blueprint.
- Hiding a missing model, agent, search tool, repository history, domain glossary, ADR, browser,
  network asset, or destination peer.

An explicitly requested visual technical-design report may write one disposable file to the OS
temporary directory and open it. That is a report-delivery effect, not project mutation; it must be
separately visible and must never fall back to writing inside the repository.

### 2.6 Decisions that remain with the user

The user owns scope when several interpretations would materially change the answer; whether to
continue from locating into tracing or explanation; whether to request technical-design advice;
which deepening candidate or interface direction to pursue; whether to ask Critique to review the
result; whether to dispatch the retained Architect; and whether any downstream peer starts.
Automatic mode selection may reduce ceremony, but it may not silently cross the explicit
`technical-design` gate or the project-read-only invariant.

---

## 3. Source evidence and proposed ledger changes

All assigned bodies and their directly relevant registrations and bundles were inspected in full
on 2026-08-03. Hashes are of the inspected bytes. Line anchors, if later added, are valid only while
those hashes match.

### 3.1 Occurrence inspection record

| Occurrence / identifier | Component and live location | Invocation and availability | Complete declaration or registration | Immutable provenance |
|---|---|---|---|---|
| `cm-codebase-comprehension-01` / `how` | skill; `~/.claude/skills/how` symlink → `/mnt/c/Users/kurop/Desktop/University/Intern/monster-prompt/claude/skills/how/` | skill name `/how`; live (**O**) | `name: how`; description: explain codebase architecture and optionally critique; no authority fields (**O**) | clean `monster-prompt` revision `6abccfa5f83a82f2bff309228b956323a11e4d2a`; `SKILL.md` `b6097e3854c746d5db4cdd3efcd145669897d44c2fbf4f679590b9231c5eac50` |
| `cm-codebase-comprehension-02` / `code-tracing` | skill; `~/.claude/skills/code-tracing` symlink → `/mnt/c/Users/kurop/Desktop/University/Intern/monster-prompt/claude/skills/code-tracing/` | skill name `/code-tracing`; live (**O**) | `name: code-tracing`; `effort: low`; multiline locate-only description; no invocation restriction (**O**) | same clean revision; `SKILL.md` `9810975a10c402bf2a53928186f5925c8b69d42e26b5a279969f58843a593314` |
| `cm-codebase-comprehension-03` / `codebase-design` | skill and independent reference; `~/.claude/skills/codebase-design` symlink → `~/.agents/skills/codebase-design/` | `/codebase-design`; live (**O**) | `name`, description only; OpenAI metadata `display_name: Codebase Design`, `short_description: Vocabulary for deep-module design` (**O**) | `SKILL.md` `a8d50abac5a4018f60e1d911d4b6f4e36454ca14d6c390c0695a578c7de65dad`; metadata `edebc9e4fcfe102114012575eaa9600b9b5fd08c311664f389c36e7bc717740f` |
| `cm-codebase-comprehension-04` / `improve-codebase-architecture` | skill; `~/.claude/skills/improve-codebase-architecture` symlink → `~/.agents/skills/improve-codebase-architecture/` | `/improve-codebase-architecture`; live; user-only (**O**) | `name`; description; `disable-model-invocation: true`; OpenAI metadata display/description and `policy.allow_implicit_invocation: false` (**O**) | `SKILL.md` `4b4cb798c3863d5b6f5c0b4604af1ecb5beb6df82553c972898a91ba38bcf289`; metadata `c8cb20f68ebf0edb4e497bc11ae5fcaa196004e661cd189015b04f4109ced7f1` |
| `cm-codebase-comprehension-05` / `feature-dev:code-explorer` | agent in enabled `feature-dev@claude-plugins-official`; `~/.claude/plugins/cache/claude-plugins-official/feature-dev/unknown/agents/code-explorer.md` | agent type `feature-dev:code-explorer`; live; README also documents manual natural-language launch (**O**) | `name`, full description, tools `Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch, KillShell, BashOutput`, `model: sonnet`, `color: yellow` (**O**) | agent `3b277703de7458988ec3b8021c716f79f642e174950ed332629310f68322029a` |
| `cm-plan-and-spec-14` / `feature-dev:code-architect` | retained agent in the same enabled plugin; `~/.claude/plugins/cache/claude-plugins-official/feature-dev/unknown/agents/code-architect.md` | agent type `feature-dev:code-architect`; live; manual natural-language launch documented (**O**) | same tool list, `model: sonnet`, `color: green`, plus its exact name/description (**O**) | agent `c50fb08d59a4bbd19660860626a049e44cf1a2b0c1cf782e6c7a99ba7e71b0c3` |

**Complete declaration values.** The compact table above records every field; the exact
descriptions are transcribed here so declaration evidence is not reduced to a label:

| Identifier | Exact declared description and additional interface metadata |
|---|---|
| `how` | `Explain how something works in this codebase by exploring code and producing a clear architectural explanation. Optionally critique the architecture for issues.` |
| `code-tracing` | `Fast code tracing: grep once to locate, disambiguate from the grep output by eye, and stop — the hit list is the deliverable. Read (always with offset/limit) only when you actually need a method body. Locating is a separate phase from understanding; don't blur them.` |
| `codebase-design` | `Shared vocabulary for designing deep modules. Use when the user wants to design or improve a module's interface, find deepening opportunities, decide where a seam goes, make code more testable or AI-navigable, or when another skill needs the deep-module vocabulary.` OpenAI metadata is exactly `Codebase Design` / `Vocabulary for deep-module design`. |
| `improve-codebase-architecture` | `Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.` OpenAI metadata is exactly `Improve Codebase Architecture` / `Find and grill architecture improvements`; implicit invocation is false in both host declarations. |
| `feature-dev:code-explorer` | `Deeply analyzes existing codebase features by tracing execution paths, mapping architecture layers, understanding patterns and abstractions, and documenting dependencies to inform new development` |
| `feature-dev:code-architect` | `Designs feature architectures by analyzing existing codebase patterns and conventions, then providing comprehensive implementation blueprints with specific files to create/modify, component designs, data flows, and build sequences` |

The plugin manifest declaration is exactly name `feature-dev`, description `Comprehensive feature
development workflow with specialized agents for codebase exploration, architecture design, and
quality review`, and author `{name: Anthropic, email: support@anthropic.com}`; it has no version
field (**O**).

The directly relevant plugin bundle census is one `/feature-dev` command and three agents; no hook,
MCP server, tool server, or LSP declaration is present (**O**). The command frontmatter is exactly
description `Guided feature development with codebase understanding and architecture focus` and
`argument-hint: Optional feature description`. The census-only `code-reviewer` agent declares its
exact name and high-confidence code-review description, the same full tool list as Explorer and
Architect, `model: sonnet`, and `color: red`. Its behavior and primary home are outside this
assignment; reading it establishes bundle shape, not a disposition claim.

The Feature Dev registration is **O**: `settings.json` enables
`feature-dev@claude-plugins-official`; `installed_plugins.json` records a user-scoped install at
the inspected cache path with `version: unknown`, installed 2026-03-31 and updated 2026-08-03.
The plugin manifest names `feature-dev`, Anthropic as author, and the exploration / architecture /
review workflow, but declares no version. Its README says `1.0.0`. The mismatch is a **P**
provenance obligation rather than permission to choose either value. Relevant registration hashes
are manifest `66e5b7724eae5bc5b24f18fafe4c425ba3763c543218ba1c68dcc22c589a99d9`,
installed registry `d6963627a077c6b61aee8b277e99b63f4f52e075b6275ce2beb2e4890eaa7095`,
and settings `0e553d6e5eb95b9fc5b63b5f65e15d22bbfef538558e3bb66eea6c6ce27eed1a`.
The cache's assigned agent and manifest bytes match the marketplace copies (**O**), but the
marketplace directory has no inspected Git revision (**U**).

### 3.2 Full body and bundle evidence

| Source | Bodies inspected in full | Observed behavior, authority, dependencies, and failure shape |
|---|---|---|
| `how` | 139-line skill plus `explorer-prompt.md` (52), `explainer-prompt.md` (55), `critic-prompt.md` (59), and `critique-rubric.md` (58) | **O:** simple questions dispatch one read-only general-purpose “latest Sonnet” explainer; complex questions dispatch 2–4 parallel explorers then a synthesizer. It states an interpretation instead of asking when scope is ambiguous. Explanations cite files/functions, reconcile contradictions, and expose gaps. Critique mode explains first, then dispatches three independent critics and performs lead judgment. Agent/model availability and the host's `readonly` enforcement are prerequisites; no explicit fallback is declared. |
| `code-tracing` | 98-line skill and complete four-case `evals/evals.json` bundle | **O:** body defines locating as a separate phase: one grep, disambiguate from hits, stop; read only a bounded body; use `sg` only for a declaration shape grep cannot express. A literal `sg` pattern can silently return exit 0 with no matches when decoration nodes differ, so the playbook uses `kind` plus a name regex and `--debug-query`; arrow-function declarations are a named TS/JS exception. **O conflict:** the eval bundle expects structured caller maps, snippets, and an end-to-end call chain. That bundle drift must be characterized before implementation or retirement; this design does not guess which behavior has runtime authority. |
| `codebase-design` | 114-line skill, 37-line `DEEPENING.md`, 44-line `DESIGN-IT-TWICE.md`, and OpenAI metadata | **O:** defines **module**, **interface**, **implementation**, **depth**, **seam**, **adapter**, **leverage**, and **locality**; the interface is the test surface; one adapter is a hypothetical seam, two a real one. Dependency categories are in-process, local-substitutable, remote-but-owned, and true external. Design-it-twice dispatches 3+ separate agents and asks the user to choose. It references project `CONTEXT.md`, which is not bundled and may be absent. It is explicitly shared vocabulary for other skills. |
| `improve-codebase-architecture` | 71-line skill, complete 123-line `HTML-REPORT.md`, and OpenAI metadata | **O:** scope-first scan prefers Git hot spots, reads `CONTEXT.md` and relevant ADRs, dispatches an Explore agent, applies the deletion test, writes a fresh temp HTML report using Tailwind and Mermaid CDNs, opens it, and asks the user to select a candidate. It forbids interface proposals before selection. Its terminal loop invokes `/grilling`; it may invoke `/domain-modeling` to edit or create `CONTEXT.md` and may offer an ADR. Those mutations conflict with this peer's read-only promise and are not silently inherited. Missing Git history, glossary, ADRs, temp write, GUI, CDN/network, Agent, Grilling, or Domain Modeling capability are **I** distinct degradations; the source specifies only the temp-dir fallback. |
| `feature-dev:code-explorer` | complete 51-line agent, plugin manifest, 412-line README, 125-line command, and all three 34/46/51-line agent bodies as a bounded bundle census | **O:** separate Sonnet context traces entry points, call/data flow, architecture layers, dependencies, side effects, errors, performance, technical debt, and essential files. The command invokes 2–3 explorers, then the controller rereads their key files. Its declared tools omit `Write`, `Edit`, and `Bash` but do not declare a `readonly` field; this is evidence of limited tools, not proof of an enforced read-only sandbox. The agent names no dispatch/tool failure protocol; honest gaps are part of its requested output. |
| `feature-dev:code-architect` | complete 34-line agent and the same registration/bundle | **O:** separate Sonnet context finds patterns, chooses one approach decisively, and returns a file-by-file implementation blueprint and build sequence. The enclosing command instead dispatches 2–3 differently biased Architect agents, compares approaches, and returns the final choice to the user. The single agent's “pick one and commit” policy therefore must remain distinguishable from the command's user-choice protocol. Neither body declares an agent-unavailability fallback. |

Additional inspected bundle hashes are: How critic prompt
`384dbe2e16b558f7139b22d6b6acdf07f0a36aa4e000d6402e9b00388b52a422`, rubric
`8ac5786e430f5043e6eae1ed81e9b8cef5fb5825bf1043428dd5fcfe57f4ed2a`, explainer
`5a5223f5fe1c22447638fa285cc74f1be98ea53c4941aaa4231260ee84a384e0`, explorer
`0cf798751cf535d35697b7902d19d257da0a1e046337d18a40759fd5ec109f76`; tracing evals
`1c30901a8123b7bda100df652d83d9ed2f27250a6f178711c13811f9cd5f9221`; Deepening
`125e6b77413ad2bc7cf7a772bc74336d580a50f9e797db2178ed133d62333d06`, Design It Twice
`21c3264953bd30ee87b181a3ccaf0e70649f461e5ffd7dc654acee4ba1788b31`; HTML report
`0b0936104158abeef7246ff6cbabefa4dc055f17589f2833f2d93001421910a1`; Feature Dev README
`8dca1b27e026cab4b8bb8118709935b08fc27d2911efd9e1061b9836b534fbc1`, command
`652e5d6264fd253fcb70c2f84de986a88d77109a02410aacd90230a6ab4bf557`, and reviewer
`a7df173bf77a00da5584c6401a1061524fdbe477b6fef5dd496d4c7a9113c78c`.

### 3.3 Disposition and contribution

| Occurrence | Proposed primary disposition and home | Contribution | Explicit secondary or independent role |
|---|---|---|---|
| `how` | proposed Astra design → `astra-understand-code` | **Machinery, Protocol, Playbook, Jurisdiction**: complexity-sensitive exploration, synthesis, architecture explanation, evidence-linked result | `astra-critique` owns the source's independent critic lenses and adversarial judgment; Understand retains explain-first evidence only |
| `code-tracing` | proposed Astra design → `astra-understand-code` | **Playbook, Protocol, Jurisdiction**: fast locate-only stop rule, bounded reads, AST fallback | Eval/body conflict remains a **P** characterization obligation, not a second home |
| `codebase-design` | independent reference → retained independent | **Reference**: exact deep-module vocabulary, dependency categories, seam discipline, design comparison | Consumed by `astra-understand-code` and `astra-implement`; not absorbed or made retirement-eligible |
| `improve-codebase-architecture` | proposed Astra design → `astra-understand-code` | **Playbook, Protocol, Jurisdiction, Prerequisite**: scope-first deepening scan, glossary/ADR context, visual candidates, user selection | Critique owns adversarial evaluation. Its Grilling/Domain Modeling mutation tail remains a current external/manual bridge until reassigned or explicitly retired by the user |
| `feature-dev:code-explorer` | proposed Astra design → `astra-understand-code` | **Playbook, Prerequisite**: separate-context comprehensive exploration and evidence packet | Later self-containment must preserve the agent delivery shape where used; it may not flatten the separate context into one prose paragraph |
| `feature-dev:code-architect` | retained agent, coordinated → `astra-understand-code` | **Separate, Prerequisite**: decisive implementation blueprint after pattern analysis | Remains independently invocable with its agent delivery shape; Understand may emit or, after explicit approval, pass an evidence brief. It never absorbs the agent's decision policy |

No source is declared absorbed or preserved merely because its proposed primary home is this design.
Those are later behavioral claims gated by section 9.

### 3.4 Exact proposed collision-ledger changes

Only the phase-0 coordinator may apply these rows. The current rows are already `claimed`; this
design proposes the evidence and refined secondary-role text, not a direct edit.

| Occurrence ID | Primary disposition | Primary home | Secondary roles | Claim state after coordinator application | Evidence |
|---|---|---|---|---|---|
| `cm-codebase-comprehension-01` | proposed Astra design | `astra-understand-code` | `astra-critique`: independent code/architecture critic lenses; no nested critique mode in Understand | `claimed` | this design §§3.1–3.3 and full How bundle hashes; roster reconciliation pending |
| `cm-codebase-comprehension-02` | proposed Astra design | `astra-understand-code` | — | `claimed` | this design §§3.1–3.3 and both tracing hashes; body/eval authority resolution pending |
| `cm-codebase-comprehension-03` | independent reference | retained independent | `astra-understand-code`, `astra-implement` | `claimed` | this design §§3.1–3.3 and full reference-bundle hashes; user reference disposition pending |
| `cm-codebase-comprehension-04` | proposed Astra design | `astra-understand-code` | `astra-critique`: adversarial architecture review and inbound `H` route back to Understand; current `/grilling` remains external | `claimed` | this design §§3.1–3.3 and full skill/report/metadata hashes; peer-profile reconciliation pending |
| `cm-codebase-comprehension-05` | proposed Astra design | `astra-understand-code` | preserve separate agent execution context | `claimed` | this design §§3.1–3.3 and Feature Dev registration/bundle hashes; roster reconciliation pending |
| `cm-plan-and-spec-14` | retained agent, coordinated | `astra-understand-code` | `astra-plan` may consume a user-approved blueprint; it does not own or invoke the agent | `claimed` | this design §§3.1–3.3 and Feature Dev registration/bundle hashes; Plan reconciliation pending |

**Reference/cleanup ledger proposal.** The existing `codebase-design` row already names
`astra-understand-code` and `astra-implement` as `consuming_designs`. Preserve that exact consumer
set. Preserve `disposition: unassigned` and the pending user `keep` / `defer` / `exclude` decision;
this design does not infer `keep`. No additional reference row is proposed.

---

## 4. Collision analysis

### 4.1 Why the entries looked duplicative

All six occurrences read code and discuss architecture. `how` and Code Explorer both trace flows;
`code-tracing` and both explorers search for symbols; `how` Critique and Improve Architecture both
surface architectural issues; Codebase Design and Architect both discuss interfaces; Improve
Architecture and Architect both produce technical direction. Their labels therefore collide even
though their stopping points, authority, and delivery shapes do not.

### 4.2 What is genuinely shared

The shared kernel is evidence acquisition followed by a bounded model of existing behavior. The
question determines how deep the evidence chain must go:

```text
symbol hits → connected flow → coherent system model → read-only technical consequence
```

Every later stage depends on the earlier facts, but a request may stop at any stage. That graduated
depth is shared protocol and playbook, not proof that every source is interchangeable.

### 4.3 Aliases and shallow delegation

None is a safe alias.

- `code-tracing` is deliberately narrower than `how`; its hit list is the result.
- Code Explorer is a separate agent context with a comprehensive evidence contract, not a renamed
  search command.
- `improve-codebase-architecture` orchestrates Codebase Design, Explore, HTML delivery, Grilling,
  and Domain Modeling. Its 71-line body is coordination behavior, not an architecture perspective.
- Codebase Design is independently useful vocabulary with live sibling consumers.
- Architect is a retained agent with incompatible decision authority, not an internal mode that can
  be paraphrased away.

### 4.4 Apparent duplicates that are different jobs

| Apparent overlap | Actual distinction |
|---|---|
| `how` explanation vs `how` Critique | Existing-system understanding belongs here; independent adversarial judgment belongs to Critique |
| Locate vs trace | Locate reports symbol sites and stops; trace establishes connected execution/data/state flow |
| Trace vs explain | A trace is ordered evidence; an explanation organizes the evidence into a working mental model |
| Technical-design advice vs Architect | Understand exposes alternatives and trade-offs without project mutation; Architect makes one decisive blueprint in a retained context |
| Technical-design advice vs Plan | Advice identifies a possible module/interface/seam choice; Plan creates approved executable work |
| Architecture concern vs code defect | Module/interface/seam placement belongs here as read-only decision support; bounded code remediation belongs to Implement |
| Existing test explanation vs test design | Understand may map current tests; Test owns strategy, fixtures, execution, and adequacy judgment |

### 4.5 Instruction conflicts that must remain visible

1. **Tracing body versus eval bundle.** The body says locate and stop; three evals demand caller
   bodies or end-to-end traces. This is an unresolved source-authority conflict (**O**), so the
   candidate preserves separate locate and trace modes and retirement waits for characterization.
2. **Embedded critics versus flat Critique.** `how` dispatches three architecture critics and a
   lead judge; the roster gives public adversarial judgment to `astra-critique`. The explanation
   phase remains here; the critic lenses become a Critique secondary role, not a hidden panel.
3. **Read-only job versus Improve mutations.** Improve may edit `CONTEXT.md` through Domain Modeling
   and offer an ADR after Grilling. Current user authority makes this peer project-read-only. The
   behavior is recorded as an external/manual tail and blocks source retirement until reassigned,
   explicitly waived, or preserved elsewhere with user approval.
4. **User choice versus decisive Architect.** Design It Twice and the Feature Dev command compare
   alternatives and return the choice to the user; the standalone Architect commits to one
   approach. The agent stays retained and its output remains attributable.
5. **Best-guess scope versus material ambiguity.** `how` says to state a best guess and explore
   without asking. The proposed interface preserves that for cheap, reversible exploration but
   asks when different interpretations would materially change cost, repository scope, or the
   technical decision (**I**, later characterization required).

### 4.6 Why one coherent deep module is plausible

The deletion test supports one module: delete the proposed graduated-depth coordinator and callers
must again decide among one-pass grep, bounded reads, multi-hop tracing, parallel exploration,
synthesis, glossary/ADR review, deepening analysis, and delivery format. That complexity reappears
at every caller. Behind one small interface it creates leverage for Spec, Plan, Implement, Test,
Debug, Critique, and the user, while evidence and correction concentrate for locality.

The module remains deep only if callers do not need to learn every source's dispatch strategy,
prompt format, model selection, HTML scaffold, or dependency behavior. Locate, trace, explain, and
technical-design are modes, not separate public peers, because they answer one bounded question at
increasing evidence depth and preserve explicit stop points.

### 4.7 Declared positive advantage

**Advantage class: cross-depth codebase questions.** On questions that begin with an uncertain
symbol or entry point and end in a subsystem or technical-design decision, the reference convener
and self-contained candidate should produce a more complete, evidence-traceable mental model than
the strongest single source, while doing less irrelevant exploration than always running the
deepest source. A positive win requires at least one supported critical flow, invariant, seam, or
dependency consequence that the preselected source oracle misses, without losing the oracle's
home-jurisdiction facts.

Routing convenience and one invocation are secondary advantages. They do not satisfy the quality
gate by themselves. The candidate must also show zero project mutations and no hidden Critique or
Architect invocation.

---

## 5. Preserved distinctions

### 5.1 Locate is a complete result

Preserve `code-tracing`'s low-effort discipline: one appropriately scoped search, disambiguation
from the hit lines, and an immediate file:line result. Read a bounded body only when requested or
needed to distinguish a declaration shape. Use AST-aware search only when text search cannot
express the shape. A locate request must not pay for synthesis merely because deeper modes exist.

Concrete matter: finding every invocation of one overload amid logs, strings, comments, and another
overload. Expanding into architectural explanation raises latency and can introduce unsupported
claims without helping the decision.

### 5.2 Trace is not explanation

Trace preserves ordered entry points, callers/callees, data transformations, side effects,
dependencies, integration edges, errors, and file:line anchors. It may include bounded snippets and
explicitly unresolved hops. It does not add architectural praise, criticism, or redesign advice.

Concrete matter: a REST request that acquires a lock, writes a database record, calls an external
system, and has a rollback divergence. The ordered edges matter even when the reader does not need
an onboarding narrative.

### 5.3 Explanation preserves complexity-sensitive delivery

For a simple question, preserve one read-only explorer/explainer context. For a complex subsystem,
preserve 2–4 non-duplicative exploration angles followed by one synthesizer that rereads evidence
when findings conflict. Preserve overview, key concepts, flow, relevant file map, gotchas, and open
questions, adapting rather than emitting empty headings.

Concrete matter: a one-function utility should not launch four explorers; a rendering pipeline
spanning state, measurement, and DOM behavior should not be guessed from one file.

### 5.4 Critique and technical-design ownership

The source's coupling/seam, failure-mode, and evolution/maintainability critic lenses remain useful,
but they belong to public Critique. Understand may supply the explanation and evidence anchors that
those lenses inspect. It may later accept the user's selected `H` capsule for an architecture or
technical-design problem and explore read-only alternatives. It never convenes the critics, ranks
their findings, or invokes Critique.

Critique's evidence-gated production-code lens from `/diss` and its structure-first, recall-first
lens from `review` also remain there. Understand constructs the factual code map those policies may
judge; it does not choose a filing threshold or turn missing test evidence into a verdict. Code
Explorer's observed contract may mention strengths, issues, or opportunities, but the proposed
Explain mode labels those as candidate observations. They become design advice only after explicit
technical-design intent, or critique findings only inside Critique.

Concrete matter: “how does this seam work?” triggers Understand; “is this seam misplaced?”
triggers Critique; “given the accepted finding, what module/interface/seam alternatives fit the
evidence?” may return to Understand through the user.

### 5.5 Read-only technical-design advice

Preserve Improve Architecture's hot-spot scoping, relevant glossary and ADR reading, organic
exploration, deletion test, recommendation strengths, dependency classification, before/after
visual explanation, top recommendation, and user selection. Preserve its rule not to propose
interfaces before a candidate is selected. If the user continues, use Codebase Design's comparison
method and return the final choice to the user.

Do not preserve project mutation inside this interface. Updating `CONTEXT.md`, writing an ADR,
editing code, or turning advice into tasks requires a separately authorized external workflow. The
report may write only to an explicit OS-temp delivery path. This is a deliberate authority split,
not a claim that the source never mutated.

### 5.6 Exact independent vocabulary

Use **module**, **interface**, **implementation**, **depth**, **seam**, **adapter**, **leverage**, and
**locality** exactly when those concepts apply. An interface includes invariants, ordering, error
modes, required configuration, and performance characteristics. A seam is the location of that
interface. An adapter satisfies it. Do not substitute “component,” “service,” “API,” or “boundary”
when those words would erase the intended concept.

Preserve the four dependency categories and their consequences: in-process, local-substitutable,
remote-but-owned with a port and at least production/test adapters, and true external with an
injected port and mock adapter. Do not introduce a seam for hypothetical reuse. The external
`codebase-design` reference remains addressable to other consumers.

### 5.7 Separate agent delivery shapes

Code Explorer's comprehensive pass remains a separate context when selected. Its evidence packet
must include entry points, flow, architecture, dependencies, side effects, essential files, and
gaps. A later self-contained candidate may internalize the prompt behavior, but not collapse the
separate context into the controller's unlabelled opinion.

Architect remains the installed `feature-dev:code-architect` agent. Its decisive blueprint,
file-level change map, and build sequence are attributable to that agent. Understand may prepare a
brief and may coordinate an explicit user-approved dispatch; it does not internalize the role,
present the result as its own, or make Architect a child Astra skill.

### 5.8 Authority, prerequisites, delivery, and failure behavior

| Distinction to preserve | Evidence and consequence |
|---|---|
| `effort: low` for locate | Tracing frontmatter (**O**); later runtime must characterize an equivalent low-cost mode rather than running the deepest path |
| Technical-design explicit invocation | `disable-model-invocation: true` and `allow_implicit_invocation: false` (**O**); no auto-router may cross it |
| Read-only exploration | How requests `readonly: true`; agent tool lists omit mutation tools (**O**) but host enforcement is not proven. The candidate needs a real forbidden-effect gate, not prose confidence |
| Model/context variation | How requests latest Sonnet general-purpose contexts; Feature agents pin `model: sonnet` (**O**). Missing dispatch/model capacity must be reported; reduced direct exploration may be offered but cannot be called equivalent before validation |
| Markdown, structured trace, and visual HTML | Three observed result shapes. Output normalization must not discard source-unique evidence or silently write to the repo |
| Missing glossary or ADR | Treat as absent context, not failure and not permission to invent domain language or re-litigate a decision |
| Missing Git history | Accept a user-bounded scan; report that hot-spot weighting was unavailable |
| Missing GUI/CDN/network | Return the absolute temp report path and a legible static fallback; do not report the visual delivery as fully preserved unless later tested |
| Search ambiguity or broken flow | Return candidate hits or an unresolved edge with the searches/files checked; never bridge it by guess |

These distinctions are documentary obligations, not proof that later behavior already passes.

---

## 6. Proposed skill design

### 6.1 Architecture hypothesis and depth

The proposed module has one external seam and one conceptual operation:

```text
understand(question, code_context, optional_mode) → understanding report
```

This is an interface sketch, not a schema or implementation. The interface includes the mode
authority rules, project-read-only invariant, evidence expectations, uncertainty behavior, and
cost characteristic as well as the three conceptual inputs. Exact frontmatter, field names, tool
declarations, and packaging remain deferred.

The implementation is deep because the caller does not select grep syntax, AST node kinds,
exploration angles, agent counts, synthesis prompts, glossary/ADR order, dependency category,
diagram renderer, or fallback behavior. Those choices sit behind the interface. Depth is leverage
at that interface, not a line-count ratio.

The architecture is a hypothesis. A simpler explicit set of specialist modes replaces the
coordinator if section 9 finds that automatic depth selection adds noise, cost, or unsupported
claims without a positive cross-depth win.

### 6.2 Internal modules

| Internal module | Responsibility | Why it remains internal |
|---|---|---|
| **Question framer** | Resolve repository/revision, scope, desired decision, and safe mode; state a cheap interpretation or ask only when ambiguity changes authority or cost | Callers should express the question, not learn routing rules |
| **Evidence acquirer** | Search, bounded read, AST-aware declaration search, revision/hot-spot lookup, and optional separate explorer dispatch | Search mechanics vary while the evidence contract remains stable |
| **Flow modeler** | Construct callers/callees, transformations, state changes, side effects, dependencies, error paths, and unresolved edges | The same evidence supports trace, explanation, and technical-design modes |
| **System explainer** | Turn the flow model into a senior-engineer mental model; reconcile duplicate or contradictory findings against code | Narrative structure should not leak into evidence acquisition |
| **Technical-design advisor** | Explicit-only: apply the independent vocabulary, deletion test, dependency categories, glossary/ADRs, candidate comparison, and recommendation without project mutation | The user should not need the deepening playbook for ordinary explanation |
| **Evidence renderer** | Emit hit list, structured trace, explanatory Markdown, or optional temp HTML while retaining anchors and uncertainty | The source set demonstrates multiple real delivery adapters |
| **Handoff framer** | Render peer-consumable evidence or an Architect brief; name a peer without invoking it unless the user separately authorizes the retained non-peer agent | Handoff mechanics must not acquire solution authority |

These are proposed internal modules, not public skills or a universal Astra runtime. No shared Astra
module is proposed: this design alone does not meet the two-design threshold for extraction.

### 6.3 Modes and stopping rules

| Mode | Entry rule | Work hidden behind the interface | Required stop |
|---|---|---|---|
| `locate` | User asks where a symbol, declaration, or call site is | One scoped text search; hit-line disambiguation; bounded body/AST search only when necessary | File:line hit list and ambiguity notes; no explanation |
| `trace` | User asks what calls what or how data/state moves | Locate entry point; follow each relevant hop; record transformations, effects, errors, and gaps | Ordered evidence map; no architecture verdict |
| `explain` | User asks for a working mental model | Simple direct explorer/explainer or complex parallel exploration and synthesis | Standalone explanation with anchors and open questions |
| `technical-design` | User explicitly asks for read-only improvement or a selected Critique architecture problem | Explain first; scope hot spots; read available glossary/ADRs; apply deletion test and dependency categories; compare selected interface options only after user choice | Evidence-backed advice and user-owned next decision; no project edit, plan, or implementation |

`auto` may select among the first three modes and may escalate one step when the requested result
cannot be supported at the current depth. It must disclose the escalation. It never enters
`technical-design` without explicit user intent.

### 6.4 Information flow

1. Frame the question, code context, revision, and desired decision. Record unavailable context.
2. Select the least-deep mode capable of answering the question.
3. Acquire evidence. For a simple question use direct search and one context; for a complex
   question split 2–4 genuinely different exploration angles. Preserve every explorer's file list
   and open gaps.
4. Build one flow model. Contradictory agent findings remain unresolved until checked against code;
   the synthesizer does not vote.
5. Render the requested result at the selected depth with source anchors and certainty.
6. In explicit technical-design mode only, classify current dependencies, identify real pressure,
   apply the deletion test, and present ranked candidates. If the user selects a candidate and asks
   for interface alternatives, compare them by depth, locality, and seam placement and return the
   choice to the user.
7. Offer, but never start, the appropriate peer or retained-agent bridge. Stop.

The design does not use an internal critic panel. A Critique report may be an input artifact, but
its findings remain attributable and its user-selected problem class bounds the work.

### 6.5 Internal seams and adapters

Two observed variations justify an internal seam inside Evidence Acquirer:

- a direct adapter uses search and bounded reads for narrow questions; and
- a separate-context explorer adapter gathers a comprehensive evidence packet for complex ones.

Two observed variations also justify a renderer seam: Markdown/structured text and visual temp
HTML. These seams stay private. Tests in a later phase should exercise observable results through
the external interface rather than reaching past it.

No `ArchitectPort` is proposed. Only one retained Architect adapter exists, so a new port would be a
hypothetical seam. Coordination is a user-mediated call to that existing agent with a documented
brief. Likewise, `codebase-design` is read as an independent reference; wrapping it in a one-adapter
module would add indirection without depth.

### 6.6 Technical-design authority

The advisor may describe current shallowness, leakage across a seam, dependency category, likely
deepening, alternative interfaces, leverage, locality, test surface, and trade-offs. It may
recommend one option. It may not:

- edit the project, glossary, or ADR;
- mark a recommendation approved;
- convert it into tasks or a build sequence;
- ask Architect to commit to it without a separate user decision;
- ask Critique to endorse it; or
- imply that an untested redesign is better because it sounds cleaner.

If an ADR contradicts a candidate, report both and why reopening might be justified. The user
decides whether to revisit it. If a domain term is missing, propose the term in the report; an
external documentation workflow owns any write.

### 6.7 Uncertainty, failure, and degradation

| Condition | Proposed behavior |
|---|---|
| Repository or revision unavailable | Answer from supplied artifacts only, label the evidence limit, and do not claim current-code coverage |
| Symbol has multiple plausible matches | Return candidates and discriminators; ask only if choosing would materially change the trace |
| Flow edge cannot be established | Name the missing hop, searches and files checked, and the downstream claim it prevents |
| Separate agents or requested model unavailable | Offer a reduced direct pass with `degraded: no-isolated-explorers`; do not claim equivalent independence or coverage |
| Explorer findings conflict | Re-read the relevant code; if still unresolved, retain both claims and the missing evidence |
| Git history unavailable | Skip hot-spot weighting; use explicit user scope or a bounded static scan and say so |
| `CONTEXT.md` or ADRs absent | Continue with code vocabulary and label domain/decision context absent; do not create files |
| Codebase Design reference unavailable | Explanation can continue; technical-design mode reports that its exact vocabulary and comparison playbook are unavailable and does not pretend fidelity |
| Temp directory unwritable | Return Markdown in the conversation; never write inside the project as a fallback |
| Browser or CDN unavailable | Return the absolute HTML path when created plus a text-equivalent report; mark diagrams/styling degraded |
| Critique profile missing or inconsistent | Keep the problem and evidence visible; emit no guessed handoff capsule |
| Retained Architect unavailable | Return the complete Architect brief for manual use; the understanding report remains valid |

### 6.8 Decisions still hypothetical

- Whether `auto` should select locate versus trace or whether those must remain explicit for latency
  predictability.
- Whether separate explorer contexts add enough supported recall over direct exploration to justify
  their cost on medium questions.
- Whether the visual HTML adapter adds decision value beyond Markdown.
- Whether technical-design comparison belongs in the same invocation after candidate selection or
  should require a second explicit invocation.
- Whether a read-only recommendation can preserve enough of Improve Architecture to justify later
  retirement when its current mutation tail is intentionally outside this interface.

Section 9 turns each into a measurable obligation; none is represented as validated.

---

## 7. Dependencies and delivery shape

### 7.1 Separate dependencies

| Dependency | Delivery shape and relation | Behavior when absent |
|---|---|---|
| Project repository and read/search tools | External artifact plus host tools; **reads** only | Degrade to supplied files and record coverage limit |
| Git history | Optional local runtime used for revision anchors and hot-spot scoping | Use explicit scope or bounded static scan |
| Separate explorer contexts | Agent delivery; future candidate **invokes** only as internal implementation machinery for complex questions | Direct degraded pass, explicitly losing isolation/parallel coverage |
| `codebase-design` | Retained independent reference; technical-design mode **reads/consumes** it; never replaces it | Disable vocabulary-fidelity claim and deepening comparison, not explanation |
| `feature-dev:code-architect` | Retained external agent; user-approved coordination only; never absorbed | Emit a manual brief and stop |
| `CONTEXT.md` and ADRs | Optional project references; **read**, never written | Name the missing context; do not invent it |
| Temp filesystem, browser opener, Tailwind/Mermaid CDNs | Optional visual-report delivery prerequisites | Conversation Markdown or static report; no repository fallback |
| Original source files | Reference convener only; unchanged originals are **invoked/read** during later comparison | Missing source invalidates that source's convener run; a final candidate depending on it is not self-contained |

The proposed self-contained candidate may continue to depend on general host facilities such as
filesystem reads, search, agent dispatch, and optional browser delivery. Self-containment forbids a
runtime dependency on original source files proposed for replacement; it does not mean vendoring a
Git implementation, browser, model, or OS temp directory.

### 7.2 Precise flat-peer relations

Codes retain the roadmap meanings: **R** is roster reconciliation, **I** is later consumption of a
peer output or capability, **H** is Critique's user-mediated problem handoff, and **P** is unresolved
provenance or external behavior. None means invocation. Every peer workflow starts only when the
user requests it.

| Peer | Code, direction, and exact information class | Minimum payload | User decision and unavailable behavior |
|---|---|---|---|
| `astra-critique` | **R:** split `how`'s explanation from its critic lenses. **H inbound:** Critique → user → Understand for section 7.3's problem. Optional **I:** a user may supply an Understanding report as Critique evidence; neither peer invokes the other | For optional evidence: artifact/revision, question, paths/symbols, observed flow/invariants, gaps. For `H`, section 7.3 | User chooses zero or one Critique route or separately starts Critique. Missing profile preserves the report and marks a reconciliation gap |
| `astra-spec` | **R:** existing-code facts must not become product intent. **I:** Understand → Spec, which may consume constraints and existing behavior; no invocation | Question answered, relevant modules/flows, observed behavior, invariants, integration constraints, evidence anchors, gaps | User starts Spec. If unavailable, the understanding report remains usable; Understand does not author requirements |
| `astra-plan` | **R:** technical advice is not an executable plan. **I:** Understand → Plan with a user-accepted technical decision; no invocation | Repository/revision, relevant paths/symbols, accepted module/interface/seam choice, invariants, constraints, alternatives rejected by the user, evidence gaps | User decides whether the advice is accepted and starts Plan. Without Plan, no tasks are manufactured |
| `astra-implement` | **R:** project-read-only versus mutation authority. **I:** Understand → Implement directly only when an approved plan already owns the change; otherwise via Plan; no invocation | Code map, observed invariants, affected interfaces/seams, evidence anchors, accepted constraints, unresolved risks | User supplies the approved plan and starts Implement. If unavailable, no mutation occurs |
| `astra-test` | **R:** explaining current tests is not test design. **I:** Understand → Test, which may consume existing seams, flows, failure paths, and current coverage facts; no invocation | Repository/revision snapshot, behavior flow, current test locations, observable interfaces and invariants, dependencies/adapters, accepted architecture constraints, known edge cases and gaps | User starts Test. If unavailable, Understand reports existing evidence only and makes no adequacy claim |
| `astra-debug` | **R:** code comprehension is not failure-first causal diagnosis. **I:** Understand → Debug as a code map or trace; no invocation | Reproduction context if supplied, entry point, ordered trace, state/effect edges, suspected-but-unproven gaps, revision | User decides whether diagnosis starts. If unavailable, the report labels the anomaly unexplained rather than treating it as cause |
| `astra-ship` | **R:** preserve Understand's read-only evidence role and Ship's finalization/publication authority. **I user-mediated:** Understand → user → Ship; never `H`, never invocation | Understanding-report reference, repository/revision, affected paths or symbols, observed invariants and dependency/compatibility notes, evidence anchors, and unresolved gaps | User alone decides whether to attach the report and start Ship. If Ship is unavailable or not selected, retain the report and attempt no VCS effect; Ship independently owns commit shaping, changelog/version work, publication, integration, and cleanup |

There is no implicit peer invocation, no peer nesting, and no peer fallback substitution. A named
peer may be unavailable without invalidating the understanding report.

### 7.3 Critique handoff acceptance

**Accepts Critique handoff: yes.** The owned post-critique problem class is
`architecture-or-technical-design`: a supported finding that the current module/interface/seam/
adapter placement, dependency structure, or system flow needs further read-only explanation and
option analysis before the user can choose a direction.

Critique's common problem envelope already carries destination, artifact, problem, finding IDs,
evidence, impact, scope, constraints, open decisions, prerequisites, and context gaps. The compact
destination-only payload adds only Understand-specific routing information:

| Field | Required content |
|---|---|
| `problem_class` | exact value `architecture-or-technical-design` |
| `requested_mode` | one of `locate`, `trace`, `explain`, explicit-only `technical-design`, or `unknown`; this selects the required analysis depth without expanding scope. **`unknown` is required** whenever Critique cannot classify the depth without prescribing Understand's method — the same escape `astra-test` gives `required_test_mode`, and for the same reason: forcing a choice would make Critique decide a destination workflow depth it has no basis to decide. Understand then selects the mode at intake |
| `analysis_question` | the envelope `finding_ids` whose resolution requires analysis, plus **only** the framing the envelope does not already supply: what must be decided, phrased without a remedy. It **references** `problem_statement` rather than restating it — the convention `astra-test`'s `proof_obligation` sets. A restatement can diverge from the envelope's text, leaving Understand owning a second, unreconciled problem statement |
| `technical_decision_kind` | `system-flow`, `module-depth`, `interface-shape`, `seam-placement`, or `adapter-or-dependency-placement` |

All artifact and revision anchors, paths and symbols, observed facts, finding evidence, impact,
affected scope, constraints, open decisions, prerequisites, ADR/domain context, and context gaps
arrive through Critique's common envelope. The destination payload neither repeats nor overrides
them.

The profile rejects a specific code defect with an approved remedy (`astra-implement`), an execution
plan defect (`astra-plan`), a test gap (`astra-test`), or an unknown runtime cause (`astra-debug`).
If Critique reviewers nominate incompatible owners for the same problem, the user resolves that
classification before any capsule exists. Critique retains every independent route in its report,
emits zero or one immediate user-selected capsule, and never invokes or reads Understand's full
workflow. Understand owns solution exploration after acceptance and may still conclude that more
evidence is required.

The roadmap previously described Improve Architecture's `/grilling` step as an `H` edge. Under the
current authoritative relation definition, `H` originates only at Critique after its report. This
design therefore does **not** label Understand → Critique as `H`: a user may start Critique as a
separate review invocation, while the only `H` edge here is Critique → user → Understand. The
coordinator must reconcile that terminology with the ledger's secondary-role text.

### 7.4 Retained-agent coordination

Code Explorer and Architect have different dispositions:

- The Explorer occurrence belongs to the candidate behavior, but its separate agent context is a
  delivery invariant. The reference convener invokes the unchanged installed agent. A later
  self-contained candidate must reproduce the role in a separate context without reading the
  original agent file before that source can retire.
- Architect remains retained and independently invocable. Understand emits an **Architect brief**:
  bounded decision, repository/revision, existing patterns, essential files, flow model, module /
  interface / seam facts, user constraints, selected direction if any, alternatives considered,
  and evidence gaps. The user then either invokes the agent manually or explicitly authorizes
  coordination. The agent's decisive recommendation and file/build map remain attributable to it.

Architect coordination is not an `I` or `H` peer edge because Architect is an external retained
agent, not an Astra peer. Its absence never causes Understand to imitate it.

### 7.5 Deferred general-purpose peers as manual bridges only

| Deferred peer | Honest bridge; no implemented capability claimed |
|---|---|
| Context | Manually supply repository/revision, question, scope, prior trace, user decisions, and gaps on every new or resumed invocation |
| Guard | State read-only project scope, allowed temp-report effect, forbidden paths/effects, and host safety rules explicitly |
| Delegate | How/Explorer's bounded source-specific contexts are not general delegation; every unrelated dispatch returns to the user |
| Automate | No scheduled, repeated, hook-driven, or background understanding run; re-invoke manually |
| Incident | An outage may supply logs or code context, but stabilization and incident command remain external |
| Deploy | Understand may explain deployment code; live rollout, rollback, credentials, and environment mutation remain external |

### 7.6 Provenance dependencies

The following **P** relations block absorption or retirement claims but do not block this prose
design: tracing body/eval authority; Feature Dev's `unknown` installed version versus README
`1.0.0`; actual host enforcement of `readonly`; equivalence between latest-Sonnet and pinned-Sonnet
agent behavior; Critique's unreconciled code/architecture source expansion and destination profile;
and the user's pending disposition for the independent Codebase Design reference.

---

## 8. Manual bridge

No Astra runtime exists. The following current invocations approximate the proposed modes while all
originals remain installed.

### 8.1 Locate

```text
/code-tracing Find every real call to <symbol or overload>; return file:line hits only.
```

Use this when the hit list is the deliverable. If a body is required, ask for the bounded body
explicitly. Do not ask it for an explanation and then treat extra tracing as a source failure.

### 8.2 Trace and explain

```text
/how Explain how <bounded behavior> works in <repository/path/revision>. Use Explain mode only.
```

For a comprehensive feature trace in the installed Feature Dev delivery shape, use the README's
documented manual pattern:

```text
Launch code-explorer to trace how <feature> works. Return entry points, each flow hop, data/state
transformations, dependencies, side effects, essential files, and unresolved edges with file:line
evidence. Do not modify the project.
```

The exact registered agent is `feature-dev:code-explorer`. The natural-language form is safest for
the current host because the plugin README documents it; a future Astra implementation must not
assume that this manual phrase is a stable programmatic interface.

### 8.3 Read-only technical-design scan

```text
/improve-codebase-architecture <bounded module, subsystem, or pain point>
```

Add this explicit authority instruction to the current source:

```text
Read-only project analysis. You may write the requested report only to the OS temp directory.
Stop after presenting candidates and asking which one I want to explore. If I answer, restate my
selection and stop before Grilling. Do not edit or create CONTEXT.md, an ADR, source, tests, or
docs; do not invoke domain-modeling; do not start implementation.
```

The current skill may still open a browser and load Tailwind/Mermaid from CDNs. If that is
unavailable, request the same findings in Markdown. Invoke `/codebase-design` separately when the
exact glossary or Design It Twice method is needed; it remains an independent reference.

### 8.4 Current critique seam

If the user wants an adversarial architecture review today, the installed source oracle is:

```text
/how Explain <bounded subsystem>, then run its Critique mode. Keep the result report-only.
```

This approximates the current source, not the future ownership split: its embedded critics are the
behavior to reconcile into public Critique later. After any current critique, manually preserve all
route candidates. If the user selects `architecture-or-technical-design`, copy the common envelope
plus section 7.3's four compact fields into a new `/how` or read-only
`/improve-codebase-architecture` invocation. Start no other route automatically.

### 8.5 Optional retained Architect

Only after the user explicitly requests a decisive blueprint:

```text
Launch code-architect to design <selected technical direction>. Use this evidence brief:
<question, revision, patterns, essential files, flow, constraints, decision, and gaps>.
```

The exact registered agent is `feature-dev:code-architect`. Its output is an external retained-agent
result, not `astra-understand-code` output and not an approved plan. The user may next take it to
Plan. If the agent is unavailable, keep the brief and stop.

### 8.6 What the bridge cannot approximate

No current invocation provides the graduated locate → trace → explain → explicit technical-design
interface, enforces the read-only split across every source, preserves the future Critique handoff,
and coordinates Architect without either absorbing or implicitly invoking it. Manual instructions
cannot prove host-enforced authority. That gap is why section 9 compares actual later systems.

---

## 9. Deferred implementation and validation

Nothing in this section was run during phase 0. It records skill-specific later obligations only;
`docs/phase-0.md` section 8 owns the phase-wide deferred-work list.

### 9.1 Declared advantage and three comparison systems

**Declared advantage class:** cross-depth questions whose evidence path spans locating, connected
flow, explanation, and a bounded technical-design consequence. A positive win is a supported
critical flow, invariant, seam, or dependency consequence that the strongest preselected original
misses, combined with no loss of the original's home-jurisdiction facts and no project mutation.

Later evaluation compares identical public tasks through:

| System | Role in this design |
|---|---|
| **Source oracle** | Strongest applicable original selected before outputs are seen: tracing body for locate, How for explanation, Code Explorer for comprehensive feature analysis, Improve Architecture for deepening scan; Codebase Design and Architect remain independent references/dependencies rather than merger oracles |
| **Reference convener** | Temporary adapter that selects and coordinates the unchanged originals, retains separate agent contexts, and normalizes only input/output shape |
| **Self-contained candidate** | Proposed final adapter that reproduces retained `how`, tracing, Improve, and Explorer behavior internally without reading those original files; it still reads the independent Codebase Design reference and may coordinate the retained Architect only after explicit approval |

The neutral comparison wrapper may provide the same repository, revision, question, and output
headings. It may not add search hints, expected symbols, perspective text, a preferred design, or
the identity of the expected winner.

### 9.2 Fixed corpus

The versioned corpus is selected before outputs and contains:

**Home-jurisdiction cases**

- exact symbol and overload locating amid comments, strings, logs, generated files, and similarly
  named methods;
- one declaration shape requiring AST-aware search and one ordinary shape where AST search would
  be waste;
- a small utility explanation that should use one context;
- a multi-file, multi-layer subsystem requiring parallel exploration and synthesis;
- a feature analysis requiring entry points, data/state transformations, integrations, side
  effects, errors, performance constraints, and essential files;
- a scoped deepening scan with Git hot spots, a domain glossary, and applicable ADRs;
- the same scan with no Git history, no `CONTEXT.md`, and no ADRs; and
- an optional visual-report case whose graph materially clarifies dependencies.

**Claimed-advantage cases**

- a question whose entry point is initially unknown, whose flow crosses several modules, and whose
  likely seam cannot be evaluated correctly until the trace is complete;
- a subsystem with a shallow cluster whose apparent fix is invalidated by an ADR or domain
  invariant discovered during explanation;
- a question where one early search hit is a misleading adapter while a separate-context explorer
  finds the actual implementation; and
- a mixed request whose correct result stops at locate, proving the coordinator can avoid needless
  depth rather than always doing more.

**Expected-divergence and convergence controls**

- tracing's locate-only body versus the end-to-end expectations in its eval bundle;
- How's explanation output versus its embedded critic output on the same subsystem;
- Improve's user-returning candidate selection versus Architect's decisive one-blueprint output;
- Improve's current `CONTEXT.md`/ADR mutation tail versus the candidate's project-read-only result;
- direct one-context and parallel-explorer results on a genuinely simple question, where they
  should converge on facts and parallelism should add no invented complexity; and
- How and Code Explorer on the same feature, where shared flow facts should converge even if
  presentation depth differs.

**Peer-routing and authority cases**

- one Critique finding accepted as `architecture-or-technical-design`;
- a specific code defect, plan defect, test gap, and unknown runtime cause that must route to
  Implement, Plan, Test, and Debug rather than this peer;
- two independent Critique routes, of which the user selects one while both remain in the report;
- an Architect brief that is emitted but not dispatched, and a second case with explicit dispatch;
- attempts to trigger technical-design implicitly; and
- canary files in source, `CONTEXT.md`, ADRs, tests, and docs plus Git state, proving zero project
  mutations across every mode and failure path.

**Prerequisite-failure cases**

- missing search tool or AST tool; missing separate agent/model; partial explorer failure; ambiguous
  symbol; unresolved call edge; unavailable repository revision; missing Codebase Design reference;
  unwritable temp directory; unavailable GUI or CDN/network; unavailable Architect; and missing or
  inconsistent Critique profile.

### 9.3 Method and measures

Run the three systems on identical repository snapshots and questions. Repeat each stochastic run
at least three times. When explanation or design quality requires judgment, de-identify and
randomize output order for evaluators who have the task rubric and repository evidence but not the
system label. Record every mode selection and degradation state.

Measures are:

- critical edge, invariant, dependency, and technical-decision recall;
- supported-claim precision and unsupported-claim rate;
- source-unique supported findings retained;
- path/symbol/line-anchor accuracy and stale-anchor rate;
- trace completeness and false-edge rate;
- mental-model usefulness to a blinded engineer answering fixed comprehension questions;
- actionable technical-design consequences and explicit trade-off quality;
- duplicate/noise load and irrelevant files read;
- mode-routing accuracy, unnecessary-depth rate, and technical-design implicit-entry count;
- Critique destination accuracy, capsule traceability, and wrong-owner rate;
- project mutation count, hidden peer invocation count, and unauthorized Architect dispatch count;
- correct degradation disclosure and unresolved-gap retention;
- input/output tokens, tool calls, wall-clock time, and peak parallel contexts; and
- visual-report decision value, temp-path correctness, and offline legibility when that adapter is
  exercised.

Project mutations, hidden peer invocations, implicit technical-design entry, and unauthorized
Architect dispatch must all remain zero. Lower cost alone is not a positive quality advantage.

### 9.4 Gates and failure consequences

1. **Source characterization.** Reproduce locate/trace, explanation/critique, user-choice/decisive,
   and read-only/mutation distinctions in at least two of three original-source trials. Resolve the
   tracing body/eval authority before making its mode contract normative. A failed distinction is
   reclassified; it is not preserved as folklore.
2. **Home-jurisdiction non-regression.** The convener and candidate retain every reproducible
   critical fact, source-unique playbook result, authority field, result shape, and degradation
   behavior of the source oracle, with no higher unsupported-claim rate. Failure narrows the
   candidate or keeps that original installed.
3. **Positive cross-depth advantage.** On at least one preregistered advantage class, both combined
   systems add a supported critical flow, invariant, seam, or dependency consequence missed by the
   source oracle in at least two of three runs, while satisfying home non-regression. Failure
   rejects the automatic combined architecture; retain explicit specialist modes or originals.
4. **Internalization fidelity.** The self-contained candidate matches the reference convener on
   characterized distinctions, source-unique supported findings, separate-context behavior,
   explicit gates, delivery adapters, uncertainty, and prerequisite degradation. A matching final
   recommendation does not excuse a lost trace, glossary/ADR constraint, or user choice. A convener
   win followed by candidate loss blocks internalization and retirement.
5. **Read-only and routing integrity.** All project canaries and Git state remain unchanged; temp
   output stays outside the repo; Critique and Architect are never invoked implicitly; every peer
   route has the correct owner and payload; unavailable dependencies produce named degradation.
   Any violation blocks the candidate regardless of answer quality.
6. **Retirement.** Each source passes its source-specific gate below and then requires explicit user
   approval. One source's pass cannot retire another. The independent reference and retained agent
   are not retirement candidates of this design.

### 9.5 Source-specific retirement gates

| Source | Later retirement gate | Failure consequence |
|---|---|---|
| `how` | Preserve simple/complex routing, read-only separate contexts, 2–4 differentiated explorers, evidence reconciliation, standalone explanation shape, diagrams only when useful, gotchas/gaps, and explicit degradation. Critic-lens behavior must be accepted by the reconciled Critique design rather than silently lost | Keep `how` installed or retire only the proven explanation slice after the user approves the cross-peer allocation |
| `code-tracing` | Resolve body/eval authority; preserve `effort: low`, one-search stopping, overload/noise disambiguation, bounded body reads, AST fallback only when justified, and any characterized structured trace obligations | Keep it installed; do not let a slower general explanation count as equivalent |
| `improve-codebase-architecture` | Preserve explicit-only invocation, hot-spot/glossary/ADR scoping, deletion test, dependency classification, visual candidate report, recommendation strength, user selection, and failure behavior. Separately account for Grilling, Domain Modeling edits, ADR offer, temp/GUI/CDN delivery, and exact vocabulary. Retirement requires either preservation in an authorized destination or explicit user approval to drop each mutation behavior | Keep it installed. A read-only report alone cannot retire a source whose useful mutation/delivery tail remains unowned |
| `feature-dev:code-explorer` | Preserve a separate Sonnet-equivalent context or demonstrate a non-regressing substitute; entry points, complete flow, architecture, dependencies, side effects, errors, performance, improvement observations, essential files, exact anchors, tool limits, and failure reporting must survive without reading the original agent file | Keep the agent installed or narrow the self-contained claim to modes that do not use it |
| `codebase-design` | Not owned for retirement. It remains independently addressable, its exact vocabulary and both method references remain available to all consumers, and the user decides the global reference disposition | No Astra Understand Code gate can retire it |
| `feature-dev:code-architect` | Not owned for retirement. Coordination must preserve separate context, full declaration/tool/model evidence, decisive blueprint authority, attribution, explicit user dispatch, and manual fallback | Retain the agent. A successful brief adapter proves coordination only, never absorption |

The Feature Dev plugin is a bundle. Even if Explorer someday passes its gate, the plugin command,
Architect, and Reviewer cannot be retired from this occurrence's evidence alone. Bundle-level
uninstallation needs every component's allocation, version/provenance resolution, dependency gate,
delivery-shape gate, and user approval.

---

## 10. Provenance and open questions

### 10.1 Inspection summary

**Observed.** All assigned source bodies, direct support files, agent declarations, plugin manifest,
plugin README and command, live symlink targets, relevant enabled/installed registration entries,
roadmap sections, ledger rows, Critique's code/architecture and handoff design, Implement's adjacent
seams, and the complete Codebase Design vocabulary/deepening references were inspected on
2026-08-03. The two monster-prompt skills were clean at Git revision
`6abccfa5f83a82f2bff309228b956323a11e4d2a`.

**Inferred.** A graduated-depth module can add supported cross-depth value without erasing the
locate stop rule; Code Explorer's limited tool declaration can support a future enforced
project-read-only adapter; and a read-only technical-design mode can retain enough of Improve
Architecture to be personally useful. These are section 9 hypotheses, not validated claims.

**Unavailable.** An immutable installed version or Git revision for the `feature-dev/unknown`
cache; evidence that the host enforces How's `readonly: true` or makes the Feature agents read-only;
runtime evidence from any Astra candidate; and reconciled final contracts for sibling Spec, Plan,
Test, Debug, Ship, and Critique's source expansion.

### 10.2 Immutable source-artifact index

```text
b6097e3854c746d5db4cdd3efcd145669897d44c2fbf4f679590b9231c5eac50  how/SKILL.md
384dbe2e16b558f7139b22d6b6acdf07f0a36aa4e000d6402e9b00388b52a422  how/references/critic-prompt.md
8ac5786e430f5043e6eae1ed81e9b8cef5fb5825bf1043428dd5fcfe57f4ed2a  how/references/critique-rubric.md
5a5223f5fe1c22447638fa285cc74f1be98ea53c4941aaa4231260ee84a384e0  how/references/explainer-prompt.md
0cf798751cf535d35697b7902d19d257da0a1e046337d18a40759fd5ec109f76  how/references/explorer-prompt.md
9810975a10c402bf2a53928186f5925c8b69d42e26b5a279969f58843a593314  code-tracing/SKILL.md
1c30901a8123b7bda100df652d83d9ed2f27250a6f178711c13811f9cd5f9221  code-tracing/evals/evals.json
a8d50abac5a4018f60e1d911d4b6f4e36454ca14d6c390c0695a578c7de65dad  codebase-design/SKILL.md
125e6b77413ad2bc7cf7a772bc74336d580a50f9e797db2178ed133d62333d06  codebase-design/DEEPENING.md
21c3264953bd30ee87b181a3ccaf0e70649f461e5ffd7dc654acee4ba1788b31  codebase-design/DESIGN-IT-TWICE.md
edebc9e4fcfe102114012575eaa9600b9b5fd08c311664f389c36e7bc717740f  codebase-design/agents/openai.yaml
4b4cb798c3863d5b6f5c0b4604af1ecb5beb6df82553c972898a91ba38bcf289  improve-codebase-architecture/SKILL.md
0b0936104158abeef7246ff6cbabefa4dc055f17589f2833f2d93001421910a1  improve-codebase-architecture/HTML-REPORT.md
c8cb20f68ebf0edb4e497bc11ae5fcaa196004e661cd189015b04f4109ced7f1  improve-codebase-architecture/agents/openai.yaml
66e5b7724eae5bc5b24f18fafe4c425ba3763c543218ba1c68dcc22c589a99d9  feature-dev/.claude-plugin/plugin.json
8dca1b27e026cab4b8bb8118709935b08fc27d2911efd9e1061b9836b534fbc1  feature-dev/README.md
652e5d6264fd253fcb70c2f84de986a88d77109a02410aacd90230a6ab4bf557  feature-dev/commands/feature-dev.md
3b277703de7458988ec3b8021c716f79f642e174950ed332629310f68322029a  feature-dev/agents/code-explorer.md
c50fb08d59a4bbd19660860626a049e44cf1a2b0c1cf782e6c7a99ba7e71b0c3  feature-dev/agents/code-architect.md
a7df173bf77a00da5584c6401a1061524fdbe477b6fef5dd496d4c7a9113c78c  feature-dev/agents/code-reviewer.md
d6963627a077c6b61aee8b277e99b63f4f52e075b6275ce2beb2e4890eaa7095  ~/.claude/plugins/installed_plugins.json
0e553d6e5eb95b9fc5b63b5f65e15d22bbfef538558e3bb66eea6c6ce27eed1a  ~/.claude/settings.json
```

The source file hashes are reproducible provenance. The two registration hashes describe a whole
mutable registry/settings file and therefore prove only the inspected snapshot; a later hash change
requires re-reading the relevant entries, not assuming the Feature Dev registration changed.

### 10.3 Provisional decisions

- One public job supports four evidence depths; technical-design remains explicit-only and
  project-read-only.
- `how`'s explanation stays here; its independent critic lenses belong to Critique.
- A Critique architecture problem may return through the user with the destination-owned payload in
  section 7.3; Critique never invokes this peer.
- Codebase Design remains an independent reference with a pending user disposition.
- Code Explorer behavior may move into a self-contained candidate only with its separate-context
  delivery preserved.
- Architect remains a retained agent with explicit user-mediated coordination.
- Project mutation, plan creation, testing methodology, diagnosis, shipping, deployment, and
  incident response remain outside the interface.
- Originals remain installed. No validation, preservation, absorption, or retirement approval has
  occurred.

### 10.4 Open authority and design questions

1. **Which tracing artifact governs: the locate-only skill body or the trace-heavy eval bundle?**
   **Consequence:** both locate and trace modes remain provisional, and `code-tracing` cannot retire,
   until original behavior is characterized and the authority conflict is resolved.
2. **Who owns the source's three architecture critics after Critique's code-source expansion?** This
   design assigns public judgment to Critique and retains explanation here, but the existing
   Critique design has not yet consumed this destination profile. **Consequence:** `how` retirement
   and the `cm-codebase-comprehension-01/-04` secondary-role text remain reconciliation work.
3. **What happens to Improve Architecture's Domain Modeling and ADR mutation tail?** Options are an
   explicitly authorized Document/Plan/Implement bridge, permanent source retention, or user-
   approved loss. **Consequence:** the source cannot retire on read-only parity alone.
4. **Does `technical-design` stop after candidate selection or continue into Design It Twice in one
   invocation?** **Consequence:** the later corpus must compare user comprehension, authority
   clarity, and latency before the external interface fixes that interaction seam.
5. **Can the host enforce project-read-only behavior for all agent and delivery adapters while
   allowing an explicit OS-temp report?** **Consequence:** without enforcement evidence, no runtime
   candidate passes the read-only gate even if its observed runs happen not to mutate.
6. **Which immutable version identifies Feature Dev?** The installed registry and cache say
   `unknown`, the manifest omits a version, and the README says `1.0.0`. **Consequence:** bytes may be
   compared by hash, but plugin-level retirement or upgrade claims remain provenance-deferred.
7. **Should `cm-plan-and-spec-14` record Plan as a secondary consumer of Architect output?** This
   design proposes that relation only after the user accepts a blueprint; Plan must confirm its
   payload. **Consequence:** the current primary retained-agent disposition stands, but the
   secondary role remains provisional.
8. **What user decision applies to the reference-ledger `codebase-design` row?** **Consequence:** it
   remains `unassigned` globally and independently installed; this design may consume but cannot
   retire it.

### 10.5 Coordinator reconciliation required

The phase-0 coordinator must apply or reject section 3.4's refined evidence and secondary roles,
reconcile section 7.2 with the other seven public peers, record the section 7.3 destination profile
as canonical if accepted, and leave every row `claimed` rather than `resolved` until the final
roster-wide trigger and ownership pass. This design deliberately does not edit
`docs/phase-0-ledgers.md`, `docs/design-roadmap.md`, any source, or any sibling design.

This draft was self-reviewed against `docs/design-requirements.md` sections 11 and 12. It contains
no placeholder, implementation artifact, runtime validation claim, source-retirement claim, or
authority to change the exact eight-peer public tranche.
