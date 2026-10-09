# Angela Clash 内核

本分支是 Angela Clash 的内核跟踪分支，不是另一个协议栈。

| 项 | 值 |
|---|---|
| 产品名 | Angela Clash |
| 分支 | `chain-dev` |
| 当前基线 | 官方发布标签 `v1.19.32` @ `88dcbf7f1614a67c3b36b848ee3592dfa92ada36`（2026-09-30） |
| 本分支型号 | `v1.19.32-chain.1` |
| 跟踪上游 | [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo) 正式发布标签 |
| 客户端 | [dukangalex/AngelaClash](https://github.com/dukangalex/AngelaClash) 分支 `dev` |
| 姐妹产品 | [dukangalex/AngelaBox](https://github.com/dukangalex/AngelaBox)（sing-box，内核不等价） |

对外产品名是 **Angela Clash**。下游产品名不得包含 `mihomo`。仓库名保留是因为这是上游仓库的 fork，便于对照，不作为产品名。

## 不要合并 `main` 或未发布的 Alpha 提交

上游和本 fork 的 `main` 都不是 Clash 内核（那是另一份同名 Python 仓库的默认分支）。内核历史在上游 `Alpha`，但它可能领先于正式发布标签；本分支按正式 Mihomo 发布标签同步，不自动带入标签之后的 Alpha 预发布提交。

- 只把官方 Mihomo 正式发布标签 merge 进 `chain-dev`
- 禁止把上游或本 fork 的 `main` merge 进 `chain-dev`
- 不改写 git 历史
- 冲突时，只解决与链式覆盖层、本文件、`Makefile` 中 `chain-dev` 版本相关的内容
- 客户端子模块指向本分支的同步提交

本次同步以官方 `v1.19.32`（`88dcbf7`）为准。当前 `Alpha` 已推进到该标签之后的预发布提交，因此不纳入本次更新。

```bash
git remote add upstream https://github.com/MetaCubeX/mihomo.git
git fetch upstream refs/tags/v1.19.32:refs/tags/v1.19.32
git checkout chain-dev
git merge --no-ff v1.19.32
```

## 构建时的版本号

在 `chain-dev` 上，`make` 用 `git describe --tags` 作为 `constant.Version`。本分支标签形如 `v1.19.32-chain.1`。Go module 路径仍是 `github.com/metacubex/mihomo`，不改，否则 Android JNI 对不上。
