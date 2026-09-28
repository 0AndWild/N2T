# N2T セットアップガイド

<p align="center">
  <a href="USAGE.md">English</a> | <a href="USAGE.ko.md">한국어</a> | <a href="USAGE.ja.md">日本語</a> | <a href="USAGE.zh-CN.md">简体中文</a>
</p>

[N2Tの紹介と使い方に戻る](../README.ja.md)

## Skills CLI

通常は、コマンドを実行したプロジェクトにインストールされます。複数のプロジェクトで使いたい場合は、下の例のように`--global`を付けてください。シンボリックリンクを使えない環境では、`--copy`を付けてファイルをコピーできます。

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code --global
```

手元のスキルが認識されるか確認するには、N2Tリポジトリのルートで次を実行します。

```sh
npx skills add . --list
```

`0AndWild/N2T`を指定すると、GitHub上のファイルが使われます。手元で編集した内容は、コミットしてプッシュするまでインストールに反映されません。

## インストール後の管理

インストール済みの一覧は`npx skills list`、更新は`npx skills update n2t`、削除は`npx skills remove n2t`で行えます。選択画面が表示されたら、対象のプロジェクトやツールを確認してください。

以下では、Skills CLIを使わずにファイルを直接配置する方法を説明します。

## 手動でセットアップする

1. Codex CLIまたはClaude Codeをインストールし、ログインします。
2. `skills/n2t`フォルダー全体を、使用するエージェントのSkillディレクトリにコピーします。
3. 作業フォルダーでCLIを起動し、N2Tに取り組みたい作業を伝えます。

N2TはMarkdownファイルで構成されているため、サーバーの起動やビルドは不要です。Pythonも使いません。以下の手順でリポジトリを取得するにはGitが必要です。また、ガイドの生成には利用するAIサービスへのログインが、Web調査には検索やページ閲覧の機能が必要になります。

## 1. CLIをインストールする

すでにCLIを使っている場合は、次の手順へ進んでください。以下のコマンドは各提供元の公式インストーラーを実行します。

### Codex CLI

Windows PowerShell:

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

macOS / Linux:

```sh
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

インストール後、新しいターミナルでバージョンを確認し、初回起動の案内に従ってログインします。

```sh
codex --version
codex
```

詳しくは、[Codex CLIのセットアップ](https://learn.chatgpt.com/docs/codex/cli)と[公式インストーラーの説明](https://learn.chatgpt.com/docs/config-file/environment-variables)をご覧ください。

### Claude Code

Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS / Linux / WSL:

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

インストール後、新しいターミナルでバージョンを確認し、初回起動の案内に従ってログインします。

```sh
claude --version
claude
```

OS別の動作要件とログイン方法は、[Claude Codeの公式セットアップガイド](https://code.claude.com/docs/en/setup)を参照してください。

## 2. N2Tをインストールする

エージェントのCLIを終了し、通常のターミナルで実行します。リポジトリを取得済みの場合は、そのフォルダーに移動してクローンを省略してください。

```sh
git clone https://github.com/0AndWild/N2T.git
cd N2T
```

`skills/n2t`フォルダー全体をコピーしてください。`SKILL.md`だけではHTMLガイドの作成基準が含まれません。リポジトリをクローンするだけではSkillはインストールされません。

### 複数のプロジェクトで使う場合

| エージェント | インストール先 | エージェントのチャットで呼び出す |
| --- | --- | --- |
| Codex | `~/.agents/skills/n2t/` | `$n2t 取り組みたい作業` |
| Claude Code | `~/.claude/skills/n2t/` | `/n2t 取り組みたい作業` |

`~`はホームディレクトリです。両方のエージェントを使う場合は、それぞれの場所にコピーします。配置先は[CodexのSkillドキュメント](https://learn.chatgpt.com/docs/build-skills)と[Claude CodeのSkillドキュメント](https://code.claude.com/docs/en/skills)に基づいています。

**Windows PowerShell** — N2Tリポジトリのルートで実行します。使うツールに合わせて、コピー先を指定する行を選んでください。CodexとClaude Codeを両方使う場合は、それぞれの設定で一度ずつ実行します。

```powershell
# Codex
$n2tParent = Join-Path $HOME '.agents/skills'
# Claude Codeでは、上の行の代わりに次の行を使います。
# $n2tParent = Join-Path $HOME '.claude/skills'

$n2tDestination = Join-Path $n2tParent 'n2t'
if (Test-Path -LiteralPath $n2tDestination) {
    throw "N2Tはすでにインストールされています: $n2tDestination"
}
New-Item -ItemType Directory -Path $n2tParent -Force | Out-Null
Copy-Item -LiteralPath './skills/n2t' -Destination $n2tDestination -Recurse
Test-Path -LiteralPath (Join-Path $n2tDestination 'SKILL.md')
```

最後に`True`と表示されれば、Skillファイルがコピーされています。

**macOS / Linux / WSL (Bash)** — N2Tリポジトリのルートで実行します。使うツールに合わせて、コピー先を指定する行を選んでください。CodexとClaude Codeを両方使う場合は、それぞれの設定で一度ずつ実行します。

```bash
# Codex
n2t_parent="$HOME/.agents/skills"
# Claude Codeでは、上の行の代わりに次の行を使います。
# n2t_parent="$HOME/.claude/skills"

if [ -e "$n2t_parent/n2t" ] || [ -L "$n2t_parent/n2t" ]; then
  printf 'N2Tはすでにインストールされています: %s\n' "$n2t_parent/n2t"
else
  mkdir -p "$n2t_parent" && cp -R ./skills/n2t "$n2t_parent/n2t"
fi
```

### 特定のプロジェクトだけにインストールする

個人用インストールの代わりに、**N2Tを使いたいプロジェクトのルート**配下に、`skills/n2t`全体をコピーできます。

| エージェント | ファイルの配置先 |
| --- | --- |
| Codex | `.agents/skills/n2t/SKILL.md` |
| Claude Code | `.claude/skills/n2t/SKILL.md` |

複数のプロジェクトで使うか、このプロジェクトだけで使うかに合わせて、配置先を選んでください。両方に置くと一覧が重複したり、意図しない方のファイルが読み込まれたりすることがあります。WindowsとWSLではホームディレクトリが異なります。普段CLIを使っている環境にインストールしてください。

## 更新とトラブルシューティング

- **更新：** 元のリポジトリで`git pull --ff-only`を実行し、インストール済みの`n2t`フォルダーを新しい`skills/n2t`のコピーに置き換えてください。手元で加えた変更は先にバックアップします。リポジトリの更新だけでは、コピーしたインストール先は更新されません。
- **スキルが表示されない：** 配置が`n2t/SKILL.md`であり、`n2t/n2t/SKILL.md`のように二重になっていないか確認して、新しいCLIセッションを開始してください。Codexでは`$n2t`、Claude Codeでは`/n2t`で呼び出します。
- **検索できない：** 実行環境のWebツールとネットワーク権限を確認してください。Webにアクセスできない場合、N2Tは利用可能な資料に基づく未検証の下書きとして出力します。
- **HTMLの作成基準が見つからない：** `references/html-guide.md`もコピーされているか確認してください。
- **`codex`や`claude`が起動しない：** ターミナルを開き直し、公式インストール文書のPATH設定を確認してください。
- **アンインストール：** 選択したインストール先の`n2t`フォルダーだけを削除します。作成済みのHTMLガイドは別に残ります。
