# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | the plan's diagnosis read against the evidence block's steps, artifacts, and control runs | The diagnosis the plan names is consistent with what the repro evidence shows. A diagnosis that contradicts a control run or ignores a step that rules it out is a fail. Unclear means the plan names no cause at all. | required |
| scope | the plan's 'in scope' and 'not in scope' statements, and the approach list, read together | The change is one bounded fix traceable to the cited diagnosis. Refactors, migrations, or a redesign included with the actual fix are a fail, even if the bug fix is correct. | required |
| executability | the plan's approach section. files or areas named, method described, order of work | A stranger who has never touched the repo could start executing without asking the author anything. No files named and no chosen approach is a fail. Every real decision deferred to build time ("whichever is easier", "somewhere") is a fail. | required |
| test-plan | the test plan read against the repro evidence's steps and artifacts | The test plan names a specific observable outcome tied to the repro evidence (the repro case passes, or a specific behavior flips, for example). Vague instructions like 'run the full test suite' with no outcome for the fix itself is a fail. | required |
| comms | the plan comment read against the thread highlights for maintainer signals, and the repo-facts block for AI-use policy and contribution conventions | The comment references any explicit maintainer direction in the thread (a root cause, a failed test, a stated preference). If the repo's stated policy requires AI-use disclosure, the comment discloses it. Silence when a disclosure is required is a fail. A comment that ignores maintainer signals and posts a plan as if the thread were empty is a fail. | required |

## Verdict rule

Accept if all required checks pass. If any required check fails or is unclear, reject. Unclear counts as fail throughout.
