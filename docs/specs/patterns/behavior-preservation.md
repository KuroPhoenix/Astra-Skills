# Pattern: Behavior Preservation

**Date:** 2026-07-29
**Status:** Draft — no cluster record written yet
**Selected when:** any cluster member declares anything in the behavior-bearing frontmatter set —
defined once at `../condensation-policy.md` §4.3, not enumerated here.
**Scope:** how authority survives condensation — hook vendoring, hook union and collision, scoped
tool authority, the tier constraint, and the escalation path that replaces a `Read` for
behavior-bearing skills.

**Governed by** `../condensation-policy.md`. That document owns eligibility, classification,
the six preservation obligations, the autonomy rule, composition and the seven universal
conformance evidence items.

---

## 1. This is an overlay, not an alternative

The other four patterns are selected by dimension and may compose freely with each other. This one
is **purely additive** — it applies *in addition to* whatever else was selected (policy §8 rule 1),
never instead of it, and it can appear alongside any combination of the others. A ship pipeline
whose stages declare tools gets pipeline mechanics **and** these. A panel whose convening skill
needs `AskUserQuestion` gets panel mechanics **and** these.

It appears alone only when a cluster's members differ at no other dimension — which the safety
cluster is: `careful`, `freeze`, `unfreeze`, `guard` share priors, method and subject, and
differ solely in what they are permitted to do.

---

## 2. Reading a skill is not invoking it

The constraint everything here follows from. `README.md`, *"Reading a skill is not invoking it"*, states it; this is the operative
table:

| Carried by invocation | Carried by `Read` |
|---|---|
| `allowed-tools` permission boundary | ✗ |
| Frontmatter `hooks` | ✗ |
| `effort` / model overrides | ✗ |
| `argument-hint` and argument binding | ✗ |
| Skill-scoped agents and context handling | ✗ |
| The instruction text | ✓ |

`gstack/guard/SKILL.md:12-30` is the proof. It declares `allowed-tools` plus three
`PreToolUse` matchers:

```yaml
allowed-tools: [Bash, Read, AskUserQuestion]
hooks:
  PreToolUse:
    - matcher: "Bash"
      hooks: [{ command: "bash $HOME/.claude/skills/gstack/careful/bin/check-careful.sh" }]
    - matcher: "Edit"
      hooks: [{ command: "bash $HOME/.claude/skills/gstack/freeze/bin/check-freeze.sh" }]
    - matcher: "Write"
      hooks: [{ command: "bash $HOME/.claude/skills/gstack/freeze/bin/check-freeze.sh" }]
```

Reading that file yields a *description* of protection. Only invoking it installs protection.

It is also marked `AUTO-GENERATED from SKILL.md.tmpl`, which means gstack **generates** a
composition-by-reference: `guard` is `careful` + `freeze` expressed as two paths into a sibling
collection. Uninstall gstack and `guard` still declares hooks, still loads, and silently
protects nothing. That is the failure this pattern exists to make impossible.

---

## 3. Two hard constraints

### 3.1 Never Tier 2a — but Tier 2b is available

> A skill declaring anything in the behavior-bearing frontmatter set
> (`../condensation-policy.md` §4.3) **must never be Tier 2a**. It may be **Tier 1 or Tier 2b**.

This follows from §2: Tier 2a's miss handler works by instructing the agent to `Read` a cold
skill's `SKILL.md` (`README.md`, *"The router is the miss handler"*), and a `Read` confers none
of the behavior above. Demoting a behavior-bearing skill to **2a** does not make it cheaper — it
makes it inert while appearing present.

**Tier 2b is the correct destination for most condensations under this pattern.** The README
already defines it: cold, zero context cost, reachable by you, and reached by the agent through
the router *surfacing the miss* rather than reading the file —

> `README.md`, *"Reading a skill is not invoking it"*: *"be cold, but it is **Tier 2b**: the
> router must never service it with a `Read`."*
>
> *"**Tier 2b (behaviour-bearing)** — the router surfaces the miss to you."*

An earlier draft of this document asserted **"Tier 1 is mandatory"**, which was wrong in a way
worth recording, because it inverted the pattern's own purpose:

- It contradicted `../condensation-policy.md` §6, which requires the condensed skill to enter at
  the most restrictive tier among its inputs.
- It contradicted §3.2 of *this* document, which describes the Tier 2b escalation path.
- Most seriously, it **promoted autonomy under the cover of a safety rule.** Tier 1 means
  model-invoked. Forcing every safety, ship and setup condensation to Tier 1 would have handed
  the agent autonomous reach over exactly the skills that write, delete and deploy — as a
  mandatory consequence of a requirement that reads like a hardening measure.

Tier 1 remains permissible when the inputs were already model-invoked and the skill's effects are
reversible. It is never required by this pattern.

### 3.2 Escalation replaces the read

When the router meets a miss on a behavior-bearing skill it does **not** read it. It surfaces
the miss:

> *"This needs `/astra:guard`. Type it."*

That still records demand — the router consulted the skill, which is a `Read`-adjacent signal
`/astra:tune` can mine (`README.md`, *"Where the numbers come from"*) — without pretending a `Read` conferred a boundary it
cannot confer. `README.md`, Principles §4 (*"Nothing is ever silently lost"*), is satisfied: the skill is one hop away, not lost.

---

## 4. Hook union

When condensation merges skills that each declare hooks:

1. **Vendor every script.** Copy it inside the plugin. No `$HOME/.claude/skills/<other>/…`
   path survives condensation. Policy P5, and the whole point of the `guard` lesson.
2. **Union the hooks, never intersect.** Every matcher from every input is present in the
   condensed skill. Intersecting would drop protection, violating P1.
3. **Same-matcher collisions run in declared order.** Two inputs both hooking `PreToolUse`
   on `Bash` produce two hook entries under that matcher, in an order the record states. Order
   matters when one hook mutates state the other reads.
4. **Blocking beats warning.** If two hooks on the same matcher disagree — one blocks, one warns
   and permits — the merged behavior **blocks**. A condensation may not weaken a guard by
   averaging it with a laxer one.
5. **A hook may not be dropped for redundancy.** Two hooks that appear to check the same thing are
   both kept unless the §7.1 baseline shows identical interception sets across the whole corpus.
   Policy §2 corollary 2: the burden is on the merge, and "these look like the same check" is not
   the evidence.

Rule 4 is the asymmetry that makes this pattern safe. Everywhere else, condensation preserves
the union. For *authority*, it preserves the union of restrictions and the intersection of
permissions — the most restrictive reading in both directions.

---

## 5. Tool union and invocation mode

| Field | Merged how | Why |
|---|---|---|
| `allowed-tools` | **Union at the skill boundary, scoped per path** — §5.1 | A flat union grants every path every input's authority. |
| `disallowed-tools` | **Union** | A denial from any input applies to all. Denials never merge away. |
| Invocation mode / tier | **Most restrictive** | Policy §6. One user-invoked input fixes the merged skill. |
| `effort` | **Highest declared** | Effort is totally ordered. Downgrading changes behavior silently; a skill that asked for more asked for a reason. |
| `model` | **Not auto-resolved** — a recorded decision | §5.2. |
| `argument-hint` | **Preserved per entry point**, never merged | Two inputs with different argument shapes are two entry points, not one with a union of hints. |
| skill-scoped `agents/` | **Union, vendored** | Each agent keeps its own tool set; the skill does not inherit it. |

### 5.1 Tool union is not route-safe on its own

A flat union is the defect this section exists to close. Consider condensing a read-only input
(`Read`, `Grep`) with a writing one (`Bash`, `Write`):

```
input A: allowed-tools [Read, Grep]        ← read-only analysis path
input B: allowed-tools [Bash, Write]       ← writing path, hooks gate the writes

flat union: [Read, Grep, Bash, Write]      ← A's path can now Bash and Write
```

The hooks do **not** close this. B's hooks gate `Bash` and `Write` against B's *policy* — a
freeze boundary, a destructive-command check. They say nothing about whether A's execution path
should be reaching those tools at all. A's path was read-only by construction, and after
condensation it is not. Nothing in the transcript looks wrong; the tool was legitimately declared
and the hook legitimately passed it.

> **The union is the skill's outer bound. Within it, authority is scoped to the path that owns
> it.**

| Composed with | Scope unit |
|---|---|
| Pipeline | the **stage**. A stage holds its own tools; it does not inherit its siblings'. |
| Method library | the **playbook**. A playbook declares the tools its steps need. |
| Adapter set | the **adapter**. A credential-touching adapter's authority does not leak to a local one. |
| Panel | not applicable — seats hold no authority at all (§8). |

Where the harness cannot enforce per-path scoping, the condensation **splits into separate entry
points** rather than widening one. That is the same remedy `pipeline.md` §6 uses for the
prefix/writing split, and for the same reason: two authorities that cannot be separated inside one
skill are two skills.

E2 (policy §9) records the scoped result, not just the outer union. An authority diff showing only
the union hides exactly the widening this section forbids.

### 5.2 `model` has no total ordering

An earlier draft merged `model` as "highest declared," which assumes a total ordering over model
names that does not exist. `effort` is ordered; model identity is not — a newer small model and an
older large one are not comparable, and the harness's roster changes.

So: **a `model` conflict between inputs is not auto-resolved.** It is a decision recorded in the
condensation record (policy §10 section 4) with a reason. Where inputs agree, the shared value
carries. Where they disagree and no reason can be given, the condensation splits rather than
guessing — a model override exists because some input needed it, and silently overriding that is a
behavior change the record cannot justify after the fact.

---

## 6. Pattern-specific conformance evidence

In addition to policy E1–E7:

| # | Evidence |
|---|---|
| B1 | **Vendoring proof** — every hook command resolves inside the plugin. No path contains `$HOME/.claude/skills/` pointing outside it. Grep-checkable. |
| B2 | **Hook completeness** — every matcher from every input is present. Count and compare. |
| B3 | **Interception baseline (RED)** — each source skill's interception set, recorded per source before condensation. §7.1. |
| B4 | **Interception preservation (GREEN)** — the condensed skill's interception set equals the union of the sources', with a `Read`-only negative control and an unhooked convergence control. §7.2. |
| B5 | **Tier check** — the condensed skill is Tier 1 or Tier 2b, **never Tier 2a**. §3.1. |
| B6 | **Escalation check** — the router surfaces a miss on this skill rather than instructing a `Read`. §3.2. |
| B7 | **Collision order** — where two inputs hooked the same matcher, the record states the order and the blocking-beats-warning resolution. |
| B8 | **Scope check** — no execution path holds authority beyond what its own source input held. §5.1. Where the harness cannot enforce scoping, the record shows the split into separate entry points instead. |

---

## 7. B3 — testing behavior, not text

This is the pattern's form of policy E5, and it is the one where a documentation-shaped test is
worthless. Every other pattern's contrastive run compares *outputs*. Here the claim under test
is that an **effect occurs**, so the fixture must attempt the thing.

Policy E5 requires **both** gates. An earlier draft of this section specified only the second,
which meant it could confirm the condensed skill's hooks fire without establishing what the
source skills' hooks caught — so a condensation that silently dropped one input's interception
would still pass.

### 7.1 RED — source characterization

Run **each original source skill**, by invocation, before any condensation exists. For each,
record the **interception set**: which attempted operations it blocks, which it warns on, and
which it lets through untouched.

1. Build a fixed, versioned operation corpus spanning every matcher any input declares —
   destructive `Bash`, in-boundary `Edit`, out-of-boundary `Edit`, `Write`, and at least one
   operation no input hooks at all.
2. Run the corpus against each source skill separately. `careful` alone, `freeze` alone,
   `guard` alone.
3. Repeat to expose ordering nondeterminism where one skill declares two hooks on one matcher.
4. Persist each source's interception set as the baseline.

Step 2 is what makes a dropped hook detectable. Without a per-source baseline, "the condensed
skill blocks destructive `Bash`" cannot be distinguished from "the condensed skill blocks
destructive `Bash` *and silently stopped enforcing the freeze boundary*."

### 7.2 GREEN — extraction preservation

1. Install the condensed skill by **invoking** it — never by reading it.
2. Run the same corpus. Its interception set must be the **union** of every source's, operation
   for operation. An operation any source blocked, this must block. §4 rule 4's
   blocking-beats-warning resolution applies where sources disagree.
3. **Negative control:** perform the same attempts after only `Read`ing the skill. They must
   *not* be intercepted. A fixture where the read path also blocks is measuring something else —
   probably an unrelated global hook — and proves nothing about this skill.
4. **Convergence control (policy E5 rule 2):** the operation no source hooked must still pass
   unimpeded. A skill that blocks everything is not protecting, it is broken.
5. Any operation blocked by a source and passed by the condensed skill is a **P5 violation**,
   which policy §5.1 makes non-waivable. It blocks the condensation, not merely the retirement.

Step 3 of §7.2 is the step that makes this test meaningful at all. Without it, a passing result is
consistent with the hooks never having been installed.

---

## 8. Composition

| With | How |
|---|---|
| **Pipeline** | Overlay on stages. A stage's tools and hooks are the stage's; the pipeline unions them under §4–§5 and may not waive a stage's gate (`pipeline.md` §6). |
| **Panel** | Overlay on the convening skill. Seats run in subagent contexts and hold no authority of their own — a seat cannot carry hooks, and a persona file declaring any is malformed. |
| **Method library** | Overlay where a playbook needs tools. The playbook declares prerequisites; authority stays with the invoking skill. |
| **Adapter set** | Overlay, likely for credential-touching adapters — `agentcore` (AWS), `vercel-sandbox`. |

The panel row is a constraint worth stating positively: **authority lives in the convening
skill, never in a persona or playbook.** A persona is inert text by construction (`panel.md`
§6 C1–C10 depend on it), so authority cannot be smuggled in through a seat.

---

## 9. Candidate clusters

| Cluster | n | Note |
|---|---:|---|
| Safety | 4 | `careful`, `freeze`, `unfreeze`, `guard`. The pure case — this pattern alone. `guard` is already `careful` + `freeze` by reference, so condensation here is largely *fixing* an existing composition rather than creating one. `unfreeze` is the inverse of `freeze` and must remain separately reachable: a skill that can only ever restrict is a trap. |
| Ship & VCS | 17 | Overlay on `pipeline.md`. `/commit`, `/pr`, `/build-push-ecr` declare tools and MCP servers. |
| Setup & config | 8 | Overlay on `pipeline.md`. `update-config` and `fewer-permission-prompts` write `settings.json` — the file that configures hooks, which makes them capable of changing this pattern's own substrate. |

The setup & config note is the sharpest ordering hazard in the whole policy: a skill that edits
`settings.json` can alter the hooks that constrain it. Any condensation touching that cluster
must state whether the condensed skill can modify its own guard configuration, and if so, what
gates that (`pipeline.md` §3).
