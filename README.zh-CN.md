# gitmoji-commit

> 默认阅读中文文档。
>
> Need English? Click here: [README.md](./README.md)

支持 git commit / PR / release 的可移植 skill，内置全量 gitmoji catalog，默认使用 Conventional Commit，支持中文或英文提交，默认不添加 AI co-author 信息。

## 安装

```bash
npx skills add final00000000/gitmoji-commit
```

## 这个 skill 是做什么的

这是一个**以 commit 为核心**的 skill。
它默认负责检查仓库状态、只暂存目标文件，并给出或执行安全的 Conventional Commit。
PR / release 相关能力属于建立在 commit-first 之上的扩展工作流。

## 默认行为

- 默认输出：plain Conventional Commit，例如 `feat(scope): summary`
- 明确要求 gitmoji / emoji：`✨ feat(scope): summary`
- shell / terminal / 编码环境不确定：回退到 ASCII-only Conventional Commit
- commit title 与 PR title 默认沿用同一种风格，除非用户明确要求不同

## 触发规则

除非用户明确说出以下触发词，否则保持 plain Conventional Commit：
- `gitmoji`
- `emoji`
- `icon`
- `带图标`

像“好看一点”“prettier”这类模糊描述，不应自动开启 emoji 模式。

## 执行前会检查什么

- 仓库状态（`git status --short`）
- staged / unstaged diff
- 是否只暂存了目标文件
- 是否存在 secrets / credentials
- 是否处于 merge / rebase / conflict 等异常状态
- 当前 host / 编码环境是否足以安全输出 emoji 或非 ASCII 文本

## 使用方式

`gitmoji-commit` 是一个面向 AI Agent 的可移植 Git 工作流 skill。
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

## 常见提示词

- 只要 commit 标题候选
- 安全提交当前 staged 改动
- 只提交 docs 改动
- 生成中文 Conventional Commit
- 明确生成 gitmoji commit
- commit 并 push
- commit 后继续准备 PR

## 已验证 / 目标环境

Primary validated path：
- local git workflows
- 通过 `gh` 的 GitHub 路径

在明确验证之前应视为 guidance / best-effort 的路径：
- 通过 `glab` 的 GitLab
- 通过 `az repos` 的 Azure DevOps
- 通过 `tea` 的 Gitea / Forgejo / Codeberg
- 通过 git + web/API fallback 的 Bitbucket

本 skill 面向 Claude Code、Codex CLI 这类支持 skills 的 host。
当前仓库提供的是可移植 workflow spec，是否达到上线标准仍取决于真实 host runtime、shell、编码场景下的验收结果。

## 已知限制

- 这个仓库是 skill 规范，不是独立 CLI。
- 仓库已同时提供 POSIX 与 PowerShell 示例，但仍需要在真实 runtime 中验证行为一致性。
- 对 GitHub 之外平台的支持，在没有通过完整测试矩阵前，应视为 guidance / best-effort，而不是已验证能力。

