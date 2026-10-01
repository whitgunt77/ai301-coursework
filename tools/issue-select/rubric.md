# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `maintainer-active` | Repo-facts block: "last push to any branch", the "last 5 default-branch commits", and the "maintainer first-response sample" | A maintainer comment response within 90 days OR at least 3 of the last 5 default-branch commits occurred within the past 60 days. | required |
| `unclaimed` | Repo-facts block: "this issue: assignees" and "linked PRs" | The assignees field lists "none", and there are no open linked PRs actively racing or claiming the issue. | required |
| `ai-policy` | Repo-facts block: "contribution policy" line | The contribution policy explicitly allows assistive AI use, OR states no restrictions against AI-generated code and documentation (it does not explicitly ban AI contributions outright). | required |
| `bounded-scope` | Issue body, labels, and comment thread | Fails only when an umbrella signal is present: the issue calls itself a tracking, umbrella, meta, or mega-issue; asks for a change across the whole codebase or "all" modules/files; is a list of separately claimable pieces of work, each meant to be its own PR or taken by a different contributor (e.g., "pick one", one checkbox per module, linked sub-issues) — several files changed as parts of one coherent change, delivered in one PR, do not count; or has an unresolved design debate in the comment thread with no agreed approach. Otherwise passes, including terse maintainer-filed issues and long issues with a single settled spec. | required |
| `good-first-issue` | Issue body and labels | The issue carries a "good first issue" or "help wanted" label, or is a straightforward doc/bug fix suitable for a newcomer. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if every required check passes. Preferred checks never change the verdict and are used solely to rank accepted issues. An `unclear` grade on any required check counts as a fail and results in a reject verdict.
