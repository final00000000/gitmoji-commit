# gitmoji-commit

支持 git commit / PR / release 的可移植 skill，内置全量 gitmoji catalog，默认使用 Conventional Commit，支持中文或英文提交，默认不添加 AI co-author 信息。

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
默认生成 **Conventional Commit 标题**。

当用户明确要求 gitmoji / emoji 输出时，skill 会从 `references/gitmoji-map.md` 的**全量 gitmoji catalog** 中选择最合适的 emoji 并加到标题前面。
如果环境明确无法安全显示 UTF-8，则保持 ASCII-only 的 Conventional Commit 输出。

## 默认输出示例

- `feat(auth): 增加令牌刷新处理`
- `fix(config): 处理工作区路径缺失`
- `refactor(paths): 重命名 skill 引用路径`
- `ci(actions): 更新发布工作流动作`

## Emoji 模式示例

- `✨ feat(auth): 增加令牌刷新处理`
- `🐛 fix(config): 处理工作区路径缺失`
- `🔒️ fix(auth): 加固令牌校验`
