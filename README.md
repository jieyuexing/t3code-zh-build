# t3code-zh-build

Builds the unsigned macOS arm64 DMG of [jieyuexing/t3code-zh](https://github.com/jieyuexing/t3code-zh) on GitHub-hosted runners.

The fork keeps GitHub Actions disabled, because enabling them would also run every upstream workflow it inherits. This repository holds only the build workflow and checks out the fork at the commit you give it.

## Run

```sh
gh workflow run build-dmg.yml -R jieyuexing/t3code-zh-build \
  -f commit=<zh-i18n SHA> -f nightly_tag=<v…-nightly.…>
gh run download <run-id> -R jieyuexing/t3code-zh-build
```

The artifact contains the DMG, its `.candidate.json` and the `--audit-dmg` receipt. It is kept for 7 days.

The DMG is not signed, so macOS asks for confirmation the first time it opens.
