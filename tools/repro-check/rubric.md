# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env | the repro report's environment line (version, OS, architecture) compared to the version the issue targets using the repo's Releases section | Tool version and OS are specified. If the reporter's version differs from the issue's stated target, the difference is called out explicitly. Fail if either is absent. | required |
| repo-steps | the repro report's steps section compared to the README and the issue's stated trigger. the repo-facts block for whether the repo is public and accessible. | A stranger can follow the steps from nothing to trigger without guessing: starting state is explicit, trigger commands are quoted, and no step requires a private repo or unshared config. | required |
| behavior-matches | the quoted artifact (output excerpt, log, error text) in the repro report compared to the behavior the issue describes. | The artifact is present and shows the specific behavior the issue names (same error code, same symptom, same failure mode). Confirmation of repro without a matching artifact is a fail. an honest 'cannot reproduce' that shows the attempt and names what is different is a pass. | required |
| comms | the claim comment text for specificity and honest intent. the repo-facts block's contribution policy for any AI-use disclosure requirement. | the claim comment names what was found and what comes next, tied to this issue. if the repo's stated policy requires AI-use disclosure, the comment either discloses the tool and how it was used, or explicitly states no AI was used. silence on AI use when disclosure is required is a fail. a boilerplate comment that is interchangeable across issues or promises a guaranteed timeline fails regardless of the repro issue. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if all required checks pass. If any required check fails or is unclear, reject. Preferred checks never change the verdict but are to be used to rank comments.
