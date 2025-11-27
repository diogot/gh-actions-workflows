# gh-actions-workflows

Reusable GitHub Actions and workflows.

## Actions

### create-release

Create a GitHub release using the native `gh` CLI. A secure alternative to third-party release actions.

#### Usage

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    body-file: release_notes.md
    files: |
      dist/*.tar.gz
      dist/*.sha256
```

#### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `tag` | no | `${{ github.ref_name }}` | Tag name for the release |
| `title` | no | Tag name | Release title |
| `body` | no | | Release notes (inline) |
| `body-file` | no | | Path to release notes file |
| `files` | no | | Newline-separated glob patterns for assets |
| `draft` | no | `false` | Create as draft |
| `prerelease` | no | `false` | Mark as prerelease |
| `latest` | no | `true` | Mark as latest release |
| `token` | **yes** | | GitHub token for authentication |

#### Examples

**Simple release with notes file:**

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    body-file: CHANGELOG.md
```

**Release with inline notes:**

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    body: |
      ## What's New
      - Feature A
      - Bug fix B
```

**Release with binary assets:**

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    body-file: release_notes.md
    files: |
      dist/*.tar.gz
      dist/*.sha256
```

**Draft prerelease:**

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    body-file: release_notes.md
    draft: true
    prerelease: true
```

#### Permissions

The workflow requires write access to create releases:

```yaml
permissions:
  contents: write
```

## License

MIT
