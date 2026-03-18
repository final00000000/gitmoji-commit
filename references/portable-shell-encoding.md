# Portable Shell and Encoding Rules

Use this file when the environment is Windows, PowerShell, mixed shells, or any terminal where emoji or non-ASCII text may render poorly.

## Default output mode

Use **ASCII-only** by default for:

- commit titles
- PR / MR titles
- release titles
- temporary filenames
- generated changelog headings

Examples:

- `feat(ui): refine sidebar layout`
- `fix(release): publish full changelog notes`

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

- Portable default: `type(scope): summary`
- Emoji mode: `<emoji> type(scope): summary`
- Chinese mode: `<emoji> type(scope): 中文描述`
- If the host UI, CI logs, or terminal output are uncertain, use the portable default
