# N2T 详细安装说明

<p align="center">
  <a href="USAGE.md">English</a> | <a href="USAGE.ko.md">한국어</a> | <a href="USAGE.ja.md">日本語</a> | <a href="USAGE.zh-CN.md">简体中文</a>
</p>

[返回项目介绍与使用示例](../README.zh-CN.md)

## Skills CLI

默认情况下，N2T 会安装到运行命令时所在的项目。如果希望在多个项目中使用，可以像下面这样加上 `--global`。不方便使用符号链接时，加上 `--copy` 即可改为复制文件。

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code --global
```

想确认本地的技能文件能否被识别，可以在 N2T 仓库根目录运行：

```sh
npx skills add . --list
```

指定 `0AndWild/N2T` 时，安装的是 GitHub 上的文件。在本地改过的内容，需要提交并推送后才会生效。

## 安装后如何管理

运行 `npx skills list` 查看已安装的技能，`npx skills update n2t` 更新 N2T，`npx skills remove n2t` 卸载。出现选择提示时，确认要操作的项目和工具。

如果不想用 Skills CLI，也可以按下面的方法手动复制文件。

## 手动安装

1. 安装 Codex CLI 或 Claude Code 并登录。
2. 将整个 `skills/n2t` 文件夹复制到对应工具的 Skill 目录。
3. 在工作目录中启动 CLI，向 N2T 描述当前任务。

N2T 由 Markdown 文件组成，不需要启动服务器、编译代码，也不用安装 Python。按下面的方法下载仓库需要 Git。生成指南前，请先登录所用的 AI 服务；要查阅网络资料，还需要允许工具搜索和读取网页。

## 1. 安装 CLI

如果已经安装了 CLI，可以跳到下一步。以下命令会运行各提供方的官方安装脚本。

### Codex CLI

Windows PowerShell:

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

macOS / Linux:

```sh
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

安装后打开新终端，检查版本，并按照首次启动的提示登录。

```sh
codex --version
codex
```

详细说明见 [Codex CLI 安装指南](https://learn.chatgpt.com/docs/codex/cli)和[官方安装脚本说明](https://learn.chatgpt.com/docs/config-file/environment-variables)。

### Claude Code

Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS / Linux / WSL:

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

安装后打开新终端，检查版本，并按照首次启动的提示登录。

```sh
claude --version
claude
```

操作系统要求和登录方式请参阅 [Claude Code 官方安装文档](https://code.claude.com/docs/en/setup)。

## 2. 安装 N2T

退出 AI 工具的 CLI，在普通终端中运行以下命令。如果已下载仓库，进入仓库目录并跳过克隆步骤。

```sh
git clone https://github.com/0AndWild/N2T.git
cd N2T
```

请复制整个 `skills/n2t` 文件夹。只复制 `SKILL.md` 会缺少 HTML 指南的编写要求。仅克隆仓库并不会完成 Skill 安装。

### 在多个项目中使用

| 工具 | 安装位置 | 在工具的对话框中调用 |
| --- | --- | --- |
| Codex | `~/.agents/skills/n2t/` | `$n2t 描述当前任务` |
| Claude Code | `~/.claude/skills/n2t/` | `/n2t 描述当前任务` |

`~` 表示用户主目录。如果同时使用两种工具，请分别安装到对应位置。安装路径依据 [Codex Skill 文档](https://learn.chatgpt.com/docs/build-skills)和 [Claude Code Skill 文档](https://code.claude.com/docs/en/skills)。

**Windows PowerShell** — 在 N2T 仓库根目录运行。根据所用工具选择对应的路径设置。两种工具都要用的话，分别设置路径，各执行一次即可。

```powershell
# Codex
$n2tParent = Join-Path $HOME '.agents/skills'
# 使用 Claude Code 时，用下面这一行替换上一行。
# $n2tParent = Join-Path $HOME '.claude/skills'

$n2tDestination = Join-Path $n2tParent 'n2t'
if (Test-Path -LiteralPath $n2tDestination) {
    throw "此位置已安装 N2T: $n2tDestination"
}
New-Item -ItemType Directory -Path $n2tParent -Force | Out-Null
Copy-Item -LiteralPath './skills/n2t' -Destination $n2tDestination -Recurse
Test-Path -LiteralPath (Join-Path $n2tDestination 'SKILL.md')
```

最后输出 `True` 表示 Skill 文件已复制。

**macOS / Linux / WSL (Bash)** — 在 N2T 仓库根目录运行。根据所用工具选择对应的路径设置。两种工具都要用的话，分别设置路径，各执行一次即可。

```bash
# Codex
n2t_parent="$HOME/.agents/skills"
# 使用 Claude Code 时，用下面这一行替换上一行。
# n2t_parent="$HOME/.claude/skills"

if [ -e "$n2t_parent/n2t" ] || [ -L "$n2t_parent/n2t" ]; then
  printf '此位置已安装 N2T: %s\n' "$n2t_parent/n2t"
else
  mkdir -p "$n2t_parent" && cp -R ./skills/n2t "$n2t_parent/n2t"
fi
```

### 仅为某个项目安装

也可以不做个人安装，而是将整个 `skills/n2t` 文件夹复制到**需要使用 N2T 的项目根目录**下的对应位置。

| 工具 | 文件应放置的位置 |
| --- | --- |
| Codex | `.agents/skills/n2t/SKILL.md` |
| Claude Code | `.claude/skills/n2t/SKILL.md` |

根据实际需要，选择装到用户目录还是某个项目里。同一个技能装在多个位置，可能会重复显示，或读到另一份文件。Windows 和 WSL 的主目录不同，请安装到平时运行 CLI 的那一侧。

## 更新与问题排查

- **更新：** 在源仓库中运行 `git pull --ff-only`，然后用新的 `skills/n2t` 副本替换已安装的 `n2t` 文件夹。如有自行修改，请先备份。更新源仓库不会自动更新复制安装的副本。
- **看不到 N2T 技能：** 确认文件位于 `n2t/SKILL.md`，而不是嵌套的 `n2t/n2t/SKILL.md`，然后启动新的 CLI 会话。在 Codex 中使用 `$n2t`，在 Claude Code 中使用 `/n2t`。
- **无法搜索：** 检查运行环境的网络工具和网络权限。无法访问网络时，N2T 会注明输出是基于现有材料生成的未验证草稿。
- **缺少 HTML 编写要求：** 确认已一并复制 `references/html-guide.md`。
- **运行不了 `codex` 或 `claude`：** 重新打开终端，并查阅官方安装文档中的 PATH 配置说明。
- **卸载：** 仅删除所选安装位置的 `n2t` 文件夹。已生成的 HTML 指南会单独保留。
