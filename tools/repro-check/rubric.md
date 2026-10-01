# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `environment-logged` | Repro report (its environment line or section), compared against the issue body's stated platform/version | The OS and the versions of the tool and dependencies the issue concerns are explicitly recorded in the report; if the issue names a specific platform, version, driver, or build setting, the report states its own value for it. | required |
| `repro-steps` | Repro report (its steps and commands) | Step-by-step instructions are provided that are public, actionable, and allow a third party to attempt replication from a stated starting state, without access to private code, unshared configs, or unstated setup. | required |
| `behavior-shown` | Repro report's output excerpts, logs, or screenshots, compared against the issue body's reported behavior | Demonstrates either a successful reproduction whose shown output matches the error, message, exit code, or behavior reported in the issue body, produced with the issue's trigger input (any version or input difference from the issue is stated in the report), **OR** a genuine, documented attempt that shows its output and honestly names what differed between the reporter's environment and the attempt, leading to a cannot-reproduce outcome. | required |
| `honest-claims` | Claim comment and repro report, checked against the artifacts the report shows | Claims are backed by direct evidence or explicit steps, avoiding unsupported "+1" affirmations, confident guesswork without artifacts, or fabricated findings. | required |
| `claim-specific` | Claim comment, compared against the issue body | The claim names at least one specific detail from this issue (an error message, command, file, function, or version) and promises only investigation or a report as the next step, never a fix, a guaranteed outcome, or a delivery date. | required |
| `conditional-disclosure` | Repo-facts block's "contribution policy" line; claim comment and repro report | If the target repository's explicit policy requires AI/automation disclosure, the claim comment or repro report discloses it; if the policy does not require it, absence of disclosure does not fail. | required |

## Verdict rule

An item passes if it meets `environment-logged`, `repro-steps`, `behavior-shown`, `honest-claims`, `claim-specific`, and `conditional-disclosure`. Honest cannot-reproduce reports that document attempted replication steps and variances pass `behavior-shown`. Terse phrasing or minor, acknowledged version differences do not cause a failure. An `unclear` grade on any required check counts as a fail, except on a claim-only draft, where the repro-report checks (`environment-logged`, `repro-steps`, `behavior-shown`) are not yet applicable and do not count toward the verdict.
