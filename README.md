# dotfiles

这是一台 macOS 电脑的基础软件清单。它只管理由 Homebrew 安装的命令行工具和桌面 App；不包含终端配置、项目代码、登录状态、密码、token 或 SSH 密钥。

## 新电脑恢复

先安装 Homebrew，然后运行：

```bash
brew bundle --file="$HOME/dotfiles/Brewfile"
```

Homebrew 会安装清单中缺失的软件；已经安装的软件会跳过。

## 检查

检查当前电脑是否已满足清单：

```bash
brew bundle check --no-upgrade --file="$HOME/dotfiles/Brewfile"
```

这项检查只确认软件是否已安装，不要求它们是最新版本。要查看可升级的软件，运行 `brew outdated`。

## 更新清单

安装或移除软件后，先查看变更是否符合预期，再更新 `Brewfile`。可以手动编辑文件，或生成临时快照进行比较：

```bash
brew bundle dump --file=/tmp/Brewfile --force --no-describe
diff -u "$HOME/dotfiles/Brewfile" /tmp/Brewfile
```

确认后，手动将需要保留的项目更新到 `Brewfile`。

## 安全提示

不要运行 `brew bundle cleanup`。该命令会卸载不在此清单中的软件，可能删除临时安装或未记录的工具。

`ollama-app`、`openchamber`、`kabi-discord-cli` 与 `kabi-tg-cli` 已特意排除：它们不会被此清单安装或管理，但本机已有安装不会受到影响。
