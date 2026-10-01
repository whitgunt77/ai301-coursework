# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

whitgunt77

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57#issuecomment-5936599288

````markdown
I've investigated issue #57, building on my repro above (with only the two Python files `primary_language` is `Python`; adding root-level `node_modules/` and `build/` files changes it to `JavaScript`) and Arnavsharma2's earlier notes.

Calling `_should_skip_file` directly shows that `_should_skip_file` in `agent/tools/tech_detector.py` uses patterns with a leading slash (`"/node_modules/"` and `"/build/"`), which causes root-level vendored and build files to slip through exclusion filtering. Nested files are caught correctly, but root-level files skew language detection:

```text
'node_modules/lib/index.js'              -> False
'project/node_modules/lib/index.js'      -> True
```

**Plan of action:**
* Update `_should_skip_file` to match skipped paths at the start of strings or after any slash.
* Remove `xfail` markers from `test_node_modules_excluded` and `test_build_directory_excluded`.
* Defer the separate `sorted(languages)[0]` language-ordering bug in `tech_detector.py` as out of scope for this fix.
* Re-run the reproduction steps to confirm `Python` is correctly reported.

I will proceed with these changes in `agent/tools/tech_detector.py` and post updates once the implementation and testing are complete.
````

---

## Your branch

**Branch**

`fix/57-root-vendored-paths` (https://github.com/whitgunt77/pathreview-ai301-fa26-s1/tree/fix/57-root-vendored-paths)

**Evidence**

**Before** (unmodified code, commit `f89c06f`):

```text
$ git rev-parse --short HEAD
f89c06f

$ python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py', 'utils.py', 'node_modules/lib/index.js', 'build/static/app.js']}))"
2026-10-01 13:15:03 [info     ] tech_detected                  frameworks_count=0 languages_count=2 primary_lang=JavaScript
ToolResult(success=True, data={'primary_language': 'JavaScript', 'all_languages': ['JavaScript', 'Python'], 'frameworks': []}, error=None)

$ pytest tests/unit/test_tech_detector.py -k "node_modules or build" -v
tests/unit/test_tech_detector.py::TestTechDetector::test_node_modules_excluded XFAIL [ 50%]
tests/unit/test_tech_detector.py::TestTechDetector::test_build_directory_excluded XFAIL [100%]
====================== 25 deselected, 2 xfailed in 0.69s =======================
```

**After** (branch `fix/57-root-vendored-paths`, commit `d054a7d`):

```text
$ git branch --show-current
fix/57-root-vendored-paths

$ python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py', 'utils.py', 'node_modules/lib/index.js', 'build/static/app.js']}))"
2026-10-01 13:17:39 [info     ] tech_detected                  frameworks_count=0 languages_count=1 primary_lang=Python
ToolResult(success=True, data={'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}, error=None)

$ pytest tests/unit/test_tech_detector.py -k "node_modules or build" -v
tests/unit/test_tech_detector.py::TestTechDetector::test_node_modules_excluded PASSED [ 50%]
tests/unit/test_tech_detector.py::TestTechDetector::test_build_directory_excluded PASSED [100%]
======================= 2 passed, 25 deselected in 0.66s =======================

$ python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py','core/app.py','project/node_modules/lib/index.js','project/build/bundle.js']}))"
2026-10-01 13:17:41 [info     ] tech_detected                  frameworks_count=0 languages_count=1 primary_lang=Python
ToolResult(success=True, data={'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}, error=None)

$ make test-unit  (branch)
377 passed, 51 xfailed, 5 warnings
$ make test-unit  (main, same machine)
375 passed, 53 xfailed, 5 warnings
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (`--limit 3`): "agreement: 3/3 scored items"
2. Full run, saved with `--save-run`: "agreement: 19/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

* Package: `pkg-14`
* Verdicts: Your rubric: `reject` | Gold label: `accept`
* Reasoning: My rubric rejected pkg-14 under `approach-buildable` because it defers pinning the exact functions to be updated until after tracing query issuance with debug logs. The grader's evidence: "'exact functions to be pinned in the PR after tracing the query issuance with debug logs' — no actual files/functions named, decision deferred". However, the gold label rates this as an honestly scoped-down, acceptable plan ("honestly scoped-down: reattach handshake fix with a regression-window repro; defers the untestable Windows variant and says so; arguable on the deferral, ready as scoped") because the Unix reattach handshake scope is already bounded and backed by repro evidence. My check failed to distinguish between "deferred everything" and "deferred specific function pointers while scope remains bounded."

**Check rationale**

| `approach-buildable` | The plan's approach section and files-to-touch list | The plan names specific files to change and a clear, concrete implementation approach, avoiding deferred decisions ("whichever is easier") or missing file targets. | required |

* Why it reads this way: It targets the unbuildable category's core failure mode—decisions deferred to build time (explicitly calling out anti-patterns like "whichever is easier" inspired by `pkg-18`). I kept it strict on purpose to automatically flag vague, ungrounded plans rather than adding loose subjective exceptions.

**Trade-offs**

* What it gives up: It sacrifices `pkg-14`, an honest and bounded plan that got rejected because it defers final function pinning (eval run: "pkg-14  clear-accept       accept  reject   NO     failed: approach-buildable").
* Why this trade-off is accepted: This strictness is exactly what successfully catches all three unbuildable plans ("unbuildable 3/3"), such as `pkg-10` ("No specific files named anywhere in the plan"), `pkg-17` ("'gocui? tcell? not sure which layer is responsible' — deferred decision, no files named"), and `pkg-18` ("'fix the type logic, either upstream or in the vendored copies, whichever turns out to be easier' — no files named, decision deferred"). Loosening the check to rescue `pkg-14` risks allowing those unbuildable plans through, and a 19/20 score already clears the course bar comfortably.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
