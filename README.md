# packaging

> <sub>本文档由 Anthropic 的 Claude Fable 5.2 生成。</sub>

这个仓库存放 Miyu 系列程序发布到各个软件源时使用的模板和工作流，例如 AUR 的 `PKGBUILD`。

它和 [miyu-agent/packages](https://github.com/miyu-agent/packages) 不是一回事：`packages` 是 Miyu 软件包的收录目录，这个仓库只管把程序本身发布到系统的软件源。

## 分工

| 内容 | 在哪里 |
|---|---|
| 各平台的压缩包、校验文件、构建出处证明 | 各程序自己的仓库，由它们的发版流程生成，放在 GitHub Release 上 |
| 发布到软件源时使用的模板和工作流 | 这个仓库 |

发布用的密钥只保存在这个仓库的设置里，各程序的源码仓库不保存。

## 目前的内容

| 工作流 | 做什么 | 密钥 |
|---|---|---|
| [`aur.yml`](.github/workflows/aur.yml) | 把 [LiteMiyu](https://github.com/miyu-agent/litemiyu) 的一次发布推到 AUR（包名 `litemiyu-bin`） | `AUR_SSH_PRIVATE_KEY` |
| [`npm.yml`](.github/workflows/npm.yml) | 把 LiteMiyu 的一次发布发到 npm（主包 `litemiyu` 和三个平台包） | `NPM_TOKEN` |

两个工作流都是手动触发，默认只演练，不往外推。它们的做法相同：

1. 从程序的仓库取模板，从它的 GitHub Release 下载压缩包和校验文件，核对哈希和构建出处证明。
2. 填好模板，在不接触密钥的环境里真装一遍、运行一次。
3. 不是演练时，才在另一个只做推送的任务里使用密钥。

模板放在程序自己的仓库里（LiteMiyu 的在它的 `packaging/` 目录），随程序的版本一起改。Homebrew 的配方由 [miyu-agent/homebrew-tap](https://github.com/miyu-agent/homebrew-tap) 自己的工作流更新，那里不需要另外的密钥。

## 发布一个版本

以 `v2026.11.0` 为例：

```bash
# 先演练
gh workflow run aur.yml -R miyu-agent/packaging -f tag=v2026.11.0
gh workflow run npm.yml -R miyu-agent/packaging -f tag=v2026.11.0

# 演练通过以后再真的发布
gh workflow run aur.yml -R miyu-agent/packaging -f tag=v2026.11.0 -f dry_run=false
gh workflow run npm.yml -R miyu-agent/packaging -f tag=v2026.11.0 -f dry_run=false
```

标签对应的 GitHub Release 必须已经公开，草稿下载不到。
