# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53


**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A csummary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Summary

All three issues come from the correct scoped repo (codepath/pathreview-ai301-fa26-s1), so all are valid candidates. Repo-level facts (shared across all three): 5 most recent commits land within the last few days (last: 2026-09-16), two issues were opened within the past month, 0 releases, 1 star — 2 of the 5 active-repo conditions are true (recent commit + recent issue), so active-repo passes. No CONTRIBUTING.md, AI_POLICY.md, AI_USAGE_POLICY.md, or AGENTS.md exists (all 404) — silence passes, so ai-allowed passes for all three. The README describes the project as an "AI-powered portfolio review assistant" using RAG — neat-subject passes (preferred) for all three, so it doesn't differentiate ranking.

Accepted, ranked:
1. #53 — PII scrubber fails to redact parenthesized US phone numbers. Most concretely scoped: exact repro code, exact failing test names, single regex fix in one file, unassigned, zero comments. Best fit for a first PR.
2. #69 — Output parser crashes on top-level JSON array fallback. Clear root cause, relevant files, 2–4h estimate, unassigned. A classmate (jacho15) posted "I'd like to attempt this" plus a full confirmed repro — per the Path Review house rule this doesn't block the issue, and their repro write-up is a head start, not a blocker.
3. #68 — Keyword search raises ZeroDivisionError when index is empty. Same quality of scoping (root cause, relevant files, 2–4h estimate), unassigned, zero comments — ties with #69 on structure but lacks the extra confirmation a classmate already provided on #69.

No issue was rejected — all three required checks pass for all candidates.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "active-repo", "grade": "pass", "evidence": "Most recent commit 2026-09-16 (within 3 months) and issue #73 opened 2026-09-16 (within past month) — 2 of 5 conditions true"},
      {"name": "good-first-issue", "grade": "pass", "evidence": "Body gives exact repro code, names failing tests (test_us_phone_number_redaction, etc.), single-file regex fix; labeled 'good first issue'"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], comments: 0"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s) — silence passes"},
      {"name": "neat-subject", "grade": "pass", "evidence": "README: 'AI-powered portfolio review assistant' using RAG"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
    "checks": [
      {"name": "active-repo", "grade": "pass", "evidence": "Most recent commit 2026-09-16 and issue #73 opened 2026-09-16 — 2 of 5 conditions true"},
      {"name": "good-first-issue", "grade": "pass", "evidence": "Root cause stated (.items() called on a list), relevant files named, 'Estimated effort: 2–4 hours', labeled 'good first issue'"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; classmate jacho15 (author_association: NONE) posted claim/repro comments 2026-09-19, but Path Review house rule says classmate claim comments don't block"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s) — silence passes"},
      {"name": "neat-subject", "grade": "pass", "evidence": "README: 'AI-powered portfolio review assistant' using RAG"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "active-repo", "grade": "pass", "evidence": "Most recent commit 2026-09-16 and issue #73 opened 2026-09-16 — 2 of 5 conditions true"},
      {"name": "good-first-issue", "grade": "pass", "evidence": "Root cause stated (BM25Okapi ZeroDivisionError on empty corpus), relevant files named, 'Estimated effort: 2–4 hours', labeled 'good first issue'"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], comments: 0"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (404s) — silence passes"},
      {"name": "neat-subject", "grade": "pass", "evidence": "README: 'AI-powered portfolio review assistant' using RAG"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

11, 15, 17, 18, 18, 20

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

Issue 1: 
My rubric accepted this issue.

Gold Label:
{"id": "issue-01", "source": "conda/conda#16475", "category": "clear-accept", "calibration": false, "verdict": "accept", "note": "docs task with a stated home and scope; active repo, unclaimed"},

Reasoning:
My rubric's active-repo check lists several ways to ensure that the repo is still active and requires that at least 2 of them are true. This repo passed due to the following reasons:
1. the repo has 100+ stars
2. the most recent push was just 1 day prior to capture date
3. the most recent release was within the past year
4. there have been 5 new issues opened on repo in past week

My rubric's good-first-issue check requires that the issue provide enough details for a new contributer. It requires that the issue provide enough details via either clear scope, repro steps, acceptance criteria, or a root cause. I also excluded issues that have multiple abandoned PRs attached to them.

This issue passed due to the very descriptive explanation of the problem, and a proposed solution. The clear scope makes it a clear pass.

My rubric's unclaimed check requires that no one be actively working on a solution and that the issue be unassigned. This issue meets both criteria.

My rubric's ai-allowed check requires that there is no policy or instructions on the repo that prohibit ai contributions. This repo's policy explicitly allows ai so it passes the criteria.

My neat-subject check sets a preference for repos related to math, statistics, data, science, engineering, ai, machine learning, or llms. The conda repo is package manager rather than an stem-related repo so it would have failed this check.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

| active-repo | time passed since the most 5 recent commits were merged. time passed since the most recent release. issues opened within the past month. maintainer first response to the 5 most recent opened issues | At least 2 of these items must be true to consider the repo active: there has been at least 1 active commit in the last 3 months, there has been at least 1 new issue opened in the past month, there has been a new release within the past 12 months, or the maintainer has an average response time to new issues of no more than 30 days, or repo has at least 100 stars. | required |

I had originally broken this check out into several different required checks but that proved to be too strict and caused issues that should have been accepted to be rejected instead. I ended up combining all of the active-repo related tests into 1 check but required that at least 2 of the items be true in order to pass. This gave the right level of flexibility for the repo to not be immediately rejected for overly strict activity criteria but also still ensured that it was active.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check could potentially omit a newer repo where there hasn't been a release yet and the maintainer is just actively adding issues. So although it could be otherwise a good repo, and would likely be active, it would fail this check because only the recent issues portion of the criteria would pass.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
- The issue appears to have clear steps to reproduce and a clear description so it seems like it would be a good fit given the time constraints. The repo is a RAG repo which passes my neat-subject preferred criteria as well.
2. What the verdict identified correctly, and what you weighed that the rubric could not.
- The rubric correctly identified that these were good first issues and that the the repository was active based on my criteria. There was also no ai policy so this check passed as well. Since issues 3 passed, I reviewed descriptions individually to see which had the most clear descritption. Issue #53 had the clearest repro steps and no one had commented that they were interested in working on it yet. These items contributed to my selection.
3. The anticipated difficulty in claiming it.
- Since the issue has clear repro steps and failing tests cases that can act as acceptance criteria, I think it should be relatively straightforward to implement a fix. I don't anticipate it being overly difficult.
]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
