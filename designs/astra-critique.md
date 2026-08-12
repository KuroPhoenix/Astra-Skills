# Astra Critique — phase-0 design

**Normalized:** 2026-07-31 · **Original design:** 2026-07-29 (`f264c20`, reviewed at `ff889a4`)

**Six-skill reconciliation:** 2026-08-11 · surviving public home for review, diagnosis, and
Critique-authority consultation; `astra-debug` is superseded historical evidence

> **Authority.** `docs/design-requirements.md` governs this document; `docs/phase-0.md` owns
> phase scope and the global ledgers. This is one per-skill design, not a universal condensation
> policy and not an implemented skill.
>
> **Historical appendices.** Appendix A (panel protocol and schemas), Appendix B (packaging
> proposals), and Appendix C (cost model and a later measurement sketch) predate the phase-0 scope.
> `docs/phase-0.md` section 8 defers packaging, schemas, routers, tiers, telemetry, and
> conformance harnesses. They are retained as research evidence because the condensation and
> panel reasoning they support is this design's substance. Core §9 owns this design's normative
> validation obligations. Nothing in the appendices is settled, and no fixture, harness, or
> benchmark is authorized here.
>
> **README anchors.** The `README.md` hash recorded in §10 predates commit `a037f20`. Cite README
> headings, never line numbers.
>
> **Conformance.** Sections 1–10 map one-to-one and in order onto
> `docs/design-requirements.md` sections 7.1–7.10. Section 11 applies the six-skill contract in
> requirements section 7.11 and has normative precedence over conflicting pre-reconciliation
> wording. Self-reviewed against that document's section 11 checklist; the appendices carry no
> phase-0 requirements.

> 留其精華，去之糟粕 — but a voice is not 糟粕 merely because another voice already spoke.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-critique` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhood | Adversarial critique (16 occurrences) plus one Design & visual cross-neighborhood source |
| Six-skill role | Surviving public home for review findings, causal findings, and read-only Critique consultation; Debug source reassignment remains deferred |

**User job.** *When I want evidence-backed findings about what is wrong or why an observed
failure occurs, before any solution is selected or target behavior is changed.*

**Personal value — explicit.** The user's standing global instructions make adversarial critique
a permanent requirement, not a preference: `claude/rules/persona.md` mandates *"Truth over
comfort… Correct the user when they're wrong — challenge flawed premises before implementing
solutions. This counteracts sycophancy,"* and requires that *"Multiple valid interpretations
exist → present them with tradeoffs, never pick silently."* A skill whose output is several
attributable positions plus an explicit user choice is the direct mechanical expression of that
instruction.

Usage is supporting evidence only: the neighborhood records 50 July invocations, and `/diss`
alone is 31 agent-fired — the highest autonomous count of any source on the machine.

`proposed` is the only phase-0 status. Priority `now` reflects that value plus the fact that this
neighborhood is the only one where the user already invokes a source daily.

---

## 2. Interface and scope

**Requests that should trigger it.** "Review this before I ship it." "Attack this plan." "Is this
the right architecture or design choice?" "Is this the right approach, or am I fooling myself?"
"What breaks if I do this?" "Why is this failing?" "Find the root cause." Reviewing a code diff,
plan, specification, architecture decision, infra change, prompt, CLAUDE.md, or running visual
interface; or diagnosing an observed deterministic, intermittent, performance, resource, or
environment-difference failure.

**Nearby requests that should not.**

| Request | Belongs to |
|---|---|
| "Do the tests pass?" | Testing |
| "Find the vulnerabilities" | `cso`'s jurisdiction and attacker priors |
| "Explain how this works" | Codebase comprehension |
| "Make this change" | Any implementation skill — this skill never edits |
| "Add instrumentation or repair the failure" | `astra-spec` then `astra-implement`; Critique identifies the evidence obligation but never mutates the target |
| "Interview me until my plan is sharp" | Sharpened but distinct — see §5.7 |

**Accepted context, conceptually.** One artifact with an identifiable set of decisions in it, plus
whatever evidence the artifact's own domain supplies (a diff and its repository, a plan and its
stated intent, an architecture decision and its constraints, a prompt and the published practices
it should meet, or a running interface and its reachable states and screenshots).

**User-visible result.** A versioned Finding Set. In review mode, its report makes every
substantive judgment attributable to a named reviewer, checks factual disputes against evidence,
and surfaces every normative disagreement as an explicit choice rather than silently resolving
it. In diagnose mode, it records the observed failure, competing causal hypotheses, proof
obligations, and only those causal claims established by evidence. The Finding Set retains a
traceable route candidate for every independently actionable problem class. After it renders,
the result adds either one user-selected, destination-specific handoff capsule or an explicit
statement that no immediate handoff was selected. Unselected candidates remain in the result.

The critique report is the primary result. The handoff is a smaller routing capsule derived from
that report: it restates the problem and evidence for the owning peer but does not attempt to
solve it.

**Non-goals.** Making the change or adding target-repository instrumentation. Deciding tradeoffs on the user's behalf. Producing a single
merged verdict that hides disagreement. Prioritizing independent problems on the user's behalf.
Replacing test execution or security auditing. Invoking, loading, or executing the recommended
destination skill. Defining the downstream solution, implementation plan, tool choice, or success
criteria.

**Decisions that remain with the user.** Every normative tradeoff. Panel composition, when
overridden. Whether to act on any finding. Whether an unresolved factual dispute blocks. How to
classify a problem when surviving reviewers nominate incompatible owners. Which independent route,
if any, should become the immediate handoff.

The interface is deliberately smaller than the behavior: one invocation and one artifact, against
a panel whose composition, protocol, and conflict handling stay behind it. The output remains one
report and at most one typed handoff; the handoff starts no second workflow.

---

## 3. Source evidence

The original 18 sources were inspected 2026-07-30; `design-review` was inspected 2026-07-31.
Every row is **Observed** unless marked otherwise. gstack sources are reached at
`~/.claude/skills/<name>/SKILL.md`, which is a **symlink** whose target is
`~/.claude/skills/gstack/<name>/SKILL.md`; the hash is of the target bytes.

### 3.1 Inspection record

| Identifier | Component | Location | Invocation | Avail. | Declaration (authority fields) | sha256 |
|---|---|---|---|---|---|---|
| `grilling` | skill | `skills/grilling/` | `/grilling`, model-invocable | live | `name`, `description` only — **no authority fields** | `44331dda…` |
| `grill-me` | skill | `skills/grill-me/` | `/grill-me` | live | **`disable-model-invocation: true`** | `6189dfce…` |
| `grill-with-docs` | skill | `skills/grill-with-docs/` | `/grill-with-docs` | live | **`disable-model-invocation: true`** | `610d0910…` |
| `/diss` | command | `commands/diss.md` | `/diss <pr\|empty>` | live | `argument-hint`; `allowed-tools` incl. `Agent`, `Task*`, 2× mysql MCP | `b4e029d6…` |
| `/diss-api` | command | `commands/diss-api.md` | `/diss-api <pr\|spec>` | live | `argument-hint`; `allowed-tools` | `f2b765a4…` |
| `diss-infra` | skill | `skills/diss-infra/` | `Skill(diss-infra)` | live | **`effort: xhigh`** | `94b3172c…` |
| `diss-claudemd` | skill | `skills/diss-claudemd/` | `Skill(diss-claudemd)` | live | **`effort: xhigh`**; **no `allowed-tools` despite MCP use** | `4778d24b…` |
| `/elon` | command | `commands/elon.md` | `/elon <problem>` | live | `argument-hint`; `allowed-tools` | `f1528542…` |
| `/trim` | command | `commands/trim.md` | `/trim <file>` | live | `argument-hint`; `allowed-tools` incl. 2× context-mode MCP | `0ac5d05a…` |
| `office-hours` | skill | `skills/office-hours/` | `/office-hours` | live | `allowed-tools`, `triggers`; v2.0.0 | `b5a0b9d7…` |
| `plan-ceo-review` | skill | `skills/plan-ceo-review/` | `/plan-ceo-review` | live | `allowed-tools`, `triggers` | `c18016a3…` |
| `plan-eng-review` | skill | `skills/plan-eng-review/` | `/plan-eng-review` | live | `allowed-tools`, `triggers` | `41c92a82…` |
| `plan-design-review` | skill | `skills/plan-design-review/` | `/plan-design-review` | live | `allowed-tools`, `triggers`; v2.0.0 | `0f756585…` |
| `plan-devex-review` | skill | `skills/plan-devex-review/` | `/plan-devex-review` | live | `allowed-tools`, `triggers`; v2.0.0 | `4d6cc577…` |
| `devex-review` | skill | `skills/devex-review/` | `/devex-review` | live | `allowed-tools`, `triggers` | `aa162970…` |
| `autoplan` | skill | `skills/autoplan/` | `/autoplan` | live | `allowed-tools`, `triggers`; `AUTO-GENERATED from SKILL.md.tmpl` | `73e2bf3e…` |
| `design-review` | skill | `skills/design-review/` | `/design-review` | live | `allowed-tools`, `triggers`; v2.0.0 | `a7fb587d…` |

**Secondary-role sources — inspected as evidence, primary home not claimed.**
`docs/design-requirements.md` section 7.3 authorizes exactly this inspection.

| Identifier | Component | Location | Invocation | Avail. | Declaration | sha256 |
|---|---|---|---|---|---|---|
| `review` | skill | `skills/review/` | `/review` | live | `allowed-tools`, `triggers` | `92ee16af…` |
| `cso` | skill | `skills/cso/` | `/cso [flags]` | live | `allowed-tools`, `triggers`; v2.0.0 | `4d5da636…` |

### 3.2 Disposition and contribution

Contribution categories are from `docs/design-requirements.md` section 5.

| Source | Contribution | Primary home | Secondary role |
|---|---|---|---|
| `grilling` | **Protocol** (one question at a time, decision-tree traversal, dependency-first) · **Machinery** (recommend an answer per question; look facts up rather than asking) | `astra-critique` | — |
| `grill-me` | **Machinery** (7-line delegating stub) · authority field | `astra-critique` | — |
| `grill-with-docs` | **Machinery** (7-line stub) · **Separate** (its `/domain-modeling` half is a documentation job) | `astra-critique` | Docs & knowledge — `domain-modeling` |
| `/diss` | **Perspective** (adversarial, production-consequence, evidence-gated) · **Playbook** (code map, risk classification, evidence-only verifier) · **Jurisdiction** (code diffs) · **Prerequisite** (mysql MCP, with CLI fallback) · **Machinery** (subagent dispatch, task tracking) | `astra-critique` | — |
| `/diss-api` | **Jurisdiction** (OpenAPI specs) · **Playbook** (`design-api` compliance audit) · register variant | `astra-critique` | `design-api` as retained reference |
| `diss-infra` | **Jurisdiction** (Terraform / CloudFormation) · **Playbook** (dependency tracing, attack-surface and cost analysis) · authority (`effort: xhigh`) | `astra-critique` | — |
| `diss-claudemd` | **Perspective** (prompt-engineering specialist — *shared with `/trim`*, not with `/diss`) · **Playbook** (published-practice audit) · **Jurisdiction** (CLAUDE.md) · **Prerequisite** (context-mode MCP, undeclared, no fallback) | `astra-critique` | — |
| `/elon` | **Perspective** (reduce to irreducible components, rebuild without inherited assumptions) | `astra-critique` | — |
| `/trim` | **Perspective** (provisional — reduction prior) · **Playbook** (published-practice audit) · **Jurisdiction** (prompts and `SKILL.md`) · **Prerequisite** (context-mode MCP) · authority (`Edit`/`Write`, `AskUserQuestion`) | `astra-critique` | Plan & spec: prompt or skill remediation |
| `office-hours` | **Perspective** (is the problem even understood yet) · authority (**hard gate: no implementation**) · **Prerequisite** (gbrain context, optional) | `astra-critique` | Ops & routine |
| `plan-ceo-review` | **Perspective** (scope up, completeness is cheap) | `astra-critique` | Plan & spec: plan revision |
| `plan-eng-review` | **Perspective** (blast radius, reversibility, refactor not rewrite, production ownership) | `astra-critique` | Plan & spec: plan revision |
| `plan-design-review` | **Perspective** (what the user sees first, second, third) · **Playbook** (design review) | `astra-critique` | Plan & spec: plan revision |
| `plan-devex-review` | **Perspective** (developer advocate, TTHW) · **Jurisdiction** (plan document) | `astra-critique` | Plan & spec: plan revision |
| `devex-review` | **Jurisdiction** (running artifact) · **Playbook** (live execution, error-message screenshots, CLI help evaluation) — *same perspective as `plan-devex-review`* | `astra-critique` | — |
| `autoplan` | **Protocol** (fresh specialist contexts, explicit blind filing, staged consensus and auto-decisions) · **Machinery** (dual-model dispatch, degradation tags, decision audit) · **Jurisdiction** (plans) | `astra-critique` | Plan & spec: plan revision |
| `design-review` | **Jurisdiction** (running visual interface) · **Playbook** (first impression, design-system extraction, page and interaction audit, screenshots, evidence-backed report) · **Separate** (test bootstrap, source fixes, atomic commits, and re-verification) | `astra-critique` | `astra-interface`: fix and verify; Testing (future design): bootstrap and regression |
| `review` | **Perspective** (structure-first, recall-first) — secondary evidence only | **Code review** (unclaimed by this design) | `astra-critique`: the contrastive counterpart to `/diss` (§5.1) |
| `cso` | **Perspective** (attacker priors) · **Jurisdiction** (dependencies, CI, git history) · parameterized evidence gate — secondary evidence only | **Language / stack reference** (unclaimed) | `astra-critique`: third policy on the evidence-threshold axis (§5.1) |

Every occurrence has exactly one primary disposition. `office-hours` is a known repeated README
occurrence; its primary home is claimed here and its Ops & routine appearance is the secondary
role. `design-review` is a cross-neighborhood primary source whose audit and report belong here;
its mutation and testing phases remain explicit secondary roles. `review` and `cso` keep their
primary homes elsewhere — inspecting them did not move ownership.

### 3.3 Proposed ledger changes

The phase-0 coordinator mirrors the following in `docs/phase-0-ledgers.md` under the protocol in
`docs/phase-0.md` section 5. This design records the source reasoning; the ledger owns the
authoritative state:

- 16 Adversarial-critique occurrences → `primary_home: astra-critique`,
  `claim_status: claimed` until the roster-wide reconciliation.
- `design-review` (Design & visual occurrence) → `primary_home: astra-critique`; record
  `astra-interface` for fix-and-verify delivery and the future Testing design for bootstrap and
  regression behavior. Critique does not inherit its mutation authority.
- `office-hours` (Ops & routine occurrence) → `duplicate occurrence`, secondary role recorded.
- `grill-with-docs` → secondary role on `domain-modeling` (Docs & knowledge).
- `/trim`, the four `plan-*-review` sources, and `autoplan` → keep their review behavior here and
  record their post-review mutation behavior as a Plan & spec secondary role.
- `review` (Code review occurrence) → unchanged primary; add `astra-critique` to
  `secondary_roles`.
- `cso` (reference ledger, section 6) → `consuming_designs: [astra-critique]`; disposition
  (`keep`/`defer`/`exclude`) stays with the global ledger.
- `design-api` (reference ledger) → `consuming_designs: [astra-critique]` via `/diss-api`.

---

## 4. Collision analysis

**Why the sources appeared duplicative.** Seven of the large gstack sources are
chassis-then-persona in that order, and the chassis dominates:

| Skill | Lines | Identical to `plan-ceo-review` | Persona begins |
|---|---:|---:|---:|
| `plan-ceo-review` | 1476 | — | ~866 |
| `plan-design-review` | 1514 | 995 | ~843 |
| `plan-devex-review` | 1460 | 991 | ~849 |
| `review` | 1852 | 979 | ~844 |
| `office-hours` | 1697 | 959 | ~874 |
| `plan-eng-review` | 1050 | 915 | ~805 |
| `cso` | 1285 | 841 | ~791 |

The `## Voice` block is byte-identical across all seven, each reciting the same house style before
declaring a different character underneath it. Descriptions therefore collide while bodies
diverge — which is precisely why `docs/design-requirements.md` section 4.1 forbids merging on
descriptions alone.

`design-review` did not enter through a duplicate Critique row. It was inspected because the user
placed visual review in Critique, and its single public command combines three jobs: audit/report,
fix/verify, and test bootstrap. Section 5.6 assigns only the first job here and records the other
two as explicit secondary roles.

**`autoplan` already implements a partial convener.** It reads the four full plan-review skills
from disk (`:907-911`), dispatches fresh reviewers explicitly told they have seen no prior review
(`:1181-1189`, `:1304-1315`, `:1380-1391`, `:1506-1517`), runs Claude and Codex voices when
available (`:1155-1158`), tags degraded modes (`:1191-1196`), and records an incremental decision
audit (`:1567-1580`). It is therefore stronger than a description-level baseline of "sequential
specialist reviews." Its limits are equally material: it covers plans only, auto-decides most
intermediate choices (`:907-924`), and depends on the original files remaining installed.

The source also carries `<!-- AUTO-GENERATED from SKILL.md.tmpl -->`; templating reduces upstream
drift, but composition by reference still breaks when those source files are removed. Existing
composition proves that a small interface can hide specialist behavior. It does not prove that
rewriting those specialists into one self-contained implementation preserves or improves them.

**What is actually shared.** The chassis (preamble tiers, `AskUserQuestion` protocol, a shared
question registry), the Voice block, and the adversarial framing. All of it is machinery or
protocol; none of it is a decision policy.

**Which entries are aliases or shallow delegation.** `grill-me` and `grill-with-docs` are 7 lines
each and contain one instruction apiece — `Run a /grilling session`, the second adding
`using the /domain-modeling skill`. Neither carries a prior. Both nonetheless declare
`disable-model-invocation: true`, so they are behaviour-bearing despite being stubs.

**Which apparent duplicates are different jobs.**

- `office-hours` versus `/elon`: one refuses to move past the problem statement, the other
  rebuilds the solution from atomic truths. Adjacent, not equivalent.
- `devex-review` versus `plan-devex-review`: one perspective over two jurisdictions (§5.5).
- `autoplan` versus the four reviews it sequences: an existing plan-jurisdiction convener and
  protocol, not a fifth voice and not a baseline for non-plan artifacts.

**Where source instructions conflict.** Two genuine conflicts, both established by reading
bodies:

1. `/diss` versus `review` on whether an unproven structural suspicion may be filed at all
   (§5.1). This is the sharpest conflict in the neighborhood and it crosses into the Code review
   row.
2. `diss-claudemd` versus its own name (§5.4). It shares `/trim`'s role and playbook, not
   `/diss`'s voice, so the four `diss*` entries are not one persona over four subjects.

**Why the proposal is one coherent module.** Every retained source answers the same user
question — *what is wrong with this, why does it matter, and where do qualified reviewers
disagree* — over an artifact the user already has, and returns judgment rather than changes. The
variation between them is in priors, evidence method, and standing, which is variation *inside*
one job. The sources that turned out to answer a different question are recorded as `Separate`
rather than absorbed.

**Expected positive advantage over the source oracle.** On artifacts whose important decisions
cross jurisdictions, one invocation should surface supported, decision-changing conflicts that
the strongest applicable single source misses, while preserving each source's home-jurisdiction
quality. Broader routing and self-containment are separate maintenance advantages; they do not
count as evidence that the critique itself is better. Section 9 defines the later test.

---

## 5. Preserved distinctions

### 5.1 Resolved: the `/diss` voice, code-structure judgment, and test-evidence judgment

`docs/design-requirements.md` section 9 requires this normalization to resolve the ambiguity
explicitly. Resolution, in three parts:

**(a) The `/diss` voice is one perspective, not two.** Linus and Ramsay occur in exactly one
construction in the entire source set — a conjoined register inside a single role line.
`diss.md:7`: *"You are a venomous, cynical code reviewer. Channel Linus Torvalds + Gordon
Ramsay."* The only other occurrence, `diss-infra/SKILL.md:17`, fuses them the same way. **No
source artifact has them as separate seats.** Under section 6, a difference of register alone is a
persona field, not a persona.

**(b) Test-evidence judgment inside `/diss` is a playbook and a filter, not a rival prior.**
`/diss` holds one adversarial policy plus two mechanical rules:

- `diss.md:339` — coverage below the 85% threshold emits exactly one High finding, computed from
  JaCoCo XML.
- `diss.md:406` — *"Any finding without concrete evidence (file:line + code trace or test output)
  is discarded. No exceptions."*

A threshold and a filter compute; they hold no priors and cannot disagree with anything.

**(c) Consequence — the Linus-versus-Ramsay fixture is withdrawn.** The original claim that *"on
working code shipped with stubbed tests Linus passes it and Ramsay refuses it"* has no source
basis, so the mandatory contrastive fixture built on it (Appendix C) is void. Recorded rather
than deleted, because it was a load-bearing claim of the reviewed design.

**Where the real distinction lives: `/diss` versus `review`.**

| | `/diss` | `review` |
|---|---|---|
| Stated job | adversarial review of a diff bound for production | *"structural issues that tests don't catch"* — code-structure judgment defined by **excluding** test evidence |
| Unproven suspicion | **discarded** — `:406`, "No exceptions" | **filed** — that is its jurisdiction |
| Prior on completeness | precision-first | recall-first — `review:669`, *"AI makes completeness cheap, so the complete thing is the goal. Recommend full coverage (tests, edge cases, error paths)"* |
| Missing test | mechanical coverage finding (`:339`) | proposes one — `review:1381-1385`, findings may carry a `test_stub` |

On working code shipped with stubbed tests these file **incompatible dispositions on the same
decision and target**: `/diss` discards the structural suspicion for want of evidence and emits
only a threshold finding; `review` files the structural issue *because* tests do not catch it,
and attaches a proposed test. Two decision policies.

So the correct first contrastive fixture is **`/diss` versus `review` on working code with
stubbed tests**, replacing Linus versus Ramsay. `review`'s primary home stays in the Code review
neighborhood; this design claims only a secondary role.

**A third policy on the same axis.** `cso` makes the precision/recall threshold a *user-selected
parameter* — `/cso` runs an 8/10 confidence gate, `/cso --comprehensive` a 2/10 gate. That is
neither `/diss`'s hard filter nor `review`'s recall preference, and it suggests the evidence gate
may belong in the protocol as an invocation parameter rather than inside any single perspective.
Recorded as an observation; `cso` keeps its reference disposition.

### 5.2 Retained: `plan-eng-review` is not the `/diss` voice

`plan-eng-review`, "Cognitive Patterns — How Great Eng Managers Think," `:845` — *"Incremental
over revolutionary — Strangler fig, not big bang. **Refactor, not rewrite** (Fowler)"* — negates
the characteristic `/diss` move of naming the data structure that should have existed and judging
the code against it. The same file holds its own override at `:836` (*"If the existing foundation
is broken, say 'scrap it and do this instead'"*), so the eng-manager voice has a standing rule
plus an exception where the `/diss` voice has only the exception. A clean rewrite requiring an
irreversible big-bang migration is a real input on which they file incompatible recommendations.
**Two decision policies.** Hash unchanged since the original inspection, so this evidence stands.

### 5.3 Corrected: `grilling` is not a perspective

Its entire body is 12 lines and contains no prior about any artifact. Every decision is
explicitly returned to the user: *"The **decisions**, though, are mine — put each one to me and
wait for my answer."* It cannot produce an incompatible recommendation because it does not
recommend — it interrogates and defers. Under section 6 it contributes **protocol** (one question
at a time; walk the decision tree resolving dependencies one by one) and **machinery** (offer a
recommended answer per question; look facts up rather than asking). Downgraded from the original
design's "persona."

What survives is valuable and was previously mis-filed: the one-at-a-time interaction bound is a
reader-load protocol parameter, and *"asking multiple questions at once is bewildering"* is its
stated rationale.

### 5.4 Corrected: `diss-claudemd` does not carry the venomous register

Zero occurrences of *venomous*, *cynical*, *Linus*, *Ramsay*, or *brutal* anywhere in the file.
Its role is delivered inside an `Agent` subagent prompt at `:205` and reads *"You are a prompt
engineering specialist reviewing a CLAUDE.md file for compatibility with the latest Claude
models"* — which is `/trim:9`'s role, *"You are a prompt engineering specialist. You review
prompts and SKILL.md files against Anthropic's official best practices."* Both then run the same
playbook: fetch and index the published practices, then audit against them.

The original's "one persona, four jurisdictions" for the `diss*` family is therefore wrong. Three
share the venomous register (`/diss`; `/diss-api` in variant form at `:9`, *"venomous API design
critic… pedantry of a standards committee with the patience of a burnt-out tech lead"*;
`diss-infra`), and `diss-claudemd` groups with `/trim` instead.

**This makes `/trim`'s persona less provisional, not more.** It now has a second independent
artifact expressing the same reduction-and-published-practice prior over a neighbouring
jurisdiction. The provisional label is retained pending behavioral evidence, but the documentary
basis is stronger than the original recorded.

### 5.5 Resolved: `devex-review` versus `plan-devex-review`

Same perspective, different jurisdiction and playbook.

- Shared perspective: `plan-devex-review:849` — *"You are a developer advocate who has onboarded
  onto 100 developer tools"* — with "DX First Principles" (`:869`) and TTHW benchmarks (`:922`).
  `devex-review` runs the same TTHW metric (`:27`).
- Different jurisdiction: `plan-devex-review` reads a **plan**; `devex-review` audits a **running
  artifact** — *"screenshots error messages, evaluates CLI help text"* (`:27`), triggering on
  "try the onboarding" (`:30`).
- Different playbook: live execution and screenshot capture versus plan reading.

Under section 6 that is one perspective over two jurisdictions with two playbooks — not two
voices. This closes the open question raised when `devex-review` was added to the row.

### 5.6 Resolved: `design-review` is a three-stage bundle

`design-review` presents one command but performs three different user jobs:

1. **Audit and report** — its first-impression, design-system, page, interaction, consistency,
   screenshot, and report phases inspect a running interface and produce findings. This is the
   visual-interface lens inside `astra-critique`.
2. **Fix and verify** — its triage and fix loop edits source, creates atomic commits, captures
   before/after screenshots, and re-runs the audit. This belongs to `astra-interface`.
3. **Bootstrap testing** — it may select and install a test framework, create tests and CI, and
   write testing guidance. This belongs to the future Testing design.

The primary home is `astra-critique` because the user explicitly placed review there and because
the audit/report is the prerequisite artifact from which every later action follows. Primary home
does not transfer the other stages: Critique retains finding IDs, evidence, visual captures, and
the report shape, then emits a typed handoff carrying them. It never edits source, commits a fix,
or bootstraps tests. Until both secondary roles preserve those behaviors, `design-review` cannot
pass its source-specific retirement gate.

### 5.7 `grilling` versus this skill

Both interrogate, but the outcomes differ: `grilling` drives toward *shared understanding before
acting* and returns every decision to the user unresolved; this skill returns *attributable
judgments about an existing artifact*. The interaction protocol is shared and absorbed (§5.3);
the user outcome is not. Recorded so the triggers do not silently collide during the coordinator's
roster-wide pass.

### 5.8 Authority fields, prerequisites, and failure behavior that must survive

| Must survive | Source evidence | Why it cannot be waived in prose |
|---|---|---|
| `disable-model-invocation: true` ×2 | `grill-me`, `grill-with-docs` frontmatter | Removes the skill from autonomous reach; a prose merger silently re-enables it |
| `effort: xhigh` ×2 | `diss-infra`, `diss-claudemd` frontmatter | A reasoning-effort override cannot be reproduced by instruction text |
| Hard gate: no implementation | `office-hours` — *"Do NOT invoke any implementation skill, write any code, scaffold any project"* | The gate is the guarantee that a critique stays a critique |
| `Edit`/`Write` + `AskUserQuestion` | `/trim` `allowed-tools` | The reduction review stays here, but mutation becomes a Plan & spec secondary role; Critique must not inherit the write authority |
| Source edits, atomic commits, and re-verification | `design-review` phases 8–9 | Preserved by `astra-interface`; Critique hands off only the defect, evidence, impact, and constraints |
| Test-framework bootstrap and regression tests | `design-review` setup and phase 8e.5 | Preserved by the future Testing design; Critique reports only the testing gap and evidence |
| `Agent` dispatch + `Task*` | `/diss` `allowed-tools` | Its reviewer roles run as separate contexts, not as prose sections |
| Fresh reviewer isolation and blind filing | `autoplan:1181-1189,1304-1315,1380-1391,1506-1517` | The existing plan convener prevents earlier reviews from contaminating later filings; the candidate may improve the protocol but cannot claim this mechanism as new |
| Dual-model degradation and decision audit | `autoplan:1155-1196,1567-1580` | Outside voices may fail independently, and auto-decisions remain attributable on disk instead of disappearing into synthesis |
| mysql MCP **with** CLI fallback | `diss.md:236` — *"CLI fallback (only if MCP unavailable)"* | The one source that degrades correctly; its shape is the rule |
| context-mode MCP **without** fallback | `/trim` `allowed-tools`; `diss-claudemd:32,209,213` | Declared-and-broken in one case, **undeclared and broken** in the other — see §7 |
| Evidence-only verification | `diss.md:282-296` — keyed on `finding_id`, reports `RESOLVED`/`PERSISTING`/`NEW`, no persona, *"No evidence = no finding"* | The seat that filed a claim is the worst possible judge of it |
| Register as a field | `diss.md:7`, `diss-api.md:9`, `diss-infra:17` | Three registers over one prior; collapsing them loses tone the user chose, collapsing the prior loses judgment |

`autoplan`'s policy of auto-deciding most intermediate choices is deliberately **replaced**, not
silently preserved: it conflicts with the user's standing rule against resolving normative
tradeoffs without surfacing them. The auditability and failure handling survive; the normative
resolution policy changes explicitly. The same decomposition applies to every mutation-capable
source: Critique preserves the review and its evidence, while a typed problem handoff routes to
the peer that owns the downstream job without attempting or prescribing that job.

---

## 6. Proposed skill design

**Architecture hypothesis:** one shallow public `astra-critique` facade with a fixed procedural
core and one level of directly selected, non-invocable review lenses. Its candidate composition
rule remains:

> **Panel seat = Perspective × Playbook × Jurisdiction. Panel = Protocol + one or more seats.**

The four layers, and the evidence each already exists:

| Layer | Question it answers | Evidence today |
|---|---|---|
| **Perspective** | *why* it reaches a conclusion — priors, decision policy, register | `plan-eng-review` "Cognitive Patterns" `:838-855`; `plan-ceo-review` `:906-923`; `cso` `:789-795` |
| **Playbook** | *what* evidence it gathers, which tests it runs | `diss.md` "Code Map" `:141-180`, "Risk Classification" `:182-205`, verifier `:282-295`; `plan-devex-review` TTHW `:922` |
| **Jurisdiction** | *which* artifact, this invocation | declared in the convening skill's panel table |
| **Protocol** | isolation, conflict handling, rendering, user control | `autoplan` fresh-context and degradation machinery plus the proposed normative-conflict rule; see Appendix A |

**A lens is packaging, not a fifth reasoning layer.** A lens is one directly referenced support
resource that declares the eligible seat rows for an agenda or artifact class. Perspective,
playbook, and jurisdiction remain fields on each row; they do not become nested skills,
directories, or recursive dispatch. A lens has no trigger metadata, cannot be invoked by the
user or model, cannot load another lens, and cannot render or hand off independently. The
Critique core selects every lens directly.

**The playbook layer is load-bearing.** `diss.md:151-193` builds a code map and risk
classification *before any voice speaks*. That is neither a personality nor generic chassis — it
is the investigation method the adversarial seat runs across every jurisdiction. Under a
three-layer model it has nowhere to live, so it would bloat the perspective, leak into the
chassis, or be discarded. Separating it also makes seats recombinable: the same
failure-mode-mapping playbook produces different findings under the eng-manager prior ("what is
the blast radius") than under the attacker prior ("what does this expose").

**Why a panel is the candidate rather than a settled fact.** Several sources have overlapping
standing over the same artifact and documentary evidence of incompatible policies — §5.1 and
§5.2 each identify a concrete pair. A flat merged voice would have to pick one prior silently,
which is the outcome the user's standing instruction forbids. But documentary disagreement does
not prove that convening the perspectives improves an output. The panel survives as the proposed
architecture only if §9 shows a positive cross-jurisdiction win over the source oracle without
home-jurisdiction regression.

**Information flow.** Artifact and agenda classification → direct lens selection → decision
catalogue → fresh-context blind filing → seat-declared conflict scan → targeted response →
factual verification or user resolution → problem-class and destination nomination → procedural
report rendering with every route candidate → same-problem classification resolution → user
selection of zero or one immediate route → selected-profile validation → typed problem handoff
rendering when selected → stop. A home-jurisdiction request loads the strongest applicable lens
and may select one seat; the protocol does not load extra lenses or convene extra perspectives
merely because they exist. Cross-jurisdiction requests may fan out to several directly selected
lenses, but no lens calls another. When several seats run, each commits its claims before seeing
any other filing. Fresh contexts provide the isolation that `autoplan` already demonstrates;
ordering controls later exposure.

**What is inherited and what is new.** Fresh contexts, blind filing, dual-model redundancy,
degradation tags, consensus tables, and decision auditing already exist in `autoplan` for plans.
They are behaviors to preserve or deliberately simplify, not Astra Critique's novelty. The
candidate additions are artifact routing across diffs, API specs, IaC, plans, running developer
experiences, architecture and technical-design decisions, prompts, and CLAUDE.md; a wider seat
pool; evidence-only factual verification; and refusal to auto-decide normative conflicts.

**Where user choices occur.** Normative disagreements route to the user as an explicit choice with
every surviving side quoted. Panel composition is declared data, overridable by the user.
Whether to act is always the user's. Each seat may classify the problem and nominate the peer
skill that owns that problem class. The procedural chair may validate and render those
nominations but may not invent one or choose between incompatible surviving nominations. If the
nominations conflict over the same problem, classification becomes a user choice. If several
independent problems map to different peers, the report preserves every route and the user chooses
which one, if any, continues now. The chair may not rank the independent routes or drop the
unselected ones.

**How uncertainty is represented.** Factual disputes go to an evidence-only verifier whose result
describes the evidence — supported, contradicted, or indeterminate — never who wins. An
indeterminate result is rendered as explicit uncertainty with both sides quoted, never silently
resolved.

**Failure and degradation.** A missing prerequisite degrades that seat, not the panel: the seat
either runs a reduced playbook and says so, or is dropped with its absence reported. A missing
lens invalidates that route rather than falling through to an unrelated lens. A panel that cannot
convene any seat reports that rather than emitting a merged opinion. An unavailable destination
does not erase the report; when its reconciled profile exists, the selected handoff identifies the
unavailable peer and the prerequisite or manual alternative. A missing or inconsistent profile
leaves the route candidate in the report and marks a reconciliation gap rather than fabricating a
capsule. The `/diss` fallback shape — prefer MCP, detect absence, fall back — and `autoplan`'s
per-voice degradation matrix are the observed models.

**Depth and internal seams.** The public interface remains one invocation plus one artifact.
Perspective / playbook / jurisdiction are internal seams because §5.1 and §5.5 demonstrate the
same perspective over different playbooks and jurisdictions, and §5.4 demonstrates the same
playbook under two different names. Routing, factual verification, rendering, and handoff
validation stay internal modules. The chair is separate from the seats because §5.1(b) shows
mechanical rules and substantive priors are different kinds of thing. None of those seams becomes
caller-facing. There are no child Critique skills: all Astra skills remain public peers, and the
handoff is an output edge mediated by the user rather than a parent invoking a child.

**Review scope is independent of the destination roster.** The accepted artifact and directly
selected lenses determine whether Critique can review a request. Destination profiles are
consulted only after the critique report exists, to shape an optional handoff. A missing or
not-yet-designed profile cannot make code, an architecture or design choice, a plan, IaC, a
prompt, or any other supported jurisdiction out of scope, and it cannot force the problem into
one of the currently documented Design destinations.

**Report and typed-handoff shape.** The report renders before the handoff and remains useful even
when no destination is available. For every independently actionable problem it records the
problem class, candidate destination or unresolved owner, finding IDs and evidence, and profile
state. The table below is the conceptual common envelope for the zero or one selected immediate
capsule; exact field names, serialization, and runtime schema remain deferred:

| Field | Rule |
|---|---|
| `destination_skill` | Exact peer Astra skill, or `none` when no further job is justified |
| `why_this_skill` | Reviewer-attributable reason this peer owns the identified problem class |
| `invocation` | Exact suggested invocation carrying the problem; never executed by Critique |
| `artifact` and `agenda` | The reviewed artifact and the bounded problem scope |
| `problem_statement` | Concise statement of what is wrong or uncertain, without a proposed remedy |
| `finding_ids` and `evidence` | Traceable links back to surviving findings and their evidence |
| `observed_impact` and `affected_scope` | Who or what the problem affects and why it matters |
| `constraints` and `open_decisions` | User-supplied boundaries, unresolved choices, and user rulings; not a design prescription |
| `prerequisites` and `context_gaps` | Evidence or state the destination may need; unavailable items remain explicit |
| `destination_payload` | Small typed variant containing only problem evidence unique to the selected peer |

**Problem/solution boundary.** The handoff must not contain a proposed design, remedy,
implementation sequence, tool choice, or Critique-authored success criteria. A source reviewer
may mention a possible fix inside its attributable critique when source fidelity requires it, but
the chair neither selects nor elaborates that fix and never promotes it into the handoff.
The destination skill owns solution exploration, solution decisions, planning, and the criteria
by which its solution will be judged.

The destination profiles are support data, not a skill registry or allowlist. Each later
per-skill design that accepts Critique handoffs is authoritative for its accepted problem class
and destination-only payload. During final roster reconciliation, the coordinator records that
accepted profile as the canonical peer contract; the Critique design consumes the reconciled
snapshot rather than defining another peer's interface unilaterally. Destination selection uses
that reconciled Astra peer roster, not the examples below. After the user selects an immediate
route, the Critique core reads at most that one profile directly; it never reads the destination's
full `SKILL.md` at runtime.

The three currently approved Design peers are the **first profile tranche only because their
designs are being worked on first**. They illustrate payload variation; they do not limit what
Critique can review or where it may hand off. `astra-interface` appears twice: roadmap amendment 3
folded the proposed `astra-presentation` into it on the user's decision, so Interface now owns two
seeded problem classes. Roadmap section 3.2 requires each to keep a **separately named payload**,
because one merged payload would lose exactly the distinction Critique needs in order to route:

| First-tranche Design destination | Owned problem class | Problem-only additional payload |
|---|---|---|
| `astra-product-design` | Approved design-direction problem | Observed experience problem, affected user journey, supporting user evidence, and research gaps |
| `astra-interface` | Interaction, accessibility, or visual-system defect | Affected surfaces and states, reproduction evidence, and observed accessibility or interaction defects |
| `astra-interface` | Narrative or data-comprehension problem | Audience, observed narrative or data-comprehension problem, affected slides or sections, and supporting evidence |
| `astra-brand` | Identity or audience-signal inconsistency | Identity inconsistency, assets or tokens where it appears, and the conflicting audience signal |

Later roster-approved profiles may cover code changes, architecture or technical-design choices,
plans and specifications, infrastructure, prompts, testing, or any other peer-owned problem
class. Their exact skill names and payloads belong to those later designs; this document does not
invent them in advance. If a correct peer exists but its profile is missing, Critique keeps the
report and common problem envelope, marks the profile as a reconciliation prerequisite, and does
not substitute an unrelated Design peer.

If incompatible nominations for the same problem survive, the chair presents the classifications
through `AskUserQuestion`. If several independent route candidates survive, the chair presents
all of them without ranking and the user selects zero or one for the immediate capsule. The
unselected candidates stay in the report. If no actionable finding survives, or the user defers
all routes, the result emits no immediate handoff. In every case Critique stops after rendering.

**Three later implementations exercise the same task interface.**

| Implementation | Purpose | Eligible as final? |
|---|---|---|
| Source oracle | Preselected strongest original for the artifact and jurisdiction | No; baseline only |
| Reference convener | Routes to and coordinates the unchanged originals | No; validation scaffold that breaks when originals are deleted |
| Self-contained candidate | Vendors or re-expresses the retained playbooks, perspectives, jurisdictions, authority, and degradation behavior internally | Yes, only after §9 passes |

This sequence makes the failure legible. If the reference convener adds no value, reject or
narrow the panel before rewriting sources. If it wins but the self-contained candidate loses,
the extraction is at fault rather than the idea of coordination.

**No shared Astra module is proposed.** `docs/design-requirements.md` section 7.6 requires two
designs demonstrating the same seam. This is one. The directory layout in Appendix A is
historical for exactly that reason.

---

## 7. Dependencies and delivery shape

| Dependency | Type | Relationship | Behavior when absent |
|---|---|---|---|
| Reviewer contexts | agent | The design **invokes** separate contexts per seat; `/diss` uses `Agent`, and `autoplan` gives each phase a fresh reviewer explicitly denied prior reviews | Sequential in-context seats lose isolation — must be stated, not silently accepted |
| Original source files | skills and commands | The later reference convener **invokes or reads** them unchanged for comparison only; the self-contained candidate **replaces** that dependency | A missing original invalidates its convener comparison. Any final candidate that still needs it is not self-contained and cannot retire it |
| `mcp__awslabs-mysql-mcp-server`, `-uat` | MCP server | **Coordinates** — preferred path for SQL evidence | Falls back to tunnel + CLI, per `diss.md:236`. **Not currently configured** |
| context-mode MCP (`ctx_fetch_and_index`, `ctx_search`) | MCP server | **Coordinates** — fetches published practices for the prompt-audit playbook | **No fallback exists in either consumer.** Plugin not installed |
| `design-api` | skill (reference) | **Reads** as the compliance standard for the OpenAPI jurisdiction | Jurisdiction degrades to generic critique; must be reported |
| `domain-modeling` | skill (reference) | **Documents only** — `grill-with-docs`'s other half is a separate job | Not this skill's concern; recorded as a cross-neighborhood role |
| gbrain context | external runtime | **Documents only** — `office-hours` preflight, already optional upstream | Upstream already handles stale-but-usable fallback |
| `git`, `gh`, JaCoCo XML | runtime | **Coordinates** — evidence sources for the code jurisdiction | Playbook runs reduced and says which evidence was unavailable |
| Destination Astra skills | peer skills | **Documents only** — each destination design owns its accepted problem class and profile; the coordinator reconciles the canonical snapshot; Critique names at most one user-selected peer and never reads or invokes its full workflow | Report retains every route candidate. A missing or inconsistent profile is a reconciliation gap; a known but unavailable peer can still be named with prerequisites or a manual bridge |

**Planned self-contained delivery shape.** Exact filenames remain implementation work, but the
depth constraint is normative:

```text
astra-critique/
├── SKILL.md
└── references/
    ├── lens-<agenda>.md
    └── handoff-<destination>.md
```

`SKILL.md` owns routing, protocol, the common handoff envelope, report rendering, and the rule for
when each directly linked reference is read. It should remain below the skill-authoring guidance's
500-line threshold. Every lens and destination profile is one level below it; there is no
`SKILL.md` under `references/`, no support-file chaining, and no recursive skill discovery.
Detailed source-derived rubrics and destination-only payload fields live in those on-demand
references rather than bloating the root context. This is an implementation invariant, not
authorization to create the directory during phase 0.

**A finding for the README's MCP table.** The README records three commands reaching for
unconfigured MCP servers (`/diss` with a fallback, `/pr` and `/trim` without). **`diss-claudemd`
is a fourth, and it is worse than `/trim`:** it calls `ctx_fetch_and_index` and `ctx_search` at
`:32`, `:209`, and `:213` while declaring **no `allowed-tools` at all**, and it ships no fallback.
`/trim` at least declares the dependency it cannot satisfy. This is the same
reaching-outside-the-unit failure the README identifies for `guard`, in its quietest form: an
undeclared dependency on an absent server.

**Two further sideways reaches, for the same principle.** `autoplan:907` — *"reads the full CEO,
design, eng, and DX review skill files from disk"* — and `:714`, which shells out to
`~/.claude/skills/gstack/bin/gstack-question…`. Both break if gstack is uninstalled. They are
why `autoplan` is useful as reference-convener evidence but cannot be the final architecture
when the originals are meant to be deleted. They are evidence for the self-containment
principle, not phase-0 implementation work.

**Tool authority.** Pre-approval is not restriction: the seats need read and search authority over
the artifact and its repository, and the design must record that **no seat may edit the artifact
under review**. `/trim`, the plan reviewers, and `design-review` demonstrate mutation behaviors
that must survive in destination skills, not exceptions that weaken Critique's boundary. Detailed
permission design is deferred; the forbidden effect is not.

---

## 8. Manual bridge

Usable today, in this order:

1. **Code diff** — `/diss` (or `/diss-api` for a spec, `Skill(diss-infra)` for IaC). Highest-value
   single step; the mysql MCP is absent, so it takes the documented CLI fallback.
2. **Plan** — `/autoplan` for the sequenced CEO → design → eng → DX pass, or the four
   `/plan-*-review` commands individually when you want to read them separately. Explicitly ask
   for report-only review when the plan file must remain unchanged.
3. **Running visual interface** — invoke `/design-review` with the explicit instruction *"audit
   and report only; stop before test bootstrap, source edits, commits, or fix verification."*
   Its native workflow does not expose a first-class report-only mode, so this override is a
   manual approximation rather than preserved delivery behavior.
4. **Problem statement** — `/office-hours` before either, when the problem may not be understood
   yet; `/elon` when the requirement itself is suspect.
5. **Prompt or `SKILL.md`** — `/trim`. **Missing prerequisite:** its first two research steps are
   context-mode MCP
   calls and the plugin is not installed, so the published-practice grounding is unavailable and
   the review proceeds on the model's own recollection. Ask it to report without applying edits.
   `Skill(diss-claudemd)` has the same gap for CLAUDE.md and does not declare it.
6. **Cross-checking a `/diss` result** — run `/review` on the same branch. Per §5.1 these two
   carry incompatible filing policies and are predicted to disagree on the stubbed-test fixture.
   The pair is the manual approximation of a two-seat panel; the later characterization run must
   establish whether that disagreement is reproducible and useful rather than assumed.

After any current review, manually append one route candidate for every independent actionable
problem: candidate skill and reason; problem statement; finding IDs and evidence; artifact and
bounded problem scope; observed impact and affected scope; user constraints, open decisions,
prerequisites, context gaps, and whether a reconciled destination profile exists. Do not add a
proposed solution, implementation steps, tool choice, or new success criteria: the downstream
skill owns them. Ask the user to select zero or one immediate candidate, then append its exact
suggested invocation and destination-only payload only when the reconciled profile exists. If it
does not, retain the selected route as a named reconciliation gap and emit no capsule. Preserve
unselected candidates in the report and stop. This approximates the typed handoff without
pretending that any current source implements it.

**What the bridge does and cannot approximate.** `/autoplan` already supplies fresh independent
reviewers, explicit blind filing, dual-model degradation, consensus tables, and an audit trail
for plans. It does not span the other jurisdictions, and it auto-decides most intermediate
questions. Separate `/diss` and `/review` runs have no shared decision catalogue or chair. No
current path combines all jurisdictions, preserves attributable positions, and routes normative
conflicts to an explicit user choice through one self-contained interface. No current path also
emits the typed peer handoff while guaranteeing that the destination remains uninvoked.

---

## 9. Deferred implementation and validation

Skill-specific only; `docs/phase-0.md` section 8 owns the phase-wide list.

### 9.1 Hypotheses and comparison systems

| Hypothesis | Comparison | Failure consequence |
|---|---|---|
| **H1 — routing** | The candidate selects the source-oracle jurisdiction and required playbooks from the artifact and request | Narrow the trigger or require an explicit mode; do not hide uncertain routing |
| **H2 — coordination value** | The reference convener versus the source oracle on cross-jurisdiction artifacts | Reject the panel or reduce it to routing among specialist modes; convenience alone cannot be called better critique |
| **H3 — internalization fidelity** | The self-contained candidate versus the reference convener on identical artifacts | Rework the extracted seat or keep the source installed; no retirement |
| **H4 — retirement safety** | The passing self-contained candidate versus each source's behavior, authority, dependencies, delivery shape, and failure paths | Keep the affected source; other sources may retire only through their own gates |
| **H5 — bounded disclosure and handoff** | The self-contained candidate on single- and cross-jurisdiction cases plus downstream-routing cases | Reject the packaging or destination-profile set if unrelated lenses or destination skills load, an independent route is lost, more than one immediate capsule is emitted, the wrong peer is nominated, solution instructions leak into the handoff, or Critique starts another workflow |

The three systems are:

1. **Source oracle:** the strongest applicable original selected before outputs are seen. For a
   source's home-jurisdiction case, that source is its own oracle. `autoplan` is an oracle or
   existing-convener reference for plans only; it is not the baseline for diffs, API specs, IaC,
   running artifacts, prompts, or CLAUDE.md.
2. **Reference convener:** one temporary invocation that coordinates unchanged originals. It
   tests routing and panel value without rewriting their behavior.
3. **Self-contained candidate:** the proposed final superskill with retained behavior
   internalized and no dependency on the source files it may later replace.

### 9.2 Fixed corpus and method

The later corpus must be versioned and selected before outputs are generated. It includes:

- **home-jurisdiction cases:** code diff, OpenAPI specification, Terraform or CloudFormation,
  decision or problem statement, plan, running developer experience, running visual interface,
  prompt or `SKILL.md`, and CLAUDE.md;
- **cross-jurisdiction advantage cases:** artifacts containing decisions on which two retained
  perspectives have standing;
- **expected-divergence cases:** `/diss` versus `review` on working code with stubbed tests
  (§5.1); `plan-eng-review` versus the `/diss` perspective on an irreversible big-bang rewrite
  (§5.2); and `/trim`'s reduction prior versus a completeness-first perspective on one
  `SKILL.md` (§5.4);
- **expected-convergence control:** `devex-review` and `plan-devex-review` must not manufacture
  incompatible recommendations once decision and jurisdiction are held constant (§5.5);
- **handoff-routing cases:** first-tranche Design examples for `astra-product-design`,
  `astra-brand`, and **both** of `astra-interface`'s seeded classes — an interaction,
  accessibility, or visual-system defect and a narrative or data-comprehension problem — which the
  corpus must keep as two separable routing decisions rather than one Interface case; non-Design
  problems in code,
  architecture or technical design, and plan or specification jurisdictions routed to their
  roster-approved peers once those peer designs exist; a missing-profile case that must not fall
  back to an unrelated Design peer; incompatible nominations for the same problem that require a
  classification choice; several independent problems with different accepted destinations whose
  unselected routes must remain in the report; and a completed review for which no further skill
  is actionable; and
- **prerequisite failures:** absent context-mode MCP, absent mysql MCP with its CLI fallback,
  missing `design-api`, a missing selected lens, an unavailable destination peer, and individual
  reviewer-context failure.

Run all three systems on identical artifact, evidence, and decision-catalogue inputs at least
three times. A neutral wrapper may normalize the output schema but may not add perspective text,
expected answers, or pair identities. A blinded evaluator receives de-identified,
order-randomized outputs and the fixture rubric.

Record critical-decision recall, supported-claim precision, unsupported-claim rate,
source-unique supported findings, actionability, duplicate/noise load, informative-conflict
yield, routing accuracy, loaded-lens count, irrelevant-context input tokens, handoff-routing
accuracy across Design and non-Design fixtures, destination-coverage by Critique jurisdiction,
route-candidate recall, unselected-route retention, finding-to-handoff traceability,
solution-prescription leakage, unrelated-profile fallback, excess immediate capsules, unintended
destination invocations, input and output tokens, wall-clock time, and degradation state.
Solution-prescription leakage, unrelated-profile fallback, excess immediate capsules, dropped
independent routes, and unintended destination invocations must all remain zero. `Decisions
surfaced` alone is diagnostic, not quality.

### 9.3 Gates

1. **Source characterization.** Each proposed divergence must appear on the same decision and
   target in at least two of three blind original-source runs; the convergence control must not
   manufacture a conflict. A distinction that fails characterization is reclassified before it
   becomes an internal seat.
2. **Home-jurisdiction non-regression.** The reference convener and self-contained candidate
   lose no seeded critical decision that the source oracle finds reproducibly, introduce no
   higher unsupported-claim rate, and do not lower median actionability within any source's home
   jurisdiction.
3. **Positive coordination advantage.** On at least one preregistered cross-jurisdiction class,
   both combined systems must add a supported critical decision or a supported normative conflict
   that blind evaluation judges decision-changing and that the source oracle misses in at least
   two of three runs. Routing convenience, lower maintenance, or lower token cost does not satisfy
   this quality gate.
4. **Internalization fidelity.** The self-contained candidate preserves the reference convener's
   characterized divergences, convergence controls, source-unique supported findings, and
   prerequisite degradation. A matching final recommendation does not excuse lost evidence or a
   silenced perspective.
5. **Bounded topology and handoff integrity.** The candidate loads only its core, every directly
   selected lens, and at most the selected destination's compact handoff profile. It loads no
   nested `SKILL.md`, follows no lens-to-lens link, and neither reads nor invokes the destination
   skill. Each handoff identifies the correct peer and remains traceable to surviving finding IDs
   and evidence. It contains the problem, impact, scope, and preserved user constraints but no
   proposed solution, implementation steps, tool choice, or Critique-authored success criteria.
   The routing corpus covers both Design and non-Design problems; a missing profile is reported
   rather than replaced by an unrelated peer. Same-problem destination conflicts go to the user;
   multiple independent routes all remain in the report while zero or one becomes the immediate
   capsule. No-action and defer-all cases emit no capsule. Any dropped route, excess capsule,
   solution leakage, unrelated-profile fallback, or unintended destination invocation fails the
   gate.
6. **Retirement.** After gates 1–5 pass, each source separately requires preserved invocation
   authority, delivery shape, external dependencies or fallbacks, failure behavior,
   self-containment from that source's files, and explicit user approval. Failure blocks only that
   source's retirement; it does not erase evidence earned for another source.

Nothing here authorizes building a fixture or harness during phase 0.

---

## 10. Provenance and open questions

**Inspection.** Nineteen sources are recorded in §3.1: the original 18 were inspected
2026-07-30, and `design-review` was inspected 2026-07-31. Component type, location, invocation,
availability, and declaration were recorded for each. Every material claim in §5 is
**Observed** — quoted from an inspected body — except the two labeled provisional (`/trim`'s
perspective, and `cso`'s gate as a protocol parameter rather than a perspective field), which are
**Inferred**. No source in this design is **Unavailable**, and none is claimed as absorbed.

**Anchoring.** Headings and unique quoted phrases are the primary anchors. Line numbers are
convenience coordinates against the hashes below; a hash mismatch invalidates the line anchors
until the source is re-inspected and they are regenerated.

Gstack sources resolve at `~/.claude/skills/<name>/SKILL.md` → symlink →
`~/.claude/skills/gstack/<name>/SKILL.md`; commands at `~/.claude/commands/`.

```text
44331dda57f461db4fec3f2efb6ddabe7aaaa0a57ae0f88a883bc61aed8a0587  grilling/SKILL.md
6189dfceb7304a6e5558f75d87e68fa3bc7fcf7ba120e44f21f8a61fe01eba54  grill-me/SKILL.md
610d091047bcfb9db0f75c057d15538481a721111579fc5ec7f83ad9131a2165  grill-with-docs/SKILL.md
94b3172c61321dfa7bb0701bb9a4e3b1f305ba8a94e78ffed2ed3a17df75da03  diss-infra/SKILL.md
4778d24b660e04515492909d3d204a9d0ec7ec8ac38e99d1c0e7a420de0c8408  diss-claudemd/SKILL.md
aa162970e42dbca046f7f6ffb0b40167cf63b76b50d197d87fd4895937680513  devex-review/SKILL.md
c18016a320c7516814d41067936b9b239899e08f27b133a306f4de4c20921284  plan-ceo-review/SKILL.md
0f756585231f5630d80e3a3163ca664312acf78ea34e2bb535275816ffb1bfd0  plan-design-review/SKILL.md
4d6cc577f07af1a0268e89ba0fdf45eb595583bdad306f809cbb8b6645c18951  plan-devex-review/SKILL.md
41c92a82319c081ef48a17733bcd5815d83637cf1e0390c45db5f9ccbbca08e9  plan-eng-review/SKILL.md
92ee16af71d5e0088326869b0a211c50f94b9261eeae75656bc21f9bcfae2031  review/SKILL.md
b5a0b9d72f4a992ba0b52cd7b27d15e7e0e29e35c4b775477ec3a031c47f5c92  office-hours/SKILL.md
4d5da6367475aaad38bbf59f29e5c7fa2b184d48590951100b1d409b723133ea  cso/SKILL.md
73e2bf3e7b1868493fc162dccf9f26c182f50e4cfcad3e4f02efce0e3099e472  autoplan/SKILL.md
a7fb587db289843467c0008d1941ebd39eff57afed0eab422f08b7d6604107e5  design-review/SKILL.md
b4e029d6c927b1ba671748b5d23e026d1c8059bde96e955fb504490da22b9b69  diss.md
f2b765a4ed00c80e40fc600d7d09af518925744c581e5f606a471c2fe7431b02  diss-api.md
f15285425fe5e94914350c10e9ee71526c7b194eeb30fe1881471d7dad95e042  elon.md
0ac5d05a598ca73edf0e35956efddf10ce989a0a68c9483bb6355cab3da73fff  trim.md
efd896c5a85f3983c2dd979676736855bfae5a6aca75ab32b78948ba8c6f5559  README.md (STALE — see below)
```

The original 18 source hashes were re-verified on 2026-07-30 and all matched;
`design-review` was hashed from the live registered source on 2026-07-31. The `README.md` hash
records the then-unstaged working draft whose amendments Appendix B proposed; that draft was
committed at `a037f20` and revised afterwards, so it **no longer matches** and every
`README.md:<line>` anchor in this document is invalid. Cite README headings instead.

**Architecture comparison.** The primary-source comparison in
[`docs/research/2026-07-31-critique-skill-architecture.md`](../docs/research/2026-07-31-critique-skill-architecture.md)
supports the one-public-facade, one-level-support-resource topology. It is architecture evidence,
not source-preservation or retirement evidence.

**Claims disproved on inspection and corrected here.** `grilling` as a perspective (§5.3);
`diss-claudemd` as part of the venomous family (§5.4); Linus and Ramsay as separate voices, and
the fixture built on them (§5.1); the `plan-eng-review` merge, disproved in the original review
and re-verified here (§5.2); and the description-level treatment of `autoplan` as mere sequential
review, corrected by reading its full body (§§4, 6, 8). Two successive cost-scaling
characterizations and the claim that fixtures guarantee conflict detection were corrected in the
original review and are retained in Appendix C.

### Open questions

- **Whether the panel earns its cost.** Documentary evidence establishes candidate distinctions,
  not a quality win. *Consequence:* if §9's positive-advantage gate fails, retain a
  self-contained interface only as explicit specialist modes after their own preservation gates,
  or abandon the merger; do not ship the panel as a quality improvement.
- **Lens and playbook roster.** Which direct lenses exist and how finely the playbooks inside
  them are divided. The depth is settled: every lens is one-level, directly selected, and
  non-invocable. *Consequence:* too fine and the selection table becomes unreadable; too coarse
  and §5.5's jurisdiction split has nowhere to live.
- **Destination-profile roster.** The four Design-peer payloads are the first tranche, not the
  destination boundary. Exact profiles for code, architecture or technical design, plans and
  specifications, infrastructure, prompts, testing, and other peer-owned jobs await their own
  designs. Each accepting peer design owns its problem class and payload; the coordinator records
  the canonical profile during final roster reconciliation and Critique consumes that snapshot.
  *Consequence:* every peer that accepts Critique handoffs must reconcile one compact profile
  before that route can pass §9.3 gate 5; a missing or inconsistent profile remains visible in the
  report, never narrows Critique's review scope, and never redirects the problem to an unrelated
  Design peer.
- **Does the evidence gate belong to the protocol or to each perspective?** `cso` parameterizes
  what `/diss` hard-codes (§5.1). *Consequence:* if it is a protocol parameter, `/diss`'s "no
  exceptions" filter becomes a default rather than a prior, which weakens the case for treating
  precision-first as part of its perspective at all.
- **`/trim`'s perspective.** Provisional pending behavioral evidence, now with two supporting
  artifacts (§5.4). *Consequence:* if it merges, the reduction prior disappears from the roster
  and prompt review loses its only counterweight to completeness-first voices.
- **Whether `review` should move.** Its primary home is the Code review neighborhood, but §5.1
  makes it this skill's sharpest contrastive counterpart. *Consequence:* if Code review's own
  design also claims it as central, the coordinator has a genuine ownership conflict rather than a
  secondary role.
- **monster-prompt.** Unchanged from the README. *Consequence:* `/diss`, `/diss-api`, `/elon`, and
  `/trim` are all monster-prompt commands, so four of this design's sources sit inside the
  unresolved boundary.

---

## 11. Six-skill reconciliation amendment

This section records the approved authority change before the remaining relevant skills are
absorbed. It does not claim that the Debug sources have already been re-inspected by this design,
that their ledger homes have moved, or that Critique's complete future behavior is now specified.
Where sections 1–10 or the historical appendices conflict with this section or
`docs/design-requirements.md` section 7.11, this section governs the surviving public design.

### 11.1 One public interface, three authority-preserving modes

| Mode | Owns | Required result | Forbidden effect |
|---|---|---|---|
| `review` | Evidence-backed judgment about an artifact or decision | Review findings with attributable claims, evidence, and unresolved normative choices | Selecting the remedy or changing the artifact |
| `diagnose` | Evidence-backed causal judgment about an observed failure | Causal findings, competing hypotheses, rejected hypotheses, and proof obligations | Adding probes, tests, configuration, instrumentation, or repairs to the target repository |
| `consult` | Read-only preservation of Critique authority in a downstream invocation | `pass`, `drift`, or `authority_gap` with Finding IDs and evidence anchors | Rerunning Critique, mutating a downstream artifact, approving it, or expanding an upstream contract |

The coding council remains the design's central novelty in both `review` and `diagnose`. In
diagnosis, seats independently form and challenge causal hypotheses. The chair may render
disagreement and the verifier may test factual claims, but a cause becomes established only when
observed evidence discriminates it from its live alternatives. Register, confidence, consensus,
or user preference cannot promote a hypothesis into a causal finding.

Critique may inspect the repository, logs, history, captured runtime state, and supplied
artifacts. It may run already-authorized existing tests and diagnostic commands and retain
isolated evidence captures that cannot affect target behavior. When establishing a cause needs a
new probe, test, configuration change, or instrumentation, Critique emits a
`diagnostic-instrumentation-required` finding containing the hypotheses and proof obligation. It
does not make the change itself.

### 11.2 Finding Set authority

The Finding Set is Critique's authoritative artifact. Exact runtime serialization remains
deferred, but every later candidate must preserve this conceptual spine:

| Field | Meaning |
|---|---|
| Finding Set identity | Immutable artifact ID, revision, content hash, input artifact identities, and mode |
| `finding_id` | Stable identity for one independently actionable observed problem or causal claim |
| Observation | What was reviewed or what failed, separated from interpretation |
| Evidence | Reproducible anchors, commands, outputs, logs, history, or artifact locations supporting the finding |
| Judgment or cause | Review judgment, or causal claim with `proven`, `probable`, or `unestablished` certainty |
| Hypotheses and proof obligations | Live alternatives, rejected alternatives with discriminating evidence, and evidence still required |
| Affected scope and observed impact | The bounded contract, behavior, path, user, or environment implicated by the evidence |
| Constraints and authority limits | User-supplied boundaries, unavailable prerequisites, and forbidden effects |
| Route candidates | Every independently owned downstream problem class, without selecting its solution |
| Consultant history | Inbound Understand determination and report identity when applicable, plus the Finding Set and downstream artifact identities, checkpoint, determination, and evidence anchors for each consultation |

The Finding Set contains no chair-selected solution, target behavior, delivery task, commit
sequence, or Critique-authored acceptance criterion. A source-faithful reviewer may mention a
possible remedy inside an attributable filing, but that mention is not an approved disposition
and cannot cross into Spec as selected intent without the user's decision.

### 11.3 Forward-only diagnostic continuation

For an incompletely diagnosed failure, Critique emits the symptom, available evidence, competing
hypotheses, and proof obligations. Spec may approve conditional outcomes for each supported,
contradicted, or indeterminate result. Implement maps those outcomes to exact diagnostic and
repair tasks. During execution, the persistent Critique consultant evaluates causal claims and
diagnostic evidence; the Spec consultant decides whether that evidence enters an already approved
branch. Implement proceeds without restarting Critique.

Critique consultation occurs at least before a critique-driven Specification is approved, before
an Implement roadmap is approved, at a roadmap's causal branch decisions, at Implement's final
verification checkpoint, and before Test or Ship closes a Finding ID. A determination is bounded
to the referenced Finding Set and downstream artifact revision. Evidence outside every approved
branch, evidence that invalidates the Finding Set, or a new user-owned decision returns
`authority_gap`; it never causes the consultant to invent a branch or rewrite history.

When a Finding Set directly relies on an Understanding Report, Critique invokes one persistent
Understand Code consultant after completing the Finding Set draft and before issuing it, and
reuses that consultant after new evidence or a repository revision changes a relied-on fact. It
passes the exact report and draft identities, revisions, and hashes; the exact relied-on claims;
and the changed evidence. Understand Code judges current-state support only and cannot create,
waive, or reclassify a finding. Critique owns any `drift` repair inside its active draft. A stale,
contradicted, or too-narrow report returns `authority_gap` and stops Finding Set issuance. If the
user continues, a new immutable Critique cycle must use a new report or independently ground the
affected fact without relying on the report.

### 11.4 Debug source preservation and deferred absorption

`astra-debug` is now a superseded historical design. Its inspected sources, bundled executables,
behavioral corpus, diagnosis techniques, causal certainty vocabulary, prerequisite degradation,
and source-specific retirement gates remain required evidence for Critique's later
source-expansion pass. Its former repair and instrumentation authority does not migrate into
Critique: specification belongs to Spec, mutation and atomic commits belong to Implement,
independent verification belongs to Test, and publication belongs to Ship.

Until that source-expansion pass and coordinator reconciliation occur:

- no Debug source row is represented as absorbed or resolved by this amendment;
- `staging-debug`'s deployment-effect allocation remains an open source-specific decision;
- the exact relationship between the coding council and the Debug design's phase machine remains
  a hypothesis for three-system comparison; and
- the historical Debug fixtures and source retirement gates remain intact rather than being
  silently generalized into Critique's existing corpus.

## 12. 92-component source-expansion amendment

The user-approved 92-component target in `docs/six-skill-source-absorption.md` performs the
source-expansion pass deferred by section 11.4. That coordinator design is the canonical census,
provenance record, cross-stack equivalence argument, and retirement-gate table. This design adopts
its following 18 primary source identifiers:

- code review: `code-review`, `review`, `requesting-code-review`,
  `receiving-code-review`, `superpowers:requesting-code-review`,
  `superpowers:receiving-code-review`, `feature-dev:code-reviewer`, and
  `code-review:code-review`;
- exploratory and health review: `dogfood`, `qa`, `qa-only`, and `health`;
- independent diagnosis and jurisdictional review: `codex`, `rca`, `cso`, and `java`; and
- device and visual review: `ios-qa` and `ios-design-review`.

These sources become internal review profiles behind Critique's existing `review`, `diagnose`,
and read-only consultant interfaces. Each profile preserves its exact input prerequisites,
separate-agent or tool delivery shape, evidence kind, confidence/severity vocabulary, degradation,
and source-specific retirement obligations. Every profile normalizes its authoritative output into
the Finding Set while retaining attributable source evidence; normalization does not erase a
source-unique field or collapse competing reviewer judgments.

Source-native repair, refactoring, instrumentation, bridge installation, commit, posted-comment,
or publication steps do not migrate into Critique. They become explicit downstream routes through
Spec, Implement, Test, and Ship. `rca` supplies causal-investigation method to `diagnose`, while
live stabilization and incident communication remain the separate `firefighting` job. `health`
supplies read-only quality judgment and trend facts; a pinned measurement may later be Test
evidence, but Critique does not certify the delivered revision.

This amendment proposes source allocation only. It changes no coordinator ledger row, runtime
skill, adapter, corpus, harness, installation, source-retirement state, push, or PR. The 18 rows
remain unabsorbed and unresolved until the coordinator migration, three-system comparison, and
their source-specific gates succeed.

---

# Appendix A — Panel protocol (historical detail)

> **Historical.** `docs/phase-0.md` section 8 defers exact schemas, routers, and conformance
> harnesses. Retained because it records *which distinctions must survive condensation* —
> structured stance, claim identity, revision status, reader bounds — not because any field is
> specified. Read as design reasoning, not as a contract. The shared `personas/`, `playbooks/`,
> and `protocol/` directories referenced throughout are a single-design proposal and do not meet
> the two-design threshold in `docs/design-requirements.md` section 7.6.

## A.1 Proposed design decisions

| # | Proposed decision | Rationale |
|---|---|---|
| D1 | *(historical — packaging deferred)* Astra ships as one plugin; the plugin is the self-contained module. | Shared modules would sit inside the unit. Recorded against the README's install question, which remains open. |
| D2 | Decision catalogue → blind round → seat-declared conflict scan → targeted response → resolution → procedural rendering. | Known decisions receive shared identifiers before seats run. Independence is preserved by *ordering* — each seat commits before seeing any other's. |
| D3 | The chair is procedural. It sorts; it does not rule. | A mediator with substantive power is a homogenizer in a neutral hat, and it touches the output last. |
| D4 | Distinctness is decided by the behavioral disagreement test. | A panel whose members cannot disagree burns N dispatches to produce one opinion. Reading proposes a distinction; a contrastive run must exercise it. |
| D5 | Known decision IDs are invocation data; novel decisions remain emergent. | Seats select shared IDs rather than minting them blindly. The mechanical backstop is deliberately incomplete for emergent findings. |
| D6 | Reader limits are protocol parameters enforced at seat submission. | The chair may neither paraphrase nor trim. Bounded claims protect the reader without giving the chair discretion. |

## A.2 Panel declaration is data, not inference

Skill selection must be inferential — the router cannot know in advance what will be asked. Seat
selection need not be: by the time a seat is needed a skill has already fired, so the task is
already classified. Inferring the panel pays for that classification twice, and the second payment
reintroduces the routing collision one level down.

The seat roster is therefore a table inside the convening `SKILL.md`, already in context when the
skill fires. This is what the three declared reviewer roles at `diss.md:323,349,373` do today.

Three declared escape hatches, in descending order of trust:

1. **Conditional seats** — `if the diff touches auth or crypto → add seat cso@security`.
2. **User-named** — `/astra-denounce --with karpathy`.
3. **Index lookup** — read only when the panel is genuinely open-ended. This is the path that can
   degrade, so it is the fallback, not the mechanism.

## A.3 Decision catalogue is invocation data

Seat selection classifies *who should speak*; it does not name the artifact-specific decisions they
discuss. Before the blind round, the convening skill creates a neutral decision catalogue from
explicit user questions and artifact anchors. If the artifact does not enumerate its decisions, an
evidence-only preflight extractor may identify targets and phrase neutral questions; it may not
recommend an answer.

Every seat receives the same catalogue and selects from it. Seats may still surface a novel decision
under a seat-scoped `emergent:<seat.id>:<n>` identifier. This preserves discovery outside the
catalogue while making the A.7 backstop operational for every catalogued decision.

## A.4 Interface sketch

```yaml
panel_invocation:
  id:          string
  artifact:    <path or ref>
  decisions:                         # non-empty, fixed before blind dispatch
    - id:      string
      target:  <file:line, section, diff hunk, or artifact ref>
      question: string               # neutral; contains no recommended stance
      source:  explicit_user | artifact_anchor | preflight_extractor
  seats:       [<seat.id>]
  limits:                            # resolved protocol values, not skill choices
    max_claims_per_seat:       6
    max_words_per_claim:       60
    max_words_per_final_position: 180
```

The three limits are provisional defaults. A skill may request a lower value, never higher. A
submission outside these limits is rejected back to its originating seat; the chair never truncates
it.

```yaml
seat:
  id:            string             # panel-unique, e.g. "eng@migration-plan"
  perspective:   <name>
  playbook:      <name>
  jurisdiction:
    artifact:    <path or ref>
    scope:       string
  constraints:
    requires:    [<playbook output>]
    forbidden_playbooks: [<name>]    # illegal combinations
```

`forbidden_playbooks` is what prevents illegal seats — most importantly, an evidence-only verifier
playbook may never be paired with a perspective, and the chair may never be paired with a
substantive playbook.

```yaml
claim:
  id:           string              # "<seat.id>.<n>"
  seat:         <seat.id>
  round:        1
  kind:         factual | normative
  decision_id:  string              # catalogue ID or "emergent:<seat.id>:<n>"
  position:     string              # one atomic assertion
  stance:
    target:     <file:line or artifact ref>
    disposition: accept | reject | rewrite | defer | block
  evidence:     [ { ref, quote } ]
```

`decision_id` + `stance` exist to make the mechanical backstop implementable. Without a structured
stance, "incompatible positions" is a semantic judgment, and only seats may make those. `kind`
determines routing: factual claims are resolvable by evidence, normative ones are not.

```yaml
challenge:
  challenger:   <seat.id>
  contests:     <claim.id>
  ground:       string              # one line, why it is contested
  kind:         factual | normative

verification:
  verifier:     verify-<domain>      # evidence-only, no perspective
  claims:       [<claim.id>]
  evidence:     [ { ref, quote } ]
  result:       supported | contradicted | indeterminate

final_position:
  seat:         <seat.id>
  revision:     integer             # 0 blind; 1 rebuttal; 2 post-verification
  status:       active | withdrawn
  text:         <string or null>
  supports:     [<claim.id>]
  supersedes:   <revision or null>
```

A challenge is not a rebuttal — it is a seat asserting that a conflict exists, the semantic judgment
the chair is forbidden from making. `verification.result` describes the evidence, never who wins.
The highest schema-valid revision is a seat's effective position; the chair never selects an excerpt,
because selection biases the result exactly as paraphrase does.

## A.5 Protocol

**Blind round.** Each seat receives perspective + playbook + jurisdiction + the neutral catalogue +
protocol limits, and nothing from any other seat. Independence is structural here.

**Conflict scan — seats declare, chair does not.** Each seat receives its own context again plus the
merged claim list, and returns **only** Challenge records. Anchoring is prevented by *ordering, not
blindness*: every seat's own claims are committed and immutable before it sees anyone else's.

**Targeted rebuttal.** Only seats involved in contested claims are re-dispatched, batched one
dispatch per seat. Claimant and challenger always remain in separate contexts. A seat with no
contested claim is never re-dispatched; its revision 0 becomes effective mechanically.

**Resolution.**

| Clash kind | Route |
|---|---|
| **Normative** | `AskUserQuestion` with every surviving side quoted verbatim |
| **Factual** | Verifier playbook; affected seats re-dispatched once to revise, withdraw, or retain |
| **Factual, indeterminate** | Rendered as explicit uncertainty, both sides quoted. Never silently resolved |

This matches the house norm already in place — `plan-ceo-review:874`, *"Present each
scope-expanding idea as an AskUserQuestion"*, and `:879`, *"In ALL modes, the user is 100% in
control."*

**Procedural rendering.** For each seat the chair reads the highest schema-valid `final_position`.
An `active` revision is copied verbatim; a `withdrawn` one is omitted. Revision number, schema
validity, and status are mechanical fields, so the chair makes no textual choice.

## A.6 Chair invariants

| # | Invariant |
|---|---|
| C1 | Every non-scaffold sentence in the final output appears **verbatim** in a speaker submission. |
| C2 | The chair emits zero claims of its own. |
| C3 | Scaffold text comes from a fixed, versioned allowlist. |
| C4 | Every rendered position is a seat-nominated `final_position` reproduced **whole** — never a substring. |
| C5 | Every seat's highest schema-valid `active` revision is rendered exactly once; withdrawn and superseded revisions zero times. |
| C6 | Attribution is preserved on every rendered block; ordering is deterministic. |
| C7 | Every unresolved clash renders **every** surviving side. |
| C8 | Every claim surviving to output traces to a round-1 claim ID. |
| C9 | Verification evidence may be added after round 1 but must link to existing claim IDs. An unrelated late claim restarts the claim cycle. |
| C10 | Every Claim and FinalPosition satisfies the invocation's count and word limits. An invalid submission returns to its seat; the chair never truncates it. |

C3 stops the chair smuggling substance in as connective tissue. C5 closes the gap in "every rendered
position was nominated," which permits dropping one. **The chair is not a perspective** — naming it
one invites exactly the substantive behavior C1–C10 forbid.

## A.7 Verifier playbooks and conflict detection

Factual verification runs through an **evidence-only playbook with no perspective attached**.
Routing a factual clash back through the claimant's perspective would inherit its confirmation
bias. **This already exists:** `diss.md:282-296` is a working evidence-only verifier — keyed on
`finding_id`, reporting `RESOLVED`/`PERSISTING`/`NEW` with `file:line` evidence, carrying no
perspective, and enforcing *"No evidence = no finding."* That line becomes the verifier playbook's
governing rule.

Three detection mechanisms:

1. **Seat-declared contest (primary).** Preserves standing. Fails when no seat notices a conflict
   outside its beat.
2. **Mechanical backstop.** Identical catalogued `decision_id` with incompatible
   `stance.disposition` triggers a conflict even if uncontested. Incompatible pairs:
   `accept`×`reject`, `accept`×`block`, `rewrite`×`accept`, `defer`×`block`. This compares enum
   values against a fixed table, so it does not violate C2. It deliberately ignores `emergent:*`
   identifiers, because deciding that two differently named novel findings mean the same thing
   would be a semantic judgment.
3. **Conformance fixtures (test time only).** Expected clashes live in fixtures, **never in runtime
   perspective content.** Runtime "disagrees with" blocks are rejected: they create pairwise
   coupling, go stale silently, and prime performative disagreement.

**Recorded limitation.** None of the three guarantees detection of a novel conflict. A conflict that
is novel, prose-only, and unnoticed by every seat **will pass silently.** This is a known and
accepted gap, not an oversight.

---

# Appendix B — Packaging proposals (historical, not applied)

> **Historical and superseded.** This appendix proposed amendments to `README.md` that were **never
> applied**. `docs/phase-0.md` section 8 defers packaging, and `docs/design-requirements.md`
> section 2 keeps the README authoritative as source inventory, so the README text these
> subsections proposed to replace still stands as written. Retained to record what was considered.

## B.1 Proposed replacement of Principles §2(a) — not applied

The README declares **skill-level** self-containment with a single carve-out for router discovery
(Principles, "2. Self-containment"). This proposed replacing it with **plugin-level**
self-containment: every astra implementation file inside the plugin, skills consuming declared
shared modules, nothing reaching outside the plugin.

**That replacement was not made.** The README's skill-level rule and its router exception remain the
active statement. The proposal's stated consequences would have been: the router exception
disappears into ordinary intra-plugin composition; MCP stops being a filesystem exception and
becomes an external runtime prerequisite; the `bin/` rule and "vendor it, never link out" apply at
the plugin boundary; and skills are no longer independently portable.

## B.2 Proposed closure of the install question — not applied

This answered "Should astra ship as a plugin?" with **yes**, accepting two costs as implementation
constraints: paths resolving through `${CLAUDE_PLUGIN_ROOT}` / `${CLAUDE_SKILL_DIR}` rather than
literals, and namespaced command names (`/astra:denounce`) that any later transcript mining would
have to match.

**The question remains open**, still listed under the README's open questions.

## B.3 Collision-map corrections — applied

Both corrections proposed for the adversarial-critique row hold in the current README:
`plan-eng-review` is retained as a distinct perspective, and `/trim` is retained pending its
behavioral-distinctness evidence. Cluster totals were unaffected — neither was ever proposed for
deletion, only for merger into another voice. The row now holds 16 after `devex-review` was added;
§5.5 accounts for it.

---

# Appendix C — Cost model and measurement protocol (historical)

> **Historical.** `docs/phase-0.md` section 8 defers telemetry, conformance harnesses, and runtime
> preservation fixtures, and `docs/design-requirements.md` section 7.9 requires the confirming
> behavior to be *recorded, not built* during phase 0. Retained as the
> implementation detail of what a later phase could measure; core §9 is authoritative. It
> authorizes no fixture, harness, or benchmark, and none of its constants are measurements. **The
> Linus-versus-Ramsay fixture is withdrawn by §5.1; the fixture slot is now `/diss` versus
> `review`.**

## C.1 Cost model

Use tokens, not source lines. Let `Pᵢ` = seat `i`'s perspective + playbook + jurisdiction +
catalogue + limits; `C` = average round-1 claim-set tokens per seat; `B` = distinct seats in
targeted response (`B ≤ N`, because dispatches batch); `F`/`V` = verifier dispatches and one
verifier's context; `A` = distinct seats re-dispatched after verification; `H`/`L` = chair context
and average effective final-position tokens; `X`, `Y` = targeted-clash and verification payloads.

| Phase | Approximate uncached input |
|---|---|
| Decision-catalogue preflight | one evidence-only extractor context, when the artifact does not enumerate decisions |
| Blind filing | `Σᵢ Pᵢ` |
| Conflict scan | `Σᵢ Pᵢ + N²C` |
| Targeted response | `Σᵢ∈B Pᵢ + X` |
| Factual verification and seat update | `F·V + Σᵢ∈A Pᵢ + Y` |
| Procedural rendering | `H + N·L` |

The conflict scan is therefore **`O(N·P + N²·C)`, not merely `O(N²·C)`**. A resumed agent does not
make `Pᵢ` disappear from model input; its prior context is replayed and billed unless the provider
reports it as cached. At the permitted `N = 2/4/6`, repeated perspective + playbook context is
expected to dominate the quadratic claim payload. The expensive axis at small N is the number of
**seat-bearing phases**.

**The 49% figure is withdrawn as a claim.** `autoplan` reading four skills is
1476 + 1514 + 1050 + 1460 = 5,500 source lines against an estimated ~2,800 under this design. That
is a source-line ratio, not a token measurement; it ignores per-subagent setup and every later
phase's replayed input.

## C.2 Measurement protocol

Cost measurement cannot establish that condensation preserved the voices or that combining them
improved the critique. Compare three systems on identical inputs:

| Label | System | What it isolates |
|---|---|---|
| **A** | Source oracle selected before outputs are seen | Best applicable original quality |
| **B** | Reference convener using unchanged originals | Routing and coordination value |
| **C** | Self-contained candidate | Internalization fidelity |

`autoplan` may serve as A or as existing-convener evidence for plan cases. It is not a universal
baseline for diffs, API specs, IaC, running artifacts, prompts, or CLAUDE.md.

**Source characterization.** For each candidate pair with overlapping standing, build at least
three fixed, versioned artifacts with fixture-supplied decision IDs and targets, including one
expected-divergence case and one expected-convergence control. Run each original blind on
identical artifact + evidence + catalogue, three times, under a wrapper that adds only output
schema and protocol limits — no perspective text, expected answer, or pair identity. A
divergence passes when incompatible `stance.disposition` values on the same decision and target
appear in at least two of three runs; a convergence control passes when manufactured
incompatibility does not. No observed disagreement makes two voices candidates for merger; it
never proves equivalence.

**Three-way quality comparison.** Run A, B, and C on the fixed corpus with three-run repetition.
For panels at **N = 2, 4, 6**, use nested versioned rosters so the marginal-seat measurement does
not silently change composition. A blinded evaluator receives de-identified, order-randomized
outputs and the fixture rubric, scoring recall of seeded decisions, supported-claim precision,
unsupported-claim rate, source-unique supported findings, informative-conflict yield,
actionability, duplicate/noise load, and reader load.

B and C must first meet the home-jurisdiction non-regression floor against A. They must then
demonstrate §9's positive cross-jurisdiction advantage. C must additionally preserve B's
characterized divergences, convergence controls, source-unique supported findings, authority,
and degradation behavior. If B fails, reject or narrow the panel before extraction. If B passes
and C fails, rework internalization and keep the originals. `Decisions surfaced` is a diagnostic
count, not a quality metric.

For every dispatch, record phase, seat, fresh/resumed status, uncached input tokens, cache
read/write tokens, output tokens, and wall-clock. The cost claims to defend are **marginal cost per
seat**, **marginal cost per seat-bearing phase**, and total cost at the declared cap.

## C.3 Panel-size cap

A default cap is considered only if the panel passes §9, then set from C.2 results. The historical
provisional default is **4 seats**, escalating to 6 only where the artifact warrants and the user
opts in. The cap is a protocol parameter, not a per-skill choice, so it cannot drift upward one
skill at a time.
