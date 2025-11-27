# Plan: Create Release Action

## Goal

Create a composite GitHub Action to replace `softprops/action-gh-release@v2` using the native `gh` CLI.

## Repository Setup

**Repo:** `diogot/gh-actions-workflows`

```
gh-actions-workflows/
├── actions/
│   └── create-release/
│       └── action.yml
├── README.md
└── LICENSE
```

## Composite Action: `create-release`

### Location

`actions/create-release/action.yml`

### Usage

```yaml
- uses: diogot/gh-actions-workflows/actions/create-release@main
  with:
    tag: ${{ github.ref_name }}
    title: "Release ${{ github.ref_name }}"
    body-file: release_notes.md
    files: |
      dist/*.tar.gz
      dist/*.sha256
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `tag` | no | `${{ github.ref_name }}` | Tag name for the release |
| `title` | no | Tag name | Release title |
| `body` | no | `""` | Release notes (inline) |
| `body-file` | no | `""` | Path to release notes file |
| `files` | no | `""` | Newline-separated glob patterns for assets |
| `draft` | no | `false` | Create as draft |
| `prerelease` | no | `false` | Mark as prerelease |
| `latest` | no | `true` | Mark as latest release |

## Security

- Uses `gh release create` (native GitHub CLI)
- No third-party dependencies
- Minimal attack surface
