I opened my first open source contribution, a refactor for MFC, a free fluid dynamics simulation tool used by engineers and researchers. Several pieces of logic were copy/pasted and duplicated throughout its visualizer, which makes it easy for a future change to be missed in one place, potentially resulting in unexpected bugs.

I moved the repeated code into shared functions and wrote the first tests for that part of the program. When my tests ran on the project's servers, they exposed a separate hidden bug. The program crashed on servers missing an optional software library instead of switching to its backup. I fixed that too, and the checks now pass.

The change is waiting for the maintainers' review, so it isn't merged yet. It was exciting to learn about contributing to open source and the etiquette involved in interacting with maintainers. Additionally, my previous degree was in Civil Engineering so it was interesting to contribute to software that might be used by fellow engineers. My goal is to make this a habit and keep contributing to this and other software tools for engineers.

https://github.com/MFlowCode/MFC/pull/2170.