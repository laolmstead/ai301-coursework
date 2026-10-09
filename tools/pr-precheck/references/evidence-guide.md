# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

Where it lives:
- **Eval bundle**: `## Plan context` (accepted plan scope, not-in-scope, deviations), `## Candidate PR` description claims, and `### Diff`.
- **Live mode**: local `plan.md` (including deviation notes), branch diff from `git diff <default-branch>...HEAD` (usually `git diff main...HEAD`), draft PR title/description in `pr_draft.md`, and the issue thread for explicit scope constraints.

What good looks like:
- Every material file/behavior in the diff is inside plan scope, or out of scope work is explicitly disclosed as a justified deviation tied to the same issue.
- Description fidelity claims match the diff (neither overstating nor hiding what changed).

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

Where it lives:
- **Eval bundle**: plan-context test plan, candidate PR `### Test evidence`, and repo-facts required checks from `## Repo facts`.
- **Live mode**: plan test plan in `plan.md`, captured local test output, and repository check expectations (PR template/contributing docs). Test output is saved in `test_evidence.md`.

What good looks like:
- Evidence shows an observable claim tied to the issue behavior (before/after or equivalently decisive proof), not only a generic "all green" statement.
- Repo-level checks requested by standards are reported (or an explicit, honest limitation is disclosed).

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

Where it lives:
- **Eval bundle**: candidate PR `### Commits` and `### Diff`.
- **Live mode**: branch commit list (`git log main...HEAD`) and full unified diff (`git diff <default-branch>...HEAD`, usually `git diff main...HEAD`).

What good looks like:
- The fixing intent is visible and reviewable without making unrelated changes.
- Unrelated changes are absent or minor enough not to obscure the fix. Substantial drive-by changes make the package unreviewable.
- Working files used for live review (`plan.md`, `pr_draft.md`, `test_evidence.md`) are excluded from the implementation diff unless the target repo explicitly requires them.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

Where it lives:
- **Eval bundle**: `## Repo facts` (template asks, contribution policy, disclosure asks), `## Thread highlights`, and candidate PR title/ description.
- **Live mode**: repo PR template, CONTRIBUTING/policy docs, issue/PR thread highlights, and draft PR title/description.

What good looks like:
- Required template asks and policy disclosures are present with concrete content.
- Explicit maintainer direction in the thread is engaged in the PR text.
- Boilerplate that ignores required asks or thread instructions is a failure.
