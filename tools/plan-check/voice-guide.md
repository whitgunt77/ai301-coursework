# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a working web developer and student new to this Python codebase, making course contributions starting with issue #57. Readers can expect careful reproductions backed by evidence, clear updates when I have new findings, and direct questions when I get stuck.

## Rules I write by

### Rule: Investigate, Don't Promise Fixes

Commit only to investigating or reporting findings rather than guaranteeing a fix or a delivery date.

- Wrong: "I'll have a PR with a complete fix up for this by Friday evening!"
- Right: "I'm reproducing the failure locally and will share my findings shortly."

### Rule: Observe, Don't Assume

Describe exact observed behavior and terminal outputs rather than speculating on unverified root causes.

- Wrong: "This is definitely happening because the path parser is ignoring root directories."
- Right: "When running the tests, I observed that `test_node_modules_excluded` failed with exit code 1."

### Rule: Name Specific Artifacts

Reference precise functions, files, or tests instead of using vague umbrella terms like "the bug" or "this issue".

- Wrong: "I'm looking into this bug in the repo files now."
- Right: "I'm reviewing `agent/tools/tech_detector.py` and the associated test cases."

### Rule: Standalone Contributions

Contribute original findings and independent reproductions instead of piggybacking on existing threads with empty affirmations.

- Wrong: "Same issue here! +1."
- Right: "I tested this behavior on my local setup; here are my reproduction logs and environment details."

## Things I never post

- Arbitrary deadlines or promises of quick patches (e.g., "Will fix this in 10 minutes").
- Vague "+1" or me-too comments without supporting logs or investigation.
- Unverified AI-generated text or code pasted directly without local testing and validation.
- Apologetic filler or excessive pleasantries that obscure technical details.
