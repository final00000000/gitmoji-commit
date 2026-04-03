# gitmoji-commit

Portable git commit / PR / release skill with a full gitmoji catalog, Conventional Commits by default, Chinese or English commit text, and no AI co-author trailers by default.

[简体中文说明 / Chinese README](./README.zh-CN.md)

## Install

```bash
npx skills add final00000000/gitmoji-commit
```

## Usage

`gitmoji-commit` is a portable Git workflow skill for AI agents.
It helps generate and execute cleaner **commit / PR / release** flows.
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

The skill checks repository state, staging, and diff first,
then generates **Conventional Commit titles by default**.

When a user explicitly asks for gitmoji or emoji output, the skill consults the
**full gitmoji catalog** in `references/gitmoji-map.md` and prepends the most suitable emoji.
If the environment clearly cannot render UTF-8 safely, the skill keeps ASCII-only Conventional Commit output.

## Default output examples

- `feat(auth): add token refresh handling`
- `fix(config): handle missing workspace path`
- `refactor(paths): rename skill references to canonical paths`
- `ci(actions): refresh release workflow actions`

## Emoji mode examples

- `✨ feat(auth): add token refresh handling`
- `🐛 fix(config): handle missing workspace path`
- `🔒️ fix(auth): harden token verification`
