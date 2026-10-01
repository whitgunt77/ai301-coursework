# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57

**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
All three issues pass every required check in your rubric, so all three are **accept**. Ranked by your preferred check, then your fit profile:

**1. #57: tech detector counts `node_modules/` and `build/` files (accept)**
- **Why it fits best:** it's a small, well-defined bug with a repro script and two failing tests (`test_node_modules_excluded`, `test_build_directory_excluded`), so you know exactly when it's fixed. It gets you reading an unfamiliar backend module (`agent/tools/tech_detector.py`), which is your main growth goal.
- **Watch out:** it's Python, which isn't in your listed stack, though the fix should be small.
- **Already investigated:** Arnavsharma2 posted a full repro on 2026-09-26. Their likely cause: `_should_skip_file` matches `"/node_modules/"`, which misses paths that start at the repo root. Under the house rule their comments don't count as a claim.

**2. #47: add example `curl` commands to `docs/API.md` (accept)**
- It's labeled `good first issue`, is a docs-only change to one file, and is estimated at 2–3 hours.
- You'd have to run the API to check each example, which is light backend practice. It teaches you less about the code than #57.

**3. #40: "Copy link" button for a public review summary (accept, but a stretch)**
- It fails your preferred `good-first-issue` check: it's a `tier-2` feature request estimated at 5–8 hours, with no beginner label.
- It's the closest match to your React/TypeScript plus full-stack goal. It touches `ReviewPage.tsx`, `shareService.ts` and `reviews.py`, plus a login-free link that expires after 30 days.
- It still passes `bounded-scope`, because it's one feature delivered in one PR. It would make a good second issue.

**Shared evidence:**
- **Maintainer:** all of the last 5 default-branch commits are from 2026-08-24 to 2026-09-16, within 60 days of today. All three issues were filed by Aburke225, a collaborator.
- **AI policy:** `docs/CONTRIBUTING.md` and the PR template don't mention AI at all, so silence passes. The PR template does require green CI on all five jobs and removing the `xfail` markers once a bug is fixed.
- **Claims:** none of the three has an assignee or a linked PR. None of the repo's open PRs (#74–#79) references them.

**Limits on this run:** I gathered evidence through the public GitHub API and web pages because the `gh` CLI needed approval. Comment summaries came from a page reader, not verbatim quotes. I didn't sample how quickly maintainers reply to issues; recent commits alone satisfied that check.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "All of the last 5 default-branch commits by Andrew Burke (Aburke225) are dated 2026-08-24 to 2026-09-16, within 60 days of 2026-10-01."},
      {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; Development: no linked PRs; no repo PR references #57. Arnavsharma2's 2026-09-26 repro comments are ignored under the Path Review house rule."},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI policy text; silence passes."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Single bug in tech_detector.py with a repro script and two named failing tests; no umbrella, sub-issue or design-debate signal."},
      {"name": "good-first-issue", "grade": "pass", "evidence": "Labels: bug, good first issue, agent, tier-1."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/47",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "All of the last 5 default-branch commits are dated 2026-08-24 to 2026-09-16, within 60 days of 2026-10-01."},
      {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; Development: no linked PRs; 0 comments; no repo PR references #47."},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template contain no AI policy text; silence passes."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Docs-only change to one file, docs/API.md; estimated effort 2-3 hours."},
      {"name": "good-first-issue", "grade": "pass", "evidence": "Labels: good first issue, docs, tier-1."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/40",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "All of the last 5 default-branch commits are dated 2026-08-24 to 2026-09-16, within 60 days of 2026-10-01."},
      {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; Development: no linked PRs; 0 comments; no repo PR references #40."},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template contain no AI policy text; silence passes."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One coherent feature (shareable read-only link that expires after 30 days) across 3 named files in one PR; no umbrella or debate signal."},
      {"name": "good-first-issue", "grade": "fail", "evidence": "Labels: enhancement, frontend, tier-2; no good-first-issue or help-wanted label; a 5-8 hour feature, not a simple doc or bug fix."}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Smoke run (`--limit 3`), original rubric: "agreement: 2/3 scored items"
2. Partial (`--only issue-01,issue-04,issue-05,issue-06,issue-10`), bounded-scope widened to accept expected vs. actual behavior for bugs: "agreement: 3/5 scored items"
3. Partial (same 5 issues), bounded-scope flipped to fail only on umbrella signals: "agreement: 4/5 scored items"
4. Partial (`--only issue-01`, with `--out` to read the grader's reasoning): "agreement: 0/1 scored items"
5. Partial (`--only issue-01,issue-05,issue-10`), sub-task clause clarified to separately claimable work: "agreement: 3/3 scored items"
6. Full run: "agreement: 16/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)"
7. Partial (`--only issue-01,issue-02,issue-07,issue-12,issue-14`), added `ai-policy` and the commit route in `maintainer-active`: "agreement: 5/5 scored items"
8. Full run, saved with `--save-run`: "agreement: 18/20 scored items  (bar: 18/20: PASS)"

**Issue analysis**

`issue-01` (conda/conda#16475, "Add permanent docs for installing PyPI packages with `conda install`"). Rubric decision: accept. Gold label: accept.

The issue successfully clears liveness, claim, and AI-policy checks with active maintainers ("All 5 of the last 5 default-branch commits are dated 2026-08-04, 1 day before the 2026-08-05 capture"), no assignees or linked pull requests ("assignees: none; linked PRs: none"), and explicit project guidelines stating "generative AI tools welcome; you are responsible for all contributions...".

Navigating the bounded-scope check required a careful look because an earlier version of my bounded-scope check rejected it as an umbrella task: the grader read it as "Issue lists 5 separate sub-tasks across 5 different files … — a checklist of independent sub-tasks". I rewrote the check so it fails only on separately claimable work, where "several files changed as parts of one coherent change, delivered in one PR, do not count." Under that wording it qualifies because these edits are unified under "a single coherent doc-consolidation change, not an umbrella list," targeting a singular documentation initiative rather than disparate features.

The failed good-first-issue check ("only 'type::documentation' (no good-first-issue/help-wanted label)") did not change the verdict because preferred checks only rank contributions rather than gate them.

**Check rationale**

| `maintainer-active` | Repo-facts block: "last push to any branch", the "last 5 default-branch commits", and the "maintainer first-response sample" | A maintainer comment response within 90 days OR at least 3 of the last 5 default-branch commits occurred within the past 60 days. | required |

The original version incorrectly required both a push within 12 months and a maintainer comment response within 90 days, which caused gold-label accept issue-14 to be wrongfully rejected because its sample issue had "no maintainer comment in thread" since it was opened just a day before capture.

A sparse response sample is weak evidence of inactivity when the repository is clearly alive, making recent default-branch commits a much fairer and more direct indicator that maintainers are actively working.

The "3 of the last 5 within 60 days" threshold remains strict enough to reliably filter out dead repos like issue-02 ("no commits or releases in over a year") and issue-07 ("repo without maintainer activity since 2025"), whose commits fall far outside the window.

**Trade-offs**

By relaxing the requirement into an OR condition, the check introduces a blind spot where a repo with active weekly maintainer commits can pass even if the core team never reviews outside PRs or responds to newcomer issues. The commit route measures whether maintainers are working rather than whether they interact with the community.

However, canary verification confirms this loosening did not compromise accuracy; re-running the dead-repo check with `--only issue-01,issue-02,issue-07,issue-12,issue-14` produced an `"agreement: 5/5 scored items"` output with both `issue-02` and `issue-07` correctly staying rejected, and the final full run reported `"dead-repo 3/3"` to ensure abandoned repos remain blocked.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to my interests and the time available.** Issue #57 fits my growth goal to dive into unfamiliar codebases—specifically exploring `agent/tools/tech_detector.py` and its associated tests. The finish line is concrete and measurable: getting two specific failing tests (`test_node_modules_excluded` and `test_build_directory_excluded`) to pass. As a tier-1 issue labeled good first issue, it works well within a standard course load across Units 2 through 4, even though working in a Python codebase is a stretch outside of my primary JavaScript/TypeScript stack.

2. **What the verdict identified correctly, and what I weighed that the rubric could not.** The verdict correctly identified key repository facts: an active maintainer with recent commits, an unclaimed status with no assignee or linked PRs, no AI restrictions, and a well-bounded bug with a clear reproduction. However, the rubric couldn't account for my personal learning curve in Python or local environment setup challenges. It also missed strategic decisions, such as my picking #57 over #40 (which was closer to my React/TS stack but required 5–8 hours of heavier frontend-plus-backend work), as well as the helpful head start provided by a classmate's existing reproduction and suspected cause.

3. **The anticipated difficulty in claiming it.** While house rules mean claim comments don't technically block a submission, practical competition is a factor. Another contributor, Arnavsharma2, has already posted a full reproduction and a likely cause involving root-level paths in `_should_skip_file`, meaning my PR must stand firmly on its own with independent tests and a clear explanation. Additionally, because claim commenting waits until Unit 2 and the underlying bug looks straightforward once diagnosed, my primary challenge will be demonstrating original understanding rather than simply echoing an existing diagnosis.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
