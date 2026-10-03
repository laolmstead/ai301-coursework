# Procedure: how this skill grades a plan package

## Read order

Read in this order before grading any check:

1. **Repo facts block** - note the contribution policy and any AI-use disclosure requirement. Note whether the thread has an owner or maintainer comment that names a culprit or gives a direction.
2. **Issue body and thread highlights** - note what behavior is being reported and any explicit maintainer signals (a named file, a posted patch, a stated preference). These are the facts the plan comment must address.
3. **Repro evidence block** - read the steps, artifact, and control runs carefully before touching the plan. Note what the controls rule out. The repro evidence is the ground truth the diagnosis must follow from.
4. **Candidate plan** - read the diagnosis, scope, approach, and test plan in order. At each section, check it against what the repro evidence established in step 3.
5. **Candidate plan comment** - read last, against the thread highlights from step 2.

The order matters: reading the repro evidence before the plan prevents anchoring on the plan's framing. A diagnosis that sounds plausible in isolation often contradicts a control run you would have caught if you read the evidence first.

## Evidence gathering

Gather evidence for each check family before executing any check. Record a one-line note per family.

| Family | Where to pull from | What to record |
|---|---|---|
| Diagnosis | Plan's diagnosis line + repro-evidence block (steps, artifact, control runs) | The cause the plan names, and whether any control run rules it out |
| Scope | Plan's in scope/not in scope statements and approach list | Count of distinct concerns in the approach. Whether each maps to the diagnosed cause |
| Executability | Plan's approach list | Named files or areas (yes/no), chosen mechanism named (yes/no), any deferred decisions quoted |
| Test plan | Plan's test plan line and repro-evidence expected/actual | The stated observable outcome. Whether it ties to the repro steps |
| Comms | Plan comment, thread highlights, and repo-facts contribution policy | Whether maintainer signals are acknowledged, and whether AI disclosure is present if required |

Do not pull evidence mid check. Gather all five families first, then execute the checks in order.

## Check execution

Execute checks in this order: `diagnosis` → `scope` → `executability` → `test-plan` → `comms`.

The order reflects dependency: a wrong diagnosis makes scope and executability checks easier to grade (a plan built on the wrong cause often scopes the wrong thing too), and comms is always last because the comment is graded against what the thread actually said, which you established in the read order.

For each check:

- State the one fact or quote from gathered evidence that decides the grade.
- Grade `pass`, `fail`, or `unclear`.
- `unclear` means the evidence needed is genuinely absent from the package, not that the plan is thin or the writing is vague. For example, a plan with no diagnosis section at all yields `unclear` on `root cause`. A plan that states a cause that contradicts a control run yields `fail`.
- Do not reread the whole package per check. Use the notes from evidence gathering. Reread only the specific line if the note is insufficient to quote directly.

If evidence for a check is absent from the package and cannot be inferred from context, grade `unclear` and note the gap. Do not invent evidence.

## Verdict assembly

Apply the rubric's verdict rule after all five checks are graded:

- If all five required checks pass → `accept`
- If any required check fails or is `unclear` → `reject`
- `unclear` counts as `fail` throughout.

In the output JSON, the `evidence` field for each check must quote the specific fact or line that decided the grade, not a summary of the check's intent. The deciding check for a `reject` is the first failed required check in execution order. Name it in the readable summary before the JSON block.

There is no third verdict. Do not hedge with "borderline" or "conditional accept". If the package is not clearly ready, it is `reject`.
