# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| active-repo | time passed since the most 5 recent commits were merged. time passed since the most recent release. issues opened within the past month. maintainer first response to the 5 most recent opened issues | At least 2 of these items must be true to consider the repo active: there has been at least 1 active commit in the last 3 months, there has been at least 1 new issue opened in the past month, there has been a new release within the past 12 months, or the maintainer has an average response time to new issues of no more than 30 days, or repo has at least 100 stars. | required |
| good-first-issue | description, repro steps, acceptance criteria, root cause. optionally, tag specifying it's a good first issue. | Clear description of the issue scope, steps to reproduce, potential root causes, or acceptance criteria. Or issue is a very small, simple fix. Or it's an obvious/noticable bug. Codebase wide issues are only acceptible if one of the previous criteria pass. If multiple people have started and abandoned PRs fail. | required |
| unclaimed | whether the issue is currently assigned | issue is unassigned and no one is working on a solution | required |
| ai-allowed | whether the repository allows contributions from ai users/sources | there is no policy or instructions on the repo prohibitting contributions by ai and users of ai | required |
| neat-subject | repo description | the repo's description mentions one of the following subjects: math, statistics, data, science, engineering, ai, machine learning, llm | preferred |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required checks pass. If any required check fails or is unclear, the verdict is Reject. A preferred check never changes
the verdict but use the prefered checks to rank the issues. If all required checks pass, Accept the issue
