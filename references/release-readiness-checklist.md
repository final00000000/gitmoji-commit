# Release Readiness Checklist

Use this checklist before declaring the skill production-ready.

## Contract clarity
- [ ] Default behavior is plain Conventional Commit
- [ ] Emoji mode only activates on explicit request
- [ ] ASCII fallback behavior is clearly documented
- [ ] Commit / PR / release style rules are not contradictory

## Documentation alignment
- [ ] `SKILL.md` matches `README.md`
- [ ] `SKILL.md` matches `README.zh-CN.md`
- [ ] `SKILL.md` matches `agents/openai.yaml`
- [ ] `references/*` do not conflict with the top-level contract

## Validation claims
- [ ] GitHub is identified as the primary validated path
- [ ] Other hosts are labeled guidance-only or fallback-only unless validated
- [ ] Intended host/runtime claims match actual validation evidence

## Fallback behavior
- [ ] Encoding fallback is standardized
- [ ] Host auth / CLI fallback is standardized
- [ ] Unusual git-state fallback is standardized
- [ ] Blocked-mode output is consistent across docs

## Shell trust
- [ ] Bash-only examples are labeled as such
- [ ] PowerShell examples exist where file-writing is needed
- [ ] Windows / mixed-shell safe defaults are documented

## Safety
- [ ] No AI attribution by default
- [ ] No blind staging in mixed worktrees
- [ ] No destructive remediation by default
- [ ] Secret-handling guidance is explicit
