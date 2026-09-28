# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

laolmstead

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5848386724

Hello! I would like to claim this issue. Please note, this is my first time contributing to this repo. Looking at the repro steps, I'm thinking the PIIScrubber() regex may have missed escaping the '()' characters or may not be accounting for the space after area code. I will review the issue in more detail and post back shortly with my findings and a repro report if I'm able to reproduce the issue.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5861863613

Repro report:

Environment: Forked codepath/pathreview-ai301-fa26-s1 to laolmstead/pathreview-ai301-fa26-s1. Commit 996fabe53f348eca80467c22cdcd23a47d57aed6, Python 3.14.4, Ubuntu 26.04.1 for WSL 2.

```
$ gh repo clone laolmstead/pathreview-ai301-fa26-s1
$ cd pathreview-ai301-fa26-s1
$ cp .env.example .env
$ docker compose up -d
$ make setup
```

- Opened pathreview-ai301-fa26-s1 folder Visual Studio Code
- Selected .venv (3.14.4) ./.venv/bin/python as the Python Interpreter

Running the unit tests in test_pii_scrubber.py from the Visual Studio Code terminal in the projects python .venv produces the failed tests described below, which matches what is described in the issue.

```
pytest tests/unit/test_pii_scrubber.py -rx
============ test session starts ============
platform linux -- Python 3.14.4, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /home/laolmstead/repos/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: benchmark-5.3.0, platformdirs-4.12.0, anyio-4.15.1, cov-7.1.0, asyncio-1.4.0, hypothesis-6.168.2, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 25 items                          

tests/unit/test_pii_scrubber.py ..xx. [ 20%]
......x.....x....x..                  [100%]

========== short test summary info ==========
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_mixed_pii_and_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
======= 20 passed, 5 xfailed in 0.38s =======
```

Also, I tried reproducing the issue directly in the repo's python .venv as described in the repro instructions and observed the same issue described in the issue.

```
(.venv) laolmstead@DESKTOP-43LRVQL:~/repos/pathreview-ai301-fa26-s1$ python
Python 3.14.4 (main, Aug 20 2026, 10:41:58) [GCC 15.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
Ctrl click to launch VS Code Native REPL
>>> from safety.pii_scrubber import PIIScrubber
>>> s = PIIScrubber()
>>> print(s.scrub('Call me at (555) 123-4567 or 555-123-4567'))
Call me at (555) 123-4567 or [REDACTED]
>>> print(s.detect('Call me at (555) 123-4567'))
2026-09-27 20:39:04 [info     ] pii_detected                   count=0 types=0
[]
```

Expected: All tests in test_pii_scrubber.py pass.

Actual: The following tests in test_pii_scrubber.py fail:  test_us_phone_number_redaction, test_us_phone_formats, test_detect_phone_pii, test_phone_at_start_of_text, test_mixed_pii_and_text.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19
20

**Package analysis**

pkg-20. My rubric: reject. Gold label: reject. The repro description meets the criteria (correct version, clear steps, terminal output matching the issue exactly) but the ghostty repo-facts block says all AI usage must be disclosed, and the claim comment says nothing about AI use. My `comms` check requires disclosure when the repo's policy requires it, so silence is a fail. That single required-check failure results in a reject.

**Check rationale**

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| comms | the claim comment text for specificity and honest intent. the repo-facts block's contribution policy for any AI-use disclosure requirement. | the claim comment names what was found and what comes next, tied to this issue. if the repo's stated policy requires AI-use disclosure, the comment either discloses the tool and how it was used, or explicitly states no AI was used. silence on AI use when disclosure is required is a fail. a boilerplate comment that is interchangeable across issues or promises a guaranteed timeline fails regardless of the repro issue. | required |

I originally didn't have the AI disclosure check, I just checked whether the claim was specific to the issue and explains what comes next. This caused Test 20 to fail on my first run (pkg-20 got accepted, but should be rejected). I saw in the test run that the Disclosure criteria was what failed so I added a rule requiring AI disclosure when a policy specifies. Once I made this change, all test cases passed.

**Trade-offs**

With respect to this portion of the `comms` check:
"a boilerplate comment that is interchangeable across issues... regardless of the repro issue."

There may be a known bug that maybe a package version upgrade could resolve. In this case, a boilerplate comment may be suffient but would fail in this case.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
