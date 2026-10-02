# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `diff-matches-plan` | Plan context (including deviation notes), PR `description`, and PR `diff` | The PR diff implements the plan's scope without unplanned work or silent creep, and every change the PR description claims is present in the diff. Any deviations or shortfalls from the plan are explicitly disclosed in both the plan's deviation notes and the PR description. | required |
| `test-evidence-valid` | Plan context (test plan section) and PR `test_evidence` | For the failure the issue reports (each failure mode the plan's test plan names, using the issue's trigger input), the test evidence shows the commands and their output before and after the change. Every other case the test plan names (new-behavior checks, suite runs, unchanged-control confirmations) is at least reported with its outcome (e.g. "`go test ./...` passes"). Fails on claims without output for a reported failure ("tested locally", "works on my machine"), on evidence that only exercises an unchanged path or control, or when any case the test plan names is missing or not mentioned. | required |
| `diff-hygiene-clean` | PR `diff` and `commits` | In lines the PR adds or changes, the diff contains no debug prints, commented-out code, dead functions, or unrelated import/formatting churn. | required |
| `standards-wall-met` | Repo-facts block (`pull requests:` line and `contribution policy` line) and PR `description` | The PR satisfies every requirement the repo-facts `pull requests:` line names (such as issue references, checklists, or changelog entries). If the contribution policy requires AI-use disclosure, the PR description discloses it; if the policy does not require it, absence of disclosure does not fail. | required |
| `well-scoped-pr` | PR `diff`, compared against the plan's files-to-touch list | The diff touches only files named in the plan's files-to-touch list. | preferred |

## Verdict rule

Accept (ready) only if every required check passes. Preferred checks never change the verdict and are used solely to rank accepted pull requests. An `unclear` grade (`?`) on any required check counts as a fail and results in a reject (hold) verdict.
