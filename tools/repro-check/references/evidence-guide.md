# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: week 1 handed you this file
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
nobody else can execute; your operator swap showed you what that feels
like. Write the map you wish your executor had.
-->
Every rubric check needs an evidence source. This guide describes the places you can look: on github.com when you are evaluating a live issue, and in the packages folder when you are in eval mode. If a signal is not listed in these evidence sources, name your own source in the rubric but display it somewhere a grader can actually look.

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

The environment record says what the reporter ran on. A missing or incomplete environment is the most common reason a stranger cannot re-run the steps.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Repo/Tool Version | The draft repro report's first paragraph or environment section | The repro report's opening environment line (e.g., "HTTPie 3.2.4 (pip), Python 3.12.4, multidict 6.6.0, macOS 14.5 (arm64)") |
| OS and architecture | Same line as Repo/Tool version. look for OS name, version, and architecture (e.g., "Fedora 44 (x86_64)", "macOS 14.6 (arm64)") | Same line as Repo/Tool version. look for OS name, version, and architecture (e.g., "Fedora 44 (x86_64)", "macOS 14.6 (arm64)") |
| Runtime or dependency versions | Same line as repo/tool version. any library or runtime the issue targets should appear (e.g., multidict version for an httpie bug, rustc version for a Rust project) | Same line as repo/tool version. any library or runtime the issue targets should appear (e.g., multidict version for an httpie bug, rustc version for a Rust project) |
| Match to issue target | Compare the versions in the environment line to the versions named in the issue body | The issue body under "## Issue" shows what the reporter ran |


## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

The steps are the procedure a stranger follows to trigger the behavior. Unfollowable steps are the second-most-common reason a package fails.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Starting state | The repro report's steps section. Look for what exists before the first command (a config file written, a service started, a flag set) | Same |
| The trigger commands | Numbered or sequenced shell commands in the repro report. Whether the commands require private files or a private repo | Same |
| Driver, backend, or config choices | Named in the steps or the environment line (e.g., `--driver vmware`, `--window-theme=dark`) | Same |
| Control run | A separate run that shows the expected behavior, isolating what triggers the bug | Same |


## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

The artifact is the thing that either confirms or fails to confirm the issue. This is the deciding family for most packages.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| The artifact itself | Command output, console log, terminal capture, error text quoted in the repro report, screenshots | Same |
| Match to issue's symptom | Issue body under "## Issue" and "## Thread highlights" | Compare the artifact to the behavior the issue describes; e.g., pkg-01's issue says `Content-Type` is absent and the artifact shows it absent |
| Wrong-target flag | The artifact shows a different error, exit code, or failure mode than the issue describes (e.g., pkg-02's artifact shows `exit status 1` with a graceful validation message, not the `capacity overflow` / `exit status 101` the issue describes) | Same |
| Cannot reproduce | The report states it could not reproduce and names what differed. the artifact shows the attempt (e.g., pkg-09's marker-order output), not a blank | Same |


## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Honesty checks whether the report's claims match what the artifacts actually show.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Overclaiming | Claims confirmation but the artifact shows a different outcome (e.g., pkg-02: "confirming the reported crash" when the output is a validation error, not a crash) | Same |
| Underclaiming or backwards expected/actual | The expected and actual fields are swapped, or the report understates what was found | Same |
| Certainty without evidence | Assertions like "guaranteed reproducible", "I verified the root cause", or "I can confirm" with no artifact or step that backs them up (e.g., pkg-13, pkg-15) | Same |
| Root cause diagnosis | A report that asserts a cause (e.g., "debounce race condition") must show the evidence for the diagnosis, not just the symptom | Same |


## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Comms covers whether the claim comment and repro report are useful and honest to the maintainer, and whether they meet the repo's stated rules.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Claim comment specificity | The draft claim comment. look for a named next step, a specific aspect of the codebase, and a statement of what was found | The claim comment under "## Candidate claim comment". look for a named next step, a specific aspect of the codebase, and a statement of what was found |
| Boilerplate over-promising | A claim comment that promises a fixed timeline (e.g., "guaranteed 2-day fix"), assigns itself without intent, or is interchangeable across any issue (e.g., pkg-19) | Same |
| AI-use disclosure requirement | CONTRIBUTING.md, AI_POLICY.md, or AI_USAGE_POLICY.md in the repo root or `.github/`. Also PR/issue templates | The repo-facts block under "contribution policy". If the policy names an AI disclosure requirement, check the claim comment for the disclosure |
| Disclosure present | The claim comment text. Pass if it names the tool and the nature of the usage (e.g., pkg-07: "I used an AI assistant to help me organize this report. I ran and verified every step myself."), or explicitly states no AI was used. Silence — a comment that neither discloses nor denies — is a fail when the policy requires disclosure. | Same |
| Repo template asks | The bug report template linked from the New Issue page compared against the draft comment. The draft comment should match what the template asks for. | The repo-facts block under "bug reports" compared to what the repro report actually provides |
