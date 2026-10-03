# Plan: issue #53, PII scrubber does not redact parenthesized US phone numbers

Repo: `codepath/pathreview-ai301-fa26-s1`, commit `f89c06fc3ff292df2a04a39ac51319d32a76b779` (main). My posted repro report lists `996fabe` by mistake. The repro was run on this commit. Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

## Diagnosis

`PIIScrubber.PII_PATTERNS["phone_us"]` in `safety/pii_scrubber.py` (line 16) only allows `-` or `.` between the phone number's groups (`[-.]?`). It doesn't include the space character, so any number with a space between groups never matches. `(555) 123-4567` fails because of the space after `)`.

My repro report on the issue shows the four named tests XFAIL and `scrub('Call me at (555) 123-4567 or 555-123-4567')` redacting only the dashed number. Separately from that report, I checked the pattern directly against the test formats below and the issue is the space, not the parentheses:

- `(555)123-4567` matches, which rules out the parentheses.
- `555 123 4567` and `+1 555 123 4567` do not match so the gap is the space separated number groups, not only the parenthesized one.
- `555-123-4567` and `555.123.4567` also match as the issue says.

## Scope

In scope: one regex change in `PII_PATTERNS["phone_us"]`, plus removing the `xfail` markers from the tests that this fix makes pass.

Not in scope: the `test_mixed_pii_and_text` is also failing in TestPIIScrubber but the phone number is correctly redacted in this test so this appears to be a separate issue. I stepped through the function in debug and this failure appears to be caused by the `street_address` regex pattern. Because this is a separate issue from the `phone_us` fix, it is out of scope for this change.

## Approach

1. In `safety/pii_scrubber.py`, change the three `[-.]?` separators in `phone_us` (country code, after the area code, after the exchange) to `[-. ]?`, to include a space. Only `phone_us` changes; `phone_intl` has a similar separator and is left alone. Only the separators change in this step.
2. Replace the leading `\b` with `(?<!\w)` so the match can begin at the opening `(` (`\b` cannot match between a space and `(`, which left a stray `(` in the output). Result: `(?<!\w)(?:\+?1[-. ]?)?\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})\b`.
3. In `tests/unit/test_pii_scrubber.py`, delete the `@pytest.mark.xfail(strict=True, ...)` decorator from `test_us_phone_number_redaction`, `test_us_phone_formats`, `test_detect_phone_pii`, and `test_phone_at_start_of_text` as required per CONTRIBUTING.md.

## Test plan

- Before the fix running TestPIIScrubber from the VS Code Testing Extention reports 20 passed, 5 xfailed.
- After the fix, the four tests `test_us_phone_number_redaction`, `test_us_phone_formats`, `test_detect_phone_pii`, and `test_phone_at_start_of_text` pass with their xfailed markers removed, 24 passed, 1 xfailed (`test_mixed_pii_and_text`).
- The issue snippet now redacts all of `(555) 123-4567` including the opening parenthesis (`Call me at [REDACTED] or [REDACTED]`), and `detect('Call me at (555) 123-4567')` returns one `phone_us` item with value `(555) 123-4567`.

## Deviations

One change to the approach. My plan only widened the separators to `[-. ]?`. When I ran the issue snippet after that change, the digits were redacted but the opening `(` stayed in the output (`Call me at ([REDACTED]`), and `detect()` returned `555) 123-4567` instead of the full number. The leading `\b` cannot match between a space and `(`, so the match started at the digits. I replaced `\b` with `(?<!\w)` (a step I added as step 2), which keeps the same guard against matching mid-word (`x5551234567` is still not matched) but lets the match start at `(`. I also tightened the test plan to check the full number is redacted, not just the digits.

Status: all three steps are applied. The marker removal in step 3 was first blocked by the tool permission check and went through once I explicitly approved it. Final result: 24 passed, 1 xfailed (`test_mixed_pii_and_text`).
