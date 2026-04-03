# Portable Shell and Encoding Rules

Use this file when the environment is Windows, PowerShell, mixed shells, or any terminal where emoji or non-ASCII text may render poorly.

## Trusted operating mode summary

When the shell, terminal, or encoding conditions are uncertain:

- default to ASCII-safe Conventional Commit output
- do not assume Bash heredocs or POSIX-only syntax
- prefer English ASCII over risky non-ASCII output
- if emoji or Chinese output garbles once, keep the rest of the task/session in ASCII-safe mode

## Default output mode

Use **ASCII-safe Conventional Commit output** by default for:

- commit titles
- PR / MR titles
- release titles
- temporary filenames
- generated changelog headings

Examples:

- Default: `feat(auth): add token refresh handling`
- Emoji mode: `✨ feat(auth): add token refresh handling`
- Chinese default: `feat(auth): 增加令牌刷新处理`

Switch to emoji mode only if the user explicitly wants it and UTF-8 rendering is clearly correct.
Switch to Chinese text only if the user explicitly wants Chinese or the repo convention is Chinese and UTF-8 rendering is clearly correct.

## Avoid mojibake

- Avoid smart quotes, unusual punctuation, or decorative Unicode in command examples.
- If a terminal garbles `✨` once, stop using emoji in that session.
- Keep temporary file names ASCII-only, such as `release-notes.md` and `.git/TEMP_PR_BODY.md`.

## Shell portability

Prefer simple CLI commands that work unchanged across shells.

When a notes/body file is needed, use the current shell's native file-writing syntax instead of assuming Bash heredocs.

### POSIX shell example

```bash
printf '%s\n' '## Summary' '- item 1' '- item 2' > .git/TEMP_PR_BODY.md
```

### PowerShell example

```powershell
@"
## Summary
- item 1
- item 2
"@ | Set-Content -Path .git/TEMP_PR_BODY.md
```

## Commit title policy

- Default: `type(scope): summary`
- Emoji mode on explicit request: `<emoji> type(scope): summary`
- Chinese mode: `type(scope): 中文描述`
- If the host UI, CI logs, or terminal output are uncertain, use the ASCII-safe default
