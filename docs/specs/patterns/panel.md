# Pattern: Panel

**Date:** 2026-07-29
**Status:** Approved for implementation planning
**Selected when:** the **judgment** dimension carries ≥2 distinct values — cluster members hold
different priors that can produce incompatible recommendations on the same artifact.
**Scope:** panel mechanics only — the seat model, the panel module interface, the debate
protocol, the chair's invariants, and panel-specific cost and validation.

**Governed by** `../condensation-policy.md`. That document owns eligibility, the dimension
classification that selects this pattern, the six preservation obligations, the autonomy rule,
pattern composition, packaging, and the seven universal conformance evidence items. This
document adds panel-specific mechanics on top and subtracts nothing.

> 留其精華，去之糟粕 — but a voice is not 糟粕 merely because another voice already spoke.

---

## 1. The measurement

Seven persona-bearing gstack skills, diffed against each other:

| Skill | Lines | Identical to `plan-ceo-review` | Persona begins |
|---|---:|---:|---:|
| `plan-ceo-review` | 1476 | — | ~866 |
| `plan-design-review` | 1514 | 995 | ~843 |
| `plan-devex-review` | 1460 | 991 | ~849 |
| `review` | 1852 | 979 | ~844 |
| `office-hours` | 1697 | 959 | ~874 |
| `plan-eng-review` | 1050 | 915 | ~805 |
| `cso` | 1285 | 841 | ~791 |

Every file is chassis-then-persona in that order. The `## Voice` block is byte-identical
across all seven (`plan-ceo-review:631`, `plan-eng-review:607`, `cso:606`), each reciting the
same house style before declaring a different character underneath it.

**The authors already found the split.** `autoplan/SKILL.md:21` carries
`<!-- AUTO-GENERATED from SKILL.md.tmpl -->` — gstack templates the chassis in at build time.
What a template cannot do is stop shipping it seven times.

**Two costs, stated separately.** Maintenance and drift across seven files is the larger one.
Context cost is per-invocation only — SKILL.md bodies are not preloaded, descriptions are — but
it is real: `plan-ceo-review` loads 1,476 lines to deliver roughly 600 lines of CEO.

---

## 2. Decisions locked

| # | Decision | Rationale |
|---|---|---|
| D1 | **Astra ships as one plugin. The plugin is the self-contained module.** | Shared `personas/`, `playbooks/`, `protocol/` are inside the unit. Unlike `guard` reaching into gstack, nothing here can be uninstalled independently. **Now owned by `../condensation-policy.md` §11** — it applies to every pattern, not only this one; retained here because the seat model depends on it. |
| D2 | **Decision catalogue → blind round → seat-declared conflict scan → targeted response → resolution → procedural rendering.** | Known decisions receive shared identifiers before seats run. Independence is preserved by *ordering* — each seat commits its claims before seeing any other's. Debate is bought without spending diversity of prior. |
| D3 | **The chair is procedural. It sorts; it does not rule.** | A mediator with substantive power is a homogenizer in a neutral hat, and it touches the output last. |
| D4 | **Distinctness is decided by the behavioral disagreement test (§9, §11.3).** | A panel whose members cannot disagree burns N dispatches to produce one opinion. Reading proposes a distinction; a contrastive run must exercise it. |
| D5 | **Known decision IDs are invocation data; novel decisions remain emergent.** | Seats select shared IDs rather than minting them blindly. Emergent findings remain discoverable, but the mechanical backstop is deliberately incomplete for them. |
| D6 | **Reader limits are protocol parameters enforced at seat submission.** | The chair may neither paraphrase nor trim. Bounded claims and final positions protect the reader without giving the chair substantive discretion. |

---

## 3. Architecture — four layers

**Panel seat = Persona × Playbook × Jurisdiction.**
**Panel = Protocol + one or more seats.**

| Layer | Question it answers | Evidence it exists today |
|---|---|---|
| **Persona** | *Why* it reaches a conclusion — priors, decision policy, register | `plan-eng-review`, “Cognitive Patterns — How Great Eng Managers Think” (`:838-855`); `plan-ceo-review`, “Cognitive Patterns — How Great CEOs Think” (`:906-923`); `cso`, “Chief Security Officer Audit” (`:789-795`) |
| **Playbook** | *What* evidence it gathers and which tests it performs | `diss.md`, “Code Map” (`:141-180`), “Risk Classification” (`:182-205`), and verifier (`:282-295`); `plan-devex-review`, “TTHW Benchmarks” (`:922`); `cso`, “Attack Surface Census” (`:919-923`) |
| **Jurisdiction** | *Which* artifact, this invocation | declared in the convening skill's panel table |
| **Protocol** | Blindness, conflict handling, rendering, user control | `protocol/` |

The playbook layer is not optional. `diss.md:151-193` builds a code map and risk
classification *before any voice speaks*. That is neither Linus's personality nor generic
chassis — it is the investigation method the venomous seat runs across every jurisdiction.
Under a three-layer model it has nowhere to live, so it would bloat the persona, leak into
the chassis, or be discarded during condensation.

Playbook separation also makes seats recombinable: the same failure-mode-mapping playbook run
by the eng-manager persona ("what is the blast radius") and by the CSO persona ("what does
this expose") produces different findings from identical evidence.

### Panel declaration is data, not inference

Skill selection must be inferential — the router cannot know in advance what will be asked.
Seat selection need not be: by the time a seat is needed a skill has already fired, so the
task is already classified. Inferring the panel pays for that classification twice, and the
second payment reintroduces the routing collision one level down.

The seat roster is therefore a table inside the convening `SKILL.md`, which is already in
context when the skill fires. This is what the three declared reviewer roles at
`diss.md:323,349,373` do today. The **wider 15-skill adversarial-critique cluster**, not
`/diss` alone, records 50 July invocations in the working `README.md`, *"The collision map"* → adversarial-critique row.

Three declared escape hatches, in descending order of trust:

1. **Conditional seats** — `if the diff touches auth or crypto → add seat cso@security`.
   Declared; the condition is evaluated against facts.
2. **User-named** — `/astra:denounce --with karpathy`.
3. **Index lookup** — `personas/INDEX.md`, read only when the panel is genuinely open-ended.
   This is the path that can degrade, so it is the fallback, not the mechanism.

### Decision catalogue is invocation data

Seat selection classifies *who should speak*. It does not assign shared names to the
artifact-specific decisions they discuss. Before the blind round, the convening skill creates
a neutral decision catalogue from explicit user questions and artifact anchors. If the
artifact does not enumerate its decisions, an evidence-only preflight extractor may identify
targets and phrase neutral questions; it may not recommend an answer.

Every seat receives the same catalogue and selects from it. Seats may still surface a novel
decision under a seat-scoped `emergent:<seat.id>:<n>` identifier. This preserves discovery
outside the catalogue while making the §8.2 backstop operational for every catalogued
decision. The catalogue can therefore improve coverage but cannot guarantee it.

---

## 4. Panel module interface

The panel is a deep module. This is its interface — every field below is load-bearing for at
least one chair invariant (§6), conflict mechanism (§8), or reader bound.

### PanelInvocation

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

The three limits are provisional defaults. An individual skill may request a lower value but
never a higher one; raising a default requires a versioned protocol change informed by
§11.3. A submission outside these limits is rejected back to its originating seat for
resubmission. The chair never truncates it.

“Word” means a Unicode word-segmentation unit under the Unicode version pinned by the
protocol release. Dispatch validation and the conformance harness use the same counter, so
C10 does not depend on a model's interpretation of word boundaries.

### Seat

```yaml
seat:
  id:            string             # panel-unique, e.g. "eng@migration-plan"
  persona:       personas/<name>.md
  playbook:      playbooks/<name>.md
  jurisdiction:
    artifact:    <path or ref>
    scope:       string             # which part of it
  constraints:
    requires:    [<playbook output>] # evidence this seat needs to exist first
    forbidden_playbooks: [<name>]    # combinations that are illegal
```

`constraints.forbidden_playbooks` is what prevents illegal seats — most importantly, an
evidence-only verifier playbook (§7) may never be paired with a persona, and the chair may
never be paired with a substantive playbook.

### Claim

```yaml
claim:
  id:           string              # globally unique: "<seat.id>.<n>"
  seat:         <seat.id>           # originating seat
  round:        1
  kind:         factual | normative
  decision_id:  string              # catalogue ID or "emergent:<seat.id>:<n>"
  position:     string              # one atomic assertion, <= max_words_per_claim
  stance:                           # structured, enables mechanical comparison
    target:     <file:line or artifact ref>
    disposition: accept | reject | rewrite | defer | block
  evidence:     [ { ref, quote } ]
```

`decision_id` + `stance` exist to make the mechanical backstop (§8.2) implementable. A seat
must use the catalogue ID whenever its claim bears on a catalogued question. Without a
structured stance, "incompatible positions" is a semantic judgment, and only seats may make
those. An emergent ID remains a valid traceability key but is not mechanically comparable to
another seat's independently named emergent decision.

`kind` is asserted by the filing seat and determines routing at §5.4: factual claims are
resolvable by evidence, normative claims are not.

### Challenge

```yaml
challenge:
  challenger:   <seat.id>
  contests:     <claim.id>
  ground:       string              # one line, why it is contested
  kind:         factual | normative
```

A challenge is not a rebuttal. It is a seat asserting that a conflict exists — the semantic
judgment the chair is forbidden from making.

### Verification

```yaml
verification:
  verifier:     playbooks/verify-<domain>.md   # evidence-only, no persona
  claims:       [<claim.id>]                   # must already exist
  evidence:     [ { ref, quote } ]
  result:       supported | contradicted | indeterminate
```

`result` describes the evidence, never who wins. Seats revise, withdraw or retain their own
positions in response.

### FinalPosition

```yaml
final_position:
  seat:         <seat.id>
  revision:     integer             # 0 blind; 1 rebuttal; 2 post-verification
  status:       active | withdrawn
  text:         <string or null>     # active only; <= max_words_per_final_position
  supports:     [<claim.id>]         # non-empty if active; may be empty if withdrawn
  supersedes:   <revision or null>
```

Every seat nominates revision 0 with its blind claims. A re-dispatched seat may replace it
with one higher revision. The highest schema-valid revision is that seat's effective
position. `withdrawn` requires `text: null` and is never rendered; `active` requires non-empty
`text` and `supports`. The chair never selects an excerpt — selection biases the result
exactly as paraphrase does.

### Decision

```yaml
decision:
  id:           <decision_id>
  kind:         normative
  sides:        [ { seat, final_position } ]   # EVERY surviving side
  rendered_as:  AskUserQuestion
```

---

## 5. Protocol

### 5.1 Blind round

Each seat receives persona + playbook + jurisdiction + the neutral decision catalogue +
protocol limits, and nothing from any other seat. It submits numbered atomic claims plus
`final_position.revision: 0`. Independence is structural here.

### 5.2 Conflict scan — seats declare, chair does not

Each seat receives its persona + playbook again, plus the merged claim list, and returns
**only** Challenge records: contested claim IDs plus a one-line ground. Nothing else. Whether
the host resumes a seat context or starts a fresh one, the model input contains the seat
context again; §11.1 prices that replay.

Anchoring is prevented by **ordering, not blindness** — every seat's own claims are committed
and immutable before it sees anyone else's. Seeing other claims at this point cannot
retroactively change what it filed.

This step is where the chair would otherwise have to make a semantic judgment. It cannot, so
standing stays with the speakers.

### 5.3 Targeted rebuttal

Only seats involved in contested claims are re-dispatched. All contests involving the same
seat are batched into **one dispatch for that seat**; otherwise one busy seat would repay its
persona and playbook once per claim. Claimant and challenger always remain in **separate
contexts**. Each receives its contested claims plus the relevant counterpart positions and
ends by nominating one bounded `final_position.revision: 1`.

A seat with no contested claim is never re-dispatched: its revision 0 position becomes
effective mechanically. A seat may not introduce an unrelated claim during rebuttal; C9
restarts the claim cycle if it does.

### 5.4 Resolution

| Clash kind | Route |
|---|---|
| **Normative** (tradeoff, design, taste) | `AskUserQuestion` with every surviving side quoted verbatim |
| **Factual** | Verifier playbook (§7). Affected seats are then re-dispatched once, batched per seat, to revise, withdraw or retain. |
| **Factual, verifier returns `indeterminate`** | Rendered as explicit uncertainty, both sides quoted. Never silently resolved. |

Normative clashes go to the user; factual ones go to evidence; only genuinely undecidable
ones are rendered as uncertainty. This matches the house norm already in place —
`plan-ceo-review`, “Mega Plan Review Mode,” `:874` — *"Present each scope-expanding idea as
an AskUserQuestion"* — and `:879` — *"In ALL modes, the user is 100% in control."*

After factual verification, each affected seat receives its persona + playbook, the verifier
record and its contested claims in its own context. It may nominate
`final_position.revision: 2`. Multiple verified clashes for one seat are again batched into
one dispatch.

### 5.5 Procedural rendering

For each seat, the chair reads its highest schema-valid `final_position.revision`. An
`active` revision is copied verbatim into the report; a `withdrawn` revision is omitted.
Revision number, schema validity and status are mechanical fields, so the chair makes no
textual choice.

---

## 6. `protocol/chair.md` — invariants

Mechanically testable. Each is a check a conformance harness can run against a transcript.

| # | Invariant |
|---|---|
| C1 | Every non-scaffold sentence in the final output appears **verbatim** in a speaker submission. |
| C2 | The chair emits zero claims of its own. |
| C3 | Scaffold text comes from a **fixed, versioned allowlist**. The chair may not generate new scaffold prose. |
| C4 | Every rendered position is a seat-nominated `final_position` reproduced **whole** — never a substring. |
| C5 | Every seat's highest schema-valid `active` revision is rendered exactly once; a highest `withdrawn` revision and every superseded revision are rendered zero times. |
| C6 | Attribution is preserved on every rendered block; ordering is deterministic. |
| C7 | Every unresolved clash renders **every** surviving side. |
| C8 | Every claim surviving to output traces to a round-1 claim ID. |
| C9 | Verification evidence may be added after round 1, but must **link to existing claim IDs**. An unrelated late claim restarts the claim cycle rather than entering the report. |
| C10 | Every Claim and FinalPosition satisfies the invocation's count and word limits. An invalid submission returns to its seat; the chair never truncates or paraphrases it. |

C3 is what stops the chair from smuggling substance in as connective tissue. C5 closes the
gap in "every rendered position was nominated" — which permits dropping one. C10 protects
the reader without weakening C1 or giving the chair editorial power.

**The chair does not live under `personas/`.** It lives at `protocol/chair.md`. Naming it a
persona invites exactly the substantive behavior C1–C10 forbid.

---

## 7. Verifier playbooks

Factual verification runs through an **evidence-only playbook with no persona attached**.
Routing a factual clash back through the claimant's persona would inherit the claimant's
confirmation bias — the seat that filed a claim is the worst possible judge of it.

The verifier reports evidence. The original seats revise, withdraw, or retain.

**This already exists.** `diss.md:282-296` is a working evidence-only verifier:

- keyed on `finding_id` — claim-ID linkage, as C9 requires
- reports `RESOLVED` / `PERSISTING` / `NEW` with `file:line` evidence
- carries no persona, no priors, no register
- enforces **"No evidence = no finding."**

That line becomes the verifier playbook's governing rule.

---

## 8. Conflict detection — three mechanisms and their limits

### 8.1 Seat-declared contest (primary)

§5.2. Preserves standing. Fails when no seat happens to notice a conflict outside its beat.

### 8.2 Mechanical backstop

**Identical catalogued `decision_id` with incompatible `stance.disposition` triggers a
conflict even if no seat contests it.** Incompatible pairs: `accept`×`reject`,
`accept`×`block`, `rewrite`×`accept`, `defer`×`block`.

This is mechanical, not semantic — it does not require the chair to interpret prose, only to
compare two enum values against a fixed table. It therefore does not violate C2.

The pre-dispatch catalogue (§3) makes this operational: seats select a shared identifier
instead of minting one independently. The backstop deliberately ignores seat-scoped
`emergent:*` identifiers because deciding that two differently named novel findings mean the
same thing would be a semantic judgment. Those conflicts remain detectable only through
seat-declared contests.

### 8.3 Conformance fixtures (test time only)

Expected clashes live in fixtures and panel-selection metadata, **never in runtime persona
content.** Runtime `Disagrees with` blocks are rejected because they create pairwise coupling
between persona files, go stale silently, and prime performative disagreement — telling Linus
he clashes with Ramsay invites him to manufacture a clash.

### 8.4 Recorded limitation

**None of the three guarantees detection of a novel conflict.** Fixtures catch only conflicts
represented in the corpus. The backstop catches only conflicts that reduce to structured
disposition on a catalogued `decision_id`. Seat-declared contests depend on seats noticing.

A conflict that is novel, prose-only, and unnoticed by every seat **will pass silently.** This
is a known and accepted gap, not an oversight. The mitigation is that fixtures grow with the
corpus, and a missed conflict that later appears in a fixture becomes a regression test on
panel composition.

---

## 9. Persona distinctness

The distinctness test and the dimension exclusions that route a difference to register,
jurisdiction, playbook or persona are owned by `../condensation-policy.md` §4. The judgment-row
test is restated here because everything below executes against it:

> **Two voices are distinct iff, holding artifact, available evidence and decision constant,
> their different priors can produce incompatible recommendations within overlapping
> standing.**

What follows is the panel-specific form of the policy's universal E5 obligation — reading
proposes a distinction, a contrastive run must exercise it — plus the worked adjudication of
the cluster that selected this pattern.

### The disagreement test is behavioral

Reading source files identifies candidate personas; it does not prove them distinct. For each
candidate pair with overlapping standing:

1. Run the **original source skills**, blind, against the same fixed artifact, evidence and
   fixture-supplied decision catalogue.
2. Include contrastive fixtures expected to make the priors diverge and convergence controls
   on which manufactured disagreement would be a failure.
3. Compare structured stances on the same decision and target across repeated runs.
4. Preserve a persona when the expected incompatible recommendation is reproducible.
5. Treat no observed disagreement across the corpus only as evidence for merger, never as a
   proof of equivalence.
6. After extraction, rerun the corpus against the condensed seat and require source-behavior
   preservation.

This is the executable form of the rule above. §11.3 defines the corpus, repetition and
quality measurements. The first mandatory contrastive fixture is Linus versus Ramsay on
working code with stubbed tests; it should yield incompatible dispositions without either
runtime persona being told to disagree.

### Worked example — adversarial critique cluster (15 skills)

| Absorbed | Prior | Verdict |
|---|---|---|
| `grill-me`, `grill-with-docs` | none — 7-line stubs delegating to `grilling` | **machinery** |
| `autoplan` | none — sequences four skills | **protocol**, not a voice |
| `/diss`, `/diss-api`, `diss-infra`, `diss-claudemd` | identical priors, four subjects | **one persona, four jurisdictions** |
| `/trim` | shorter prompts achieving the same result are strictly better (`trim.md:72`); published-practice audit; prompts and `SKILL.md` only | **provisional persona × prompt-audit playbook × jurisdiction**, convened only for prompt/skill artifacts; behavior-bearing frontmatter is preserved separately |
| `grilling` | "you have not thought this through and I will not let you move on" | **persona** |
| `/elon` | "the requirement itself is probably wrong; rebuild from physics" | **persona** |
| `office-hours` | "is the problem even understood yet?" | **persona** — attacks the problem statement where Elon rebuilds the solution |
| `plan-ceo-review` | cathedral, scope-up, completeness-is-cheap (`:874,878`) | **persona** |
| `plan-eng-review` | blast radius, boring-by-default, strangler-fig, reversibility, production ownership (“Cognitive Patterns,” `:838-855`) | **persona** — see below |
| `plan-design-review` | "what does the user see first, second, third" | **persona** |
| `plan-devex-review` | "first five minutes decide everything" (“DX First Principles,” `:873`) | **persona** |

`/trim` is intentionally the hard case. Its role label alone does not establish a persona,
but its reduction rule can produce a decision prior incompatible with a completeness-first
seat on the same `SKILL.md`. Until the behavioral corpus demonstrates equivalence, the
lossless choice is to preserve that prior provisionally. Its official-practices rubric is a
playbook, its prompt/skill restriction is jurisdiction, and its `AskUserQuestion` plus
`Edit`/`Write` frontmatter remains behavior-bearing machinery rather than persona text. A
passing merger fixture may later remove only the provisional persona; the playbook,
jurisdiction and invocation behavior still survive.

**`plan-eng-review` is NOT merged into Linus.** An earlier draft proposed this from grep hits
without reading the region; reading it disproves the merge. `plan-eng-review`, “Cognitive
Patterns — How Great Eng Managers Think,” `:845` —
*"Incremental over revolutionary — Strangler fig, not big bang. **Refactor, not rewrite**
(Fowler)"* — directly negates Linus's characteristic move of naming the data structure that
should have existed and judging the code against it. The same file holds its own override at
`:836` (*"If the existing foundation is broken, say 'scrap it and do this instead'"*), which
means the eng-manager voice has a standing rule plus an exception where Linus has only the
exception. A clean, elegant rewrite requiring an irreversible big-bang migration is a real
input on which they file incompatible recommendations. **Two decision policies.**

Note what survives that a jurisdiction-based split would have destroyed: **Linus and Ramsay
remain separate**, because on working code shipped with stubbed tests Linus passes it and
Ramsay refuses it. A roster carved by domain collapses both into "the code quality voice."

---

## 10. Collision map correction

Packaging and the README self-containment amendments are owned by
`../condensation-policy.md` §11–§12; they apply to every pattern. What remains here is
specific to the cluster this pattern was selected for.

The adversarial-critique row keeps `plan-eng-review` as a distinct persona. Cluster totals
are unaffected — it was never proposed for deletion, only for merger into another voice.
The same row retains `/trim` as a conditional prompt/skill-review composition pending its
behavioral distinctness fixture; §9 now accounts for all 15 entries.

---

## 11. Cost model and measurement plan

### 11.1 Complete model

Use tokens, not source lines. Let:

- `Pᵢ` = seat `i`'s persona + playbook + jurisdiction + catalogue + limits
- `C` = average round-1 claim-set tokens produced by one seat
- `B` = distinct seats participating in targeted response (`B ≤ N` because §5.3 batches)
- `F` = factual-verifier dispatches and `V` = one verifier's context
- `A` = distinct seats re-dispatched after verification (`A ≤ N` when batched)
- `H` = chair protocol context and `L` = average effective final-position tokens
- `X`, `Y` = targeted-clash and verification-evidence payloads respectively

| Phase | Approximate uncached input |
|---|---|
| Decision-catalogue preflight | one evidence-only extractor context, when the artifact does not enumerate decisions |
| Blind filing | `Σᵢ Pᵢ` |
| Conflict scan | `Σᵢ Pᵢ + N²C` |
| Targeted response | `Σᵢ∈B Pᵢ + X` |
| Factual verification and seat update | `F·V + Σᵢ∈A Pᵢ + Y` |
| Procedural rendering | `H + N·L` |

The conflict scan is therefore **`O(N·P + N²·C)`, not merely `O(N²·C)`**. A resumed agent
does not make `Pᵢ` disappear from model input; its prior context is replayed and billed unless
the provider reports it as cached. Fresh and resumed implementations must therefore report
uncached input, cache reads and cache writes separately.

At the permitted `N = 2/4/6`, repeated persona + playbook context is expected to dominate the
quadratic claim payload. `N²C` remains the asymptotic scaling hazard, but it is not assumed to
be the operational cost driver below the cap. The expensive axis at small N is the number of
**seat-bearing phases**. Condensation removes duplicated chassis from `Pᵢ`; it does not make
the specialist context free on later phases.

### 11.2 The 49% figure is withdrawn as a claim

`autoplan` reading four skills is 1476 + 1514 + 1050 + 1460 = 5,500 source lines against an
estimated ~2,800 under this design. That is **a source-line ratio, not a token measurement.**
It ignores per-subagent setup and every later phase's replayed input and output. It is an
estimate pending §11.3 and is labelled as such wherever it appears.

### 11.3 Behavioral and cost measurement protocol

Cost measurement cannot establish that condensation preserved the voices or improved the
report. The benchmark therefore has three gates, in order.

#### A. Source characterization — RED

For each candidate persona pair with overlapping standing:

1. Build at least three fixed, versioned artifacts with fixture-supplied decision IDs and
   targets. Include at least one expected-divergence case and one expected-convergence
   control.
2. Run each **original source skill** blind on identical artifact + evidence + catalogue.
   A common characterization wrapper may add only the Claim/FinalPosition output schema and
   protocol limits; it contains no persona text, expected answer or pair identity. Run each
   fixture three times to expose stochastic one-offs.
3. A divergence fixture passes when incompatible `stance.disposition` values on the same
   decision and target appear in at least two of three runs. A convergence control passes
   when manufactured incompatibility does not appear in at least two of three runs.
4. Persist claims, stances and expected clashes as §8.3 fixtures. Runtime personas never see
   the expectation metadata.

The first required fixture is Linus versus Ramsay on working code with stubbed tests. Failure
to reproduce the expected clash blocks their merger. No observed disagreement across the
corpus makes two voices **candidates** for merger; it does not prove equivalence.

#### B. Extraction preservation — GREEN

Run each extracted persona + playbook seat on the same corpus, with the same catalogues and
three-run repetition. It must preserve every source fixture's expected divergence and
convergence result. It must also retain source-unique supported findings; a matching final
disposition does not excuse losing a playbook's evidence. Any loss blocks retirement of the
source skill.

#### C. Panel quality and cost

Baseline: current `autoplan` on the fixed corpus. Comparison: the same artifacts through the
astra panel at **N = 2, 4 and 6 seats**. The rosters are nested and versioned: the N=4 roster
contains the N=2 seats, and N=6 contains N=4, so the marginal-seat measurement does not
silently change composition. Run each configuration three times.

A blinded evaluator receives de-identified, order-randomized outputs and the fixture rubric.
It scores:

- recall of seeded material decisions and known failure modes
- supported-claim precision and unsupported-claim rate
- preservation of expected persona divergences and convergence controls
- actionability of the surfaced decisions
- reader load: total words and words per supported material decision

The panel passes only if it preserves every mandatory divergence fixture, loses no seeded
critical decision found by the baseline, introduces no higher unsupported-claim rate than
the baseline, and does not lower the median actionability score. `Decisions surfaced` remains
a diagnostic count; by itself it is not a quality metric.

For every dispatch, record phase, seat, fresh/resumed status, uncached input tokens, cache
read/write tokens, output tokens and wall-clock. Also record seats dispatched, claims,
challenges, distinct rebuttal seats, verifier calls, post-verification seat updates,
effective final-position words and total report words.

The cost claims to defend are **marginal cost per seat**, **marginal cost per seat-bearing
phase**, and total cost at the declared cap. The benchmark reports the measured contribution
of `N·P` and `N²·C`; it does not assume or search for a crossover outside the supported panel
size.

### 11.4 Panel-size cap

A default cap is declared as part of this design, set from §11.3 results. Provisional default
is **4 seats**, escalating to 6 only where the artifact warrants and the user opts in.
The cap is a protocol parameter, not a per-skill choice, so it cannot drift upward one skill
at a time. The claim and final-position limits in §4 are governed the same way and are
validated by the reader-load measurements before implementation planning closes.

---

## 12. Open questions this design does not close

- **Playbook roster.** Which playbooks exist, and their granularity. Same budgeting question
  as the persona roster, one layer down.
- **Conformance harness.** Where C1–C10 run, and whether a failing chair transcript blocks
  output or annotates it.
- **Persona roster and Tier 1/Tier 2 assignment.** Unchanged from `README.md` open questions.
- **monster-prompt.** Unchanged. D1 makes it sharper — if astra is one plugin, monster-prompt
  is either inside it or explicitly outside.

---

## 13. Provenance

Claims in earlier drafts were disproved on inspection and are corrected here: the
`plan-eng-review` merge (§9), two successive cost-scaling characterizations (§11.1), and the
assertion that fixtures guarantee conflict detection (§8.4). Review also closed catalogued
`decision_id` assignment, added reader limits and behavioral characterization, adjudicated
all 15 worked-example inputs, and corrected the README replacement range.

### Evidence snapshot

Headings and unique quoted phrases are the primary evidence anchors. Line numbers are
convenience coordinates against the exact 2026-07-29 inputs below; a hash mismatch means the
line anchors must be regenerated before relying on them.

Gstack sources resolve under `~/.claude/skills/gstack/<name>/SKILL.md`; command sources resolve
under `~/.claude/commands/`.

```text
c18016a320c7516814d41067936b9b239899e08f27b133a306f4de4c20921284  plan-ceo-review/SKILL.md
0f756585231f5630d80e3a3163ca664312acf78ea34e2bb535275816ffb1bfd0  plan-design-review/SKILL.md
4d6cc577f07af1a0268e89ba0fdf45eb595583bdad306f809cbb8b6645c18951  plan-devex-review/SKILL.md
92ee16af71d5e0088326869b0a211c50f94b9261eeae75656bc21f9bcfae2031  review/SKILL.md
b5a0b9d72f4a992ba0b52cd7b27d15e7e0e29e35c4b775477ec3a031c47f5c92  office-hours/SKILL.md
41c92a82319c081ef48a17733bcd5815d83637cf1e0390c45db5f9ccbbca08e9  plan-eng-review/SKILL.md
4d5da6367475aaad38bbf59f29e5c7fa2b184d48590951100b1d409b723133ea  cso/SKILL.md
73e2bf3e7b1868493fc162dccf9f26c182f50e4cfcad3e4f02efce0e3099e472  autoplan/SKILL.md
b4e029d6c927b1ba671748b5d23e026d1c8059bde96e955fb504490da22b9b69  diss.md
0ac5d05a598ca73edf0e35956efddf10ce989a0a68c9483bb6355cab3da73fff  trim.md
efd896c5a85f3983c2dd979676736855bfae5a6aca75ab32b78948ba8c6f5559  README.md (committed at a037f20)
```

The `README.md` hash records the draft whose amendments §10 specifies. That file was an unstaged
working draft when this spec was written and is now committed at `a037f20` with identical content,
so the hash and every line coordinate taken against it remain valid.
