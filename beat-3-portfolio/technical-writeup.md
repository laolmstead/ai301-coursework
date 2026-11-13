# Removing Duplicate Code in MFC's Visualizer and Fixing the CI Failure It Exposed

## Overview
As part of CodePath's AI Capstone course, I made my first open source contribution to MFC, a computational fluid dynamics simulation tool. I chose it because I wanted to contribute to a repo in physical engineering or the hard sciences, and MFC fit that. The issue ([#1518](https://github.com/MFlowCode/MFC/issues/1518)) asked for a refactor of `toolchain/mfc/viz/interactive.py`: three pieces of logic were copy-pasted in several places and needed to move into helper functions, with the file's first unit tests added to verify the behavior. I wrote the three helpers test-first, and when CI failed on my first push I found and fixed a second, unrelated bug that was blocking the tests from running. My PR is open and CI is passing, but no maintainer has reviewed it yet.

PR: https://github.com/MFlowCode/MFC/pull/2170

## What happened
The first thing I did after choosing the issue was follow the setup instructions and get the repository running locally. I was missing several required libraries, including a Fortran runtime. After some trial and error I completed the setup and ran the existing tests for a baseline.

Since my issue was a refactor rather than a bug, I first had to confirm the duplication still existed. I searched the codebase and found all three duplicates as the issue described: the status `html.Div` block, the log-transform closure with its hardcoded `1e-300` floor, and the 11-value 3D mesh cache key.

I refactored one duplicate at a time using TDD, write one test, watch it fail for the expected reason, write the least code to pass it, then refactor. My first plan actually put the tests last, which contradicted the comment I had posted on the issue saying I would write tests first. I rolled back my one code commit and rewrote the plan around red-green cycles. Later I also revised my plan to use a `_Mesh3Key` named tuple instead of a plain tuple mesh cache key, because the tuple version still repeated the 11 values at six call sites. Refactoring this allowed my to cleanly pass the key around and only exposing the 11 values as needed.

After everything passed locally, I opened the PR. CI ran and failed with all nine of my new tests erroring out with `RuntimeError: Unable to locate turbojpeg library`. One CI runner didn't have the native `libturbojpeg` library installed. The repo already had an import guard around `TurboJPEG()` that fell back to Pillow, but it only caught `ImportError` and `OSError`. The current PyTurboJPEG raises `RuntimeError`, so the guard never ran and `interactive.py` couldn't even be imported.

**The fix.** I added `RuntimeError` to the guard and updated the comment above it:

```diff
-# is not in LD_LIBRARY_PATH it raises OSError even if the pip package is
-# installed. Fall back to Pillow in that case.
+# is not in LD_LIBRARY_PATH it raises OSError (RuntimeError in current
+# PyTurboJPEG) even if the pip package is installed. Fall back to Pillow in
+# that case.
 try:
     from turbojpeg import TurboJPEG as _TurboJPEG  # type: ignore[import]

     _tj = _TurboJPEG()
-except (ImportError, OSError):
+except (ImportError, OSError, RuntimeError):
     _tj = None
```

**The test that backs it.** I wrote this regression test first, so it failed until the guard was changed. It reloads the module with `TurboJPEG()` raising the same error CI saw and checks that the Pillow fallback is used:

```python
class TestTurboJPEGFallback(unittest.TestCase):
    def test_missing_native_library_falls_back_to_pillow(self):
        import importlib
        from unittest import mock

        from . import interactive as m

        self.addCleanup(importlib.reload, m)
        with mock.patch("turbojpeg.TurboJPEG", side_effect=RuntimeError("Unable to locate turbojpeg library")):
            importlib.reload(m)
        self.assertIsNone(m._tj)
```

This was a change I made to my own work because of a failed run. My original PR only touched the three refactors, and the CI failure showed it needed this extra fix to be testable at all. Since the issue didn't ask for it, I explained it in a PR comment and offered to move it to a separate PR if the maintainers preferred:

> "CI failed on the new tests because interactive.py can't be imported on runners without the native libturbojpeg. This PyTurboJPEG version raises RuntimeError, but the existing import guard was only excepting ImportError and OSError. I added RuntimeError to that except, with a test, so the module falls back to Pillow as its comment says. If you'd prefer a different fix or want this change moved to a different PR, please let me know and I'd be happy to adjust as needed."

**What landed.** After I pushed the fix, CI passed and Codecov reported that all modified lines were covered by tests. No maintainer has reviewed or merged the PR yet, so that passing CI run is the result so far.

## Limitations and what's next
My PR is still open and awaiting review, so I don't know yet whether the maintainers will accept it or want changes. In particular, the turbojpeg fix goes beyond what the issue asked for, so they may ask me to split it into its own PR. I offered that in my comment and would do it.

Also, `interactive.py` is still largely procedural. It could be improved by restructuring it with OOP principles, but that isn't what the maintainers asked for, so I kept my scope small. Refactoring it in small, testable pieces is more manageable anyway, and I agree with that approach.

Next, I'll respond to any review feedback promptly. If the PR is merged, I'd like to keep contributing to this repo and take on more complex issues. With my Civil Engineering background, I'd also like to contribute to other technical repos where my unique skillset could be an asset.
