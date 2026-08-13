# Six-skill source-absorption design

**Date:** 2026-08-11

**Status:** Locked phase-0 coordinator allocation record; 92-component target approved by the
user on 2026-08-11; allocations, revised dispositions, and the documentation deferral locked by
the user on 2026-08-12

**Lifecycle authorities:** `astra-critique`, `astra-understand-code`, `astra-spec`,
`astra-implement`, `astra-test`, `astra-ship`

**Reporting surface:** `astra-report` is additional and non-authoritative. Its approved secondary
source slices do not join or change the 92-component target.

## 1. Decision and scope

The approved first absorption target is **92 distinct source component identifiers**:

```text
51 already-planned source identifiers + 41 newly approved identifiers = 92
```

This count is source accounting, not a public-skill count and not a claim that any source is
already behaviorally absorbed. The lifecycle-authority interface remains exactly six skills;
Report is an additional directly invocable presentation surface with no lifecycle authority. The
92-component target records which source behavior the six authority designs must internalize
before any original can be considered for retirement.

This document is the shared evidence and allocation record allowed by
`docs/design-requirements.md` section 6. Each surviving design keeps its own authority and adopts
only its relevant rows. The global roadmap and ledgers remain unchanged in this tranche. A later
coordinator migration may copy these proposals into `docs/design-roadmap.md` and
`docs/phase-0-ledgers.md`, keeping every collision row `claimed`, never `resolved`, until the
roster-wide review is complete.

**Lock record (2026-08-12).** The user reviewed this record and locked its allocations: the
51-identifier baseline in section 2; the 41-identifier expansion in section 3 with its primary
homes and secondary roles; the six revised dispositions in section 7; and the non-absorption
boundary in section 8, including the five-source documentation deferral. A locked row changes
only by a new recorded user decision. The lock fixes disposition ownership so the coordinator
migration can proceed; it does not resolve a ledger row, claim behavioral absorption, satisfy a
retirement gate, or migrate anything by itself.

Phase 0 still creates prose only. This design does not create runtime skills, consultants,
adapters, tests, a harness, an installation, a push, a PR, source retirement, or deletion.

### 1.1 Counting rules

- Count exact source identifiers, including commands and agents, rather than only `SKILL.md`
  registrations.
- Count one source identifier once even when it appears in more than one collision neighborhood.
  `skillify` therefore contributes one identifier although it has Browser & QA and Skill meta
  occurrences.
- Preserve repeated registrations when they are independently invocable. `skill-creator` and
  `skill-creator:skill-creator` remain two identifiers even though their inspected entry files are
  byte-identical.
- Do not count supporting scripts, prompts, fixtures, or skill-scoped agents as additional source
  identifiers unless the inventory registers them independently. Their delivery shapes still
  belong in the parent source's retirement gate.
- Do not count an unavailable built-in toward absorption. Unavailable bytes remain `P`/deferred.

## 2. The 51-component baseline

The 51 identifiers below are the source basis already assigned by the six surviving designs and
the Plan/Debug authority transfers. Their polished prose remains proposed phase-0 evidence, not a
completed absorption claim.

| Surviving primary home | Count | Existing source identifiers |
|---|---:|---|
| `astra-critique` | 22 | `grilling`, `grill-me`, `grill-with-docs`, `/diss`, `/diss-api`, `diss-infra`, `diss-claudemd`, `/elon`, `/trim`, `office-hours`, `plan-ceo-review`, `plan-eng-review`, `plan-design-review`, `plan-devex-review`, `devex-review`, `autoplan`, `design-review`, `investigate`, `diagnosing-bugs`, `superpowers:systematic-debugging`, `java-leak-resolver`, `local-debug` |
| `astra-understand-code` | 4 | `how`, `code-tracing`, `improve-codebase-architecture`, `feature-dev:code-explorer` |
| `astra-spec` | 6 | `superpowers:brainstorming`, `spec`, `to-spec`, `superpowers:writing-plans`, `planb`, `to-tickets` |
| `astra-implement` | 4 | `superpowers:executing-plans`, `superpowers:subagent-driven-development`, `implement`, `code-simplifier` |
| `astra-test` | 7 | `tdd`, `superpowers:test-driven-development`, `bdd`, `spock`, `nextjs-test`, `shell-scripting:bats-testing-patterns`, `superpowers:verification-before-completion` |
| `astra-ship` | 8 | `ship`, `landing-report`, `/pr`, `/commit`, `commit-commands:commit`, `commit-commands:commit-push-pr`, `resolving-merge-conflicts`, `superpowers:finishing-a-development-branch` |
| **Total** | **51** | — |

## 3. Expansion allocation: 41 identifiers

Every row below passes the three-part problem, methodology, and input/output equivalence test.
`Primary home` identifies the design responsible for source fidelity and disposition. Secondary
roles own only their stage-specific authority; they never permit the primary design to perform a
peer's effects.

### 3.1 Code review

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `code-review` — `cm-code-review-01` | skill | `astra-critique` | Standards/spec diff input becomes a Finding Set; Spec, Implement, and Test own remediation | `6a65cc61114f` |
| `review` — `cm-code-review-02` | skill | `astra-critique` | Pre-landing diff findings become a Finding Set; auto-fixes route forward; Ship consumes the final review result | `c803e5d15c02` |
| `requesting-code-review` — `cm-code-review-03` | skill | `astra-critique` | Base/head plus requirements select an independent review context; the review response becomes findings | `a5ff68586ccf` |
| `receiving-code-review` — `cm-code-review-04` | skill | `astra-critique` | Feedback is verified and classified as findings; accepted changes proceed through Spec, Implement, and Test | `c9382e92b8f3` |
| `superpowers:requesting-code-review` — `cm-code-review-05` | skill | `astra-critique` | Same reviewer-context job with its 6.2.0 prompt shape preserved | `d71cc01ba56d` |
| `superpowers:receiving-code-review` — `cm-code-review-06` | skill | `astra-critique` | Same evidence-before-action protocol; mutation is never performed inside Critique | `091df1629510` |
| `feature-dev:code-reviewer` — `cm-code-review-07` | agent | `astra-critique` | Separate reviewer context becomes an internal review adapter; output is a Finding Set | `a7df173bf77a` |
| `code-review:code-review` — `cm-code-review-08` | command | `astra-critique` | GitHub PR discovery and parallel review become review machinery; a posted comment remains a Ship effect | `7d5a0bc9a41b` |

### 3.2 Browser and QA

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `webapp-testing` — `cm-browser-and-qa-08` | skill | `astra-test` | An approved behavior and environment become Playwright evidence in the Test Evidence Packet | `51b7349e77ec` |
| `benchmark` — `cm-browser-and-qa-14` | skill | `astra-test` | A pinned baseline and budget produce repeatable performance evidence and trend facts | `b4b2b9e05a24` |
| `dogfood` — `cm-browser-and-qa-15` | skill | `astra-critique` | Exploratory actions, screenshots, and reproduction video produce observed usability findings | `c86db6b33c8f` |
| `qa` — `cm-browser-and-qa-16` | skill | `astra-critique` | Discovery produces findings; its repair/commit loop is replaced by Spec, Implement, Test, and Ship authority | `1e3f07d20bcf` |
| `qa-only` — `cm-browser-and-qa-17` | skill | `astra-critique` | Report-only exploration produces findings and never gains mutation authority | `dcc6761693de` |

### 3.3 Cross-stack lifecycle and orchestration

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `feature-dev:feature-dev` — `cm-plan-and-spec-15` | command | `astra-spec` | Discovery and approved architecture enter Spec; Understand, Implement, Critique, and Test own their respective stages | `652e5d6264fd` |
| `feature-dev:code-architect` — `cm-plan-and-spec-14` | agent | `astra-spec` | A separate architecture context becomes a bounded Spec advisor; only the user approves the selected solution | `c50fb08d59a4` |
| `superpowers:using-git-worktrees` — `cm-ship-and-vcs-16` | skill | `astra-implement` | Approved isolation setup enters the Delivery Roadmap and Execution Ledger; Ship owns provenance-scoped teardown | `8cfb86f12126` |
| `coding-agent` — `cm-delegation-and-autonomy-01` | skill | `astra-implement` | Approved workdir, task, model, PTY/background mode, and limits become a bounded executor assignment | `94c6b4de7743` |
| `codex` — `cm-delegation-and-autonomy-02` | skill | `astra-critique` | Review, challenge, and consult modes become independent Critique seats/adapters; external-model failures remain explicit | `acb5a9686e5d` |
| `superpowers:dispatching-parallel-agents` — `cm-delegation-and-autonomy-03` | skill | `astra-implement` | Independent approved tasks may run concurrently; integration and final verification remain controller obligations | `1968923066f3` |
| `sdd` — `cm-plan-and-spec-07` | skill | `astra-spec` | Repository artifact state projects the current six-skill stage and next valid entry without creating a seventh authority | `652a1039fe72` |

### 3.4 Diagnostic and domain-design profiles

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `health` — `cm-code-review-12` | skill | `astra-critique` | Quality-tool results, score, and trends become a read-only health Finding Set; Test may consume pinned measurements | `faf103f39b2a` |
| `rca` — `cm-debug-and-incident-04` | skill | `astra-critique` | Timeline, IS/IS NOT, hypotheses, falsification, and causal evidence become `diagnose` findings | `4ca9f6f1a52f` |
| `cso` — reference row | skill | `astra-critique` | Security census, threat model, active verification, severity, and confidence become security findings | `83cb85f852b6` |
| `java` — reference row | skill | `astra-critique` | Java/Spring review output becomes findings; requested refactoring proceeds through Spec, Implement, and Test | `fb17387a7eb3` |
| `design-api` — reference row | skill | `astra-spec` | Requirements, resources, state machines, errors, and idempotency become approved interface requirements; OpenAPI writing is an Implement task | `89fff2b1fb57` |
| `design-db` — reference row | skill | `astra-spec` | Entities, invariants, indexes, and expand/migrate/contract semantics become approved requirements; DDL and rollback scripts are Implement artifacts | `9f3e236a358b` |
| `mcp-builder` — reference row | skill | `astra-spec` | Tool/resource design and evaluation criteria become the approved contract; server code and evaluations proceed through Implement and Test | `0f4592dcb53c` |

### 3.5 Platform and language execution profiles

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `ios-qa` — `cm-ios-01` | skill | `astra-critique` | Live-device exploration produces findings; bridge installation, fixes, and verification route forward | `2ea691e20a63` |
| `ios-fix` — `cm-ios-02` | skill | `astra-implement` | An approved bug specification becomes a scoped edit, rebuild, redeploy, and focused verification record | `4a11fc9ca427` |
| `ios-design-review` — `cm-ios-03` | skill | `astra-critique` | Device screenshots and HIG/design evidence produce visual findings without mutation | `93918baf408a` |
| `ios-sync` — `cm-ios-04` | skill | `astra-implement` | An approved bridge-update task produces generated/source changes and build/device evidence | `5abbb25344c9` |
| `ios-clean` — `cm-ios-05` | skill | `astra-implement` | Approved DebugBridge removal produces a bounded cleanup commit and release-build evidence | `02c45a71495a` |
| `shell-scripting:bash-pro` — reference row | agent | `astra-implement` | A bounded Bash task produces defensive source, tests, and validation evidence; the separate agent context survives | `fb54b5e109ea` |
| `shell-scripting:posix-shell-pro` — reference row | agent | `astra-implement` | A bounded POSIX task produces portable source and multi-shell evidence; the separate agent context survives | `f3573d8989a1` |

### 3.6 Skill-artifact profile

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `skill-creator` — `cm-skill-meta-01` | skill | `astra-spec` | Skill intent, trigger contract, behaviors, and evaluation criteria become an Approved Change Specification | `dcd4803e61e9` |
| `skill-creator:skill-creator` — `cm-skill-meta-02` | skill | `astra-spec` | Same authored body and profile through a separate plugin registration; bundled agents remain tracked | `dcd4803e61e9` |
| `writing-great-skills` — `cm-skill-meta-03` | skill | `astra-spec` | Concision, progressive disclosure, trigger, splitting, and failure-mode rules constrain the skill specification | `4d6ccbc3760b` |
| `superpowers:writing-skills` — `cm-skill-meta-04` | skill | `astra-spec` | Skill RED/GREEN/REFACTOR becomes an approved skill-artifact branch across Spec, Implement, and Test | `d34db5c8aed6` |
| `skillify` — `cm-skill-meta-05`; duplicate occurrence `cm-browser-and-qa-10` | skill | `astra-implement` | An approved browser-flow specification becomes a self-contained script, fixture, tests, staged write, and atomic commit | `15e7912a1d4b` |
| `benchmark-models` — `cm-skill-meta-10` | skill | `astra-test` | Approved prompts, models, budget, and judge criteria produce comparative evidence with cost and latency | `eac159f56b39` |

### 3.7 Durable repository documentation

| Source and ledger record | Type | Primary home | Secondary roles and normalized I/O | Entry sha256 |
|---|---|---|---|---|
| `document-release` — `cm-ship-and-vcs-13` | skill | `astra-implement` | A delivered diff and approved documentation obligations become durable repository prose before publication; Ship verifies the exact revision | `140194ea50eb` |

The expansion therefore contributes **35 skills, 2 commands, and 4 agents**. Primary ownership is
18 Critique, 10 Spec, 10 Implement, and 3 Test identifiers. Understand Code and Ship gain
secondary obligations but no new primary source identifier in this tranche.

## 4. Why these are stack duplicates

| Cohort | Same problem | Same methodology | Compatible inputs and outputs | Why no public peer is added |
|---|---|---|---|---|
| Code review | Judge an existing change and act on supported problems | Diff scoping, independent review, evidence, severity, feedback verification | Revision/spec in; findings, approved remediation, commits, and evidence out | Critique owns judgment and the forward chain already owns every effect |
| Browser and QA | Find or verify failures in a running artifact | Reconnaissance, action, observation, repro, screenshots, focused checks | URL/build/requirements in; findings or Test evidence out | Browser choice is an adapter; exploratory versus pinned evidence selects Critique or Test |
| Lifecycle orchestration | Move an approved change through understanding, design, execution, review, and completion | Phase gates, bounded delegation, isolation, status inspection, independent consultation | Intent and repository state in; the six versioned artifacts out | The source is a compressed controller over authorities the six already separate |
| Diagnostic and domain design | Explain causes, judge quality, or select code-facing contracts | Competing hypotheses, checklists, threat models, state machines, migration planning | Symptoms/requirements in; findings or approved requirements out | Security, Java, API, DB, and MCP are jurisdictions behind existing interfaces |
| iOS and shell | Change and verify code in a specialized runtime | Platform setup, edit/build/run loops, framework-specific checks | Approved task in; source changes and evidence out | Hardware and language details are adapters or bounded agents, not new authority |
| Skill artifacts | Specify, build, test, and publish a repository artifact | Intent refinement, progressive disclosure, RED/GREEN, evals, benchmarks | Skill intent/source in; specification, commits, evidence, and publication out | `SKILL.md` is a repository artifact with a domain profile, not a seventh lifecycle |
| Repository documentation | Keep shipped developer prose accurate | Diff audit, Diataxis coverage, factual editing, review | Delivered diff and doc obligations in; atomic doc changes and publication proof out | Implement already owns durable prose and Ship already verifies it |

## 5. Authority-preserving decomposition

### 5.1 Critique

Critique adopts the 18 primary rows assigned above. It may expose internal review profiles for
code, QA, performance health, security, Java, iOS visual/device review, and causal analysis.
Every profile emits the same Finding Set interface while retaining its source-specific evidence,
confidence, severity, and prerequisite fields.

Critique never performs a source's auto-fix, instrumentation, bridge installation, refactor,
commit, PR comment, or publication step. Those effects become findings and proceed through Spec,
Implement, Test, and Ship. `rca` joins `diagnose`; live-outage stabilization remains the separate
`firefighting` job outside the six-skill coding stack.

### 5.2 Understand Code

Understand Code receives no new primary row. It remains the read-only current-state authority used
when Feature Dev, API/DB/MCP design, QA, iOS, or skill-artifact work needs an explicit
Understanding Report. It does not inherit architecture selection from
`feature-dev:code-architect`, QA findings, or implementation authority from any platform profile.

### 5.3 Spec

Spec adopts ten primary rows. Its small interface remains the Approved Change Specification;
Feature Dev, SDD, API, database, MCP, and skill-authoring behaviors become selectable internal
profiles. The profiles may add domain-specific fields, but every selected solution, rejected
alternative, state transition, interface, migration order, acceptance case, and user decision
remains Spec authority.

Architecture agents advise; they do not decide. Generated OpenAPI, DDL, MCP server code,
`SKILL.md`, fixtures, or scripts are repository delivery tasks owned by Implement rather than
content silently written during Spec.

### 5.4 Implement

Implement adopts ten primary rows. Its Approved Delivery Roadmap chooses the required worktree,
executor, platform/language profile, exact files, generated outputs, focused checks, atomic commit
boundaries, and stop conditions. Its Execution Ledger preserves every external-agent invocation,
device or runtime prerequisite, output, failure, residual process, and protected pre-existing
change.

Implement never treats a source's autonomous fix or commit default as authority. Worktree creation,
agent dispatch, iOS bridge changes, shell specialization, skill generation, and repository-doc
edits occur only as approved Roadmap tasks. The source-specific tool remains an adapter behind the
Implement interface until a self-contained candidate proves it can replace that delivery shape.

### 5.5 Test

Test adopts three primary rows and receives secondary evidence obligations from QA, iOS, shell,
MCP, database, API, Java, and skill-artifact profiles. `webapp-testing`, `benchmark`, and
`benchmark-models` extend Test's evidence methods without changing its independent authority.
Exploratory runs without pinned requirements remain Critique work.

Test records exact runtime, browser/device/model, baseline, cost, timestamps, commands, outputs,
and residue in the Test Evidence Packet. It does not repair a QA failure, edit a benchmark to pass,
or weaken a skill evaluation criterion.

### 5.6 Ship

Ship receives no new primary row. It owns only publication effects that survive the decomposition:
posting an authorized review comment, verifying worktree teardown, publishing an evaluated skill
artifact, and confirming that `document-release` obligations cover the exact head. It may not use
those secondary roles to change code, tests, docs, findings, requirements, or the Execution Ledger.

## 6. Preserved delivery shapes and prerequisites

| Source family | Delivery shape that survives | Failure or degradation that must remain visible |
|---|---|---|
| Request/review sources | Fresh independent reviewer context, explicit base/head/spec package, confidence/severity calibration | Reviewer unavailable or ambiguous baseline stops or degrades explicitly; no self-review is presented as independent review |
| Browser/QA | Python Playwright helper, browser CLI/MCP adapters, screenshots, videos, console/network capture | Missing browser, authentication, runtime, or recording support is recorded; report-only modes never acquire edits |
| Feature Dev | Separate Explorer, Architect, and Reviewer contexts plus the command's phase order | The plugin has `version: unknown`; content hashes are the current provenance and retirement stays blocked until a stable revision is pinned |
| Worktrees and delegation | Native workspace when available, `git worktree` fallback, ignored-directory check, baseline tests, PTY/background and external-model adapters | Dirty baseline, unsupported isolation, failed setup, executor failure, timeout, or unavailable model stops according to the Roadmap |
| Health/RCA/CSO | Read-only tool runs, longitudinal health history, timeline and hypothesis artifacts, independent security verification | No tool result is invented; low-confidence or unavailable checks remain gaps; incident stabilization is not smuggled into RCA |
| API/DB/MCP | OpenAPI, ERD, migration/rollback, tool schemas, language-specific MCP SDK guidance, evaluation questions | Database/provider/framework choice and external documentation are pinned; deploy effects remain out of scope |
| iOS | DebugBridge package, StateServer tunnel, real-device screenshots/state, build/deploy tools, cleanup/sync generators | Missing device, signing, tunnel, or build capability fails visibly; instrumentation requires an approved forward task |
| Shell agents | Separate Bash and strict POSIX contexts, ShellCheck/shfmt, Bats/ShellSpec, multi-shell validation | Missing target shells/tools narrows evidence explicitly; destructive shell examples are not copied as authority |
| Skill authoring | Skill-scoped analyzer/comparator/grader agents, eval fixtures, review UI, trigger optimizer, browser script fixture, model judge | Duplicate registrations remain separately traceable; cost/model approval and absent eval machinery stop or reduce assurance |
| Document release | Authored template plus Diataxis release body, architecture-doc drift check, CHANGELOG safeguards | It moves before publication; no silent VERSION bump, CHANGELOG clobber, or unrelated documentation sweep is authorized |

Static knowledge files may remain internal references, but a retirement candidate must become
self-contained. Composition by reaching sideways into an original skill is acceptable only in the
temporary reference convener, never in the final candidate.

## 7. Prior decisions revised by the approved target

The user's approval of the 92-component target on 2026-08-11 revises these provisional or older
allocations at the design layer:

| Earlier decision | Revised disposition | Preserved distinction |
|---|---|---|
| `rca` provisionally routed to `astra-incident` under roadmap D3 | Causal investigation moves to Critique `diagnose` | `firefighting` retains live-outage stabilization, operational commands, and incident communication outside the coding stack |
| `sdd` kept as an independent reference under D7 | Workflow navigation and artifact-state projection move to Spec/the stack | `/sdd update` remains a setup adapter or explicit retirement residue; Spec gains no installation authority |
| `health` kept as an independent reference under D7 | Read-only code-health judgment moves to Critique | Longitudinal history and composite scoring remain a health profile; Test consumes only pinned evidence |
| `feature-dev:code-architect` retained as a coordinated external agent | The job moves to Spec while the separate agent context remains an internal delivery shape | The advisor cannot select or approve architecture |
| `document-release` deferred to an unwritten `astra-document` | Repository-change documentation moves to Implement, with Ship verification | Standalone non-repository writing remains outside this tranche |
| Provisional `astra-qa`, `astra-ios`, and `astra-skill-design` peers | Their coding-lifecycle slices become profiles across the six | Browser capability, iOS hardware, and skill-evaluation machinery remain explicit adapters and prerequisites |

The user locked all six revised dispositions on 2026-08-12. These revisions do not silently alter
the global ledger. The later migration must cite the 2026-08-11 approval and the 2026-08-12 lock
and preserve the historical rows as superseded evidence.

## 8. Explicit non-absorption boundary

The following nearby sources do not enter the 92 target because at least one equivalence axis
fails:

- Browser-control and environment adapters such as `agent-browser`, `browse`, cloud-browser,
  Electron, Slack, cookie setup, and the Playwright MCP expose capability I/O rather than a coding
  lifecycle artifact.
- `scrape` produces extracted data; `pair-agent` grants scoped browser access; neither shares the
  six-skill problem or output.
- `firefighting`, `triage`, deployment/canary/setup, recurring automation, safety enforcement,
  context serialization, and configuration change operational state or authority outside the
  six artifacts.
- `research`, `codebase-design`, `github`, `security`, `karpathy-guidelines`, and static
  provider/language guides remain independently addressable references rather than workflows with
  equivalent authoritative output.
- `commit-commands:clean_gone` retains a distinct destructive branch-cleanup job and its recorded
  authority defect.
- Product design, brand, art, communications, meetings, retrospectives, model training,
  deployment, and publication formats with their own durable artifacts remain separate jobs.
- Unavailable built-ins remain deferred because no problem/method/I/O conclusion can substitute
  for inspectable source bytes.

The five standalone repository-documentation candidates—`document-generate`, `/doc`, `rtfm`,
`claude-md-management:revise-claude-md`, and
`claude-md-management:claude-md-improver`—remain outside this first target. On 2026-08-12 the user
locked this deferral: none of the five joins the 92 target in this tranche, each keeps its current
independent registration, and no surviving design may claim one as a primary or secondary home
without a new recorded user decision. Whether docs-only change cycles belong to the six-skill
coding job remains that later, separate decision. Deferral is a scope boundary, not inspection
evidence: it supports no exclusion, absorption, or retirement claim for these five sources.

## 9. Manual bridge before implementation

Until a self-contained candidate exists, use the original source only inside the authority stage
that owns its effect:

1. Start with Critique for an observed problem, or Spec for greenfield intent.
2. When specialist evidence is needed, invoke the matching original with immutable input
   references and retain its unmodified output as source evidence.
3. Manually translate that output into the active Astra artifact without granting the original
   any broader authority. Review/diagnostic results become findings; design results become
   requirements; executor results enter the Execution Ledger; verification results enter the Test
   Evidence Packet.
4. Stop before any source-native mutation, commit, push, PR, install, device instrumentation, or
   publication effect that the active Astra stage does not own.
5. Record missing prerequisites, source failures, and translation loss. Do not call the bridge
   absorption or retirement evidence.

This bridge is the reference convener. The source oracle remains the strongest applicable
original for each jurisdiction. The future self-contained candidate must reproduce the retained
behavior without reading the originals.

## 10. Validation and retirement gates

### 10.1 Corpus classes

The fixed comparison corpus must cover:

- one home-jurisdiction case for every one of the 92 source identifiers;
- every source-specific mode and authority difference named in sections 3 and 6;
- cross-stage bundles such as `qa`, Feature Dev, iOS QA/fix, MCP building, skill creation, and
  document release;
- expected-divergence cases where reviewers, causal hypotheses, databases, languages, platforms,
  or evidence thresholds should differ;
- expected-convergence controls where equivalent sources should reach the same supported result;
- missing browser/device/model/tool/credential/runtime cases; and
- forbidden-effect cases proving that Critique and Test stay read-only, Spec does not write
  delivery artifacts, Implement does not publish, and Ship does not reinterpret upstream work.

### 10.2 Source-specific retirement obligations

| Source set | Gate required before its originals can retire |
|---|---|
| Eight code-review identifiers | Preserve standards/spec separation, independent contexts, severity/confidence, feedback verification, base/head selection, and authorized external-comment behavior |
| `webapp-testing` | Match Python Playwright setup, reconnaissance-first operation, logs/screenshots, helper behavior, and failure cleanup |
| `benchmark` | Match baseline identity, repeated measurements, performance budgets, trend comparison, and browser degradation |
| `dogfood` | Match exploratory coverage, step screenshots, repro video, and actionable evidence without source mutation |
| `qa` | Preserve the full find/fix/reverify value while proving every effect is routed through Spec, Implement, Test, and Ship |
| `qa-only` | Prove report-only behavior and equivalent defect/reproduction quality with zero repository mutation |
| Feature Dev command and two added agents | Preserve discovery, clarification, architecture options, user approval, separate contexts, implementation handoff, and independent review; resolve the unknown plugin revision |
| `using-git-worktrees` | Preserve consent, native-first fallback, ignore safety, dependency setup, clean baseline evidence, and provenance-scoped teardown |
| `coding-agent` | Preserve workdir, CLI/model choice, PTY/background operation, progress, timeout/error reporting, and optional isolated workspace |
| `codex` | Preserve review/challenge/consult modes, read-only use, model/session selection, cost visibility, and failure handling |
| `dispatching-parallel-agents` | Preserve independence analysis, focused task briefs, concurrency, integration review, and final whole-result verification |
| `sdd` | Preserve artifact-state diagnosis, ambiguity/staleness detection, one-next-action output, backward-flow guidance, and explicit setup/update residue |
| `health` | Preserve read-only tool detection, raw failures, composite score, configuration distinction, persistent history, and trend explanations |
| `rca` | Preserve timeline, IS/IS NOT, interaction map, at least three hypotheses, falsification, reproduction, and evidence-backed cause without taking stabilization authority |
| `cso` | Preserve attack-surface census, secrets/history/supply-chain/LLM/OWASP/STRIDE jurisdictions, daily/comprehensive confidence gates, independent verification, severity, and trend output |
| `java` | Preserve Java/Spring/MyBatis/Java-21 jurisdiction, structured review output and scoring, while routing optional refactoring forward |
| `design-api` | Preserve resource/state/actor modeling, idempotency, permission and error matrices, OpenAPI completeness, and review checklist |
| `design-db` | Preserve MySQL/PostgreSQL distinctions, entities/constraints/index rationale, ERD, forward/rollback scripts, and migration safety ordering |
| `mcp-builder` | Preserve protocol/framework research, tool discoverability, structured outputs/errors, implementation guidance, tests, and ten realistic evaluations |
| Five iOS identifiers | Preserve real-device state, DebugBridge/StateServer lifecycle, screenshots, HIG review, rebuild/redeploy, regression evidence, sync, cleanup, and release-build checks |
| Bash and POSIX agents | Preserve separate language contexts, defensive/portable source, documentation, Bats/ShellSpec, ShellCheck/shfmt, multi-version or multi-shell evidence, and safe degradation |
| Two `skill-creator` registrations | Preserve both invocation identities, the authored body, analyzer/comparator/grader delivery shapes, eval viewer, qualitative/quantitative iteration, and trigger optimization |
| `writing-great-skills` | Preserve concise descriptions, progressive disclosure, split/prune decisions, references, and failure-mode guidance |
| `writing-skills` | Preserve skill-specific RED/GREEN/REFACTOR, rationalization resistance, testing pressure, and deployment checklist |
| `skillify` | Preserve successful-flow capture, self-contained browser script, fixture, tests, staged write, user approval, atomic commit, and post-write verification |
| `benchmark-models` | Preserve same-prompt cross-model runs, cost approval, latency/token/cost measures, optional judging, and reproducible baseline output |
| `document-release` | Preserve complete doc discovery, Diataxis coverage, architecture drift, factual repository edits, CHANGELOG/VERSION safeguards, documentation debt, and exact-revision publication proof |

Every set must pass home-jurisdiction non-regression against its source oracle. Cross-source
coordination must demonstrate at least one positive advantage over the strongest oracle. The
self-contained candidate must match the reference convener on retained behavior and delivery
shape. Any failure narrows or rejects the relevant profile and blocks retirement of the affected
source; it does not invalidate unrelated source rows automatically.

## 11. Provenance and open work

The 41 entries were re-inspected on 2026-08-11. gstack authored templates are from clean revision
`a3259400a366593e0c909dd9ac3e59752efd2488`, release `1.60.1.0`. Superpowers entries are package
`6.2.0`. Shell agents are package `1.2.3` and marketplace revision
`c4b82b0ad771190355eb8e204b1329732a18449a`. `monster-prompt` and its vendored Anthropic sources
were read at clean revision `e39e86c76d7a720cc94635413292598294c374db`. Feature Dev,
`code-review:code-review`, and the namespaced Skill Creator cache paths still report version
`unknown`; their content hashes are reproducible, but a stable upstream release pin remains a
retirement prerequisite.

The short hashes in section 3 identify the exact entry bytes. Supporting-body records in the
existing per-skill designs and component ledger remain part of the evidence: Feature Dev's three
agents, Requesting Code Review's reviewer prompt, Skill Creator's analyzer/comparator/grader,
gstack authored templates and section files, webapp-testing helpers, MCP Builder references, and
iOS bridge/runtime assets cannot be discarded as implementation detail.

Coordinator sequence after the 2026-08-12 lock and 2026-08-13 trigger reconciliation:

1. migrate the 41 dispositions and seven reference rows into the coordinator-owned ledger —
   complete in roadmap amendment 7;
2. reconcile the older 24-skill roadmap with the six lifecycle authorities and these profiles —
   complete in roadmap amendment 7;
3. reconcile all 15 directed consultant pairs and the final trigger surface — complete in
   roadmap amendments 8 and 9;
4. select one non-retiring vertical slice, write only its behavioral acceptance cases, and
   capture drift-risk oracle behavior; no reusable harness is designed up front;
5. implement and dogfood the slice while allowing minimum runner mechanics to emerge from
   demonstrated needs; and
6. widen the corpus or extract a reusable harness only after repeated needs justify stable seams,
   then run source-specific gates before requesting any preservation or retirement decision.

### 11.1 Coordinator progress after the lock

Roadmap amendment 7 completed items 1 and 2 while keeping every migrated collision row `claimed`,
not `resolved`. Roadmap amendment 8 and the 2026-08-12 pair-first audit completed the 15-pair half
of item 3. Roadmap amendment 9 and the trigger-surface audit complete the remaining half, so
**item 3 is complete**. The approved slice-first resequencing changes section 11's open-work
ordering, which the allocation lock did not freeze; it changes no locked allocation, source
denominator, or ledger state. Items 4–6 now separate acceptance evidence, slice implementation,
and only then reusable harness extraction or corpus growth. No runtime, corpus runner, reusable
harness, installation, deletion, or retirement authority follows from this progress.
