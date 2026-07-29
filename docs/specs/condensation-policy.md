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
which skills belong together. `README.md:599` requires the absorption workflow to handle a
skill that arrives tomorrow and appears in no map; a policy that took clustering as input
could not serve that case. The collision map at `README.md:384` is therefore a **cached result
of applying this procedure**, not an input to it.

### Co-eligibility test

> Two skills are co-eligible iff a single plausible user request could route to either.

Write the request. If you cannot write one, the skills are not duplicative and no amount of
surface similarity makes them so.

### The four outcomes

| Finding | Outcome |
|---|---|
| Not co-eligible — no shared request routes to both | **Keep separate.** Reference skills (`README.md:417`): single-purpose documentation for one library, framework or standard. Fusing them produces the "skills that try to do everything" anti-pattern. |
| Co-eligible, but no behavior is shared at any dimension | **Keep separate.** Nothing to deduplicate; a shared entry point would add a routing decision and remove nothing. |
| Target is dead | **Sweep, do not absorb.** A dead skill cannot be absorbed (`README.md:430` — the 133 dangling symlinks). Record the sweep; do not add a collision-map row. |
| Co-eligible with shared behavior | **Condense.** Proceed to §4. |

Keep-separate still produces a record (§10). An unrecorded decision to leave two skills alone
is indistinguishable from never having looked.

---

## 4. Classification dimensions

Six dimensions. For each: the question it answers, when values are *distinct*, and the
representation distinct values take.

| Dimension | Question | Distinct when | Representation |
|---|---|---|---|
| **Judgment** | *Why* does it conclude X? | Holding artifact, evidence and decision constant, different priors can produce incompatible recommendations within overlapping standing | **Seat** — `patterns/panel.md` |
| **Method** | *What* evidence does it gather, which tests does it run? | Run on the same artifact, they yield different *supported findings* — not merely different prose | **Playbook** — `patterns/method-library.md` |
| **Substrate** | *Which runtime* does it execute on? | They require different runtime prerequisites, distinguishable by a capability probe | **Adapter** — `patterns/adapter-set.md` |
| **Sequence** | *In what order*, and with which gates? | Execution order is load-bearing and stages carry approval gates or irreversible effects | **Stage** — `patterns/pipeline.md` |
| **Authority** | What is it *permitted* to do? | Any difference in invocation mode, `allowed-tools`, or frontmatter `hooks` | **Preserved wholesale** — `patterns/behavior-preservation.md` |
| **Subject** | *Which artifact* is it pointed at? | **Only when the behavioral contract also differs.** Identical contracts over different subjects are not distinct. | **Parameter** (when contracts match) — otherwise reclassify at the dimension that actually differs |

### The subject dimension is conditional

This is the correction that makes the model non-absolute. A differing subject collapses into a
parameter **only when the behavioral contract is otherwise identical**. `/diss` and
`/diss-api` share priors, method and authority, so their subject is a parameter. But a skill
whose subject change also changes its prerequisites, its evidence, or what it is permitted to
do has not merely changed subject — reclassify it at the dimension that moved.

### Authority is never a parameter

Authority differences are preserved wholesale, never averaged and never parameterized. This
follows from `README.md:232` — invocation carries `allowed-tools`, `hooks`, `effort` and
argument binding; a `Read` carries only text. A dimension whose values cannot survive being
read cannot survive being flattened either.

---

## 5. Preservation obligations

Six obligations. Every condensation satisfies all six or states in its record exactly which it
did not, and why.

| # | Obligation |
|---|---|
| **P1 — Capability** | Every capability of every absorbed skill survives, or the record states explicitly that it was given up and why. `README.md:179` §4: nothing is ever silently lost. |
| **P2 — Judgment** | Distinct priors survive as separate seats. Never averaged, never blended, never summarized into a neutral middle. |
| **P3 — Method** | Distinct methods survive as separate playbooks. **A matching conclusion does not excuse losing a method's evidence** — two playbooks that agree on the verdict may still surface different supporting findings, and both sets survive. |
| **P4 — Authority** | The condensed skill inherits the **most restrictive invocation mode** among its inputs, and may not acquire a tool no input held. See §6. |
| **P5 — Hooks** | Behavior-bearing frontmatter is **vendored, never referenced**, and never serviced through a `Read`. The `guard` lesson (`README.md:232`, and `gstack/guard/SKILL.md:12-30`). |
| **P6 — Prerequisites** | Every runtime prerequisite is declared together with its behavior when absent. `README.md:128` §2(b). Absence must be loud. |

---

## 6. Condensation cannot increase autonomy

Stated separately because it is the one invariant whose violation is silent, irreversible in
effect, and attractive in the moment.

> **A condensed skill's invocation mode is the most restrictive among its inputs. Condensation
> is never a promotion.**

`README.md:172` §3 already establishes that provenance, not frequency, decides what runs
autonomously — and that for side-effecting skills, heavy manual use is evidence the user wants
to *keep* control, not evidence they want to give it away. `/pr` is 39 typed against 1
agent-fired. A ship-and-VCS condensation that merged `/pr` into a model-invoked skill would
hand the agent commit rights as a side effect of tidying, which no one approved.

Two consequences:

- **Tier assignment is not a condensation decision.** Giving a condensed skill a `description`
  is a promotion, and promotions go through `/astra-tune` against a full window of evidence
  (`README.md:375` — approving a use is not approving a tier change). A newly condensed skill
  enters at the most restrictive tier its inputs occupied.
- **Tool acquisition is bounded by the union of inputs.** The condensed skill may hold the
  union of its inputs' `allowed-tools` — each input already held its own — but not one tool
  beyond that union.

---

## 7. Pattern selection procedure

1. **Eligibility** (§3). Keep-separate → write the record and stop.
2. **Classify** every cluster member along the six dimensions of §4. For each dimension, count
   distinct values using that dimension's test.
3. **Select** patterns from the table below — one per dimension with ≥2 distinct values.
4. **Compose** if more than one pattern was selected (§8).
5. **Validate** behaviorally (§9 E5). A distinctness claim that no contrastive run exercises is
   provisional, and provisional means preserved.
6. **Record** (§10).

| Dimension with ≥2 distinct values | Pattern selected |
|---|---|
| Judgment | Panel |
| Method | Method library |
| Substrate | Adapter set |
| Sequence | Pipeline |
| Authority (any input carries frontmatter behavior) | Behavior preservation — **overlay, always** |
| Subject only, contracts identical | No pattern — parameterize |
| None | Keep separate (§3) |

Selection is mechanical given the classification. The judgment in this procedure lives entirely
in step 2, which is why step 5 exists to check it.

---

## 8. Pattern composition

Patterns are not alternatives. A cluster differing at three dimensions receives three
patterns, composed by these rules:

1. **Behavior preservation is an overlay, never a choice.** It applies to any condensation
   whose inputs declare `hooks`, `allowed-tools`, `effort`, or a model override — on top of
   whatever other pattern was selected.
2. **Pipeline is outermost.** When sequence is load-bearing, stages are the top-level
   structure and other patterns nest inside individual stages.
3. **Panel and method library compose vertically.** A panel seat *is* persona × playbook ×
   jurisdiction, so a cluster differing at both judgment and method yields seats that draw
   from the playbook library. The playbook has no standing of its own; the seat that runs it
   does.
4. **Adapter set composes beneath everything.** Substrate is orthogonal to who speaks and how
   they investigate — a playbook may run on any adapter that satisfies its prerequisites,
   subject to that adapter set's parity matrix.
5. **Pattern isolation.** *An unresolved problem in one pattern does not block condensations
   using another.* This is why the panel's mechanics were moved out of this document:
   `patterns/panel.md` §8.4 records that novel prose-only conflicts between emergent decision
   IDs can pass undetected. That is a panel limitation. It has no bearing on whether a browser
   adapter set or a ship pipeline may proceed, and it must never be cited as though it did.

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
therefore defines a contrastive fixture form, and the same four rules govern all of them:

1. Run the **original source skills**, blind, against a fixed versioned artifact.
2. Include at least one **expected-divergence** fixture and at least one
   **convergence control** — a case where manufactured difference would itself be a failure.
3. Repeat to expose stochastic one-offs. A fixture passes on reproducibility, not on a single
   run.
4. **No observed difference across the corpus makes two values candidates for merger. It never
   proves equivalence.** Preservation is the default when validation is absent or
   inconclusive.

Per-pattern fixture forms:

| Pattern | Contrastive fixture compares |
|---|---|
| Panel | structured stances on the same catalogued decision and target (`patterns/panel.md` §11.3) |
| Method library | supported finding sets produced from the same artifact |
| Adapter set | which operations succeed, against the declared parity matrix |
| Pipeline | gate inventory and irreversibility ordering across a full run |
| Behavior preservation | whether the hook actually fires — not whether the text mentions it |

---

## 10. The condensation record

One per cluster, at `records/<cluster>.md`. Required sections:

```
1. Cluster members            every skill considered, with source hash
2. Eligibility verdict        co-eligible or keep-separate, with the routing request written out
3. Dimension classification   the six dimensions, distinct-value counts, and the test applied
4. Patterns selected          with composition order (§8)
5. Capability trace           E1
6. Authority diff             E2
7. Prerequisite table         E3
8. Behavioral validation      E5 — fixtures, runs, results; provisional preservations flagged
9. Given up                   every capability deliberately dropped, with a reason
10. Retirement gate           which source skills may now be uninstalled, and what proved it
```

Section 9 is not optional and is not a formality. A condensation that gives up nothing has
either preserved everything or failed to notice what it dropped, and the record is where that
distinction becomes visible.

Section 10 exists because `README.md:624` sequences uninstallation after verification. A
source skill is retired by evidence, not by the condensed skill's existence.

---

## 11. Packaging — the plugin is the module

**Astra ships as one plugin, and the plugin is the unit of self-containment.** Shared modules
under `protocol/`, `personas/`, `playbooks/` and `adapters/` are inside that unit. Unlike
`guard` reaching into gstack — a collection that can be uninstalled independently — nothing
here can vanish while the rest remains.

This closes `README.md:577`. The two costs that section names are accepted as implementation
constraints: paths resolve through `${CLAUDE_PLUGIN_ROOT}` / `${CLAUDE_SKILL_DIR}` and never
as literals; command names are namespaced (`/astra:denounce`), which `/astra-tune` must match
when mining transcripts.

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
  §2(b) — a different category. `README.md:548` is recategorized accordingly.
- **The `bin/` rule (`README.md:197`) and "vendor it, never link out" (`:615`) still apply**,
  at the plugin boundary rather than the skill boundary.
- **Skills are no longer independently portable.** Stated, not implied.

### 12.2 Add pattern selection to the absorption workflow (`README.md:599-620`)

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

### 12.3 Close the install question (`README.md:577`)

Answered: yes, a plugin. See §11.

### 12.4 Reclassify the collision map's status (`README.md:384`)

The map is a cached result of §3, not an input to it. Note this in the section so a future
reader does not treat cluster membership as given.

---

## 13. Open questions

- **Cluster boundaries for mixed clusters.** Design & visual (20 skills) differs at judgment,
  method *and* substrate. §8 says patterns compose, but whether that cluster is one condensed
  skill or several is not decided by this policy and needs a record of its own.
- **`records/` for the 17 existing clusters.** None written yet. The policy is untested against
  anything but the adversarial-critique cluster.
- **Playbook and adapter roster granularity.** Same budgeting question as the persona roster,
  one dimension across.
- **Conformance harness location.** Where E1–E7 are checked, and whether a failing check blocks
  a condensation or annotates it.
- **monster-prompt.** Unchanged from `README.md:641`. §11 sharpens it: if astra is one plugin,
  monster-prompt is either inside that plugin or explicitly outside it.

---

## 14. Provenance

This policy generalizes a document that began as a panel specification and described itself as
a general policy while defining only panel mechanics. Three framings were corrected during
review: the absolute "two layers never merge, three always merge" rule (§2, §4); the
assumption that cluster membership was an input rather than an output (§3); and the placement
of panel-specific mechanics — including the emergent-decision-ID limitation — inside the
universal document, where they would have appeared to gate unrelated condensations (§8 rule 5).
