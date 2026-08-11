# Astra Test — phase-0 design

**Date:** 2026-08-03 · **Six-skill reconciliation:** 2026-08-11 · **Status:** `proposed`

> **Authority.** `docs/phase-0.md` governs phase scope and ledger ownership;
> `docs/design-requirements.md` is the sole per-skill contract; the current user handoff fixes the
> public drafting tranche and its order. This document proposes one design. It does not implement a
> skill, edit either global ledger, install or remove a dependency, validate behavior, or authorize
> retirement.
>
> **Conformance.** Sections 1–10 map one-to-one and in order onto
> `docs/design-requirements.md` sections 7.1–7.10. Section 11 applies the cumulative consultant,
> immutable-artifact, and new-cycle rules in requirements section 7.11 and governs conflicting
> eight-peer wording. The available bodies for
> `cm-testing-01..07`, their directly relevant registrations, and every file in their source bundles
> were inspected in full. `cm-testing-08` (`run`) has no inspectable immutable body and remains
> provenance-deferred.
>
> **Certainty labels.** **O** = observed directly in an inspected artifact or current registration;
> **I** = inferred or proposed and still requires reconciliation or later validation; **U** =
> unavailable. Unless a source claim is marked **I** or **U**, source claims in this document are
> **O**. Design choices are proposals, not observed runtime behavior.
>
> **Coordinator gap.** All eight assigned ledger rows are currently `unclaimed` and `unassigned`.
> Section 3.3 proposes exact changes, but only the phase-0 coordinator may apply them. Originals
> remain installed.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-test` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhood | Testing (`cm-testing-01..08`) |
| User job | **When I want to establish fresh, rerunnable evidence that accepted behavior holds, including the tests and framework setup needed to prove it.** |
| Accepts Critique handoff | **yes** — the owned problem class is `test-evidence-gap`; see section 7.3 |

The job has one outcome: trustworthy evidence. Constructing a test, applying a framework-specific
playbook, executing it, and checking whether a claim is supported are modes that contribute to that
outcome. They do not turn Test into the owner of product intent, production-code mutation, causal
diagnosis, independent judgment, or publication.

**Personal value: explicit.** The user selected `astra-test` for the reconciled public stack:
`astra-critique`, `astra-understand-code`, `astra-spec`, `astra-implement`, `astra-test`, and
`astra-ship`. Plan and Debug remain superseded historical evidence. The user also explicitly requires
construction, framework, execution, and final-verification modes to remain distinct. That is direct
evidence of personal project-development value. As supporting evidence only, the inventory records
six agent-fired uses of `superpowers:test-driven-development`, the only usage in this neighborhood.

`now` prioritizes completing this design contract. It does not imply that a runtime skill exists or
that any source is ready to retire. Context, Guard, Delegate, Automate, Incident, and Deploy are
deferred general-purpose concerns; section 7.4 names only honest manual or external bridges for them.
They are not public peers, internal modules, or absorbed capabilities in this design.

---

## 2. Interface and scope

### 2.1 Requests that should trigger it

- “Write or update tests for this accepted behavior,” with a specification, contract, bug
  reproduction, or approved plan that supplies the expected behavior.
- “Work test-first at these agreed seams,” including a request to produce the next failing test and
  its red evidence before any production change.
- “Create Behave features from this OpenAPI contract,” “write Spock tests,” “test this Next.js
  change with Vitest or Playwright,” or “add Bats coverage for this shell script.”
- “Bootstrap the test framework or CI test step,” when the user has explicitly authorized the
  bounded test-infrastructure files and dependency changes.
- “Run these tests,” “do the tests pass at this revision?”, or “collect fresh evidence for this
  completion claim.”
- “Verify this regression proof,” when the expected red and green states, snapshot, and permitted
  effects are explicit.

### 2.2 Nearby requests that should not trigger it

| Request | Owner or current bridge | Why Test stops |
|---|---|---|
| “What should this product or API do?” | `astra-spec` | Test consumes accepted behavior; it does not invent it |
| “Explain this subsystem or choose its architecture” | `astra-understand-code` | Comprehension and technical design are not evidence construction |
| “Turn the accepted behavior into exact repository delivery work” | `astra-implement` | Implement owns dependency order and mutation scope under the approved Specification |
| “Change the production code so this test passes” | `astra-implement` | Test may write test/evidence artifacts, never production code |
| “Why is this failure happening?” | `astra-critique diagnose` | A failing test is evidence, not a diagnosis |
| “Judge whether this implementation or test strategy is good” | `astra-critique` | Independent judgment remains read-only and public |
| “Commit, push, open a PR, merge, release, or deploy this” | `astra-ship` for publication; deployment remains external | Fresh evidence carries no publication authority |
| Exploratory browser QA or an operational probe without an accepted assertion | Explicit manual/external workflow | This design owns reproducible tests and evidence, not an extra public peer |

### 2.3 Conceptual input

One invocation supplies or makes resolvable:

1. an Approved Change Specification or other accepted-behavior authority, plus its immutable
   identity and acceptance criteria;
2. the artifact and immutable-enough target snapshot: repository/worktree, revision or dirty-state
   note, relevant paths, and existing test assets;
3. the evidence target: behavior, regression, framework setup, suite, or completion claim;
4. the requested mode, or permission for Test to recommend one of the four modes in section 6;
5. writable **test/evidence-artifact scope** and forbidden files/effects;
6. available runtimes, exact project-native commands when already known, and required environment;
7. permission or prohibition for dependency installation, network access, live endpoints, test-data
   creation, and cleanup; and
8. the freshness requirement and any evidence the caller already has; and
9. on the primary change path, the Approved Delivery Roadmap, Execution Ledger, atomic commit
   identities, and exact delivered revision.

An absent accepted behavior, target snapshot, or effect boundary is a stop condition. Test may ask
the user to resolve it or name the relevant peer; it may not guess and continue.

### 2.4 Small public interface and user-visible result

The future module exposes one conceptual operation: **establish evidence for this accepted
behavior at this artifact snapshot**. A caller may request one mode or an ordered combination, but
does not need to know which source playbooks or framework adapters sit behind the seam.

The result is a reusable, versioned **Test Evidence Packet** plus any authorized test artifacts.
It carries an immutable packet ID, revision, content hash, input artifact identities, consultant
determinations, and exact tested revision. It records:

- accepted-behavior and artifact-snapshot references;
- selected mode and framework jurisdiction, including why routing was certain or uncertain;
- created or changed test, fixture, test-config, and CI-test files;
- agreed test seams and independently derived expected results;
- exact commands, working directories, material environment facts with secrets redacted, start/end
  state, exit status, failure count, and relevant output or artifact paths;
- red evidence, green evidence, and mutation-sensitivity evidence when applicable;
- coverage or dry-run evidence only when actually produced, with the tool and denominator stated;
- gaps, unavailable prerequisites, partial runs, cleanup state, and unsupported claims;
- any production change, specification decision, diagnosis, critique, or publication action still
  owned elsewhere; and
- an overall state of `supported`, `failed`, `blocked`, or `inconclusive`, never an invented pass.

The packet is the stable peer artifact. A passing test alone is not enough when the requested claim
also needs a typecheck, build, lint, E2E run, or line-by-line requirement check. Conversely, failure
does not authorize a production fix.

### 2.5 Effect authority and non-goals

With explicit scope, Test may create or edit test sources, fixtures, test helpers, test-runner
configuration, test-only CI steps, and evidence reports. Test dependency manifests and lockfiles are
included only when the user separately approves framework bootstrap. Test may execute approved
commands and create their normal test artifacts or bounded test data.

Test does **not**:

- edit production source, weaken production validation, or delete pre-test production code;
- change accepted product/API behavior or silently rewrite a failing assertion to match the server;
- choose architecture, write an implementation plan, diagnose an unknown cause, or repair code;
- issue a quality score or absorb Spock’s mandatory implementation-review judgment;
- silently create a reviewer agent, invoke Critique, Implement, Debug, or any other peer;
- treat plugin-level tool pre-approval as a hard runtime restriction or as mutation authorization;
- install packages, use a live endpoint, create remote data, or clean it up without the user’s
  explicit effect decision;
- claim unrun, stale, partial, delegated, or unread verification as current evidence; or
- commit, amend, push, open a PR, merge, release, deploy, or retire a source.

### 2.6 Decisions that remain with the user

The user confirms test seams; resolves ambiguous expected behavior; chooses between materially
conflicting TDD policies; authorizes test-infrastructure files and dependency changes; permits any
network, live-system, test-data, or cleanup effect; decides whether a failing result is a product
bug, a changed specification, or a test defect when the evidence does not settle it; approves any
production mutation through Implement; accepts or rejects incomplete evidence; and chooses whether
to start a new Critique cycle or Ship after Test stops.

---

## 3. Source evidence

### 3.1 Inspection record

All available bundle files were read in full on 2026-08-03. A bundle hash is the SHA-256 of the
sorted `sha256sum` output for every relative file path under that source root; section 10 records
the command and per-file hashes. Registration metadata was inspected separately so a skill body is
not mistaken for its complete delivery shape.

| Occurrence and source | Component, live registration, invocation, availability | Complete declaration and bundle | Behavior, authority, dependencies, and failure behavior | Provenance |
|---|---|---|---|---|
| `cm-testing-01` — `tdd` | Standalone skill; `~/.claude/skills/tdd` symlink → `~/.agents/skills/tdd`; exact skill name `tdd`; **live** | Frontmatter: `name`, `description`; OpenAI interface metadata only (`display_name`, `short_description`); `SKILL.md`, `tests.md`, `mocking.md`, `agents/openai.yaml` | General red→green construction; user-confirmed public seams; vertical slices; behavior-facing tests; independently derived expectations; mocks only at system edges. It reads optional `CONTEXT.md`/ADRs. It says refactoring belongs to review, not its loop. No explicit tool or effort field. Missing seam confirmation stops test writing. Its green step implies production mutation, which Test cannot inherit. | Main `5363bb27…`; bundle `8a73e40f…` |
| `cm-testing-02` — `superpowers:test-driven-development` | Plugin skill in enabled `superpowers@claude-plugins-official` 6.2.0; exact invocation name `superpowers:test-driven-development`; **live**; identical body in the Codex 6.2.0 cache | Frontmatter: `name`, `description`; `SKILL.md` plus `writing-good-tests.md`. The Codex plugin advertises plugin-wide Interactive/Read/Write capability; this is registration metadata, not per-invocation authority. | Strict red→verify-red→green→verify-green→refactor; applies to features, fixes, refactors, and behavior changes unless the human approves a named exception. It requires real behavior, independent expectations, complete mocks, and a mutation check. Wrong red/errors loop until the expected failure; failures are fixed rather than hidden. Its delete/rewrite and production-green steps remain Implement effects. | Installed commit `eafe962b…`; main `bf1b8216…`; bundle `b23b6e44…` |
| `cm-testing-03` — `bdd` | Standalone skill; `~/.claude/skills/bdd` symlink → the `monster-prompt` source tree; exact skill name `bdd`; **live** | Frontmatter: `name`, `effort: high`, multiline `description`; `SKILL.md`, three prompt files, and two references | OpenAPI-driven Python Behave construction: explicit HTTP Gherkin, journeys plus endpoint constraints, positive/negative/security/auth cases, generated clients rather than handwritten HTTP, dynamic data, real responses, multi-environment config, cleanup, coverage audit, and zero undefined steps on dry-run. Requires OpenAPI, Python/Poetry/Behave, generated clients, config/test users, and sometimes a live API. It mandates a fresh coverage-auditor subagent; that delivery shape remains a manual/external bridge here. It forbids faked success and changing spec-derived assertions to match a server bug. `prompts/generate-features.md` cites an absent `coverage-checklist.md`. | Repository `6abccfa5…`; main `7b181df7…`; bundle `f7fcf217…` |
| `cm-testing-04` — `spock` | Standalone skill; `~/.claude/skills/spock` symlink → the `monster-prompt` source tree; exact skill name `spock`; **live** | Frontmatter: `name`, `effort: xhigh`, multiline `description`; `SKILL.md`, `examples.md`, `reference.md` | Java/Groovy Spock unit-test playbook: mandatory implementation review and score, refusal below 7, attack-surface cases, `*Test.groovy`, no Spring boot, mocks/stubs for external dependencies, no Spy, strict interactions, data tables, concurrency probes, and 85% JaCoCo branch/instruction targets. Requires Java/Groovy/Spock/Gradle/JaCoCo and contract evidence. Test failure is reported rather than repaired in production. The quality judgment belongs to Critique, not Test. The body cites an absent `concurrency.md`; its examples acknowledge strict interaction checks can couple tests to implementation. | Repository `6abccfa5…`; main `2e451982…`; bundle `70382106…` |
| `cm-testing-05` — `nextjs-test` | Standalone skill; `~/.claude/skills/nextjs-test` symlink → the `monster-prompt` source tree; exact skill name `nextjs-test`; **live** | Frontmatter: `name`, `effort: xhigh`, multiline `description`; `SKILL.md`, `references/patterns.md` | Next.js 15 decision matrix across Vitest unit tests, RTL, Playwright E2E, and screenshots; one-to-one test paths; self-verification commands; no secrets or unit-test network; optional Vitest bootstrap. Requires Node/pnpm and project-specific packages/config; E2E may require browser/runtime state. Its self-verification loop starts with a production change and prefers fixing implementation on failure—both are Implement effects. Its “caps at 100” utility example expects `110`, an internal evidence inconsistency. The `~33` count is project-specific, not a universal target. | Repository `6abccfa5…`; main `f664eaa7…`; bundle `313d3519…` |
| `cm-testing-06` — `shell-scripting:bats-testing-patterns` | Namespaced skill in enabled `shell-scripting@claude-code-workflows` 1.2.3; body name `bats-testing-patterns`; exact registered invocation `shell-scripting:bats-testing-patterns`; **live** | Frontmatter: `name`, `description`; `SKILL.md`, `references/details.md`; plugin manifests register `skills: ./skills/` for Codex and auto-discovery for Claude | Bats assertions for status/output/files, setup/teardown, fixtures, stubs, error paths, Bash/sh/dash compatibility, parallel runs, and CI/Make integration. Requires Bats plus selected shells and utilities; optional examples use `jq`, npm, Homebrew, or Git. Some examples skip missing tools; others assume them. Cleanup examples use unvalidated `rm -rf` variables and the detailed reference ends at a stray `#`, so invocation safety and missing content must be resolved rather than copied. | Installed commit `b6af3711…`; main `d7992dbf…`; bundle `d68e4849…` |
| `cm-testing-07` — `superpowers:verification-before-completion` | Plugin skill in enabled `superpowers@claude-plugins-official` 6.2.0; exact invocation name `superpowers:verification-before-completion`; **live**; identical body in Codex cache | Frontmatter: `name`, `description`; one `SKILL.md`; Codex interface metadata supplies display text only | Final evidence gate: identify the proving command, run it fresh and fully, read complete output/exit/failure count, compare it with the claim, then state only supported status. It rejects stale, partial, adjacent, or delegated evidence. Regression proof includes red/green; requirements need line-by-line checks. It requires the project’s proving commands and readable output. Reverting a production fix for a red proof and inspecting delegated work are external/manual or peer-owned effects, not Test mutation or Delegate absorption. | Installed commit `eafe962b…`; main `2befe7fc…`; bundle `2e5c5f82…` |
| `cm-testing-08` — `run` | Harness built-in skill; identifier `run`; ledger says **live**, but it has no path, manifest, declaration, inspectable invocation contract, body, bundle, or immutable host-version pin | **U:** all source bytes and declaration fields | **U:** behavior, authority, dependencies, failure behavior, and relation to project-native runners cannot be inspected. Repository inventory supports only the existence/category claim. It cannot inform a candidate adapter or source oracle. | **U / P:** no immutable provenance |

### 3.2 Disposition and contribution

| Source | Proposed contribution | Proposed primary home | Explicit secondary role or limit |
|---|---|---|---|
| `tdd` | **Protocol** (red/green vertical slices) · **Playbook** (seams, behavior tests, independent oracle, mocking) · **Machinery** (optional project-context lookup) | `astra-test` | `astra-implement` owns the minimal production-green half; no automatic invocation |
| `superpowers:test-driven-development` | **Protocol** (strict red/green/refactor with verified transitions) · **Playbook** (good-test gates and mutation check) · **Authority** (human-approved exceptions) | `astra-test` | `astra-implement` owns deletion, production edits, and production refactor; Test preserves the evidence contract |
| `bdd` | **Jurisdiction** (OpenAPI REST acceptance) · **Playbook** (Gherkin, coverage, generated clients, real API) · **Prerequisite** (Behave stack, configs, live environments) · **Separate** (fresh agent context) | `astra-test` | `astra-spec` owns product-contract/annotation changes; the fresh coverage auditor is manual/external until separately justified |
| `spock` | **Jurisdiction** (Java/Groovy unit tests) · **Playbook** (Spock data/interaction/attack patterns) · **Prerequisite** (Gradle/Spock/JaCoCo) · **Separate** (quality judgment) | `astra-test` | `astra-critique` owns implementation-quality judgment and any score/refusal; Test owns only testability and attack-surface facts |
| `nextjs-test` | **Jurisdiction** (Next.js 15 Vitest/RTL/Playwright) · **Playbook** (test-kind routing, patterns, verification) · **Prerequisite** (Node/pnpm/browser packages) | `astra-test` | `astra-implement` owns production changes/fixes; project-specific count targets remain scoped evidence |
| `shell-scripting:bats-testing-patterns` | **Jurisdiction** (shell/Bats) · **Playbook** (fixtures, assertions, dependency stubs, dialects) · **Prerequisite** (Bats and selected shell tools) | `astra-test` | No peer acquires its test behavior; unsafe cleanup and truncated reference remain open defects |
| `superpowers:verification-before-completion` | **Protocol** (evidence-before-claim gate) · **Playbook** (claim-to-command proof, regression and requirement checks) | `astra-test` | `astra-ship` may consume the packet; it receives no commit or publication authority |
| `run` | **U:** no contribution can be characterized | `unassigned` with `defer` disposition | Provenance dependency only; not proposed as absorbed, preserved, excluded, or retirement-ready |

No inspected available source is an alias or delegating stub. The two TDD sources overlap strongly
but contain independently authored, conflicting policy. BDD is both a construction protocol and a
framework jurisdiction; Spock, Next.js, and Bats are framework jurisdictions; final verification is
a distinct protocol. Those differences remain modes rather than being flattened into generic test
advice.

### 3.3 Exact proposed collision-ledger changes

These are proposals inside this design only. The coordinator decides whether to apply them and
keeps every row `claimed`, not `resolved`, until roster-wide reconciliation.

| Occurrence ID | Proposed primary disposition | Proposed primary home | Proposed secondary roles | Proposed claim state | Evidence |
|---|---|---|---|---|---|
| `cm-testing-01` | proposed Astra design | `astra-test` | `astra-implement`: production-green half of TDD, artifact-mediated only | `claimed` | §3.1–§5.1 |
| `cm-testing-02` | proposed Astra design | `astra-test` | `astra-implement`: delete/edit/refactor effects, artifact-mediated only | `claimed` | §3.1–§5.1 |
| `cm-testing-03` | proposed Astra design | `astra-test` | `astra-spec`: accepted OpenAPI contract and annotation authority; fresh auditor stays external/manual | `claimed` | §3.1–§5.2 |
| `cm-testing-04` | proposed Astra design | `astra-test` | `astra-critique`: implementation-quality judgment and score/refusal | `claimed` | §3.1–§5.2 |
| `cm-testing-05` | proposed Astra design | `astra-test` | `astra-implement`: production-change/fix half of the source loop | `claimed` | §3.1–§5.2 |
| `cm-testing-06` | proposed Astra design | `astra-test` | — | `claimed` | §3.1–§5.2 |
| `cm-testing-07` | proposed Astra design | `astra-test` | `astra-ship`: consumes fresh evidence only; `astra-implement`: may consume required commands | `claimed` | §3.1–§5.4 |
| `cm-testing-08` | defer | `unassigned` | —; `astra-test` records **P** only and consumes no behavior | `claimed` | §3.1 **U**, §10 |

**Reference and cleanup ledger:** no change proposed. The inspected official links and runtime tools
are external prerequisites, not live independent-reference entries consumed from that ledger.
The existing `design-review` row already names future Testing as a secondary bootstrap/regression
role; this bounded assignment neither reinspects nor changes that source’s primary disposition.

---

## 4. Collision analysis

### 4.1 Why the entries looked duplicative

Every available description mentions tests, test-driven work, a test framework, or verification.
Several can write tests and run a command. Label-level clustering therefore makes them look like
substitutes. Body inspection shows four different decisions behind that surface:

1. **Construction:** what test should exist, at which seam, and what independently derived outcome
   makes it meaningful;
2. **Framework:** how that test is represented for OpenAPI/Behave, Java/Spock, Next.js, or shell/Bats;
3. **Execution:** which concrete command/environment ran and what it actually returned; and
4. **Final verification:** whether the fresh evidence is sufficient for a specific claim.

### 4.2 Behavior genuinely shared

The seven available sources agree that tests must be tied to observable behavior or a contract,
that expected values must not be changed merely to make a failure disappear, that both success and
failure evidence matter, and that a completion statement must not outrun the command output. They
also produce artifacts that can be passed to another workflow without invoking it.

Shared machinery is limited: intake of an artifact/contract, discovery of existing test tooling,
command execution, output capture, and evidence rendering. The source-specific protocols,
framework rules, prerequisites, and failure behavior do not become generic machinery.

### 4.3 Apparent duplicates that are different jobs

- `tdd` and `superpowers:test-driven-development` are competing general construction policies, not
  aliases. One requires pre-agreed seams and excludes refactoring from its loop; the other includes
  refactoring and applies an iron-law delete/restart policy unless the human approves an exception.
- `bdd` turns an accepted OpenAPI contract into executable acceptance specifications and step
  definitions. It is not generic unit TDD.
- `spock`, `nextjs-test`, and Bats each encode framework and stack jurisdiction. Selecting one
  because of the artifact is routing; merging their instructions into one rubric would be loss.
- `superpowers:verification-before-completion` does not decide what tests to write. It decides what
  evidence a status claim requires.
- `run` may be an execution surface, but that is **U** rather than evidence of equivalence.

### 4.4 Source conflicts and defects that must remain visible

| Conflict or gap | Design consequence |
|---|---|
| `tdd` excludes refactor from the loop; Superpowers includes it | Preserve selectable construction policies; the user resolves policy until later evidence supports a default |
| General TDD prefers public-interface behavior and boundary-only mocks; Spock mandates isolated unit mocks, strict internal interaction counts, and accepts implementation coupling | Framework mode may override the general default only inside the Spock jurisdiction and must report the tradeoff |
| BDD needs real API responses; Next unit tests forbid external network and Bats commonly stubs commands | Execution policy follows the selected jurisdiction; no universal “always mock” or “never mock” rule |
| TDD and Next sources fix or rewrite production code; Test’s authority ends at test/evidence artifacts | Emit a production-change need for the user to pass to Implement; never complete the green step silently |
| Spock’s mandatory score/refusal is independent implementation judgment | Test may gather attack-surface facts, but only Critique or the user supplies that judgment |
| BDD mandates a fresh coverage-auditor subagent | Keep it a manual/external bridge; do not implement or absorb deferred Delegate |
| BDD treats OpenAPI as truth even when the server differs | Record non-compliance and return specification changes to the user/Spec; never normalize the test to the server silently |
| Spock’s 85% thresholds and Next’s `~33` target are source/jurisdiction-specific | No global coverage number appears in the public interface |
| `bdd` lacks `coverage-checklist.md`; Spock lacks `concurrency.md`; Bats details end incomplete; Next contains a contradictory “caps at 100” example | Keep the affected behavior provisional and require source-specific recovery or characterization before retirement |
| `run` bytes and declaration are unavailable | Defer its row; do not use it for routing, internalization, source-oracle comparison, or retirement claims |

### 4.5 Why one coherent deep module is still plausible

The user asks one question across the modes: “What current evidence establishes this accepted
behavior?” The public interface can stay small while internal routing, framework conventions,
prerequisite checks, command capture, and claim gating remain local. Deleting the module would
force every caller to rediscover those four decisions and reconstruct the same evidence packet;
that is useful depth rather than a pass-through.

The framework seam is real because four available adapters vary today: Behave/OpenAPI, Spock,
Next.js testing, and Bats. Construction and final verification are protocols around those adapters,
not extra public skills. The proposal is not a Critique-style panel: the sources do not hold rival
normative perspectives that should all file opinions. Test selects or sequences modes and preserves
their evidence; it does not convene votes.

### 4.6 Declared positive advantage

**I — coordination-quality advantage.** On an artifact whose accepted behavior crosses more than
one test seam—such as an OpenAPI-backed Java service requiring Spock unit attacks, Behave acceptance
scenarios, and a fresh whole-claim verification—the proposed module should retain more supported
critical test gaps and produce more traceable, claim-complete evidence than the strongest single
applicable source, without increasing unsupported claims or duplicate/noise load.

Routing convenience alone is not the claimed win. Section 9 requires both the unchanged-source
convener and the self-contained candidate to beat the preselected source oracle on at least one such
combination class. No comparison has run. If the gate fails, the combined sequence is withdrawn or
narrowed to explicit specialist modes; the design may not continue to claim better testing.

---

## 5. Preserved distinctions

### 5.1 Construction mode

| Behavior that must survive later implementation | Evidence and concrete decision where it matters |
|---|---|
| Confirm the public seam with the user before test writing | `tdd`; prevents a database-side assertion from replacing the caller-visible behavior |
| One vertical tracer at a time | `tdd`; avoids a horizontal pile of tests against imagined structure |
| Independently derive expected values and name the production break each test catches | Both TDD bundles; distinguishes a real oracle from a tautological mirror assertion |
| Watch the red state fail for the expected reason | Superpowers; distinguishes a regression test from a test that already passed or merely errored |
| Verify focused green and the relevant surrounding suite with pristine output | Superpowers; distinguishes local success from a regression elsewhere |
| Preserve `tdd`’s no-refactor loop and Superpowers’ red-green-refactor policy as distinct choices | They can prescribe incompatible next steps after green; no silent default is evidence-backed yet |
| Keep human-approved exceptions explicit | Superpowers; prototype/generated/config exceptions cannot be inferred by Test |
| Keep production deletion, minimal implementation, and refactor outside Test | Required authority split; the evidence packet carries the next needed change to Implement, and the user starts it |

The cross-peer TDD cycle is deliberately visible: Test produces and proves the red test; the user may
start Implement with that artifact; Implement mutates only the approved production scope and returns
a snapshot; the user may start Test again for green and final evidence. Test never invokes Implement
and never reports the cycle complete merely because it emitted a handoff.

### 5.2 Framework mode

**Behave/OpenAPI.** Preserve explicit method/path/body/query/response Gherkin, business journeys,
per-field constraints, positive and negative scenarios, auth/security/error coverage, dynamic data,
generated clients, shared Behave context rather than module globals, async wrappers, real response
propagation, reverse-order cleanup, zero undefined dry-run steps, and environment-specific failure.
The absent `coverage-checklist.md` means its minimum-count/tag guidance is not reproducible. A fresh
coverage audit stays external/manual until section 9 proves an internal replacement.

**Spock.** Preserve `*Test.groovy` naming and mirrored paths, attack cases derived from the contract,
unit isolation, no Spring boot, Mock-versus-Stub choice, no Spy, combined stubbing/verification,
specific argument constraints, terminal `0 * _`, data tables for data-only variation, sequential and
dynamic returns, exception policy, concurrency/idempotency probes, and JaCoCo evidence. The
implementation-quality score and refusal are not Test behavior; the missing `concurrency.md` and the
source’s admitted implementation-coupling tradeoff must remain visible.

**Next.js.** Preserve the source’s unit/E2E/screenshot decision matrix, one-to-one test path
convention, Zod boundary patterns, RBAC mocking placement, sync component accessibility queries,
async Server Component E2E route, test-safe secrets/network rules, self-verification commands, and
optional one-time Vitest setup. Keep its Next.js 15 and project-specific path/count assumptions
scoped rather than global. Production repair remains Implement’s job.

**Bats.** Preserve exit/output/file assertions, setup/teardown, bounded fixtures, function and
command stubs, success/error paths, shell-dialect checks, parallel-case intent, TAP/CI integration,
and explicit missing-tool behavior. Do not preserve unsafe command spelling as a virtue: temporary
cleanup must resolve and validate an actual test-owned directory before deletion. The truncated
reference means no “advanced patterns” behavior is claimed.

These are internal framework adapters at a shared seam, not one flattened rubric. A caller provides
accepted behavior and receives the same evidence-packet shape, while each adapter retains its
jurisdiction’s interface facts, prerequisites, and failure semantics.

### 5.3 Execution mode

Execution preserves the exact project-native command, working directory, target snapshot, material
environment, start/end time, exit status, failure count, and complete relevant output. A local unit
runner, browser-backed E2E runner, and live API acceptance run have different effects and
prerequisites; “tests ran” is not a sufficient normalization.

Missing tooling yields `blocked`; unreachable live systems or unauthorized cleanup yield
`inconclusive` or `blocked`; a nonzero exit yields `failed`. A skipped dependency is recorded as a
skip rather than a pass. Partial output and interrupted commands cannot support a whole-suite claim.
The built-in `run` contributes nothing to this mode until its bytes and host contract become
inspectable.

### 5.4 Final-verification mode

Preserve the source’s five-step gate: identify the command that proves the exact claim, run the full
command fresh, read all output and the exit/failure count, compare evidence to the claim, then state
only what follows. A test pass does not prove a build; a linter does not prove compilation; a diff
does not prove an agent’s result; and a previous run is stale unless the stated freshness contract
says otherwise.

Regression proof must contain an observed red and green state against controlled snapshots.
Production-code revert/restore belongs to an approved Implement or manual isolated-worktree action;
Test cannot manufacture it. Requirements claims also need a line-by-line evidence check. This mode
may produce evidence for Ship, but it owns no commit, PR, merge, or release effect.

### 5.5 Authority, prerequisites, and failure behavior

- Test-artifact writes and test execution are separate permissions. Bootstrap additionally requires
  dependency-manifest/lockfile and network authority.
- Expected behavior comes from Spec, a plan, a bug reproduction, or the user. When source behavior
  and the accepted contract disagree, Test reports both and stops.
- No source frontmatter is treated as enforcement. Plugin-wide Read/Write advertising is not user
  approval, and absence of `allowed-tools` is not a guarantee that writes cannot happen.
- Real API tests may create and delete data. The evidence packet records owner, identifiers, cleanup
  outcome, and residue; missing cleanup authority never triggers guessed credentials or fake data.
- Missing test tooling is reported with the exact failed probe. Test does not install it unless the
  user approved bootstrap.
- A failing test is preserved. Test may repair a defective test inside the agreed test-artifact
  scope when the contract proves the test wrong; it does not weaken a correct assertion or mutate
  production to make it green.
- An unknown cause produces a Debug-ready evidence packet; a known, approved production change
  produces an Implement-ready packet. In both cases the user starts any next workflow.
- Spock’s quality threshold, BDD’s fresh reviewer context, and any delegated-work verification stay
  outside the module unless later evidence and roster authority explicitly relocate them.

---

## 6. Proposed skill design

### 6.1 Deep public module and interface

**Architecture hypothesis:** one deep `astra-test` module behind one external seam. The conceptual
interface takes an accepted-behavior reference, artifact snapshot, evidence target, optional mode,
and effect limits; it returns authorized test artifacts plus one Test evidence packet. The interface
includes its invariants and errors: no accepted behavior or scope means stop; no fresh full evidence
means no pass; production and publication effects are forbidden.

Callers do not select source files, reproduce framework checklists, or interpret runner output
formats. That complexity remains implementation-local, providing leverage to every peer that can
consume the packet and locality when a framework or evidence rule changes. Tests of the future
module should cross this same public seam and assert packet/artifact outcomes, not internal router
state.

### 6.2 Internal modes and modules

| Internal module or mode | Responsibility | Explicit limit |
|---|---|---|
| Intake and authority gate | Resolve contract, snapshot, writable test scope, external effects, and freshness | Cannot infer missing intent or permission |
| Mode router | Select or recommend construction, framework, execution, and final-verification modes; preserve uncertainty | Cannot load `run` or silently choose between conflicting TDD policies |
| Construction mode | Apply selected general TDD protocol; author behavior-facing test artifacts and red evidence | Cannot delete/edit/refactor production code |
| Framework mode | Select one or more justified adapters: Behave, Spock, Next.js, or Bats | Cannot flatten framework rules or invent missing references |
| Execution mode | Preflight and run approved commands; capture environment, effects, complete output, and artifacts | Cannot auto-install, use live systems, or clean up without authority |
| Final-verification mode | Map exact claims to fresh evidence and render supported/failed/blocked/inconclusive status | Cannot turn adjacent/partial evidence into success |
| Evidence ledger | Keep test IDs, behavior anchors, commands, snapshots, red/green states, and gaps traceable | Session-local artifact only; no phase-0 runtime or persistent system is designed here |
| Packet renderer | Produce peer-usable evidence and a named optional next destination | Names only; never invokes a peer |

Construction can feed a framework adapter; either can feed execution; execution can feed final
verification. The modes remain independently requestable. The internal ordering is not a universal
pipeline: a user asking only whether an existing suite passes enters execution and verification,
while a BDD construction request may stop after feature files and dry-run evidence.

### 6.3 Information flow

```text
accepted behavior + target snapshot + effect limits
  → authority and prerequisite preflight
  → explicit or evidence-backed mode selection
  → optional test-artifact construction
  → optional framework adapter
  → approved command execution and effect capture
  → exact claim-to-evidence gate
  → Test evidence packet + authorized artifacts
  → stop
```

If a production mutation is needed between red and green, the flow stops and records it. A later
user-started Test invocation consumes the new snapshot rather than resuming through a hidden
Implement call. If Critique, Debug, or Ship is appropriate, the packet names the candidate and
minimum evidence but starts nothing.

### 6.4 Internal seams and dependency categories

The framework seam is justified by four actual adapters with different artifact formats and
prerequisites. Construction policy is an internal strategy variation justified by the two
conflicting TDD sources. Command execution is a local-runtime seam whose concrete adapters vary by
runner and output shape. Live BDD endpoints are true external dependencies: the module must expose
their absence in the packet and must not substitute fabricated responses.

No generic port or shared Astra module is fixed in phase 0. A production command adapter and an
in-memory test adapter would justify a later internal seam; one hypothetical adapter would not.
Framework reference material stays internal to Test rather than becoming caller-facing or nested
public skills. Shared extraction with another Astra skill remains prohibited until two later
implementations demonstrate the same stable seam and meaningful adapter variation.

### 6.5 Routing, uncertainty, and degradation

- Explicit framework requests win when compatible with the artifact. An auto recommendation names
  its evidence and asks when two policies remain materially valid.
- Missing accepted behavior stops before test authoring. A source/server mismatch is rendered as a
  contract conflict, not silently adjudicated.
- Missing local tooling yields an exact blocked preflight. User-authorized bootstrap may produce a
  bounded dependency/config change; otherwise the packet contains manual prerequisites.
- Missing live credentials/endpoints, denied data creation, or denied cleanup yields a reduced or
  blocked BDD run. No mock is presented as acceptance evidence.
- Missing BDD/Spock references narrow only the affected playbook and block its source-specific
  fidelity claim. The candidate reports the missing rule.
- `run` remains unavailable and never becomes a fallback. Project-native exact commands are used
  only when supplied or discovered from the target project and confirmed.
- Failure to read complete output, count failures, or bind evidence to the snapshot yields
  `inconclusive`, even if a visible tail line says “pass.”

### 6.6 Architectural hypotheses still requiring comparison

The one-interface/four-mode shape, automatic routing, construction-policy selector, multi-adapter
sequence, evidence packet, and any internal replacement for BDD’s fresh coverage auditor are **I**.
The later three-system comparison decides whether they create depth and positive quality or merely
hide useful specialist interfaces. No implementation directory, prompt, schema, router, harness,
or adapter is created in phase 0.

---

## 7. Dependencies and delivery shape

### 7.1 Separate runtimes, tools, and external effects

| Dependency or artifact | Type and relationship | Behavior when absent or unauthorized |
|---|---|---|
| Target repository, accepted contract, revision/dirty snapshot | Input artifact; Test reads and may write only approved test/evidence paths | Stop when identity, expected behavior, or safe separation is missing |
| Project-native test/build/typecheck/lint commands | Local runtimes; execution mode invokes only approved exact commands | `blocked` with probe/command evidence; never infer a pass |
| Python, Poetry, Behave, OpenAPI Generator, generated clients, config/test users | BDD prerequisites | Construction may be partial; dry-run/live evidence is blocked and the exact gap is reported |
| Live API, credentials, test data, cleanup | True external dependency and external effects | Require explicit authority; no fake acceptance result; residue is reported |
| Java, Groovy, Spock, Gradle, JaCoCo | Spock prerequisites | Preserve test artifacts, report unavailable compile/run/coverage separately |
| Node, pnpm, Next.js 15 project, Vitest, RTL, Playwright, browser runtime | Next.js prerequisites | Bootstrap only with approval; unit/E2E evidence degrades independently |
| Bash/sh/dash, Bats, core utilities, optional `jq` | Bats prerequisites | Record skipped dialect/tool separately; do not call the whole suite passed |
| Spock 2.3 documentation URLs | Source-provided external references, not source bodies or independent-ledger entries | The links were observed but not inspected; local syntax guidance remains usable, while unsupported upstream claims stay unverified |
| Fresh BDD coverage auditor | Separate agent context in the original | Manual/external bridge only; not an implemented Delegate capability and not silently invoked |
| Original skill files | Reference-convener inputs only | Missing original invalidates that comparison; a final candidate depending on them is not self-contained |
| `run` built-in | **P** provenance dependency | Remains deferred; no adapter, source-oracle role, preservation claim, or retirement gate until bytes/version are available |

The inspected bundles add no test-specific hook, MCP server, LSP server, background runtime, or
separately invocable agent. `agents/openai.yaml` files are interface metadata, not agent delivery
components. Plugin manifests and symlink registrations remain installed. A later self-contained
candidate may internalize validated playbooks, but it need not vendor true external runtimes; it
must declare and degrade around them.

### 7.2 Relation vocabulary

- **R** means roster reconciliation of ownership, trigger, or relation semantics.
- **I** means a later artifact/capability flow. It does not authorize workflow invocation.
- **H** is only Critique’s zero-or-one user-selected problem capsule naming a destination.
- **P** means provenance/availability must resolve before absorption or retirement can be claimed.

All public peers are flat. Every row below explicitly forbids implicit invocation.

### 7.3 Relations with all seven public peers

| Peer | Relation, direction, and exact information class | Minimum payload | Who starts; unavailable behavior |
|---|---|---|---|
| `astra-critique` | **R:** judgment versus evidence ownership. **H:** Critique → user → Test for `test-evidence-gap`. **I:** Test evidence may be supplied to a later Critique run. Neither invokes the other. | H profile below plus Critique common envelope; reverse evidence is the packet’s snapshot, commands, results, gaps, and test IDs | User selects zero or one Critique route and separately starts Test. Missing/inconsistent profile stays in Critique’s report. If Critique is unavailable, Test still runs from accepted behavior but makes no independent quality judgment |
| `astra-understand-code` | **R:** explanation/technical-design versus test-seam ownership. **I:** Understand Code → Test may supply observed paths, public interfaces, invariants, dependency map, and evidence anchors. No invocation. | Artifact snapshot; relevant paths/symbols; observed interfaces/invariants; uncertainty; accepted architecture constraints | User supplies the artifact. If unavailable, Test proceeds only when the contract and seams are independently clear; otherwise stop |
| `astra-spec` | **R:** product/API intent versus executable evidence. **I:** Spec → Test supplies accepted behavior and contract version; Test → Spec may return observed contract/server disagreement. No invocation. | Spec/OpenAPI ID and version; acceptance examples; required/forbidden behavior; unresolved decisions; compatibility constraints | User starts Test with the accepted contract. If absent or ambiguous, stop for user/Spec resolution rather than invent expected behavior |
| `astra-plan` | **R:** test strategy/evidence obligations versus production execution ordering. **I:** Test → Plan supplies seams, test artifacts, exact commands, prerequisites, and evidence gates; Plan → Test may supply approved task scope and required checks. No invocation. | Plan/spec reference; target snapshot; seams; command/cwd; expected outcomes; fixture/environment needs; effect limits | User chooses which artifact crosses. Without a sufficient plan, Test can still answer a bounded direct testing request; it cannot plan production mutation |
| `astra-implement` | **R:** test-artifact authority versus production mutation. **I:** Test → Implement supplies red/failing evidence and required commands; Implement → Test supplies the changed snapshot for green/final evidence. This is a visible user-mediated loop, not **H**, and neither peer invokes the other. | Accepted behavior; test IDs/files; seam; exact red/failing command/output; expected green; allowed production scope if already approved; snapshot/base | User starts each half. If Implement is unavailable, Test returns red/failed evidence and stops; it never edits production |
| `astra-debug` | **R:** failure observation versus unknown-cause diagnosis. **I:** Test → Debug supplies a reproduction/evidence packet; Debug → Test may return an identified fix snapshot and regression target. This is not **H** and no invocation occurs. | Failing command/cwd/snapshot; full relevant logs; deterministic/non-deterministic note; environment; last-known-good; attempts limited to test scope | User decides whether Debug starts. If unavailable, preserve `failed`/`inconclusive` evidence without causal claims |
| `astra-ship` | **R:** fresh evidence versus commit/publication authority. **I only, never H:** Test → Ship supplies the evidence packet; a clean result is not a problem handoff. Test does not invoke or route into Ship. | Snapshot/base; exact commands and timestamps; exit/failure counts; relevant logs/artifacts; red/green proof; gaps/skips/residue; test-file changes | User alone starts Ship. If unavailable or not selected, retain the packet and working state; Test performs no commit, push, PR, merge, release, or cleanup |

**Accepts Critique handoff: yes.** Test owns the post-critique problem class
`test-evidence-gap`: accepted behavior lacks adequate, trustworthy, or fresh executable evidence.
Critique’s report must preserve every actionable finding and route; the user may select zero or one
immediate capsule. In addition to Critique’s common problem envelope, Test owns this compact,
problem-only destination payload:

| Destination-only field | Required content |
|---|---|
| `problem_class` | Literal `test-evidence-gap` |
| `gap_kind` | Observed absence, stale evidence, wrong seam, weak oracle, missing negative/regression case, missing runner/config, or incomplete final verification |
| `proof_obligation` | The accepted behavior, risk, requirement, or completion claim whose executable support is missing; reference the common-envelope problem/evidence rather than restating it |
| `required_test_mode` | Construction, framework, execution, final verification, or an ordered subset; `unknown` when Critique cannot classify it without prescribing Test’s solution |
| `proof_shape` | The missing form of proof, such as observed red→green regression, framework dry-run, focused/full suite, coverage with a stated denominator, E2E evidence, or a requirements check; never a framework/tool choice or new success criterion |
| `freshness_requirement` | The revision, artifact event, environment change, or time boundary after which evidence is stale |

Destination, artifact, problem statement, finding IDs and evidence, impact, affected scope,
constraints, open decisions, prerequisites, and context gaps come from Critique’s common envelope
and are not duplicated in this destination-only payload. The payload contains no proposed test
design, framework choice, implementation sequence, tool selection, production fix, or
Critique-authored success criteria. Test explores those only after the user starts it. Critique
never reads or invokes Test’s full workflow. A missing profile remains a reconciliation gap; it
does not narrow Critique’s testing-evidence lens or redirect the problem.

### 7.4 Manual/external bridges for deferred general-purpose concerns

| Deferred concern | Honest bridge; no capability is implemented or absorbed |
|---|---|
| Context | Supply contract/version, snapshot, current test artifacts, command history, environment facts, and prior evidence at every invocation/resume |
| Guard | State writable test paths, forbidden production/publication effects, network/live-system limits, cleanup rules, and dependency-install authority before work |
| Delegate | For BDD’s fresh coverage audit, the user manually starts a separate fresh session with only the OpenAPI spec and feature files, then returns its gap report; Test creates no general delegation facility |
| Automate | Repeated/watch/CI execution remains project-native and explicitly configured; Test creates no scheduler, hook, loop, or background worker |
| Incident | Live instability is external; Test may collect an approved reproduction but does not coordinate stabilization or incident authority |
| Deploy | Environment access and rollout are external; Test may consume an endpoint/config supplied by the user but performs no deployment or teardown |

### 7.5 Delivery shape and self-containment

The future public delivery shape is one skill interface with directly selected internal reference
material for construction and framework modes. Exact files, frontmatter, prompts, schemas, and tool
declarations are deferred. No nested public skills, recursive source reads, or universal adapter
runtime is proposed. Framework adapters and evidence rendering stay behind Test’s interface.

The reference convener may temporarily coordinate unchanged originals for evaluation. The final
self-contained candidate must not read or invoke the seven available source bundles. `run` remains
outside both until P resolves. External compilers, runners, browsers, package managers, credentials,
and live endpoints remain declared prerequisites rather than being falsely “absorbed.”

---

## 8. Manual bridge

No Astra runtime exists. Use the installed originals, still installed, with an explicit session
instruction: **write only the approved test/evidence artifacts; do not modify production code,
silently change the accepted contract, install dependencies, access live systems, clean up remote
data, invoke a peer, or publish; stop with the section 2.4 evidence packet.**

### 8.1 Construction and framework invocations

Choose one current source from the artifact and requested policy; do not run every source by
default:

| Need | Exact current invocation | Required manual qualification |
|---|---|---|
| User-confirmed-seam, vertical-slice TDD | `/tdd` | Stop after test artifact and observed red when production change is needed; no refactor in this loop |
| Strict Superpowers TDD | `/superpowers:test-driven-development` | Stop before its delete/production-green/refactor effects; record the required Implement action |
| OpenAPI/Behave acceptance tests | `/bdd` | Supply the accepted OpenAPI file and effect limits; do not fake a missing API or alter spec-derived assertions |
| Java/Groovy Spock tests | `/spock` | Treat the implementation score/refusal as requiring user or separate Critique judgment; Test itself only records testability/attack facts |
| Next.js Vitest/Playwright | `/nextjs-test` | Confirm the project is Next.js 15-compatible and authorize any Vitest/package setup separately |
| Shell/Bats tests | `/shell-scripting:bats-testing-patterns` | Confirm Bats/shell prerequisites; do not copy an unvalidated variable-based recursive cleanup command |

On Codex, the installed equivalents are selected by naming `$tdd`,
`$superpowers:test-driven-development`, or `$superpowers:verification-before-completion`; the other
four source registrations audited here belong to the inventoried Claude host. The slash forms above
are that host’s current user-facing bridge. The exact names, not a guessed `run` wrapper, are the
evidence-bearing choice.

For BDD coverage audit, open a separate fresh session manually and provide only the accepted
OpenAPI spec and generated `.feature` files. Ask for endpoints without scenarios, required fields
without absence cases, constraints without boundary cases, query parameters without absence cases,
defined errors without triggers, and string inputs without security cases, each with source anchors.
Return the report to the BDD session and repair only test artifacts. This preserves fresh-context
intent without introducing Delegate.

### 8.2 Exact source-native execution commands

Run commands from the target repository root, after confirming they are the project’s real scripts
and the user approved their effects. Capture the full output and exit status; do not infer success
from these examples merely existing:

```bash
poetry run behave --dry-run features/api/
./gradlew test jacocoTestReport
./gradlew jacocoTestCoverageVerification
pnpm test --run
pnpm type-check
pnpm e2e
bats tests/*.bats
```

Only run the commands applicable to the selected source and target project. BDD live execution also
needs its configured environment and cleanup authority. Next first-time package installation changes
the manifest/lockfile and uses the network; it requires separate approval before following the
source’s `pnpm add -D …` setup. Spock’s `open` coverage-report command is a GUI convenience, not
proof and not part of this invocation-safe bridge.

### 8.3 Final evidence gate and stop

Invoke `/superpowers:verification-before-completion` with the exact claim and the commands that
prove it. Re-run the full command in the current session, read all output, record exit/failure count,
and render the evidence packet. Do not invoke built-in `run`: its body and host contract are **U**.

If a test fails because production behavior is wrong and the cause/fix is already approved, return
the packet for a user-started Implement invocation. If the cause is unknown, return it for a
user-started Debug invocation. If the accepted behavior itself is unclear, return to the user/Spec.
After fresh complete evidence, stop; the user alone decides whether Critique or Ship starts.

**Bridge limitations.** No existing source enforces the production-mutation split across the full
TDD loop, emits the common evidence packet, or coordinates all four modes. BDD’s missing
`coverage-checklist.md`, Spock’s missing `concurrency.md`, the truncated Bats reference, the Next
example inconsistency, and `run` provenance remain unresolved. The bridge approximates behavior; it
does not prove preservation.

---

## 9. Deferred implementation and validation

Nothing in this section has been run. Phase 0 builds no wrapper, convener, candidate, corpus,
harness, fixture, or benchmark.

### 9.1 Declared advantage and three comparison systems

**Advantage class:** supported critical-gap recall and claim-complete evidence on artifacts that
need coordinated construction, framework, execution, and final-verification behavior. A positive win
is a source-unique, contract-supported test gap or evidence defect found by both combined systems
and missed reproducibly by the preselected source oracle, with no authority escape.

1. **Source oracle:** before outputs are seen, select the strongest applicable original among
   `tdd`, Superpowers TDD, BDD, Spock, Next.js Test, Bats, or Verification Before Completion for
   that artifact/jurisdiction. Each source is its own oracle on its home cases. `run` is ineligible
   while **U**.
2. **Reference convener:** a temporary adapter presents the proposed interface while coordinating
   unchanged originals. BDD’s fresh coverage reviewer remains a separately user-started external
   session. The convener records production changes as peer handoffs rather than performing them.
   It is a scaffold, not a retirement-ready implementation.
3. **Self-contained candidate:** the proposed final adapter internalizes only retained, validated
   behavior and no longer reads or invokes the originals. It preserves the same production,
   judgment, diagnosis, delegation, and publication limits. It cannot include `run` until P resolves.

### 9.2 Fixed corpus

The corpus is versioned and fixed before output generation. It covers:

| Corpus class | Required cases |
|---|---|
| Home jurisdiction | General feature and bug-fix TDD at an agreed seam; OpenAPI REST features/steps with positive, negative, auth, constraint, and spec/server mismatch cases; Java/Spock unit attacks including dependency failure and idempotency; Next.js Zod/RBAC/sync-component/async-page and setup cases; Bash success/error/dependency/dialect/temp-file cases; fresh completion claims for tests, typecheck, build, lint, and requirements |
| Claimed advantage | OpenAPI-backed Java service needing Spock unit, Behave acceptance, and final evidence; Next.js change needing unit plus browser E2E and final evidence; shell change needing a red test, Bats dialect/error coverage, and a full claim gate |
| Expected divergence | `tdd` no-refactor versus Superpowers refactor; public-interface/boundary-mock default versus Spock strict interactions; BDD spec truth versus current server behavior; test failure needing production mutation versus a defective assertion |
| Expected convergence | Simple pure function with an agreed seam and literal oracle where both general TDD sources should produce the same meaningful red test without framework or production-scope invention |
| Prerequisite failure | Missing/incorrect runner, generated client, config, credentials, live endpoint, cleanup authority, Gradle/JaCoCo, pnpm/network/bootstrap authority, browser, Bats/dash/`jq`, missing referenced files, interrupted/partial output, ambiguous contract, dirty snapshot, and unavailable `run` |

### 9.3 Method and measures

Run all three systems on identical accepted behavior, artifact snapshot, effect limits, and
available prerequisites. Use repeated trials (at least three for nondeterministic judgment-bearing
steps). Preselect the source oracle. Where test quality or actionability is judged, de-identify and
randomize output order for a blinded evaluator. Machine evidence—compilation, dry-run, exit status,
failure counts, mutation sensitivity, and path/effect logs—remains raw.

Record:

- critical behavior/defect and test-gap recall;
- supported-claim precision, unsupported-claim rate, and source-unique supported findings;
- independent-oracle quality, observed-red validity, mutation sensitivity, and regression strength;
- runnable test-artifact correctness and framework-convention fidelity;
- routing accuracy across the four modes and four framework adapters;
- command/snapshot/freshness completeness and finding-to-evidence traceability;
- actionability, duplicate/noise load, skips, false passes, and residual external effects;
- production/test-path mutation containment and unintended peer invocations;
- cost, latency, tool/install/network use, and degradation state.

Unsupported pass claims, unauthorized production/publication effects, fabricated live responses,
dropped source-unique behavior, and unintended peer invocations must remain zero.

### 9.4 Gates and failure consequences

| Gate | Passing requirement | Failure consequence |
|---|---|---|
| Source characterization | Each proposed distinction reproduces on the same decision; convergence controls do not invent conflict | Reclassify the behavior; do not expose an unsupported mode/policy switch |
| Home-jurisdiction non-regression | Convener and candidate retain every reproducible critical behavior, source-specific failure path, and authority condition without worse unsupported-claim or false-pass rate than the oracle | Keep affected source installed and narrow/rework its adapter |
| Positive advantage | On at least one preregistered combination class, both combined systems add a supported decision-changing test/evidence gap missed by the oracle, without higher noise or authority escape | Withdraw the claimed quality merger; use explicit source-like modes or retain originals rather than claiming better output |
| Internalization fidelity | Candidate matches the convener’s source-unique findings, divergences/convergence, artifacts, prerequisites, and degradation | A convener win followed by candidate loss blocks internalization and every affected retirement |
| Interface and authority | Correct routing; complete packet; zero production mutation, independent Critique judgment, causal diagnosis, hidden delegation, peer invocation, unauthorized install/live/cleanup effect, or Ship action | Hard fail; redesign seam/effect gates before further evaluation |
| Source-specific retirement | Section 9.5 gate for that source plus all gates above and explicit user approval | Failure blocks only that source’s retirement; no source is retired by neighborhood-level averages |

### 9.5 Source-specific retirement gates

These are later obligations, not readiness claims:

| Source | Additional gate before that source could become retirement-eligible |
|---|---|
| `tdd` | Preserve confirmed-seam gate, public-interface behavior, vertical tracer slices, independent expectations, anti-tautology and boundary-mocking rules, optional context/ADR lookup, and its no-refactor policy. Demonstrate that the user-mediated Implement split preserves the production-green behavior without Test mutating production. Preserve symlink/interface delivery facts or an approved replacement. |
| `superpowers:test-driven-development` | Reproduce expected red, minimal green requirement, relevant-suite green, good-test/mutation gates, explicit human exceptions, and refactor policy. Prove that delete/edit/refactor effects remain in Implement/manual authority and that this decomposition loses no source outcome. Preserve plugin/version/degradation behavior. |
| `bdd` | Preserve explicit HTTP Gherkin, OpenAPI-wide positive/negative/constraint/auth/security coverage, generated clients, async/context/config patterns, real-error propagation, dynamic data, dry-run, live environment and cleanup behavior, and fresh independent coverage audit. Recover or explicitly replace the missing `coverage-checklist.md`; validate any replacement for the agent delivery shape. |
| `spock` | Preserve Spock naming, unit-isolation and Mock/Stub/no-Spy rules, strict interactions, data-driven forms, attack/exception/concurrency/idempotency cases, and JaCoCo evidence. Recover or replace `concurrency.md`; reconcile interaction coupling. Demonstrate that the separate Critique/user quality judgment preserves the mandatory review/refusal outcome without Test absorbing it. |
| `nextjs-test` | Preserve the Next.js 15 unit/E2E decision matrix, Vitest/RTL/Playwright patterns, path conventions, CodeGuard rules, setup/dependency behavior, and self-verification evidence while routing production fixes to Implement. Resolve/characterize the `110` versus “caps at 100” inconsistency and keep project-specific count targets from becoming global. |
| `shell-scripting:bats-testing-patterns` | Preserve Bats assertions, fixtures, stubs, error/dependency/dialect/parallel/CI behavior and namespaced plugin delivery. Recover the truncated advanced section or establish from immutable upstream evidence that no additional behavior existed at this revision; replace unsafe variable-based recursive cleanup with behaviorally equivalent validated test-owned cleanup and prove portability assumptions. |
| `superpowers:verification-before-completion` | Preserve fresh full command execution, complete output/exit/failure reading, exact claim mapping, red/green regression proof, requirements checklist, and distrust of delegated/adjacent evidence. Demonstrate that production reverts and Ship effects stay external without weakening proof. Preserve plugin/version behavior. |
| `run` | First obtain immutable source bytes or an approved host-version pin plus declaration, invocation, authority, dependencies, and failure behavior. Only then characterize a source oracle and write a behavior-specific gate. Until then it stays P/deferred and cannot be called absorbed, preserved, excluded, or retirement-ready. |

Matching a final “pass/fail” label is insufficient if a source-unique test playbook, framework
artifact, failure state, fresh-context property, authority field, or evidence trace disappears.

---

## 10. Provenance and open questions

### 10.1 Inspection and immutable anchors

Inspection date: **2026-08-03**. Every available source bundle file listed below was read in full.
The aggregate bundle hash was calculated from each source root with:

```bash
find . -type f -print0 | sort -z | xargs -0 sha256sum | sha256sum
```

The relative filenames are included in the inner hashes, so a file add/remove/rename or byte change
invalidates the bundle anchor.

**Standalone `tdd` registration and bundle.** `~/.claude/skills/tdd` resolves to
`~/.agents/skills/tdd`; no repository revision was available, so byte hashes are authoritative.

```text
5363bb2775679fe9311fbb67947f95359169c6e7f1fac77c0f25e190bca6cf2f  SKILL.md
ea6f01cf1b8c06a4b0f5b649d74b1b8ce8685e72af1b38d70d877693e092af0b  agents/openai.yaml
3ceb807fdf4a47d6a93d4d9a891e5ba6d362a6247bd08adc451feebfc17361ef  mocking.md
859f9e592c188fda4fc7277dd180e4ce9c7a2e13f6efe1f6f29eccc9d28c106a  tests.md
8a73e40fe4d4c2265a0b4fa1434d3b0c041609cf8d1d0de7512d6f5a58abb987  bundle
```

**`monster-prompt` standalone sources.** The three registered symlinks resolve into repository
revision `6abccfa5f83a82f2bff309228b956323a11e4d2a`; the three source directories were clean at
inspection.

```text
# bdd
7b181df709954ece6450097d31afca3be20a1c8ee4aa85e84d9ec80efc1ed6e2  SKILL.md
858f74f41729de1f60146dc29005c04249f6780bcd9c9fd250d68262a0e810c8  prompts/generate-features.md
e618a34258aa5923f03d6d0d9eb758821168b69ae4d68aa709d9682b8b9460fc  prompts/generate-steps.md
d861e0a62c2253c6166db727e3c6b119d8f2bf4fb73b92a6c5d10d5fd5a1ad1e  prompts/update-features.md
b1570de0161dd37b6b01005b63eafaeaae3240d7d63abf501d224f66ba244dfb  references/feature-writing.md
a09ccb6578587aa1b77572ba18a9af43a7968bf75bb9692b50c3ff220590dd87  references/step-implementation.md
f7fcf217ab52c41f24bc18d0d663ed64e2bac5ddca63c08c0ef5a57070872ea7  bundle

# spock
2e4519821e9d2cb78a9a3d32bdd5991c471149ad27521b608889027e7b0b96c3  SKILL.md
c2665f93b6805c394a3d2463f090f5206524805a31da532b4e7131ea3032e629  examples.md
30d5c62778f6270f194a8c0fb49912d6b78e99f70094c813e9119f1e4b7f22c7  reference.md
703821065d907cdd13cfbc35ec06c5fe361954f5d9a8c0b5c2851d957a85fa23  bundle

# nextjs-test
f664eaa7f19879c3c201bc3cd954cf8e423fce38b1013195e6038d5c4518ff87  SKILL.md
bf7499103114492797ee091ea8286ed6d6bd22ffacf4f1b350e9d7af5591a7a7  references/patterns.md
313d35199d0b647be477856edcc5191a9feaf6ccc8e148f284404a7fbcce34c4  bundle
```

The repository marketplace manifest is
`8992866835bd21e2e213de359b51e29885f6217236a425f020a1e1acd7921780`; its complete registration
declares only the `loop-goal` plugin. It does not register BDD, Spock, or Next.js Test. Their live
delivery is therefore the three top-level personal-skill symlinks plus the frontmatter and bundle
files recorded above, not an undeclared plugin component.

**Superpowers 6.2.0.** Installed registration records immutable commit
`eafe962b18f6c5dc70fb7c8cc7e83e61f4cdde06`; Claude plugin manifest SHA-256 is
`5e9f9b99d9d009ccbcdbce82644a5bf902691c39f152b79540b4542533fe53c3`.
The Codex cache bodies match the Claude cache byte-for-byte; its plugin manifest is
`b271065c5e906e73757b7f9c26f7c57bb662ee47a31ed479dc32fb253729a25c`.

The complete Claude manifest fields are `name`, `description`, `version`,
`author{name,email}`, `homepage`, `repository`, `license`, and `keywords`. The complete Codex
manifest adds `author.url`, `hooks`, `skills`, and the `interface` object (display/developer names,
descriptions, category, colors, icons/logo, default prompts, website/privacy/terms links, and
plugin-wide capabilities). Those interface fields describe plugin delivery; they do not silently
grant Test mutation authority.

```text
# test-driven-development
bf1b8216e523851a411e91d429a7c1c2a173e79d88957bc78e348218d50edd54  SKILL.md
51471c853306ff92ca8bb41dcaea05f31c0e46b03651f8f3c99754b7172f4ae1  writing-good-tests.md
b23b6e44500c5a101529fff13df1c60f576022c9a2fcca7a8722ad89f568bffa  bundle

# verification-before-completion
2befe7fc55bcadaa3d97dd9e8efeb633d2561c0ebe74c5a8b17c4d9e7e4520b3  SKILL.md
2e5c5f8225aa6e3e8ab5ce8ebff5d6f3e365c14e94dda01d6394a5b53979f960  bundle
```

Codex interface metadata hashes are
`d1fd223b137ce6eca628d521031213a2dc002a97865f00e2f6fce03529b9ca05`
for TDD and `0eaad1a982ab8c95d8b938f1567f207dbc6fd9d172707b1e268e0cc8ab999705`
for Verification.

**Shell Scripting 1.2.3.** Installed registration records immutable commit
`b6af3711058190e4b5c5274b9758498fe626ec5a`; Claude plugin manifest SHA-256 is
`24539c0d652508ffd5cb80d5fe85f5d3553ec09fb45a96945c1a8ac7207d5131`, and its
Codex plugin manifest is `a0b61457122578d46b6bb01c863642b3cc9b12cba751f4801a8d4a8e57eaa435`.

The complete Claude manifest fields are `name`, `version`, `description`, `author{name,url}`, and
`license`. The complete Codex manifest adds `skills` and `interface{displayName,shortDescription,
category}`. The installed-registration entries for both plugins record `scope`, `installPath`,
`version`, `installedAt`, `lastUpdated`, and `gitCommitSha`; relevant enablement values are `true`.

The inspected Claude registration-state files were also content-anchored:
`installed_plugins.json` is
`d6963627a077c6b61aee8b277e99b63f4f52e075b6275ce2beb2e4890eaa7095`, and
`settings.json` is `0e553d6e5eb95b9fc5b63b5f65e15d22bbfef538558e3bb66eea6c6ce27eed1`.
Only the relevant Superpowers/Shell Scripting entries and enablement values were used; unrelated
settings are not evidence for this design.

```text
d7992dbf589789f1ae446161d86c1cab026b9dfc4acfed5491d552be97338e62  SKILL.md
b3a82965886d700debae915949a6eccd7768568d97c0d996d7354abb43fee4b5  references/details.md
d68e484985d31d63e9a6888e572b72a2205e6c25cdf63fc63664d6ba6df5a9a8  bundle
```

**Unavailable built-in.** `README.md` “Four source categories” and the collision-map Testing row,
`docs/phase-0.md` section 5, `docs/phase-0-ledgers.md` row `cm-testing-08`, and roadmap section 5.12
all record `run` as a live harness built-in with no path/manifest and unresolved immutable
provenance. Those repository records establish the **U/P** state, not its behavior.

### 10.2 Provenance caveats and observed source defects

- Symlink registration proves current reachability, while the byte or repository hashes anchor the
  body inspected. A hash mismatch invalidates behavior anchors until reinspection.
- Plugin-level capabilities and enablement are registration facts, not per-skill mutation authority.
- BDD’s `coverage-checklist.md` and Spock’s `concurrency.md` are referenced but absent from the
  inspected bundles.
- Bats `references/details.md` ends at line 402 with a lone `#`; no unseen advanced-pattern behavior
  is inferred.
- Next’s `calculateProgress` example says “caps at 100” but asserts `110`; the intended behavior is
  not inferred from that contradiction.
- The current `run` source has no reproducible bytes or declaration. No hash, line anchor, source
  characterization, preservation statement, or exclusion rationale is fabricated.
- Phase 0 inspected prose and registration only. It did not execute source workflows, install
  dependencies, access external systems, write tests, or run the three-system evaluation.

### 10.3 Provisional decisions

- One Test peer with four internal modes is the smallest coherent hypothesis; it is not a validated
  router or universal testing runtime.
- Test owns test/evidence artifacts and fresh evidence. Implement owns production mutation; Debug
  owns unknown-cause diagnosis; Critique owns independent judgment; Ship owns publication.
- General TDD policy conflicts remain selectable rather than silently resolved.
- Framework-specific behavior remains behind actual internal adapters and does not become generic
  advice.
- BDD’s fresh coverage context is a manual/external bridge; deferred Delegate is neither implemented
  nor absorbed.
- `run` stays deferred and absent from all absorption, preservation, exclusion, and retirement
  claims.
- Originals remain installed. No runtime validation or retirement approval has occurred.

### 10.4 Open questions and consequences

1. **Test-infrastructure authority.** May Test edit dependency manifests, lockfiles, and CI test
   steps after explicit user approval, or should it only propose them for Implement?
   **Consequence:** until reconciled, bootstrap mode must ask before each such file class and cannot
   advertise unattended setup.
2. **Default TDD policy.** Should refactor remain outside the Test loop (`tdd`) or be a named
   post-green construction step (Superpowers)? **Consequence:** auto mode cannot choose between them;
   the user selects a policy and production refactor still belongs to Implement.
3. **Spock judgment boundary.** Does the source’s quality-score/refusal become an accepted Critique
   profile, a user checklist, or a reason to retain Spock independently? **Consequence:** Spock cannot
   pass internalization or retirement while that mandatory behavior has no accepted owner.
4. **BDD fresh audit.** Can an internal non-agent coverage check match the original fresh-context
   audit, or is a retained manual reviewer necessary? **Consequence:** no self-contained retirement
   claim for BDD until the comparison answers this without absorbing Delegate.
5. **Incomplete source references.** Can the missing BDD and Spock files and truncated Bats content
   be recovered at their inspected revisions? **Consequence:** affected playbooks stay partial and
   their sources stay installed.
6. **Live-test effect policy.** Which environments permit test-data creation and cleanup, and what
   residue blocks a supported result? **Consequence:** live BDD execution remains explicitly
   authorized per invocation and cannot default to production-like environments.
7. **Evidence freshness and storage.** How long may a packet remain current, and which outputs may be
   retained or must be redacted? **Consequence:** the phase-0 design records snapshot/timestamps but
   defers persistence, telemetry, and exact schema.
8. **Built-in `run` provenance.** What host-version pin or immutable distribution artifact can expose
   its declaration and bytes? **Consequence:** `cm-testing-08` remains P/deferred and ineligible for
   every comparison until resolved.
9. **Roster reconciliation.** The sibling Test-facing contracts are provisional until all seven
   peers’ designs exist and the coordinator reconciles direction, payload, and trigger ownership.
   **Consequence:** no absent peer contract is treated as implemented, and no peer is silently
   invoked in the interim.

---

## 11. Six-skill verification amendment

Test is the independent evidence authority after Implement, not an implementation repair stage.
This section supersedes the historical seven-peer relation table where it conflicts with the
cumulative consultant graph. Sections 1–10 remain source evidence and preserve Test's construction,
framework, execution, and final-verification playbooks for later source allocation.

### 11.1 Primary-path intake and authority

For a delivered change, Test pins:

- the Finding Set when Critique authority is present;
- the Approved Change Specification revision/hash and every applicable requirement and criterion;
- the Approved Delivery Roadmap revision/hash;
- the Execution Ledger, atomic commit identities, and exact delivered revision; and
- an Understanding Report when its current-state claims were used downstream.

Stale or mismatched identities stop verification. Test may select and run evidence methods within
its approved test/evidence scope, but it cannot weaken a criterion, reinterpret a finding, expand
the delivered functionality, or repair production code. Implement's focused checks are inputs,
not proof that Test may simply repeat the completion claim.

On the normal path, durable tests, fixtures, configuration, and test documentation required by the
Specification are Implement Roadmap tasks and appear in atomic commits before Test begins. If Test
discovers that a new durable repository artifact is required, it records the gap rather than
silently adding publishable scope. Any separately authorized Test-created artifact remains
uncommitted evidence until a new approved change cycle incorporates it.

### 11.2 Cumulative consultant gate

One persistent consultant for each present upstream authority participates before Test issues its
packet:

| Consultant | Judgment preserved |
|---|---|
| Critique | Whether Finding IDs, causal claims, and proof obligations are represented honestly |
| Spec | Whether the tested claims and expected outcomes match the approved requirements, criteria, constraints, and branch |
| Implement | Whether the tested revision, delivered scope, atomic commits, and Execution Ledger are the actual implementation result |
| Understand Code, conditional | Whether relied-on current-state claims remain correctly interpreted at the tested revision |

Consultants return `pass`, `drift`, or `authority_gap`; they do not choose Test methodology or
dictate the overall evidence state. Test independently decides whether the evidence supports the
claim. An unavailable required consultant fails closed unless the user records reduced assurance.

Test exposes its own narrow read-only `consult` mode to Ship. It validates packet identity,
freshness, adequacy, tested revision, gaps, skips, residue, and the exact claims the publication
would make. It cannot authorize a push, PR, merge, release, or deployment.

### 11.3 Test Evidence Packet and traceability

The packet records the pinned artifact chain, mode and framework jurisdiction, exact commands and
working directories, environment facts, start/end timestamps, exit states, failure counts,
relevant logs and artifacts, red/green evidence, mutation sensitivity where applicable, coverage
denominator where actually measured, cleanup and residue, gaps and skips, consultant
determinations, and an overall `supported`, `failed`, `blocked`, or `inconclusive` state.

Every claim maps through:

```text
finding -> requirement -> acceptance criterion -> roadmap task -> atomic commit
        -> test evidence
```

A genuine `failed`, or an `inconclusive` result that blocks an approved criterion, cannot be
repaired inside Test or waived by a consultant. It creates a new Critique finding and therefore a
new immutable change cycle if the user continues. Earlier artifacts and the failed packet remain
unchanged and are referenced by the new cycle.

### 11.4 Deferred reconciliation

The complete Test source inventory, browser/QA adjacency, durable-test effect boundary, and
six-peer relation table still require later absorption and coordinator reconciliation. This
amendment changes no ledger, source installation, runtime skill, harness, comparison system, or
retirement state. Test is policy-grounded but not yet fully fleshed out from every related source.

This document is phase-0 prose only. It runs no behavioral validation and grants no retirement
authority.

## 12. 92-component source-expansion amendment

The user-approved census, source hashes, cross-stack equivalence evidence, and retirement gates
live in `docs/six-skill-source-absorption.md`. This design adopts three new primary identifiers:
`webapp-testing`, `benchmark`, and `benchmark-models`.

They extend Test's evidence methods without changing its interface or independent authority.
`webapp-testing` supplies browser reconnaissance, Playwright execution, log capture, screenshots,
and cleanup against pinned behavior. `benchmark` supplies named baselines, repeated performance
measurements, budgets, and trends. `benchmark-models` supplies same-prompt cross-model runs with
explicit model, cost, token, latency, and optional judge records. Each method preserves its exact
prerequisites, raw output, environment identity, degradation, and source-specific retirement gate
inside the Test Evidence Packet.

QA, iOS, API, database, MCP, Java, shell, and skill-artifact profiles also create secondary Test
obligations. Their approved criteria and exact delivered revision select the evidence method;
Test does not infer an unapproved contract from a source's defaults. Exploratory browser or device
work without pinned requirements remains Critique. Durable fixtures, scripts, instrumentation, or
product repairs required by a failed run return through a new approved change cycle rather than
being written by Test.

This amendment changes no coordinator ledger row and performs no browser, benchmark, model,
device, or test run. It creates no runtime profile, corpus, harness, repository mutation,
publication, or source-retirement claim.
