# Contribution: viz/interactive.py: dedup repeated status Div, log-transform closure, and 3D mesh cache key (+ first unit tests)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Lindsey Olmstead
**GitHub Username:** laolmstead
**Issue:** https://github.com/MFlowCode/MFC/issues/1518
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built an issue scout that searches GitHub for first contribution issues**

I built my scout to pull a list of 100 bugs that were tagged with both "good first issue" and "help wanted". Additionally, I limited my search to open, unassigned issues, with python listed as the language. In my ranking filters, I de-prioritized issues that were documentation only and added a preference for fewer comments to try to filter out issues complex issues that have been debated.

When I first ran my scout, it only returned issues from 1 repository because there was one particularly spammy repository where 100s of translation tickets were being created at once. To fix this I updated my query to add a jq filter which limited the search to one issue per repository.

**Unit 6: Installed the voice guard and wrote a memory file for MFC**

I added an Upstream section to my voice guide and installed the voice-guard hook. My first install didn't work because I pasted the hook into `~/.claude.json` instead of `~/.claude/settings.json`, so it never fired. I only caught that when I checked the guard log, which had no hook entries. After moving it, the wiring test blocked `gh issue comment --help`, and my claim draft passed the guard's check. 

For MFC, I wrote a short `CLAUDE.local.md` with the contributing rules, the parts of `interactive.py` and `test_viz.py` my issue touches, and the test commands. I kept it out of my PR with `.git/info/exclude`, and I dropped the `@AGENTS.md` import since a CLAUDE.md file exists for the repo.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

[1-2 paragraphs in your own words: how you searched, what your scan
surfaced, what your scout's verdict said, why this issue fits your
profile, and what you hope to learn. If your scout's verdict on it
was reject and you chose it anyway, say so here and say why; choosing
against your own tool silently is what loses points. Close with an
honest read of the tool itself: where the scout fell short on a real
wild search and what you changed or would change, or what convinced
you it held up. **Record the link to your claim comment in this section too.**
Not claimed yet? Write `claim pending` and today's date where the link goes,
and add the link the moment your claim lands.]

I searched by reviewing the issues and repositories on https://open-source-issue-tracker.onrender.com/ and picking a few that interested me. Several already had open PRs or comments saying someone had started on them, so the search took quite some time. I then expanded beyond bugs to include enhancements, and that's when I found the MFC repo and my issue. I ran my scout a few times and it always ranked this issue at the top. Its verdict was accept, with a difficulty note of straightforward: the issue names the files, line numbers, and three pure-function extractions plus the unit tests to add, and it has no assignee and no comments. The scout did fail the neat-subject check, because the repo description ("Exascale multiphase flow solver") contained none of my keywords at the time. That check is only preferred, not required, so it did not block the accept, and I chose the issue anyway because MFC is a fluid dynamics simulator, which fits my earlier background in Civil/Environmental Engineering.

The issue is also a fairly straightforward refactor that I can finish in the allotted time given my work schedule. I hope to learn more about this repository so I can keep contributing to it and to other open source Civil/Environmental Engineering repos. I would love to become part of this niche contributor community. I also read MFC's contributing guide (https://mflowcode.github.io/documentation/contributing.html). It says nothing about AI, so nothing prohibits AI-assisted contributions, and the repo's `AGENTS.md` and `.github/copilot-instructions.md` tell AI coding agents how to work in it, which suggests AI tools are expected.

My scout did a good job of weeding out issues that were already taken, even when the PR was linked from another issue, but it fell short in two places. It initially rejected an issue where a commenter had posted repro steps and the fix that worked for her, even though she never opened a PR or claimed the issue; she was only explaining the fix as part of her repro. I fixed this by giving claims and reporter fixes a 90-day expiration. The neat-subject check also failed MFC even though fluid dynamics modeling is part of civil engineering, so I added physics, simulation, solver, and fluid to the keyword list. A word list is still a blunt tool for judging a subject, and I plan to keep refining the scout during and after this class.

https://github.com/MFlowCode/MFC/issues/1518#issuecomment-6406052284

**Toolkit**

- Tool: issue-scout. I picked my top candidates from the class's issue list (open-source-issue-tracker.onrender.com) and graded them against my rubric by URL.
- What it produced: It accepted MFC #1518 with a "straightforward" difficulty note. It failed neat-subject (a preferred check) because "Exascale multiphase flow solver" had none of my keywords. It rejected the other picks I graded (MFC #2086, for the reporter's own fix) and accepted TaskChampion #410 below #1518. I gave up the rest of my picks.
- Difficulties: The scope check rejected most real issues, and my claimed check rejected issues with years-old "I'll work on this" comments. My neat-subject word list also missed a fluid solver. #1518 is an enhancement, not a bug, so I judged that fit myself.
- What changed: I replaced my good-first-issue check with the scope-feasible check and added the difficulty note, then dated the change in scan-notes.md. I also gave claim comments a 90-day expiration and added physics, simulation, solver, and fluid to neat-subject.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
