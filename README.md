# t3code-zh-build

Builds and publishes [jieyuexing/t3code-zh](https://github.com/jieyuexing/t3code-zh) on GitHub-hosted runners.

The fork keeps GitHub Actions disabled, because enabling them would also run every upstream workflow it inherits. This repository holds only the build workflow and checks out the fork at the commit you give it.

## What `build.yml` does

| Job | Runner | Output |
| --- | --- | --- |
| `dmg` | macos-15 | `T3-Code-V-arm64.dmg`, audited read-only |
| `archives` | ubuntu-24.04 | `t3-V-linux-x64.tar.gz` and `t3-V-win32-x64.zip`, Linux smoke |
| `windows-smoke` | windows-2025 | Windows CLI smoke receipt |
| `publish` | ubuntu-24.04 | `zh-vV` Release on the fork via `scripts/release-desktop-zh.mjs` |

The publisher re-checks every candidate and receipt against a clean checkout, and the commit must equal `origin/zh-i18n`. With `publish` off it only does a dry run. Artifacts are kept for 7 days.

The Windows NSIS installer is not built. Packages are unsigned, so macOS and Windows ask for confirmation the first time they open.

## Run

```sh
gh workflow run build.yml -R jieyuexing/t3code-zh-build \
  -f commit=<zh-i18n SHA> -f nightly_tag=<v…-nightly.…> -f publish=true
```

Publishing uses the repository secret `T3CODE_ZH_RELEASE_TOKEN`, a fine-grained token limited to `jieyuexing/t3code-zh` with Contents read and write. When it expires the `publish` job fails with a 401; replace it with `gh secret set T3CODE_ZH_RELEASE_TOKEN -R jieyuexing/t3code-zh-build`.
