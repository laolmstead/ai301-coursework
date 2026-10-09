---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

You are grading one PR package to answer a single question: is this PR ready to submit? A PR package is the candidate pull request title, description, commit set, diff, and test evidence, read against (1) the plan it claims to implement (including the deviation notes) and (2) the issue that plan belongs to. Do not grade anything else (not team process, not style preferences outside stated repo standards, not future work ideas). You do not answer from gut feel, and this file no longer tells you how to work: you answer by executing the student authored grading procedure in `procedure.md`, which applies the rubric in `rubric.md` to evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

One of two modes:

- **Live mode**: pre-submit check of a real student branch
  - Read `plan.md` associated with this issue from unit 3 (including any deviation notes).
  - Read the branch diff relative to default branch from the working copy (`git diff <default-branch>...HEAD`, usually `git diff main...HEAD`).
  - Read the draft PR title and description in `pr_draft.md`: first line title, remaining lines description.
  - Read provided test evidence/output in `test_evidence.md`.
  - Read the issue the plan targets, plus required repo side standards evidence sources listed in `references/evidence-guide.md`.
  - If the student is on a house chain, read the house plan and house repro pack in place of a personal repro thread and grade with the same checks.
  - Treat `plan.md`, `pr_draft.md`, and `test_evidence.md` as working notes that should not be part of the implementation diff unless the target repo explicitly requires them.

- **Eval mode**: a package bundle (a markdown file containing the repo facts, issue, thread highlights, and plan context, along with the candidate PR and test evidence), such as files in `/eval/packages`:
  - The bundle text is the entire world. Do not fetch GitHub, do not read local branch state, do not infer from anything outside bundle text.
  - Grade every check and apply the full verdict rule.
  - Do not consult `golden-labels.json` while grading. That file is the answer key for evaluation, not grading evidence.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read `scope.md` in this skill directory before anything
else. It names where the student's issue must live and the house rules
that apply there; a house rule changes how evidence is read in that
environment. Refuse to grade a package for an issue outside the scoped
source. If the scope's repo line still carries an unfilled placeholder,
stop without grading and tell the student to get their cohort's scope
file from the instructor; never guess a scope. In eval mode, ignore
`scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, also read `voice-guide.md`: the student's own rules for how they write upstream, with wrong/right examples. Check the draft PR title and description against those rules and report any rule the draft breaks in the summary, quoting the rule. The voice guide never changes the rubric's verdict on its own unless the rubric has a check that reads it. In eval mode, ignore `voice-guide.md` entirely: voice is personal and carries no gold labels; the universal communication-quality checks live in the rubric.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read and execute components as a strict chain:

1. Read `rubric.md` to get checks, weights, and verdict rule. The rubric contains a table of checks. Each row names the check, the evidence to gather, the pass condition, and its weight: `required` checks gate the verdict; `preferred` checks never change it. It also contains a verdict rule: how check results combine into a final verdict.
2. Read `references/evidence-guide.md` to locate each evidence family. The evidence guide is the rubric's map: where each kind of evidence lives in a package (and in live mode), and what good looks like there.
3. Execute `procedure.md` exactly as written to gather evidence, run checks, and assemble the verdict. The procedure decides the read order, how each evidence family gets gathered, how a check executes against gathered evidence, and how check grades become the verdict. Follow it as written, the same way an executor follows a rubric: exactly, without improvising around gaps. 

If `procedure.md` is silent on a needed step, do not improvise. Note the
gap in the summary and continue only where the written procedure still
supports deterministic grading.

If `rubric.md` has no checks filled in, or `procedure.md` has no steps
filled in, stop and say so: this skill cannot grade without a rubric
AND a procedure, and that is by design.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

Verdict is binary:

- `accept` = ready to submit.
- `reject` = hold.

You may provide a short human-readable summary before the JSON. End with
the fenced JSON block below, valid and last, with nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

Apply these rules on every run:

- Evidence first: every check grade must cite the deciding fact or quote.
- Grade the artifact, not polish: evaluate plan/diff/evidence (or package draft PR) against the issue, not writing flair or formatting aesthetics.
- Rubric authority: if a check meets the rubric pass condition, it passes even if you personally dislike it. Note your tensions in the summary if you want but the fix belongs in the rubric, not in the run.
- Procedure authority: follow `procedure.md` as written and report gaps instead of inventing hidden steps.
- Treat `unclear` as the rubric's verdict rule directs. If the rule
  does not say, treat `unclear` as `fail`.
