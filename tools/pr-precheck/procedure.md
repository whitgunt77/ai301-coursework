# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order
1. Read `rubric.md` and `references/evidence-guide.md` to establish active checks, evidence sources, and the verdict rule. In live mode only, also read `scope.md` first (and stop if the issue is outside the scoped repo) and `voice-guide.md`; eval mode ignores both.
2. Read the package in a protective, skeptical order to avoid the "beautiful mystery" trap (where a polished description masks an unaligned diff):
   - First, read **the plan** (including its scope, files to touch, test plan, and deviation notes) to establish what *should* be there.
   - Second, read **the diff and commits** to see what *is* actually there.
   - Third, read **the test evidence** to verify what was *run*.
   - Fourth, read **the PR title and description last**, checking its claims against steps 1–3 rather than taking them on trust.
   - Finally, read **repo facts** (`pull requests:` line and `contribution policy`) and issue thread highlights to evaluate standards and comms.

## Evidence gathering
1. For `diff-matches-plan`, list each file and hunk in the diff and mark it as planned, a disclosed deviation, or unplanned. Then list each claim in the PR description and mark whether it is present or absent in the diff.
2. For `test-evidence-valid`, list every test case named in the plan's test plan, then mark each case as shown before and after (with command and output visible) on the correct trigger input.
3. For `diff-hygiene-clean`, scan all *added* lines for debug prints, commented-out code, dead functions, and unrelated import or formatting churn.
4. For `standards-wall-met`, list each item requested in the repo-facts `pull requests:` line and mark each as met or unmet. Then read the policy line for any conditional AI disclosure requirement.
5. For `well-scoped-pr` (preferred check), compare the files in the diff directly against the plan's files-to-touch list to check for clean alignment.

## Check execution
1. Execute the required checks in a logical sequence: first evaluate `diff-matches-plan`, followed by `test-evidence-valid`, `diff-hygiene-clean`, and `standards-wall-met`.
2. For every check, cite a precise, one-line quote from the package text as evidence.
3. If evidence required for a check is genuinely absent, assign an `unclear` (`?`) grade rather than guessing or assuming intent.
4. Once evidence is recorded during the gathering stage, grade directly from those notes, re-reading only when a note fails to settle the check.
5. Evaluate the preferred `well-scoped-pr` check last; note its presence for ranking purposes only, ensuring it never alters the core verdict.
6. In live mode, ensure draft PR titles and descriptions adhere to your voice-guide rules, noting that voice infractions never alter the binary pass/fail verdict.

## Verdict assembly
1. Apply the verdict rule: assign an `accept` (ready) verdict if and only if all required checks pass.
2. Treat any `unclear` (`?`) or failed required check as a failure that results in a `reject` (hold) verdict.
3. Ensure preferred checks (like `well-scoped-pr`) and live-mode voice observations never change the final binary pass/fail outcome.
4. Output the final verdict alongside a concise justification quoting the deciding check.
