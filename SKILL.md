---
name: gitmoji-commit
description: Create portable git commits, PRs, and release flows with gitmoji + Conventional Commit by default, falling back to plain Conventional Commit only when the user explicitly asks or encoding is unsafe. Use when the user asks to commit with icons, gitmoji, prettier history, avoid AI co-author attribution, work across multiple AI CLIs, or manage GitHub, GitLab, Azure DevOps, Gitea/Forgejo, Codeberg, and Bitbucket workflows. Supports full-catalog gitmoji selection, safe staging, mixed-state handling, cross-host CLI workflows, rebase/conflict recovery, initial-commit handling, amend/revert guidance, and ASCII-safe defaults.
license: MIT
allowed-tools: Bash
---

# gitmoji-commit

**Mental model**

- Default: gitmoji + Conventional Commit titles such as `✨ feat(scope): summary`
- If the user explicitly asks for no emoji / ASCII-only: fall back to plain Conventional Commit titles such as `feat(scope): summary`
- If shell / host / encoding safety is uncertain: fall back to ASCII-only Conventional Commit output
- Keep the chosen style consistent across commit titles and PR titles unless the user explicitly wants a different style

Create clean Git commits using **gitmoji + Conventional Commits by default** with **ASCII-safe fallback when needed** while keeping Git operations safe, scoped, and predictable.

When the user invokes this skill for commit-related work, default to `gitmoji + Conventional Commit`. Use `references/gitmoji-map.md` to choose the most suitable emoji, and only disable emoji when the user explicitly asks or the environment is unsafe for UTF-8.

## Core contract

Primary validated path:
- local git workflows
- GitHub operations through `gh` when installed and authenticated

Guidance-only paths until explicitly validated:
- GitLab via `glab`
- Azure DevOps via `az repos`
- Gitea / Forgejo / Codeberg via `tea`
- Bitbucket via git + web/API fallback

The default responsibility of this skill is to:
1. inspect repository state
2. stage only the intended files
3. propose or create a safe gitmoji + Conventional Commit
4. fall back to plain Conventional Commit only when the user explicitly asks for no emoji or the environment is unsafe for UTF-8

PR / release / multi-host flows are extended workflows layered on top of that commit-first behavior.

For maximum compatibility, treat this as a **portable workflow spec**:

- the core contract lives in `SKILL.md` + `references/*`
- `agents/openai.yaml` is optional UI metadata for one runtime only
- other AI tools can ignore `agents/` and still use the workflow

## When to use

Use this skill when the user:

- asks to "commit with icon", "emoji commit", "gitmoji", or "提交带图标"
- wants prettier GitHub commit history
- wants to avoid AI attribution or co-author trailers in commits / PRs / releases
- wants one workflow that can be reused across different AI agents / AI CLIs
- wants to choose Chinese or English for commit / PR / release text
- wants a commit message generated from current changes
- wants help staging one logical change safely
- wants to commit and optionally push the current branch
- wants to open a PR with `gh`
- wants to create a GitHub Release, upload assets, or publish a full changelog with `gh`
- wants similar flows for GitLab / Azure DevOps / Gitea / Forgejo / Codeberg / Bitbucket
- wants help with amend / revert / hook-failure commit recovery

Do **not** use this skill when the user only wants:

- a diff review with no commit
- a pure prose article unrelated to the repo's Git/GitHub workflow
- destructive history rewrites

## Safety rules

- Never commit secrets, tokens, `.env` files, private keys, or credentials.
- Never change git config.
- Never use `--no-verify` unless the user explicitly asks.
- Never use destructive commands such as `git reset --hard`, force push, or history rewrite unless explicitly requested.
- Never force push to `main` / `master`.
- If unrelated files are modified, stage only the files relevant to the requested change.
- Do not use `git add .` or `git commit -a` blindly when the tree contains mixed or unrelated work.
- Never add AI attribution or co-author trailers such as `Co-authored-by`, `Generated-by`, or `AI-assisted` unless the user explicitly requests them.
- If any wrapper/tool exposes `includeCoAuthoredBy`, keep it disabled / false unless the user explicitly requests co-author trailers.
- Always inspect `git status --short` before staging.
- Always inspect `git diff --staged` if files are staged; otherwise inspect `git diff`.
- Always check for unresolved conflicts before committing.
- If push is requested, check branch/upstream state first; push normally only when safe.
- Use `gh` only when installed and authenticated.
- Default to gitmoji + Conventional Commit titles when generating commit / PR / release text.
- Always consult `references/gitmoji-map.md` as the canonical full catalog for emoji selection.
- Fall back to plain ASCII Conventional Commit output on unknown terminals, unknown AI CLIs, unknown host encodings, or whenever the user explicitly asks for ASCII-only / no-emoji text.

## Standard fallback policy

When uncertain, downgrade rather than improvise:

1. Unknown or unsafe encoding -> ASCII-only Conventional Commit output
2. Missing host-specific CLI or failed auth -> stop host automation and provide ready-to-paste title/body/notes instead
3. Merge / rebase / cherry-pick / conflict state -> stop the normal commit flow and explain the next safe step
4. Mixed or unclear language convention -> use English ASCII by default or provide bilingual suggestions
5. If emoji or non-ASCII output garbles once -> revert to ASCII-safe no-emoji output for the rest of the task/session


## AI attribution policy

Default posture: **no AI attribution**.

- Keep Git author metadata as the user's existing Git identity.
- Do not append `Co-authored-by` for AI tools.
- Do not add `Generated-by`, `AI-assisted`, or similar banners to commit messages, PR bodies, or release notes unless explicitly requested.
- If a human co-author is real and requested, add that human only.
- If a tool has an `includeCoAuthoredBy` option, treat the safe default as `false`.

## Portability and encoding rules

Default mode: **gitmoji + Conventional Commit when UTF-8 is safe**.

- Generate gitmoji + Conventional Commit titles by default.
- Use `references/gitmoji-map.md` to select the most specific matching emoji.
- If the user explicitly asks for no emoji / ASCII-only output, switch to plain Conventional Commit.
- If encoding safety is uncertain, fall back to English ASCII Conventional Commit output.
- If mojibake or garbled text appears once, immediately fall back to ASCII-only titles and notes.
- Prefer plain Markdown and explicit CLI arguments over tool-specific hidden options.
- Use shell-appropriate file-writing commands; do not assume Bash heredocs in PowerShell environments.

## Language selection rules

Commit, PR, and release text can be written in either:

- `en` -> English
- `zh` -> Chinese

Selection order:

1. explicit user choice wins
2. otherwise inspect recent commit history and follow the dominant repo convention
3. if the repo is mixed or unclear, provide both Chinese and English suggestions, or ask the user if interaction is appropriate
4. if encoding safety is uncertain, use English ASCII even if Chinese would otherwise be acceptable

Language scope:

- keep one commit in one primary language
- keep PR title/body and release title/notes aligned with the selected language unless the user explicitly wants bilingual output
- if bilingual output is requested, prefer:
  - title in one primary language
  - body / notes with separate `ZH` and `EN` sections

## CLI and host confidence

Primary validated workflow:
- `git` CLI for local repository inspection, staging, and commits
- `gh` for GitHub PR / release flows when installed and authenticated

Guidance-only workflows until explicitly validated:
- `glab` for GitLab
- `az repos` for Azure DevOps
- `tea` for Gitea / Forgejo / Codeberg when host support is confirmed
- Bitbucket via `git` + REST API / web fallback

Shell examples in this file are primarily POSIX / Bash-flavored unless otherwise noted. On Windows or mixed-shell environments, use `references/portable-shell-encoding.md` for the safe default behavior.

Quick checks:

```bash
git --version
gh --version
gh auth status
git remote get-url origin
```

Use `references/platform-host-matrix.md` to select the right host workflow.
Use `references/portable-shell-encoding.md` to avoid garbled output and shell incompatibilities.

## Core inspection workflow

Run these checks first:

```bash
git status --short
git branch --show-current
git rev-parse --verify HEAD >/dev/null 2>&1 || echo INITIAL_COMMIT
git rev-parse --abbrev-ref --symbolic-full-name @{upstream} 2>/dev/null || true
test -f .git/MERGE_HEAD && echo MERGE_IN_PROGRESS || true
test -f .git/CHERRY_PICK_HEAD && echo CHERRY_PICK_IN_PROGRESS || true
test -d .git/rebase-merge -o -d .git/rebase-apply && echo REBASE_IN_PROGRESS || true
git diff --name-only --diff-filter=U
```

Then inspect the diff:

```bash
# If files are already staged
git diff --staged

# Otherwise
git diff
```

If the user also wants GitHub operations, check:

```bash
gh auth status
git remote -v
git tag --sort=-version:refname | head -n 5
```

If the host is not GitHub, identify it from the remote URL first and switch to the matching host workflow reference.

Use `references/git-status-matrix.md` when the repository state is mixed or unusual.
Use `references/gh-pr-release-flow.md` when the user wants PRs, Releases, assets, or full changelog publishing.
Use `references/platform-host-matrix.md` when the remote is not GitHub.
Use `references/portable-shell-encoding.md` when working in PowerShell, Windows terminals, or any environment with encoding risk.

## Standard workflow

1. Inspect repository state.
2. Determine whether the user wants:
   - suggestions only
   - commit only
   - commit + push
   - commit + push + PR
   - tag + release
   - release notes / changelog update attached to a GitHub release
3. Detect the host / CLI path:
   - GitHub -> `gh`
   - GitLab -> `glab`
   - Azure DevOps -> `az repos`
   - Gitea / Forgejo / Codeberg -> `tea` if available, otherwise web fallback
   - Bitbucket -> `git` + REST API / web fallback
4. Choose output language:
   - user requested Chinese -> `zh`
   - user requested English -> `en`
   - otherwise inspect recent commits and follow repo convention
   - if encoding is risky -> force `en` ASCII-safe mode
5. If the working tree contains unrelated changes, stage only the requested files:

```bash
git add path/to/file1 path/to/file2

# If only part of a file should be committed
git add -p path/to/file
```

6. Choose one title style for the task:
   - default -> gitmoji + Conventional Commit
   - if the user explicitly requests no emoji / ASCII-only -> plain Conventional Commit
   - if encoding is unsafe -> keep ASCII-only Conventional Commit output
7. Reuse that style consistently for commit titles and PR titles unless the user explicitly wants a different style.
8. Write the title in one of these formats:

Default:

```text
<emoji> <type>[optional scope]: <description>
```

No-emoji / ASCII-safe mode on explicit request:

```text
type[optional scope]: <description>
```

Examples:

- `feat(schema-editor): simplify nested category editing`
- `feat(schema-editor): 优化分类编辑体验`
- `fix(sidebar): remove harsh background corner`
- `fix(sidebar): 修复侧边栏直角背景问题`
- `✨ feat(schema-editor): simplify nested category editing`
- `🐛 fix(sidebar): remove harsh background corner`
- `🔒️ fix(auth): harden token verification`
- `👷 ci(actions): refresh release workflow actions`

8. Create the commit.

Single-line:

```bash
git commit -m "✨ feat(scope): short summary"
```

Multi-line:

```bash
git commit -m "$(cat <<'EOF'
✨ feat(scope): short summary

- bullet 1
- bullet 2
EOF
)"
```

9. Push only if requested and safe:

```bash
git push origin $(git branch --show-current)
```

10. If PR or release work is requested, switch to the host-specific reference and use explicit title/body/notes files rather than vague autogenerated text when the user wants polished output.

## State-specific handling

### 1. Nothing to commit

If `git status --short` is empty:

- do not stage anything
- tell the user there are no changes to commit
- optionally offer 2-3 example commit titles if they only wanted a format

### 2. Untracked-only changes

If the tree only contains `??` files:

- review whether they are intended
- watch for generated files, secrets, archives, or local-only files
- stage only the requested files explicitly

### 3. Mixed staged + unstaged changes

If both staged and unstaged changes exist:

- inspect `git diff --staged`
- inspect `git diff`
- avoid accidentally committing unstaged unrelated work
- if the user wants only the staged work committed, commit staged contents only
- if the user wants a combined commit, stage the remaining intended files explicitly

### 4. Detached HEAD

If `git branch --show-current` is empty:

- do not push automatically
- explain that the repo is in detached HEAD state
- commit only if the user explicitly wants a local detached commit
- otherwise recommend checking out a branch first

### 5. Merge in progress

If `.git/MERGE_HEAD` exists:

- do not invent a normal feature/fix commit blindly
- inspect status and merge result
- if the user wants to finish the merge, use a merge-resolution style message only when appropriate
- do not use amend/revert flows here unless explicitly requested

### 6. Cherry-pick in progress

If `.git/CHERRY_PICK_HEAD` exists:

- treat this as completing a cherry-pick, not a normal clean-room commit
- do not push automatically unless the user requests it

### 7. Rebase in progress

If `.git/rebase-merge` or `.git/rebase-apply` exists:

- treat this as continuing a rebase, not a normal standalone commit
- resolve conflicts first if any exist
- stage resolved files explicitly
- prefer `git rebase --continue` instead of inventing a fresh commit flow
- do not push until the rebase is fully complete and the user requests it

### 8. Unmerged paths / conflicts

If `git diff --name-only --diff-filter=U` returns files or status shows conflict entries such as `UU`, `AA`, or `DD`:

- do not create a normal commit yet
- resolve conflicts first
- stage only resolved files
- continue the merge / rebase / cherry-pick flow that is already in progress

### 9. Initial commit

If there is no `HEAD` yet:

- do not assume amend/revert workflows are available
- verify only intended bootstrap files are staged
- use a clear initial-style message only when it matches the actual diff
- do not push automatically unless the user explicitly asks

### 10. Hook failure

If `git commit` fails because of hooks:

- do not use `--no-verify`
- read the hook output
- fix the issue if possible
- re-run commit normally
- only bypass hooks if the user explicitly asks

### 11. Amend

If the user explicitly asks to amend:

```bash
git commit --amend -m "📝 docs(scope): refined summary"
```

Rules:

- use amend only when explicitly requested
- do not amend already-pushed commits unless the user explicitly asks and understands push implications

### 12. Revert

If the user explicitly asks to revert a commit:

```bash
git revert <commit>
```

Rules:

- do not use reset-based reverts unless explicitly requested
- prefer `git revert` for shared history

### 13. Push rejected / protected branch

If `git push` is rejected because of remote updates, missing permissions, or branch protection:

- surface the exact error to the user
- do not retry with force
- recommend the safe next step such as pull/rebase, opening a PR, or checking permissions

## Push checks

Before pushing, check upstream status:

```bash
branch="$(git branch --show-current)"
upstream="$(git rev-parse --abbrev-ref --symbolic-full-name @{upstream} 2>/dev/null || true)"
if [ -n "$upstream" ]; then
  git rev-list --left-right --count "$upstream...HEAD"
fi
```

Interpretation:

- no upstream -> ask whether to push with `-u`
- ahead only -> normal push is usually safe
- behind only -> do not push blindly; warn the user first
- ahead and behind -> branch diverged; do not push blindly
- `main` / `master` / protected release branches -> be extra cautious and avoid destructive remediation

If safe and requested:

```bash
git push origin "$(git branch --show-current)"
```

If no upstream and safe:

```bash
git push -u origin "$(git branch --show-current)"
```

## GitHub workflow via gh CLI

Use `references/gh-pr-release-flow.md` for exact commands.

Rules:

- Prefer explicit `--title` and `--body` / `--body-file` for PRs.
- Prefer explicit `--notes-file` for releases when the user wants a full curated changelog.
- Do **not** rely on autogenerated compare-range style notes when the user explicitly wants complete release notes.
- Avoid `gh pr create --fill` unless the user explicitly wants commit-derived PR text.
- Be careful with `gh pr create --dry-run`; it may still push branch changes.
- For releases with assets, prefer labeled uploads such as `dist/app.zip#Windows build`.
- If `gh auth status` fails, stop and report the auth prerequisite instead of guessing.

## Split-commit guidance

If the working tree clearly contains multiple unrelated changes:

- recommend splitting into separate commits
- stage subsets explicitly
- use `git add -p` when one file contains multiple logical changes
- do not auto-stage everything by default

Example:

```bash
git add src/ui/*
git commit -m "🎨 style(ui): refine sidebar visual hierarchy"

git add .github/workflows/*
git commit -m "🔧 ci(actions): refresh workflow action versions"
```

## Commit writing rules

- Keep the title under 72 characters when possible.
- Use present tense and imperative mood.
- Prefer user-visible summaries over implementation trivia.
- In default mode, use `type(scope): summary`.
- In emoji mode, use `<emoji> <type>[scope]: <summary>` only when the user explicitly asks for gitmoji / emoji output.
- In Chinese mode, keep the type token in English and write the summary in Chinese.
- Good Chinese default example: `feat(editor): 优化分类编辑交互`
- Good English default example: `feat(editor): simplify category editing flow`
- Good Chinese emoji example: `✨ feat(editor): 优化分类编辑交互`
- Good English emoji example: `✨ feat(editor): simplify category editing flow`
- Use scope when it improves clarity.
- Use `!` and a `BREAKING CHANGE:` footer only when the diff truly introduces a breaking change.
- If the user only wants suggestions, provide 2-3 candidate titles instead of committing.

## Quick decision guide

Default output is Conventional Commit. Use `references/gitmoji-map.md` when the user explicitly wants emoji / gitmoji output.

- Maximum compatibility -> no emoji, use `feat/fix/docs/...`
- New feature -> `feat`, optional emoji `✨`
- Standard bug fix -> `fix`, optional emoji `🐛`
- Critical hotfix -> `fix`, optional emoji `🚑️`
- Docs -> `docs`, optional emoji `📝`
- Refactor -> `refactor`, optional emoji `♻️`
- Performance -> `perf`, optional emoji `⚡️`
- Tests -> `test`, optional emoji `✅` or `🧪`
- CI / workflows -> `ci`, optional emoji `👷` or `💚`
- Dependencies -> `build` / `chore`, optional emoji `⬆️` `⬇️` `➕` `➖` `📌`
- Security / privacy fix -> `fix`, optional emoji `🔒️`
- Move / rename -> `refactor` / `chore`, optional emoji `🚚`
- Breaking change -> use `!` / `BREAKING CHANGE:`, optional emoji `💥`
- Accessibility -> `feat` / `fix`, optional emoji `♿️`
- Validation -> `fix` / `feat`, optional emoji `🦺`

## Suggestion mode

If the user asks for suggestions only:

- when language is specified, return candidates only in that language
- when language is not specified, it is acceptable to return paired candidates such as:
  - EN: `✨ feat(editor): simplify nested category editing`
  - ZH: `✨ feat(editor): 优化嵌套分类编辑体验`

## Deliverables

Depending on the request, provide one of:

1. **Commit suggestions only**
   - 2-3 candidate titles
2. **Commit executed**
   - exact commit message used
   - files staged
3. **Commit + push executed**
   - commit hash
   - target branch
   - whether upstream existed
4. **Commit + PR executed**
   - commit hash
   - branch
   - PR URL / number
   - whether PR was draft or ready
5. **Release / changelog executed**
   - tag
   - release title
   - uploaded assets
   - whether notes were manual or generated
   - host platform / CLI used
6. **Commit blocked for safety**
   - detected repository state
   - exact reason commit/push was not executed
   - safe next steps

## Validation checklist

Before finishing, confirm:

- only intended files were staged
- no secrets were included
- no unresolved conflicts were left
- no AI attribution trailers or banners were added unless explicitly requested
- output was ASCII-safe or UTF-8 was explicitly confirmed
- no mojibake / garbled characters appeared in commit, PR, or release text
- commit title matches the actual diff
- emoji and type are aligned
- unusual repo state was handled correctly
- push happened only if requested
- host-specific CLI was used only when installed and authenticated
- manual notes were used when the user requested full changelog quality
- push was not attempted blindly on detached, behind, or diverged branches
