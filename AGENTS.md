# t3code-zh-build — Agent 入口

- 总仓登记 id `t3code-zh-build`；遵守总仓 `projects/personal/AGENTS.md` 与总仓根 `AGENTS.md`。
- 本仓只拥有 `.github/workflows/build.yml` 与说明：在 GitHub 托管 runner 上按给定提交构建、验证 `jieyuexing/t3code-zh` 三平台产物，并按参数发布 Release；构建步骤与发布条件以 `README.md` 为准。
- 不放 fork 源码、i18n 字典或同步流程（归 fork 仓 `i18n/README.md` 与总仓 `projects/README.md`「上游 fork」）。
- `publish=true` 是对外发布；只在 t3code-zh 每日同步流程或用户明确要求时触发。发布令牌只存仓库 secret，不进文件与日志。
