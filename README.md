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

仓库刚刚建立，内容会随着 [LiteMiyu](https://github.com/miyu-agent/litemiyu) 的正式版一起加入。

## 许可证

这个仓库里的模板和脚本以 MIT 许可证发布。
