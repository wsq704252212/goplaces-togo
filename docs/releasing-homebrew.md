# goplaces Homebrew Release Playbook

Manual/local tap update from GitHub release assets.

## Prereqs

- Homebrew installed.
- Access to `steipete/homebrew-tap`.

## Release

1) Tag + push: `git tag vX.Y.Z && git push origin vX.Y.Z`
2) GitHub Actions builds binaries (workflow artifacts).
3) Create/publish GitHub release `vX.Y.Z` and upload archives.
4) Update the tap locally:
   - In `../homebrew-tap/Formula/goplaces.rb`, set `version`, `url`, `sha256`.
   - Commit + push in `../homebrew-tap`.

## Verify install

```bash
brew update && brew install steipete/tap/goplaces
```

## Troubleshooting

- CI does not publish GitHub releases or Homebrew automatically.
