# AngelaBox Clash 内核

本分支是 AngelaBox Clash 的内核跟踪分支，不是另一个协议栈。

| 项 | 值 |
|---|---|
| 产品名 | AngelaBox Clash |
| 分支 | `chain-dev` |
| 当前基线 | 官方 tag `v1.19.30`（`ac017cdd246ce8bd547653d927e7bf77d7ee73d5`） |
| 本分支型号 | `v1.19.30-chain.1` |
| 跟踪上游 | [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo) 分支 **`Alpha`** |
| 客户端 | [dukangalex/ClashMetaForAndroid](https://github.com/dukangalex/ClashMetaForAndroid) 分支 `dev` |
| 姐妹产品 | [dukangalex/AngelaBox](https://github.com/dukangalex/AngelaBox)（sing-box，内核不等价） |

对外产品名是 **AngelaBox Clash**。下游产品名不得包含 `mihomo`。仓库名保留是因为这是上游仓库的 fork，便于对照，不作为产品名。

## 不要合并 `main`

上游和本 fork 的 `main` 都不是 Clash 内核（那是另一份同名 Python 仓库的默认分支）。内核历史在 `Alpha`。

- 只从 `upstream/Alpha` merge 进 `chain-dev`
- 禁止把 `main` merge 进 `chain-dev`
- 不改写 git 历史
- 只解决与链式覆盖层、本文件、`Makefile` 里 `chain-dev` 版本行相关的冲突
- 客户端尚未验证的官方提交先不要推进子模块

```bash
git remote add upstream https://github.com/MetaCubeX/mihomo.git
git fetch upstream Alpha
git checkout chain-dev
git merge upstream/Alpha
```

官方 `Alpha` 在本基线之后还有提交。按 AngelaBox 的规则，先验证 Android 客户端能编过、链式覆盖没有静默落到 DIRECT，再把那些提交合进来。

## 构建时的版本号

在 `chain-dev` 上，`make` 用 `git describe --tags` 作为 `constant.Version`。打在本分支上的 tag 形如 `v1.19.30-chain.1`。Go module 路径仍是 `github.com/metacubex/mihomo`，不改，否则 Android JNI 对不上。
