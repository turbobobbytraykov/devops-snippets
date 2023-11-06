**Potential use**: If you want to create a branch for changes to an Azure DevOps yml pipeline, but you want to target/work with the state of the code in another ref (branch/tag/commit).

In Azure DevOps at the time of writing this, you cannot reliably overwrite the "self" repository (either as checkout or resources.repositories.repository) to point to a different ref (branch/tag/commit) than the current one.
By default, you have:
1. Self repo checked out with the latest commit of the branch
2. Self repo is checked out in detached HEAD state, so you cannot just checkout a different ref

So the solution is in 2 steps:
3. checkout self
4. re-attach the local copy of the git repo to the remote, sync it and checkout the ref you need.

These steps **DO NOT** affect the code of the pipeline as it is already evaluated & being executed.
**NB**: More complex scenarios may have "gotcha" situations - test & be vigilant! 