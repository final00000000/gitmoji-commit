# Git Status Matrix

Use this file when repository state is not a simple "edit -> stage -> commit" flow.

## Common states

### Clean working tree

- `git status --short` returns nothing
- Action: report there is nothing to commit

### Untracked files only

- status contains only `??`
- Action: review whether files are intentional before staging

### Unstaged changes only

- status contains ` M`, ` D`, etc. with no staged entries
- Action: inspect `git diff`, then stage explicit files

### Staged changes only

- status contains `M `, `A `, etc. with no unstaged entries
- Action: inspect `git diff --staged`, then commit staged contents

### Mixed staged and unstaged changes

- both columns in `git status --short` are populated
- Action: inspect both staged and unstaged diff; avoid committing unrelated unstaged work

### Detached HEAD

- `git branch --show-current` is empty
- Action: do not push automatically

### Merge in progress

- `.git/MERGE_HEAD` exists
- Action: treat as merge completion, not a normal isolated commit flow

### Cherry-pick in progress

- `.git/CHERRY_PICK_HEAD` exists
- Action: treat as cherry-pick completion, not a fresh commit flow

### Rebase in progress

- `.git/rebase-merge` or `.git/rebase-apply` exists
- Action: resolve any conflicts, stage resolved files, then use `git rebase --continue`

### Unmerged paths / conflicts

- `git diff --name-only --diff-filter=U` returns files
- `git status --short` may show `UU`, `AA`, `DD`, etc.
- Action: do not create a normal commit until conflicts are resolved

### Initial commit

- `git rev-parse --verify HEAD` fails
- Action: verify intended bootstrap files only; do not assume amend/revert flows

### Ahead / behind / diverged

Check:

```bash
git rev-list --left-right --count @{upstream}...HEAD
```

Interpretation:

- `0 N` -> ahead
- `N 0` -> behind
- `N M` -> diverged

Recommended behavior:

- ahead -> push is usually safe if requested
- behind -> warn before push
- diverged -> do not push blindly

### Push rejected / protected branch

- remote rejects push because of branch protection, permissions, or remote updates
- Action: surface the exact error; do not force push; recommend PR, sync, or permission fix
