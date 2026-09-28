# N2T — Installation and usage options

<p align="center">
  <a href="USAGE.md">English</a> | <a href="USAGE.ko.md">한국어</a> | <a href="USAGE.ja.md">日本語</a> | <a href="USAGE.zh-CN.md">简体中文</a>
</p>

[README](../README.md)

## Skills CLI

Project installation is the default. Run installation commands from the project where you want to use N2T. Add `--global` to use it across projects. Add `--copy` if you prefer copied files instead of symlinks.

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code --global
```

To inspect unpublished local changes, run this from the N2T repository root:

```sh
npx skills add . --list
```

GitHub installation commands use the published repository. Local changes become available through those commands only after they are committed and pushed.

## Manage a Skills CLI installation

Use `npx skills list` to see installed skills, `npx skills update n2t` to update N2T, and `npx skills remove n2t` to remove it. Check the selected scope and agents in the prompts. The manual-copy instructions below apply only to manually installed copies.

## Manual installation and CLI setup

## Getting started

1. Install Codex CLI or Claude Code and sign in.
2. Copy the entire `skills/n2t` folder into your agent's Skill directory.
3. Start the CLI in your working folder and describe your task to N2T.

N2T is a Markdown-based Skill: no server, build step, or Python installation is required. The clone command below requires Git. Generating a guide requires access to your chosen AI service, plus search and page-reading tools for web research.

## 1. Install a CLI

Skip this step if you already use a CLI. These commands run each provider's official installer.

### Codex CLI

Windows PowerShell:

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

macOS / Linux:

```sh
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Open a new terminal after installation, check the version, and follow the first-run sign-in instructions.

```sh
codex --version
codex
```

Sources: [Codex CLI setup](https://learn.chatgpt.com/docs/codex/cli), [Official installer reference](https://learn.chatgpt.com/docs/config-file/environment-variables).

### Claude Code

Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS / Linux / WSL:

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

Open a new terminal after installation, check the version, and follow the first-run sign-in instructions.

```sh
claude --version
claude
```

See the [official Claude Code setup guide](https://code.claude.com/docs/en/setup) for operating system requirements and sign-in options.

## 2. Install N2T

Exit the agent CLI and run these commands in your terminal. If you already have the repository, open its directory and skip cloning.

```sh
git clone https://github.com/0AndWild/N2T.git
cd N2T
```

Copy the entire `skills/n2t` folder. Copying only `SKILL.md` leaves out the HTML guide instructions. Cloning the repository alone does not install the Skill.

### Personal installation: use across local projects

| Agent | Install directory | Invoke in the agent chat |
| --- | --- | --- |
| Codex | `~/.agents/skills/n2t/` | `$n2t describe your task` |
| Claude Code | `~/.claude/skills/n2t/` | `/n2t describe your task` |

`~` means your home directory. If you use both agents, install a copy in each location. These paths follow the [Codex Skill documentation](https://learn.chatgpt.com/docs/build-skills) and [Claude Code Skill documentation](https://code.claude.com/docs/en/skills).

**Windows PowerShell** — Run from the N2T repository root. Choose only one parent-directory assignment for the agent you use.

```powershell
# Codex
$n2tParent = Join-Path $HOME '.agents/skills'
# For Claude Code, use the following line instead.
# $n2tParent = Join-Path $HOME '.claude/skills'

$n2tDestination = Join-Path $n2tParent 'n2t'
if (Test-Path -LiteralPath $n2tDestination) {
    throw "N2T is already installed at: $n2tDestination"
}
New-Item -ItemType Directory -Path $n2tParent -Force | Out-Null
Copy-Item -LiteralPath './skills/n2t' -Destination $n2tDestination -Recurse
Test-Path -LiteralPath (Join-Path $n2tDestination 'SKILL.md')
```

A final result of `True` confirms that the Skill file was copied.

**macOS / Linux / WSL (Bash)** — Run from the N2T repository root. Choose only one parent-directory assignment for the agent you use.

```bash
# Codex
n2t_parent="$HOME/.agents/skills"
# For Claude Code, use the following line instead.
# n2t_parent="$HOME/.claude/skills"

if [ -e "$n2t_parent/n2t" ] || [ -L "$n2t_parent/n2t" ]; then
  printf 'N2T is already installed at: %s\n' "$n2t_parent/n2t"
else
  mkdir -p "$n2t_parent" && cp -R ./skills/n2t "$n2t_parent/n2t"
fi
```

### Install for one project

Instead of a personal installation, copy the whole `skills/n2t` folder into one of these locations under **the project where you want to use N2T**.

| Agent | Final file location inside your project |
| --- | --- |
| Codex | `.agents/skills/n2t/SKILL.md` |
| Claude Code | `.claude/skills/n2t/SKILL.md` |

Choose the scope you need. Installing the same Skill in multiple locations can cause duplicates or select a different copy. Windows and WSL have different home directories; install inside the environment where you run the CLI.

## Updates and troubleshooting

- **Update:** Run `git pull --ff-only` in the source repository, then replace the installed `n2t` folder with the new `skills/n2t` copy. Back up any edits to your installed copy first. Updating the repository does not automatically update a copied installation.
- **Skill not found:** Check that the installation contains `n2t/SKILL.md`, not `n2t/n2t/SKILL.md`, and start a new CLI session. Invoke `$n2t` in Codex or `/n2t` in Claude Code.
- **Search unavailable:** Check the host's web tools and network permissions. Without web access, N2T labels its output as an unverified draft based on the available material.
- **HTML instructions missing:** Make sure `references/html-guide.md` was copied too.
- **CLI command not found:** Open a new terminal and check the PATH guidance in the official installation documentation.
- **Uninstall:** Remove only the `n2t` folder at your chosen installation location. Previously generated HTML guides remain separate.
