# gitmoji-commit

Portable git commit / PR / release skill with a full gitmoji catalog, Conventional Commits by default, Chinese or English commit text, and no AI co-author trailers by default.

[简体中文说明 / Chinese README](./README.zh-CN.md)

## Install

```bash
npx skills add final00000000/gitmoji-commit
```

## What this skill does

This is a **commit-first** skill.
Its default job is to inspect the repository state, stage only the intended files, and propose or create a safe Conventional Commit.
PR / release workflows are secondary extensions built on top of that commit-first behavior.

## Default behavior

- Default output: plain Conventional Commit, e.g. `feat(scope): summary`
- If you explicitly ask for gitmoji / emoji: `✨ feat(scope): summary`
- If shell / terminal / encoding safety is uncertain: ASCII-only Conventional Commit output
- Commit and PR titles should keep the same chosen style unless you explicitly ask for a different style

## Trigger rules

The skill should stay in plain Conventional Commit mode unless you explicitly ask for:
- `gitmoji`
- `emoji`
- `icon`
- `带图标`

Requests like "make it prettier" or "make it nice" should not automatically enable emoji mode.

## What it checks before acting

- repository state (`git status --short`)
- staged vs unstaged diff
- whether only intended files are being staged
- whether secrets or credentials are present
- whether the repo is in an unusual state such as merge / rebase / conflict
- whether host / encoding conditions are safe enough for emoji or non-ASCII output

## Usage

`gitmoji-commit` is a portable Git workflow skill for AI agents.
It is **not a standalone CLI command** and is intended to be invoked
in chat by agents that support skills, such as Codex or Claude Code.

You can:

- explicitly mention `gitmoji-commit` in your prompt
- let agents such as **Codex / Claude Code** call the skill

```text
Please use gitmoji-commit, inspect the current changes, and suggest 3 suitable commit titles.
```

```text
Please use gitmoji-commit, stage only the relevant files, create a Chinese gitmoji commit, and commit without pushing.
```

## Common prompt patterns

- Suggest commit titles only
- Commit the staged changes safely
- Commit only the docs change
- Create a Chinese Conventional Commit
- Create a gitmoji commit explicitly
- Commit and push
- Prepare a PR after commit

## Verified / intended environments

Primary validated path:
- local git workflows
- GitHub through `gh`

Intended / guidance-only paths until explicitly validated:
- GitLab through `glab`
- Azure DevOps through `az repos`
- Gitea / Forgejo / Codeberg through `tea`
- Bitbucket through git + web/API fallback

Designed for skill-capable hosts such as Claude Code and Codex CLI.
Current repository examples are verified as a portable workflow spec, but full launch readiness still depends on host-runtime validation across shell and encoding scenarios.

## Known limitations

- This repository is a skill spec, not a standalone CLI.
- POSIX and PowerShell examples are both documented, but host/runtime behavior must be validated in real environments.
- Non-GitHub hosts should be treated as guidance-driven until explicitly validated in the launch test matrix.

