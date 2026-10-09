# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

Read the package in this order before grading any check:

1. **Repo facts and issue context**: capture required PR-template asks,
   contribution policy requirements (including AI disclosure if
   present), the issue body, and any explicit maintainer direction in thread highlights.
2. **Plan context**: read accepted plan scope/boundary, not-in-scope
   limits, test plan, and any recorded deviation notes.
3. **Candidate PR title and description**: note claims about what was
   changed and what was tested (in live mode this is often from
   `pr_draft.md`, first line title and remaining lines description).
4. **Commit list and unified diff**: capture actual touched files,
   behavioral change surface, and reviewability/debris signals (in live
   mode from `git diff <default-branch>...HEAD`, usually
   `git diff main...HEAD`).
5. **Candidate test evidence**: capture observable before/after evidence
   and repo-check outcomes (in live mode often from
   `test_evidence.md`).

This order prevents anchoring on PR verbiage. The plan establishes allowed scope before reading the diff, and the diff establishes reality before trusting test claims.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

Gather all evidence families first, then execute checks. Record a one line note per family

| Family | Where to pull from | What to record |
|---|---|---|
| Plan fidelity | Plan context (scope + not-in-scope + deviations), PR description claims, unified diff | Planned boundary, actual touched files/behaviors, and any mismatch (more/less) with whether it is explicitly disclosed |
| Test evidence | Plan's test plan, PR test-evidence block, repo-facts required checks | Observable outcome named, before/after (or equivalent) shown, and requested repo checks reported |
| Diff quality | Unified diff + commit list | Whether fix is visible and focused, and any unrelated garbage that harms reviewability |
| Standards and comms | Repo facts asks/policy, thread highlights, PR title/description | Which required sections/disclosures are present, and whether explicit maintainer direction is acknowledged |

Evidence gathering rules:

- Do not pull evidence mid check. Gather all four families first, then execute the checks in order.
- Record one decisive line or quote per family that can support check grading.
- Do not invent missing evidence. If a required signal is absent, mark the family as missing and carry that to check execution as `unclear` or `fail` per rubric condition.
- In eval mode, only read bundle text. In live mode, gather from sources named in the evidence guide.
- In live mode, if `plan.md`, `pr_draft.md`, or `test_evidence.md` appear in the implementation diff and are not required by repo policy, record that as reviewability debris for the diff-quality check.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

Execute checks in rubric order:

1. `plan-fidelity`
2. `test-evidence`
3. `diff-quality`
4. `standards-comms`

For each check:

- Use gathered evidence only; reread specific source lines only if you need a precise quote.
- Grade `pass`, `fail`, or `unclear`.
- `unclear` means the necessary evidence is genuinely unavailable in the package/source world for this mode, not that the plan is thin or the writing is vague.
- Write a single evidence line naming the fact/quote that decided the grade.

If evidence for a check is absent from the package and cannot be inferred from context, grade `unclear` unless the rubric's
pass/fail condition explicitly makes that absence a fail. Note the gap. Do not invent evidence.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

Assemble the rubric's verdict rule after all four checks are graded:

- If all required checks pass: `accept`.
- If any required check fails or is unclear: `reject`.
- Treat `unclear` as fail for verdict purposes.

For summary reporting, the deciding failure is the first non-passing
required check in rubric order. Name that check in the readable summary
before emitting JSON.

Output must end with the required fenced JSON block and nothing after
it.

There is no third verdict. Do not hedge with "borderline" or "conditional accept". If the package is not clearly ready, it is `reject`.
