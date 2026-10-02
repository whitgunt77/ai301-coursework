# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/82

**Branch**

`fix/57-root-vendored-paths`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (`--limit 3`): "agreement: 3/3 scored items"
2. Full run: "agreement: 16/20 scored items  (bar: 18/20: below the bar)"
3. Partial (`--only pkg-05,pkg-13,pkg-16,pkg-19,pkg-04,pkg-07,pkg-10,pkg-14`), test-evidence-valid loosened so only failure cases need output: "agreement: 7/8 scored items"
4. Partial (`--only pkg-05,pkg-07,pkg-14,calib-04 --include-calibration`), non-failure cases need a stated outcome: "agreement: 3/3 scored items"
5. Full run, saved with `--save-run`: "agreement: 20/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

* Package: `pkg-05`
* Verdicts: Final Rubric: `accept` | Gold label: `accept` (Note: It was incorrectly rejected as reject in runs 2 and 3). Gold note: "merge identity widened to (name, mode, modifier, keycode) with a replace warning; engages fdncred's uniqueness question explicitly; repro table before/after shown; template sections filled".
* Reasoning: In the initial runs, `pkg-05` failed `test-evidence-valid` because it asserted test suite success (`cargo test passes`) without showing command output — the grader wrote: “"`cargo test -p nu-protocol` passes (312 tests); fmt and clippy clean." is asserted with no command/output shown” — and, after the first revision, because it omitted the specific output for the second named case (the same-key warning binding test): "Plan's second named case ('re-run with two same-name same-key bindings, expect one row plus a warning') has no shown command/output". After adjusting the check to require before/after output only for the failure the issue reports, while accepting stated outcomes for new-behavior checks, suite runs, and controls, `pkg-05` correctly passed once the before/after repro output clearly showed the pre-fix state and post-fix binding rows: "Before/after repro output shows only the 'up' row pre-fix and both 'control/char_r' and 'none/up' rows post-fix; same-key-warning case and 'cargo test -p nu-protocol passes (312 tests)' are reported with outcome".

**Check rationale**

| `test-evidence-valid` | Plan context (test plan section) and PR `test_evidence` | For the failure the issue reports (each failure mode the plan's test plan names, using the issue's trigger input), the test evidence shows the commands and their output before and after the change. Every other case the test plan names (new-behavior checks, suite runs, unchanged-control confirmations) is at least reported with its outcome (e.g. "`go test ./...` passes"). Fails on claims without output for a reported failure ("tested locally", "works on my machine"), on evidence that only exercises an unchanged path or control, or when any case the test plan names is missing or not mentioned. | required |

* Reasoning: This check underwent an iterative tuning history: it started too strict (requiring full terminal transcripts for every named case, including general suite runs), was relaxed to accept stated outcomes for suite checks and controls, and then for new-behavior checks, while keeping its strict before/after output requirement for the failure the issue reports. Silence or lack of evidence on any explicitly named test case still correctly fails the check (retaining rejections on tricky edge cases like `calib-04`).

**Trade-offs**

* What it gives up: By loosening `test-evidence-valid` to accept stated outcomes for general test suites rather than forcing raw command/output blocks for every single line, the check will now pass a PR that falsely or inaccurately states that a secondary test suite or check passed without printing the raw terminal output.
* Why this trade-off is accepted: The canaries and final validation runs proved this trade-off is safe because it successfully preserved all core rejections under the not-tested category ("not-tested 4/4"), correctly catching silent failures like `pkg-07` ("Test evidence only shows the one-file control case passing ('Verified the fix on a single-file case...'), never the two-file repro that is the issue's actual reported failure.") and `pkg-14` ("neither repro command (single-header POST with JSON) is shown before/after."). It strikes the ideal balance between catching real missing test evidence and accommodating standard high-level test suite summaries.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
