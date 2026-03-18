# Platform Host Matrix

Use this file to choose the correct code-host workflow from the repository remote URL.

## Host detection

Inspect:

```bash
git remote -v
git remote get-url origin
```

Common patterns:

- GitHub -> `github.com`
- GitLab -> `gitlab.com` or self-managed GitLab domain
- Azure DevOps -> `dev.azure.com` or `visualstudio.com`
- Gitea / Forgejo / Codeberg -> host-specific URL; Codeberg is Forgejo-based
- Bitbucket Cloud -> `bitbucket.org`

## Recommended CLI by host

### GitHub

- Preferred CLI: `gh`
- PR: `gh pr create`
- Release: `gh release create`
- Notes: prefer explicit `--body-file` / `--notes-file`

### GitLab

- Preferred CLI: `glab`
- Merge request: `glab mr create`
- Release: `glab release create`
- Notes: prefer explicit file-based notes when available

### Azure DevOps

- Preferred CLI: `az repos`
- Pull request: `az repos pr create`
- Work items can be linked during creation
- Release entities are not a direct Azure Repos equivalent; treat tags, artifacts, and pipeline/release processes separately

### Gitea / Forgejo / Codeberg

- Preferred CLI: `tea` when installed and supported by the host
- Official Gitea sources describe `tea` as a CLI for pulls, issues, and releases
- If `tea` is unavailable, fall back to `git push` plus the web UI

### Bitbucket Cloud

- Use `git` for branch / tag / push operations
- For automation, use Bitbucket Cloud REST API or web UI
- Use app passwords / tokens or other supported auth for API automation
- Do not assume a first-party CLI equivalent to `gh` / `glab`

## Safe fallback

If no host-specific CLI is available:

1. create the local commit safely
2. push the branch with `git`
3. generate a ready-to-paste PR / MR / release title and body
4. tell the user which web page or API flow to use next
