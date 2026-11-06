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

**Unit 7: Installed the ship-gate and wrote its manifest for MFC**

I wrote the manifest from MFC's contributing guide, whose Lint Gate lists six checks that `./mfc.sh precheck` bundles, and ran every command in a shell before trusting it. `./mfc.sh lint` failed on `test_format_tar_zst` because `zstd` was not installed, so my first draft excluded it; after I installed `zstd`, precheck passed all seven steps and I replaced several rows with one `./mfc.sh precheck -j 4` row. I also added a row that runs `test_viz.py` and one for `./mfc.sh test -j 12`, whose baseline on master (726 passed, 62 minutes) tells me the gate will take about an hour per run. I have not run the ship-gate on my branch yet, so what it says about my changes is still to come.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

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

Three different pieces of logic are repeated in multiple places in the code base. The duplicate logic presents a risk that if a change is made in one place, it could be missed or copied wrong in another which could lead to unintended bugs.

The goal of this issue is to de-depulicate this logic and add unit tests to verify the existing behavior.

**Expected Behavior**

1. One function `_status_div(step, shape, dmin, dmax) -> html.Div` exists for the function shape `html.Div (step {step} / · shape {raw.shape} / Br / min+value / max+value, same _YELLOW/_MUTED/_BLUE/_RED styles)` and it is called on lines 1971, 2120, 2470, 2626.
2. `_log_transform(log: bool)` exists instead of the duplicate `_tf(arr)` logic returning the transform and the `cmin`/`cmax` pair. The 1e-300 floor is moved to a module constant `_LOG_FLOOR`
3. Add `_mesh3_key(...) -> tuple` and use it on lines 350, 432, and 1890.
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

- Tool: plan-check. Its diagnosis check reads my plan's account of the issue against the issue text and the code on master, so it was the tool that tested whether I had understood the issue correctly.
- What it produced: It confirmed the facts my four answers rest on: four status Div copies, `_tf` at 379/386/1853/1861, the key built at 350 and 432, and no tests for `interactive.py`. Its last run also confirmed that the status Div has 7 children, not the 8 the issue says.
- Difficulties: It accepted my first reading of the issue's third key site, where I only replaced the two tuples, so it did not catch that "use it at all three sites" meant the six `_update` calls too. I found that by rereading the issue myself. It also has no rule for refactor issues with no repro comment, so it checked my understanding against the issue body only.
- What changed: I rewrote my plan to use the key at all three sites, and kept the issue's wording differences (7 children, the `_Mesh3Key` name) stated openly in my plan and plan comment instead of quietly matching the issue.

---

## Reproduction Process

**Environment Setup**

Ran on master @ e95a827a334601f7d03162ff3f3a1cae6bf484a1 (`toolchain/mfc/viz/interactive.py`). Environment: WSL2 Ubuntu 26.04 (x86_64), Python 3.14.4, gfortran 15.2.0, Open MPI 5.0.10 (mpif90), cmake 4.2.3, make 4.4.1, gcc/g++ 15.2.0. The issue was filed against `40dde5e`; the line numbers it cites are unchanged at `e95a827`. All three duplications described in the issue are present, and I found no tests for `interactive.py`.

Setup (no build needed; this is a refactor issue, and `./mfc.sh` creates the Python venv in `build/venv` on first use):
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
- **My findings:** All three duplications in the issue reproduce on `e95a827`, and `interactive.py` has no tests. Two details differ slightly from the issue's wording. (a) The `_tf` duplication is at lines 379/386 and 1853/1861, and the same `1e-300` floor is also inlined at lines 302-304, 382-383, and 1856-1857, so `_LOG_FLOOR` should replace those too. (b) The literal `key = (step, var, mode, ...)` tuple only appears at lines 350 and 432. Line 1890 is a `_get_cached_3d_mesh(...)` call that passes the same arguments, not a key tuple, and the same call is made at 2025, 2075, and 2142, so how `_mesh3_key` applies there needs to be settled in my plan. Lint passes and 801 of 802 tests pass; the one failure (`test_format_tar_zst`) is in archive code and unrelated.

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

Lint passes and the existing viz tests in `test_viz.py` pass; none of them exercise `interactive.py`. The one failure (`test_format_tar_zst`) is in archive code and unrelated to this issue.

Follow-up (2026-10-31): that failure came from `zstd` not being installed (`/bin/sh: zstd: not found` in the pytest output). I installed it with `sudo apt install zstd` (now in the setup line above), and `./mfc.sh precheck -j 4` then passed all seven steps (formatting, spelling, toolchain lint, source lint, doc references, parameter docs, example validation) with exit 0. The run above is the original, pre-`zstd` baseline.

**Toolkit**

- Tool: repro-check skill, run on my reproduction write-up.
- What it produced: A failing grade on the first couple of runs, with the suggestion to use grep commands to show the duplication instead of just citing line numbers from the code.
- Difficulties: It failed my write-up a couple of times before it passed, because the line numbers were unsupported assertions.
- What changed: I replaced the manually cited line numbers with the grep commands and their pasted output (Environment Setup and Steps to Reproduce), so a stranger can re-run each check.

---

## Solution Approach

**Analysis**

`toolchain/mfc/viz/interactive.py` (the Dash/Plotly interactive viewer) was built up by copy-paste, so three small pure-function pieces exist in several places with nothing keeping the copies in sync. There is no bug to fix; the risk is that a later edit changes one copy and misses the others. `interactive.py` also has no unit tests, so nothing would catch that.

1. Status `html.Div` ("step N", "· shape ...", `Br`, min, max): the same 7-child block inside `_update` at four sites: the 3D server-side (kaleido) render path (~L1971), the 3D patch path (~L2120), the 2D patch path (~L2470), and the full-figure path shared by all dimensions (~L2626). Only the local names for min/max differ.
2. Log/identity transform: `_tf(arr)` is defined as a closure twice in `_prefetch_3d_mesh` (~L379/386) and twice in `_update` (~L1853/1861), each beside an inline `cmin`/`cmax = log10(max(v, 1e-300))`. The `1e-300` floor is also inlined in the 2D path (~L302-304). The floor is a bare literal nine times, in those three blocks.
3. Mesh cache key: the 11-field tuple `(step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` is built by hand in `_prefetch_3d_mesh` (L350) and `_get_cached_3d_mesh` (L432). These two must produce identical keys or prefetched meshes are never found. `_update` passes the same 11 values as positional arguments at six calls (~L1774, 1806, 1890, 2025, 2075, 2142), each listing them again in order, with the same `float(iso_min_frac or 0.2)`-style defaults; this is the third site the issue names (~L1890). The six calls differ only in `step` (the two prefetches use the next step, `_ns`), and none of the 11 values change after `log` is resolved (~L1736).
4. No test in `toolchain/mfc/viz/test_viz.py` imports `interactive.py`.

**Proposed Solution**

Extract each piece into one module-level helper in `interactive.py` and call it from every existing site. Behavior stays identical.

- `_LOG_FLOOR = 1e-300`, a module constant that replaces every inline literal.
- `_status_div(step, shape, dmin, dmax) -> html.Div`, called at the four sites.
- `_log_transform(log: bool, vmin: float, vmax: float) -> tuple`, returning `(tf, cmin, cmax)`. The issue writes `_log_transform(log)`, but it also asks for the cmin/cmax pair, which needs vmin/vmax, so I take them as arguments. It replaces the four `_tf` closures and their adjacent cmin/cmax lines; the 2D path (~L302-304) computes the same values, so it uses it too.
- `_Mesh3Key`, a small `typing.NamedTuple` with the 11 fields `(step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)`. This is the issue's "small namedtuple" option, used at all three sites it names: `_update` builds one key per call (`mesh_key`), passes it to its four `_get_cached_3d_mesh` lookups and `mesh_key._replace(step=_ns)` to its two `_prefetch_3d_mesh` calls, and `_prefetch_3d_mesh(key, get_ad_fn)` and `_get_cached_3d_mesh(key)` take the key instead of 11 separate arguments (replacing the tuples at L350 and L432). The issue writes `_mesh3_key(...)`; a namedtuple class is named `_Mesh3Key` by Python convention. Because the key is built once, its `or 0.2`-style defaults are written once instead of six times; the issue does not ask for that, but it follows from passing one key and removes the same kind of drift.
- Add `TestStatusDiv`, `TestLogTransform` and `TestMesh3Key` to `toolchain/mfc/viz/test_viz.py`, the first tests for `interactive.py`. Keep them short, since the file is at 917 lines and the soft limit is 1000.

Not changing:
- Callback control flow, `_update`'s structure (beyond the one added `mesh_key` line and the six simpler calls), `turbojpeg` handling, any other file, and any rendered output.

**Implementation Plan**

1. Branch `feature/viz-interactive-dedup` from the synced upstream `master` (done; branched from `a03848a0`).
2. Extract `_log_transform` and `_LOG_FLOOR`, using TDD (done; committed as `46ce57ab`). Each cycle is: write one test in `test_viz.py` (`TestLogTransform`), run it and confirm it fails for the expected reason (red), write the least code in `interactive.py` that makes it pass (green), tidy, and re-run the suite before the next test.
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
7. Push the branch to my fork and check that the lint-gate CI run there can import `interactive.py` (the `turbojpeg` risk below). If it cannot, handle it before opening the PR.
8. Open the PR from my fork, using the PR template, with `Fixes #1518`, and state that AI assistance was used.

Tests come first because my claim comment on the issue says I would write the tests first and implement against them, and the issue asks for tests that make the dedup verifiable. Each helper is committed with its tests because the pre-commit hook runs the unit tests and would reject a commit with a failing test.

Risk: `interactive.py` raises at import where `libturbojpeg` is missing (the `except` catches `ImportError`/`OSError`, but this `turbojpeg` raises `RuntimeError`), so the new tests need that library installed locally. If CI also lacks it, the tests would fail there; I'll check the first CI run and handle it in the PR rather than widening scope silently.

Deviations from this plan:

- 2026-11-01: My first draft put the tests last, which contradicted my claim comment on the issue ("I'll start by writing the unit tests ... then implement the fix against them"). I rolled back the one code commit I had made. My second draft wrote all the tests at once before any helper, which is not TDD, so I discarded those too. The plan now uses red-green-refactor cycles, one test at a time, with each helper its own numbered step (steps 2 to 4) and committed together with its tests and call-site changes.
- 2026-11-04: Rewrote step 3 again to use the issue's "small namedtuple" option. Building a plain-tuple key at each of the six `_update` calls still repeated the 11 values and their defaults six times. With a `_Mesh3Key` namedtuple, `_update` builds the key once and the prefetches use `mesh_key._replace(step=_ns)`, so the values and defaults appear once. I undid the uncommitted plain-tuple version of step 3 and started it again from this plan.
- 2026-11-04: Corrected two facts in the Analysis after re-checking `master`: the four status Div sites are the 3D kaleido, 3D patch, 2D patch and shared full-figure paths (I had named them wrongly), and the floor literal appears nine times, not five. Also added the type hints to `_log_transform`'s signature and marked steps 1 and 2 done.
- 2026-11-04: Rewrote step 3 to pass the key. My first version only replaced the two hand-built tuples (L350, L432) and left the 11-argument signatures, which met two of the issue's three sites and left most of the copy-paste hazard in place. The issue says to use `_mesh3_key` "at all three sites", including the `_update` calls at ~L1890, so `_prefetch_3d_mesh` and `_get_cached_3d_mesh` now take the key and `_update` builds it. `test_prefetch_then_lookup` is dropped, because with both functions taking the same key object it no longer checks anything the new tests do not. I undid the uncommitted step 3 code and started it again from this plan.
- 2026-11-02: In step 3, replaced `test_cache_lookup` (which only exercises the lookup side) with `test_prefetch_then_lookup`, which runs `_prefetch_3d_mesh` and then `_get_cached_3d_mesh`, so it covers both places that build the key.
- 2026-11-01: The issue calls the status Div "8-child"; the code has 7 children (6 `Span`s and one `Br`). Corrected in the Analysis.
- 2026-11-01: Added step 7 (push to my fork and check the CI lint-gate run for the `turbojpeg` import) so the risk below is checked, not just noted.
- 2026-11-01: Added step 5 (before/after comparison and a manual run of the interactive viewer) because unit tests cannot reach the closures inside `_update`. Nothing from it is committed.

**Toolkit**

- Tool: plan-check skill, run in Claude Code on `plan.md` and my draft `plan-comment.md` against issue #1518. It checked the plan against the live issue and the code, then graded five required checks (diagnosis, scope, executability, test-plan, comms) and read the comment against my voice guide. I re-ran it each time the plan changed, as its instructions say to.
- What it produced: `accept` on all five runs, with all five checks passing each time. The runs covered the TDD restructure, the added CI check, passing the key into `_prefetch_3d_mesh` and `_get_cached_3d_mesh`, and the final `_Mesh3Key` namedtuple version. Each time it re-checked my facts on `master` (4 status Divs with 7 children each, 9 `1e-300` literals, `_tf` at 379/386/1853/1861, the key built at 350/432, six `_update` calls, no `interactive` references in `test_viz.py`). The last run also listed four voice-guide breaks in my plan comment: too long for my "Be concise" rule, a redundant re-claim, a vague closing question, and no mention of the `_Mesh3Key` rename or the defaults being written once.
- Difficulties: My procedure expects a posted repro comment, and this refactor issue has none, so it graded the diagnosis on the issue body and its own live check; my procedure has no rule for that case. It also exposed that `procedure.md` calls the first check `root cause` while the rubric calls it `diagnosis`, and that the evidence guide's honesty section has no rubric check. Because it accepted every version, it did not catch that my first mesh key plan met only two of the issue's three sites; I found that by rereading the issue. One run happened on the wrong model, so I switched and re-ran.
- What changed: The plan changed between runs because of my own review, not because plan-check rejected anything. After the last run I rewrote the plan comment to six short sentences: I dropped the re-claim and the long cause paragraph, named both differences from the issue (the `_log_transform` arguments and the `_Mesh3Key` namedtuple with its defaults written once), and made the question say what it is about. It is still over my four-sentence target, because I kept the CI risk and the AI disclosure. I still need to fix the `root cause` and `diagnosis` naming in my procedure, and add a rule for issues with no repro.

---

## Testing Strategy

Two observable checks prove the fix, and both are recorded in my `test_evidence.md` with their output.

**1. The reproduction, before and after.** I re-ran the four greps from Reproduction Process on my branch (`5dfd5ba4`, steps 2 to 4 committed):

| Check | Before (master) | After (branch) |
|---|---|---|
| Status `html.Div` copies (`shape {raw.shape}`) | 4 copies (L1971, 2120, 2470, 2626) | 0 copies; `_status_div(...)` called at the 4 sites |
| `_tf` closures and the `1e-300` floor | `_tf` at L379/386/1853/1861, `1e-300` nine times | no `_tf`; `1e-300` only in `_LOG_FLOOR`; `_log_transform(...)` called at 3 sites |
| Hand-built mesh cache key | tuple at L350 and L432, 11 arguments at six `_update` calls | no tuples; one `_Mesh3Key` built in `_update` and passed to all six calls |
| Tests for `interactive.py` in `test_viz.py` | 0 | `TestLogTransform`, `TestMesh3Key`, `TestStatusDiv` |

**2. The repo's own checks** (the rows of my ship-gate manifest): `./mfc.sh precheck -j 4` passes all seven steps (formatting, spelling, ruff plus every toolchain unit test, source lint, doc references, parameter docs, example cases); `test_viz.py` gives 67 passed and 19 skipped (86 passed with the render tests); and `./mfc.sh test -j 12`, the full regression suite, is running (baseline on an older master, `e95a827a`: 726 passed, 0 failed, 39 skipped).

How the new tests were checked: each was written before its code, and all but one failed first for the expected reason. The exception, the any-field guard on `_Mesh3Key`, passed immediately, as the plan allowed. It and the `_prefetch_3d_mesh` range test, which guards the field order, were checked with a negative control: a deliberate temporary bug that the test caught.

Code the unit tests cannot reach: the changed lines inside `_update`, the Dash callback. For those I used three checks: an AST comparison showing every rewritten call gets exactly the key or values it got before; a script comparing `master` and the branch's prefetch caches on identical inputs (2D 36 of 36 and 3D 48 of 48 identical; a deliberately wrong key made 48 of 48 differ); and both viewers side by side on the 2D and 3D fixtures, which looked the same, with 0 errors and the same rate of prefetched-mesh hits during 3D playback (about 98%).

What these do not cover: the kaleido server-side render path and the prefetch call used when no single-variable reader is passed. Kaleido rendering fails on `master` and my branch alike (`to_image() got an unexpected keyword argument 'engine'`), and `./mfc.sh viz` always passes a reader, so no viewer run reaches them; only the AST checks cover those two sites.

**Toolkit**

- Tool: the ship-gate, through the project checks in my manifest that it runs before a PR opens: `./mfc.sh precheck -j 4`, the `test_viz.py` row and `./mfc.sh test -j 12`. I ran them on my branch first; what the gate itself says will be added when I run it.
- What it produced: precheck passes all seven steps, `test_viz.py` gives 67 passed and 19 skipped, and the full regression suite is running (baseline on an older master: 726 passed, 0 failed, 39 skipped). The before and after output the gate's pr-precheck will read is in my `test_evidence.md`.
- Difficulties: The manifest's checks cannot reach the changed calls inside `_update`, because no unit test can, so those needed checks the gate does not run: an AST comparison, a master-vs-branch cache comparison and a side-by-side viewer run. One test run put `MFC_SKIP_RENDER_TESTS=1` in front of `cd` instead of `python`, so the render tests ran and the counts looked wrong (79 passed instead of 60 passed and 19 skipped). `./mfc.sh test` takes about an hour, so every gate run will too, and my baseline is from an older master.
- What changed: The skip variable now goes directly before the `python` command. I recorded the extra checks, and the two sites nothing could reach, in `test_evidence.md` so the gate and a reviewer can see them, and gave a negative control to any test that passed without failing first.

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-11-01**

Before writing code I checked that the new tests can import `interactive.py`. They couldn't: `import mfc.viz.interactive` raised `RuntimeError: Unable to locate turbojpeg library`. The module's `except (ImportError, OSError)` around `TurboJPEG()` doesn't catch that error type, so the Pillow fallback never runs. Neither the contributing guide, the setup docs nor `pyproject.toml` tells contributors to install the native library, so I treated it as a local workaround, not a project change. I installed it with `sudo apt install libturbojpeg0` (the package named `libturbojpeg` doesn't exist on Ubuntu), added it to the setup line in Reproduction Process, and confirmed the import now works with `_tj` loaded. I'm not changing the `except` in this PR, since it is outside the plan; I'll mention it in the plan comment and watch whether CI has the same problem.

**2026-11-01 (later)**

Re-read my claim comment on the issue and saw it promised tests first, but my plan had them last. I rolled the branch back to `a03848a0` (upstream `master`, unchanged since my baseline). I then wrote all three test classes at once before any helper existed (7 failed with `AttributeError`, 1 passed), but that is not TDD: TDD adds one failing test, makes it pass, and only then adds the next. I discarded those tests (nothing was committed) and rewrote the plan as one-test-at-a-time cycles. Each helper will be committed with its tests, because the pre-commit hook runs the unit tests and rejects a failing commit. Mistake caught along the way: a Python one-liner Claude Code ran truncated `plan.md` by opening it for writing before reading it; I restored it from this story's Solution Approach, which holds an identical copy.

**2026-11-01 (step 2: `_log_transform` and `_LOG_FLOOR`)**

Built `_log_transform` in three red-green cycles, one test at a time: log values with NaN for non-positive input, then the identity branch for `log=False`, then the `_LOG_FLOOR` clamp. Each test failed for the expected reason before any code existed. The refactor replaced the four `_tf` closures and their `cmin`/`cmax` lines, plus the 2D JPEG path's inline log, which the issue does not list. Because that 2D site was my own addition, I checked it by running `master` and my branch on the same 56 inputs and comparing the arrays passed to the image encoder, with a deliberately broken floor as a control (20 of 56 then differed). Review changes: I moved `_LOG_FLOOR` from the middle of the file to the top constants block where the file keeps its other numbers, added the `log: bool` type hints the issue's signature shows, and renamed the tests (for example `test_log_true_clamps_zero_vmin_to_floor`) so their names say what they check. Claude Code had committed for me with long messages; I undid that so I review and make every commit myself, with one-line messages. Committed as `46ce57ab`.

**2026-11-02 (step 3, first attempt)**

My first `_mesh3_key` version only replaced the two hand-built key tuples (L350, L432) with a helper call, plus a round-trip test that prefetches a mesh and looks it up. The six `_update` calls still passed the same 11 arguments each. I did not commit it.

**2026-11-04 (step 3, redesign)**

I asked whether the round-trip test was really needed, and then whether `_prefetch_3d_mesh` should take a key instead of 11 separate arguments. Rereading the issue ("use it at all three sites", "passed positionally from `_update` at ~1890", "or a small namedtuple"), I decided the key should be built by the caller and passed in. A plain-tuple version still listed the 11 values and their defaults at all six calls, so I switched to a `_Mesh3Key` `typing.NamedTuple` that `_update` builds once; the prefetches use `mesh_key._replace(step=_ns)` for the next step. I checked that none of the 11 inputs change after `log` is resolved, so building the key there is safe, and that `_replace` returns a new key instead of changing the one the lookups use. Each redesign went through `plan.md`, this story and the plan comment together, with plan-check re-run (accept each time). TDD: field order and the any-field guard, then `_get_cached_3d_mesh(key)` and `_prefetch_3d_mesh(key, get_ad_fn)` each failed while they still took 11 arguments. The prefetch test checks the stored volume range, so a swapped unpack would fail it (confirmed with a control). The six `_update` calls have no unit tests, so the refactor was done from the parsed code and checked with the AST: each call gets exactly the key it got before. Committed as `0c3b9c10`.

**2026-11-04 (step 4: `_status_div`)**

Two red-green cycles: the Div's children, text and colors, then the `.4g` number format (the first version printed raw numbers until the second test asked for `.4g`). Before replacing the four copies in `_update`, I checked with the AST that each one is exactly the helper's body with its own variables; all four were, differing only in the min/max names. Claude Code's first refactor script read the wrong part of each `html.Span` and matched nothing, but its "exactly four" check stopped it before it wrote anything. `test_viz.py` is now 1,018 lines, over the 1,000-line soft limit, which I still need to decide on. Committed as `5dfd5ba4`.

**2026-11-04 to 2026-11-05 (step 5: before/after checks)**

A throwaway script ran `master` and my branch on the same inputs and compared their prefetch caches: 36 of 36 2D cases and 48 of 48 3D cases identical, and a deliberately wrong key made all 48 3D cases differ. Then I ran both viewers side by side on the 2D and 3D fixtures; they looked the same, and their logs showed the same rate of prefetched-mesh hits during 3D playback (about 98%). Two changed sites cannot be reached from the viewer here: kaleido rendering fails on both versions (`to_image() got an unexpected keyword argument 'engine'`, an existing plotly/kaleido mismatch unrelated to this change), and one prefetch call only runs when no single-variable reader is passed. The AST checks from steps 3 and 4 cover both.

**2026-11-05 (step 6: manifest checks)**

`./mfc.sh precheck` passes all seven steps and `test_viz.py` passes (67 passed, 19 skipped). The four reproduction greps now show each duplication gone and the new tests present. The full regression suite (`./mfc.sh test -j 12`, about an hour) is running; my baseline was on an older `master`, so if a test fails I will rerun it on the branch's base before deciding whether it is related.

**Toolkit**

- Tool: plan-check, re-run during the build each time my plan changed, as its instructions say to do after a deviation.
- What it produced: `accept` on each re-run: after I changed step 3 to pass the key into `_prefetch_3d_mesh` and `_get_cached_3d_mesh`, and after I switched to the `_Mesh3Key` namedtuple built once in `_update`. Each time it re-checked the new claims against master, including the six `_update` calls and that none of the key's inputs change after `log` is resolved.
- Difficulties: It grades the plan, not the code, so it could not tell me whether what I built matched the plan; the tests and AST checks did that. It also accepted every version, including my first step 3 that met only two of the issue's three sites, so the redesigns came from my own rereading of the issue, not from its feedback.
- What changed: At each change I updated `plan.md`, the Implementation Plan and the Deviations list together before re-running it, so it graded what I was actually going to build, and I abandoned and redid uncommitted step 3 code instead of letting it drift from the plan.

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
