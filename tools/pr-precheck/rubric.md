# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | Plan context scope/boundary + deviation notes, candidate PR diff, and PR description fidelity claims (see evidence guide Plan fidelity) | Pass when the changed files and behavior claims stay inside the accepted plan boundary, or any difference is explicitly disclosed as an intentional deviation tied to the same issue. Fail on silent drift in either direction (diff does more or less than the plan states without disclosure, or description claims conflict with diff). Unclear when scope cannot be determined from package evidence. | required |
| test-evidence | Candidate PR test-evidence section read against the plan test plan and the repo-facts check expectations (see evidence guide Test evidence) | Pass when evidence shows an observable before/after or equivalent proof tied to the issue behavior, and reports outcome of repo-level checks requested by repo standards. Fail when evidence is generic ("tests pass"), missing observable outcome, or omits required repo checks without disclosure. Unclear when evidence is absent or unverifiable. | required |
| diff-quality | Unified diff and commit list (see evidence guide Diff quality) | Pass when the change is reviewable: primary fix is visible, commits/diff are focused, and unrelated changes (debug prints, dead/commented blocks, broad formatting changes, drive-by edits) does not materially obscure review. Fail when unrelated/debris changes materially reduce reviewability. Unclear when the package does not provide enough diff detail to evaluate. | required |
| standards-comms | Repo facts policy/template asks + candidate PR title/description content (see evidence guide Standards and comms) | Pass when required PR template asks/policy disclosures are addressed with concrete content and any explicit maintainer direction in thread highlights is engaged. Fail when required asks are ignored, disclosure required by policy is missing, or maintainer directives are visibly ignored. Unclear when the package does not contain the needed standards evidence. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. Reject if any required
check fails or is unclear. Unclear counts as fail throughout.
