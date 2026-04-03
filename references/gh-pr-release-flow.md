# GitHub gh PR / Release / Changelog Flow

Use this reference only when the repository remote is GitHub and `gh` is the selected CLI.

## Prerequisites

```bash
gh --version
gh auth status
git remote -v
```

If `gh auth status` fails, stop and report that GitHub CLI authentication is required.
If the remote is not GitHub, go back and use `platform-host-matrix.md` instead.

## No-AI attribution rule

- Do not add `Co-authored-by` for AI tools.
- Do not add `Generated-by`, `AI-assisted`, or similar banners.
- If a wrapper exposes `includeCoAuthoredBy`, keep it `false` unless explicitly requested.

## PR flow

1. Push the branch first if needed:

```bash
git push -u origin "$(git branch --show-current)"
```

2. Prepare a clean PR body file:

```bash
cat > .git/TEMP_PR_BODY.md <<'EOF'
## Summary
- item 1
- item 2

## Testing
- test 1
- test 2
EOF
```

3. Create the PR with explicit text:

```bash
gh pr create \
  --base main \
  --head "$(git branch --show-current)" \
  --title "✨ add token refresh handling" \
  --body-file .git/TEMP_PR_BODY.md
```

Useful options:

- draft PR: `--draft`
- reviewers: `--reviewer user1 --reviewer org/team`
- labels: `--label enhancement --label ui`
- project: `--project "Roadmap"`

Safety notes:

- Prefer explicit `--title` and `--body-file` over `--fill` for polished output.
- `gh pr create --dry-run` may still push changes; do not treat it as side-effect free.
- Use `gh pr checks` after creation if the user wants CI visibility.

## Release + full changelog flow

1. Inspect recent tags:

```bash
git tag --sort=-version:refname | head -n 5
```

2. Create and push the tag if needed:

```bash
git tag -a v1.2.3 -m "v1.2.3"
git push origin v1.2.3
```

3. Write a manual notes file when the user wants a full changelog:

```bash
cat > release-notes.md <<'EOF'
## Highlights
- key highlight

## Added
- item

## Changed
- item

## Fixed
- item

## Refactor / Performance
- item

## Docs / Build / CI
- item
EOF
```

4. Create the release with manual notes:

```bash
gh release create v1.2.3 \
  ./dist/*.zip \
  --title "v1.2.3" \
  --notes-file release-notes.md \
  --latest
```

5. Update notes later if needed:

```bash
gh release edit v1.2.3 --notes-file release-notes.md
```

Useful options:

- fail if no new commits: `--fail-on-no-commits`
- verify remote tag exists already: `--verify-tag`
- prerelease: `--prerelease`
- asset labels: `./dist/app.zip#Windows build`

Rules:

- Prefer `--notes-file` for complete curated release notes.
- Use `--generate-notes` only if the user explicitly wants GitHub auto-generated notes.
- Do not rely on compare-range-only output when the user wants a full update log.
- If release assets are part of the flow, verify paths exist before calling `gh release create`.
