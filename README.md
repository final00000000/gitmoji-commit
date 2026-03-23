# gitmoji-commit

Portable git commit / PR / release skill with optional moji, Chinese or English commit text, and no AI co-author trailers by default.

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
then generates cleaner messages with **Conventional Commits + optional gitmoji**,
without AI co-author trailers by default.
