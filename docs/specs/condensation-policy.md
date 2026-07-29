# Condensation Policy

**Date:** 2026-07-29
**Status:** Approved for implementation planning
**Scope:** The universal decision procedure for condensing duplicative skills into astra
skills, and the invariants every condensation must satisfy regardless of which pattern it
uses.

> 留其精華，去之糟粕 — but nothing is 糟粕 merely because something else already occupies the
> same shelf.

This document decides **what** must be preserved and **which pattern** a cluster gets. It does
not specify pattern mechanics. Those live in `patterns/`.

---

## 1. Three artifact types

| Artifact | Path | Owns |
|---|---|---|
| **Policy** | `condensation-policy.md` (this) | Universal decision procedure and invariants. Applies to every cluster. |
| **Pattern** | `patterns/<name>.md` | Specialized mechanics for one representation. Selected by §7, never chosen by preference. |
| **Condensation record** | `records/<cluster>.md` | Which patterns one cluster received, the classification that selected them, and the conformance evidence. |

The patterns currently specified:

| Pattern | Selected when | Spec |
|---|---|---|
| Panel | judgment differs | `patterns/panel.md` |
| Method library | method differs | `patterns/method-library.md` |
| Adapter set | substrate differs | `patterns/adapter-set.md` |
| Pipeline | sequence is load-bearing | `patterns/pipeline.md` |
| Behavior preservation | any input carries frontmatter behavior | `patterns/behavior-preservation.md` |

A cluster may receive one pattern, several composed (§8), or none — **keep separate** is a
first-class outcome, not a failure to condense.

---

## 2. The governing rule

> **Equivalent behavior is deduplicated. Distinct behavior is preserved using the
> representation appropriate to its dimension.**

Three corollaries, each load-bearing:

1. **Condensation removes duplicate expressions, never behavior.** Seven copies of one voice
   become one voice. Two voices never become one voice.
2. **The burden of proof falls on the merge, not on preservation.** Absent evidence of
   equivalence, preserve. "I could not find a case where they differ" is a reason to look
   harder, not a proof of sameness (§9 E5).
3. **A representation is not a ranking.** Becoming a parameter is not demotion; a persona is
   not more important than a playbook. The dimension decides the representation, and nothing
   else does.

This replaces an earlier formulation ("two layers never merge, three always merge"), which was
too absolute: whether a differing subject collapses into a parameter depends on whether the
behavioral contracts are otherwise identical, not on the dimension alone.

---

## 3. Eligibility — and the keep-separate outcome

**The policy owns eligibility.** It does not assume the collision map has already decided
which skills belong together. `README.md`, *"Absorbing new skills"*, requires the absorption workflow to handle a
skill that arrives tomorrow and appears in no map; a policy that took clustering as input
could not serve that case. The collision map (`README.md`, *"The collision map"*) is therefore a **cached result
of applying this procedure**, not an input to it.

### Co-eligibility test

> Two skills are co-eligible iff a single plausible user request could route to either.

Write the request. If you cannot write one, the skills are not duplicative and no amount of
surface similarity makes them so.

### The four outcomes

| Finding | Outcome |
|---|---|
| Not co-eligible — no shared request routes to both | **Keep separate.** Reference skills (`README.md`, *"Not merge targets — reference skills"*): single-purpose documentation for one library, framework or standard. Fusing them produces the "skills that try to do everything" anti-pattern. |
| Co-eligible, but no behavior is shared at any dimension | **Keep separate.** Nothing to deduplicate; a shared entry point would add a routing decision and remove nothing. |
| Target is dead | **Sweep, do not absorb.** A dead skill cannot be absorbed (`README.md`, *"Not merge targets — the dead science collection"* — the 133 dangling symlinks). Record the sweep; do not add a collision-map row. |
| Co-eligible with shared behavior | **Condense.** Proceed to §4. |

Keep-separate still produces a record (§10). An unrecorded decision to leave two skills alone
is indistinguishable from never having looked.

### 3.2 From pairwise co-eligibility to a cluster

Co-eligibility is a **pairwise** relation, so it does not by itself define a cluster. A chain
where A↔B and B↔C but A↮C has to resolve somehow, and the three available readings give
different answers.

> **A cluster is a maximal set in which every member is co-eligible with every other member —
> a clique, not a connected component.**

Consequences:

- The A↔B↔C chain with A↮C yields **two overlapping clusters**, `{A,B}` and `{B,C}`. B is a
  member of both and appears in both records.
- **Overlap is expected, not an error.** The collision map already records three such skills —
  `pair-agent`, `office-hours` and `skillify` each sit in two clusters (`README.md`, *"Total
  absorbed"*).
- A connected-component reading is rejected because transitivity does not hold for co-eligibility:
  it would drag unrelated skills into one cluster through a single bridging member, and the
  bridge's own breadth would decide the cluster's contents.
- When a member appears in two clusters, **each record classifies it independently.** The same
  skill may contribute a seat in one cluster and a playbook in another; that is composition
  (§8), not contradiction.
- Where two records would condense the same member into two different survivors, that conflict is
  resolved before either condensation proceeds, and both records cite the resolution.

Cluster membership is therefore itself a recorded finding, not an input (§10 section 1).

---

## 4. Classification dimensions

**Six dimensions, plus register.** For each: the question it answers, when values are *distinct*,
and the representation distinct values take. Register occupies the seventh row but is **not** a
dimension — it is listed so that tone-only differences have a stated disposition instead of falling
through the table (§4.1).

| Dimension | Question | Distinct when | Representation |
|---|---|---|---|
| **Judgment** | *Why* does it conclude X? | Holding artifact, evidence and decision constant, different priors can produce incompatible recommendations within overlapping standing | **Seat** — `patterns/panel.md` |
| **Method** | *What* evidence does it gather, which tests does it run? | Run on the same artifact, they yield different *supported findings* — not merely different prose | **Playbook** — `patterns/method-library.md` |
| **Substrate** | *Which runtime* does it execute on? | They require different runtime prerequisites, distinguishable by a capability probe | **Adapter** — `patterns/adapter-set.md` |
| **Sequence** | *In what order*, and with which gates? | Execution order is load-bearing and stages carry approval gates or irreversible effects | **Stage** — `patterns/pipeline.md` |
| **Authority** | What is it *permitted* to do? | Any difference in the behavior-bearing frontmatter set (§4.3) | **Preserved wholesale** — `patterns/behavior-preservation.md` |
| **Subject** | *Which artifact* is it pointed at? | **Only when the behavioral contract also differs.** Identical contracts over different subjects are not distinct. | **Parameter** (when contracts match) — otherwise reclassify at the dimension that actually differs |
| **Register** | *How* does it sound? | Never. Tone alone is not a distinction. | **A field on the persona** — never its own unit, never a pattern |

### 4.1 Register is a field, not a dimension

Register is listed so that tone-only differences have a stated disposition rather than falling
through. Two candidates differing *only* in how they sound are one persona with one register; the
louder one does not earn its own file. Where register genuinely varies with context — the same
priors stated gently to a newcomer and bluntly to a maintainer — that is a parameter on the
persona, not two personas.

The failure this prevents: a cluster of five skills that all say the same thing at five volumes
producing five seats, whose panel then generates disagreement that is purely stylistic. That is
`patterns/panel.md` §11.3's convergence-control case, and it fails.

### The subject dimension is conditional

This is the correction that makes the model non-absolute. A differing subject collapses into a
parameter **only when the behavioral contract is otherwise identical**. `/diss` and
`/diss-api` share priors, method and authority, so their subject is a parameter. But a skill
whose subject change also changes its prerequisites, its evidence, or what it is permitted to
do has not merely changed subject — reclassify it at the dimension that moved.

### Authority is never a parameter

Authority differences are preserved wholesale, never averaged and never parameterized. This
follows from `README.md`, *"Reading a skill is not invoking it"* — invocation carries the
frontmatter's declared behavior; a `Read` carries only the instruction text. A dimension whose
values cannot survive being read cannot survive being flattened either.

### 4.3 The behavior-bearing frontmatter set

This set is defined **once, here**, and referenced everywhere else. It appears in the authority
distinctness test above, in P4 and P5 (§5), in the autonomy rule (§6), in E2 (§9), and in
`patterns/behavior-preservation.md`. An earlier draft enumerated a partial list separately in
each place, and the lists had already drifted apart.

> **A frontmatter field is behavior-bearing if invoking the skill changes what the agent may do,
> which model or effort runs it, what context it receives, or how arguments bind — anything a
> `Read` of the same file cannot reproduce.**

The definition is by effect, not by enumeration, because the harness's field set changes and an
enumerated list silently stops being complete. Currently known members:

| Field | Carries |
|---|---|
| `allowed-tools` | permission grant |
| `disallowed-tools` | permission denial |
| `hooks` | `PreToolUse` / `PostToolUse` interception |
| `disable-model-invocation` | tier / reachability |
| `model` | which model executes |
| `effort` | reasoning budget |
| `argument-hint` | argument binding |
| skill-scoped `agents/` | separate contexts with their own tools |
| context and background declarations | how the skill's context is managed |

**Any field not on this list is treated as behavior-bearing until shown otherwise.** The test is
whether a `Read` reproduces its effect; unknown fields fail that test by default, which is the
safe direction. This also matches `README.md`'s treatment of unfamiliar plugin manifest fields
in the absorption workflow — keep and leave alone until understood, rather than assume inert.

---

## 5. Preservation obligations

Six obligations, in two classes. **The class determines whether a record entry can excuse a
violation.**

| # | Obligation | Waivable? |
|---|---|---|
| **P1 — Capability** | Every capability of every absorbed skill survives, or the record states explicitly that it was given up and why. `README.md`, Principles §4: *"Nothing is ever silently lost."* | **Yes**, with a named give-up and a reason (§10 section 9). |
| **P2 — Judgment** | Distinct priors survive as separate seats. Never averaged, never blended, never summarized into a neutral middle. | **Yes**, only on a passing convergence fixture (E5). Never on assertion. |
| **P3 — Method** | Distinct methods survive as separate playbooks. **A matching conclusion does not excuse losing a method's evidence** — two playbooks that agree on the verdict may still surface different supporting findings, and both sets survive. | **Yes**, only on a passing convergence fixture (E5). Never on assertion. |
| **P4 — Authority** | The condensed skill enters at the **most restrictive tier** among its inputs, and may not acquire authority no input held. See §6. | **No.** |
| **P5 — Hooks** | Behavior-bearing frontmatter is **vendored, never referenced**, and never serviced through a `Read`. The `guard` lesson (`README.md`, *"Reading a skill is not invoking it"*; `gstack/guard/SKILL.md:12-30`). | **No.** |
| **P6 — Prerequisites** | Every runtime prerequisite is declared together with its behavior when absent. `README.md`, Principles §2(b). Absence must be loud. | **No.** |

### 5.1 P4, P5 and P6 are not waivable

An earlier draft permitted any obligation to be violated with a record entry. That is wrong for
the last three, and the reason is asymmetric consequence.

P1–P3 waivers **lose capability**, which is visible: something the old skill did, the new one
does not, and the record says so. A user who disagrees can read the give-up and object.

P4–P6 waivers **grant authority or hide failure**, which is invisible by construction. A skill
that quietly holds a tool no input held, or whose guard was referenced instead of vendored, or
whose missing prerequisite fails silently, produces no symptom at the moment it is wrong — only
later, and not obviously connected. A record entry saying "we waived the autonomy rule" does not
make the resulting behavior safe, and nobody reads a record at the moment a hook fails to fire.

So: a condensation that cannot satisfy P4, P5 and P6 is not condensed yet. There is no entry
that makes it done.

Note the tightening on P2 and P3 as well: they are waivable only against a **passing convergence
fixture**, never against an argument. Merging two voices or two methods is a §2 corollary 2
situation — the burden falls on the merge.

---

## 6. Condensation cannot increase autonomy

Stated separately because it is the one invariant whose violation is silent, irreversible in
effect, and attractive in the moment.

> **A condensed skill enters at the most restrictive tier among its inputs. Condensation is
> never a promotion.**

`README.md`, Principles §3 (*"Provenance over frequency"*) already establishes that who
initiated an invocation — not how often it fired — decides what runs autonomously, and that for
side-effecting skills heavy manual use is evidence the user wants to *keep* control. `/pr` is 39
typed against 1 agent-fired. A ship-and-VCS condensation that merged `/pr` into a model-invoked
skill would hand the agent commit rights as a side effect of tidying, which no one approved.

Three consequences:

- **Tier assignment is not a condensation decision.** Giving a condensed skill a `description`
  is a promotion, and promotions go through `/astra:tune` against a full window of evidence
  (`README.md`, *"Approving a use is not approving a tier change"*). A newly condensed skill
  enters at the most restrictive tier its inputs occupied.
- **Behavior-bearing does not imply Tier 1.** The README's tier model resolves this directly:
  a behavior-bearing skill may be **Tier 2b** — cold, zero context cost, reachable by you, and
  reached by the agent through the router *surfacing the miss* rather than reading the file
  (`README.md`, *"Tier 2b (behaviour-bearing) — the router surfaces the miss to you"*). The
  constraint is **never Tier 2a**, not "always Tier 1." An earlier draft of
  `patterns/behavior-preservation.md` asserted Tier 1 was mandatory, which would have forced
  every safety and ship condensation into model invocation — promoting autonomy through a rule
  that looked like a safety requirement.
- **Authority acquisition is bounded by the union of inputs, and scoped within it.** The
  condensed skill may hold no authority beyond the union of its inputs' behavior-bearing
  frontmatter (§4.3). It must additionally not route one input's authority to another input's
  execution path — see `patterns/behavior-preservation.md` §5.

---

## 7. Pattern selection procedure

1. **Eligibility** (§3). Keep-separate → write the record and stop.
2. **Classify** every cluster member along the six dimensions of §4 (register per §4.1). For each dimension, count
   distinct values using that dimension's test.
3. **Select** patterns from the table below — one per dimension with ≥2 distinct values.
4. **Compose** if more than one pattern was selected (§8).
5. **Validate** behaviorally (§9 E5). A distinctness claim that no contrastive run exercises is
   provisional, and provisional means preserved.
6. **Record** (§10).

| Classification result | Outcome |
|---|---|
| Judgment ≥2 distinct | Panel |
| Method ≥2 distinct | Method library |
| Substrate ≥2 distinct | Adapter set |
| Sequence load-bearing | Pipeline |
| Authority differs, **or** any input declares behavior-bearing frontmatter (§4.3) | Behavior preservation — **overlay, always additive** |
| Subject differs, contracts identical | No pattern — parameterize |
| **No dimension differs — members are behaviorally equivalent** | **Plain deduplication** (§7.1) |
| **No behavior shared at any dimension** | Keep separate (§3) |

Selection is mechanical given the classification. The judgment in this procedure lives entirely
in step 2, which is why step 5 exists to check it.

### 7.1 Plain deduplication

The last two rows are opposites and were previously conflated under a single "none" outcome,
which routed exact duplicates to keep-separate — the precise inverse of §2.

> **No dimension differs** means the members are behaviorally equivalent. §2 requires them to
> be deduplicated. **No behavior is shared** means they merely answer the same need by unrelated
> means; there is nothing to deduplicate and §3 keeps them separate.

Plain deduplication is a real outcome with no specialized pattern:

1. One member survives as the condensed skill. Choose the survivor by evidence — highest
   agent-fired count, then most complete prerequisite declarations — and state the choice in the
   record.
2. Every other member is retired. Their entry points become aliases on the survivor if they were
   user-invoked, so typed muscle memory keeps working (`README.md` §4, *"Nothing is ever
   silently lost"*).
3. P1 still binds. Equivalent behavior does not mean identical *text*: if a retired member's
   phrasing covers a case the survivor's does not, that content merges into the survivor. The
   claim being made is behavioral equivalence, not textual redundancy.
4. E5 still binds, and this is the outcome where it binds hardest. Plain deduplication asserts
   the strongest possible equivalence, so it needs the strongest evidence — a passing convergence
   fixture across the full corpus. Absent that, the members are *provisionally distinct* and
   preserved (§2 corollary 2).

`grill-me` and `grill-with-docs` are the archetype: seven-line stubs that delegate to `grilling`.
Under the previous table they would have been kept separate forever.

The asymmetry in step 4 is deliberate. Every other outcome preserves something on weak evidence;
this one destroys something. It carries the heavier burden.

---

## 8. Pattern composition

Patterns are not alternatives. A cluster differing at three dimensions receives three
patterns, composed by these rules:

1. **Behavior preservation is an overlay, never a choice.** It applies to any condensation whose
   inputs declare anything in the behavior-bearing frontmatter set (§4.3) — *in addition to*
   whatever other pattern was selected, never instead of it. The other four patterns are
   selected by dimension and may themselves compose with each other; this one is purely
   additive and can appear alongside any combination of them.
2. **Pipeline is outermost.** When sequence is load-bearing, stages are the top-level
   structure and other patterns nest inside individual stages.
3. **Panel and method library compose vertically.** A panel seat *is* persona × playbook ×
   jurisdiction, so a cluster differing at both judgment and method yields seats that draw
   from the playbook library. The playbook has no standing of its own; the seat that runs it
   does.
4. **Adapter set composes beneath everything.** Substrate is orthogonal to who speaks and how
   they investigate — a playbook may run on any adapter that satisfies its prerequisites,
   subject to that adapter set's parity matrix.
5. **Pattern isolation — for open questions.** *An unresolved problem in one pattern does not
   block condensations using another.* This is why the panel's mechanics were moved out of this
   document: `patterns/panel.md` §8.4 records that novel prose-only conflicts between emergent
   decision IDs can pass undetected. That is a panel limitation. It has no bearing on whether a
   browser adapter set or a ship pipeline may proceed, and it must never be cited as though it
   did.

6. **Composition interface — for runtime.** Rule 5 isolates *questions*; it says nothing about
   whether composed patterns can interfere at runtime, which is a separate and currently
   **unspecified** concern. Until it is specified, every record composing two or more patterns
   states, in section 11, the following for each composition boundary:

   | Must state | Why |
   |---|---|
   | Which context holds authority | Authority must not cross a boundary implicitly. A panel seat holds none (`patterns/behavior-preservation.md` §8); a pipeline stage holds its own. |
   | What crosses the boundary | Named artifacts and fields only. A composition that passes "whatever the previous step produced" cannot be reasoned about. |
   | Which side owns teardown | Sessions and gates outlive stages. `patterns/adapter-set.md` A5 assigns teardown to whoever acquired. |
   | What happens when the inner pattern fails | An inner panel failing mid-stage must not leave the outer pipeline believing the stage completed. |

   This is a record obligation, not a runtime specification. It makes the gap visible per record
   rather than pretending composition is free — and §13 carries it as an open question, because
   four records saying "we thought about it" is not the same as a specified interface.

---

## 9. Universal conformance evidence

Every condensation produces all seven, regardless of pattern. Pattern docs add their own on
top; none may subtract.

| # | Evidence |
|---|---|
| **E1 — Capability trace** | Each absorbed skill mapped to where each of its capabilities landed, or an explicit give-up with a reason. Satisfies P1. |
| **E2 — Authority diff** | Invocation mode, `allowed-tools` and `hooks` before and after, demonstrating no increase. Satisfies P4 and §6. |
| **E3 — Prerequisite table** | Every runtime prerequisite with its absence behavior. Satisfies P6. |
| **E4 — Containment proof** | No filesystem reference resolves outside the plugin. Satisfies §11. |
| **E5 — Behavioral validation** | **Reading proposes a distinction; a contrastive run must exercise it.** See below. |
| **E6 — Evidence snapshot** | Content hashes of every source consulted, so line-number anchors can be invalidated rather than silently rotting. Convention established in `patterns/panel.md` §13. |
| **E7 — The condensation record** | §10. |

### E5 — behavioral validation is universal

Source-reading identifies *candidate* distinctions. It cannot establish them. Every pattern
defines a contrastive fixture form, and the same five rules govern all of them:

1. **Source characterization (RED).** Run the **original source skills**, blind, against a fixed
   versioned artifact — before any extraction exists.
2. Include at least one **expected-divergence** fixture and at least one **convergence
   control** — a case where manufactured difference would itself be a failure.
3. Repeat to expose stochastic one-offs. A fixture passes on reproducibility, not a single run.
4. **Extraction preservation (GREEN).** Run the **condensed artifact** on the same corpus. It must
   reproduce every source result from rule 1 — every divergence, every convergence, and every
   source-unique output. Any loss blocks retirement of the source skill.
5. **No observed difference across the corpus makes two values candidates for merger. It never
   proves equivalence.** Preservation is the default when validation is absent or inconclusive.

**Rules 1 and 4 are both mandatory for every pattern.** An earlier draft let three patterns
validate only their own declarations against the condensed artifact — checking that a parity
matrix matched observed behavior, that a gate inventory was internally consistent, that a hook
fired. Those are self-consistency checks. They establish that the new thing does what the new
thing claims; they cannot establish that it does what the *old* things did, which is the only
question P1 asks. A pattern without rule 1 has no baseline and cannot detect a silent loss.

Per-pattern fixture forms — each compares something different, and each needs both gates:

| Pattern | RED compares (source) | GREEN compares (condensed vs source) |
|---|---|---|
| Panel | structured stances on the same catalogued decision and target | every source divergence and convergence preserved, plus source-unique supported findings (`patterns/panel.md` §11.3) |
| Method library | supported finding sets from the same artifact | every source finding still produced (`patterns/method-library.md` §4) |
| Adapter set | which operations each source skill's substrate actually supports | condensed adapters support exactly the source-supported operations; declared matrix matches both (`patterns/adapter-set.md` §6) |
| Pipeline | each source skill's gate points, effect ordering and resume behavior | no baseline gate lost, no ordering inversion, no resume regression (`patterns/pipeline.md` §7) |
| Behavior preservation | which operations each source skill's hooks actually intercept | condensed hooks intercept every source-intercepted operation, with a `Read`-only negative control (`patterns/behavior-preservation.md` §7) |

The adapter row is the clearest illustration of why rule 1 cannot be skipped: validating a parity
matrix against the condensed adapters proves the matrix is honest about the *new* code. Only
running the source skills first establishes what parity existed to preserve.

---

## 10. The condensation record

One per cluster, at `records/<cluster>.md`. Required sections:

```
 1. Cluster members            every skill considered; clique justification per §3.2; overlaps named
 2. Eligibility verdict        co-eligible or keep-separate, with the routing request written out
 3. Dimension classification   six dimensions + register disposition; distinct-value counts; tests
 4. Patterns selected          with composition order (§8), or "plain deduplication" per §7.1
 5. Capability trace           E1
 6. Authority diff             E2 — every field of the §4.3 set, before and after
 7. Prerequisite table         E3
 8. Containment proof          E4
 9. Behavioral validation      E5 — RED and GREEN gates, runs, results; provisionals flagged
10. Pattern-specific evidence  every check the selected patterns add (M*, A*, S*, B*)
11. Composition interface      where patterns compose: which context holds which authority (§8.6)
12. Evidence snapshot          E6 — content hash of every source consulted, including README
13. Given up                   every capability deliberately dropped, with a reason
14. Retirement gate            which source skills may now be uninstalled, and what proved it
```

Sections 8, 10, 11 and 12 were absent from an earlier schema, which required E1–E7 in §9 and then
provided nowhere to put four of them. A conformance item with no home in the record is an item
nobody produces.

Section 13 is not optional and is not a formality. A condensation that gives up nothing has
either preserved everything or failed to notice what it dropped, and the record is where that
distinction becomes visible. Per §5, entries here can excuse only P1–P3 — never P4, P5 or P6.

Section 14 exists because `README.md`, *"Migration"*, sequences uninstallation after
verification. A source skill is retired by evidence, not by the condensed skill's existence.

---

## 11. Packaging — the plugin is the module

**Astra ships as one plugin, and the plugin is the unit of self-containment.** Shared modules
under `protocol/`, `personas/`, `playbooks/` and `adapters/` are inside that unit. Unlike
`guard` reaching into gstack — a collection that can be uninstalled independently — nothing
here can vanish while the rest remains.

This closes the open question at `README.md`, *"Should astra ship as a plugin?"*. The two costs
that section names are accepted as implementation constraints: paths resolve through
`${CLAUDE_PLUGIN_ROOT}` / `${CLAUDE_SKILL_DIR}` and never as literals; and **every command name is
namespaced** — `/astra:denounce`, `/astra:tune`, `/astra:ship`.

The namespacing has one consequence worth stating rather than discovering: the transcript miner
must match the namespaced form. The README predates this decision and writes `/astra-tune`
throughout, so §12 renames it there. These specs use the namespaced form exclusively.

---

## 12. README amendments this policy requires

### 12.1 Replace §2(a) (`README.md:132-141`)

Current text declares skill-level self-containment with a single carve-out for router
discovery. Replace with:

> **(a) Filesystem self-containment — the plugin is the module.** Every astra implementation
> file lives inside the plugin. Skills may consume declared shared modules under `protocol/`,
> `personas/`, `playbooks/` and `adapters/`; nothing reaches outside the plugin.

Consequences:

- **The router exception disappears.** Router discovery becomes ordinary intra-plugin
  composition, not a carve-out.
- **MCP is not a filesystem exception at all.** It is an external runtime prerequisite under
  §2(b) — a different category. The MCP row in *"Treatment by component type"* is recategorized accordingly.
- **The `bin/` rule (*"Vendored scripts. Never reach outside this directory."*) and "vendor it, never link out" still apply**,
  at the plugin boundary rather than the skill boundary.
- **Skills are no longer independently portable.** Stated, not implied.

### 12.2 Add pattern selection to the absorption workflow

The nine-step workflow goes from step 2 "locate the cluster" to step 3 "diff against the
incumbent" to step 7 "place it on the ladder" with no rule for *how* the new capability is
represented. Insert after step 3:

> **3a. Classify and select.** Run the condensation policy's dimension classification
> (`docs/specs/condensation-policy.md` §4) against the incumbent. The dimension that differs
> selects the representation: judgment → seat, method → playbook, substrate → adapter,
> sequence → stage, authority → preserved wholesale, subject alone → parameter. Steps 4 and 5
> then apply *within* that representation.

Without this, 留其精華 has no rule for where 精華 goes, and step 7's ladder placement is asked
to carry a decision it cannot see.

### 12.3 Close the install question

Answered: yes, a plugin. See §11.

### 12.4 Reclassify the collision map's status

The map is a cached result of §3 and §3.2, not an input to it. Note this in the section so a future
reader does not treat cluster membership as given, and note that clusters are cliques — the three
skills the map already records in two clusters each are the expected shape, not anomalies.

### 12.5 Rename every astra command to its namespaced form

§11 makes commands plugin-namespaced. The README writes the unnamespaced form throughout —
`/astra-tune` in *"Tuning"*, and the `astra-<verb>` directory convention in *"Architecture"* and
*"Naming"*. Rename to `/astra:tune` and friends.

Two places where this is more than cosmetic:

- **The transcript miner.** *"Where the numbers come from"* specifies matching `<command-name>`
  entries. It must match the namespaced form, or the promotion signal reads as zero for every
  astra command.
- **The endgame audit.** *"Naming"* proposes that anything in `~/.claude/skills/` not matching
  `astra-*` is a removal candidate. Under §11 astra skills do not live there at all, so the audit
  rule inverts: **anything in `~/.claude/skills/` is a removal candidate**, because the plugin
  holds everything astra owns.

### 12.6 Record the amendment order

12.1 and 12.5 both touch *"Architecture"* and *"Naming"*. Apply 12.1 first — it changes what
self-containment means, which is what makes the 12.5 audit inversion correct rather than arbitrary.

---

## 13. Evidence anchoring and the source snapshot

Adopting the convention `patterns/panel.md` §13 established, and extending it to every document
in this set.

> **Headings and unique quoted phrases are the primary evidence anchors. Line numbers are
> convenience coordinates against a hashed snapshot, never the citation itself.**

### 13.1 Why this is not merely tidiness

**The committed `README.md` at this branch's HEAD is two lines long.** The 600-line document these
specs cite as governing evidence is an **unstaged working draft**. A clean checkout cannot
reproduce a single line citation, which means anyone validating these specs from the repository
alone finds nothing where the citations point.

That is a real reproducibility failure, and the snapshot is what makes it survivable: a reader can
verify they hold the same source the specs were written against, and a hash mismatch tells them
the coordinates are stale before they conclude the claim is false.

### 13.2 Two citation classes

| Class | Form | Example |
|---|---|---|
| **Evidentiary** — cited to support a claim | Document + heading + quoted phrase. No line number required. | `README.md`, Principles §3 (*"Provenance over frequency"*) |
| **Amendment target** — cited to say *edit here* | Line range, explicitly qualified as coordinates against the snapshot hash | `README.md:132-141` @ `efd896c5…` |

Evidentiary citations must survive the source being edited. Amendment targets cannot — they are
instructions to modify a specific region, so they carry line numbers and a hash, and become
invalid together when the hash changes. §12's targets are all of the second class.

### 13.3 Snapshot

```text
efd896c5a85f3983c2dd979676736855bfae5a6aca75ab32b78948ba8c6f5559  README.md (unstaged working draft)
ab22714e84c096eed506f314aa49f44161f08eb37a4b4651fb2725bab6ca07ff  gstack/guard/SKILL.md
```

Every line coordinate in §12 is relative to the README hash. `patterns/panel.md` §13 carries the
snapshot for the gstack and command sources *it* cites; that list is not duplicated here. `guard`
is added because this document and `patterns/behavior-preservation.md` both cite it and it was
absent from panel's list.

**A hash mismatch invalidates the coordinates, not the claims.** Regenerate the line anchors
against the new source, and re-verify each quoted phrase still appears — the phrase is the
evidence.

### 13.4 The README must be committed before implementation planning closes

The amendments in §12 apply to a file that is not in version control. Until the working draft is
committed, §12 cannot be executed as written and E6 cannot be satisfied for any record. This is
tracked in §14.

---

## 14. Open questions

- **The README working draft is uncommitted.** §13.4. Blocks §12 execution and E6 for every
  record. Highest-priority item in this list because everything else cites it.
- **Composed-pattern runtime interference.** §8 rule 6 makes it a per-record disclosure, which is
  a stopgap, not a specification. What is missing: whether composed contexts can observe or
  mutate each other's state, and what the authority boundary is at runtime rather than on paper.
- **Cluster boundaries for mixed clusters.** Design & visual (20 skills) differs at judgment,
  method *and* substrate. §8 says patterns compose and §3.2 says clusters are cliques, but
  whether that cluster is one condensed skill or several is not decided here and needs its own
  record.
- **`records/` for the 17 existing clusters.** None written yet. The policy is untested against
  anything but the adversarial-critique cluster, and §7.1 (plain deduplication) has never been
  exercised at all.
- **Playbook and adapter roster granularity.** Same budgeting question as the persona roster,
  one dimension across.
- **Conformance harness location.** Where E1–E7 and the pattern-specific checks run, and whether
  a failing check blocks a condensation or annotates it.
- **`model` override conflicts.** §4.3 lists `model` as behavior-bearing, but there is no total
  ordering over model names, so "keep the higher one" is not defined. Currently a recorded
  decision rather than a rule (`patterns/behavior-preservation.md` §5).
- **monster-prompt.** Unchanged from `README.md`, *"Open questions"*. §11 sharpens it: if astra is
  one plugin, monster-prompt is either inside that plugin or explicitly outside it.

---

## 15. Provenance

This policy generalizes a document that began as a panel specification and described itself as
a general policy while defining only panel mechanics. Three framings were corrected in the first
review: the absolute "two layers never merge, three always merge" rule (§2, §4); the assumption
that cluster membership was an input rather than an output (§3); and the placement of
panel-specific mechanics — including the emergent-decision-ID limitation — inside the universal
document, where they would have appeared to gate unrelated condensations (§8 rule 5).

A second review found two defects in the core policy, both now closed, and both worth recording
because they were failures of the same kind — a rule that read as protective while doing the
opposite:

- **Exact duplicates could not condense.** §2 requires equivalent behavior to be deduplicated, but
  the §7 selection table routed "no dimension differs" to keep-separate, conflating it with "no
  behavior shared." The two are opposites. `grill-me` and `grill-with-docs` — seven-line stubs
  delegating to `grilling` — would have been preserved permanently by the policy whose purpose is
  to condense them. Closed by §7.1.
- **Behavior preservation promoted autonomy.** `patterns/behavior-preservation.md` asserted that
  behavior-bearing skills must be Tier 1, which is model-invoked. Applied to the safety, ship and
  setup clusters, a rule that reads as hardening would have granted the agent autonomous reach
  over every skill that writes, deletes or deploys. The README's own Tier 2b — cold,
  behavior-bearing, reached by escalation rather than by `Read` — was the answer already available.
  Closed by that document's §3.1 and §6, and by §6 here.

Nine further corrections came out of the same review: non-waivable P4–P6 (§5.1), the canonical
behavior-bearing frontmatter set replacing four drifted enumerations (§4.3), clique-based cluster
formation (§3.2), register's missing disposition (§4.1), the record schema's four missing evidence
sections (§10), both E5 gates required of every pattern rather than three patterns validating only
their own declarations (§9), the composition interface disclosure (§8 rule 6), evidence anchoring
against a hash because the cited README is uncommitted (§13), and `model` having no total ordering
(§14).

The pattern documents carry their own corrections: pipeline's contradictory partial-autonomy mode
and its unevaluable `effect_free` condition, adapter-set's missing capability baseline,
method-library's inverted selection precedence, and behavior-preservation's route-unsafe tool
union.
