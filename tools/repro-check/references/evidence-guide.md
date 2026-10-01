# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives**
- Eval package: the repro report's environment line or section (often the first
  line: "Environment: …"). Compare it against the issue body, which states the
  platform, version, or build setting the bug was reported on.
- Live mode: the draft repro comment's environment section; the issue body and
  thread on GitHub for the reporter's stated target.

**What good looks like**
- The report names the OS and the version of the tool and of any dependency the
  issue concerns (e.g. "HTTPie 3.2.4, Python 3.12.4, multidict 6.6.0, macOS 14.5").
- If the issue names a specific platform, version, driver, or build setting, the
  report states its own value for that same item. A Windows-specific issue
  reproduced with no OS stated fails; a different version that is called out
  ("issue says 3.8.4; I tested 3.9.6") passes.

## Steps

**Where it lives**
- Eval package: the reproduction report's steps or procedure section detailing how replication was attempted.
- Live mode: the step-by-step instructions section of the draft claim or repro report.

**What good looks like**
- Steps provide explicit starting states, exact configuration requirements, and precise command-line sequences that a stranger can execute independently.
- Relies on public repositories, open resources, and fully detailed commands; vague instructions ("set up the project", "run the usual tests") or instructions requiring private repos fail.

## Behavior shown

**Where it lives**
- Eval package: the logs, terminal outputs, screenshots, or explicit explanation blocks in the repro report, compared directly against the bug's described behavior in the issue body.
- Live mode: the verification logs or attempt records in the draft report.

**What good looks like**
- Artifacts exhibit the exact error message, exit code, failure symptom, or trigger input specified in the issue; any version or input difference from the issue is stated in the report.
- An honest cannot-reproduce report includes clear execution records, exact environment discrepancies, and an explanation of why the bug could not be triggered.

## Honesty

**Where it lives**
- Eval package: the claim comments and repro reports, cross-referenced with their accompanying logs, artifacts, or step logs.
- Live mode: the claims made in the draft comment compared against actual terminal outputs.

**What good looks like**
- Every assertion ("reproduced", "observed failure", "traced to line X") is backed by direct evidence or reproducible steps.
- Over-claiming without proof fails, including unsupported "+1" comments, "guaranteed fixes", or claims of verification ("I verified") with zero logs or artifacts provided.

## Comms

**Where it lives**
- Eval package: the claim comment text, issue discussion history, and repo-facts contribution policy line.
- Live mode: the final draft claim comment and repository guidelines document.

**What good looks like**
- The claim names specific details from the issue and commits to investigation or reporting rather than promising immediate fixes or arbitrary deadlines.
- AI disclosure is present when required by the repository's explicit contribution policy; its absence does not fail when the policy does not mandate it.
