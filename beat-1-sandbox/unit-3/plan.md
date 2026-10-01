# Plan: Fix root-level vendored file exclusion (#57)

## Diagnosis
The root cause of issue #57 is that `_should_skip_file` in `agent/tools/tech_detector.py` misses root-level vendored paths because every pattern includes a leading slash (`"/node_modules/"`, `"/build/"`), restricting matches to paths where the folder appears nested.
* Local check I ran on my fork (commit `f89c06f`), calling `_should_skip_file` directly (not part of my posted repro; the first and third lines are also quoted in my plan comment):
  > `'node_modules/lib/index.js'              -> False`
  > `'build/bundle.js'                        -> False`
  > `'project/node_modules/lib/index.js'      -> True`
  > `'project/build/bundle.js'                -> True`
* My posted repro shows the effect: with only `main.py` and `utils.py`, the result is `'primary_language': 'Python'`; adding `node_modules/lib/index.js` and `build/static/app.js` changes it to `'primary_language': 'JavaScript'`, `'all_languages': ['JavaScript', 'Python']`. The vendored `.js` files are not filtered, so JavaScript enters the language set.
* Nested-path control (local check on my fork, not part of my posted repro): the same kind of files one level down are filtered. `['main.py','core/app.py','project/node_modules/lib/index.js','project/build/bundle.js']` returns `{'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}`.

## Scope
### In Scope
* Fix path matching in `_should_skip_file` to ensure skipped folders match correctly at the start of the path as well as after any `/`, covering all patterns (`node_modules/`, `build/`, `vendor/`, `dist/`, `.git/`, etc.).
* Remove `xfail` markers from `test_node_modules_excluded` and `test_build_directory_excluded` so they pass.

### Not In Scope
* The `sorted(languages)[0]` "most common" language sorting bug.
* **Reason for deferral:** This is a separate behavior where the alphabetically first language wins over actual frequency. It is out of scope for #57, and issue #57's tests do not require fixing it. Explicitly separating this prevents scope creep.

## Branch
* `fix/57-root-vendored-paths` on my fork (`whitgunt77/pathreview-ai301-fa26-s1`)

## Files to Touch
* `agent/tools/tech_detector.py` (`_should_skip_file`)
* `tests/unit/test_tech_detector.py` (`test_node_modules_excluded`, `test_build_directory_excluded`)

## Approach
1. In `_should_skip_file`, match the patterns against `"/" + filepath` instead of `filepath`, so a folder at the start of the path gets the same leading slash the patterns already expect. The pattern list itself stays unchanged.
2. Remove the `@pytest.mark.xfail(strict=True, ...)` decorators from `test_node_modules_excluded` and `test_build_directory_excluded`.
3. Verify via unit tests and manual repro runs that root-level vendored files are successfully filtered out.

## Test Plan
1. Re-run my Unit 2 repro Step 3 against the modified code:
   ```bash
   python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py', 'utils.py', 'node_modules/lib/index.js', 'build/static/app.js']}))"
   ```
   * **Before:** `ToolResult(success=True, data={'primary_language': 'JavaScript', 'all_languages': ['JavaScript', 'Python'], 'frameworks': []}, error=None)`
   * **Expected after:** `ToolResult(success=True, data={'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}, error=None)`
2. Run the two target tests:
   ```bash
   pytest tests/unit/test_tech_detector.py -k "node_modules or build" -v
   ```
   * **Before:** both report `XFAIL`.
   * **Expected after:** `2 passed`, no `XFAIL`.
3. Re-run the nested-path control from the Diagnosis as a regression check; expected output stays `{'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}`.
4. Run `make test-unit`; expected: no new failures compared with `main`, since CI requires `test-unit` to stay green.

## Risks and Unknowns
* `test_vendor_files_excluded` currently lacks an assertion and passes regardless. Decision: leave it unchanged and out of scope for this fix; the `"/" + filepath` change also covers root-level `vendor/` paths, but adding assertions to other tests is separate test-quality work.
* Filtering paths by segment could potentially create edge cases if a valid source folder is genuinely named `build/` at the root.

## Deviations
Nothing changed; the plan held: same approach, same files touched, and `test_vendor_files_excluded` was left alone as planned.
