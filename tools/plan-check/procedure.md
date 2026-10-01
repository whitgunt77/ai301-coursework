# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order
1. Read `rubric.md` and `references/evidence-guide.md` to establish the active checks, verdict rule, and evidence mappings. In live mode, also read `scope.md` (confirm the issue is in the scoped repo) and `voice-guide.md`.
2. Read the package in a protective order: first read the repro evidence and control run, then read the issue and thread, and finally read the plan (`plan.md` in live mode) and the plan comment (`comment.md` in live mode). Reading the repro evidence first prevents you from falling into the wrong-cause trap where a confident plan diagnosis sways your judgment before checking what the control run actually ruled out.

## Evidence gathering
1. For `diagnosis-grounded`, record each run in the repro evidence (its input and its result), noting especially what the control run shows working; then pull the plan's diagnosed root cause and compare it directly against those runs.
2. For `scope-bounded`, extract the plan's scope section, files-to-touch list, and look for concrete creep signals (such as package upgrades, new options, rewrites, CI/CD changes, or UI additions) or reasoned deferrals.
3. For `approach-buildable`, pull the specific files listed and the concrete implementation approach described in the plan.
4. For `test-plan-observable`, pull the test plan section and look for concrete, observable outcomes (such as re-running the repro steps with expected before/after outputs).
5. For `thread-convention-aligned`, examine the plan comment and plan text against any explicit direction given by maintainers in the issue thread, open PRs, and the repo's contribution policy regarding conditional AI disclosure.
6. For `not-in-scope-stated` (preferred check), search the plan for an explicit "not in scope" line or reasoned exclusion boundary.

## Check execution
1. Execute the required checks in a logical sequence: first evaluate `diagnosis-grounded`, followed by `scope-bounded`, `approach-buildable`, `test-plan-observable`, and `thread-convention-aligned`.
2. For every check, cite a precise, one-line quote from the package text as evidence.
3. Grade each check from the evidence recorded during gathering; re-read the package only when the recorded evidence does not settle the check.
4. If evidence required for a check is genuinely absent, assign an `unclear` (`?`) grade rather than guessing or assuming intent.
5. Evaluate the preferred `not-in-scope-stated` check last; note its presence for ranking purposes only, ensuring it never alters the core verdict.

## Verdict assembly
1. Apply the verdict rule: assign an `accept` (ready) verdict if and only if all required checks pass.
2. Treat any `unclear` (`?`) or failed required check as a failure that results in a `reject` (hold) verdict.
3. Ensure preferred checks (like `not-in-scope-stated`) never change the final binary pass/fail outcome.
4. In live mode, note any voice-guide rule the plan comment breaks, quoting the rule; this never changes the verdict.
5. Output the final verdict alongside a concise justification quoting the deciding check.
