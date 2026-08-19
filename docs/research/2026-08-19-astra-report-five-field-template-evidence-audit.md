# Astra Report five-field template — evidence and risk audit

**Date:** 2026-08-19

**Status:** Research and design-exploration record only. The user subsequently approved the
conditional recommendation in section 6, which is recorded authoritatively in
`designs/astra-report.md`; this file does not itself amend that design, authorize runtime work, or
claim that the proposed template has been empirically validated.

**Question:** What does the available book distillation and Deep Research evidence support about
the repeated section shape below, and what risks arise if Astra makes it a Standard default?

```text
[TOPIC]
  [MOTIVATION]
  [WHAT IS IT?]
  [IMPACT]
  [ACTION]
```

## 1. Executive conclusion

The evidence supports all five **communication functions** individually. It does not establish
five mandatory visible headings, their fixed order, or their universal use across report jobs.

The template is defensible as a default semantic checklist and comparison route for a
**multi-topic decision or review report** when the producer supplies complete case semantics. It
should not become a rigid grammar for progress updates, failures, incident timelines, raw evidence
audits, single-answer explanations, or other jobs whose natural structure differs.

The safest continuation is therefore:

> Preserve `TOPIC / MOTIVATION / WHAT IS IT? / IMPACT / ACTION` as a recognizable multi-topic
> route, while allowing redundant fields to merge, irrelevant fields to disappear, and `ACTION`
> or the governing conclusion to move first for a blocker or live decision.

This is a coherent synthesis of the local [book distillation](./2026-08-18-astra-report-book-distillation.md#5-evaluation-of-the-repeated-five-field-topic-block)
and the stance [Deep Research resolution](./2026-08-19-astra-report-stance-deep-research-resolution.md),
especially its answers to questions 31–34. The stance investigation appears scattered on report
structure because its primary problem was delegated authority and principal switching, not the
optimal prose grammar.

## 2. Evidence classification

- **Direct:** the source addresses a closely matching writing or reporting operation.
- **Analogical:** the source studies another medium or task and suggests a testable transfer.
- **Astra synthesis:** the rule combines source advice with Astra's authority and artifact model.
- **Product choice:** an explicit default that must be evaluated rather than attributed to a
  source.

## 3. Field-level evidence and limits

| Function | Evidence supporting the function | Boundary relevant to Astra |
|---|---|---|
| `TOPIC` | **Direct.** Minto's governing-point and logical-grouping guidance; Redish's meaningful topics and headings; Rogers and Lasky-Fink's separation of distinct ideas and grouping of related ones. | A category label such as `Testing` is not itself a useful governing point. The heading should normally expose the producer's conclusion or significance, for example `Testing — retry behavior remains unverified`. |
| `MOTIVATION` | **Direct.** Williams and Bizup's condition/problem/cost framing; Redish's reader-purpose planning; Rogers and Lasky-Fink's “why care” operation; Diátaxis on bounded context in explanation. | Motivation must come from the producer case or the user's explicit reporting question. Report may not invent urgency, relevance, or project purpose merely to fill the field. |
| `WHAT IS IT?` | **Direct + analogical.** Redish, Williams and Rogers/Lasky-Fink support familiar, explicit wording; multimedia pre-training work analogically supports establishing necessary unfamiliar concepts before relying on them. | Re-explaining an already clear term adds noise. If `MOTIVATION` depends on an unfamiliar concept, Report may need to explain that concept first rather than preserve the proposed order mechanically. |
| `IMPACT` | **Direct.** Williams and Bizup's cost/consequence reasoning; Minto's requirement to state what support means; Rogers and Lasky-Fink's relevance operation; Nygard's consequences field. | `MOTIVATION` and `IMPACT` easily duplicate one another. Motivation should mean why the topic is live; impact should mean what follows from the finding or decision, including material uncertainty and caveats. |
| `ACTION` | **Direct.** Rogers and Lasky-Fink support gathering the ask and reducing response effort; Minto distinguishes uncontroversial next steps from disputed recommendations; BLUF precedent puts a governing point first. | Fifth position is unsafe for a blocker, urgent failure, or live approval request. `No action required` is valid only when the producer explicitly supplies that condition. Report may not invent an option or preferred choice. |
| Repeated shape | **Direct + analogical.** Minto, Redish and Rogers/Lasky-Fink support consistent grouping and navigable structure; signaling research analogically supports organizational cues. | No inspected source validates exactly five labels, this order, or repeated static blocks for engineering supervision. Repetition helps only when topics are genuinely comparable. |

Primary or first-party anchors include the authors' [Writing for Busy Readers checklist](https://writingforbusyreaders.com/wp-content/uploads/2023/10/Writing-for-Busy-Readers-Checklist.pdf),
Redish's first-party chapters on [planning](https://redish.net/wp-content/uploads/Redish_2nd_ed_Chap_2.pdf)
and [key messages](https://redish.net/wp-content/uploads/redish_2nd_ed_chap_7.pdf),
Nygard's original [ADR essay](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions),
[Diátaxis Explanation](https://diataxis.fr/explanation/), and the official
[W3C PROV-DM](https://www.w3.org/TR/prov-dm/). Precise local-book editions, hashes, chapters, and
page locators are preserved in the [book distillation](./2026-08-18-astra-report-book-distillation.md#11-local-source-record).

## 4. Material risks in continuing unchanged

### 4.1 Rigid repetition can recreate overload

Five headings per short topic can cost more attention and tokens than they save. `TOPIC` may
already communicate `WHAT IS IT?`; `MOTIVATION` and `IMPACT` may contain the same sentence; an
informational topic may have no real `ACTION`. Mandatory empty or repetitive fields contradict the
busy-reader principle of reducing ideas, requests, formatting, and response effort.

**Mitigation:** treat the fields as semantic obligations to check, not mandatory headings to print.
Merge or omit a field when doing so loses no information.

### 4.2 The governing point or action can be buried

Minto, Redish, and BLUF precedent all support exposing the governing point early. A live approval,
blocker, or urgent failure placed after four fields delays the information that controls the
reader's task.

**Mitigation:** use the normal order for deliberate comparison; move `ACTION` and its consequence
first when the producer marks the topic blocking, urgent, or decision-required.

### 4.3 A generic topic name can hide the conclusion

`Testing`, `Architecture`, or `Security` tells the reader where a section belongs, but not what it
means. The user must still reconstruct the finding.

**Mitigation:** make the topic line an informative, attributed headline carrying the producer's
governing point: `2/5 Testing — Test finds the retry path unverified`.

### 4.4 The order can violate familiar-to-new flow

`MOTIVATION` may use a technical term whose explanation does not arrive until `WHAT IS IT?`.

**Mitigation:** explain a necessary unfamiliar concept before relying on it, or place the plain
explanation directly in the informative topic heading. Field order is subordinate to
comprehension and fidelity.

### 4.5 The template can force unauthorized inference

If the producer supplies a finding but no motivation, consequence, action, or recommendation,
pressure to complete all five fields can cause Report to invent the missing case.

**Mitigation:** producer inputs must distinguish recorded content, `none`, `not applicable`, and
missing information. Report omits, merges, or names a gap; it never fabricates a plausible field.

### 4.6 Independent blocks can hide relationships

One block per topic can fragment shared causes, dependencies, one decision spanning several
findings, or disagreements among producers. It can also expose several unrelated `ACTION` fields
at once and recreate reply-surface overload.

**Mitigation:** preserve producer-recorded dependency/conflict links, group only relationships the
producer supplies, and consolidate actual user commitments in one decision panel where their
semantics allow it. Conflicting principals remain separate and attributed.

### 4.7 Principal, evidence, and caveats are not named by the five labels

The block is not authority-complete merely because all five fields appear. A stance-bearing report
still needs to reveal whose position is being presented, which source revision supports it, and
which material qualification could change the decision.

**Mitigation:** incorporate the represented principal into the topic heading and attach stable
evidence links to consequential claims. Keep caveats in the field they qualify rather than adding
another repetitive boilerplate heading.

### 4.8 Different report jobs need different grammars

Progress is naturally chronological or state-oriented; an incident may require a timeline; a
failure needs error, boundary, consequence, and permitted next action; an evidence audit needs
claim-to-evidence trace; a single answer may need only one governing sentence and support.

**Mitigation:** choose structure from the report job. The five-field route is a strong default for
several comparable explanatory or decision topics, not for every output entering Report.

### 4.9 No direct validation exists for the exact template

No inspected study tests this exact five-field structure for agentic engineering supervision. The
field count, labels, order, and effects on decision quality remain Astra product hypotheses.

**Mitigation:** document the default as testable and compare it with job-specific and flatter
reports using decision accuracy, severe-item recall, time to correct action, navigation cost,
unsupported inference, and user workload. Preference alone is insufficient.

## 5. Recommended conditional contract

### 5.1 When the route applies

Use the five functions when all of the following are true:

1. the report contains several producer-defined topics;
2. the topics are comparable enough that repeated orientation aids scanning;
3. each topic has a recorded governing point, reason or context, explanation, consequence, and
   action state—or an explicit `none/not applicable` value;
4. dependencies and conflicts remain visible; and
5. the repeated labels add more orientation than visual and token cost.

### 5.2 Rendering rules

```text
2/5  [PRODUCER] Informative topic headline carrying the governing point
     MOTIVATION  Why this topic is live, when distinct
     WHAT IS IT? Plain explanation and exact technical term, when needed
     IMPACT      Recorded consequence, uncertainty, and caveat
     ACTION      Exact ask, decision, or producer-recorded no-action state
     Evidence    Stable source references attached compactly
```

The indentation shows semantic ownership; it is not a requirement to print every label. Report
may render two adjacent functions as one sentence when their meanings coincide. It may not merge
different principals, hide a caveat, or strengthen a recommendation.

For a blocking or time-critical topic, use:

```text
2/5  [PRODUCER] Informative topic headline
     ACTION      Complete decision or required response
     IMPACT      Consequences and qualification
     WHAT IS IT? Minimum explanation needed to decide safely
     MOTIVATION  Additional recorded context, only if useful
```

### 5.3 Report-level coherence

Repeated topic blocks do not themselves provide a global conclusion. A multi-topic report should
therefore open with one producer-supported governing outcome or live decision and make
cross-topic dependencies visible. This need not recreate Capsule/NOW/menu terminology or require
another conversational turn.

### 5.4 Interaction rule

All top-level topic sections may be delivered in one consolidated Standard response. Evidence and
audit depth remain addressable without forcing one conversational turn per topic. Actual decisions
and polished user feedback use the separately approved consolidated decision panel.

## 6. Evidence-based decision

Continuing with the user's template is reasonable if Astra adopts it as a **conditional semantic
skeleton** rather than a universal literal form. The evidence argues against abandoning it, but
also against claiming the sources prove its exact labels, order, or universal superiority.

The design should say:

> For a report containing several comparable explanatory or decision topics, Report normally
> checks and presents the topic's governing point, motivation, plain explanation, impact, and
> action. It may merge or omit a redundant or inapplicable visible field, reorder the functions
> when a producer-marked blocker or live decision requires the action first, and select a
> job-specific grammar when the five-field route would distort the material.

That rule preserves the user's intended comprehension path while respecting the books' strongest
common conclusion: purpose and the reader's actual task determine structure.

## 7. Source-status note

The official June 2026 [MARADMIN 281/26](https://www.marines.mil/News/Messages/Messages-Display/Article/4521548/announcement-of-the-operational-data-integration-nexus-odin-as-the-authoritativ/)
states that MCO 3000.2J reporting requirements remain effective until a future MCO 3000.2K is
released. No official 2K publication was found during this audit. The existing method canon may
continue treating 2J as current operational precedent, while noting the pending rewrite and ODIN
platform transition.
