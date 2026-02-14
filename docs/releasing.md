# Releasing

Quick, repeatable release checklist. Mirrors gifgrep cadence.

## Before

- Update `CHANGELOG.md` for the new version.
- Run gate: `./scripts/check-coverage.sh` + `golangci-lint run ./...`.
- Ensure `main` is clean and pushed.
- Ensure `gh` is authenticated for `steipete/goplaces` + `steipete/homebrew-tap`.

## Tag + Build

```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

GitHub Actions runs GoReleaser build on tag push (`.github/workflows/release.yml`).
Artifacts are stored on the workflow run.

## Publish GitHub Release

Create a release from the tag and upload built archives (`goplaces_<version>_<os>_<arch>.tar.gz|zip`):

```bash
gh release create vX.Y.Z ./dist-archives/* --repo steipete/goplaces --title vX.Y.Z --notes-file /tmp/release-notes.md
```

Homebrew update: see `docs/releasing-homebrew.md`.

## Notes

- CLI version set via ldflags in `.goreleaser.yml`:
  `-X github.com/steipete/goplaces/internal/cli.Version={{.Version}}`
- Local smoke build: `make goplaces`
