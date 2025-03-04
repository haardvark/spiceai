# Spice.ai Release Process

## Release environments

|                     | Production                     | Development                 | Local                         |
| ------------------- | ------------------------------ | --------------------------- | ----------------------------- |
| Short name          | prod                           | dev                         | local                         |
| spiced Docker image | ghcr.io/spiceai/spiceai:latest | ghcr.io/spiceai/spiceai:dev | ghcr.io/spiceai/spiceai:local |
| Spice Rack URL      | https://api.spicerack.org      | https://dev.spicerack.org   | http://localhost:80           |

## Endgame issue

Create an endgame issue with the following content:

```markdown
- [ ] Ensure all outstanding `spiceai` feature PRs are merged
- [ ] Full test pass and update if necessary over README.md (please get screenshots!)
- [ ] Full test pass and update if necessary over Docs (please get screenshots!)
- [ ] Full test pass and update if necessary over new Samples (please get screenshots/videos!)
- [ ] Full test pass and update if necessary over new Quickstarts (please get screenshots/videos!)
- [ ] Merge Docs PRs
- [ ] Merge Registry PRs
- [ ] Merge Samples PRs
- [ ] Merge Quickstarts PRs
- [ ] Merge release notes
- [ ] Update acknowledgements
- [ ] Update data-components-contrib repo with latest tag and reference it in spiceai. See [Components contrib version update](https://github.com/spiceai/spiceai/blob/trunk/docs/RELEASE.md#components-contrib-version-update)
- [ ] Update version using documented process at [docs/RELEASE.md](https://github.com/spiceai/spiceai/blob/trunk/docs/RELEASE.md#version-update)
- [ ] Final test pass on released binaries
- [ ] Reddit announcement to [reddit.com/r/spiceai](https://reddit.com/r/spiceai)
- [ ] Discord announcement to [#announcements](https://discord.gg/zv8ahzZVpf)
- [ ] For major releases, [blog.spiceai.org](https://blog.spiceai.org) announcement
- [ ] For major releases, email announcement

PR reference:
-
```

## Post release

- [ ] Update version to next-highest version with `-rc`

## Version update

- Major and minor updates can drop the patch. I.e. `v0.3` not `v0.3.0`
- Create a PR updating version.txt to remove the `-rc` flag.
  - i.e. `0.1-alpha.4-rc` -> `0.1-alpha.4`
- Ensure the release notes at `docs/release_notes/v{version}.md` already exists (or add to the version bump PR)
- Merge the PR created in step 1. Verify the releases are created appropropriately with the right version tag.
- Create a new PR updating version.txt to bump to the next version with the `-rc` flag.
  - i.e. `0.1-alpha.4` -> `0.1-alpha.5-rc`
- Merge that PR and verify the new RC release is created.

## Components contrib version update

- Tag the latest commit on https://github.com/spiceai/data-components-contrib with the same version as the main `spiceai` repo for this release
- Create a PR in `spiceai` to update the version of `github.com/spiceai/data-components-contrib` to the latest version tag.
  - To update, run `go get -u github.com/spiceai/data-components-contrib@<version tag>` and commit the `go.mod` and `go.sum` changes

## Acknowledgements update

- Run the `generate-acknowledgements` target and commit the result for each in:
  - spiceai
  - quickstarts
  - samples
  - data-components-contrib
