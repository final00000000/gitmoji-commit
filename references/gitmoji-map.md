# Gitmoji Map

Use this as a lightweight mapping table for commit titles.

| Emoji | Type | Use case |
|------|------|----------|
| ✨ | feat | New user-visible feature |
| 🐛 | fix | Bug fix |
| 📝 | docs | Documentation changes |
| 🎨 | style | UI polish / formatting / non-functional visual cleanup |
| ♻️ | refactor | Internal refactor without feature change |
| ⚡ | perf | Performance improvement |
| ✅ | test | Test additions or updates |
| 🔧 | ci | CI, workflow, tooling configuration |
| 🚀 | chore(release) | Version bump or release preparation |
| 🔒 | fix/security | Security-related fix |
| 🔥 | chore / refactor | Remove dead code, obsolete files, cleanup |
| 🚑 | fix | Hotfix / urgent repair |
| 📦 | build | Package / dependency / artifact changes |
| 🌐 | feat / docs | Localization or translation updates |
| 💄 | style | Pure visual polish |

Preferred title pattern:

```text
<emoji> <type>[scope]: <summary>
```

Examples:

- `✨ feat(auth): add token refresh handling`
- `✨ feat(auth): 增加令牌刷新处理`
- `🐛 fix(config): handle missing workspace path`
- `🐛 fix(config): 处理工作区路径缺失`
- `📝 docs(readme): clarify installation steps`
- `📝 docs(readme): 补充安装说明`
- `🚀 chore(release): bump version to 1.2.0`
- `🚀 chore(release): 发布 1.2.0 版本`
