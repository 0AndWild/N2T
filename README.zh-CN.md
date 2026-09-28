# N2T — New To This

![N2T — New To This: Just enough knowledge for your next quest.](assets/n2t-banner.png)

<p align="center">
  <a href="README.md">English</a> | <a href="README.ko.md" lang="ko">한국어</a> | <a href="README.ja.md" lang="ja">日本語</a> | <a href="README.zh-CN.md" lang="zh-CN">简体中文</a>
</p>

[![License: MIT](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)](LICENSE)
![Agent Skill](https://img.shields.io/badge/Agent-Skill-8b5cf6?style=flat-square)

> Every expert was a newbie once. You don't need to learn everything. Just enough knowledge for your next quest.

每位专家都曾是新手。我们不可能懂得所有领域的知识，也不必每做一件新事，就先成为那个领域的专家。

但要让 AI 把事情做好，我们仍然需要对想做的东西有一些基本了解：该提出什么要求，哪些条件不能漏，结果是否符合预期。这些判断都离不开领域知识。

这就是开发 N2T 的初衷：**不必学会一切，先弄懂眼前这件事需要的知识。** N2T 是一个开源 AI 技能，会查找陌生领域的核心概念和术语，结合图片、视频与实际案例，整理成 HTML 指南。

比如想用 AI 剪视频，不必先学完整套剪辑技术。知道硬切、叠化和匹配剪辑是什么、各自带来什么感受，就能比“衔接自然一点”更具体地表达想要的效果。

## 这份指南能帮你了解什么

- 开始动手前需要知道的概念和常用术语
- 这些知识在实际业务中怎么用，哪些地方容易弄混
- 值得参考的资料、具体看点和来源链接
- 接下来可以做什么，哪些内容暂时不用学

指南会保存为 HTML 文件，用浏览器就能打开，无需安装专门的阅读软件。

遇到不熟悉的任务时，随时问一次就可以，不用维护学习记录或设置定期提醒。正文支持离线阅读；查看外部图片、视频和链接时可能需要联网。

## 从需要的知识卡片开始

页面顶部是当前任务，下方按**现在必须了解、接下来再看、可以留到以后**分组展示知识卡片。点击卡片，会弹出简短说明和相关图片、视频、网站链接。如果预览中无法点击，请下载 HTML 文件，用浏览器打开。

## 如何选择参考资料

- **图片：** 在弹窗中展示有助于理解概念的参考图片，附上来源和看点。自行绘制的示意图会单独标明；找不到合适且能展示的图片时，会说明原因。
- **视频：** 只链接已确认相关内容可免费观看的视频。付费课程、需要订阅或购买的视频，以及无法确认是否免费的内容，都不收录。
- **网站：** 优先查阅官方文档和实际产品，并说明它们与当前任务的关系。

技能要求检查图片能否显示，并在加载失败时保留来源提示。如果环境不支持搜索或浏览器验证，会说明哪些部分未能确认。

## 通过 Skills CLI 安装

准备好 [Node.js 和 npm](https://nodejs.org/en/download)，就可以运行下面的命令。[Skills CLI](https://github.com/vercel-labs/skills) 通过 `npx` 启动，不用提前单独安装。

在终端运行以下命令，然后按提示选择要使用 N2T 的工具：

```sh
npx skills add 0AndWild/N2T
```

想先看看仓库里有哪些技能，可以只查看列表：

```sh
npx skills add 0AndWild/N2T --list
```

如果 Codex 和 Claude Code 都要用，可以一次装好：

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code
```

如果要在多个项目中使用，在同一命令后加上 `--global`。

Claude Desktop 普通聊天需要另外安装。将整个 `skills/n2t` 文件夹打包为 ZIP，在 Skills 设置中上传并启用。ZIP 内应包含 `n2t/SKILL.md` 及其配套文件。详见 [Claude 官方 Skills 指南](https://support.claude.com/en/articles/12512180-use-skills-in-claude)。

`skills/n2t/SKILL.md` 定义了技能的工作流程，`references/html-guide.md` 则说明了 HTML 指南的编写要求。

需要安装 CLI、指定安装位置或手动复制文件？请查看[详细安装说明](docs/USAGE.zh-CN.md)。

## 使用方法

如果之前已经在对话中说明任务，可以直接说 `$n2t 帮我了解当前任务需要的知识`，不用重复背景，也不必事先知道概念的名称。

进入准备保存指南的文件夹，启动 Codex。加上 `--search`，就可以搜索最新的网页资料：

```sh
codex --search
```

启动后，在 **Codex 的对话框**里这样提问：

```text
$n2t 我想用 AI 剪视频，但不太了解转场。请讲讲硬切、叠化和匹配剪辑有什么区别、分别适合什么时候用，以及怎么向 AI 描述想要的效果。再找一些参考图片和免费视频，整理成简体中文 HTML 指南。
```

使用 Claude Code 时，在工作目录中启动：

```sh
claude
```

在 **Claude Code 的对话框**里，用 `/n2t` 开头即可：

```text
/n2t 我想用 AI 剪视频，但不太了解转场。请讲讲硬切、叠化和匹配剪辑有什么区别、分别适合什么时候用，以及怎么向 AI 描述想要的效果。再找一些参考图片和免费视频，整理成简体中文 HTML 指南。
```

`$n2t` 和 `/n2t` 要在启动 Codex 或 Claude Code 后输入到对话框里，不要直接当作终端命令运行。提问时可以说清楚：要做什么、已经了解多少、希望用什么语言阅读。

换一个领域，也可以这样问：

```text
我在做物流管理看板。入库、出库、库存和交货周期在业务上是什么关系？请讲到足够我设计页面的程度，并把指南保存到 outputs/logistics-guide.html。
```

如果只有一个主题，还看不出你要做什么，N2T 会先问清楚。参考资料会围绕任务挑选；没有查证的内容，也会明确说明。

### 打开生成的指南

如果没有指定路径，指南会保存到当前工作目录的 `outputs/n2t-<quest-slug>.html`。如果运行环境有专门的产物保存规则，则遵循该规则。可以打开完成消息中的链接，或用浏览器直接打开 HTML 文件。

## 更新与问题排查

更新、卸载和其他安装方法请参阅[安装与问题排查](docs/USAGE.zh-CN.md)。

## 仓库结构

```text
N2T/
├── README.md
├── README.ko.md
├── README.ja.md
├── README.zh-CN.md
├── docs/
└── skills/
    └── n2t/
        ├── SKILL.md                 # 两种工具共用的执行指令
        ├── agents/
        │   └── openai.yaml          # Codex 显示信息
        ├── assets/
        │   └── gallery-guide.html
        └── references/
            └── html-guide.md        # HTML 指南编写要求
```

`agents/openai.yaml` 是 Codex 使用的可选元数据。Claude Code 使用相同的 `SKILL.md` 和参考文档，工作流程不依赖 Codex 专用工具。

安装步骤已按 2026-09-28 查阅的官方文档核对。所用工具及其权限会影响能查到的资料和最终生成的内容。

## 许可证

[MIT](LICENSE) — 可自由使用、修改和分发。
