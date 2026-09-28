# N2T — New To This

![N2T — New To This: Just enough knowledge for your next quest.](assets/n2t-banner.png)

<p align="center">
  <a href="README.md">English</a> | <a href="README.ko.md" lang="ko">한국어</a> | <a href="README.ja.md" lang="ja">日本語</a> | <a href="README.zh-CN.md" lang="zh-CN">简体中文</a>
</p>

[![License: MIT](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)](LICENSE)
![Agent Skill](https://img.shields.io/badge/Agent-Skill-8b5cf6?style=flat-square)

> Every expert was a newbie once. You don't need to learn everything. Just enough knowledge for your next quest.

Every expert was a newbie once. We cannot know every field, and we should not have to become experts every time we take on something new.

But working well with AI takes some understanding of what we want to create. We need enough domain knowledge to know what to ask for, which constraints matter, and whether the result is what we intended.

That is why N2T exists: **learn just enough for the task in front of you.** It is an open-source AI Skill that researches unfamiliar concepts and terminology and brings them together in an HTML guide with images, videos, and real-world examples.

If you want to edit a video with AI, you do not need to learn all of video editing first. Understanding cuts, dissolves, and match cuts—and the effect each creates—helps you describe the transition you want more precisely than “make it flow naturally.”

## What you get

- Essential concepts and terminology for your current task
- Connections between concepts, practical examples, and common misconceptions
- Curated references with source links and notes on what to look for
- Actionable next steps and topics you can leave for later
- A standalone HTML file you can open in a browser

Call N2T when you need it and receive a one-off guide. It does not create learning records or recurring reminders automatically. The written guide works offline; external images, videos, and websites may need an internet connection.

## Explore the guide

Your quest stays at the top. Below it, concept cards are grouped into **Essential now**, **Useful next**, and **Can wait**. Select a card to open a short explanation, relevant images, video links, and real websites in a modal. The downloadable HTML works without a server; if an inline preview blocks interactions, open it in your browser.

## How do I ask?

This guide was created with the following prompt:

```text
$n2t I’m editing a video with AI, but I don’t know much about transitions—what should I know to describe the effects I want?
```

### The result

<table>
  <tr>
    <td width="33%" align="center"><a href="assets/examples/n2t-gallery-main.jpg"><img src="assets/examples/n2t-gallery-main.jpg" alt="Concept gallery" width="100%"></a><br><sub>Concept gallery</sub></td>
    <td width="33%" align="center"><a href="assets/examples/n2t-cross-dissolve-detail.jpg"><img src="assets/examples/n2t-cross-dissolve-detail.jpg" alt="Concept detail" width="100%"></a><br><sub>Concept detail</sub></td>
    <td width="33%" align="center"><a href="assets/examples/n2t-ai-prompt-example.jpg"><img src="assets/examples/n2t-ai-prompt-example.jpg" alt="AI prompt & references" width="100%"></a><br><sub>AI prompt & references</sub></td>
  </tr>
</table>

Reference image shown in the screenshot: [A2o dissolve — grm_wnr](https://commons.wikimedia.org/wiki/File:A2o_dissolve.ogv), [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

## How references are selected

- **Images:** Relevant reference images appear inside the modal with attribution and notes on what to notice. Original diagrams are labeled separately. If no suitable image can be displayed, the guide explains why.
- **Videos:** Only videos confirmed to offer the relevant content for free are linked. Paid courses, subscription-only videos, and videos with unverified free access are excluded.
- **Websites:** Official documentation and real products are preferred, with an explanation of how each helps the current task.

The Skill calls for checking image rendering and preserving source links when images fail to load. If research or browser verification is unavailable, it discloses those limits.

## Installation as Skills

Prerequisite: install [Node.js with npm](https://nodejs.org/en/download). Run the open [Skills CLI](https://github.com/vercel-labs/skills) through `npx`; there is no need to install `skills` separately.

Install N2T and choose your agents when prompted:

```sh
npx skills add 0AndWild/N2T
```

List available skills without installing:

```sh
npx skills add 0AndWild/N2T --list
```

Install N2T for both Codex and Claude Code:

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code
```

Add `--global` to the same command to use N2T across projects.

Claude Desktop chat needs a separate installation. ZIP the entire `skills/n2t` folder, upload it in the Skills settings, and enable it. The ZIP should contain `n2t/SKILL.md` and its supporting files. See the [official Claude Skills guide](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

`skills/n2t/SKILL.md` is the standard entrypoint. The Skill loads `references/html-guide.md` when creating an HTML guide.

For CLI setup, global or project installation, manual installation, and troubleshooting, see [Installation and usage options](docs/USAGE.md).

## Usage

If you have already described your task in the conversation, a short request such as `$n2t Help me understand what I need for this task` is enough. You do not need to repeat the context or know the concept names in advance.

Start the CLI in the working folder where you want the guide saved. For live web research in Codex:

```sh
codex --search
```

Enter in the **Codex chat input**:

```text
$n2t I'm editing a video with AI and don't know much about transitions. Explain cuts, dissolves, and match cuts, and when to use each. Include examples of how to describe the transition I want to an AI, plus reference images and free videos, in an English HTML guide.
```

For Claude Code, start it in your working folder:

```sh
claude
```

Enter in the **Claude Code chat input**:

```text
/n2t I'm editing a video with AI and don't know much about transitions. Explain cuts, dissolves, and match cuts, and when to use each. Include examples of how to describe the transition I want to an AI, plus reference images and free videos, in an English HTML guide.
```

`$n2t` and `/n2t` are invocations inside the agent conversation, not shell commands. Include your goal, current knowledge, and preferred language to help focus the guide.

Another task to describe after the invocation:

```text
I need to build a logistics dashboard. Explain how receiving, shipping, inventory, and lead time connect in real operations, with just enough detail to design the screens. Save the guide to outputs/logistics-guide.html.
```

If you provide a topic without a clear task, N2T asks what you want to accomplish first. It selects media for their teaching value and does not claim to have verified inaccessible material.

### Open the result

Unless you specify a path, the guide is saved as `outputs/n2t-<quest-slug>.html` in the current workspace. Host-specific artifact rules take precedence when present. Open the link in the completion message or open the HTML file in your browser.

## Updates and troubleshooting

See [installation and troubleshooting](docs/USAGE.md) for updates, removal, and alternative setups.

## Repository structure

```text
N2T/
├── README.md
├── README.ko.md
├── README.ja.md
├── README.zh-CN.md
├── docs/
└── skills/
    └── n2t/
        ├── SKILL.md                 # Shared instructions for both agents
        ├── agents/
        │   └── openai.yaml          # Codex UI metadata
        ├── assets/
        │   └── gallery-guide.html
        └── references/
            └── html-guide.md        # HTML guide requirements
```

`agents/openai.yaml` provides optional Codex metadata. Claude Code uses the same `SKILL.md` and reference document; the workflow does not depend on Codex-specific tools.

Installation instructions were checked against official documentation on 2026-09-28. Generation quality and available web and media tools depend on your environment.

## License

[MIT](LICENSE) — free to use, modify, and distribute.
