# Salvage worktree isolation
---
## Why worktrees
Git worktrees give multiple working directories sharing one object store.
| Isolated per worktree | Shared (dangerous if concurrent write) |
| --- | --- |
| HEAD, index, reflog, MERGE_HEAD | objects, refs/heads, config, hooks |
| File checkout | `git gc`, `git fetch` side effects |
Worktrees prevent branch-level checkout conflicts. They do **not** make git operations thread-safe.
---
## Salvage pattern (recommended)
```
repo/
  .git/ # or bare clone hub
  main/ # human checkout — agent does not write here
  salvage/<run-id>/ # agent worktree on branch salvage/<run-id>
```
### Create
```bash
# from main checkout or bare hub
git fetch origin
git worktree add -b salvage/$(date -u +%Y%m%dT%H%MZ) \
  ../salvage-run-$(date -u +%Y%m%dT%H%MZ) origin/main
cd ../salvage-run-...
```
### Agent rules
1. **cwd is the worktree.** All git/file ops run with explicit worktree path.
2. **Writers do not push to main.** Agent commits on `salvage/*` only.
3. **Commit is the barrier.** No merge until `git status` is clean *and* commit exists.
4. **Archive before clean.** `rsync -a --checksum` dirty paths into `versioning/salvage/` inside the worktree first.
5. **One branch per worktree.** Git enforces this.
6. **Sequential git writes.** Never parallel `git commit` / `git rebase` across worktrees sharing the same repo.
### Safe remove
```bash
# only if: no unpushed commits OR commits already on remote
git worktree list
git log origin/salvage/... ^origin/main # check unpushed
git worktree remove <path> # clean trees only
# if dirty or unpushed:
git worktree remove --force <path> # ONLY after archive + push confirmed
git worktree prune
```
**Hard rule:** never force-remove if unpushed commits exist and archive failed.
### Integrator role (optional multi-agent)
| Role | Does |
| --- | --- |
| Writer | edits + tests in worktree; does not merge |
| Integrator | commits in worktree, merges to salvage branch, pushes, prunes |
| Orchestrator | enforces order: writer done → commit barrier → merge → cleanup |
---
## Anti-patterns
| Avoid | Why |
| --- | --- |
| Agent writing in main checkout | clobber human WIP |
| Parallel git write ops on shared repo | index/ref corruption risk |
| `git worktree remove --force` before archive | data loss |
| Same branch in two worktrees | git refuses; conflicts |
| Long-lived salvage worktrees without sync | drift; hard merges |
---
## Bare hub layout (optional scale)
```
~/worktrees/grok-morph-skills/
  .bare/
  main/
  salvage-20260814T1700Z/
```
```bash
git clone --bare git@github.com:Jadon-Fox/grok-morph-skills.git .bare
git worktree add main main
git worktree add -b salvage/... salvage-... main
```
