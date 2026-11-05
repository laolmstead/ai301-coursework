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

- Tool:
- What it produced:
- Difficulties:
- What changed:

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

1. Status `html.Div` ("step N", "· shape ...", `Br`, min, max): the same 7-child block inside `_update` at four sites (ends of the 1D/2D, 3D patch, 3D full-figure and slice paths, ~L1971, 2120, 2470, 2626). Only the local names for min/max differ.
2. Log/identity transform: `_tf(arr)` is defined as a closure twice in `_prefetch_3d_mesh` (~L379/386) and twice in `_update` (~L1853/1861), each beside an inline `cmin`/`cmax = log10(max(v, 1e-300))`. The `1e-300` floor is also inlined in the 2D path (~L302-304). The floor is a bare literal in five places.
3. Mesh cache key: the 11-field tuple `(step, var, mode, log_bool, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac)` is built by hand in `_prefetch_3d_mesh` (L350) and `_get_cached_3d_mesh` (L432). These two must produce identical keys or prefetched meshes are never found. `_update` only passes the same values as positional arguments (~L1774, 1806, 1890, 2025, 2075, 2142); it does not build the tuple itself.
4. No test in `toolchain/mfc/viz/test_viz.py` imports `interactive.py`.

**Proposed Solution**

Extract each piece into one module-level helper in `interactive.py` and call it from every existing site. Behavior stays identical.

- `_LOG_FLOOR = 1e-300`, a module constant that replaces every inline literal.
- `_status_div(step, shape, dmin, dmax) -> html.Div`, called at the four sites.
- `_log_transform(log, vmin, vmax) -> (tf, cmin, cmax)`. The issue writes `_log_transform(log)`, but it also asks for the cmin/cmax pair, which needs vmin/vmax, so I take them as arguments. It replaces the four `_tf` closures and their adjacent cmin/cmax lines; the 2D path (~L302-304) computes the same values, so it uses it too.
- `_mesh3_key(step, var, mode, log, vmin_in, vmax_in, iso_min_frac, iso_max_frac, iso_n, vol_min_frac, vol_max_frac) -> tuple`, used where the key is built (L350, L432).
- Add `TestStatusDiv`, `TestLogTransform` and `TestMesh3Key` to `toolchain/mfc/viz/test_viz.py`, the first tests for `interactive.py`. Keep them short, since the file is at 917 lines and the soft limit is 1000.

Not changing:
- Signatures of `_prefetch_3d_mesh` and `_get_cached_3d_mesh`. The issue's third site (~L1890) is a call that passes arguments to one of these, not a tuple literal. Changing the signatures would touch every call in `_update` and is a public-signature change.
- The repeated `float(iso_min_frac or 0.2)`-style defaults at the `_update` call sites.
- Callback control flow, `_update`'s structure, `turbojpeg` handling, any other file, and any rendered output.

**Implementation Plan**

1. Branch `feature/viz-interactive-dedup` from the synced upstream `master` (done; it sits at `a03848a0`).
2. Extract `_log_transform` and `_LOG_FLOOR`, using TDD. Each cycle is: write one test in `test_viz.py` (`TestLogTransform`), run it and confirm it fails for the expected reason (red), write the least code in `interactive.py` that makes it pass (green), tidy, and re-run the suite before the next test.
   1. Test: `log=True` returns the log10 transform (NaN for non-positive input) with `cmin`/`cmax`. Then add `_log_transform` to pass it.
   2. Test: `log=False` returns the input unchanged with `vmin`/`vmax`. Then add the identity branch.
   3. Test: `vmin=0` clamps to the `_LOG_FLOOR` constant. Then add `_LOG_FLOOR` and use it in the helper.
   4. Refactor: replace the four `_tf` closures, their adjacent cmin/cmax lines, and the 2D-path floor literals with `_log_transform`; the existing viz tests must still pass.
   5. Commit the helper, its call-site changes and its tests as one commit.
3. Extract `_mesh3_key`, using TDD with the same cycle (`TestMesh3Key`).
   1. Test: `test_prefetch_then_lookup` runs `_prefetch_3d_mesh` on a tiny fake 3D array, waits for it to finish, and checks that `_get_cached_3d_mesh` finds the result with the same 11 arguments, so both places that build the key are shown to agree. It passes before any change, so it pins current behavior.
   2. Test: `_mesh3_key` returns the 11 fields in order. Then add `_mesh3_key` to pass it.
   3. Test: changing any one field changes the key. It may already pass, in which case it stays as a guard.
   4. Refactor: use `_mesh3_key` in `_prefetch_3d_mesh` and `_get_cached_3d_mesh`; the existing viz tests must still pass.
   5. Commit the helper, its call-site changes and its tests as one commit.
4. Extract `_status_div`, using TDD with the same cycle (`TestStatusDiv`).
   1. Test: the children, text and colors for simple values. Then add `_status_div` to pass it.
   2. Test: numbers use the `.4g` format. Then change the formatting to pass it.
   3. Refactor: replace the four copies in `_update` with `_status_div`; the existing viz tests must still pass.
   4. Commit the helper, its call-site changes and its tests as one commit.
5. Beyond the unit tests, which cannot reach the closures inside `_update` (nothing is committed for these): (a) run a throwaway script on `master` and on the branch that calls `_prefetch_jpeg` and `_prefetch_3d_mesh` with a fake data loader, in log and non-log mode, and compare `_jpeg_cache` and `_mesh3_cache`; (b) launch `./mfc.sh viz <fixture> --interactive` on the 2D and 3D fixtures before and after and compare the status line, color bar and log toggle. Save the output in `test_evidence.md`.
6. Run the manifest checks: `./mfc.sh precheck -j 4`, `test_viz.py`, and `./mfc.sh test -j 12` (baseline on master: 726 passed, 0 failed, 39 skipped).
7. Push the branch to my fork and check that the lint-gate CI run there can import `interactive.py` (the `turbojpeg` risk below). If it cannot, handle it before opening the PR.
8. Open the PR from my fork, using the PR template, with `Fixes #1518`, and state that AI assistance was used.

Tests come first because my claim comment on the issue says I would write the tests first and implement against them, and the issue asks for tests that make the dedup verifiable. Each helper is committed with its tests because the pre-commit hook runs the unit tests and would reject a commit with a failing test.

Risk: `interactive.py` raises at import where `libturbojpeg` is missing (the `except` catches `ImportError`/`OSError`, but this `turbojpeg` raises `RuntimeError`), so the new tests need that library installed locally. If CI also lacks it, the tests would fail there; I'll check the first CI run and handle it in the PR rather than widening scope silently.

Deviations from this plan:

- 2026-11-01: My first draft put the tests last, which contradicted my claim comment on the issue ("I'll start by writing the unit tests ... then implement the fix against them"). I rolled back the one code commit I had made. My second draft wrote all the tests at once before any helper, which is not TDD, so I discarded those too. The plan now uses red-green-refactor cycles, one test at a time, with each helper its own numbered step (steps 2 to 4) and committed together with its tests and call-site changes.
- 2026-11-02: In step 3, replaced `test_cache_lookup` (which only exercises the lookup side) with `test_prefetch_then_lookup`, which runs `_prefetch_3d_mesh` and then `_get_cached_3d_mesh`, so it covers both places that build the key.
- 2026-11-01: The issue calls the status Div "8-child"; the code has 7 children (6 `Span`s and one `Br`). Corrected in the Analysis.
- 2026-11-01: Added step 7 (push to my fork and check the CI lint-gate run for the `turbojpeg` import) so the risk below is checked, not just noted.
- 2026-11-01: Added step 5 (before/after comparison and a manual run of the interactive viewer) because unit tests cannot reach the closures inside `_update`. Nothing from it is committed.

**Toolkit**

- Tool: plan-check skill, run in Claude Code on `plan.md` and my draft `plan-comment.md` against issue #1518. It checked the plan against the live issue and the code, then graded five required checks (diagnosis, scope, executability, test-plan, comms) and read the comment against my voice guide.
- What it produced: `accept` on the first run, with all five checks passing. It re-grepped `interactive.py` and confirmed my line numbers (4 status Divs, `_tf` at 379/386/1853/1861, the key at 350/432, no `interactive` references in `test_viz.py`). It also noted that my plan comment breaks my own "Be concise" rule and repeats my claim.
- Difficulties: My procedure expects a posted repro comment on the issue, and I never posted one (my reproduction lives in this story), so it graded the diagnosis on the plan's own citations plus its live check. It also exposed that `procedure.md` calls the first check `root cause` while the rubric calls it `diagnosis`, and that the evidence guide's honesty section has no rubric check. The JSON it printed had a typo in a key name, which I caught on reading it.
- What changed: The verdict did not require any change to `plan.md`. I still need to shorten the plan comment to fit my concision rule before posting it, consider adding a line to the test plan that re-runs my four grep reproduction steps, and fix the `root cause` and `diagnosis` naming in my procedure.

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

**2026-11-01**

Before writing code I checked that the new tests can import `interactive.py`. They couldn't: `import mfc.viz.interactive` raised `RuntimeError: Unable to locate turbojpeg library`. The module's `except (ImportError, OSError)` around `TurboJPEG()` doesn't catch that error type, so the Pillow fallback never runs. Neither the contributing guide, the setup docs nor `pyproject.toml` tells contributors to install the native library, so I treated it as a local workaround, not a project change. I installed it with `sudo apt install libturbojpeg0` (the package named `libturbojpeg` doesn't exist on Ubuntu), added it to the setup line in Reproduction Process, and confirmed the import now works with `_tj` loaded. I'm not changing the `except` in this PR, since it is outside the plan; I'll mention it in the plan comment and watch whether CI has the same problem.

**2026-11-01 (later)**

Re-read my claim comment on the issue and saw it promised tests first, but my plan had them last. I rolled the branch back to `a03848a0` (upstream `master`, unchanged since my baseline). I then wrote all three test classes at once before any helper existed (7 failed with `AttributeError`, 1 passed), but that is not TDD: TDD adds one failing test, makes it pass, and only then adds the next. I discarded those tests (nothing was committed) and rewrote the plan as one-test-at-a-time cycles. Each helper will be committed with its tests, because the pre-commit hook runs the unit tests and rejects a failing commit. Mistake caught along the way: a Python one-liner of mine truncated `plan.md` by opening it for writing before reading it; I restored it from this story's Solution Approach, which holds an identical copy.

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
