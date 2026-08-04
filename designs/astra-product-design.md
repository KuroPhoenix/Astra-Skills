# Astra Product Design — phase-0 design

**Date:** 2026-08-01 · **Reviewed/amended:** 2026-08-03 · **Wave:** 1 · **Status:** `proposed`

> **Authority.** `docs/design-requirements.md` governs this document; `docs/phase-0.md` owns phase
> scope and the global ledgers; `docs/design-roadmap.md` section 10 (amendment 3) supplies this
> wave's triage. This is one per-skill design. It is not an implemented skill, and it authorizes no
> retirement.
>
> **Conformance.** Sections 1–10 map one-to-one and in order onto `docs/design-requirements.md`
> sections 7.1–7.10. Self-reviewed against that document's section 11 checklist.
>
> **Certainty labels.** **O** = observed in an inspected artifact, **I** = inferred and still
> needing confirmation, **U** = unavailable.
>
> **Provenance note.** Both primary sources are *generated* files. Their `SKILL.md.tmpl` templates,
> not the `SKILL.md` outputs, are the authored source of truth. Section 3.1 records both, and
> section 4 explains why the distinction changes this design's central claim.

---

## 1. Identity and status

| Field | Value |
|---|---|
| Provisional Astra name | `astra-product-design` |
| Status | `proposed` |
| Priority | `now` |
| Candidate neighborhood | Design & visual (primary); Plan & spec inspected for `prototype` without claiming it |
| User job | **When I want to establish a product's visual design direction, get it approved, and record it as the project's design contract.** |
| Critique handoff acceptance | **yes** — see section 7.4 |

**The job expresses one outcome.** It does not need an `or`. Establishing a direction, approving it,
and recording it are three stages of producing one artifact — an approved direction — not three
independent outcomes. The recording stage is optional in the interface (section 2) but it is not a
second job: an unrecorded approved direction is the same outcome in a weaker delivery state.

**Name and promise.** The user confirmed the name `astra-product-design` and narrowed the promise
(`docs/design-roadmap.md` section 10.2). This design therefore claims **design direction**, not
product discovery or product strategy. The sources establish aesthetic direction, explore screen
variants, and write a design contract; neither performs discovery, positioning, roadmapping, or
prioritization. `design-consultation` explicitly *routes discovery away*: when the codebase is empty
and purpose is unclear it tells the user to run `/office-hours` first
(`design-consultation/SKILL.md.tmpl:L91`, **O**). That routing is the boundary evidence, and this
design preserves it.

**Personal value: explicit.** The user selected the Design tranche as Wave 1 and approved the skill
split and name; `docs/design-roadmap.md` section 4 records that selection. Supporting inferred
value (**I**): every other Wave 1 peer consumes this skill's output — Interface implements the
approved direction and Brand supplies constraints to it — so the direction artifact is a
prerequisite for the tranche rather than a leaf.

---

## 2. Interface and scope

### 2.1 Requests that should trigger it

- "Establish the visual direction for this project" / "create the design-direction contract in
  DESIGN.md" / "design from scratch". A generic "set up a design system" request triggers this
  skill only when the user wants direction and approval, not token or component implementation.
- "Show me some design options for this screen" / "explore design variants" / "visual brainstorm"
- "I don't like how this looks" *about a running page*, where the user wants alternative directions
  rather than a defect report
- "What should this product look like?"

### 2.2 Nearby requests that should not

| Request | Correct owner | Why |
|---|---|---|
| "Build this screen in React/Tailwind" | `astra-interface` | Implementation, not direction |
| "Turn the approved mockup into production HTML" | `astra-interface` | `design-html` is the downstream adapter |
| "Define our logo rules, voice, and brand primitives" | `astra-brand` | Durable identity outlives any one product direction |
| "Review this interface and tell me what's wrong" | `astra-critique` | Report on an existing artifact, not a new direction |
| "Try three ways to structure this reducer and keep the winner" | `prototype` (retained independent) | Throwaway experiment whose artifact is discarded |
| "What did we decide about spacing last month?" | `astra-knowledge` / `astra-document` | Retrieval, not decision |

The `astra-critique` boundary is the sharpest and the easiest to get wrong, because
`plan-design-review` and `design-review` share template partials with this skill's sources (section
4.3). The distinguishing question is **whether an approved direction already exists**: if the user
wants a judgment about an artifact, that is Critique; if the user wants a direction to exist, that
is this skill.

### 2.3 Accepted artifact or context

A product context, at whatever fidelity is available: a codebase, a `README.md`, prior
`/office-hours` output, an existing `DESIGN.md`, a running local site, a screenshot, or nothing but
a spoken description. All seven are observed intake paths across the two sources (**O**).

### 2.4 User-visible result

1. An **approved visual direction**, seen as rendered mockups rather than described in prose.
2. Optionally, a **root `DESIGN.md`** recording product context, aesthetic direction, typography,
   color, spacing, layout, motion, and a decisions log — or, in plan mode, that content written into
   the plan file rather than to disk.
3. **Durable artifacts** under `~/.gstack/projects/$SLUG/designs/…`: the variant images, an
   `approved.json`, and an updated taste profile.
4. An explicit statement of what was assumed when context was thin.

### 2.5 Non-goals

- Producing production code, components, or tokens — Interface owns that.
- Defining brand identity, voice, logo policy, or brand primitives — Brand owns that.
- Deck or presentation output — Interface owns that after amendment 3.
- Product discovery, positioning, or strategy — outside the roster's Design tranche entirely.
- Reviewing or auditing an existing interface — Critique owns that.
- Deleting, disabling, or replacing any source. Phase 0 forbids it.

### 2.6 Decisions that remain with the user

Whether to research the category; which concepts to generate and how many; which variant wins;
which risks to take; whether coherence warnings are accepted or overridden; whether `DESIGN.md` is
written at all, and whether to disk or into a plan file; and whether any downstream workflow starts.
Both sources already return every one of these to the user, and both forbid the agent from blocking
on disagreement (`design-consultation/SKILL.md.tmpl:L213`, `design-shotgun/SKILL.md.tmpl:L341`,
**O**).

---

## 3. Source evidence

### 3.1 Inspection record

Inspected 2026-08-01 and re-reviewed through the authored generator inputs on 2026-08-03.
gstack sources are at commit `a3259400a366593e0c909dd9ac3e59752efd2488`, release
`1.60.1.0`; the tree was clean during re-review and live registrations point into
`~/.claude/skills/gstack/`.

**Primary sources — claimed by this design.**

| Identifier | Component type | Location | Invocation | Availability | Lines | `sha256` prefix |
|---|---|---|---|---|---:|---|
| `design-consultation` | skill (generated) | `~/.claude/skills/gstack/design-consultation/SKILL.md` | `/design-consultation` | live | 1230 | `44379ed9283c` |
| `design-consultation` | **template (source of truth)** | `…/design-consultation/SKILL.md.tmpl` | not invocable | live | 214 | `0568266027d7` |
| `design-consultation` §3–6 | section (generated) | `…/sections/proposal-and-preview.md` | read on demand | live | 408 | `90396a78db3b` |
| `design-consultation` §3–6 | **section template** | `…/sections/proposal-and-preview.md.tmpl` | not invocable | live | 294 | `adbcb43dbc8c` |
| `design-consultation` | section manifest | `…/sections/manifest.json` | passive registry | live | 14 | `bdae65759579` |
| `design-shotgun` | skill (generated) | `~/.claude/skills/gstack/design-shotgun/SKILL.md` | `/design-shotgun` | live | 1373 | `513d9e18dbe5` |
| `design-shotgun` | **template (source of truth)** | `…/design-shotgun/SKILL.md.tmpl` | not invocable | live | 344 | `ce541362b85e` |

**Generator and resolver sources — inspected, claimed by no design.**

| Identifier | Component type | Lines | `sha256` prefix | Bearing on this design |
|---|---|---:|---|---|
| `scripts/gen-skill-docs.ts` | build generator | 1230 | `cd62a5046ee6` | Expands every `{{…}}` placeholder and makes both `SKILL.md` files derived artifacts |
| `scripts/resolvers/index.ts` | resolver registry | 105 | `9e07dfe5a4ec` | Maps every placeholder below to its source resolver |
| `scripts/resolvers/design.ts` | design resolver library | 1157 | `15bb7329e323` | Authored definitions of `DESIGN_SETUP`, `TASTE_PROFILE`, `UX_PRINCIPLES`, `DESIGN_OUTSIDE_VOICES`, and `DESIGN_SHOTGUN_LOOP` |
| `scripts/resolvers/preamble.ts` | host-chassis resolver | 124 | `d6e6e2f5cd68` | Entry point for the large generated `PREAMBLE`; this upstream sharing is not Astra maintenance value |
| `scripts/resolvers/browse.ts` | browser resolver library | 138 | `70226a0c6c2a` | Defines `BROWSE_SETUP` and its setup/degradation behavior |
| `scripts/resolvers/gbrain.ts` | optional memory resolver library | 270 | `57991423d881` | Defines `GBRAIN_CONTEXT_LOAD` and `GBRAIN_SAVE_RESULTS` |
| `scripts/resolvers/learnings.ts` | optional learnings resolver library | 117 | `cf67cf308faf` | Defines `LEARNINGS_SEARCH` and `LEARNINGS_LOG` |
| `scripts/resolvers/utility.ts` | utility resolver library | 417 | `9f71ca8edea7` | Defines `SLUG_EVAL`; `BIN_DIR` is a direct path resolver in `index.ts` |

The two primary templates and the consultation section template consume the following complete
placeholder set. This is the build-input accounting that the generated-file finding requires:

| Placeholder | Consumers here | Phase-0 treatment |
|---|---|---|
| `PREAMBLE` | both primary templates | Shared gstack host chassis. Track with the generation pipeline; do not count its generated duplication as a merger benefit |
| `BROWSE_SETUP` | consultation | Preserve browser discovery, user-approved setup, and degradation or replace them explicitly |
| `DESIGN_SETUP` | both | Preserve designer/browser discovery and the no-designer HTML fallback |
| `GBRAIN_CONTEXT_LOAD`, `GBRAIN_SAVE_RESULTS` | consultation | Optional gbrain integration; preserve optionality and non-blocking failure, not the gstack implementation |
| `LEARNINGS_SEARCH`, `LEARNINGS_LOG` | consultation | Optional source-learnings integration; later design must retain, replace, or explicitly drop it with evidence |
| `SLUG_EVAL`, `BIN_DIR` | consultation / shotgun | State-path and helper discovery; retain or replace before source retirement |
| `TASTE_PROFILE` | both | Product-specific durable taste state and migration behavior; must survive in this design |
| `DESIGN_OUTSIDE_VOICES` | consultation | Optional external design voices with host-specific suppression and non-blocking degradation |
| `UX_PRINCIPLES` | shotgun | Shared usability priors consumed by Product, Interface, and Critique sources; see section 4.3 |
| `DESIGN_SHOTGUN_LOOP` | both | Shared comparison, feedback, approval, and `approved.json` machinery |

**Cross-neighborhood sources — inspected as evidence, primary claim not taken.** Generated gstack
skills list both their runtime output and their authored template.

| Identifier | Component type | Location / invocation / availability | Lines and provenance | Primary home | Role here |
|---|---|---|---|---|---|
| `design` | skill | `~/.claude/skills/design/SKILL.md`; `design`; live | 313; `413f4ab913d0` | `astra-brand` | Mockup jurisdiction; proposed secondary role only |
| `ui-ux-pro-max` | skill | `~/.claude/skills/ui-ux-pro-max/SKILL.md`; `ui-ux-pro-max`; live | 685; `adcc153bf7d8` | `astra-interface` | Independent usability source used to test the shared `UX_PRINCIPLES` classification |
| `plan-design-review` | generated skill + authored template | `~/.claude/skills/gstack/plan-design-review/{SKILL.md,SKILL.md.tmpl}`; `/plan-design-review`; live | 1514 / 294; `0f756585231f` / `412bb57ed787` | `astra-critique` | Shares three build partials; different review outcome |
| `design-html` | generated skill + authored template | `~/.claude/skills/gstack/design-html/{SKILL.md,SKILL.md.tmpl}`; `/design-html`; live | 1511 / 600; `ed44f14e570b` / `5d885cf8da57` | `astra-interface` | Downstream implementation adapter; different outcome |
| `prototype` | skill | `~/.agents/skills/prototype/SKILL.md`; `prototype`; live | 26; `03074862d4b6` | retained independent | Different, throwaway-experiment outcome; consumed, not owned |
| `prototype/LOGIC.md` | reference | `~/.agents/skills/prototype/LOGIC.md`; read by `prototype`; live | 79; `cf372862bccd` | retained with `prototype` | Logic-prototype playbook only |
| `prototype/UI.md` | reference | `~/.agents/skills/prototype/UI.md`; read by `prototype`; live | 112; `e2ca04434be5` | retained with `prototype` | UI-prototype playbook only |
| `prototype/agents/openai.yaml` | interface metadata | `~/.agents/skills/prototype/agents/openai.yaml`; not independently invocable; live | 3; `5af65e43ab41` | tracked with `prototype` | Display metadata only; **not** a separate execution context |

**Complete primary declarations.** Descriptions are reproduced in substance without changing their
trigger claims; every other field and nested query field is listed exactly.

| Field | `design-consultation` | `design-shotgun` |
|---|---|---|
| `name` | `design-consultation` | `design-shotgun` |
| `version` | `1.0.0` | `1.0.0` |
| `preamble-tier` | `3` | `2` |
| `description` | Product research and a complete aesthetic/type/color/layout/spacing/motion system; preview generation; writes `DESIGN.md`; routes existing-site audit to `/plan-design-review`; triggers on design system, brand, and `DESIGN.md` work | Multiple AI variants, comparison board, structured feedback, iteration; standalone exploration; triggers on variants/options/brainstorming or dissatisfaction with a current look |
| `allowed-tools` | Bash, Read, **Write**, **Edit**, Glob, Grep, AskUserQuestion, **WebSearch** | Bash, Read, Glob, Grep, **Agent**, AskUserQuestion |
| `triggers` | design system · create a brand · design from scratch | explore design variants · show me design options · visual design brainstorm |
| `gbrain.schema` | `1` | `1` |
| `gbrain.context_queries` | `existing-design-md`: filesystem, `DESIGN.md`, tail 1, render `Existing DESIGN.md (if any)`; `prior-design-decisions`: filesystem, `~/.gstack/projects/{repo_slug}/*-design-*.md`, mtime descending, limit 3; `brand-guidelines`: list of `ceo-plan` records tagged `repo:{repo_slug}` containing `brand`, updated descending, limit 3 | `prior-approved-variants`: filesystem, `~/.gstack/projects/{repo_slug}/designs/*/approved.json`, mtime descending, limit 5; `design-md`: filesystem, `DESIGN.md`, tail 1; `recent-design-docs`: filesystem, `~/.gstack/projects/{repo_slug}/*-design-*.md`, mtime descending, limit 3; each retains its declared `render_as` label |

**Complete cross-source declaration inventory.** `design` declares `name`, `description`,
`argument-hint`, `license: MIT`, and `metadata.{author: claudekit, version: 2.1.0}`.
`ui-ux-pro-max` declares only `name` and `description`. `plan-design-review` declares `name`,
`preamble-tier: 3`, `interactive: true`, `version: 2.0.0`, `description`, `allowed-tools`, and three
`triggers`. `design-html` declares `name`, `preamble-tier: 2`, `version: 1.0.0`, `description`,
three `voice-triggers`, three `triggers`, and `allowed-tools`. `prototype` declares `name`,
`description`, and `interface.{display_name, short_description}`; its three-line `openai.yaml`
repeats only the two interface display fields.

The declaration difference is evidence of different pre-approved capabilities, not an enforced
filesystem boundary: Shotgun's Bash access can still write. Section 5.1 therefore preserves an
explicit **forbidden-effect contract** for Explore and a user-confirmed mutation contract for
Record; detailed permission enforcement remains deferred.

### 3.2 Disposition and contribution

Contribution categories are from `docs/design-requirements.md` section 5.

| Occurrence | Primary disposition | Primary home | Contribution | Secondary role |
|---|---|---|---|---|
| `design-consultation` (`cm-design-and-visual-03`) | proposed Astra design | `astra-product-design` | **Protocol** (research-led proposal ordering) · **Playbook** (competitive research, three-layer synthesis, coherence validation, anti-slop self-gate) · **Perspective** (opinionated consultant priors: propose don't present, coherence over local optima, font blacklist) · **Jurisdiction** (the root `DESIGN.md` contract) · **Machinery** (generated preamble) | — |
| `design-shotgun` (`cm-design-and-visual-05`) | proposed Astra design | `astra-product-design` | **Protocol** (concept → confirm → parallel generate → board → confirm → save) · **Playbook** (anti-convergence test, parallel generation with retry and fallback, taste memory) · **Prerequisite** (`$D` designer binary, `Agent` capability, feedback endpoint) · **Machinery** (generated preamble) | —; `UX_PRINCIPLES` is tracked as a separate shared build input, not misattributed as an Interface-owned behavior of this occurrence |
| `design` mockup slice (`cm-design-and-visual-01`) | proposed Astra design | `astra-brand` *(unchanged)* | **Jurisdiction** (mockups) | **`astra-product-design`** — secondary role only |
| `ui-ux-pro-max` (`cm-design-and-visual-08`) | proposed Astra design | `astra-interface` *(unchanged)* | **Perspective** (usability priors) | `astra-product-design` — evidence only, no claim |
| `plan-design-review` (`cm-adversarial-critique-13`) | proposed Astra design | `astra-critique` | **Separate** review outcome · shared build machinery | Evidence only; no Product claim |
| `design-html` (`cm-design-and-visual-04`) | proposed Astra design | `astra-interface` | **Separate** implementation outcome · downstream adapter | Named handoff only; no Product claim |
| `prototype` (`cm-plan-and-spec-13`) | independent reference | retained independent | **Separate** — different outcome | Consumed, not owned |

### 3.3 Proposed ledger changes

Amendment 3 already proposes the neighborhood-level rows (`docs/design-roadmap.md` section 10.5).
This design adds or refines three. The coordinator applied them as `claimed`, not `resolved`, on
2026-08-03 after review:

| Occurrence ID | Field | Proposed value | Basis |
|---|---|---|---|
| `cm-design-and-visual-03` | `evidence` | Replace `source inspection pending` with a link to section 3.1 of this design, recording **both** the generated `SKILL.md` hash `44379ed9283c` and the authoritative `SKILL.md.tmpl` hash `0568266027d7` | The generated file is not the source of truth; recording only its hash would make the provenance rule satisfiable by a derived artifact |
| `cm-design-and-visual-05` | `evidence` | Same treatment: `513d9e18dbe5` (generated) plus `ce541362b85e` (template) | As above |
| `cm-design-and-visual-05` | `secondary_roles` | Remove the Amendment 1 `astra-interface` role. `UX_PRINCIPLES` is a resolver-owned build input consumed by four skills across three homes, not authored `design-shotgun` content and not evidence that Interface owns part of this occurrence | Section 4.3 |

**Separate installed-component record.** The build generator and resolver library are not
collision-map occurrences. The coordinator records one generation-pipeline component globally and
this design enumerates its exact consumed placeholders above. The record stays shared and retained
until every generated consumer that matters to the roster has migrated; it does not assign one Astra
design as exclusive owner of a resolver partial.

| Component | Type | Consumers / treatment |
|---|---|---|
| `gstack:skill-doc-generation-pipeline` | build generator + resolver modules | Every generated gstack skill; retain as shared provenance. For this design the consumed placeholder set is the table in section 3.1 |

The reference ledger also adds `prototype` with disposition `unassigned` pending the user's
`keep` / `defer` / `exclude` decision and `consuming_designs: [astra-product-design]`.

---

## 4. Collision analysis

### 4.1 Why the sources appeared duplicative — and why that appearance was an artifact

Amendment 1 recorded that 942 lines are byte-identical between `design-consultation` and
`design-shotgun` — 76.6% and 68.6% of each — concluded that "the remaining divergence is two
protocols over one outcome", and called this **"the best-evidenced merger currently proposed"**
(`docs/design-roadmap.md` section 8.2).

**That measurement is of generated output.** Independent measurement here finds 988 identical lines
by multiset intersection, of which **738 fall inside the generated preamble region alone**
(`design-shotgun/SKILL.md` lines 50–790, of 741 lines in that region). Both files are produced from
`.tmpl` templates by `bun run scripts/gen-skill-docs.ts`; the preamble is injected by the
`{{PREAMBLE}}` placeholder at tier 3 and tier 2 respectively.

Measured against the **authored** templates, the two sources share **95 lines, of which 36 are
non-blank** — and those 36 are:

- YAML frontmatter keys and shared tool entries (`allowed-tools:`, `- Bash`, `- Read`, `- Glob`,
  `- Grep`, `- AskUserQuestion`, `kind: filesystem`, `schema: 1`, `version: 1.0.0`);
- Markdown fence markers and `---` rules;
- three placeholders — `{{PREAMBLE}}`, `{{DESIGN_SETUP}}`, `{{TASTE_PROFILE}}`; and
- exactly **two** instruction lines: a `ls src/ app/ pages/ components/` probe and a
  `ls ~/.gstack/projects/$SLUG/*office-hours*` probe, plus a zsh-compat line and the heading
  `## Important Rules`.

**Consequence.** The duplication amendment 1 cited is not authored duplication that a merged Astra
skill would remove. It is template expansion that gstack's own generator already deduplicates, and
it would disappear from both files on the next regeneration without any Astra work. **This design
therefore does not claim maintenance as its advantage**, and section 9 does not offer a
deduplication gate. The merger survives on entirely different evidence, given below. This is the
`guard` lesson from amendment 2 recurring in a second neighborhood: the `SKILL.md` is not the
component.

### 4.2 What behavior is actually shared

Three things, all of them real:

1. **One outcome.** Both sources terminate at an approved visual direction. `design-consultation`
   reaches it through a proposal the user adjusts; `design-shotgun` reaches it through variants the
   user ranks. Neither produces anything else as its primary result.
2. **One approval loop, literally the same code.** Both invoke `{{DESIGN_SHOTGUN_LOOP}}` — the
   comparison board, per-variant ratings, feedback capture, and `approved.json` write
   (`design-shotgun/SKILL.md.tmpl:L302`; `sections/proposal-and-preview.md.tmpl:L152`, **O**). The
   approval half of the job is already unified upstream; only the generation half diverges.
3. **One durable state model.** Both read and write `~/.gstack/projects/$SLUG/designs/`, both read
   `DESIGN.md` as a default constraint, and both consult the same taste profile
   (`{{TASTE_PROFILE}}`).

### 4.3 Aliases, shallow delegation, and one genuinely wrong belief

Neither source is an alias or a stub. But inspection found a **conflict between the two sources'
instructions**, which `docs/design-requirements.md` section 7.4 requires reporting:

> `design-shotgun` states: *"When design-shotgun is invoked from plan-design-review,
> design-consultation, or another skill, the calling skill has already gathered context. Check for
> `$_DESIGN_BRIEF` — if it's set, skip to Step 2"* (`design-shotgun/SKILL.md.tmpl:L91-L93`, **O**).
>
> `design-consultation` never invokes `design-shotgun`. Its Phase 5 Path A calls
> `$D variants --brief … --count 3 --output-dir …` directly and then inlines the same
> `{{DESIGN_SHOTGUN_LOOP}}` partial (`sections/proposal-and-preview.md.tmpl:L132`, `L152`, **O**).

So `design-shotgun` believes `design-consultation` calls it; `design-consultation` reimplements the
generation step instead and shares only the approval partial. **That is a live defect, not a design
choice** (**O** for both instruction sets; **I** that the divergence is unintended). It is also the
strongest merger evidence available, because it is a duplication a merged skill genuinely removes —
unlike the generated preamble, which it does not.

**A second, larger finding: shared build inputs cross Astra home boundaries.** Four design-specific
partials are consumed across homes (the product-internal `TASTE_PROFILE` is accounted for in
section 3.1 separately):

| Partial | Consumers | Proposed Astra homes spanned |
|---|---|---|
| `DESIGN_SETUP` | `design-consultation`, `design-shotgun`, `design-html`, `design-review`, `plan-design-review` | Product Design · Interface · Critique |
| `UX_PRINCIPLES` | `design-shotgun`, `design-html`, `design-review`, `plan-design-review` | Product Design · Interface · Critique |
| `DESIGN_SHOTGUN_LOOP` | `design-shotgun`, `design-consultation`, `plan-design-review` | Product Design · Critique |
| `DESIGN_OUTSIDE_VOICES` | `design-consultation`, `design-review`, `plan-design-review` | Product Design · Critique |

Amendment 1 recorded that `design-shotgun` "carries a usability **perspective** … that overlaps
`ui-ux-pro-max`; Product and Interface must agree on one primary home for those priors"
(`docs/design-roadmap.md` section 5.4). **That is the wrong accounting model.** `design-shotgun`
references a resolver partial that four skills reference, two of which (`design-review` and
`plan-design-review`) are `astra-critique` sources. A build partial is not a collision occurrence and
does not need one exclusive Astra primary home. Each consuming design must classify the behavior it
actually uses and preserve or reject it explicitly; the coordinator tracks all consumers. A shared
Astra runtime module remains forbidden until at least two completed designs demonstrate the same
interface and variation. Section 10 records that roster-wide classification question.

### 4.4 Which apparent duplicates are different jobs

None of the claimed pair. But two adjacent things are different jobs and are not claimed:

- **`prototype`** produces a throwaway experiment and promotes only the learned decision, discarding
  the artifact (`prototype/SKILL.md:L8-L26`, **O**). This skill's artifacts are the point. Different
  outcome; retained independent, consumed if the user has findings.
- **`plan-design-review`** judges an existing design against user hierarchy and journey. Sharing
  three partials with this skill's sources does not make it the same job; a shared board widget is
  machinery, and machinery does not establish a shared outcome — which is precisely the reasoning
  section 4.1 applies to the preamble.

### 4.5 Where the sources conflict

| Conflict | `design-consultation` | `design-shotgun` | Resolution proposed |
|---|---|---|---|
| Who generates variants | `$D variants --count 3` in one call | N parallel `Agent` subagents, each running `$D generate` with retry, quality check, and verification | Adopt shotgun's protocol; keep consultation's single call as the first degradation rung (section 6.3) |
| Failure handling | none stated for `$D variants` | 3 retries on rate limit, regenerate on empty output, quality gate, sequential fallback, explicit per-variant failure reporting, never silently skip | Adopt shotgun's; this is the primary advantage claim |
| Anti-slop control | **self-gate** — "Would a human designer be embarrassed to put their name on this?" with a named reject list (`sections/proposal-and-preview.md.tmpl:L143-L148`) | absent from the generation step | Apply to both paths |
| Anti-convergence control | cross-session only ("never propose the same choices twice") | within-session, with a concrete test — "if someone could swap the headline text between two variants without noticing, they're too similar" (`design-shotgun/SKILL.md.tmpl:L200-L207`) | Keep both; they govern different axes |
| Mutation contract | declares `Write` and `Edit`; instructs writes to `DESIGN.md` and `CLAUDE.md` | omits `Write`/`Edit` but Bash can still mutate; its instructions constrain durable output to `~/.gstack` | Preserve Explore's forbidden repo effects and Record's explicit confirmation — section 5.1 |
| Invocation belief | does not call shotgun | believes consultation calls it | Defect; the merge resolves it |

### 4.6 Why this is one coherent module

Held against `docs/design-requirements.md` section 6:

| Difference | Classification | Treatment |
|---|---|---|
| Research-led proposal vs generate-and-react | Investigative technique, same decision policy — the user picks | **Playbook** |
| Phase 0–6 vs Step 0–6 ordering | Step ordering | **Protocol** |
| System-level tokens vs screen-level variants | Subject matter | **Jurisdiction** |
| Consultant register ("strong opinions") vs partner register ("brainstorming partner") | Tone only | Optional style, not a perspective |
| `Write`/`Edit`/`WebSearch` vs `Agent`, plus different instructed output locations | **Different pre-approval, prerequisite, and intended effects** | Preserve explicitly; do not misstate tool pre-approval as enforcement |

Four of the five differences are exactly the categories the requirements say belong *inside* one
skill. The fifth is the one that must not be flattened, and section 6 gives it a seam rather than a
paragraph.

### 4.7 Declared positive advantage

`docs/design-requirements.md` section 3 requires naming an expected positive advantage and, if
better judgment is claimed, at least one task class where combination should beat the best single
source.

**Advantage class is better output, on two named classes — not maintenance, and not routing.**

1. **Generation-failure robustness.** For the identical operation "produce N candidate directions
   and show them", `design-consultation` has a `$D check` plus anti-slop self-gate, but no bounded
   rate-limit retry, missing/empty-output verification, per-variant failure reporting,
   `/tmp`-then-copy sandbox workaround, or total-failure sequential fallback; `design-shotgun` has
   those recovery behaviors. A user who enters
   through the design-system door today gets a materially worse failure mode than one who enters
   through the exploration door, for the same underlying binary. The merged skill should beat
   `design-consultation` as source oracle on any corpus case that induces a generation failure —
   rate limiting, empty output, sandbox write rejection, or total generation failure.
2. **Quality-gate completeness.** The anti-slop self-gate exists only in `design-consultation`; the
   within-session anti-convergence test exists only in `design-shotgun`. Neither source applies both.
   The merged skill should beat *each* source oracle in its own home jurisdiction on the gate the
   other one owns — measurably, as slop-pattern incidence and as inter-variant distinctness.

**Explicitly not claimed.** Maintenance (section 4.1 disproves the basis). Routing (the two triggers
are already distinct and a router would suffice). Better taste — nothing in the evidence suggests
combining these sources improves aesthetic judgment, and section 9's gates do not test for it.

---

## 5. Preserved distinctions

### 5.1 Two effect states, informed but not enforced by tool declarations

`design-consultation` declares `Write` and `Edit`; `design-shotgun` declares neither and declares
`Agent` instead (**O**, section 3.1). This declaration difference is pre-approval evidence, not a
write sandbox: Shotgun also declares Bash and its own workflow writes through `$D` and `cp`.
The behavioral distinction comes from the instructed effects. Shotgun requires durable artifacts
under `~/.gstack` and never instructs repository mutation; Consultation writes `DESIGN.md` and a
Design System note in `CLAUDE.md` (`sections/proposal-and-preview.md.tmpl:L216`, `L272-L280`).

`docs/design-requirements.md` section 6 forbids waiving effect or authority differences through a
prose merger, and section 7.7 forbids expressing tool pre-approval as tool restriction. The design
therefore proposes **two named effect states** the user can see and choose between. Their eventual
permission enforcement remains later-phase work:

| State | Forbidden and permitted effects | Reached by |
|---|---|---|
| **Explore** | No repository writes; durable design artifacts only under `~/.gstack/projects/$SLUG/designs/` (temporary generation may use `/tmp` before copying) | default for exploration intake |
| **Record** | Explore effects plus the specifically confirmed repo `DESIGN.md` and `CLAUDE.md` updates | entered only after the user approves a direction *and* confirms recording |

**Concrete decision where this matters:** a user exploring three homepage directions on a client
repository must not end the session with a modified `CLAUDE.md`. Shotgun does not instruct that
effect; Consultation does. Collapsing them into one always-writing skill would silently expand the
proposed effect contract even though the current tool declarations alone do not enforce it.

### 5.2 Two intake protocols

| Protocol | Distinguishing steps | Why it cannot collapse |
|---|---|---|
| **Research-led** (`design-consultation`) | Phase 0 pre-checks → product context with the *memorable-thing forcing question* → optional WebSearch + browse competitive research → three-layer synthesis (tried-and-true / new-and-popular / first-principles) with an explicit **EUREKA** check → whole-system proposal with a **SAFE/RISK** split | Requires `WebSearch` and optionally the `$B` browse binary; produces a rationale the other protocol never generates; the SAFE/RISK framing is a decision structure, not a presentation style |
| **Brief-led** (`design-shotgun`) | 5-dimension brief (who · job to be done · what exists · user flow · edge cases) → two-round cap on questioning → optional live-site screenshot → `$D evolve` from the existing design instead of `$D variants` | Handles "I don't like THIS" — an intake with a concrete negative referent that the research-led protocol has no step for; the two-round cap is an explicit anti-over-interrogation rule |

**Concrete artifact where the difference matters:** a greenfield repository with an empty `src/` can
only be served by the research-led protocol, which will route to `/office-hours` if even the product
is unclear. A running site the user dislikes can only be served well by the brief-led protocol,
because `$D evolve --screenshot` needs the screenshot the other path never takes.

### 5.3 Two generation strategies and their degradation

`design-shotgun`'s parallel path carries five behaviors that must survive verbatim in substance
(`design-shotgun/SKILL.md.tmpl:L226-L298`, **O**):

1. **`/tmp` then `cp`.** `$D generate --output ~/.gstack/…` fails with "The operation was aborted"
   under sandbox restriction; generating to `/tmp` then copying succeeds. This is an observed
   workaround for a real environment constraint, and losing it silently breaks generation.
2. **`$D` path propagation.** Agents do not inherit the `$D` shell variable; the resolved absolute
   path must be substituted into each agent prompt.
3. **Bounded retry.** Up to 3 retries on rate limit with a 5-second wait; one retry on missing or
   empty output; one regeneration on quality-check failure.
4. **Explicit failure reporting.** Per-variant `DONE` / `FAILED` / `RATE_LIMITED` status, and *"For
   any failures: report explicitly with the error. Do NOT silently skip."*
5. **Sequential fallback.** If zero variants succeed, fall back to one-at-a-time generation and tell
   the user why.

`design-consultation` carries a different and equally required degradation ladder for research
(`design-consultation/SKILL.md.tmpl:L189-L192`, **O**): browse available → screenshots plus
snapshots plus WebSearch; browse unavailable → WebSearch only; WebSearch unavailable → built-in
design knowledge. And for preview: `DESIGN_READY` → AI mockups; `DESIGN_NOT_AVAILABLE` → a
self-contained HTML preview page; `open` fails → print the path.

### 5.4 Two quality gates, currently split

- **Anti-slop self-gate** (consultation only): reject and regenerate on purple gradient hero,
  3-column SaaS grid, centered-everything, Inter body text, generic stock-photo vibe, `system-ui`
  display font, gradient CTA, bubble-radius everything. Stated as a **hard gate**.
- **Anti-convergence test** (shotgun only): each variant must differ in font family, color palette,
  and layout approach; the operational test is whether headline text could be swapped between two
  variants unnoticed.

### 5.5 Perspective and priors that must survive

- **Propose, don't present menus.** The consultant posture is a decision policy, not a register:
  *"You don't present menus — you listen, think, research, and propose."* It changes what the user is
  shown at the highest-stakes moment.
- **Coherence over individually optimal choices**, with coherence violations surfaced as *nudges
  that never block*, and *"Accept the user's final choice."*
- **Font blacklist and overused list**, including the recorded reasoning that Space Grotesk is
  excluded specifically because *"every AI design tool converges on it as 'the safe alternative to
  Inter'"*.
- **The memorable-thing forcing question**, with the accompanying rule that *"design that tries to
  be memorable for everything is memorable for nothing"* — a constraint that governs every later
  decision in the session.

### 5.6 Prerequisites and failure behavior

| Prerequisite | Owner | Required for | Behavior when absent |
|---|---|---|---|
| `$D` designer binary (`DESIGN_SETUP`) | separately retained external capability; executable verified 2026-08-03 (`7a3091782c78`) | all mockup generation | consultation degrades to an HTML preview page; shotgun has no equivalent fallback — a gap this design resolves with rung 4 |
| `$B` browse binary (`BROWSE_SETUP`) | separately retained external capability; executable verified 2026-08-03 (`e97ed1a3f007`) | visual competitive research; live-site screenshot | research degrades to WebSearch; the evolve path becomes unavailable |
| `Agent` capability | host | parallel generation | sequential fallback |
| Feedback endpoint (HTTP POST) | `DESIGN_SHOTGUN_LOOP` | comparison board feedback | falls back to `AskUserQuestion` |
| `gstack-slug`, `gstack-taste-update` | source-owned gstack CLI scripts; executables verified 2026-08-03 (`442fce24ba87`, `0160f80754cb`) | state directory naming; taste profile updates | Retain/relocate or replace before source retirement; absence handling is unresolved |
| `~/.gstack/projects/$SLUG/` | filesystem | all durable artifacts | Hard requirement for final artifacts; `/tmp` remains allowed only as transient generation space before copy |
| WebSearch | host | competitive research | degrades to built-in knowledge |

---

## 6. Proposed skill design

### 6.1 Shape

**One workflow, one optional tail, three internal seams.** Not a panel, not a mode router.
`astra-critique`'s panel architecture is inappropriate here: a panel is justified when several
perspectives with overlapping standing can reach incompatible recommendations, and these two sources
hold one perspective between them — the divergence is protocol, playbook, authority, and
prerequisite, none of which produce rival recommendations about the same decision.

```text
                 ┌─ intake: research-led ─┐
user request ──► │                        ├─► direction generation ─► approval loop ─┐
                 └─ intake: brief-led ────┘         (one loop)          (one loop)    │
                                                                                      ▼
                                                        ┌──────────── record? (user decides) ────────────┐
                                                        │                                                │
                                                   Explore state                                    Record state
                                            (artifacts under ~/.gstack only)              (+ DESIGN.md, + CLAUDE.md)
```

### 6.2 Internal modules

Each seam below corresponds to demonstrated variation, per `docs/design-requirements.md` section
7.6. No seam is created for hypothetical reuse.

| Module | Responsibility | Seam justified by |
|---|---|---|
| **Intake** | Establish product context and a design brief | Two observed protocols with different prerequisites (`WebSearch`/`$B` vs screenshot/`$D evolve`) and different entry conditions (greenfield vs "I don't like THIS") — section 5.2 |
| **Direction generation** | Produce N distinct candidate directions | Two observed strategies with different failure profiles — section 5.3. Two implementations exist today, so this is a real adapter set, not a hypothetical one |
| **Approval** | Comparison board, ratings, feedback, confirmation, `approved.json` | Already unified upstream as one partial; **no seam** — one implementation |
| **Recording** | Token extraction, `DESIGN.md` composition, `CLAUDE.md` note, taste update | Gated by the effect state of section 5.1; plan-mode and disk-mode are two observed variants |

The Approval module deliberately has no seam. Building one would be exactly the hypothetical seam
section 7.6 forbids, and it would also re-fragment behavior gstack has already unified.

### 6.3 Generation strategy and degradation ladder

The merged skill uses one ladder, resolving section 4.5's conflict in favour of the more robust
source:

1. **Parallel agents** — N independent `Agent` contexts, each with `/tmp`-then-`cp`, absolute `$D`
   path substitution, bounded retry, quality check, and explicit status reporting.
2. **Batch** — `$D variants --count N` in a single call. This is `design-consultation`'s current
   behavior, retained as a rung because it is cheaper and does not require `Agent`.
3. **Sequential** — one `$D generate` at a time, announced to the user.
4. **No generator** — HTML preview page composed from the proposal; if `open` fails, print the path.

Every rung below the first must announce itself. Silent degradation is what makes today's
`design-consultation` path worse than it looks.

### 6.4 Where user choices occur

Whether to research · the concepts and their count (max two adjustment rounds) · the winning variant
and per-variant feedback · whether to accept or override a coherence nudge · **whether to leave
Explore and enter Record** · plan mode versus disk · whether any downstream workflow starts. The
skill never blocks on disagreement and never refuses to record a direction it dislikes.

### 6.5 Uncertainty, unavailable prerequisites, and failure

- **Thin context is stated, not hidden.** Both sources cap questioning and proceed with recorded
  assumptions; the merged skill lists those assumptions in its result rather than presenting an
  inferred brief as fact.
- **Unavailable prerequisites are named at the point of degradation**, with the capability that was
  lost — not a generic warning at start-up.
- **Generation failure is reported per variant.** Partial success proceeds with the survivors and
  says how many failed and why.
- **A failed quality gate regenerates once, then reports.** It does not silently ship a variant that
  failed the embarrassment test.

### 6.6 Architectural choices that remain hypotheses

The two-effect-state model, the four-rung ladder, and the two-intake seam are hypotheses until
section 9's comparisons run. Specifically: if the corpus shows users never distinguish Explore from
Record, the states collapse into one confirmation prompt; if the batch rung never outperforms
parallel on cost or latency, the ladder loses a rung.

---

## 7. Dependencies and delivery shape

### 7.1 External components that remain separate

| Component | Type | Relation | On unavailability |
|---|---|---|---|
| `$D` designer | separately retained external binary | **invokes** | Degrade to rung 4; announce |
| `$B` browse | separately retained external binary | **invokes** | Research degrades to WebSearch; evolve path unavailable |
| `Agent` subagents | separate execution contexts | **invokes**; never flattened into prompt text | Degrade to rung 2 |
| Comparison board feedback endpoint | local HTTP service | **invokes** | Fall back to `AskUserQuestion` |
| `gstack-slug`, `gstack-taste-update` | source-owned CLI scripts | **invokes** | Retain/relocate or replace; unresolved — section 10 |
| `gstack:skill-doc-generation-pipeline` | build generator + resolver modules | **documents only** | Not a runtime dependency; shared provenance retained until all relevant generated consumers migrate |
| `~/.gstack/projects/$SLUG/` | state directory | **reads and writes** | Hard requirement |
| `prototype` | retained independent skill; companion file is display metadata, not an agent | **reads** findings if the user has them | Proceed without |

Per `docs/design-requirements.md` section 4.3, none of these is flattened into prompt text. The
`Agent` relation in particular stays a separate execution context, because the parallel generation
protocol depends on the isolation.

### 7.2 Peer relations

| Peer | Direction and semantics | Minimum payload / information class | Who decides or starts | If the peer is unavailable |
|---|---|---|---|---|
| `astra-interface` | Product → Interface; Interface **consumes output**, never an invoked workflow | Approved variant path and `approved.json`; applicable `DESIGN.md` anchors; extracted token candidates explicitly labeled non-authoritative until projected | User | Product Design still completes and retains a named manual handoff; no implementation is fabricated |
| `astra-brand` | Brand → Product; Product **consumes Brand output** | Versioned `docs/brand-guidelines.md` identity constraints, primitive meanings, and unresolved brand decisions; not generic “brand capability” | User decides whether provisional non-brand exploration may continue | State the missing constraint; do not invent identity values. Record remains blocked for brand-owned fields unless the user explicitly accepts provisional values |
| `astra-critique` | Critique → Product; **user-mediated handoff** only | Section 7.4's common envelope plus destination-only payload | User | Section 7.4 |
| `astra-spec` | Product → Spec; Spec **consumes output** when intent is being recorded | Approved-direction summary, artifact anchors, assumptions, and unresolved product decisions | User | Keep the approved direction artifact; the user may transfer it manually later |
| `astra-plan` | Product → Plan; Plan **consumes output** in plan mode | Approved-direction plan section, artifact anchors, extracted token candidates, and Record/Explore choice | User | Keep the approved direction artifact; do not write or invoke a plan workflow |

No relation here is an invocation of a peer's workflow. The `astra-interface` edge in particular is
output consumption: this skill names `/design-html` as a next step today and must continue to *name*
rather than invoke it.

### 7.3 Artifact authority

This design accepts the Product side of the **provisional reconciliation hypothesis** in
`docs/design-roadmap.md` section 10.4. It becomes a roster contract only after Brand, Interface, the
coordinator, and the user reconcile it. Product Design's specific obligations are:

- Root `DESIGN.md` is **this skill's editorial jurisdiction** — level 3. Editor and chair, not judge
  over Brand or Interface jurisdictions.
- Brand primitives in `DESIGN.md` are **references to** `docs/brand-guidelines.md`, never
  redefinitions — level 2 outranks level 3 on identity.
- This skill **does not write** `assets/design-tokens.json`. `$D extract` produces token values from
  an approved mockup; those values enter `DESIGN.md` as recorded decisions, and Interface owns the
  projection — level 4.
- The `CLAUDE.md` Design System note is retained (it is what makes `DESIGN.md` actually consulted),
  but it is written only in Record state.

**Unresolved and named:** today `design-consultation` writes `DESIGN.md` *and* the `CLAUDE.md` note
without consulting `docs/brand-guidelines.md` at all — its only brand input is a gbrain query for
"brand-related notes from CEO plans" (**O**, section 3.1). Under level 2 that is a gap, and closing
it requires the Brand design to exist. Section 10 records it.

### 7.4 Critique handoff acceptance

**`accepts Critique handoff: yes`.**

| Field | Value |
|---|---|
| Owned problem class | **The approved design direction is wrong for this product or its users** — the direction itself, not its implementation |
| Not owned | Implementation defects, accessibility violations, and visual-system inconsistencies (Interface); identity or audience-signal inconsistency (Brand); missing tests (Test) |
| Destination-only payload | (1) path to the approved variant and its `approved.json`; (2) the `DESIGN.md` sections the finding contradicts; (3) the recorded **memorable-thing** statement, so the critique can be tested against the direction's own stated intent; (4) which stage produced the disputed decision — research synthesis, proposal, or variant approval |
| Common envelope | Unchanged: artifact, problem statement, finding IDs and evidence, observed impact, affected scope, user constraints, open decisions, context gaps |
| Who decides | The user. Critique names this skill and stops |
| If this peer is unavailable | The route candidate remains in Critique's report as a reconciliation gap; Critique must not reroute a direction problem to Interface or Brand |

The payload carries **no proposed remedy**. Receiving a handoff re-enters this skill at Intake with
the prior direction as context, not at Recording — a direction the user has disputed must be
re-approved, not patched in place.

**Roadmap reconciliation applied 2026-08-03.** The prior seed said "product-experience or
user-journey problem." This design **accepts and narrows** it: Product Design owns the *direction*
half and explicitly declines the user-journey half, which belongs to Interface where the journey is
materialized. The coordinator recorded that narrower profile in roadmap section 3.2; it remains a
claimed phase-0 contract, not runtime behavior.

### 7.5 Reference and cleanup ledger

Coordinator-applied `consuming_designs` updates (still pending the user's lifecycle disposition):

| Source | Proposed update | Basis |
|---|---|---|
| `prototype` | Add `astra-product-design` as a consuming design | Section 4.4; consumption only, lifecycle not owned |
| `canvas-design`, `algorithmic-art`, `diagram` | No claim from this design | Amendment 3 section 10.5 owns their rows |

---

## 8. Manual bridge

Until this skill exists, the closest approximation is an ordered manual workflow. It is usable
today, with one rough edge.

**For a new product's design system:**

1. `/office-hours` — only if the product itself is unclear. `design-consultation` will route you
   here anyway.
2. `/design-consultation` — Phases 0–6: pre-checks, product context and the memorable-thing
   question, optional research, the SAFE/RISK proposal, preview, and `DESIGN.md`.
3. `/design-html` — if you want the approved direction as production HTML.

**For exploring directions on one screen:**

1. `/design-shotgun` — Steps 0–6: brief, concepts, parallel generation, comparison board, approval.
2. `/design-consultation` afterwards **only if** you want a `DESIGN.md`. It will not read
   `design-shotgun`'s `approved.json` as a starting proposal; you must restate the direction.

**The rough edge, stated plainly.** Step 2 of the second workflow is where today's split costs the
user real work: `design-shotgun` writes `approved.json` and a chosen variant PNG, and
`design-consultation` has no step that reads them. The user re-describes an already-approved
direction in prose. Conversely, entering through `/design-consultation` for a design system means
its Phase 5 generation runs without retry, rate-limit handling, or fallback — so on a rate-limited
API the design-system path fails where the exploration path would have recovered.

**Prerequisites and their consequences.** The source-prescribed checks were run on 2026-08-03:
`$D` and `$B` are executable at the gstack paths recorded in section 5.6, so both manual workflows
are currently usable. If `$D` later becomes unavailable,
`/design-consultation` still works and falls back to an HTML preview page, but `/design-shotgun`
has no documented fallback and its central step cannot run. If `$B` browse is absent, competitive
research degrades to WebSearch and the "I don't like THIS" evolve path is unavailable. The local
feedback endpoint was not started during this documentary review; its declared
`AskUserQuestion` fallback remains the manual bridge.

---

## 9. Deferred implementation and validation

Phase 0 records these obligations and builds none of them. `docs/phase-0.md` section 8 remains
authoritative for phase-wide exclusions.

### 9.1 Declared advantage class and the behavior that would demonstrate a win

From section 4.7: **generation-failure robustness** and **quality-gate completeness**. A positive
win is demonstrated when, on identical briefs, the candidate produces a usable set of directions in
cases where the source oracle produces none or silently fewer, and when it applies both quality
gates where each oracle applies one.

Maintenance and routing are **not** claimed and must not be accepted as a substitute if the output
gates fail.

### 9.2 The three comparison systems

| System | Instantiation |
|---|---|
| **Source oracle** | The stronger applicable original, chosen before outputs are seen: `design-consultation` for design-system briefs; `design-shotgun` for screen-exploration briefs. Both at gstack `1.60.1.0` / `a3259400`, pinned |
| **Reference convener** | A thin adapter that dispatches to the unchanged originals by intake type and forwards `approved.json` between them. This also isolates the value of fixing the section 4.3 defect, since the convener can close it without rewriting either source |
| **Self-contained candidate** | The merged skill of section 6, internalizing the Product-specific behavior from every resolver input in section 3.1 and reproducing both generation strategies without depending on either original skill. It may still invoke separately retained `$D` and `$B` external capabilities |

A neutral wrapper normalizes brief format and result shape only. It adds no design priors, no font
opinions, and no expected answers.

### 9.3 Fixed corpus classes

| Class | Cases must include |
|---|---|
| **Home jurisdiction — consultation** | Greenfield repo with README only; existing `DESIGN.md` to update; empty repo that should route to `/office-hours`; plan-mode session |
| **Home jurisdiction — shotgun** | Single screen with rich codebase context; "I don't like THIS" against a running localhost; a repeat session with prior `approved.json` files |
| **Declared advantage — generation failure** | Rate-limited API; empty output file; sandboxed write rejection to `~/.gstack`; total generation failure; partial failure (2 of 4 variants) |
| **Declared advantage — quality gates** | Briefs that bait slop patterns (fintech dashboard, AI SaaS landing page); briefs that bait convergence (three variants of one form) |
| **Expected divergence** | Briefs where research-led and brief-led intake should reach different directions — a category with strong conventions vs a category with none |
| **Expected convergence (control)** | Briefs where both intakes should agree; disagreement here signals the merge introduced noise |
| **Prerequisite failure** | `$D` absent; `$B` absent; `Agent` unavailable; feedback endpoint down; `~/.gstack` unwritable; WebSearch unavailable |
| **Authority** | A session that must end in Explore state, verified by asserting the repository working tree is unchanged |

### 9.4 Method

Paired runs on identical briefs; repeated trials because generation is stochastic; blinded and
order-randomized evaluation for every subjective judgment. Aesthetic quality is evaluated by the
user, not by the agent, and never by the candidate itself.

### 9.5 Measures

Usable-direction yield under failure injection; slop-pattern incidence per variant set;
inter-variant distinctness; prerequisite-degradation correctness (did the announced rung match the
actual capability); assumption-disclosure rate on thin context; rationale presence on
recommendations; **authority containment** (zero unapproved repository writes in Explore state);
`DESIGN.md` completeness against the section template; cost and wall-clock latency per direction set.

### 9.6 Gates and the consequence of failing each

| Gate | Comparison | Consequence of failure |
|---|---|---|
| **Home non-regression** | Candidate vs each source oracle on its own jurisdiction | Blocks the merge. Neither entry point may get worse |
| **Positive advantage** | Candidate vs source oracle on the two declared classes | Failure means combination bought no output benefit. Because maintenance is explicitly not claimed (section 4.1), there is no fallback justification: the correct response is to withdraw the merger and keep both sources, or reduce the proposal to a router |
| **Internalization fidelity** | Self-contained candidate vs reference convener | A convener win with a candidate loss blocks internalization and therefore blocks retirement. Resolver-derived Product behavior and the consultation section template are the highest-risk internalization points |
| **Authority containment** | Explore-state sessions | Any unapproved repository write is a hard failure, not a tuning issue |
| **Source-specific retirement** | Behavior, authority, dependencies, delivery shape, degradation, user approval | Failure leaves both sources installed. External `$D`, `$B`, and feedback capabilities may remain declared, separately retained prerequisites; not vendoring them is not itself a retirement blocker, but the candidate must preserve their invocation and degradation contracts. Source-owned `gstack-slug` and `gstack-taste-update` must be retained/relocated or replaced |

**A note on what "matching recommendations" would not prove.** If the candidate reaches the same
approved variant as the oracle but lost the EUREKA check, the SAFE/RISK framing, or the
memorable-thing constraint, the gate has not passed. `docs/design-requirements.md` section 7.9 makes
a disappeared source-unique playbook a failure even when final recommendations agree.

---

## 10. Provenance and open questions

### 10.1 Inspected sources

All hashes and line counts in section 3.1 were inspected on 2026-08-01 and the generator/resolver
sources plus executable prerequisites were added on 2026-08-03. gstack is pinned at
`a3259400a366593e0c909dd9ac3e59752efd2488`, release `1.60.1.0`. Cross-neighborhood skills are
registered at the locations in section 3.1. `prototype` has no containing immutable revision, so
its four content hashes are its provenance record; `agents/openai.yaml` supplies display metadata,
not an independently invocable agent.

Line anchors in this document refer to the `.tmpl` files where the behavior is authored and to the
generated `SKILL.md` where a generated artifact is being described. A hash mismatch on any file
invalidates its anchors until re-inspection, per `docs/design-requirements.md` section 4.2.

### 10.2 Evidence gaps

- **The local feedback service was not started (U for current liveness).** Its declaration and
  `AskUserQuestion` fallback were inspected, so endpoint downtime does not make the manual bridge
  unusable.
- **`design-shotgun` has no observed fallback when `$D` is absent (O for the absence, I for the
  consequence).** No instruction in its template covers that case.
- **The gbrain `context_queries` were read as declarations, not traced to their retrieval behavior (I).**

### 10.3 Provisional decisions

1. **The merger stands, on section 4.3's evidence rather than amendment 1's.** Byte-identity is
   generator output; the real basis is one outcome, one already-shared approval loop, and a live
   defect where one source believes the other invokes it.
2. **Architecture is one workflow with three seams, not a panel and not a mode router.** Provisional
   until section 9.
3. **Two effect states rather than one.** Provisional, but the safe default: current frontmatter is
   pre-approval evidence, while the proposed no-repo-write Explore contract supplies the actual
   behavioral boundary.
4. **The generation ladder resolves in favour of `design-shotgun`'s protocol.** This is the
   substance of advantage class 1; if that gate fails, this decision fails with it.

### 10.4 Open questions

| # | Question | Consequence if unresolved |
|---|---|---|
| 1 | **Which `UX_PRINCIPLES` behavior belongs in each consumer?** Four source skills across Product Design, Interface, and Critique consume one resolver partial; it does not require an exclusive Astra owner | Each peer must classify the priors it actually needs. After at least two designs demonstrate the same seam, the coordinator may propose a shared module; until then each design owns its fidelity and the global component record preserves provenance |
| 2 | **Does the `DESIGN_SHOTGUN_LOOP` partial cross the Critique boundary?** `plan-design-review` uses the same approval loop | If Critique vendors it too, the same board machinery exists in two Astra skills — acceptable under self-containment, but it must be a recorded decision, not an accident |
| 3 | **Will Brand and Interface accept the roadmap's provisional artifact-authority stack?** `design-consultation` today consults neither `docs/brand-guidelines.md` nor the token projection | Until both peer designs and the user reconcile it, Record must not invent brand-owned values; Product's section 7.3 acceptance settles only its side |
| 4 | **Should `gstack-slug` and `gstack-taste-update` be retained/relocated or replaced?** Both are source-owned scripts this skill's state model depends on | The retirement gate cannot pass until their behavior and absence handling have an independent home; external `$D` and `$B` do not need to be vendored merely for self-containment |
| 5 | **Should the batch generation rung survive?** It exists only because `design-consultation` implements it | If it never wins on cost or latency, it is dead weight and the ladder loses a rung |
| 6 | **Does the user actually distinguish Explore from Record?** | If not, the two states collapse into one confirmation and section 6.2's Recording seam is over-built |

### 10.5 Coordinator reconciliation applied

Applied on 2026-08-03 as claimed/provisional state, per `docs/design-roadmap.md` section 6 step 8:

1. **Section 3.2 coverage table, product-experience row:** record that this destination **accepts
   and narrows** — it owns the design-direction problem class and declines the user-journey half to
   `astra-interface`.
2. **Section 5.4:** withdraw the `design-shotgun` → Interface secondary-role claim. Record
   `UX_PRINCIPLES` in the shared generation-pipeline component and require each of the three peer
   designs to classify its own use; do not invent exclusive ownership for a non-occurrence.
3. **Section 8.2:** annotate the `astra-product-design` verdict row. Its stated basis — 942
   byte-identical lines — measures generated output. The verdict is unchanged; the basis is
   replaced by section 4.3 of this design.
4. **Separate installed-component record:** add one gstack skill-document generation-pipeline record
   with the exact Product-consumed placeholder inventory in section 3.1.
5. **Reference ledger:** add `prototype` with `disposition: unassigned` pending the user and
   `consuming_designs: [astra-product-design]`.
