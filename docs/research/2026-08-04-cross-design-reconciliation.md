# Cross-design reconciliation — initial public tranche

**Date:** 2026-08-04
**Scope:** the eight designs of the initial public tranche, reconciled pairwise per
`docs/phase-0.md` section 7 step 4
**Status:** research report; proposes, applies nothing

---

## 1. Scope and authority

This pass reconciles the eight drafted designs of the initial public tranche —
[`astra-critique`](../../designs/astra-critique.md) (reviewed baseline),
[`astra-understand-code`](../../designs/astra-understand-code.md),
[`astra-spec`](../../designs/astra-spec.md), [`astra-plan`](../../designs/astra-plan.md),
[`astra-implement`](../../designs/astra-implement.md), [`astra-test`](../../designs/astra-test.md),
[`astra-debug`](../../designs/astra-debug.md), and [`astra-ship`](../../designs/astra-ship.md) —
against each other, against `docs/design-requirements.md` (notably section 7.7), against
`docs/design-roadmap.md` (notably sections 3.2, 5, and 12), and against the authoritative state in
`docs/phase-0-ledgers.md`.

**What was read.** All four governing documents in full; all eight tranche designs in full;
`designs/astra-product-design.md` only where a tranche design references it (amendment 4's
generated-source and self-containment rules). Git history was consulted to establish drafting
order: Critique (reviewed, 2026-07-31) → Understand Code and Test (2026-08-03) → Spec, Plan,
Implement, Ship, Debug (2026-08-04, in that order of last edit; Implement was revised on
2026-08-04 against four completed peers). Debug is the only design written with all seven others
available (**O**, file history and each design's own §10 inspection statements).

**What this pass may not and does not do.** It edits no design, no governance document, and —
per the standing header of `docs/phase-0-ledgers.md`, whose named coordinator has not been
handed off — no ledger row. It marks no row `resolved`: that state is reserved by the ledger's
own vocabulary for reconciliation *after the user's review*, and **none of the seven drafted
designs has been user-reviewed**. It installs, disables, retires, and declares
retirement-eligible nothing. Every proposal in sections 4 and 5 is exactly that — a proposal for
the phase-0 coordinator, with every collision row proposed `claimed`, never `resolved`.

**What this report reconciles.** Unreviewed drafts. A drafted design's conclusions are
"proposals with evidence, not accepted contracts" (roadmap §1, the **Drafted; awaiting review**
state). Where two drafts genuinely conflict on a normative question, section 6 escalates the
choice; this report does not resolve such conflicts by precedence.

**Evidence labels.** **O** = observed in an inspected artifact of this repository; **I** =
inferred; **U** = unavailable. Line anchors into `designs/astra-critique.md` were re-verified
against the working tree on 2026-08-04 (**O**).

**Baseline state confirmed (O).** `docs/phase-0-ledgers.md` is unchanged since amendment 4:
0 resolved, 63 claimed, 116 unclaimed collision rows. None of the seven drafted designs' ledger
proposals has been applied; rows the designs inspected in depth (`cm-plan-and-spec-01`,
`cm-ship-and-vcs-01`, `cm-testing-01`, `cm-debug-and-incident-01` among them) still read
"Pending source inspection."

---

## 2. Findings, ordered by severity

Classification vocabulary: **contract mismatch** (both sides wrote the seam and disagree),
**one-sided row** (one side wrote it, the other is silent), **ownership conflict**, **trigger
collision**, **factual inconsistency**, **gap** (silence, not disagreement).

### F1 — HIGH · The "plan-required" remediation route has no receiving contract

**Classification:** contract mismatch / routing gap.
**Anchors:** `designs/astra-implement.md` §7.4 ↔ `designs/astra-plan.md` §7.2 and §§2.1, 2.4,
2.5; `docs/design-roadmap.md` §3.2 (Implement row).

Implement's Critique profile routes any code-defect finding without an approved plan to Plan:

> "`plan-required` and `unknown` route to `astra-plan`, not here. Implement does not improvise
> the remedy, and a capsule alone never becomes mutation authority." (astra-implement §7.4,
> rule 4)

The roadmap's coverage row says the same: "Accepted only with an approved bounded remediation
plan attached; otherwise Plan is the destination" (roadmap §3.2). But Plan's declared handoff
class cannot receive that route. Plan owns `execution-plan-defect`, and its destination payload
presupposes a plan that already exists:

> "`plan_lifecycle_state: draft-before-approval | approved-not-started | approved-in-progress`"
> (astra-plan §7.2)

A known-cause code defect with no plan is none of these. Nor can the finding enter Plan through
its ordinary intake: "The trigger is not the word 'plan'; it is the combination of an accepted
Spec, available implementation evidence, and a request for an executable work artifact"
(astra-plan §2.1), and the §2.4 gate requires a whole-revision-accepted Spec. Plan's only other
inbound diagnosis path is titled and scoped as "**Accepted Debug evidence** … optional only for
a repair-plan request" (astra-plan §2.5) — a Critique finding is not Debug evidence, and Debug's
own class excludes findings whose cause Critique already established ("A finding that Critique
itself explained causally is not this class — it routes to Implement", astra-debug §7.3 rule 6).

**Consequence if shipped unfixed:** the most common review outcome — "this code is defective,
cause explained, no remediation plan exists" — has a declared destination (Plan) whose contract
rejects it at every entrance. Critique is forbidden to redirect to an unrelated peer or invent a
payload, so at runtime the route dies as a permanent "reconciliation gap" even though every
participant designed in good faith. **O** on all quoted contracts; the dead-end itself is **I**
(composition of the three contracts).

**Recommended resolution:** a user decision (section 6, D1) between (a) Plan generalizing its
§2.5 inbound diagnosis contract from "Accepted Debug evidence" to "accepted diagnosis evidence"
that a user-accepted Critique finding can satisfy, with the same acceptance requirements; or
(b) Plan adding a second conditional handoff sub-class (e.g. `remediation-plan-request`) with a
payload of its own. Option (a) is the smaller change and touches no handoff machinery; the
evidence for it is that Plan's §2.5 already demands exactly the fields a surviving Critique
finding carries (cause, evidence, affected contract, constraint) plus user acceptance.

### F2 — HIGH · Confirmed: Critique still names `astra-presentation` as a destination

**Classification:** factual inconsistency (design vs. roster), known defect confirmed and
scoped.
**Anchors:** `designs/astra-critique.md:588` and `:764` ↔ `docs/design-roadmap.md` §10.2
(amendment 3 fold) and §3.2 (re-targeted row).

Confirmed at exactly two anchors (**O**, re-verified against the working tree):

> line 588: "| `astra-presentation` | Audience, observed narrative or data-comprehension
> problem, affected slides or sections, and supporting evidence |"
>
> line 764: "…`astra-interface`, `astra-brand`, and `astra-presentation`; non-Design problems in
> code, …" (inside §9.2's handoff-routing corpus)

Amendment 3 folded `astra-presentation` into `astra-interface` on the user's decision
(roster 25 → 24); roadmap §3.2 re-targeted the narrative/data-comprehension class to Interface,
which therefore owns **two** seeded classes and "must give each a separately named payload or
narrow one." No other occurrence of the stale name exists in the Critique design (**O**, full
grep). Roadmap amendment 3 §10.6 and the Wave 3 revision row assign the correction to the
**Critique source-expansion revision, which has not started**.

**Consequence if shipped unfixed:** Critique's first-tranche destination table and its routing
corpus both name a peer that does not exist; a narrative-problem capsule would target a ghost,
and the corpus would validate routing against a roster the user already rejected.
**Resolution:** recorded, not fixed, per the roadmap's assignment. Section 5's draft amendment
adds this report as a second pointer so the revision cannot miss the §9.2 corpus anchor, which
amendment 3 did not cite.

### F3 — HIGH · `staging-debug` ownership: hold the move to `astra-deploy`, pending Deploy

**Classification:** ownership conflict (trigger surface vs. effect surface), known conflict
assessed as instructed.
**Anchors:** `designs/astra-debug.md` §3.4 (both the argument and its recorded counter-argument)
↔ `docs/design-roadmap.md` §5.8 (original allocation) and Wave 4 `astra-deploy` row
(amendment 5's inbound-claim note).

Debug proposes moving `cm-debug-and-incident-07` from `astra-debug` (roadmap §5.8) to
`astra-deploy` as coordinating primary home, retaining a Debug secondary for the diagnosis
slice. The evidence in §3.4 (**O**): Steps 2, 3, and 8 "build a Docker image, push it to ECR
account 471112919450, `helmfile apply` to a shared staging EKS cluster, and later restore that
cluster to `latest`"; Step 4 delegates to `/local-debug`; Step 7 delegates to `/pr`; only Steps
5–6 are diagnosis. Every irreversible effect in the source is a shared-environment deployment
effect. The counter-argument is recorded in the same section: "the source's **name and every one
of its five triggers are debug-shaped** ('staging test failing', 'fix staging', 'debug
staging'), and its user job begins with a failing test."

**Assessment: the move should hold, as a `claimed` proposal, pending Deploy.** Three
independent lines of evidence support it. First, roadmap §6.1's third triage question — does the
label match the body? — was written for exactly this case, and the body is a deployment
pipeline (**O**). Second, amendment 3 §10.5 established the precedent that a decomposing
umbrella takes a *coordinating* primary home holding the largest coherent share; here that is
the effect surface, and the authority risk (cluster mutation) sits entirely on Deploy's side.
Third, the move is now **not an isolated claim**: `astra-ship` independently re-triages
`changelog` (`cm-ship-and-vcs-12`) toward `astra-deploy` for the same reason (deployment
runbooks, astra-ship §3.3), so two tranche designs converge on Deploy as the home for
deployment-effect sources. Reverting to Debug would put a source whose only irreversible
effects are deployments inside a peer that pledges "Debug performs no image build, registry
push, `helmfile apply`, or environment restore under any circumstances" (astra-debug §7.2) —
an allocation the owning design itself could never internalize.

Because `claimed` reserves disposition ownership without approving it, applying the row now
loses nothing: if the future Deploy design declines, the roadmap Wave 4 row already prescribes
the fallback — "the source stays independent and the ledger must say so rather than leaving it
`unassigned`." The trigger surface is handled under F6/D-3: "fix staging" / "debug staging"
phrasings route by *effect intent* (deploy-and-retest → Deploy; explain-the-difference →
Debug), and Debug's own trigger claims only "it works locally but fails in staging — a
*difference* question, not a deployment request" (astra-debug §7.4).

### F4 — MEDIUM · Debug's field-for-field mapping onto Plan omits `diagnosis acceptance`

**Classification:** contract mismatch (payload).
**Anchors:** `designs/astra-debug.md` header + §7.2 (Plan row) + §2.4 ↔
`designs/astra-plan.md` §7.1 (Debug row) + §2.5.

Debug claims: "Section 2.4 defines that artifact and section 7.2 maps it field for field onto
Plan's, Implement's, Test's, and Spec's inbound rows" (astra-debug, header), and its Plan row
sends "`cause` with its certainty label, `evidence`, affected contract or path set,
`scope_exceeded`, remediation constraints, and unresolved uncertainty — mapping onto Plan's six
named fields." Plan's six named fields are:

> "Cause, evidence, affected contract, remediation constraint, **diagnosis acceptance**,
> unresolved uncertainty." (astra-plan §7.1)

and Plan §2.5 makes the sixth one load-bearing: accepted Debug evidence "must identify the
diagnosed cause, evidence, affected contract, remediation constraint, and **user acceptance of
the diagnosis**." The Debug Report (astra-debug §2.4) has no acceptance field — acceptance
happens as a user act in conversation ("User accepts a diagnosis, then separately starts repair
planning") — and `scope_exceeded` maps onto none of Plan's six. Five of six fields map; the
mapping claim overstates.

**Consequence if shipped unfixed:** Plan's whole intake philosophy is machine-visible,
non-inferred acceptance (its §2.4 gate, mirrored from Spec's `approval.decision_ref`). Handed a
Debug Report with no acceptance record, a faithful Plan implementation must either block or
infer acceptance from conversation — the exact inference Plan forbids itself elsewhere.
**Recommended resolution:** coordinator-level, no user ruling needed: add one optional field to
the Debug Report spine (e.g. `acceptance_ref`, populated when the user has accepted the
diagnosis, `null` otherwise), mirroring Spec's `approval.decision_ref` pattern; Plan validates
it at intake. Alternative — Plan records acceptance at its own intake — is workable but breaks
the symmetry Plan itself established with Spec's artifact-carried acceptance.

### F5 — MEDIUM · Verification of Debug §7.2's six "accepted as written" claims

**Classification:** acceptance-claim drift (two rows quote the peer's payload incompletely; one
overstates; three are faithful).
**Anchors:** `designs/astra-debug.md` §7.2 ↔ each peer's row, cited per line below.

Debug states: "All six rows written without a Debug contract are **accepted as written**, with
two narrowings this design owns and states plainly." Checked against the peers' actual text:

| Peer row | Peer's payload text (O) | Debug's restatement (O) | Verdict |
|---|---|---|---|
| `astra-ship` §7.2 | "Failing command and output, revision and base, environment, what was and was not published, and the exact effect boundary reached" | identical | **Faithful, verbatim** |
| `astra-spec` §7.3 | "Debug evidence ref, affected requirement/criterion IDs if known, observed-versus-expected distinction, certainty" | trivially reworded, no element added or dropped | **Faithful** |
| `astra-implement` §7.2 | "Failing command and reproduction, relevant logs, last-known-good state, worktree/base, attempted in-scope fixes, and mutation constraints" | trivially reworded, no element dropped; narrowing 2 (Debug may already have applied the in-scope fix) is stated and compatible | **Faithful, narrowing stated** |
| `astra-test` §7.3 | "Failing command/cwd/snapshot; full relevant logs; deterministic/non-deterministic note; environment; last-known-good; **attempts limited to test scope**" | omits "attempts limited to test scope"; outbound direction widened with the "no correct seam" finding — the stated narrowing 1 (in fact a widening) | **Drift: one element unquoted.** Substantively covered by Debug §2.3 item 6 (prior attempts are intake), but the coordinator's canonical snapshot must carry Test's text, not Debug's summary |
| `astra-understand-code` §7.2 | "**Reproduction context if supplied**, entry point, ordered trace, state/effect edges, suspected-but-unproven gaps, revision" | omits "Reproduction context if supplied" while claiming the row is accepted "as Understand's §7.2 row states it" | **Drift: one element unquoted.** Substantively covered by Debug §2.3 item 3 |
| `astra-plan` §7.1 | six named fields including "diagnosis acceptance" | five of six mapped; `scope_exceeded` extra; see F4 | **Overstated** — F4 |

**Consequence if shipped unfixed:** none of the drifts changes behavior today, but roadmap §3.2
and requirements §7.7 make the coordinator's reconciled snapshot the canonical contract; if that
snapshot is built from Debug's summaries rather than the peers' rows, two payload elements
silently disappear and one required element is missing. **Resolution:** the coordinator
reconciles from the peer-owned rows (the owning design is authoritative for its side), treating
Debug's §7.2 as acceptance evidence only; F4's field addition closes the one real mismatch.

### F6 — MEDIUM · "root cause analysis": adopt context-conditional routing, provisionally

**Classification:** trigger collision (known collision 1; recommendation, not rediscovery).
**Anchors:** `designs/astra-debug.md` §7.4 ("root cause analysis" row, line 1008) and §10.5 Q1
↔ `docs/phase-0-ledgers.md` rows `cm-debug-and-incident-04`/`-05` (`rca`, `firefighting` →
`astra-incident`, `claimed`) and `docs/design-roadmap.md` §5.8 / amendment 1.

Both holders have standing: `rca` is claimed for the unwritten `astra-incident` (applied,
amendment 1), and the phrase is a declared trigger of `investigate`, a Debug source. Debug's own
position: "Incident's jurisdiction during a live incident … Outside an incident, Debug. The two
designs must reconcile this string explicitly; it is the sharpest remaining collision in the
neighborhood" (astra-debug §7.4).

**Recommendation:** adopt Debug's context rule **provisionally**: route on outage context, not
on the bare string. Live-incident signals (an ongoing outage, paging/alerting language,
"production is down") → Incident, whose `rca` runs as the parallel causal session amendment 1
characterized; absent those signals → Debug. The bare string "root cause analysis" must not be
a router key by itself. This is provisional because `astra-incident` is unwritten and is the
only party that can accept the rule; the draft amendment in section 5 records the rule as
Debug-side-proposed, and the Incident design must confirm or amend it. Evidence for the rule:
amendment 1's own characterization ("`rca` runs as a separate agent session in parallel and
declines to suggest stabilization") ties `rca` to a concurrent-outage context; Debug's job has
"no outage clock" (astra-debug §4.4). The two readings partition cleanly on that fact.

### F7 — MEDIUM · `local-debug`'s BDD-execution slice: Test's side is silent; recommend acceptance

**Classification:** one-sided row (secondary role proposed onto a silent peer); known
collision 2.
**Anchors:** `designs/astra-debug.md` §3.4 (row `cm-debug-and-incident-08`) and §10.5 Q2 ↔
`designs/astra-test.md` (entire — the source appears nowhere in it, **O**).

Debug assigns `astra-test` a secondary role on `local-debug` ("Steps 1–3 BDD execution") and
routes bare test-execution triggers ("run feature tests", "run BDD tests", "behave") to Test's
jurisdiction (astra-debug §7.4). Test, drafted a day earlier, never mentions `local-debug`; its
own §10.4 Q9 anticipated exactly this: "no absent peer contract is treated as implemented."
Debug is candid about the gap: "Test's design predates this inspection and does not list the
source. Consequence: if Test declines, BDD pipeline execution has no owner and `local-debug`
cannot be retired" (astra-debug §10.5 Q2).

**Recommendation:** Test should accept the secondary role. The slice sits squarely inside
Test's declared triggers ("Run these tests," "do the tests pass at this revision?", and its
`bdd` jurisdiction covering Behave execution against live environments), and Debug's split
follows the source's own boundary marker (Step 4: "This is where AI provides the most value").
Because Test is a drafted, unreviewed document, the acceptance does not require redrafting: the
coordinator can record Test-side acceptance the same way Implement's §3.4 recorded responses to
peer-claimed roles — as an explicit acceptance entry against the peer-owned row — and Test's
next revision should mirror it. Until then the ledger row carries the secondary as
Debug-proposed, Test-unconfirmed (section 4 marks it so).

### F8 — MEDIUM · One-sided secondary roles onto silent or future owners, and one dangling applied secondary

**Classification:** one-sided rows / gap.
**Anchors:** listed per item.

The tranche leaves a set of secondary-role assertions whose named counterparty has not
responded. None is a contradiction; all must be visible at reconciliation:

1. **Onto Critique (pending its source-expansion revision):**
   `cm-testing-04` `spock` — "astra-critique: implementation-quality judgment and score/refusal"
   (astra-test §3.3); `cm-codebase-comprehension-01`/`-04` — the `how` critic lenses and the
   `improve-codebase-architecture` adversarial-review role (astra-understand-code §3.4);
   `cm-ship-and-vcs-01`/`-06` — `ship`'s "pre-landing review army" and `/pr`'s `diss` gate as
   independent judgment (astra-ship §3.4). All compatible with Critique's jurisdiction; none
   consumed by the Critique design, which predates them. These form the source-expansion
   revision's inbound work list.
2. **Onto the unwritten `astra-deploy`:** `staging-debug` (F3) and `changelog`
   (`cm-ship-and-vcs-12`, astra-ship §3.3). Two independent inbound claims now; the Deploy
   design must accept or decline both.
3. **Onto the unwritten `astra-document`:** `document-release` (`cm-ship-and-vcs-13`,
   astra-ship §3.3) and `changelog`'s alternate home.
4. **Onto Test (silent):** F7's `local-debug` slice, plus `cm-debug-and-incident-03` —
   "astra-test (defers failing-test authoring to `superpowers:test-driven-development`)"
   (astra-debug §3.4). Same treatment as F7.
5. **Dangling applied secondary:** the ledger's `cm-adversarial-critique-09` (`/trim`) carries
   "Plan & spec: prompt or skill remediation" (**O**, ledger line 46) — applied from Critique's
   §3.3. All three Plan-&-spec-derived designs have now been drafted, and **none claims prompt,
   `SKILL.md`, or CLAUDE.md remediation** (Spec's non-goals exclude project mutation; Plan's
   core has zero write authority; Implement mutates only what an approved plan names — the file
   class is never claimed as a jurisdiction). The secondary role points at a neighborhood that
   produced no owner for it. This connects to open owner E2: the pointer should be re-aimed
   (Skill Design and Document are the roadmap's candidates) or explicitly kept open; leaving it
   as "Plan & spec" now misdirects the reader to designs that refuse it.

### F9 — MEDIUM · Free-text destination-payload fields risk restating Critique's envelope

**Classification:** contract mismatch (payload discipline), design-quality.
**Anchors:** `designs/astra-understand-code.md` §7.3 and `designs/astra-debug.md` §7.3 ↔
`designs/astra-critique.md` §6 (envelope) and `designs/astra-implement.md` §7.4 (the corrective
precedent); `designs/astra-test.md` §7.3 (the guarded pattern).

Critique's common envelope already carries `problem_statement` — "Concise statement of what is
wrong or uncertain, without a proposed remedy" (astra-critique §6). Two destination payloads add
a free-text field whose content is hard to distinguish from it:

- Understand Code: `analysis_question` — "the unresolved existing-system or technical-design
  question, phrased without a remedy";
- Debug: `observed_behavior` — "The wrong behavior as observed, separated from any suspicion
  about its cause."

Implement's 2026-08-04 correction removed six fields from its own payload for exactly this
duplication class ("`expected_behavior` is precisely a success criterion", astra-implement
§7.4), and Test's `proof_obligation` shows the guarded pattern: "reference the common-envelope
problem/evidence rather than restating it" (astra-test §7.3). Two smaller asymmetries in the
same family: Understand Code's `requested_mode` lacks the `unknown` escape Test gives
`required_test_mode` ("`unknown` when Critique cannot classify it without prescribing Test's
solution"), so Critique could be forced to choose a destination workflow depth it has no basis
to choose; and no payload was found to smuggle a solution, remedy, or suspected cause — Debug's
rule 3 explicitly quarantines a supplied suspicion, which is the strongest anti-smuggling
clause in the set (**O**).

**Consequence if shipped unfixed:** duplicated problem text can diverge from the envelope's,
and the destination then owns a second, unreconciled problem statement. **Recommendation:**
coordinator normalizes both fields to the reference-not-restate convention (or to
classification enums), and adds an `unknown` value to `requested_mode`, when recording the
canonical profiles. No user ruling needed.

### F10 — MEDIUM · `triage` has lost its designated decider

**Classification:** gap (ownership decision unassigned).
**Anchors:** `docs/phase-0-ledgers.md` row `cm-debug-and-incident-09` and
`docs/design-roadmap.md` §5.8 / amendment 1 §8.4 ↔ `designs/astra-ship.md` (entire — the skill
appears nowhere in it, **O**, grep verified) and `designs/astra-debug.md` §3.6.

Amendment 1 relocated `triage` out of Debug & incident and named its candidate homes:
"`astra-ship` on `github` and `/pr` adjacency, or retained independent; the relevant designs
decide." The Ship design — the named candidate — decides nothing: it never mentions the source.
Debug records only "Debug does not claim it and has no view on Ship-versus-independent"
(astra-debug §3.6). With the tranche complete, the row sits `claimed` with "relocation pending"
and no drafted design left that owns the question.

**Consequence:** the row cannot progress at final reconciliation; acceptance criterion 4 (one
primary disposition per occurrence) will fail on it by default. **Recommendation:** put the
decision to the user directly (section 6, D5) rather than re-opening Ship: the evidence
amendment 1 gathered (issue-tracker state machine, `disable-model-invocation: true`, zero
context cost when retained) already supports **retained independent** as the default, and
nothing in Ship's thirteen-source analysis pulls it in.

### F11 — LOW · Plan's recorded Implement snapshot is stale

**Classification:** factual inconsistency (anchor drift), self-detecting.
**Anchors:** `designs/astra-plan.md` §10.1 (peer-snapshot hashes) ↔ current
`designs/astra-implement.md` bytes.

Plan recorded snapshot hashes for the five peer drafts it reconciled against and stated the
rule "a hash change requires relation reconciliation before implementation." Verified
2026-08-04 (**O**): Spec `6ec61e19…`, Understand Code `152143af…`, Test `59525a1d…`, Critique
`2fc22bad…` all still match; **Implement does not** — Plan recorded `2aac0600…`, the file is now
`b087c479…`, changed by Implement's 2026-08-04 peer-reconciliation revision. The drift is
benign in direction (the revision *adopted* Plan's schema and answered Plan's blocking question
2) but the anchor is formally stale, and Debug — which makes the tranche's strongest
acceptance claims — recorded **no** peer-snapshot hashes at all, so its §7.2 acceptances have
no equivalent staleness check. **Recommendation:** the coordinator re-verifies Plan §10.1
against current bytes when applying ledger changes, and future cross-design acceptance claims
follow Plan's snapshot-hash practice.

### F12 — LOW · Critique's chassis table still rests on generated-output byte identity

**Classification:** factual inconsistency (evidence class), pre-dating amendment 4.
**Anchors:** `designs/astra-critique.md` §4 (table, lines ~205–217) ↔
`docs/design-roadmap.md` §11.2 (amendment 4).

Critique's collision analysis presents "Identical to `plan-ceo-review`" line counts
(995/991/979/959/915/841) and "The `## Voice` block is byte-identical across all seven" —
measurements over live `SKILL.md` files that, for gstack sources, are generated outputs.
Amendment 4 later established that generated gstack bytes "cannot be the sole source oracle or
merger advantage" and withdrew this evidence class in five other pairs. Critique does not hang
its advantage claim on these counts (its declared advantage is cross-jurisdiction conflict
surfacing, and it separately disclaims maintenance advantages as quality evidence), so nothing
load-bearing collapses — but the table is the same class of evidence every post-amendment-4
design now labels "provenance, not merger evidence" (e.g. astra-debug §3.2). **Resolution:**
assign to the Critique source-expansion revision alongside F2: re-derive the chassis/persona
split from authored templates and resolver sources, or relabel the table as generated-output
measurements.

### F13 — LOW · Understand Code ↔ Test: payload field lists do not line up

**Classification:** contract mismatch (minor, payload wording).
**Anchors:** `designs/astra-understand-code.md` §7.2 (Test row) ↔ `designs/astra-test.md` §7.3
(Understand Code row).

Understand Code's stated minimum payload to Test: "Behavior flow, current test locations,
observable interfaces, dependencies/adapters, known edge cases and gaps." Test's stated minimum
from Understand Code: "Artifact snapshot; relevant paths/symbols; observed interfaces/invariants;
uncertainty; accepted architecture constraints." The receiving side requires two elements the
emitting side never names — an **artifact snapshot** (revision) and **accepted architecture
constraints** — while the emitting side offers two the receiver never asks for (test locations,
dependencies/adapters; harmless extras). Understand Code's other rows all carry
"repository/revision"; this one alone omits it. **Consequence:** a faithful Understand packet
could arrive without the snapshot Test needs to bind evidence to a revision — Test would stop
("Test proceeds only when the contract and seams are independently clear; otherwise stop"), a
safe but avoidable failure. **Resolution:** coordinator-level: add revision and
accepted-constraint fields to Understand Code's Test-row payload; no user ruling needed.

### F14 — LOW · Spec ↔ Test: "unresolved decisions" and "acceptance examples" vs. Spec's row wording

**Classification:** gap (minor, payload wording), not a mismatch.
**Anchors:** `designs/astra-test.md` §7.3 (Spec row) ↔ `designs/astra-spec.md` §7.3 (Test row)
and §2.5.

Test's required inbound minimum: "Spec/OpenAPI ID and version; acceptance examples;
required/forbidden behavior; unresolved decisions; compatibility constraints." Spec's stated
outbound minimum names "accepted `spec_id`/`revision`, criterion IDs and expected behavior."
The full Accepted Specification artifact carries everything Test asks for
(`readiness.nonblocking_question_ids`, `behavior.negative_cases`, `scope.constraints` — **O**,
astra-spec §2.5), so this is a wording gap in the row, not a missing capability. **Resolution:**
coordinator aligns Spec's row text to name the artifact sections that satisfy Test's five
elements, so neither side under-reads the other at reconciliation.

### F15 — LOW · `effort: xhigh`: Debug's "never interpreted" claim contradicts Critique

**Classification:** factual inconsistency.
**Anchors:** `designs/astra-debug.md` §10.3 ↔ `designs/astra-critique.md` §5.8.

Debug: "`effort: xhigh` appears in two sources and is not a field this repository's documents
have interpreted anywhere … its runtime meaning is **U**." Critique's §5.8 interprets it, as an
authority field that must survive: "`effort: xhigh` ×2 — `diss-infra`, `diss-claudemd`
frontmatter — A reasoning-effort override cannot be reproduced by instruction text." (Test also
records `effort: high`/`xhigh` declarations without interpretation.) Debug's *caution* is the
better epistemics — no design has runtime evidence of the field's effect — but its factual
claim that no repository document interprets the field is wrong. **Resolution:** harmonize on
Critique's framing downgraded to Debug's certainty: "declared reasoning-effort override, runtime
effect unverified (**I**)," in both designs' next revisions.

### F16 — LOW · `codebase-design` consumption: three designs, three conventions

**Classification:** factual inconsistency (ledger-practice), minor.
**Anchors:** `designs/astra-debug.md` §3.5 ↔ `designs/astra-plan.md` §3.4; also
`designs/astra-spec.md` §10.1.

Three tranche designs use the `codebase-design` vocabulary in their prose. Plan explicitly
declines a consumer entry: "…supplies the document's architectural vocabulary but is neither a
future runtime dependency nor an occurrence in the assigned phase-0 reference ledger, so this
design does not invent a `consuming_designs` row for it." Spec uses the vocabulary (§10.1
credits the source for it) and proposes nothing. Debug proposes adding itself, "matching the
usage `astra-plan` already established" — citing as precedent the design that declined. The
inconsistency is conventional, not substantive: Debug's claimed consumption (its §6.5 scope
boundary is *specified in terms of* seam/depth) is arguably closer to a real reference relation
than Plan's drafting-vocabulary use. **Resolution:** coordinator adopts an explicit rule —
`consuming_designs` records designs whose *proposed runtime behavior* reads the reference;
drafting-time vocabulary use does not qualify — then applies Debug's addition only if its
runtime candidate genuinely consults the reference (its §7.1 lists it among components that
"remain separate," which supports acceptance).

### F17 — LOW · Merge-conflict resolution outside the landing flow is claimed by no one

**Classification:** trigger gap.
**Anchors:** `designs/astra-ship.md` §2.1 ↔ `designs/astra-implement.md` §§2.1–2.2 (silence).

Ship claims conflicts only conditionally: "Resolve the conflicts from merging the base branch
into this feature branch, **when the merge is part of preparing this change-set to land**." The
source `resolving-merge-conflicts` (claimed primary by Ship) is a general-purpose conflict
skill. A user mid-implementation who syncs their base branch and hits conflicts — "resolve
these merge conflicts," no landing intent — phrases a plausible request no tranche design
claims: Implement's intake requires an approved plan task, Ship's trigger requires landing
context. **Consequence:** minor; the manual bridge (invoking the source directly) survives.
**Resolution:** record in the roster-wide trigger table that Ship's conflict mode is the owner
for conflict-resolution requests regardless of landing intent, or explicitly leave non-landing
conflicts to the retained source until reviewed. Flagged for the Ship review rather than
escalated.

### F18 — LOW · Recorded for completeness: Spec's row overstates Plan's "approval" ownership; both sides already agree

**Classification:** contract mismatch (wording only), already self-flagged.
**Anchors:** `designs/astra-spec.md` §7.3 ("R: Plan owns executable decomposition and planning
approval") ↔ `designs/astra-plan.md` §10.4 Q1 ("must … be normalized to mean that Plan carries
and presents the gate; **only the user owns the approval decision**") and §1 ("`astra-plan`
never infers approval…").

No behavioral disagreement exists — Spec's own §2.7 gives every acceptance decision to the
user — but the row text, read alone, hands Plan an authority both designs deny it. The
coordinator's snapshot should carry Plan's normalized wording.

---

## 3. Pair matrix — all 28 bilateral pairs

Legend: **agreed** — both sides wrote the seam and the texts reconcile (notes list residual
minor items); **agreed·** — agreed with a finding attached; **mismatched** — both sides wrote it
and the texts do not reconcile (all mismatches found are minor and repairable);
**one-sided** — only one side wrote a row (for Critique pairs: the destination design declares
the profile; Critique's reviewed baseline predates all seven and its side lives in the generic
envelope contract plus roadmap §3.2, so these are structurally one-sided until the Critique
source-expansion revision consumes them); **absent** — neither side wrote a row (none).

| # | Pair | Status | Notes |
|---:|---|---|---|
| 1 | Critique–Understand Code | one-sided (compatible) | `yes` / `architecture-or-technical-design` declared; fits the envelope; F9 (`analysis_question`, `requested_mode`); `how`-critics secondary awaits Critique revision (F8.1) |
| 2 | Critique–Spec | one-sided (compatible) | `yes` / `specification-gap-or-ambiguity`; two-field payload is the cleanest in the set; matches roadmap §3.2 |
| 3 | Critique–Plan | one-sided (compatible) | `conditional` / `execution-plan-defect`; F1 interacts (the class cannot receive "plan-required" remediation routes) |
| 4 | Critique–Implement | one-sided (compatible) | `conditional` / `approved-code-remediation`; payload self-corrected 2026-08-04 from nine fields to three, citing Critique's problem/solution boundary — the model correction of the tranche |
| 5 | Critique–Test | one-sided (compatible) | `yes` / `test-evidence-gap`; `proof_shape`/`required_test_mode` are borderline-prescriptive but explicitly self-guarded |
| 6 | Critique–Debug | one-sided (compatible; new class) | `conditional` / `unexplained-failure` — class did not exist in Critique's design or (pre-amendment-5) roadmap; boundary table against five sibling classes is explicit; anti-suspicion rule 3 is the strongest solution-boundary clause in the set |
| 7 | Critique–Ship | one-sided (compatible) | `conditional` / `publication-defect` + the clean-review **I** edge, both matching roadmap §3.2; `landed_state: merged` never authorizes history rewriting |
| 8 | Understand Code–Spec | agreed | I: UC→Spec facts-not-intent; payload wordings differ but contain each other |
| 9 | Understand Code–Plan | agreed | Payload lists match element-for-element; Architect blueprint route confirmed on both sides (UC §3.4 Q7 ↔ Plan §2.5) |
| 10 | Understand Code–Implement | agreed | Verbatim payload match; "directly only when an approved plan already owns the change" identical on both sides |
| 11 | Understand Code–Test | mismatched (minor) | **F13** — receiver requires snapshot + accepted architecture constraints; emitter names neither |
| 12 | Understand Code–Debug | agreed· | Debug accepts UC's row; quote drops "Reproduction context if supplied" (F5); substance intact |
| 13 | Understand Code–Ship | agreed | Verbatim payload match; "never H, never invocation" identical both sides |
| 14 | Spec–Plan | agreed· | Full artifact contract and ten-part gate adopted field-for-field by Plan; **F18** wording ("planning approval") to normalize |
| 15 | Spec–Implement | agreed | Both declare no direct workflow edge; P-routes (agent spawn, `sdd` phases) named identically on both sides; spawn remains explicitly unowned (both say so) |
| 16 | Spec–Test | agreed· | Bidirectional I matches; **F14** row-wording gap (artifact satisfies all five required elements) |
| 17 | Spec–Debug | agreed | Debug accepts Spec's row; trivial rewording only; "a cause never redefines intent" symmetric |
| 18 | Spec–Ship | agreed | Verbatim payload match incl. "no command or release instruction"; issue-close stays a P-route, accepted by Ship §3.6 "as provenance, not as a claim" |
| 19 | Plan–Implement | agreed | The strongest seam in the tranche: Implement adopts `astra.plan.executable/v0` and the immutable-version rule (answers Plan Q2, marked blocking); progress-state split enumerated on both sides |
| 20 | Plan–Test | agreed | Bidirectional optional I; payloads compatible; neither side claims execution of the other's obligations |
| 21 | Plan–Debug | mismatched (minor) | **F4** — `diagnosis acceptance` has no Debug Report field; `scope_exceeded` unmapped; otherwise the row Plan wrote blind is satisfied (Debug supplies the artifact Plan's open Q9 requested) |
| 22 | Plan–Ship | agreed | Both declare no direct edge; Ship's §7.2 explicitly answers Plan open Q10 with the indirect route ("Plan → user → Implement → user → Ship") for the reason Plan's own row gives |
| 23 | Implement–Test | agreed | The TDD loop written identically from both ends: "visible user-mediated loop, not H"; inbound/outbound payloads verbatim; Implement's return-snapshot obligation mirrors Test's green-half expectation |
| 24 | Implement–Debug | agreed· | Debug accepts Implement's row incl. its H-correction; narrowing 2 stated and gap-free ("the two rules meet without a gap and without an overlap," astra-debug §1); payload trivially reworded (F5, faithful) |
| 25 | Implement–Ship | agreed | Ship consumes Implement §2.4 field-for-field (§2.3 mapping); Ship §6.4 is the written owner Implement §9.6's three gates require — "Written is now satisfied; tested is not" |
| 26 | Test–Debug | agreed· | Debug accepts both directions; outbound widened with the "no correct seam" finding (stated); inbound quote drops "attempts limited to test scope" (F5); F7's `local-debug` secondary remains Test-unconfirmed |
| 27 | Test–Ship | agreed | Verbatim payload match; "a clean result is not a problem handoff" appears in identical words on both sides |
| 28 | Debug–Ship | agreed | Ship's blind row accepted verbatim by Debug; prohibition symmetric ("no retrying an irreversible effect to 'see what happens'") |
| — | (deferred peers) | — | Debug↔Guard (investigate freeze-state finding, F8/§4.6), Debug↔Incident (F6), Debug/Ship↔Deploy (F3, F8.2): recorded one-sided by construction; not part of the 28 |

Summary: 19 agreed (5 of them with attached minor findings), 2 mismatched-minor, 7
structurally one-sided (all Critique pairs, all compatible), 0 absent. Of the 53 directed
row-statements, the only substantive repairs needed are F4's one field and F13's two fields;
everything else is wording-level or one-sided-pending-review.

---

## 4. Proposed ledger changes

For the coordinator only. Every collision row below is proposed **`claimed`** — never
`resolved` — matching the ledger's rule that `resolved` waits for post-user-review
reconciliation. Column values not shown (component type, availability, candidate
neighborhoods) are unchanged from the seeded rows. Evidence cells cite the owning design;
the coordinator should link the design section, not this report, as the row's evidence. These
consolidate the seven drafted designs' §3.x proposals; **no two designs claim the same
occurrence as primary** (verified across all eight proposal tables, **O**), so there are no
conflicting-claim rejections to record.

### 4.1 Collision source-claim ledger

**Plan & spec (owners: astra-spec, astra-plan, astra-implement).**

| Occurrence ID | Source | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|
| `cm-plan-and-spec-01` | `superpowers:brainstorming` | proposed Astra design | `astra-spec` | `astra-plan`: provenance of the terminal writing-plans edge only; `astra-critique`: external review support remains separate | claimed | astra-spec §§3.1–3.4 |
| `cm-plan-and-spec-02` | `superpowers:writing-plans` | proposed Astra design | `astra-plan` | `astra-implement`: consumes only the approved Plan artifact, never this source | claimed | astra-plan §§3.1–3.4 |
| `cm-plan-and-spec-03` | `superpowers:executing-plans` | proposed Astra design | `astra-implement` | — | claimed | astra-implement §§3.1–3.3 |
| `cm-plan-and-spec-04` | `superpowers:subagent-driven-development` | proposed Astra design | `astra-implement` | — | claimed | astra-implement §§3.1–3.3 |
| `cm-plan-and-spec-05` | `spec` | proposed Astra design | `astra-spec` | `astra-plan`: executable-detail split; `astra-implement`: spawned-agent effect excluded (unowned); `astra-ship`: issue-close/archive provenance (accepted as provenance, astra-ship §3.6); `astra-critique`: independent evaluator behavior | claimed | astra-spec §§3.1–3.4 |
| `cm-plan-and-spec-06` | `to-spec` | proposed Astra design | `astra-spec` | issue delivery remains an explicit external adapter | claimed | astra-spec §§3.1–3.4 |
| `cm-plan-and-spec-07` | `sdd` | independent reference | retained independent | `astra-spec`: consumes persistent-spec and backward-revision principles only; `astra-implement`: P-route only (speckit Implement phase), no consumer claim | claimed | astra-spec §§3.1–3.4; astra-implement §3.4 |
| `cm-plan-and-spec-08` | `planb` | proposed Astra design (authoring slice) | `astra-plan` | `astra-implement`: reconciliation recorded in its §5.9 — claims 2 behaviors, refuses 6, partially claims phase review; five refused behaviors remain unowned roster-wide | claimed | astra-plan §§3.1–3.4; astra-implement §5.9 |
| `cm-plan-and-spec-09` | `plan-tune` | retained independent | retained `plan-tune` | — (explicit user-supplied preferences are ordinary Plan input) | claimed | astra-plan §§3.1–3.4 |
| `cm-plan-and-spec-10` | `wayfinder` | retained independent | retained `wayfinder` | candidate upstream evidence for `astra-spec`; Spec-side contract silent — coordinator decision pending | claimed | astra-plan §§3.1–3.4 |
| `cm-plan-and-spec-11` | `to-tickets` | proposed Astra design (decomposition + draft projection) | `astra-plan` | publisher delivery remains an explicit external effect, unowned | claimed | astra-plan §§3.1–3.4 |
| `cm-plan-and-spec-12` | `implement` | proposed Astra design | `astra-implement` | — (unconditional current-branch commit rejected; Ship-owned path required for retirement) | claimed | astra-implement §§3.1–3.3 |
| `cm-plan-and-spec-15` | `feature-dev:feature-dev` | defer | unassigned | phase-5 candidate for `astra-implement`; phases 1–4/6 require Spec / Understand Code / Plan / Critique reconciliation | claimed (cross-peer item) | astra-implement §§3.1–3.3 |

**Testing (owner: astra-test).**

| Occurrence ID | Source | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|
| `cm-testing-01` | `tdd` | proposed Astra design | `astra-test` | `astra-implement`: production-green half, artifact-mediated (accepted, astra-implement §3.4) | claimed | astra-test §§3.1–3.3 |
| `cm-testing-02` | `superpowers:test-driven-development` | proposed Astra design | `astra-test` | `astra-implement`: delete/edit/refactor effects (accepted with §5.6 limit) | claimed | astra-test §§3.1–3.3 |
| `cm-testing-03` | `bdd` | proposed Astra design | `astra-test` | `astra-spec`: accepted OpenAPI contract and annotation authority; fresh coverage auditor stays external/manual | claimed | astra-test §§3.1–3.3 |
| `cm-testing-04` | `spock` | proposed Astra design | `astra-test` | `astra-critique`: implementation-quality judgment and score/refusal (Critique-side consumption pending its revision — F8.1) | claimed | astra-test §§3.1–3.3 |
| `cm-testing-05` | `nextjs-test` | proposed Astra design | `astra-test` | `astra-implement`: production-change/fix half (accepted with a narrowing) | claimed | astra-test §§3.1–3.3 |
| `cm-testing-06` | `shell-scripting:bats-testing-patterns` | proposed Astra design | `astra-test` | — | claimed | astra-test §§3.1–3.3 |
| `cm-testing-07` | `superpowers:verification-before-completion` | proposed Astra design | `astra-test` | `astra-ship`: consumes fresh evidence only (accepted without qualification, astra-ship §3.6); `astra-implement`: may consume required commands | claimed | astra-test §§3.1–3.3 |
| `cm-testing-08` | `run` | defer | unassigned | — (P only; U bytes) | claimed | astra-test §3.1, §10 |

**Debug & incident (owner: astra-debug; one home change).**

| Occurrence ID | Source | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|
| `cm-debug-and-incident-01` | `investigate` | proposed Astra design | `astra-debug` | `astra-guard`: writes freeze state today (authority conflict; behavior reversed in the candidate) | claimed | astra-debug §§3.1–3.4, §4.6; authored template is the oracle; pin gstack `a3259400`, 1.60.1.0 |
| `cm-debug-and-incident-02` | `diagnosing-bugs` | proposed Astra design | `astra-debug` | `astra-understand-code`: Phase-6 handoff to `improve-codebase-architecture` | claimed | astra-debug §§3.1–3.4; content hash is sole provenance (`~/.agents` not a git repo) |
| `cm-debug-and-incident-03` | `superpowers:systematic-debugging` | proposed Astra design | `astra-debug` | `astra-test`: defers failing-test authoring (Test-side unconfirmed — F8.4) | claimed | astra-debug §§3.1–3.4; **pin 6.2.0** (`eafe962b…`); orphaned 6.1.1 must not be the oracle |
| `cm-debug-and-incident-06` | `java-leak-resolver` | proposed Astra design | `astra-debug` | — | claimed | astra-debug §§3.1–3.4; monster-prompt `6abccfa5` |
| `cm-debug-and-incident-07` | `staging-debug` | proposed Astra design | **`astra-deploy`** (coordinating; provisional pending Deploy — F3/D2) | `astra-debug`: Steps 5–6 environment-difference diagnosis; `astra-test`: Step 4; `astra-ship`: Step 7 `/pr` | claimed | astra-debug §3.4; if Deploy declines, record retained independent per roadmap Wave 4 |
| `cm-debug-and-incident-08` | `local-debug` | proposed Astra design | `astra-debug` | `astra-test`: Steps 1–3 BDD execution (Test-side unconfirmed — F7) | claimed | astra-debug §§3.1–3.4 |

**Ship & VCS (owner: astra-ship).**

| Occurrence ID | Source | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|
| `cm-ship-and-vcs-01` | `ship` | proposed Astra design (partial) | `astra-ship` | `astra-test`: consumes evidence, never generates; `astra-critique`: pre-landing review army is independent judgment (F8.1) | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-04` | `landing-report` | proposed Astra design (read-only mode) | `astra-ship` | — | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-06` | `/pr` | proposed Astra design (partial) | `astra-ship` | `astra-critique`: the `diss` gate is independent judgment; Jira comment effect unowned | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-07` | `/commit` | proposed Astra design | `astra-ship` | — | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-09` | `commit-commands:commit` | proposed Astra design | `astra-ship` | — (manifest has no version; provenance incomplete) | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-10` | `commit-commands:commit-push-pr` | proposed Astra design (partial) | `astra-ship` | — (no-gate default rejected) | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-11` | `commit-commands:clean_gone` | defer | unassigned | — (destructive authority model requires a user decision — D6) | claimed | astra-ship §§3.1–3.4, §4.5 |
| `cm-ship-and-vcs-12` | `changelog` | defer; re-triage out of Ship & VCS | unassigned; recommend `astra-deploy` | `astra-document` if the coordinator prefers a documentation home | claimed | astra-ship §§3.1–3.4; second inbound Deploy claim (F8.2) |
| `cm-ship-and-vcs-13` | `document-release` | defer | unassigned; `astra-document` candidate | `astra-ship` consumes its result as a publication-record / PR-body section | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-14` | `resolving-merge-conflicts` | proposed Astra design | `astra-ship` | — ("never `--abort`" rejected; F17 notes the non-landing trigger gap) | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-15` | `superpowers:finishing-a-development-branch` | proposed Astra design | `astra-ship` | — (the authority spine; owner required by astra-implement §9.6) | claimed | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-16` | `superpowers:using-git-worktrees` | defer | unassigned | `astra-implement`: workspace creation is its intake prerequisite; `astra-ship`: teardown only | claimed (cross-peer item) | astra-ship §§3.1–3.4 |
| `cm-ship-and-vcs-17` | `github` | independent reference | retained independent | `astra-ship` consumes forge-CLI recipes | claimed | astra-ship §§3.1–3.5 |

**Code review (partial — only the three rows a tranche design owns).**

| Occurrence ID | Source | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|
| `cm-code-review-10` | `simplify` | defer | unassigned | — (U bytes; host-version provenance unresolved) | claimed (provenance-deferred) | astra-implement §§3.1–3.3 |
| `cm-code-review-11` | `code-simplifier` | proposed Astra design | `astra-implement` | separate internal refiner delivery shape preserved | claimed | astra-implement §§3.1–3.3 |
| `cm-code-review-12` | `health` | independent reference | retained independent | `astra-implement` may consume a report | claimed | astra-implement §§3.1–3.3 |

Rows `cm-code-review-01..09` remain untouched: they await the Critique source-expansion
revision, and no tranche design claims them (**O**).

**Refined secondary-role text on already-claimed rows** (no home changes): apply
astra-understand-code §3.4's refined text for `cm-codebase-comprehension-01/-02/-04/-05` and
`cm-plan-and-spec-14` — in particular, `-04`'s "grilling becomes an H candidate" must be
re-expressed per the current relation vocabulary (H originates only at Critique;
astra-understand-code §7.3 states the correction the coordinator must carry into the ledger
cell).

### 4.2 Reference and cleanup ledger

Three new rows (disposition `unassigned`; the user keeps `keep`/`defer`/`exclude` authority)
and two `consuming_designs` updates:

| Source ID | Component type | Location | Availability | Disposition | Reason | Consuming designs | Evidence |
|---|---|---|---|---|---|---|---|
| `sdd` | skill | `~/.claude/skills/sdd` → `monster-prompt/claude/skills/sdd/` | live | unassigned | Recommend keep pending user decision: workflow-status outcome and command/effect policy not owned by Spec; Spec consumes only the persistent-spec/backward-revision slice | `astra-spec` | astra-spec §3.5; clean revision `6abccfa5…`; skill `652a1039…` |
| `health` | skill | `~/.claude/skills/health/SKILL.md` → gstack | live | unassigned | Recommend keep pending user decision: report-only quality dashboard, a different outcome from approved-plan mutation | `astra-implement` | astra-implement §3.3; gstack `a3259400` |
| `github` | skill | `~/.claude/skills/github/SKILL.md` | live | unassigned | Recommend keep pending user decision: forge-specific `gh` cookbook; Ship stays forge-agnostic and consults rather than absorbs | `astra-ship` | astra-ship §3.5; skill `40c016d1…` |
| `codebase-design` (update) | — | — | — | — | — | add `astra-debug` **only if** the F16 convention (runtime consumption, not drafting vocabulary) is adopted and Debug's candidate genuinely consults it | astra-debug §3.5; F16 |
| `nowhat` (no change) | — | — | — | — | trigger-adjacency with Debug's re-entry surface recorded, no consumer claim | — | astra-debug §3.5, §7.4 |

---

## 5. Proposed roadmap amendment 6 — drafted text, not applied

> ## 13. Amendment 6 — cross-design reconciliation of the drafted tranche
>
> **Date:** 2026-08-04
> **Scope:** roster-wide pairwise reconciliation of the eight tranche designs, per section 7
> milestone preparation and `docs/phase-0.md` section 7 step 4
> **Authority:** as in amendments 1–5. This amendment records the reconciliation result and
> updates roadmap state only. It marks no design reviewed, resolves no ledger row, and approves
> no roster.
> **Research input:**
> [`docs/research/2026-08-04-cross-design-reconciliation.md`](research/2026-08-04-cross-design-reconciliation.md).
>
> ### 13.1 Result
>
> All 28 bilateral pairs were compared over the 53 directed relation rows. 19 pairs agree, 2
> carry minor payload mismatches (Understand Code↔Test field lists; Plan↔Debug's missing
> `diagnosis acceptance` field), and the 7 Critique pairs are structurally one-sided pending the
> Critique source-expansion revision. No pair is absent and no two designs claim the same
> occurrence as primary. The seven declared Critique destination profiles are mutually
> disjoint except for one routing gap: a known-cause code-defect finding without an approved
> remediation plan is directed to `astra-plan` by both `astra-implement` §7.4 and section 3.2's
> Implement row, but `astra-plan`'s declared class and intake cannot receive it. That gap is a
> user decision recorded in the research report (D1), not a defect in either design alone.
>
> ### 13.2 Section 3.2 changes
>
> - The Implement row gains the note: *"the `plan-required` fallback route awaits a receiving
>   Plan contract — see research report F1; user decision pending."*
> - The narrative/data-comprehension row's reconciliation note gains the second stale anchor:
>   `designs/astra-critique.md` line 764 (routing corpus) in addition to line 588.
> - The infrastructure open-owner row records that two tranche designs now independently
>   propose `astra-deploy` as the effect-side home for deployment-shaped sources
>   (`staging-debug`, `changelog`); the change half remains open pending the Deploy design.
> - The prompt/`SKILL.md`/CLAUDE.md open-owner row records that all three Plan-&-spec-derived
>   designs were drafted and none claims the class; the applied `/trim` secondary role
>   ("Plan & spec: prompt or skill remediation") is dangling and should be re-pointed when
>   Skill Design or Document is drafted.
> - The running developer-experience row is unchanged: the tranche supplied no evidence
>   (`astra-test` §2.2 explicitly routes exploratory QA out).
>
> ### 13.3 Section 5 allocation annotations (evidence-based deviations by the drafted designs)
>
> - **5.2 (Code review):** `simplify` deferred (U bytes) and `health` proposed independent
>   reference rather than `astra-implement` sources; `code-simplifier` stands.
> - **5.5 (Plan & spec):** `sdd` → retained independent reference (consumed by Spec);
>   `plan-tune` and `wayfinder` → retained independent; `feature-dev:feature-dev` deferred as a
>   cross-peer item; `planb` split (authoring slice to Plan; five execution behaviors refused by
>   both Plan and Implement and now explicitly unowned).
> - **5.6 (Ship & VCS):** `changelog` withdrawn from Ship & VCS (re-triage toward
>   `astra-deploy`); `document-release` deferred toward `astra-document`;
>   `superpowers:using-git-worktrees` deferred cross-peer (creation half unowned);
>   `commit-commands:clean_gone` deferred pending a user authority decision; `github` →
>   retained independent reference.
> - **5.8 (Debug & incident):** as amendment 5 already noted, `staging-debug` → `astra-deploy`
>   coordinating home, provisional pending Deploy; `triage`'s designated decider (`astra-ship`)
>   made no decision — the relocation question returns to the user.
> - **5.12 (Testing):** allocation confirmed unchanged; `run` deferred (U bytes).
>
> ### 13.4 Trigger-surface decisions recorded
>
> - "root cause analysis": provisional context rule — live-incident context → `astra-incident`
>   (`rca`'s parallel session); otherwise → `astra-debug`. The bare string is not a router key.
>   `astra-incident` must confirm on drafting.
> - `local-debug` Steps 1–3 (BDD execution): recommend Test-side acceptance of the secondary
>   role; recorded as Debug-proposed, Test-unconfirmed until then.
> - `staging-debug` phrasings: route by effect intent — deploy-and-retest verbs → Deploy;
>   difference-explanation → Debug.
> - Input-state adjacencies that the roster-wide table must encode: "turn this into
>   an issue/ticket" (idea → Spec; approved plan → Plan's draft projection); "resolve merge
>   conflicts" outside a landing flow is currently claimed by no design (research F17).
>
> ### 13.5 What this amendment does not establish
>
> - It does not claim any source is absorbed, preserved, or eligible for retirement.
> - It does not mark any design reviewed, apply any ledger row, or convert any declared
>   profile into a canonical peer contract; section 7 milestone 3 still owns that.
> - It does not resolve the D1 routing gap, `staging-debug`'s final home, `clean_gone`,
>   `triage`, or any section 3.2 open owner.
> - It does not run the acceptance-criterion-1 coverage diff, and it does not touch the nine
>   neighborhoods still uninspected at bundle depth.

---

## 6. Decisions requiring the user

Normative conflicts this pass deliberately did not resolve:

**D1 — Where does a known-cause, no-plan remediation finding go?** (F1.) Options: (a) Plan
generalizes its accepted-diagnosis intake so a user-accepted Critique finding qualifies
(smallest change; recommended on the evidence that Plan §2.5 already demands exactly those
fields); (b) Plan adds a second conditional handoff sub-class; (c) accept the manual route
(user re-derives via Spec/Debug) and document it as a permanent limitation. Both Implement's
and Plan's texts are internally consistent — only the user can decide which design widens.

**D2 — `staging-debug`: apply the provisional Deploy home now, or leave the row unassigned
until Deploy is drafted?** (F3.) Recommendation: apply as `claimed` with `astra-deploy`
coordinating home — `claimed` reserves, it does not accept, and the Wave 4 row already defines
the decline path. The alternative (hold unassigned) keeps the ledger silent about the only
evidence-backed proposal on file.

**D3 — "root cause analysis" routing rule.** (F6.) Adopt the context-conditional rule
provisionally, or defer any rule until `astra-incident` is drafted. Recommendation: adopt
provisionally; a collision with no interim rule misroutes today's most natural phrasing.

**D4 — The unowned execution residue.** `planb`'s five refused behaviors (plan-file writes,
host task creation, general subagent dispatch, advisor calls, live adaptation), gstack `spec`'s
fresh-worktree agent spawn, `/pr`'s Jira comment, tracker writes, and release tagging now have
no owner anywhere in the roster — by two designs' explicit, matching refusals, not by
oversight. Decide whether these await the deferred Delegate/Automate/Deploy designs (default)
or any should be explicitly approved for deletion at the affected sources' retirement gates.

**D5 — `triage` disposition.** (F10.) The designated decider made no decision. Options:
retained independent (default; amendment 1's evidence supports it, and it costs no context
budget) or assign the question to the Ship review. Recommendation: retained independent.

**D6 — `commit-commands:clean_gone`.** Ship deferred it because its unconfirmed force-deletion
authority model "requires a user decision before any allocation" (astra-ship §3.3). Decide:
exclude, retain independent with a warning, or assign its *outcome* (space reclamation under
per-effect authorization) to a future Ship/Deploy revision.

**D7 — Standing reference recommendations.** Unchanged from the designs but now consolidated:
`sdd`, `health`, `github` join `research`, `codebase-design`, `nowhat`, `canvas-design`,
`algorithmic-art`, `diagram`, `prototype` as `unassigned` reference rows awaiting your
keep/defer/exclude decisions. No design infers `keep`.

---

## 7. What this pass did not establish

Following the convention of roadmap amendment sections 8.4, 9.4, 10.6, 11.x, and 12.4:

- **It reviewed nothing.** All seven drafted designs remain `proposed` and self-reviewed only;
  this reconciliation of unreviewed drafts can itself be invalidated by the user's review of
  any design.
- **It resolved nothing.** No ledger row moved, and every proposal in section 4 is `claimed`
  at most. `resolved` remains reserved for the coordinator's pass after user review.
- **It did not create canonical peer contracts.** The seven declared Critique destination
  profiles remain "written but unreviewed"; roadmap section 7 milestone 3 still owns the
  canonical snapshot, and F4/F9's payload repairs should land before it is taken.
- **It did not verify behavior.** Every agreement found here is textual. No source was
  executed, no comparison system built, no gate run; the designs' own section 9 obligations
  stand untouched.
- **It did not close the open owners.** Infrastructure's change half, prompt/`SKILL.md`/
  CLAUDE.md problems, and running developer-experience problems remain without owners; the
  tranche narrowed the first (diagnosis half to Debug, effect-side evidence pointing at
  Deploy) and supplied nothing for the other two beyond confirming no tranche peer claims
  them.
- **It could not consult the absent counterparties.** `astra-deploy`, `astra-incident`,
  `astra-document`, `astra-guard`, and `astra-qa` are unwritten; every inbound claim on them
  (F3, F6, F8) is one design's side only.
- **It did not re-run the inventory coverage diff** (acceptance criterion 1) or inspect the
  nine neighborhoods still open at bundle depth (roadmap §6.1).
- **Anchor freshness is partial.** Critique's line anchors (588/764) and four of Plan's five
  peer-snapshot hashes were re-verified against the working tree on 2026-08-04; Plan's
  Implement snapshot is stale (F11), Debug recorded no peer snapshots, and all design-file
  anchors in this report are valid only for the bytes present at that verification.
