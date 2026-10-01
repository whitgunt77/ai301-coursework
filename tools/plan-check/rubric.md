# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `diagnosis-grounded` | The plan's diagnosis section, compared against every run in the repro evidence (including any control run) | The component the plan blames is consistent with every run in the repro evidence, including any control run; fails if a run shows the blamed component behaving correctly, or shows the fault already present before the blamed component is reached. The plan quotes or cites the repro evidence it relies on. | required |
| `scope-bounded` | The plan's scope section and files-to-touch list, compared against the issue body and thread highlights | The plan addresses the specific bug at the code sites the repro evidence or thread isolates. Fails if the plan adds work the issue never asked for: dependency upgrades or migrations, new options or settings, rewrites or module restructures, CI changes, or UI rework. Explicitly stated and reasoned deferrals or "not in scope" items are acceptable. | required |
| `approach-buildable` | The plan's approach section and files-to-touch list | The plan names specific files to change and a clear, concrete implementation approach, avoiding deferred decisions ("whichever is easier") or missing file targets. | required |
| `test-plan-observable` | The plan's test plan section | The test plan specifies concrete, observable outcomes (such as re-running the repro steps with expected before/after outputs) rather than vague directives like "run the full test suite" or "should feel fast." | required |
| `thread-convention-aligned` | The plan comment, compared against thread highlights and the repo-facts block's contribution-policy line | If a maintainer or owner gave explicit direction in the thread (or an open PR addresses the issue), the plan comment follows it or engages it by name. If the repo-facts contribution policy requires AI-use disclosure, the plan comment discloses it; if the policy does not require it, absence of disclosure does not fail. | required |
| `not-in-scope-stated` | The plan's scope section | The plan includes an explicit "not in scope" or deferral line naming at least one related change it will not make. | preferred |

## Verdict rule

Accept (ready) only if every required check passes. An `unclear` grade (`?`) on any required check counts as a fail and results in a reject (hold) verdict. Preferred checks never change the verdict; they only help rank plans that are accepted.
