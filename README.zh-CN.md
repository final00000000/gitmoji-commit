# gitmoji-commit

支持 git commit / PR / release 的可移植 skill，可选 moji，支持中文或英文提交，默认不添加 AI co-author 信息。

[English README](./README.md)

## 安装

```bash
npx skills add final00000000/gitmoji-commit
```

## 使用方式

`gitmoji-commit` 是一个面向 AI Agent 的可移植 Git 工作流 skill，
用于辅助生成并执行更规范的 **commit / PR / release** 流程。
它**不是独立的 CLI 命令**，而是由支持 skills 的 Agent
（如 Codex、Claude Code）在对话中调用。

你可以：

- 在提示词中**显式指定** `gitmoji-commit`
- 让 **Codex / Claude Code** 等支持 skills 的 Agent 调用该 skill

```text
请使用 gitmoji-commit，检查当前改动后给我 3 个合适的 commit 标题候选。
```

```text
请使用 gitmoji-commit，只提交相关文件，生成中文 gitmoji commit，并直接提交，不要 push。
```

该 skill 会先检查仓库状态、暂存区和 diff，
再按 **Conventional Commits + 可选 gitmoji** 的方式生成提交信息，
默认不附加 AI co-author。
