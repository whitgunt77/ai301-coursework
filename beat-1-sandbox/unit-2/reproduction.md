# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

whitgunt77

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57#issuecomment-5932577665

> Hi, I am a developer contributing as part of a course project working on #57.
>
> I'll run the issue's test snippet targeting `agent/tools/tech_detector.py` and execute the unit tests `test_node_modules_excluded` and `test_build_directory_excluded` on my local setup to check how `primary_language` handles `node_modules/` and `build/` paths.
>
> I'll post my environment, exact steps, and observed output here for review before proposing any modifications.
>
> Note: I am using an AI assistant to help draft and check comments for this contribution.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57#issuecomment-5932842770

````markdown
## Environment
- OS: macOS 26.6.2 (arm64)
- Python: 3.12.15 (installed via Homebrew)
- Key Packages: pytest 9.1.1, structlog 26.1.0
- Fork / Commit: https://github.com/whitgunt77/pathreview-ai301-fa26-s1 at commit `f89c06fc3ff292df2a04a39ac51319d32a76b779` (unmodified, clean working tree)
- Setup Notes: Ran the Python steps of `make setup` (virtual environment creation and dev dependencies installation). Skipped Docker, database migrations, seed data, and frontend steps as they are not required for unit tests.

## Steps
1. Clone the fork and check out the commit:
   ```bash
   git clone https://github.com/whitgunt77/pathreview-ai301-fa26-s1.git
   cd pathreview-ai301-fa26-s1
   git checkout f89c06fc3ff292df2a04a39ac51319d32a76b779
   ```
2. Install Python 3.12 via Homebrew and create a virtual environment:
   ```bash
   brew install python@3.12
   python3.12 -m venv .venv
   source .venv/bin/activate
   pip install -e ".[dev]"
   ```
3. Run a smaller version of the issue's example (2 Python files, 1 `node_modules/` file, 1 `build/` file):
   ```bash
   python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py', 'utils.py', 'node_modules/lib/index.js', 'build/static/app.js']}))"
   ```
4. Run the control with only the two Python files:
   ```bash
   python -c "from agent.tools.tech_detector import TechDetector; print(TechDetector().execute({'files': ['main.py', 'utils.py']}))"
   ```
5. Run the targeted unit tests with `--runxfail` to surface the underlying assertions:
   ```bash
   pytest tests/unit/test_tech_detector.py -k "node_modules or build" --runxfail
   ```

## Observed Behavior & Comparison
- Step 3 output (expected `Python`, got `JavaScript`):
  ```text
  [info     ] tech_detected                  frameworks_count=0 languages_count=2 primary_lang=JavaScript
  ToolResult(success=True, data={'primary_language': 'JavaScript', 'all_languages': ['JavaScript', 'Python'], 'frameworks': []}, error=None)
  ```
- Step 4 control output, with only the two Python files (`main.py`, `utils.py`):
  ```text
  [info     ] tech_detected                  frameworks_count=0 languages_count=1 primary_lang=Python
  ToolResult(success=True, data={'primary_language': 'Python', 'all_languages': ['Python'], 'frameworks': []}, error=None)
  ```
  With only the two Python files, `primary_language` is `Python`; adding the `node_modules/` and `build/` files changes it to `JavaScript`.
- Step 5: Without `--runxfail`, both tests report `XFAIL`, because they are marked as expected failures for #57. With `--runxfail`, both `test_node_modules_excluded` and `test_build_directory_excluded` failed with:
  ```text
  >       assert data["primary_language"] == "Python"
  E       AssertionError: assert 'JavaScript' == 'Python'
  ```
  ```text
  2 failed, 25 deselected
  ```

## What's Next
I am continuing my investigation into how `agent/tools/tech_detector.py` evaluates and filters paths to see why `node_modules/` and `build/` directories are currently processed. I'll post what I find here.
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (`--limit 3`): "agreement: 3/3 scored items"
2. Full run, saved with `--save-run`: "agreement: 20/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

`pkg-20` (ghostty, `disclosure` category). Rubric decision: reject. Gold label: reject (gold note: "excellent repro on every proof check; ghostty's stated AI policy requires disclosing all AI usage and the comments do not disclose").

`pkg-20` is rejected despite featuring an excellent reproduction because the target repository (Ghostty) explicitly requires all AI usage to be disclosed, and neither the claim comment nor the repro report included a disclosure statement. My rubric passed every proof check — for example `behavior-shown`: "Output `^[[?997;2n` (light) for single-theme vs `^[[?997;1n` (dark) for the conditional-pair control exactly matches the issue's described mode-2031 mismatch" — and failed only `conditional-disclosure`: "Repo-facts: 'All AI usage in any form must be disclosed' — neither the claim comment nor the repro report contains any disclosure statement." This demonstrates that a flawless technical verification cannot buy back a convention violation; a repository's stated policy is a hard requirement that gates the entire contribution.

**Check rationale**

| `conditional-disclosure` | Repo-facts block's "contribution policy" line; claim comment and repro report | If the target repository's explicit policy requires AI/automation disclosure, the claim comment or repro report discloses it; if the policy does not require it, absence of disclosure does not fail. | required |

I rejected an unconditional "always disclose" rule because it would have incorrectly failed packages like `pkg-05`, where conda's policy is permissive without a disclosure requirement. I revised the check's scope to explicitly target the repo-facts contribution policy line and verify both the claim comment and repro report, ensuring disclosure is only enforced when the repository's rules demand it (as seen in `pkg-07`).

**Trade-offs**

Because the initial rubric achieved a perfect score on the first full run ("agreement: 20/20 scored items  (bar: 18/20: PASS)", with "disclosure 1/1" on the categories line), no checks required revision and no package results flipped. However, the `conditional-disclosure` check accepts a blind spot: it relies strictly on the stated policy line in the repo-facts block. If a repository buries its AI disclosure requirement elsewhere—such as in a separate PR template or discussion thread—the check will see no policy and incorrectly pass an undisclosed package, highlighting that the check reads the explicit policy line rather than hunting across peripheral repository files.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
