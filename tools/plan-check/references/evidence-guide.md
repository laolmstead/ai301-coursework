# Evidence guide: where evidence lives in a plan package

Every rubric check needs an evidence source. This guide describes where to look: on GitHub when grading a live package, and in the `packages/` bundle when in eval mode. If a signal is not listed here, name your own source in the rubric but point to something a grader can actually find.

## Diagnosis and grounding

The plan's cause must follow from what the repro evidence actually showed, not from what the issue title or thread guesses/assumes.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Stated cause | The plan's diagnosis section or opening paragraph | The `## Candidate plan` block, diagnosis line |
| Repro evidence to check against | The accepted repro comment posted on the issue thread | The `## Repro evidence` block (steps, artifact, control runs) |
| Control runs | The repro comment's control runs section | Same block. look for a "Control" or "Control runs" subsection |
| Thread diagnosis | Owner/maintainer comments naming a file, line, or mechanism associated with the issue | `## Thread highlights` block. Look for OWNER or CONTRIBUTOR labels naming a location |

## Scope

A bounded plan names exactly what changes and what does not. A plan that includes a redesign/refactor fails this check even when the fix is correct.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| In scope statement | The plan's scope section | Candidate plan's "Scope" line or "In scope" statement |
| Not in scope statement | The plan's scope section | "Not in scope" line. Absence of a not in scope line is just a signal, not an automatic fail |
| Approach list | Named files, areas, or mechanisms in the approach | The "Approach" numbered list in the candidate plan |
| Scope creep indicators | Phrases like "while we're here", "also migrate", "refactor the module", tasks unconnected to the diagnosed cause | Same. Count distinct concerns in the approach list against the single diagnosed cause |

## Executability

A executable plan lets a stranger start without asking the author anything. The test is not whether the plan is long or detailed, it is whether an executor has enough to begin.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Named files or areas | The approach section | Candidate plan's approach list. look for file paths, function names, or named subsystems |
| Chosen method | The approach describes a mechanism, not just an intention ("add a generation counter" vs. "investigate the input stack") | Same |
| Deferred decisions | Phrases like "not sure", "whichever is easier", "tbd at build time", "somewhere in the code" | Same |

## Test plan

The test plan must name an observable outcome tied to the repro evidence. Restating the goal ("should be fixed") or pointing at the full test suite without naming what the fix changes is a fail.

| Signal | On github.com | In the eval bundle |
|---|---|---|
| Observable outcome | The plan's test plan section | Candidate plan's "Test plan" line |
| Tie to repro steps | Does the test plan re-run or reference the repro evidence's trigger steps or artifact? | Compare the test plan to the `## Repro evidence` block's steps and expected/actual |
| Vague outcome indicators | "Should feel fast", "nothing else should break", "run the full test suite" with no named outcome for the fix | Same |

## Honesty

Honest plans name what they don't know. Plans that dress unknowns as certainty or omit flagged risks fail this check.

| Signal | On github.com  | In the eval bundle |
|---|---|---|
| Stated unknowns or risks | The plan body, often a "Risk" or "Open questions" line | Candidate plan. Look for explicit tradeoffs, flags for review, or noted unknowns |
| False certainty | The plan commits to outcomes it cannot yet verify (e.g., "this will fix it") without flagging the uncertainty | Same |
| Mid-build deviation | An updated plan.md recording what changed and why | N/A in eval mode; eval packages are point-in-time snapshots |

## Comms

The plan comment must engage the thread as it actually stands, not post as if the issue were still open and unexamined.

| Signal | On github.com  | In the eval bundle |
|---|---|---|
| Maintainer direction in thread | Owner/contributor comments naming a fix location, asking for a specific test, or stating a preference | `## Thread highlights`: look for OWNER or CONTRIBUTOR labels with explicit asks or culprit pointers |
| Comment engages thread | The candidate plan comment references or responds to maintainer signals | `## Candidate plan comment`. Check whether it acknowledges direction given in the thread highlights |
| AI-use disclosure requirement | CONTRIBUTING.md, AI_POLICY.md in the repo root | `## Repo facts` block, "contribution policy" line |
| Disclosure present | The comment names the ai tool and nature of use, or explicitly states no ai was used | `## Candidate plan comment`. Silence when disclosure is required is a fail |

