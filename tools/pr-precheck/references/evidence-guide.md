# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives**
- Eval package: plan context (including deviation notes), PR title, PR description, and PR diff.
- Live mode: `plan.md` in your fork's folder (with its `## Deviations` section), along with your draft PR title and description, compared against the git diff (`git diff main...HEAD`).

**What good looks like**
- The PR diff precisely implements the plan's scope without unapproved work, feature creep, or silent omissions.
- A description claiming more or less than the diff actually delivers is caught as silent drift rather than treated as a minor communication issue.
- Any shortfalls or changes from the original plan are explicitly and honestly disclosed in *both* the plan's deviation notes and the PR description, which re-ties any potential mismatch.

## Test evidence (harness category: not-tested)

**Where it lives**
- Eval package: plan context (test plan section) and PR `test_evidence` field.
- Live mode: the test plan section in `plan.md` mapped against your captured before and after test evidence transcripts (including the outcome of the repo's own checks or test suite, such as unit test results).

**What good looks like**
- The test evidence re-runs the specific cases named in the plan's test plan—covering every required case on the correct path, rather than running the wrong path or testing unchanged code paths.
- Before and after outputs are clearly visible, demonstrating the bug's presence before the fix and its resolution after.

## Diff quality (harness category: unreviewable)

**Where it lives**
- Eval package: PR `diff` and `commits` fields.
- Live mode: the output of `git diff main...HEAD` and the commit list from `git log main..HEAD`, run from your working branch.

**What good looks like**
- The diff is clean and reviewable, free of debris tells such as leftover debug prints, commented-out code blocks, dead functions, unrelated imports, or drive-by formatting churn.
- Changes are strictly scoped and focused on the task at hand.

## Standards and comms (harness category: standards-wall)

**Where it lives**
- Eval package: repo-facts block (`pull requests:` line and `contribution policy`), PR template requirements, and PR description.
- Live mode: repository template files like `.github/PULL_REQUEST_TEMPLATE.md` and contribution guidelines like `docs/CONTRIBUTING.md`, evaluated against your PR description and contribution policies.

**What good looks like**
- The PR template sections are filled out with real, substantive content (such as issue references, checklists, and changelog entries) rather than left blank or ignored.
- Repository contribution policies regarding conditional AI-use disclosure are fully complied with and clearly stated in the PR description.
- Maintainer direction or open thread discussions are actively engaged and respected.
