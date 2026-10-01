# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives**
- Eval package: the plan's diagnosis/cause section; compare it against the repro
  evidence section, especially any control run (same input with one thing changed).
- Live mode: `plan.md`'s diagnosis section, compared against the repro comment I
  posted on the issue (its steps, outputs, and control run).

**What good looks like**
- The component the plan blames is consistent with every run in the repro evidence,
  and the plan quotes the output it relies on.
- A control run that shows the blamed component working (or shows the fault already
  present before it) rules that diagnosis out, however confident the plan sounds.

## Scope
**Where it lives**
- Eval package: the plan's scope and files-to-touch lists, compared against the issue body and thread to check what was originally asked.
- Live mode: `plan.md`'s scope section, files-to-touch list, and any stated "not in scope" lines, evaluated against the issue thread.

**What good looks like**
- One bounded change at an isolated site without unapproved creep signals (such as package upgrades, new options, rewrites, CI/CD changes, or UI additions).
- Reasoned deferrals or explicit "not in scope" boundaries are clearly stated and accepted.

## Executability
**Where it lives**
- Eval package: the plan's approach section and files list.
- Live mode: `plan.md`'s approach section, specific files listed, and proposed order of work.

**What good looks like**
- Names specific files to change and outlines a concrete, step-by-step implementation approach.
- Avoids deferred decisions, vague placeholders like "whichever is easier," or indefinite locations like "somewhere in the codebase."

## Test plan
**Where it lives**
- Eval package: the plan's test plan section.
- Live mode: `plan.md`'s test plan section, mapping directly onto the Unit 2 reproduction steps.

**What good looks like**
- Specifies a concrete re-run of the repro steps with expected before and after outputs.
- Avoids vague instructions like "run the full test suite" or subjective checks like "should feel fast" that lack observable outcomes.

## Honesty
**Where it lives**
- Eval package: the plan's risks and unknowns section.
- Live mode: `plan.md`'s risks & unknowns section and the `## Deviations` heading filled in after building.

**What good looks like**
- States unknowns and potential risks plainly rather than projecting false confidence.
- Records accurate, honest deviations if the final build ends up differing from the original plan.

## Comms
**Where it lives**
- Eval package: the plan comment vs. issue thread highlights / open PRs, and the repo-facts contribution-policy line.
- Live mode: draft `comment.md` compared against maintainer direction in the issue thread and the repository's contribution policy for AI use.

**What good looks like**
- Follows or actively engages maintainer direction by name in the thread or open PRs.
- Complies with repo policy regarding conditional AI disclosure in the comment.
