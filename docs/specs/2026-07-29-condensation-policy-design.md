# Condensation Policy — Design

**Date:** 2026-07-29
**Status:** Approved for implementation planning
**Scope:** How duplicative skills are condensed into astra skills without flattening the
distinct voices they carry. Defines the panel module, its interface, and the amendments this
forces on `README.md`.

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

**The authors already found the split.** `autoplan/SKILL.md:20` carries
`<!-- AUTO-GENERATED from SKILL.md.tmpl -->` — gstack templates the chassis in at build time.
What a template cannot do is stop shipping it seven times.

**Two costs, stated separately.** Maintenance and drift across seven files is the larger one.
Context cost is per-invocation only — SKILL.md bodies are not preloaded, descriptions are — but
it is real: `plan-ceo-review` loads 1,476 lines to deliver roughly 600 lines of CEO.

---

## 2. Decisions locked

| # | Decision | Rationale |
|---|---|---|
| D1 | **Astra ships as one plugin. The plugin is the self-contained module.** | Shared `personas/`, `playbooks/`, `protocol/` are inside the unit. Unlike `guard` reaching into gstack, nothing here can be uninstalled independently. Closes `README.md:577`. |
| D2 | **Blind round → seat-declared conflict scan → targeted rebuttal → procedural rendering → resolution.** | Independence is preserved by *ordering* — each seat commits its claims before seeing any other's. Debate is bought without spending diversity of prior. |
| D3 | **The chair is procedural. It sorts; it does not rule.** | A mediator with substantive power is a homogenizer in a neutral hat, and it touches the output last. |
| D4 | **Distinctness is decided by the disagreement test (§9).** | A panel whose members cannot disagree burns N dispatches to produce one opinion. |

---

## 3. Architecture — four layers

**Panel seat = Persona × Playbook × Jurisdiction.**
**Panel = Protocol + one or more seats.**

| Layer | Question it answers | Evidence it exists today |
|---|---|---|
| **Persona** | *Why* it reaches a conclusion — priors, decision policy, register | `plan-eng-review:838-852`, `plan-ceo-review:900-920`, `cso:791` |
| **Playbook** | *What* evidence it gathers and which tests it performs | `diss.md:151` code-map, `:193` risk-classify, `:282` verifier; devex TTHW journey trace `plan-devex-review:941`; CSO attack-surface enumeration `cso:923` |
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

The panel is therefore a table inside the convening `SKILL.md`, which is already in context
when the skill fires. This is what `diss.md:323,349,373` does today at 50 invocations/month.

Three declared escape hatches, in descending order of trust:

1. **Conditional seats** — `if the diff touches auth or crypto → add seat cso@security`.
   Declared; the condition is evaluated against facts.
2. **User-named** — `/astra-denounce --with karpathy`.
3. **Index lookup** — `personas/INDEX.md`, read only when the panel is genuinely open-ended.
   This is the path that can degrade, so it is the fallback, not the mechanism.

---

## 4. Panel module interface

The panel is a deep module. This is its interface — every field below is load-bearing for at
least one chair invariant (§6) or conflict mechanism (§8).

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
  decision_id:  string              # which decision this claim bears on
  position:     string              # one atomic assertion, prose
  stance:                           # structured, enables mechanical comparison
    target:     <file:line or artifact ref>
    disposition: accept | reject | rewrite | defer | block
  evidence:     [ { ref, quote } ]
```

`decision_id` + `stance` exist to make the mechanical backstop (§8.2) implementable. Without
a structured stance, "incompatible positions" is a semantic judgment, and only seats may make
those.

`kind` is asserted by the filing seat and determines routing at §5.5: factual claims are
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
  round:        2
  text:         string              # seat-nominated, bounded, rendered verbatim
  supports:     [<claim.id>]
```

The seat nominates its own block. The chair never selects an excerpt — selection biases the
result exactly as paraphrase does.

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

Each seat receives persona + playbook + jurisdiction, and nothing from any other seat.
Submits numbered atomic claims per the Claim schema. Independence is structural here.

### 5.2 Conflict scan — seats declare, chair does not

Each seat receives the merged claim list and returns **only** Challenge records: contested
claim IDs plus a one-line ground. Nothing else.

Anchoring is prevented by **ordering, not blindness** — every seat's own claims are committed
and immutable before it sees anyone else's. Seeing other claims at this point cannot
retroactively change what it filed.

This step is where the chair would otherwise have to make a semantic judgment. It cannot, so
standing stays with the speakers.

### 5.3 Targeted rebuttal

Only contested claims are re-dispatched. Claimant and challenger are dispatched
**separately**, each receiving the contested claim plus the other's position — never a shared
context, which would reintroduce the anchoring §5.1 spent independence to avoid. Each ends by
nominating a bounded `final_position` block. Uncontested claims stand as filed and are never
re-dispatched.

### 5.4 Procedural rendering

The chair copies nominated `final_position` blocks verbatim into the report, subject to §6.

### 5.5 Resolution

| Clash kind | Route |
|---|---|
| **Normative** (tradeoff, design, taste) | `AskUserQuestion` with every surviving side quoted verbatim |
| **Factual** | Verifier playbook (§7). Seats then revise, withdraw or retain. |
| **Factual, verifier returns `indeterminate`** | Rendered as explicit uncertainty, both sides quoted. Never silently resolved. |

Normative clashes go to the user; factual ones go to evidence; only genuinely undecidable
ones are rendered as uncertainty. This matches the house norm already in place —
`plan-ceo-review:874` *"Present each scope-expanding idea as an AskUserQuestion,"* `:880`
*"In ALL modes, the user is 100% in control."*

---

## 6. `protocol/chair.md` — invariants

Mechanically testable. Each is a check a conformance harness can run against a transcript.

| # | Invariant |
|---|---|
| C1 | Every non-scaffold sentence in the final output appears **verbatim** in a speaker submission. |
| C2 | The chair emits zero claims of its own. |
| C3 | Scaffold text comes from a **fixed, versioned allowlist**. The chair may not generate new scaffold prose. |
| C4 | Every rendered position is a seat-nominated `final_position` reproduced **whole** — never a substring. |
| C5 | Every surviving nominated position is rendered **exactly once**. |
| C6 | Attribution is preserved on every rendered block; ordering is deterministic. |
| C7 | Every unresolved clash renders **every** surviving side. |
| C8 | Every claim surviving to output traces to a round-1 claim ID. |
| C9 | Verification evidence may be added after round 1, but must **link to existing claim IDs**. An unrelated late claim restarts the claim cycle rather than entering the report. |

C3 is what stops the chair from smuggling substance in as connective tissue. C5 closes the
gap in "every rendered position was nominated" — which permits dropping one.

**The chair does not live under `personas/`.** It lives at `protocol/chair.md`. Naming it a
persona invites exactly the substantive behavior C1–C9 forbid.

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

**Identical `decision_id` with incompatible `stance.disposition` triggers a conflict even if
no seat contests it.** Incompatible pairs: `accept`×`reject`, `accept`×`block`,
`rewrite`×`accept`, `defer`×`block`.

This is mechanical, not semantic — it does not require the chair to interpret prose, only to
compare two enum values against a fixed table. It therefore does not violate C2.

**This backstop is not yet operational.** It depends entirely on two seats independently
choosing the same `decision_id` for the same decision, which is an unsolved problem (§12).
Until it is solved, §8.1 is the only live detection mechanism and §8.4's limitation is wider
than stated there.

### 8.3 Conformance fixtures (test time only)

Expected clashes live in fixtures and panel-selection metadata, **never in runtime persona
content.** Runtime `Disagrees with` blocks are rejected because they create pairwise coupling
between persona files, go stale silently, and prime performative disagreement — telling Linus
he clashes with Ramsay invites him to manufacture a clash.

### 8.4 Recorded limitation

**None of the three guarantees detection of a novel conflict.** Fixtures catch only conflicts
represented in the corpus. The backstop catches only conflicts that reduce to structured
disposition on a shared `decision_id`. Seat-declared contests depend on seats noticing.

A conflict that is novel, prose-only, and unnoticed by every seat **will pass silently.** This
is a known and accepted gap, not an oversight. The mitigation is that fixtures grow with the
corpus, and a missed conflict that later appears in a fixture becomes a regression test on
panel composition.

---

## 9. The condensation rule

> **Two voices are distinct iff, holding artifact, available evidence and decision constant,
> their different priors can produce incompatible recommendations within overlapping
> standing.**

Exclusions:

| Difference is only… | Then it is… |
|---|---|
| tone | **register** — a persona field, not a persona |
| subject matter | **jurisdiction** |
| investigative technique, same decision policy | **playbook** |
| decision policy | **persona** |

### Worked example — adversarial critique cluster (15 skills)

| Absorbed | Prior | Verdict |
|---|---|---|
| `grill-me`, `grill-with-docs` | none — 7-line stubs delegating to `grilling` | **machinery** |
| `autoplan` | none — sequences four skills | **protocol**, not a voice |
| `/diss`, `/diss-api`, `diss-infra`, `diss-claudemd` | identical priors, four subjects | **one persona, four jurisdictions** |
| `grilling` | "you have not thought this through and I will not let you move on" | **persona** |
| `/elon` | "the requirement itself is probably wrong; rebuild from physics" | **persona** |
| `office-hours` | "is the problem even understood yet?" | **persona** — attacks the problem statement where Elon rebuilds the solution |
| `plan-ceo-review` | cathedral, scope-up, completeness-is-cheap (`:874,878`) | **persona** |
| `plan-eng-review` | blast radius, boring-by-default, strangler-fig, reversibility, production ownership (`:838-852`) | **persona** — see below |
| `plan-design-review` | "what does the user see first, second, third" | **persona** |
| `plan-devex-review` | "first five minutes decide everything" (`:876`) | **persona** |

**`plan-eng-review` is NOT merged into Linus.** An earlier draft proposed this from grep hits
without reading the region; reading it disproves the merge. `plan-eng-review:834` —
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

## 10. Packaging — README amendments

D1 locks plugin-root sharing. The seam **moves**; no new exception is added.

### 10.1 Replace §2(a) (`README.md:132-139`)

Current text declares skill-level self-containment with a single carve-out for router
discovery. Replace with:

> **(a) Filesystem self-containment — the plugin is the module.** Every astra implementation
> file lives inside the plugin. Skills may consume declared shared modules under
> `protocol/`, `personas/`, and `playbooks/`; nothing reaches outside the plugin.

Consequences:

- **The router exception disappears.** Router discovery becomes ordinary intra-plugin
  composition, not a carve-out.
- **MCP is not a filesystem exception at all.** It is an external runtime prerequisite under
  §2(b), which is a different category. `README.md:548` is recategorized accordingly.
- **`bin/` rule (`README.md:197`) and "vendor it, never link out" (`:615`) still apply**, at
  the plugin boundary rather than the skill boundary.
- **Skills are no longer independently portable.** Stated, not implied.

### 10.2 Close the install question (`README.md:577`)

"Should astra ship as a plugin?" is answered: **yes**. The two costs that section names are
accepted and become implementation constraints — paths resolve through
`${CLAUDE_PLUGIN_ROOT}` / `${CLAUDE_SKILL_DIR}`, never literals; and command names are
namespaced (`/astra:denounce`), which `/astra-tune` must match when mining transcripts.

### 10.3 Correct the collision map

The adversarial-critique row keeps `plan-eng-review` as a distinct persona. Cluster totals
are unaffected — it was never proposed for deletion, only for merger into another voice.

---

## 11. Cost model and measurement plan

### 11.1 Corrected model

| Phase | Input cost |
|---|---|
| Round 1 (blind) | **O(N)** — `N × (persona + playbook + jurisdiction)` |
| Round 2 (conflict scan) | **O(N²)** — each of N seats receives the merged list of ≈`N × c` claims |
| Round 3 (rebuttal) | **O(M)** — M = contested claims only |

The old model was `N × (chassis + specialist material)`; the new one is
`chassis + N × specialist material`. **Both are linear in N with a better slope — not
"super-linear to nearly flat," which was wrong.** Chassis leaves the per-seat coefficient;
it does not leave the equation.

**The debate phase does not inherit round 1's slope.** The conflict scan is quadratic in seat
count, which is the term that decides whether large panels are affordable.

### 11.2 The 49% figure is withdrawn as a claim

`autoplan` reading four skills is 1476 + 1514 + 1050 + 1460 = 5,500 source lines against an
estimated ~2,800 under this design. That is **a source-line ratio, not a token measurement.**
It ignores per-subagent context setup, round 2 and round 3 output entirely. It is an estimate
pending §11.3 and is labelled as such wherever it appears.

### 11.3 Measurement protocol

Benchmark at **N = 2, 4, and 6 seats** — a single four-seat run cannot establish scaling when
one phase is quadratic.

Baseline: `autoplan` on a real plan under current gstack.
Comparison: the same plan through an astra panel at each N.

Record per run: input tokens, output tokens, wall-clock, seats dispatched, claims filed,
challenges raised, rebuttals dispatched, decisions surfaced.

The claim to defend is **marginal cost per seat**, plus the N at which the quadratic scan term
overtakes the linear round-1 term.

### 11.4 Panel-size cap

A default cap is declared as part of this design, set from §11.3 results. Provisional default
is **4 seats**, escalating to 6 only where the artifact warrants and the user opts in.
The cap is a protocol parameter, not a per-skill choice, so it cannot drift upward one skill
at a time.

---

## 12. Open questions this design does not close

- **Playbook roster.** Which playbooks exist, and their granularity. Same budgeting question
  as the persona roster, one layer down.
- **`decision_id` assignment.** How seats agree on a shared identifier for the same decision
  without coordinating — the mechanical backstop (§8.2) depends entirely on this and it is
  unsolved. If two seats name the same decision differently, the backstop silently misses.
- **Conformance harness.** Where C1–C9 run, and whether a failing chair transcript blocks
  output or annotates it.
- **Persona roster and Tier 1/Tier 2 assignment.** Unchanged from `README.md` open questions.
- **monster-prompt.** Unchanged. D1 makes it sharper — if astra is one plugin, monster-prompt
  is either inside it or explicitly outside.

---

## 13. Provenance

Design settled across four decision points. Three claims in earlier drafts were disproved on
inspection and are corrected here: the `plan-eng-review` merge (§9), the cost-scaling
characterization (§11.1), and the assertion that fixtures guarantee a missed conflict becomes
a fixture failure (§8.4).