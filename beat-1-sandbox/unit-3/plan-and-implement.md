# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

laolmstead

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5971291681

Plan for #53 at commit f89c06fc3ff292df2a04a39ac51319d32a76b779: `phone_us` in safety/pii_scrubber.py only allows `-` or `.` between groups, so any space separated number never matches. I'll change the three separators to `[-. ]?` and remove the xfail markers from the four named tests. I will leave test_mixed_pii_and_text as a separate failure (it appears to be related to the `street_address` pattern), and confirm the four tests pass once it's built.

---

## Your branch

**Branch**

fix/53-pii-scrubber-us-phone

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

Before the build change:

```
laolmstead@DESKTOP-43LRVQL:~/repos/pathreview-ai301-fa26-s1$  source /home/laolmstead/repos/pathreview-ai301-fa26-s1/.venv/bin/activate
(.venv) laolmstead@DESKTOP-43LRVQL:~/repos/pathreview-ai301-fa26-s1$ pytest tests/unit/test_pii_scrubber.py -rx
======================================================================= test session starts ========================================================================
platform linux -- Python 3.14.4, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /home/laolmstead/repos/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: benchmark-5.3.0, platformdirs-4.12.0, anyio-4.15.1, cov-7.1.0, asyncio-1.4.0, hypothesis-6.168.2, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 25 items                                                                                                                                                 
tests/unit/test_pii_scrubber.py ..xx.......x.....x....x..                                                                                                    [100%]

===================================================================== short test summary info ======================================================================
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_mixed_pii_and_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
================================================================== 20 passed, 5 xfailed in 0.48s ===================================================================
```

After the built change:
````
(.venv) laolmstead@DESKTOP-43LRVQL:~/repos/pathreview-ai301-fa26-s1$ pytest tests/unit/test_pii_scrubber.py -rx
=============================================================== test session starts ===============================================================
platform linux -- Python 3.14.4, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /home/laolmstead/repos/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: benchmark-5.3.0, platformdirs-4.12.0, anyio-4.15.1, cov-7.1.0, asyncio-1.4.0, hypothesis-6.168.2, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 25 items                                                                                                                                

tests/unit/test_pii_scrubber.py ......................x..                                                                                   [100%]

============================================================= short test summary info =============================================================
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_mixed_pii_and_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
========================================================== 24 passed, 1 xfailed in 0.52s ==========================================================
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

agreement: 20/20 scored items  (bar: 18/20: PASS)

**Package analysis**

```
pkg-03  clear-accept       accept  accept   yes
```

`pkg-03` is a `clear-accept` package and the run shows my verdict `accept` matched the gold label `accept` (`agree: yes`).

**Check rationale**

My `diagnosis` check:
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | the plan's diagnosis read against the evidence block's steps, artifacts, and control runs | The diagnosis the plan names is consistent with what the repro evidence shows. A diagnosis that contradicts a control run or ignores a step that rules it out is a fail. Unclear means the plan names no cause at all. | required |

I wanted to ensure that the diagnosis matched what the evidence block actually cited rather than something that just sounded possible. This is why the rule fails if the diagnosis contradicts or skips repro steps specified in the evidence block.

**Trade-offs**

This check can reject a plan that might be correct if it does not explicitly link its diagnosis back to the repro evidence. I accepted this because it lowers the likelihood of false accepts in cases with the wrong root cause.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
