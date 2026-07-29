# Pattern: Behavior Preservation

**Date:** 2026-07-29
**Status:** Draft — no cluster record written yet
**Selected when:** any cluster member declares frontmatter behavior — `hooks`, `allowed-tools`,
`effort`, or a model override.
**Scope:** how authority survives condensation — hook vendoring, hook union and collision, tool
union, tier constraint, and the escalation path that replaces a `Read` for behavior-bearing
skills.

**Governed by** `../condensation-policy.md`. That document owns eligibility, classification,
the six preservation obligations, the autonomy rule, composition and the seven universal
conformance evidence items.

---

## 1. This is an overlay, not an alternative

Every other pattern is selected *instead of* the others. This one is selected *in addition*
(policy §8 rule 1). A ship pipeline whose stages declare tools gets pipeline mechanics **and**
these. A panel whose seats need `AskUserQuestion` gets panel mechanics **and** these.

It appears alone only when a cluster's members differ at no other dimension — which the safety
cluster is: `careful`, `freeze`, `unfreeze`, `guard` share priors, method and subject, and
differ solely in what they are permitted to do.

---

## 2. Reading a skill is not invoking it

The constraint everything here follows from. `README.md:232` states it; this is the operative
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

### 3.1 Tier 1 is mandatory

> A skill declaring `hooks`, `allowed-tools`, `effort`, or a model override **must be Tier 1**.
> It can never be serviced through the router's miss handler.

This follows directly from §2: the miss handler works by instructing the agent to `Read` a cold
skill's `SKILL.md` (`README.md:217`), and a `Read` confers none of the above. Demoting a
behavior-bearing skill to Tier 2 does not make it cheaper — it makes it inert while appearing
present.

### 3.2 Escalation replaces the read

When the router meets a miss on a behavior-bearing skill it does **not** read it. It surfaces
the miss:

> *"This needs `/astra:guard`. Type it."*

That still records demand — the router consulted the skill, which is a `Read`-adjacent signal
`/astra-tune` can mine (`README.md:312`) — without pretending a `Read` conferred a boundary it
cannot confer. `README.md:179` §4 is satisfied: the skill is one hop away, not lost.

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
5. **A hook may not be dropped for redundancy.** Two hooks that appear to check the same thing
   are both kept unless a contrastive run (§6 B3) demonstrates identical behavior on the corpus.
   Policy §2 corollary 2: the burden is on the merge.

Rule 4 is the asymmetry that makes this pattern safe. Everywhere else, condensation preserves
the union. For *authority*, it preserves the union of restrictions and the intersection of
permissions — the most restrictive reading in both directions.

---

## 5. Tool union and invocation mode

Two different rules, easily conflated:

| Field | Merged how | Why |
|---|---|---|
| `allowed-tools` | **Union** | Each input already held its own tools. `careful` needs `Bash`; `freeze` needs `Edit`/`Write`; `guard` needs all three. Intersecting would break the merged skill. Bounded by policy §6: the union of inputs, never one tool beyond it. |
| Invocation mode | **Most restrictive** | Policy §6. One user-invoked input fixes the merged skill as user-invoked. |
| `effort` / model override | **Highest declared** | Downgrading changes behavior silently; a skill that asked for more effort asked for a reason. |

The `allowed-tools` union is safe *because* the hooks travel with it. `guard` holding `Edit` is
not a widened permission — it is `Edit` plus the freeze check that gates it. Union the tools and
the hooks together, or neither.

---

## 6. Pattern-specific conformance evidence

In addition to policy E1–E7:

| # | Evidence |
|---|---|
| B1 | **Vendoring proof** — every hook command resolves inside the plugin. No path contains `$HOME/.claude/skills/` pointing outside it. Grep-checkable. |
| B2 | **Hook completeness** — every matcher from every input is present. Count and compare. |
| B3 | **The hook actually fires.** For each hook, a run that triggers its matcher is blocked or warned as declared. §7. |
| B4 | **Tier check** — the condensed skill is Tier 1. A behavior-bearing skill with `disable-model-invocation: true` fails. |
| B5 | **Escalation check** — the router surfaces a miss on this skill rather than instructing a `Read`. §3.2. |
| B6 | **Collision order** — where two inputs hooked the same matcher, the record states the order and the blocking-beats-warning resolution. |

---

## 7. B3 — testing behavior, not text

This is the pattern's form of policy E5, and it is the one where a documentation-shaped test is
worthless. Every other pattern's contrastive run compares *outputs*. Here the claim under test
is that an **effect occurs**, so the fixture must attempt the thing.

Fixture form:

1. Install the condensed skill by **invoking** it — never by reading it. Reading it is the
   negative control.
2. For each hook, attempt an operation its matcher covers and that it should stop.
   - `careful`-descended: a destructive `Bash` command must be intercepted.
   - `freeze`-descended: an `Edit` outside the boundary must be intercepted, and one inside it
     must pass.
3. **Negative control:** perform the same attempts after only `Read`ing the skill. They must
   *not* be intercepted. A fixture where the read path also blocks is measuring something else
   — probably an unrelated global hook — and proves nothing about this skill.
4. **Convergence control (policy E5 rule 2):** an operation no hook covers must pass unimpeded.
   A skill that blocks everything is not protecting, it is broken.
5. Repeat to expose ordering nondeterminism where two hooks share a matcher.

Step 3 is the step that makes this test meaningful. Without it, a passing result is consistent
with the hooks never having been installed at all.

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
