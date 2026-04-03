# Launch Test Matrix

Track validated behavior by host runtime, shell, encoding mode, and workflow.

| Host runtime | Shell | Encoding mode | Workflow | Status | Notes |
|---|---|---|---|---|---|
| Claude Code | Bash / POSIX | ASCII-safe | commit suggestions | pending | |
| Claude Code | Bash / POSIX | emoji explicit | commit suggestions | pending | |
| Claude Code | Bash / POSIX | Chinese | commit suggestions | pending | |
| Claude Code | Bash / POSIX | ASCII fallback | commit suggestions | pending | |
| Codex CLI | Bash / POSIX | ASCII-safe | commit suggestions | pending | |
| Codex CLI | Bash / POSIX | emoji explicit | commit suggestions | pending | |
| Windows host | PowerShell | ASCII-safe | commit / PR guidance | pending | |
| Windows host | PowerShell | UTF-8 safe | gitmoji explicit | pending | |
| GitHub via gh | Bash / POSIX | ASCII-safe | commit + push + PR | partial | Disposable smoke repo path validated |
| GitLab via glab | n/a | n/a | host guidance | pending | Guidance-only until validated |
| Azure DevOps via az repos | n/a | n/a | host guidance | pending | Guidance-only until validated |
| Gitea / Forgejo / Codeberg via tea | n/a | n/a | host guidance | pending | Guidance-only until validated |
| Bitbucket | n/a | n/a | fallback guidance | pending | Guidance-only until validated |
