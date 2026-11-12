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
**Pull Request:** https://github.com/MFlowCode/MFC/pull/2170

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

I built my scout to pull 100 open, unassigned Python bugs tagged with both "good first issue" and "help wanted". In my ranking filters, I de-prioritized issues that were documentation only and added a preference for fewer comments to try to filter out complex issues that have been debated.

When I first ran my scout, it only returned issues from 1 repository because there was one particularly spammy repository where 100s of translation tickets were being created at once. To fix this I updated my query to add a jq filter which limited the search to one issue per repository.

**Unit 6: Installed the voice guard and wrote a memory file for MFC**

I added an Upstream section to my voice guide and installed the voice-guard hook, but my first install never fired because I accidentally pasted the hook into `~/.claude.json` instead of `~/.claude/settings.json`, which I only caught when the guard log had no hook entries. After moving it, the wiring test blocked `gh issue comment --help`, and my claim draft passed the guard's check. 

For MFC, I wrote a short `CLAUDE.local.md` with the contributing rules, the parts of `interactive.py` and `test_viz.py` my issue touches, and the test commands. I kept it out of my PR with `.git/info/exclude`, and I dropped the `@AGENTS.md` import since a CLAUDE.md file exists for the repo.

**Unit 7: Installed the ship-gate and wrote its manifest for MFC**

I wrote the ship gate's manifest using MFC's contributing guide. The Lint Gate lists six checks that `./mfc.sh precheck` bundles, and I ran the commands in a shell before trusting it. `./mfc.sh lint` failed on `test_format_tar_zst` because `zstd` was not installed. After I installed `zstd`, the precheck passed. I also added rows for `test_viz.py` to run my new tests and `./mfc.sh test -j 12` to run the regression tests, but later moved the regression suite to the excluded table. On my branch it took 88 minutes to run, and two slow phase-change tests timed out under load even though both passed when run alone. I ensured that they passed locally outside of the ship gate but since the ship gate had to be run multiple time, it didn't make sense to keep re-running the ship-gate again and again.

My first gate run on the branch blocked because my pr-precheck failed. I had been editing the PR description and inadvertently left a partial sentence in its Verification section. It passed once I fixed that, but it did not catch the CI-only `turbojpeg` failure that followed. It passed on my machine, because the library was installed. I reviewed the issue and created a new commit which resolved the failures. I added a comment explaining the issue and noted that if the Maintainer would prefer a different fix, I would be happy to make a change.

**Unit 8: Installed the PR monitor and wrote my playbook for MFC**

I installed the PR monitor and wrote my playbook from MFC's data. I checked six recent merged outside contributor PRs (#2114, #2092, #2087, #2085, #2055, #2038), in which a maintainer's first response took 0.2 to 4.8 days. and set the first-review threshold at 7 quiet days with one nudge only, tagging no one if nobody has engaged. The monitor's first `--state` run read PR #2170 as "feedback-in", but the only new comments were bots (the review bot's failed run and Codecov), which I confirmed with `gh`. Once the playbook was filled in, a full run drafted "Wait, no nudge yet" through the polite-nudge form: the PR is a day old, 27 checks are still pending, and my rule says the threshold is met after 7 days. I followed the instructions and posted nothing. I also tightened my playbook so the stalled review clock is counted the way the monitor counts it (days since anyone but me commented, with bots not restarting it), because the draft had to guess which date my clock started.

---

## Why I Chose This Issue

I searched by reviewing the issues and repositories on https://open-source-issue-tracker.onrender.com/ and picked a few that interested me. Several already had open PRs or comments saying someone had started on them, so the search took quite some time. I then expanded beyond bugs to include enhancements, and that's when I found the MFC repo and my issue. The repo was related to an interesting engineering subject like I was hoping to find and the issue seemed like it would be achievable in the timeframe.
Also, this issue was graded the top choice in all of my scout runs, with a difficulty of straightforward. I hope to learn more about this repository so I can keep contributing to it and to other open source Civil/Environmental Engineering repos. I would love to become part of this niche contributor community. I also read MFC's contributing guide (https://mflowcode.github.io/documentation/contributing.html). It says nothing about AI, so nothing prohibits AI-assisted contributions, and the repo's `AGENTS.md` and `.github/copilot-instructions.md` tell AI coding agents how to work in it, which suggests AI tools are expected.

My scout did a good job of weeding out issues that were already taken, even when the PR was linked from another issue, but it fell short in two places. It initially rejected an issue where a commenter had posted repro steps and the fix that worked for her, even though she never opened a PR or claimed the issue, she was only explaining the fix as part of her repro. I fixed this by giving claims and reporter fixes a 90-day expiration. The neat-subject check also failed MFC even though fluid dynamics modeling is part of civil engineering, so I added physics, simulation, solver, and fluid to the keyword list. A word list is still a blunt tool for judging a subject, and I plan to keep refining the scout during and after this class.

https://github.com/MFlowCode/MFC/issues/1518#issuecomment-6406052284

**Toolkit**

- Tool: issue-scout. I picked my top candidates from the class's issue list (open-source-issue-tracker.onrender.com) and graded them against my rubric by URL.
- What it produced: It accepted MFC #1518 with a "straightforward" difficulty note. It failed neat-subject (a preferred check) because "Exascale multiphase flow solver" had none of my keywords. It rejected the other picks I graded (MFC #2086, for the reporter's own fix) and accepted TaskChampion #410 below #1518. I unclaimed my other picks once I decided on MFC #1518.
- Difficulties: The scope check rejected most real issues, and my claimed check rejected issues with years old "I'll work on this" comments. My neat-subject word list also missed a fluid solver. #1518 is an enhancement, not a bug, so I reached evaluated it myself and consulted with the CodePath staff to determine if the issue would work.
- What changed: I replaced my good-first-issue check with the scope-feasible check and added the difficulty note then I dated the change in scan-notes.md. I also gave claim comments a 90-day expiration and added physics, simulation, solver, and fluid to neat-subject.

---

## Understanding the Issue

**Problem Description**

Three different pieces of logic are repeated in multiple places in the codebase. The duplicate logic presents a risk that if a change is made in one place, it could be missed or copied wrong in another which could lead to unintended bugs.

The goal of this issue is to de-duplicate this logic and add unit tests to verify the existing behavior.

**Expected Behavior**

1. One function `_status_div(step, shape, dmin, dmax) -> html.Div` exists for the function shape `html.Div (step {step} / · shape {raw.shape} / Br / min+value / max+value, same _YELLOW/_MUTED/_BLUE/_RED styles)` and it is called on lines 1971, 2120, 2470, 2626.
2. `_log_transform(log: bool)` exists instead of the duplicate `_tf(arr)` logic returning the transform and the `cmin`/`cmax` pair. The 1e-300 floor is moved to a module constant `_LOG_FLOOR`
3. A new NamedTuple `_Mesh3Key` exists instead of the duplicate `key = (step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` tuple creations.
4. Unit tests have been added to `test_viz.py` for `interactive.py` which verify the behavior changed in items 1-3.

**Current Behavior**

1. `html.Div (step {step} / · shape {raw.shape} / Br / min+value / max+value, same _YELLOW/_MUTED/_BLUE/_RED styles)` is duplicated on lines 1971, 2120, 2470, 2626.
2. `_tf(arr)` is repeated on lines 379, 386, 1853, and 1861 in one of the formats below:
```
def _tf(arr):
    return np.where(arr > 0, np.log10(np.maximum(arr, 1e-300)), np.nan)
# else
def _tf(arr):
    return arr
```
The literal `1e-300` is hardcoded rather than stored as a constant.
3. The logic `(step, var, mode, log, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` is duplicated at lines 350, 432, and 1890.
4. No unit tests exist for `interactive.py`.

**Affected Components**

The python toolchain file `toolchain/mfc/viz/interactive.py` which is one of the frontend UI modes used by viz.py to visualize models.

**Toolkit**

- Tool: plan-check. Its diagnosis check reads my plan's account of the issue against the issue text and the code on master, so it was the tool that tested whether I understood the issue correctly and had a valid plan.
- What it produced: It validated my analysis of the existing behavior against the behavior described in the issue and confirmed that my plan would resolve the issue. 
- Difficulties: It accepted my first reading of the issue's third key site, where I only replaced the two tuples, so it did not catch that "use it at all three sites" meant the six `_update` calls too. I found that by rereading the issue myself. It also has no rule for refactor issues with no repro comment, so it checked my understanding against the issue body only.
- What changed: I rewrote my plan to use the key at all three sites, and kept the issue's wording differences (7 children, the `_Mesh3Key` name) stated openly in my plan and plan comment instead of quietly matching the issue.

---

## Reproduction Process

**Environment Setup**

Ran on master @ e95a827a334601f7d03162ff3f3a1cae6bf484a1 (`toolchain/mfc/viz/interactive.py`). Environment: WSL2 Ubuntu 26.04 (x86_64), Python 3.14.4, gfortran 15.2.0, Open MPI 5.0.10 (mpif90), cmake 4.2.3, make 4.4.1, gcc/g++ 15.2.0. The issue was filed against `40dde5e`; the line numbers it cites are unchanged at `e95a827`. All three duplications described in the issue are present, and I found no tests for `interactive.py`.

Setup (no build needed; this is a refactor issue, and `./mfc.sh` creates the Python venv in `build/venv` on first use). Two packages in the `apt` line are not in MFC's setup docs but are needed for `./mfc.sh lint` and the new tests to pass: `zstd`, which `test_format_tar_zst` shells out to (without it that test fails with `zstd: not found`), and `libturbojpeg0`, which `interactive.py` needs to import:
```
git clone https://github.com/MFlowCode/MFC && cd MFC
git checkout e95a827a334601f7d03162ff3f3a1cae6bf484a1
sudo apt install tar wget make cmake gcc g++ gfortran libopenmpi-dev openmpi-bin zstd libturbojpeg0
```

Then run the greps below from the repo root, followed by `./mfc.sh lint` and the pytest run it reports.

**Steps to Reproduce**

This is a refactor issue, so "reproducing" means confirming the duplication exists and that no tests cover it. On `e95a827` (setup above), from the repo root:

1. Run `grep -n -B3 -A6 'shape {raw.shape}' toolchain/mfc/viz/interactive.py`. Observed: the same `step / shape / Br / min / max` `html.Div` block at lines 1971, 2120, 2470, and 2626, differing only in the min/max local names.
2. Run `grep -n "def _tf\|1e-300" toolchain/mfc/viz/interactive.py`. Observed: `_tf(arr)` is defined at lines 379, 386, 1853, and 1861 (the log and identity variants), and the `1e-300` literal appears inline instead of as a constant.
3. Run `grep -n 'key = (step, var, mode' toolchain/mfc/viz/interactive.py`. Observed: the 11-element cache key tuple at lines 350 and 432. Then run `grep -n '_get_cached_3d_mesh\|_prefetch_3d_mesh' toolchain/mfc/viz/interactive.py` to see the callers, including line 1890.
4. Run `grep -n interactive toolchain/mfc/viz/test_viz.py`. Observed: no matches, so `interactive.py` has no unit tests.

**Reproduction Evidence**

- **Commit showing reproduction:** None of my own. This is a refactor issue, so the reproduction was grep-only and no code changed; there are no failing tests to commit because the issue is the missing tests. It was run against the base commit https://github.com/laolmstead/MFC/commit/e95a827a334601f7d03162ff3f3a1cae6bf484a1
- **Screenshots/logs:** The grep output and the `./mfc.sh lint` / pytest run are pasted below.
- **My findings:** All three duplications in the issue reproduce on `e95a827`, and `interactive.py` has no tests. Two details differ slightly from the issue's wording. (a) The `_tf` duplication is at lines 379/386 and 1853/1861, and the same `1e-300` floor is also inlined at lines 302-304, 382-383, and 1856-1857, so `_LOG_FLOOR` should replace those too. (b) The literal `key = (step, var, mode, ...)` tuple only appears at lines 350 and 432. Line 1890 is a `_get_cached_3d_mesh(...)` call that passes the same arguments, not a key tuple, and the same call is made at 2025, 2075, and 2142, so the issue's "use it at all three sites" needed a decision, which I settled in my plan. What I built is not a `_mesh3_key(...)` function but the issue's "small namedtuple" option: a module-level `_Mesh3Key` `NamedTuple` with the 11 fields (`interactive.py` L339 on my branch). `_update` builds it once as `mesh_key` and passes it to the four `_get_cached_3d_mesh` lookups, and `mesh_key._replace(step=_ns)` to the two `_prefetch_3d_mesh` calls. `_prefetch_3d_mesh(key, get_ad_fn)` and `_get_cached_3d_mesh(key)` now take the key instead of 11 separate arguments, so the two hand-built tuples at L350 and L432 no longer exist. On the baseline run lint passed ruff and 801 of 802 toolchain tests passed. The one failure (`test_format_tar_zst`) was only missing the `zstd` package, not a code problem. After `sudo apt install zstd`, `./mfc.sh lint` passes with 0 failures (856 passed on my branch on 2026-11-07, including my new tests).

1. `html.Div (step {step} / · shape {raw.shape} / Br / min+value / max+value, same _YELLOW/_MUTED/_BLUE/_RED styles)` is duplicated on lines 1971, 2120, 2470, 2626. Only the min/max local names differ.
```
laolmstead@LAOLMSTEAD:~/repos/MFC$ grep -n -B3 -A6 'shape {raw.shape}' toolchain/mfc/viz/interactive.py
1971-                status_k = html.Div(
1972-                    [
1973-                        html.Span(f"step {step}", style={"color": _YELLOW}),
1974:                        html.Span(f"  ·  shape {raw.shape}", style={"color": _MUTED}),
1975-                        html.Br(),
1976-                        html.Span("min ", style={"color": _MUTED}),
1977-                        html.Span(f"{dmin_k:.4g}", style={"color": _BLUE}),
1978-                        html.Span("  max ", style={"color": _MUTED}),
1979-                        html.Span(f"{dmax_k:.4g}", style={"color": _RED}),
1980-                    ]
--
2120-                status = html.Div(
2121-                    [
2122-                        html.Span(f"step {step}", style={"color": _YELLOW}),
2123:                        html.Span(f"  ·  shape {raw.shape}", style={"color": _MUTED}),
2124-                        html.Br(),
2125-                        html.Span("min ", style={"color": _MUTED}),
2126-                        html.Span(f"{dmin3:.4g}", style={"color": _BLUE}),
2127-                        html.Span("  max ", style={"color": _MUTED}),
2128-                        html.Span(f"{dmax3:.4g}", style={"color": _RED}),
2129-                    ]
--
2470-                status = html.Div(
2471-                    [
2472-                        html.Span(f"step {step}", style={"color": _YELLOW}),
2473:                        html.Span(f"  ·  shape {raw.shape}", style={"color": _MUTED}),
2474-                        html.Br(),
2475-                        html.Span("min ", style={"color": _MUTED}),
2476-                        html.Span(f"{dmin:.4g}", style={"color": _BLUE}),
2477-                        html.Span("  max ", style={"color": _MUTED}),
2478-                        html.Span(f"{dmax:.4g}", style={"color": _RED}),
2479-                    ]
--
2626-        status = html.Div(
2627-            [
2628-                html.Span(f"step {step}", style={"color": _YELLOW}),
2629:                html.Span(f"  ·  shape {raw.shape}", style={"color": _MUTED}),
2630-                html.Br(),
2631-                html.Span("min ", style={"color": _MUTED}),
2632-                html.Span(f"{dmin:.4g}", style={"color": _BLUE}),
2633-                html.Span("  max ", style={"color": _MUTED}),
2634-                html.Span(f"{dmax:.4g}", style={"color": _RED}),
2635-            ]
```
2. `_tf(arr)` is repeated on lines 379, 386, 1853, and 1861 and the `1e-300` floor is hardcoded rather than stored as a constant.
```
laolmstead@LAOLMSTEAD:~/repos/MFC$ grep -n "def _tf\|1e-300" toolchain/mfc/viz/interactive.py
302:                cmin = float(np.log10(max(vmin, 1e-300)))
303:                cmax = float(np.log10(max(vmax, 1e-300)))
304:                display = np.where(raw > 0, np.log10(np.maximum(raw, 1e-300)), np.nan)
379:                def _tf(arr):
380:                    return np.where(arr > 0, np.log10(np.maximum(arr, 1e-300)), np.nan)
382:                cmin = float(np.log10(max(vmin, 1e-300)))
383:                cmax = float(np.log10(max(vmax, 1e-300)))
386:                def _tf(arr):
1853:            def _tf(arr):
1854:                return np.where(arr > 0, np.log10(np.maximum(arr, 1e-300)), np.nan)
1856:            cmin = float(np.log10(max(vmin, 1e-300)))
1857:            cmax = float(np.log10(max(vmax, 1e-300)))
1861:            def _tf(arr):
```
3. The logic `(step, var, mode, log, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` is duplicated at lines 350, 432, and 1890. Additionally, there are a few other mesh calls that also could be duplicates. I will investigate these further to verify this.
```
laolmstead@LAOLMSTEAD:~/repos/MFC$ grep -n 'key = (step, var, mode' toolchain/mfc/viz/interact
ive.py
350:    key = (step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)
432:    key = (step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)
```
```
laolmstead@LAOLMSTEAD:~/repos/MFC$ grep -n '_get_cached_3d_mesh\|_prefetch_3d_mesh' toolchain/mfc/viz/interactive.py
325:def _prefetch_3d_mesh(
418:def _get_cached_3d_mesh(
1774:                        _prefetch_3d_mesh(
1806:                        _prefetch_3d_mesh(
1890:                    _get_cached_3d_mesh(
2025:                    _cached = _get_cached_3d_mesh(
2075:                    _cached = _get_cached_3d_mesh(
2142:                _cached_primary = _get_cached_3d_mesh(
```
4. `toolchain/mfc/viz/test_viz.py` has no references to `interactive`.

```
laolmstead@LAOLMSTEAD:~/repos/MFC$ ./mfc.sh lint
mfc: (venv) Running ruff on MFC's toolchain.
All checks passed!
...
collected 802 items
...
mfc/viz/test_viz.py::TestTuiCache::test_cache_hit_avoids_reload PASSED
mfc/viz/test_viz.py::TestRenderLogScale::test_render_2d_log_scale PASSED
...
FAILED mfc/run/test_archive.py::TestArchiveFormats::test_format_tar_zst - mfc.common.MFCException: Archive: 'tar --zstd' failed with exit code 2. Ensure GNU tar >= 1.31.
============================== 1 failed, 801 passed, 8 warnings, 9 subtests passed in 188.21s (0:03:08) ==============================
```

Lint passes and the existing viz tests in `test_viz.py` pass. None of them exercise `interactive.py`. The one failure (`test_format_tar_zst`) came from the missing `zstd` package on my machine, not from the repo's code, and it is fixed by installing `zstd` (see the follow-up below).

Follow-up (2026-10-31): that failure came from `zstd` not being installed (`/bin/sh: zstd: not found` in the pytest output). I installed it with `sudo apt install zstd` (now in the setup line above), and `./mfc.sh precheck -j 4` then passed all seven steps (formatting, spelling, toolchain lint, source lint, doc references, parameter docs, example validation) with exit 0. The run above is the original, pre-`zstd` baseline.

**Toolkit**

- Tool: repro-check skill, run on my reproduction write-up.
- What it produced: A failing grade on the first couple of runs, with the suggestion to use grep commands to show the duplication instead of just citing line numbers from the code.
- Difficulties: It failed my write-up a couple of times before it passed, because citing the duplicate line numbers was determined to be unsupported assertions. My issue wasn't a clear cut bug, but a refactor to remove duplicate code. I had to change up my approach to get this tool to work with my scearnio.
- What changed: I replaced the manually cited line numbers with the grep commands and their pasted output (Environment Setup and Steps to Reproduce), so a stranger can re-run each check.

---

## Solution Approach

**Analysis**

`toolchain/mfc/viz/interactive.py` (the Dash/Plotly interactive viewer) was built up by copy-paste, so three small duplicate code pieces exist in several places with nothing keeping the copies in sync. There is no bug to fix. The risk is that a later edit changes one copy and misses the others. `interactive.py` also has no unit tests, so nothing would catch that.

1. Status `html.Div` ("step N", "· shape ...", `Br`, min, max): the same 7-child block inside `_update` at four sites: the 3D server-side (kaleido) render path (~L1971), the 3D patch path (~L2120), the 2D patch path (~L2470), and the full figure path shared by all dimensions (~L2626). Only the local names for min/max differ.
2. Log/identity transform: `_tf(arr)` is defined as a closure twice in `_prefetch_3d_mesh` (~L379/386) and twice in `_update` (~L1853/1861), each beside an inline `cmin`/`cmax = log10(max(v, 1e-300))`. The `1e-300` floor is also inlined in the 2D path (~L302-304). The floor is a bare literal nine times, in those three blocks.
3. Mesh cache key: the 11-field tuple `(step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` is built by hand in `_prefetch_3d_mesh` (L350) and `_get_cached_3d_mesh` (L432). These two must produce identical keys or prefetched meshes are never found. `_update` passes the same 11 values as positional arguments at six calls (~L1774, 1806, 1890, 2025, 2075, 2142), each listing them again in order, with the same `float(iso_min_frac or 0.2)` style defaults. This is the third site the issue names (~L1890). The six calls differ only in `step` (the two prefetches use the next step, `_ns`), and none of the 11 values change after `log` is resolved (~L1736).
4. No test in `toolchain/mfc/viz/test_viz.py` imports `interactive.py`.

**Proposed Solution**

Extract each piece into one module level helper in `interactive.py` and call it from every existing site. Behavior stays identical.

- `_LOG_FLOOR = 1e-300`, a module constant that replaces every inline literal.
- `_status_div(step, shape, dmin, dmax) -> html.Div`, called at the four sites.
- `_log_transform(log: bool, vmin: float, vmax: float) -> tuple`, returning `(tf, cmin, cmax)`. The issue writes `_log_transform(log)`, but it also asks for the cmin/cmax pair, which needs vmin/vmax, so I take them as arguments. It replaces the four `_tf` closures and their adjacent cmin/cmax lines; the 2D path (~L302-304) computes the same values, so it uses it too.
- `_Mesh3Key`, a small `typing.NamedTuple` with the 11 fields `(step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)`. This is the issue's "small namedtuple" option, used at all three sites it names: `_update` builds one key per call (`mesh_key`), passes it to its four `_get_cached_3d_mesh` lookups and `mesh_key._replace(step=_ns)` to its two `_prefetch_3d_mesh` calls, and `_prefetch_3d_mesh(key, get_ad_fn)` and `_get_cached_3d_mesh(key)` take the key instead of 11 separate arguments (replacing the tuples at L350 and L432). The issue writes `_mesh3_key(...)`; a namedtuple class is named `_Mesh3Key` by Python convention. Because the key is built once, its `or 0.2`-style defaults are written once instead of six times. The issue does not ask for that, but it follows from passing one key and removes the same kind of drift.
- The `turbojpeg` import guard at the top of `interactive.py` also catches `RuntimeError`, which current PyTurboJPEG raises when the native `libturbojpeg` library is missing. Without it the module cannot be imported where the library is absent, as on CI's runners, so none of the new tests can run there. With it the module falls back to Pillow as its own comment says. The issue does not ask for this. It was added after the PR's first CI run failed (step 7), with its own test, `TestTurboJPEGFallback`.
- Add `TestStatusDiv`, `TestLogTransform` and `TestMesh3Key` to `toolchain/mfc/viz/test_viz.py`, the first tests for `interactive.py`. Keep them short, since the file is at 917 lines and the soft limit is 1000.

Not changing:
- Callback control flow, `_update`'s structure (beyond the one added `mesh_key` line and the six simpler calls), any other file, and any rendered output.

**Implementation Plan**

1. Branch `feature/viz-interactive-dedup` from the synced upstream `master` (done; branched from `a03848a0`, then rebased onto upstream `master` at `643ceae5` before pushing).
2. Extract `_log_transform` and `_LOG_FLOOR`, using TDD (done; committed as `1f6a6948`). Each cycle is: write one test in `test_viz.py` (`TestLogTransform`), run it and confirm it fails for the expected reason (red), write the least code in `interactive.py` that makes it pass (green), tidy, and re-run the suite before the next test.
   1. Test: `log=True` returns the log10 transform (NaN for non-positive input) with `cmin`/`cmax`. Then add `_log_transform` to pass it.
   2. Test: `log=False` returns the input unchanged with `vmin`/`vmax`. Then add the identity branch.
   3. Test: `vmin=0` clamps to the `_LOG_FLOOR` constant. Then add `_LOG_FLOOR` and use it in the helper.
   4. Refactor: replace the four `_tf` closures, their adjacent cmin/cmax lines, and the 2D-path floor literals with `_log_transform`; the existing viz tests must still pass.
   5. Commit the helper, its call-site changes and its tests as one commit.
3. Replace the hand-built mesh cache key with a small namedtuple, `_Mesh3Key`, that `_update` builds once and passes to the cache functions, using TDD with the same cycle (`TestMesh3Key`). `_prefetch_3d_mesh` and `_get_cached_3d_mesh` take the key instead of 11 separate arguments.
   1. Test: `_Mesh3Key` holds the 11 fields in order, readable by name (for example `key.iso_n`) and equal to the plain 11-value tuple, so it hashes and compares like the old keys. Then add `_Mesh3Key` as a `typing.NamedTuple` to pass it.
   2. Test: changing any one field changes the key. It may already pass, in which case it stays as a guard.
   3. Test: `_get_cached_3d_mesh(key)` returns the value stored under `key` in the cache. It fails while the function still takes 11 arguments. Then change it to take the key.
   4. Test: `_prefetch_3d_mesh(key, get_ad_fn)`, run on a tiny fake 3D array in volume mode, stores its result under `key`, and the stored value range matches the key's `vol_min_frac` and `vol_max_frac`, which shows the fields are read in the right order. It fails while the function still takes 11 arguments. Then change it to take the key and unpack its fields at the top; the rest of the function is unchanged.
   5. Refactor: in `_update`, build `mesh_key = _Mesh3Key(...)` once, right after `log` is resolved (~L1736; none of the 11 values change after that line), pass `mesh_key` to the four `_get_cached_3d_mesh` lookups, and pass `mesh_key._replace(step=_ns)` to the two `_prefetch_3d_mesh` calls. The existing viz tests must still pass. Cycles 3.3 and 3.4 break these calls until this step, so nothing is committed before it, and because these calls have no unit tests, step 5 checks them.
   6. Commit `_Mesh3Key`, the two signature changes, the `_update` changes and the tests as one commit.
4. Extract `_status_div`, using TDD with the same cycle (`TestStatusDiv`).
   1. Test: the children, text and colors for simple values. Then add `_status_div` to pass it.
   2. Test: numbers use the `.4g` format. Then change the formatting to pass it.
   3. Refactor: replace the four copies in `_update` with `_status_div`; the existing viz tests must still pass.
   4. Commit the helper, its call-site changes and its tests as one commit.
5. Beyond the unit tests, which cannot reach the closures and calls inside `_update` (nothing is committed for these): (a) run a throwaway script on `master` and on the branch that calls `_prefetch_jpeg` and `_prefetch_3d_mesh` (each with its own signature) with a fake data loader, in log and non-log mode, and compare `_jpeg_cache` and `_mesh3_cache`; (b) launch `./mfc.sh viz <fixture> --interactive` on the 2D and 3D fixtures before and after and compare the status line, color bar and log toggle, and on the 3D fixture use isosurface and volume mode and play through the steps, so the six changed `_update` calls (prefetch and cache lookup) run. Save the output in `test_evidence.md`.
6. Run the manifest checks: `./mfc.sh precheck -j 4`, `test_viz.py`, and `./mfc.sh test -j 12` (baseline on master: 726 passed, 0 failed, 39 skipped).
7. Push the branch and check that CI can import `interactive.py` (the `turbojpeg` risk below). It could not: on the PR's first CI run all nine new tests failed with `RuntimeError: Unable to locate turbojpeg library`. Fix it test-first: a test that reloads `interactive.py` with `TurboJPEG()` raising `RuntimeError` fails, then adding `RuntimeError` to the import guard makes it pass. Commit and push it, update the PR description, and post a PR comment that explains it and offers to move it to its own PR.
8. Open the PR from my fork, using the PR template, with `Fixes #1518`, and state that AI assistance was used.

Tests come first because my claim comment on the issue says I would write the tests first and implement against them, and the issue asks for tests that make the dedup verifiable. Each helper is committed with its tests because the pre-commit hook runs the unit tests and would reject a commit with a failing test.

Risk: `interactive.py` raises at import where `libturbojpeg` is missing (the `except` catches `ImportError`/`OSError`, but this `turbojpeg` raises `RuntimeError`), so the new tests need that library installed locally. If CI also lacks it, the tests would fail there; I'll check the first CI run and handle it in the PR rather than widening scope silently. CI did lack it; step 7 records the fix.

Deviations from this plan:

- 2026-11-06: Added a fix the issue does not ask for. On the PR's first CI run all nine new tests failed, because `interactive.py` cannot be imported without the native `libturbojpeg`: PyTurboJPEG raises `RuntimeError`, which the import guard did not catch, so the Pillow fallback never ran. I added `RuntimeError` to the guard, with a test, and removed "`turbojpeg` handling" from Not changing.
- 2026-11-04: Rewrote step 3 again to use the issue's "small namedtuple" option. Building a plain-tuple key at each of the six `_update` calls still repeated the 11 values and their defaults six times. With a `_Mesh3Key` namedtuple, `_update` builds the key once and the prefetches use `mesh_key._replace(step=_ns)`, so the values and defaults appear once. I undid the uncommitted plain-tuple version of step 3 and started it again from this plan.
- 2026-11-04: Corrected two facts in the Analysis after re-checking `master`: the four status Div sites are the 3D kaleido, 3D patch, 2D patch and shared full-figure paths (I had named them wrongly), and the floor literal appears nine times, not five. Also added the type hints to `_log_transform`'s signature and marked steps 1 and 2 done.
- 2026-11-01: The issue calls the status Div "8-child"; the code has 7 children (6 `Span`s and one `Br`). Corrected in the Analysis.
- 2026-11-01: Added step 5 (before/after comparison and a manual run of the interactive viewer) because unit tests cannot reach the closures inside `_update`. Nothing from it is committed.
- 2026-11-01: My first draft put the tests last, which contradicted my claim comment on the issue ("I'll start by writing the unit tests ... then implement the fix against them"). I rolled back the one code commit I had made. My second draft wrote all the tests at once before any helper, which is not TDD, so I discarded those too. The plan now uses red-green-refactor cycles, one test at a time, with each helper its own numbered step (steps 2 to 4) and committed together with its tests and call-site changes.

**Toolkit**

- Tool: plan-check skill, run in Claude Code on `plan.md` and my draft `plan-comment.md` against issue #1518. It checked the plan against the live issue and the code, then graded five required checks (diagnosis, scope, executability, test-plan, comms) and read the comment against my voice guide. I re-ran it each time the plan changed, as its instructions say to.
- What it produced: `accept` on all runs, with all five checks passing each time. The runs covered the TDD restructure, and the final `_Mesh3Key` namedtuple version. Each time it re-checked my facts on `master` (4 status Divs with 7 children each, 9 `1e-300` literals, `_tf` at 379/386/1853/1861, the key built at 350/432, six `_update` calls, no `interactive` references in `test_viz.py`). The last run also listed four voice-guide breaks in my plan comment: too long for my "Be concise" rule, a redundant re-claim, a vague closing question, and no mention of the `_Mesh3Key` rename or the defaults being written once.
- Difficulties: My procedure expects a posted repro comment, and this refactor issue has none, so it graded the diagnosis on the issue body and its own live check; my procedure has no rule for that case. It also exposed that `procedure.md` calls the first check `root cause` while the rubric calls it `diagnosis`, and that the evidence guide's honesty section has no rubric check. Because it accepted every version, it did not catch that my first mesh key plan met only two of the issue's three sites. I found that by rereading the issue.
- What changed: The plan changed between runs because of my own review, not because plan-check rejected anything. After the last run I rewrote the plan comment to six short sentences: I dropped the re-claim and the long cause paragraph, named both differences from the issue (the `_log_transform` arguments and the `_Mesh3Key` namedtuple with its defaults written once), and made the question say what it is about.

---

## Testing Strategy

Two observable checks prove the fix, and both are recorded in my `test_evidence.md` with their output.

**1. The reproduction, before and after.** I re-ran the four greps from Reproduction Process on my branch (`e589daa9`, steps 2 to 4 committed):

| Check | Before (master) | After (branch) |
|---|---|---|
| Status `html.Div` copies (`shape {raw.shape}`) | 4 copies (L1971, 2120, 2470, 2626) | 0 copies; `_status_div(...)` called at the 4 sites |
| `_tf` closures and the `1e-300` floor | `_tf` at L379/386/1853/1861, `1e-300` nine times | no `_tf`; `1e-300` only in `_LOG_FLOOR`; `_log_transform(...)` called at 3 sites |
| Hand-built mesh cache key | tuple at L350 and L432, 11 arguments at six `_update` calls | no tuples; one `_Mesh3Key` built in `_update` and passed to all six calls |
| Tests for `interactive.py` in `test_viz.py` | 0 | `TestLogTransform`, `TestMesh3Key`, `TestStatusDiv`, `TestTurboJPEGFallback` |

**2. The repo's own checks** (my ship-gate manifest's two rows, plus the full regression suite, which I later moved to the manifest's excluded table because of the timeouts described here): `./mfc.sh precheck -j 4` passes all seven steps (formatting, spelling, ruff plus every toolchain unit test, source lint, doc references, parameter docs, example cases); `test_viz.py` gives 68 passed and 19 skipped (87 passed with the render tests), re-run on 2026-11-07 at the branch head (my 2026-11-05 run gave 67; the extra test is `TestTurboJPEGFallback`, added on 2026-11-06); and `./mfc.sh test -j 12`, the full regression suite, ran 727 passed, 2 failed and 39 skipped in 88 minutes. The 2 failures were timeouts in a Fortran phase-change test (`AAE5C27B`, `02BD9B5E`) that ran past the suite's 1-hour limit while sharing the machine with heavy 3D tests; run alone, both passed in about 11 minutes. My baseline on an older master (`e95a827a`) was 726 passed, 0 failed, 39 skipped.

How the new tests were checked: each was written before its code, and all but one failed first for the expected reason. The exception, the any-field guard on `_Mesh3Key`, passed immediately, as the plan allowed.

Code the unit tests cannot reach: the changed lines inside `_update`, the Dash callback. For those I used three checks: an AST comparison showing every rewritten call gets exactly the key or values it got before; a script comparing `master` and the branch's prefetch caches on identical inputs (2D 36 of 36 and 3D 48 of 48 identical; a deliberately wrong key made 48 of 48 differ); and both viewers side by side on the 2D and 3D fixtures, which looked the same, with 0 errors and the same rate of prefetched-mesh hits during 3D playback (about 98%).

What these do not cover: the kaleido server-side render path and the prefetch call used when no single-variable reader is passed. Kaleido rendering fails on `master` and my branch alike (`to_image() got an unexpected keyword argument 'engine'`), and `./mfc.sh viz` always passes a reader, so no viewer run reaches them; only the AST checks cover those two sites.

**Toolkit**

- Tool: the ship-gate, through the project checks in my manifest that it runs before a PR opens: `./mfc.sh precheck -j 4` and the `test_viz.py` row, plus `./mfc.sh test -j 12`, which started in the manifest and is now in its excluded table. I ran them on my branch first, then through the gate itself. Its first run on 2026-11-06 blocked on my PR description, not on these checks, and it passed after I fixed the description (see the Pull Request section's Toolkit block).
- What it produced: precheck passes all seven steps, `test_viz.py` gives 68 passed and 19 skipped, and the full regression suite gave 727 passed with 2 timeouts in a Fortran phase-change test, which both passed when rerun alone. The before and after output the gate's pr-precheck will read is in my `test_evidence.md`.
- Difficulties: The manifest's checks cannot reach the changed calls inside `_update`, because no unit test can, so those needed checks the gate does not run: an AST comparison, a master-vs-branch cache comparison and a side-by-side viewer run. `./mfc.sh test` took 88 minutes on my branch, and under that load two slow phase-change tests can time out, so a gate run could stop for a reason that has nothing to do with my change. My baseline is also from an older master.
- What changed: I moved `./mfc.sh test -j 12` from the manifest's checks to its excluded table, dated 2026-11-05, with the timeout reason and the rerun as evidence, so the gate does not stop on a test my change cannot affect. The skip variable now goes directly before the `python` command. I recorded the extra checks, and the two sites nothing could reach, in `test_evidence.md` so the gate and a reviewer can see them, and gave a negative control to any test that passed without failing first.

---

## Implementation Notes

**2026-11-01**

Before writing code I checked that the new tests can import `interactive.py`. They couldn't: `import mfc.viz.interactive` raised `RuntimeError: Unable to locate turbojpeg library`. The module's `except (ImportError, OSError)` around `TurboJPEG()` doesn't catch that error type, so the Pillow fallback never runs. Neither the contributing guide, the setup docs nor `pyproject.toml` tells contributors to install the native library, so I treated it as a local workaround, not a project change. I installed it with `sudo apt install libturbojpeg0` (the package named `libturbojpeg` doesn't exist on Ubuntu), added it to the setup line in Reproduction Process, and confirmed the import now works with `_tj` loaded. I'm not changing the `except` in this PR, since it is outside the plan; I'll mention it in the plan comment and watch whether CI has the same problem.

**2026-11-01 (later)**

Re-read my claim comment on the issue and saw it promised tests first, but my plan had them last. I rolled the branch back to `a03848a0` (upstream `master`, unchanged since my baseline). I then wrote all three test classes at once before any helper existed (7 failed with `AttributeError`, 1 passed), but that is not TDD: TDD adds one failing test, makes it pass, and only then adds the next. I discarded those tests (nothing was committed) and rewrote the plan as TDD cycles. Each helper will be committed with its tests, because the pre-commit hook runs the unit tests and rejects a failing commit.

**2026-11-01 (step 2: `_log_transform` and `_LOG_FLOOR`)**

Built `_log_transform` in three red-green cycles, one test at a time, log values with NaN for non-positive input, then the identity branch for `log=False`, then the `_LOG_FLOOR` clamp. Each test failed for the expected reason before any code existed. The refactor replaced the four `_tf` closures and their `cmin`/`cmax` lines, plus the 2D JPEG path's inline log, which the issue does not list. Because that 2D site was my own addition, I checked it by running `master` and my branch on the same 56 inputs and comparing the arrays passed to the image encoder, with a deliberately broken floor as a control (20 of 56 then differed). Review changes: I moved `_LOG_FLOOR` from the middle of the file to the top constants block where the file keeps its other numbers, added the `log: bool` type hints the issue's signature shows, and renamed the tests (for example `test_log_true_clamps_zero_vmin_to_floor`) so their names say what they check. Claude Code had committed for me with long messages. I undid that so I review and make every commit myself, with one-line messages. Committed as `1f6a6948`.

**2026-11-02 (step 3, first attempt)**

My first `_mesh3_key` version only replaced the two hand-built key tuples (L350, L432) with a helper call, plus a round-trip test that prefetches a mesh and looks it up. The six `_update` calls still passed the same 11 arguments each. I did not commit it.

**2026-11-04 (step 3, redesign)**

Rereading the issue ("use it at all three sites", "passed positionally from `_update` at ~1890", "or a small namedtuple"), I decided the key should be built by the caller and passed in. A plain-tuple version still listed the 11 values and their defaults at all six calls, so I switched to a `_Mesh3Key` `typing.NamedTuple` that `_update` builds once; the prefetches use `mesh_key._replace(step=_ns)` for the next step. I checked that none of the 11 inputs change after `log` is resolved, so building the key there is safe, and that `_replace` returns a new key instead of changing the one the lookups use. Each redesign went through `plan.md`, this story and the plan comment together, with plan-check re-run (accept each time). TDD: field order and the any-field guard, then `_get_cached_3d_mesh(key)` and `_prefetch_3d_mesh(key, get_ad_fn)` each failed while they still took 11 arguments. The prefetch test checks the stored volume range, so a swapped unpack would fail it (confirmed with a control). The six `_update` calls have no unit tests, so the refactor was done from the parsed code and checked with the AST: each call gets exactly the key it got before. Committed as `55765ec0`.

**2026-11-04 (step 4: `_status_div`)**

Two red-green cycles: the Div's children, text and colors. Before replacing the four copies in `_update`, I checked with the AST that each one is exactly the helper's body with its own variables. All four were, differing only in the min/max names. Committed as `e589daa9`.

**2026-11-04 to 2026-11-05 (step 5: before/after checks)**

A throwaway script ran `master` and my branch on the same inputs and compared their prefetch caches: 36 of 36 2D cases and 48 of 48 3D cases identical, and a deliberately wrong key made all 48 3D cases differ. Then I ran both viewers side by side on the 2D and 3D fixtures. They looked the same, and their logs showed the same rate of prefetched-mesh hits during 3D playback (about 98%). Two changed sites cannot be reached from the viewer here: kaleido rendering fails on both versions (`to_image() got an unexpected keyword argument 'engine'`, an existing plotly/kaleido mismatch unrelated to this change), and one prefetch call only runs when no single-variable reader is passed. The AST checks from steps 3 and 4 cover both.

**2026-11-05 (step 6: manifest checks)**

`./mfc.sh precheck` passes all seven steps and `test_viz.py` passes (67 passed, 19 skipped; this was before `TestTurboJPEGFallback` was added on 2026-11-06, and the 2026-11-07 re-run gives 68 passed, 19 skipped). The four reproduction greps now show each duplication gone and the new tests present. The full regression suite (`./mfc.sh test -j 12`) took 88 minutes: 727 passed, 39 skipped, and 2 failed by timing out after an hour, both in `2D -> Phase Change model 6 -> 3 Fluid(s)`. Those are Fortran tests my change doesn't touch, and the same two UUIDs had failed in a run before I started. I reran just those two with nothing else competing for the CPU, and both passed in about 11 minutes, so the timeouts came from load, not from my code.

**2026-11-05 (step 7: rebase)**

Rebased my three commits onto the current upstream `master` (`643ceae5`) so the PR applies cleanly; none of the new upstream commits touch `toolchain/mfc/viz`, and my two files came out byte-for-byte the same. The rebase rewrote the commit hashes (`1f6a6948`, `55765ec0`, `e589daa9`), so I updated them here and in my plan. Precheck and `test_viz.py` pass again on the rebased branch.

**2026-11-06 (step 8: ship-gate, PR and a CI failure)**

My first ship-gate run blocked: my own pr-precheck failed test-evidence, because I had cut my PR description down so far that the Verification section ended mid-sentence and no longer reported the check results. After I fixed the description the gate passed, and I opened PR #2170. Its first CI run then failed on all nine new tests with `RuntimeError: Unable to locate turbojpeg library`. The module's import guard catches `ImportError` and `OSError` but not the `RuntimeError` PyTurboJPEG raises, so `interactive.py` couldn't be imported. The gate couldn't catch this because it runs on my machine, where I had installed the library. To fix it, I added a new test that reloads `interactive.py` with `TurboJPEG()` raising `RuntimeError`. It failed with the same error as CI, then passed once `RuntimeError` was added to the guard. I also corrected the comment above the guard, which only mentioned `OSError`. I considered asking the maintainers first, but chose to make CI green and say what I changed, offering to change my fix as needed. After I pushed the fix, CI passed with all ten new tests running, and I posted a PR comment explaining the change.

**2026-11-07 (PR monitor and playbook)**

With PR #2170 open and no human review, I installed the PR monitor and wrote my playbook, setting thresholds from MFC's recent merged PRs instead of guessing. A full run drafted "wait, no nudge yet" because the PR is one day old and CI was still running; I sent nothing. The one thing I changed was the playbook's clock rule, so bot comments don't count as activity. Status stays Awaiting review.

**Toolkit**

- Tool: the PR monitor, installed on 2026-11-07 and run against PR #2170 with the playbook I wrote from six recent merged outside-contributor PRs (first-review threshold of 7 quiet days, one nudge only). I ran it first with `--state`, then as a full run that drafts a reply through the polite-nudge form.
- What it produced: The `--state` run read the PR as "feedback-in". After I filled in the playbook, the full run drafted "Wait, no nudge yet": the PR was a day old, 27 checks were still pending, and my own rule says the threshold is met on 2026-11-13. I followed the draft and posted nothing.
- Difficulties: The first `--state` run counted bot comments (the review bot's failed run and Codecov) as feedback, which I confirmed with `gh`; no human had responded. The full run's draft also had to guess which date my stalled-review clock started, because my playbook did not say.
- What changed: I tightened the playbook so the clock counts days since anyone but me commented, and bot comments do not restart it. The next check is due on 2026-11-13.

---

## Pull Request

**PR Link:** https://github.com/MFlowCode/MFC/pull/2170

**PR Description:** Opened 2026-11-06 as "Dedupe repeated code in toolchain/mfc/viz/interactive.py". The description says `Fixes #1518` and that the three repeated pieces became `_log_transform`/`_LOG_FLOOR`, a `_Mesh3Key` NamedTuple and `_status_div`, with the module's first unit tests (`TestLogTransform`, `TestMesh3Key`, `TestStatusDiv`). The first version of the description was short: under Verification it only said that I added unit tests, re-ran the existing test suite and compared the 2D and 3D viewers side by side with master, and it did not mention `TestTurboJPEGFallback` or the import-guard fix, which came after the first CI run failed. I explained that fix in a PR comment on 2026-11-06 instead. I later rewrote the description so it carries that information itself. It now lists the three repeated pieces with their before and after (4 status blocks into `_status_div`; 4 `_tf` closures and 9 `1e-300` literals into `_log_transform` and one `_LOG_FLOOR`; two hand-built 11-element key tuples into a `_Mesh3Key` NamedTuple), and it calls out the import-guard fix as an unrelated change in its own commit (`6c0f6653`), offering to move it to its own PR or implement a different fix if the maintainers prefer. Verification is now a before/after table on master `799ccc66` and my branch: `test_viz.py` went from 58 to 68 passed (19 skipped), precheck passes all seven steps, the regression suite gave 727 passed with 2 phase-change timeouts that pass when run alone, and the master-vs-branch cache comparison matched. The 10 new tests are listed by class. Under AI Usage, I mentioned that I used Claude Code to summarize the codebase and draft the implementation plan.

**Maintainer Feedback:**

- 2026-11-07: none yet. No maintainer has commented or reviewed. The only other comments are the repo's automated Claude review bot (its run failed without producing a review) and Codecov. My PR monitor drafted "wait, no nudge yet", so I sent no reply. By my playbook the first nudge is due after 7 quiet days, on 2026-11-13.

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate, run by hand with `check_gate.py` on my branch and again by its hook when I opened the PR through Claude Code. It runs my manifest's checks, then my pr-precheck on the branch, plan, evidence and description.
- What it produced: The first run (2026-11-06, 00:24) blocked. Both manifest checks passed, but my pr-precheck failed. "Description's Verification section ends mid-sentence, and neither the precheck result nor the golden-suite timeout caveat is reported in the PR text." After I fixed the description it passed (00:44), and it passed again through the hook when I opened PR #2170, with all four pr-precheck checks (plan-fidelity, test-evidence, diff-quality, standards-comms) passing.
- Difficulties: It only sees my machine. It passed while the PR's first CI run failed on all nine new tests, because CI's runners lack the native `libturbojpeg` I had installed locally. Its pr-precheck also takes test evidence partly from my local `test_evidence.md`, which maintainers never see, so a pass did not mean the description on GitHub carried the evidence.
- What changed: I rewrote the Verification section until the gate passed, and fixed the CI failure in the PR with a tested one-line change to the import guard. I first chose not to edit the PR description after submitting it, and kept the full before/after evidence (the four reproduction greps, precheck, `test_viz.py`, the master-vs-branch cache comparison and the CI result) in Testing Strategy above and in my local `test_evidence.md`, since this was a refactor issue and the before steps were spelled out in the issue description. I later reversed that: a reviewer reading only the PR should not have to reconstruct the evidence from another page, so I rewrote the description to carry the before/after, the test results and the import-guard fix itself. The gate passing never meant the description on GitHub carried the evidence.

---

## Learnings and Reflections

**Technical Skills Gained**

- Test-driven development in practice: I added one `unittest` test at a time, ran red for the expected reason, then added the least code to pass it. I had done this in school previously but wanted to get real-world experience working with it.
- Open source PR ettiquette: I learned how to communicate with OS maintainers and the proper way to claim and issue and open a PR. I have opened PRs at work before but never with an Open Source repo so this was all new and interesting to me.
- Python details I used for the first time: I have mostly worked with C# in my professional career so this was my first Python repo that I've worked on (other than my own private repos).
- Claude skills and hooks:  I learned to work with and create Claude skills and hooks. I also learned how to adjust them as you go when they are not returning the desired results.

**Challenges Overcome**

- My environment broke twice before I changed any code: the toolchain tests failed without `zstd`, and `interactive.py` would not import because `turbojpeg` raised a `RuntimeError` that the module's `except` doesn't catch. Neither is in the setup docs; I installed both packages as local workarounds and put the `turbojpeg` risk in my plan.
- Reading the issue precisely. Step 3 went through three designs, and I committed the third: replacing only the two key tuples, then passing a plain tuple key, then a `_Mesh3Key` namedtuple built once in `_update`. The issue's "use it at all three sites" and "or a small namedtuple" were there from the start. I only caught them by rereading it. Each change went through `plan.md`, this story and the plan comment, and plan-check again.
- Holding myself to my claim comment. I told the maintainer I would write the tests first. My first plan put them last, and my second wrote them all at once; I rolled both back and redid the plan as TDD cycles.
- My workload outside of this class has increased over the past month so I had started to fall behind on this assignment over the past couple weeks. I got around this by staying up a little later and working on this over the weekend as needed.

**What I'd Do Differently Next Time**

- Reread my own claim comment and the issue's exact wording before writing the plan, so the test-first promise and "all three sites" shape the first plan instead of the third.
- Make every commit myself from the start, with one-line messages, instead of undoing commits made for me by Claude.
- Push to my fork and check CI before opening the PR. The `turbojpeg` failure only showed up on GitHub's runners.
- Ask about the Toolkit blocks early. I filled some with the wrong tool before a TA explained in Slack that they should describe the ship-gate, plan-check and the other course tools.

---

## Resources Used

- MFC contributing guide, https://mflowcode.github.io/documentation/contributing.html: the lint gate's six checks (the basis of my ship-gate manifest), the `feature/<short-name>` branch naming and the PR rules.
- The issue itself, https://github.com/MFlowCode/MFC/issues/1518: I went back to its exact wording ("use it at all three sites", "or a small namedtuple") more than once.
- `docs/documentation/visualization.md` in the MFC repo: the `./mfc.sh viz --interactive` commands I used to run the viewer on the repo's test fixtures.
- `.github/workflows/test.yml` and `toolchain/bootstrap/lint.sh`: how CI runs the lint gate and how the toolchain runs `pytest`, which I copied into my manifest.
- MFC's recent merged pull requests from outside contributors, read with `gh api`: how long a maintainer's first response took, which set my playbook's 7-day threshold.
- A course TA's answer in Slack about which tools belong in the Toolkit blocks.
- Claude Code
