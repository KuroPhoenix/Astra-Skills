# Pattern: Method Library

**Date:** 2026-07-29
**Status:** Draft — no cluster record written yet
**Selected when:** the **method** dimension carries ≥2 distinct values — cluster members gather
different evidence or run different tests. This pattern addresses the method difference only; where
the same cluster also differs at judgment or substrate, those select their own patterns and all of
them compose (policy §8). Nothing here assumes the priors are identical.
**Scope:** playbook mechanics — the playbook interface, how a method is selected, and the
contrastive form that proves two methods distinct.

**Governed by** `../condensation-policy.md`. That document owns eligibility, classification,
the six preservation obligations, the autonomy rule, composition and the seven universal
conformance evidence items.

---

## 1. Why this pattern exists

`tdd` is 36 lines and contains no persona at all. No `You are…`, no standing claim, no priors,
no register. All of it is method: the red→green loop, what a good test is, where seams go, the
anti-patterns, the rules of the loop. It already carries its detail one level down in
`tests.md` and `mocking.md`.

`bdd` (102 lines) and `spock` (243 lines) are the same shape pointed at Gherkin and at
Groovy/Spock respectively.

These three are not personas — none of them would reach a different *verdict* about whether
code is correct. They are three ways of *going looking*. Under a panel-only model they had
nowhere to live; under the policy's classification they are the method dimension, and this is
their representation.

`spock` also carries substrate (JVM + Groovy). Per policy §8 rule 4, that composes with
`adapter-set.md` rather than being flattened into the playbook.

---

## 2. Playbook interface

```yaml
playbook:
  id:            string
  preconditions: [<condition>]      # what must be true before this method can run
  inputs:        [<artifact kind>]  # what it operates on
  steps:         [<ordered step>]   # the method itself
  outputs:                          # what it produces, in a comparable shape
    findings:    [<finding kind>]
    artifacts:   [<produced file>]
  exit_criteria: [<condition>]      # when the method is complete
  prerequisites: [ { name, probe, on_absent } ]   # policy P6
```

`outputs.findings` is what makes distinctness testable (§4). A playbook whose outputs are
unspecified cannot be compared against another, and therefore cannot be shown to be distinct
from it — which under policy §2 corollary 2 means it is preserved by default, indefinitely.
Specifying outputs is how a playbook becomes eligible for merger.

A playbook holds **no standing**. It does not conclude; it gathers. When a panel seat runs a
playbook, the seat's persona owns the conclusion (`panel.md` §3). When a method library is
invoked standalone, the user owns it.

---

## 3. Method selection is a standing choice, not a per-invocation inference

This is the mechanic that separates a method library from a panel.

Seat selection is decided *per invocation* by the convening skill's roster (`panel.md` §3).
Method selection usually is not: whether a project does TDD or BDD is a property of the
project, decided once, changing rarely. Inferring it per invocation would re-decide a settled
question every time, and would let the agent quietly switch a project's testing discipline.

Selection ladder, in descending order of precedence:

1. **User-named** — `/astra:test --method bdd`. Highest precedence, because a one-off departure
   that a project declaration can override is not a departure at all. An earlier draft ranked
   project configuration first, which made the stated escape hatch unreachable in exactly the
   projects that declare a method — i.e. all the ones where it matters.
2. **Project declaration** — the project's own configuration or `CLAUDE.md` names the method. The
   expected common case, and the default whenever the user has not asked for something else.
3. **Precondition elimination** — if a playbook's `preconditions` cannot be satisfied (no JVM
   present for `spock`), it is not a candidate. Mechanical, not inferential.
4. **Index lookup** — `playbooks/INDEX.md`, read only when the above leave more than one
   candidate. This is the path that can degrade, so it is last.

Rules 1 and 3 interact: a user-named method whose preconditions fail **raises**. It does not
silently fall back to the project default. The user named a method; being unable to run it is
information they need, not a problem to route around (policy P6 — absence must be loud).

If step 4 leaves ambiguity, the skill asks. It does not guess: silently choosing a testing
discipline is a decision with a long tail that the user never approved.

---

## 4. Distinctness — the contrastive form

Policy §4 defines the method row: two methods are distinct when, run on the same artifact,
they yield **different supported findings — not merely different prose**.

Policy E5's five universal rules apply. Their method-library form is:

1. Fix at least three versioned artifacts. Include at least one **expected-divergence** case
   (an artifact where the two methods should surface different findings) and one
   **convergence control** (an artifact where they should surface the same findings, and where
   manufactured difference is itself a failure).
2. Run each **original source skill** blind on identical artifacts. A characterization wrapper
   may add only the finding output schema — never a hint about the other method or the expected
   result.
3. Repeat each fixture three times. A divergence fixture passes when the finding sets differ in
   at least two of three runs; a convergence control passes when they do not differ in at least
   two of three.
4. Compare **supported finding sets**, not verdicts. Two methods that reach the same verdict
   from different evidence are still distinct — policy P3 preserves both because losing one
   loses its evidence.
5. After extraction, rerun the corpus against the extracted playbook and require that every
   source finding still appears. Any loss blocks retirement of the source skill.

Rule 4 is where this test differs most sharply from the panel's. A panel fixture compares
`stance.disposition` — the conclusion. A method fixture compares evidence, because two methods
are *supposed* to agree on the conclusion. Comparing verdicts here would merge everything.

---

## 5. Composition

| With | How |
|---|---|
| **Panel** | Vertically. A seat is persona × playbook × jurisdiction; the library is where its playbook comes from. Policy §8 rule 3. |
| **Adapter set** | Beneath. A playbook declares prerequisites; any adapter satisfying them may run it, subject to that set's parity matrix. Policy §8 rule 4. `spock` is the live case. |
| **Pipeline** | Inside a stage. A pipeline stage may select a method without the pipeline knowing which. |
| **Behavior preservation** | Overlay, if any source skill carried frontmatter behavior. |

---

## 6. Pattern-specific conformance evidence

In addition to policy E1–E7:

| # | Evidence |
|---|---|
| M1 | Every absorbed method is reachable through the §3 ladder. A method that no path selects has been silently dropped, violating P1. |
| M2 | Every playbook declares `outputs.findings`. Unspecified outputs make M3 unrunnable. |
| M3 | Extraction preservation: the extracted playbook reproduces every source finding on the §4 corpus. |
| M4 | No playbook asserts a conclusion. A playbook containing a verdict has absorbed persona content and must be re-split. |

M4 is the anti-drift check. The failure mode for this pattern is a playbook slowly acquiring
opinions until it is a persona in a method's clothing — at which point it belongs in a panel
and the library has silently become a roster.

---

## 7. Cost

One playbook is loaded per invocation. Cost is `chassis + playbook`, independent of how many
playbooks the library holds — the unselected ones are files on disk (`README.md`, Principles §1 — files
inside a skill cost zero until read).

This is the cheapest pattern, and the contrast with the panel is instructive: a panel pays
`O(N·P + N²·C)` because every seat speaks. A method library pays for one method because
methods are not convened, they are chosen. Adding the twentieth playbook to a library costs
nothing at runtime; adding the sixth seat to a panel does not.

No measurement gate is required before implementation planning for this pattern. Policy E5
still applies to distinctness claims.

---

## 8. Candidate clusters

From the collision map (`README.md`, *"The collision map"*), pending records:

| Cluster | n | Note |
|---|---:|---|
| Testing | 7 | `tdd`, `bdd`, `spock`, `nextjs-test`, `bats-testing-patterns`, `verification-before-completion`. `spock` and `nextjs-test` carry substrate; composes with adapter-set. |
| Debug & incident | 9 | `investigate`, `diagnosing-bugs`, `systematic-debugging`, `rca`, `firefighting`, `java-leak-resolver`, `staging-debug`, `local-debug`, `triage`. **Check for judgment before assuming method-only** — `firefighting` (290 lines) is interactive incident response and may carry priors about stabilization-before-diagnosis that a post-hoc `rca` does not. |
| Codebase comprehension | 5 | `how`, `code-tracing`, `codebase-design`, `improve-codebase-architecture`, `code-explorer`. `code-tracing` is 11 agent-fired invocations — the most-used live skill in `~/.claude/skills/`. |

The debug cluster note is the important one: **this pattern must not become the default for
anything that looks procedural.** Classification (policy §4) runs first, and a cluster with two
distinct priors is a panel whose seats happen to run different playbooks, not a method library.
