# Astra Skills

> 留其精華，去之糟粕，集各家之大成

An inventory-driven effort to derive a personalized, non-colliding set of skills from the
existing collection.

> **Phase-0 status:** this README is source inventory and earlier research, not the governing
> design. The authoritative scope is [Astra phase 0](docs/phase-0.md), each proposed skill
> follows the [design requirements](docs/design-requirements.md), and the restored
> [Astra Critique plan](designs/astra-critique.md) is the worked example. The
> [phase-0 ledgers](docs/phase-0-ledgers.md) hold coordinator-owned source-accounting state.
> The long-term goal is self-contained superskills followed by gated deletion of the duplicative
> originals; phase 0 designs that end state but does not perform it. Packaging, tiers, caching,
> telemetry, implementation, evaluation, and retirement are deferred. Sections discussing them
> below preserve research context only.

---

## Why this repo exists

Not a tidiness project. Measured on this machine, July 2026:

| Measurement | Value | Source |
|---|---|---|
| Entries in the skills directory | **271** | `~/.claude/skills/` — 71 real dirs, 200 symlinks |
| Of those, live and invocable | **138** | 133 symlinks have missing targets |
| Live entries that are gstack | **55 of 138** | 54 skills + its router, surfaced by symlink |
| Distinct skills the agent invoked in one month | **16** | 214 transcripts, `Skill` tool calls |
| Distinct skills invoked by any path | **17** | adds `python-patterns`, typed only |
| Live skills in `~/.claude/skills/` that fired at all | **5 of 138** | `code-tracing`, `python-patterns`, `github`, `receiving-code-review`, `doc-coauthoring` |
| The rest of the working set | plugin skills (9) · local commands (2) · 1 broken link | `superpowers:*`, `shell-scripting:*`, `/diss`, `/pr` |
| gstack skills carrying usage-logging code | **82** | `grep -rl skill-usage.jsonl` |
| Times that logging has ever executed | **0** | `~/.gstack/analytics/` does not exist |
| Plugins enabled | **16** | from 4 marketplaces |
| Components those plugins add | **47 skills · 6 commands · 6 agents · 3 MCP servers · 2 hooks · 1 LSP server** | see [Plugins](#plugins) |
| Harness built-in skills | **12** | shipped with the CLI — no directory, no manifest |
| **Total invocable skills** | **197** | 138 personal + 47 plugin + 12 built-in |
| MCP tools referenced by local commands but **not configured** | **5** | jira, awslabs-mysql ×2, context-mode ×2 |

The real working set, mined from transcripts. **Two cohorts, counted separately** — they
travel different code paths and mean different things:

- **Agent-fired** — a `Skill` tool call the model issued on its own. **86 events, 16 skills.**
- **You typed** — a `/x` slash command, recorded as `<command-name>`. **74 events.**

Only the agent-fired column is evidence about autonomous discovery; see
[What counts as promotion](#what-counts-as-promotion).

| Skill | Agent-fired | You typed | Total |
|---|---:|---:|---:|
| `diss` | 31 | 19 | **50** |
| `pr` | 1 | 39 | **40** |
| `code-tracing` | 11 | — | 11 |
| `superpowers:brainstorming` | 9 | 2 | 11 |
| `shellcheck-configuration` | 1 | 7 | 8 |
| `superpowers:receiving-code-review` | 7 | — | 7 |
| `python-patterns` | — | 7 | 7 |
| `superpowers:test-driven-development` | 6 | — | 6 |
| `github` | 5 | — | 5 |
| `superpowers:using-git-worktrees` | 4 | — | 4 |
| `superpowers:executing-plans` | 3 | — | 3 |
| `receiving-code-review` | 2 | — | 2 |
| `doc-coauthoring` | 2 | — | 2 |
| `writing-skills`, `writing-plans`, `bash-defensive-patterns`, `markdown-mermaid-writing` | 1 ea | — | 4 |

**160 invocations total — 86 agent-fired across 16 skills, 74 typed. 17 distinct skills
across both paths: 5 live personal skills, 9 plugin skills, 2 local commands, 1 broken link.**

### Four source categories, not three

The counts above span four delivery mechanisms, and one of them has no directory to scan. A
census that reads only `~/.claude/skills/` misses two of the four:

| Category | Count | Enumerated from |
|---|---:|---|
| Personal skills | 138 live · 133 dangling | `~/.claude/skills/*/SKILL.md` |
| — of which gstack, surfaced by symlink | **55** | targets under `~/.claude/skills/gstack/` |
| Plugin components | 47 skills · 6 cmds · 6 agents · 3 MCP · 2 hooks · 1 LSP | plugin **manifests** — see [Plugins](#plugins) |
| Local commands | 8 | `~/.claude/commands/*.md` |
| **Harness built-in skills** | **12** | **nothing on disk** — shipped with the CLI |

Two consequences:

**gstack is 55 of the 138 live entries — 40% of the live collection.** Each
`~/.claude/skills/<name>/` is a real directory whose `SKILL.md` is a symlink into
`~/.claude/skills/gstack/<name>/`, so these skills are already counted once, at top level.
`skills/gstack/` is therefore **not** a second tier to add to the census — an earlier revision of
this table wrongly counted it as +54. What the concentration does mean: disabling gstack removes
54 skills and its router from the live set in a single move.

**Harness built-ins have no path and no manifest.** These 12 are invocable, and ten of them
already appeared in the collision map below without ever being counted here:

`artifact-capabilities` `artifact-design` `dataviz` `fewer-permission-prompts` `init`
`keybindings-help` `loop` `run` `schedule` `security-review` `simplify` `update-config`

They cannot satisfy the provenance rule in `docs/design-requirements.md` section 4.1 — there is
no immutable revision to hash, and their bytes are pinned to a CLI release that auto-updates.
**Unresolved:** how a built-in earns a ledger row without a reproducible hash.

#### Coverage check

Every measured source, diffed against what this document claims:

| Direction | Result |
|---|---|
| In the inventory, absent from this document | **3** — `artifact-capabilities`, `devex-review`, `run`, all now added below |
| Claimed here, absent from the inventory | **0** — every remaining difference is a namespace prefix, an MCP server, or a plugin agent |

Method: extract every backticked identifier from the collision map and the reference groups;
diff against `find -L ~/.claude/skills -maxdepth 2 -name SKILL.md`, the plugin manifests,
`~/.claude/commands/`, and the built-in list above. **Re-run on every plugin install and CLI
update** — it is the only check that holds the map to the machine rather than to itself.

`-maxdepth 2` with `-L` is deliberate: it resolves each entry's symlinked `SKILL.md` and yields
all 138 entry names, gstack included. Descending to depth 3 walks into `skills/gstack/` and
counts those 54 a second time.

`devex-review` is the instructive miss. It is a distinct live gstack skill whose name nearly
duplicates `plan-devex-review`, which was already mapped: one audits a live developer
experience, the other reviews a plan. That is exactly the routing collision this repo exists to
catch, and it survived because nothing had yet diffed the map against disk.

### The two failures this repo fixes

**1. Routing collision.** Five authors independently solved "interrogate my thinking,"
none aware of the others. When five descriptions all mean *critique this*, selection
degrades toward random:

| Skill | Author | Job |
|---|---|---|
| `grilling` | Matt Pocock | Relentless one-at-a-time interview |
| `/diss` | local | Adversarial code review |
| `office-hours` | gstack | YC-style challenge |
| `plan-{ceo,eng,design,devex}-review` | gstack | Four personas, one loop |
| `superpowers:brainstorming` | Anthropic | One-question-at-a-time refinement |

Within a single collection the problem is already solved — `grill-me/SKILL.md` and
`grill-with-docs/SKILL.md` are 7-line stubs that delegate to `grilling`. The collision is
**cross-collection**, and nothing but this repo can fix it.

**2. Composition by reference.** `guard/SKILL.md:16-28` wires its `PreToolUse` hooks to
`$HOME/.claude/skills/gstack/careful/bin/check-careful.sh` and `.../freeze/bin/check-freeze.sh`.
It *is* `/careful` + `/freeze` — but by pointing at their files. Uninstall gstack and guard
breaks silently. This is the same failure mode Anthropic warns about for nested references
("Claude may partially read files when they're referenced from other referenced files"):
a reach outside the unit produces a partial or broken read.

The same failure recurs across component types. `/pr` and `/trim` declare MCP tools from
servers that were never configured, and neither ships a fallback — so the dependency fails
silently rather than loudly. Reaching outside the unit is one bug with many faces:
sideways into a sibling skill, downward into a nested reference, outward into an absent
MCP server.

Since the endgame is *uninstall everything else*, this becomes a hard rule.

---

## Principles

### 1. Max atomicity, minimum sufficient granularity

Granularity is a **cost**, not a virtue. Per `writing-great-skills/GLOSSARY.md`:

> Finer division spends one of the two loads: more **model-invoked** skills spend
> **context load**; more **user-invoked** skills spend **cognitive load**.

But the cost is not uniform across axes. Only one of the three is expensive:

| Axis | Cost | Rule |
|---|---|---|
| Files inside a skill (`references/*.md`) | **Zero** until read | **Maximise.** Atomicity lives here. |
| User-invoked skills (`disable-model-invocation: true`) | Zero context; costs your memory | Cheap. Cure the memory cost with the router. |
| Model-invoked skills (carry a `description`) | Loaded every turn, every session | **Budget it.** |
| **Agent definitions** (`agents/*.md`) | Description loaded every turn | **Budget it.** Same bill as a skill. |
| **MCP tool schemas** | Name always loaded; schema on demand where the host defers it | Budget the *server*, not the tool. |
| **Commands** (`commands/*.md`) | Name loaded; body on invoke | Cheap. |

So: **push fineness down to where it is free.** Six atomic reference files behind one
description beats six descriptions.

Skills are not the only thing on the bill. A plugin can add agents, MCP servers and hooks
alongside its skills, and **an agent description costs exactly what a skill description
costs**. Counting only `~/.claude/skills/` understates the load. See [Plugins](#plugins).

Empirical bound: *"At 20-30 well-described Skills, the system works well. Beyond that,
description quality becomes critical because the model needs to quickly differentiate
between similar Skills."* Anthropic runs several hundred internally — via a marketplace
where each engineer installs only what they need. Nobody loads 271 at once.

### 2. Self-containment

Two different things get conflated here, so they are stated separately.

**(a) Filesystem self-containment — one declared exception.** Every *file* an astra skill
needs to **do its work** lives inside its own directory. No sideways reach into a sibling
skill for implementation, no dependency on a collection that may be uninstalled. The `guard`
lesson.

> **The sole exception is router discovery.** The `astra` router reads sibling
> `astra-*/SKILL.md` files by design — that is the miss handler, and it is the one
> filesystem reference across skill boundaries this design permits. It is safe because it is
> *read-only, one-directional, and confined to the astra namespace*: the router never depends
> on a sibling to function, it only points at one. Nothing else may reach sideways.

**(b) Runtime prerequisites — declared, never assumed.** No skill is dependency-free in the
larger sense: `/diss`'s own fallback shells out to `mysql`, and across the set astra will
need `git`, `gh`, browsers, AWS credentials, network endpoints and system packages. These
cannot be vendored and should not be pretended away. Each skill **declares its
prerequisites and states its behaviour when one is absent** — the same obligation MCP
carries below, generalised.

Corollary, from Anthropic's authoring guide: **references stay one level deep from
`SKILL.md`.** `SKILL.md` → `references/plan.md` is correct; `references/plan.md` →
`references/deep/detail.md` is not.

**MCP is the sharpest case of (b).** A server is a running process or a remote endpoint,
so it can never be vendored, and its absence is invisible rather than loud:

> **Declare the server, and always ship a fallback path.**

This is not theoretical. Three local commands reach for MCP servers that are not
configured — only `github` is:

| Command | Uses | Depends on | Fallback |
|---|---:|---|---|
| `/diss` | **50** | `awslabs-mysql-mcp-server`, `-uat` | ✅ `diss.md:236` — *"CLI fallback (only if MCP unavailable)"* |
| `/pr` | **40** | `mcp__jira__jira_add_comment` | ❌ `pr.md:233` — *"Use Jira MCP tool `jira_add_comment`"*, no alternative |
| `/trim` | — | `context-mode` MCP (plugin not installed) | ❌ `trim.md:13,17` — steps 1–2 *are* the MCP calls |

`/pr` ran 40 times this month and its Jira step could not have worked once. `/trim` is
structurally broken. `/diss` — the most-used of the three — degrades gracefully, and its
shape is the rule: **prefer MCP, detect absence, fall back.**

### 3. Provenance over frequency

Which skills stay hot is decided by **who initiated the invocation**, never by how often it
fired. Frequency cannot distinguish *rare and worthless* from *rare and critical* — and it
would evict exactly the safety and incident skills whose entire value is being reachable
without being asked. See [Tuning](#tuning-astra-tune).

### 4. Nothing is ever silently lost

Demotion moves a skill one hop further away, never out of reach. The router is a miss
handler, so an evicted skill can still be found and can still earn its way back.

---

## Architecture

> **Deferred research:** this architecture is not part of phase 0 and is not an implementation
> decision.

```
astra/                       Tier 0 — router + miss handler. Model-invoked.
  SKILL.md                     Names every astra skill and when to reach for it.
                               For cold skills: "Read astra-<x>/SKILL.md".

astra-<verb>/                Tier 1 — hot. Model-invoked, carries a description.
  SKILL.md                     <500 lines. Overview + dispatch. The context bill.
  references/                  Tier 3 — atomic, one level deep, free until read.
    <case>.md
  bin/                         Vendored scripts. Never reach outside this directory.

astra-<verb>/                Tier 2 — cold. disable-model-invocation: true.
  SKILL.md                     Zero context cost. Reachable by you, or by the
                               router telling the agent to Read this path.
```

### The tiers

| Tier | Invocation | Context cost | Reachable by | Eligible content |
|---|---|---|---|---|
| 0 — router | model-invoked | 1 description | agent, autonomously | — |
| 1 — hot | model-invoked | 1 description each | agent, autonomously | anything |
| **2a — cold, inert** | `disable-model-invocation: true` | **zero** | you (`/name`); agent via router → **`Read`** | pure instruction only |
| **2b — cold, behaviour-bearing** | `disable-model-invocation: true` | **zero** | you (`/name`); agent via router → **asks you to invoke it** | anything |
| 3 — references | file on disk | **zero** until read | parent skill only | pure instruction only |

Tier 2 splits because the miss handler has two different moves available, and only one of
them is safe for a skill whose frontmatter does real work.

### The router is the miss handler

This is the load-bearing design decision. A model-invoked router **cannot invoke** a
Tier 2 skill — stripping the `description` removes it from the Skill tool's valid-name
list. But it can instruct the agent to `Read` the skill's `SKILL.md`, and reading a file is
never gated.

That single hop restores the demand path, and three things follow:

- Cold skills cost nothing yet stay agent-reachable.
- A **cache miss becomes observable** — the agent wanting a cold skill leaves a `Read`
  in the transcript. Without this, a demoted skill could never be requested, so it could
  never earn promotion: a one-way ratchet that silently deletes capabilities.
- **Demotion becomes safe**, so the hot tier can be genuinely small.

### Reading a skill is not invoking it

A `Read` delivers the **instructions**. Invocation delivers the instructions **plus
everything the frontmatter declares** — and only invocation does:

| Frontmatter field | Effect that a `Read` cannot reproduce | Uses on this machine |
|---|---|---:|
| `allowed-tools` | one-turn permission pre-approval | 117 |
| `disallowed-tools` | one-turn tool denial | — |
| `hooks` | installs hooks (e.g. `guard`'s `PreToolUse` guards) | 8 |
| `argument-hint` | argument binding | 7 |
| `model` | model override | 6 |
| `background` | execution mode | 4 |
| `context` | context handling | 3 |
| `effort` | reasoning-effort override | 2 |
| `agent` | dispatch into a skill-scoped agent | 1 |

`guard` is the proof: `guard/SKILL.md:16-28` installs its safety hooks *through frontmatter*.
Reading that file yields a description of protection, not protection.

**So the tier rule is not "hot vs cold" alone — it is also "inert vs behaviour-bearing":**

> A skill declaring **any** field in the table above is **behaviour-bearing**. It may still
> be cold, but it is **Tier 2b**: the router must never service it with a `Read`.

The two miss-handler moves, by subtype:

- **Tier 2a (inert)** — pure instruction, no frontmatter behaviour. The router **reads it**.
  The demand is served immediately and silently.
- **Tier 2b (behaviour-bearing)** — the router **surfaces the miss to you**: *"this needs
  `/astra-guard`; type it."* Demand is still recorded (the router was consulted), without
  pretending a `Read` conferred a boundary it cannot confer.

Most astra skills will be 2a, which is why the tiering still pays. The 2b set is small and
mostly consists of the skills you would want to invoke deliberately anyway.

### Naming

`astra-<verb>`, lowercase and hyphenated. Anthropic's constraints: `name` ≤64 chars,
lowercase/numbers/hyphens only, and it **cannot contain the reserved words `anthropic` or
`claude`**. The uniform prefix also makes the endgame audit trivial — anything in
`~/.claude/skills/` not matching `astra-*` is a candidate for removal.

---

## Tuning: `/astra-tune`

> **Deferred research:** tuning, promotion signals and tier changes are outside phase 0.
> The Tier 2b proposal is incomplete: surfacing a miss leaves no structured transcript event
> containing the missed target, so its demand cannot be scored as currently described.

An **advisory** cache manager. It proposes; you approve. It never rewrites frontmatter
unattended.

### When it runs

Keyed to **new skill-invocations**, not to wall-clock and not to session count:

The counter runs over **evidence-bearing events** — every event that can move a score:
agent-fired `Skill` calls (86/mo) + cold-skill `Read`s + typed astra commands (74/mo).
**~160/month** at current volume. This is deliberately a *different* cohort from the one
the demotion rule uses; see the note below.

| Trigger | Runs/month at current volume | Runs seeing new data |
|---|---:|---|
| Hourly cron | 744 | ~19% |
| Per session | 214 | ~54% |
| **Per 50 evidence-bearing events** | **~3** | **100%** |

**Two cohorts, two jobs — keep them apart:**

- **Cadence** counts *all* evidence-bearing events (~160/mo). It decides *when to look*.
- **Demotion** is gated on the **agent-fired count alone**, and requires a minimum n before
  it may fire at all.

The reason for the second is statistical, not economical. In the agent-fired cohort, **ten
of sixteen skills sit at n=1–4**. A demotion decision at n=1 cannot be distinguished from an
unlucky sample — so a review may run while a given skill still has too little evidence to be
touched. Reviewing more often is safe; *acting* on thin evidence is not.

### Where the numbers come from

**Transcripts are the scoring source, not a hook log.** The three signals travel three
different code paths, and no single hook matcher sees all of them:

| Signal | Path | Appears in transcript as |
|---|---|---|
| **C** — agent reads a cold skill | `Read` tool call | `"name":"Read"` with `file_path` under the skills dir |
| **B/A** — you type `/x` | slash-command expansion, **not** a `Skill` tool call | `<command-name>` |
| demotion metric — agent fires a skill | `Skill` tool call | `"name":"Skill"` with `skill` |

A `PostToolUse` hook with `matcher: "Skill"` sees only the third. Scoring therefore runs off
`~/.claude/projects/**/*.jsonl`, which already contains all three — verified by extracting
each of them from the existing history.

The hook is a **counter only**, and needs all three paths to count honestly:

```
PostToolUse (matcher: "Skill|Read")   → bump on a Skill call, or a Read under the skills
                                         dir; if (count − last_tuned) ≥ 50, set flag
UserPromptExpansion (matcher: "^astra") → bump on a typed astra command
SessionStart                          → if flag set, inject one line:
                                         "N new events since last tune — /astra-tune"
```

**`UserPromptExpansion`, not `UserPromptSubmit`.** The former fires only for slash-command
expansion and takes a `matcher` on the command name, so an anchored regex counts exactly the
astra commands and nothing else. `UserPromptSubmit` fires on *every* prompt and would need
the hook to parse text and guess. The pattern is already in use on this machine —
`claude-security/hooks/hooks.json:4` matches `"^claude-security:claude-security$"`.

A nudge, never an auto-run. Rewriting tiers before you have seen the data changes behaviour
behind your back. The `PostToolUse` regex-matcher pattern is already proven in
`~/.claude/settings.json:24-40` for `AskUserQuestion`.

No burn-in period: 214 transcripts of history mean the first run produces a real ranking.

### What counts as promotion

Promotion currency is **provenance** — who initiated the invocation:

| Signal | Event | Weight | Why |
|---|---|---:|---|
| **C** | Agent reads a cold skill's `SKILL.md` via the router | **+3** | A literal cache miss serviced from disk. The agent decided on its own that it needed the skill and paid the slow path. Strongest evidence. |
| **B** | You type `/x` *mid-session*, after the agent already worked the topic | **+2** | A correction: "you should have used this." A miss expressed by hand. |
| **A** | You type `/x` at the start of a session | **0** | Proves usefulness, not that the agent should self-fire. |

Signal A is excluded deliberately. `pr` is 39 typed against 1 agent-fired — promoting it on
raw usage would mean the agent starts opening PRs unprompted. **For skills with side
effects, heavy manual use is evidence that you want to keep control, not evidence that you
want to give it away.**

Both signals are already mineable from `~/.claude/projects/**/*.jsonl`: transcript lines
carry `timestamp`, `sessionId`, `uuid` and `parentUuid`, so within-session ordering is
recoverable, and `Read` calls record their full `file_path`.

### Demotion and pinning

- **Demotion** — agent-fired count decays over time. Safe, because the router keeps the
  skill one hop away.
- **`pinned: true`** — never demote regardless of count. For rare-but-critical skills whose
  value is autonomous availability during an event that may happen twice a year.

### Approving a use is not approving a tier change

Kept strictly separate. If a single hurried "yes" both runs a skill and permanently promotes
it, the context budget drifts on autopilot, one distracted approval at a time. Use-approval
is inline, cheap and reversible; tier changes batch into `/astra-tune`, reviewed against a
full window of evidence.

---

## The collision map

Each row is a **candidate neighborhood for investigation**, not one decided astra skill and not
a retirement list. Phase 0 may merge a row, split it into several personalized skills, keep
entries separate, or exclude entries with a reason. **Usage** shows invocations from the July
2026 transcripts and affects prioritization only.

### Candidate collision neighborhoods

| Candidate neighborhood | Entries to investigate | n | Usage |
|---|---|---:|---:|
| **Adversarial critique** | `grilling`, `grill-me`, `grill-with-docs`, `/diss`, `/diss-api`, `diss-infra`, `diss-claudemd`, `/elon`, `/trim`, `office-hours`, `plan-ceo-review`, `plan-eng-review`, `plan-design-review`, `plan-devex-review`, `devex-review`, `autoplan` | 16 | **50** |
| **Code review** | `code-review`, `review`, `requesting-code-review`, `receiving-code-review`, `superpowers:requesting-code-review`, `superpowers:receiving-code-review`, `feature-dev:code-reviewer`, `code-review:code-review`, `security-review`, `simplify`, `code-simplifier`, `health` | 12 | **9** |
| **Browser & QA** | `agent-browser`, `browse`, `connect-chrome`, `open-gstack-browser`, `agentcore`, `vercel-sandbox`, `electron`, `webapp-testing`, `scrape`, `skillify`, `slack`, `pair-agent`, `setup-browser-cookies`, `benchmark`, `dogfood`, `qa`, `qa-only`, `playwright` MCP | 18 | 0 |
| **Design & visual** | `design`, `design-system`, `design-consultation`, `design-html`, `design-shotgun`, `design-review`, `ui-styling`, `ui-ux-pro-max`, `frontend-design`, `theme-factory`, `brand`, `brand-guidelines`, `banner-design`, `canvas-design`, `algorithmic-art`, `slides`, `dataviz`, `artifact-design`, `artifact-capabilities`, `web-artifacts-builder`, `diagram` | 21 | 0 |
| **Plan & spec** | `superpowers:brainstorming`, `superpowers:writing-plans`, `superpowers:executing-plans`, `superpowers:subagent-driven-development`, `spec`, `to-spec`, `sdd`, `planb`, `plan-tune`, `wayfinder`, `to-tickets`, `implement`, `prototype`, `feature-dev:code-architect`, `feature-dev:feature-dev` | 15 | **15** |
| **Ship & VCS** | `ship`, `land-and-deploy`, `canary`, `landing-report`, `setup-deploy`, `/pr`, `/commit`, `/build-push-ecr`, `commit-commands:commit`, `commit-commands:commit-push-pr`, `commit-commands:clean_gone`, `changelog`, `document-release`, `resolving-merge-conflicts`, `superpowers:finishing-a-development-branch`, `superpowers:using-git-worktrees`, `github` | 17 | **49** |
| **Docs & knowledge** | `document-generate`, `doc-coauthoring`, `/doc`, `make-pdf`, `internal-comms`, `learn`, `teach`, `research`, `rtfm`, `init`, `claude-md-management:revise-claude-md`, `claude-md-management:claude-md-improver`, `domain-modeling`, `slack-gif-creator` | 14 | **2** |
| **Debug & incident** | `investigate`, `diagnosing-bugs`, `superpowers:systematic-debugging`, `rca`, `firefighting`, `java-leak-resolver`, `staging-debug`, `local-debug`, `triage` | 9 | 0 |
| **Codebase comprehension** | `how`, `code-tracing`, `codebase-design`, `improve-codebase-architecture`, `feature-dev:code-explorer` | 5 | **11** |
| **Skill meta** | `skill-creator`, `skill-creator:skill-creator`, `writing-great-skills`, `superpowers:writing-skills`, `skillify`, `ask-matt`, `gstack`, `_gstack-command`, `prompt-lookup`, `benchmark-models`, `gstack-upgrade` | 11 | **1** |
| **Delegation & autonomy** | `coding-agent`, `codex`, `superpowers:dispatching-parallel-agents`, `nightnight`, `loop`, `loop-goal`, `schedule`, `pair-agent` | 8 | 0 |
| **Testing** | `tdd`, `superpowers:test-driven-development`, `bdd`, `spock`, `nextjs-test`, `shell-scripting:bats-testing-patterns`, `superpowers:verification-before-completion`, `run` | 8 | **6** |
| **Context & handoff** | `context-save`, `context-restore`, `strategic-compact`, `handoff`, `nowhat` | 5 | 0 |
| **Safety** | `careful`, `freeze`, `unfreeze`, `guard` | 4 | 0 |
| **Setup & config** | `setup-aurora-pg-mcp`, `setup-gbrain`, `sync-gbrain`, `setup-matt-pocock-skills`, `update-config`, `keybindings-help`, `fewer-permission-prompts`, `claude-code-setup:claude-automation-recommender` | 8 | 0 |
| **iOS** | `ios-qa`, `ios-fix`, `ios-design-review`, `ios-sync`, `ios-clean` | 5 | 0 |
| **Ops & routine** | `retro`, `meeting`, `office-hours` | 3 | 0 |

**Inventory: 179 candidate occurrences across 17 neighborhoods (176 distinct).** Three entries
appear in two neighborhoods and are counted twice — `pair-agent` (browser / delegation),
`office-hours` (critique / ops), and `skillify` (browser / skill-meta). Phase 0 assigns each a
primary home and records any secondary role.

`devex-review`, `artifact-capabilities`, and `run` were added by the [coverage
check](#coverage-check) after the map was first written; the neighborhood each landed in is a
candidate placement like every other row, not a decision.

### Not merge targets — reference skills

Single-purpose documentation for one library, framework, or standard. These do **not**
duplicate each other, so fusing them would produce exactly the anti-pattern Anthropic warns
against — *"Skills that try to do everything end up confusing the agent because it cannot
determine when to invoke them."* The decision here is **keep or delete**, never fuse.

| Group | Skills | n | Usage |
|---|---|---:|---:|
| Language / stack | `java`, `python-patterns`, `nextjs`, `claude-api`, `mcp-builder`, `awssdk`, `security`, `cso`, `design-api`, `design-db`, `agent-harness-construction`, `karpathy-guidelines` | 12 | **7** |
| Shell | `shell-scripting:bash-defensive-patterns`, `shell-scripting:shellcheck-configuration`, `bash-pro`, `posix-shell-pro` | 4 | **9** |
| Hugging Face | `huggingface-skills:*` | ~28 | 0 |

### Not merge targets — the dead science collection

133 entries in `~/.claude/skills/` are **broken symlinks** pointing into `~/.agents/skills/`.
That directory **does exist** and holds 30 skills — the individual targets were removed, not
the parent. They cost nothing at runtime and are not invocable, and they are the reason `ls`
reports 271 while only 138 are live.

Five of them look like merge candidates by name and are not — `what-if-oracle` and
`scientific-critical-thinking` read as critique skills, `infographics` as design,
`find-skills` as skill-meta, `markdown-mermaid-writing` as docs. All are dead. They are
listed here rather than in the collision map because **a dead skill cannot be absorbed,
only swept.** `markdown-mermaid-writing` nonetheless shows one invocation in the
transcripts, which dates the collection's breakage to sometime during July 2026.

<details>
<summary>All 133 dangling entries</summary>

`adaptyv` `aeon` `anndata` `astropy` `bgpt-paper-search` `biopython` `bioservices`
`cellxgene-census` `cirq` `citation-management` `clinical-decision-support`
`clinical-reports` `cobrapy` `consciousness-council` `dask` `database-lookup` `datamol`
`deepchem` `deeptools` `depmap` `dhdna-profiler` `diffdock` `dnanexus-integration` `docx`
`esm` `etetoolkit` `exploratory-data-analysis` `find-skills` `flowio` `fluidsim`
`generate-image` `geniml` `geomaster` `geopandas` `get-available-resources` `gget`
`ginkgo-cloud-lab` `glycoengineering` `gtars` `histolab` `hugging-science` `hypogenic`
`hypothesis-generation` `imaging-data-commons` `infographics` `iso-13485-certification`
`labarchive-integration` `lamindb` `latchbio-integration` `latex-posters`
`literature-review` `markdown-mermaid-writing` `market-research-reports` `markitdown`
`matchms` `matlab` `matplotlib` `medchem` `modal` `molecular-dynamics` `molfeat` `networkx`
`neurokit2` `neuropixels-analysis` `omero-integration` `open-notebook`
`opentrons-integration` `optimize-for-gpu` `paper-lookup` `paperzilla` `parallel-web`
`pathml` `pdf` `peer-review` `pennylane` `phylogenetics` `polars` `polars-bio` `pptx`
`pptx-posters` `primekg` `protocolsio-integration` `pufferlib` `pydeseq2` `pydicom`
`pyhealth` `pylabrobot` `pymatgen` `pymc` `pymoo` `pyopenms` `pysam` `pytdc`
`pytorch-lightning` `pyzotero` `qiskit` `qutip` `rdkit` `research-grants` `rowan` `scanpy`
`scholar-evaluation` `scientific-brainstorming` `scientific-critical-thinking`
`scientific-schematics` `scientific-slides` `scientific-visualization` `scientific-writing`
`scikit-bio` `scikit-learn` `scikit-survival` `scvelo` `scvi-tools` `seaborn` `shap`
`simpy` `stable-baselines3` `statistical-analysis` `statsmodels` `sympy` `tiledbvcf`
`timesfm-forecasting` `torch-geometric` `torchdrug` `transformers` `treatment-plans`
`umap-learn` `usfiscaldata` `vaex` `venue-templates` `what-if-oracle` `xlsx` `zarr-python`

</details>

---

## Plugins

A plugin is not a skill bundle. It ships an **open-ended set of component types** — skills,
commands, agents, MCP servers, hooks, LSP servers, monitors, and whatever the manifest schema
grows next (workflows, output styles, themes, channels, declared dependencies). Only the
first is covered by the collision map above.

**The rule is therefore procedural, not a fixed list:**

> **Enumerate the recognized fields in the plugin's manifest.** Do not scan its directory
> tree, and do not assume this document's list is current.

The reason is concrete: several component types are *declared in the manifest and have no
directory*. **12 official plugins declare `lspServers`** with nothing on disk to find — which
is exactly how the audit below originally reported `clangd-lsp` as empty and recommended
deleting a working C/C++ language server. A schema that gains a field silently would
reintroduce the same bug.

Counts below are what this machine's manifests declare today.

### What is installed

**16 plugins enabled, from 4 marketplaces.**

| Marketplace | Source | Plugins |
|---|---|---:|
| `claude-plugins-official` | `github:anthropics/claude-plugins-official` | 13 |
| `claude-code-workflows` | `github:wshobson/agents` | 1 |
| `karpathy-skills` | `github:forrestchang/andrej-karpathy-skills` | 1 |
| `monster-prompt` | `directory:.../Intern/monster-prompt` | 1 |

| Plugin | Skills | Cmds | Agents | MCP | Hooks | LSP |
|---|---:|---:|---:|---:|---:|---:|
| `huggingface-skills` | 25 | — | — | 1 | — | — |
| `superpowers` | 14 | — | — | — | 1 | — |
| `shell-scripting` | 3 | — | 2 | — | — | — |
| `feature-dev` | — | 1 | 3 | — | — | — |
| `commit-commands` | — | 3 | — | — | — | — |
| `claude-md-management` | 1 | 1 | — | — | — | — |
| `code-simplifier` | — | — | 1 | — | — | — |
| `code-review` | — | 1 | — | — | — | — |
| `playwright` | — | — | — | 1 | — | — |
| `github` | — | — | — | 1 | — | — |
| `skill-creator` | 1 | — | — | — | — | — |
| `claude-code-setup` | 1 | — | — | — | — | — |
| `andrej-karpathy-skills` | 1 | — | — | — | — | — |
| `loop-goal` | 1 | — | — | — | — | — |
| `explanatory-output-style` | — | — | — | — | 1 | — |
| `clangd-lsp` | — | — | — | — | — | **1** |
| **Total** | **47** | **6** | **6** | **3** | **2** | **1** |

Notes from the inventory:

- **`clangd-lsp` is not empty — it ships a working C/C++ language server.** Its manifest
  declares `lspServers.clangd` (`command: clangd`, `--background-index`, 9 extension
  mappings). A directory scan finds only a README and a lockfile, which is exactly how this
  component type gets missed. **It is not a free deletion.**
- **`huggingface-skills` alone is 25 skills** — 53% of all plugin skills — for a domain
  absent from a month of transcripts.
- **Three cached versions of `huggingface-skills`** (1.0.17, 1.0.18, 1.0.20) are retained
  simultaneously.
- **`skill-creator` ships 3 further agents inside its skill directory** (`analyzer`,
  `comparator`, `grader`), scoped to the skill rather than global.

### Treatment by component type

Each component type needs a different decision. Only skills and commands fuse.

| Component | Count | Treatment | Why |
|---|---:|---|---|
| **Skills** | 47 | **Absorb** into astra skills | Already in the collision map. |
| **Commands** | 6 (+8 local) | **Absorb** — a command is a user-invoked entry point | Same substance as a Tier 2 skill. |
| **Agents** | 6 | **Keep, but budget** — an astra skill *dispatches* to an agent | An agent is a separate context with its own tools. It cannot be flattened into a skill, and its description costs the same as a skill's. |
| **MCP servers** | 3 | **Declare, never vendor** — with a fallback | The self-containment exception. See [Principles §2](#2-self-containment). |
| **Hooks** | 2 | **Own them** — astra ships its own | `PostToolUse` telemetry for `/astra-tune` is itself a hook. Conflicts are a real risk. |
| **LSP servers** | 1 | **Keep — out of scope** | Language intelligence is orthogonal to skills. Nothing in astra replaces `clangd`. |
| **Monitors** | 0 | **Keep — out of scope** | None installed, but a manifest-declared type to check for on future downloads. |

The consequence for the endgame: **"uninstall all other skills" is not the same as
"disable all other plugins."** Disabling `feature-dev` removes 3 agents you may want;
disabling `playwright` removes an MCP server no skill can replace; disabling `clangd-lsp`
removes C/C++ code intelligence that no skill provides. Plugin removal has to be decided
per component, not per plugin — and the inventory must be read from the **manifest**, not
from the directory tree.

### The monster-prompt entanglement

`monster-prompt` is registered as a `directory`-source marketplace **and** is the target of
symlinks throughout the config. It is a second personal skill repo, already load-bearing:

- All 8 local commands in `~/.claude/commands/` are symlinks into it
- The global CLAUDE.md rules (`git-workflow.md`, `pr-guidelines.md`, `environment.md`,
  `persona.md`) are sourced from it
- **45 of the 67 working skill symlinks resolve into it** — 26 from its own `claude/skills/`,
  13 from `vendor/anthropic-skills/`, 6 from `vendor/vercel-agent-browser/`. Only 22 resolve
  into `~/.agents/skills/`.
- It supplies the `loop-goal` plugin

Astra Skills cannot ignore it. Either monster-prompt is absorbed into astra, or the two
repos divide responsibility explicitly. **This is unresolved** — see
[Open questions](#open-questions).

### Packaging research (deferred)

Packaging is outside phase 0. The following tradeoff is retained for a later implementation
decision. A plugin can carry
skills, commands, agents, hooks, MCP and LSP declarations as one versioned, toggleable unit
— exactly the astra component set. The alternative is loose symlinks into
`~/.claude/skills/`, which is what produced the 133 broken links this repo exists to fix.

**But it is not free, and the cost lands on two things this document has already
specified:**

- **Paths.** Plugin skills do not live in `~/.claude/skills/`. Any hardcoded path in the
  router or in `/astra-tune` breaks. The router must resolve its miss-handler target
  through `${CLAUDE_SKILL_DIR}` / `${CLAUDE_PLUGIN_ROOT}` rather than a literal path — both
  are already used on this machine (65 and 23 occurrences respectively).
- **Names.** Plugin skills are invoked namespaced, `/astra:denounce` rather than
  `/astra-denounce`. That changes every command name in this document, and it changes what
  `/astra-tune` must match when it mines transcripts.

Neither is a blocker; both are rewrites that get cheaper the earlier the decision is made.

---

## Absorbing new skills

When a new skill appears in the wild, it does not get installed alongside the astra set —
it gets **absorbed or rejected**.

1. **Sort by component type.** Enumerate the recognized fields in the plugin's **manifest**
   — never its directory tree. Skills and commands absorb; agents get budgeted and
   dispatched to; MCP servers get declared with a fallback; hooks get owned or rejected;
   LSP servers, monitors and any unfamiliar field are kept and left alone until understood.
   Only then does the rest of this apply.
2. **Locate the cluster.** Which astra skill already owns this problem? If none does, that
   is a proposal for a new astra skill, decided deliberately against the context budget.
3. **Diff against the incumbent.** What does it do that the astra skill does not?
4. **留其精華** — take only the genuinely new capability.
5. **去之糟粕** — leave behind duplicated framing, ceremony, and anything the model already
   does by default.
6. **Vendor it.** Copy scripts in. Never link out. If it needs MCP, declare the server and
   write the fallback in the same commit.
7. **Evaluate it.** Compare the strongest applicable original, a temporary convener using the
   unchanged original, and the self-contained candidate. Require home-jurisdiction
   non-regression and the design's declared positive advantage before retirement.
8. **Place it on the ladder.** New *branch* → its own `references/<case>.md`. New rule
   affecting every branch → inline in `SKILL.md`.
9. **Prune.** `SKILL.md` back under 500 lines. References stay one level deep.
10. **Record it** in the collision map above. Keep the original installed until its explicit
    retirement gate passes.

---

## Migration

1. Build the astra skills, one cluster at a time, hottest first.
2. Compare each source oracle, temporary reference convener, and self-contained candidate on the
   same fixed corpus.
3. Require home-jurisdiction non-regression, the design's declared positive advantage, and
   internalization fidelity; then obtain user approval for each retirement.
4. Uninstall only the originals whose retirement gates passed.
5. Sweep the 133 dangling symlinks.
6. **Retire plugins per component, not per plugin.** Read the component list from the
   marketplace **manifest**, not the directory tree — LSP servers and monitors are declared
   there and are invisible to a directory scan. Disable only once every component is either
   absorbed (skills, commands), replaced (hooks), or consciously given up (agents, MCP, LSP).
7. **Fix the 5 dangling MCP references** — either configure the servers or write the
   fallbacks. `/pr` and `/trim` are live breakage today, independent of this refactor.
8. **Resolve monster-prompt** — absorb it, or draw an explicit boundary.
9. Audit: anything in `~/.claude/skills/` not matching `astra-*` is a candidate for removal,
   never automatic authorization to delete it.

---

## Open questions

- **The roster.** Which astra skills exist, and what each one is called. The 17 clusters
  above are the raw material, not the answer — cluster boundaries and merge unit are still
  under discussion.
- **Tier 1 vs Tier 2 assignment.** Which skills earn a description on day one. The first
  `/astra-tune` run over existing transcripts should inform this rather than a guess.
- **Install mechanism.** Ship astra as a **plugin** (one versioned, toggleable unit that
  can carry skills + commands + agents + hooks + MCP declarations together), or as loose
  symlinks into `~/.claude/skills/`. The 133 dangling links argue against symlinks.
- **monster-prompt.** Absorb it into astra, or divide responsibility explicitly. It
  currently owns all 8 local commands, the global CLAUDE.md rules, and a marketplace.
- **Agents.** Which of the 6 plugin agents survive, and whether astra ships its own. An
  agent cannot be flattened into a skill, so this is a separate budget from the skill roster.
- **MCP.** Which servers to configure (`jira`? `awslabs-mysql`? `context-mode`?) versus
  which dependent steps to rewrite as fallbacks.
- **Scoring constants.** The +3/+2/0 weights and the 50-invocation window are starting
  points, not measurements.

---

## References

- [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) — Anthropic. 500-line limit, one-level-deep references, progressive disclosure, naming constraints.
- [Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) — Anthropic. How metadata preloading works.
- [Claude Code Skills: scope & context management](https://www.aibuilderclub.com/blog/agent-skills-best-practices-guide) — the 20-30 skill threshold, marketplace model.
- `~/.claude/skills/writing-great-skills/GLOSSARY.md` — context load, cognitive load, granularity, router skill, progressive disclosure, branch.
